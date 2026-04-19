### GitHub Copilot (and agentic coding in general)
Learning points:
- Provide as much context as possible, using extensions (@), commands (/), and file context (#)
- Keep each chat focused on a relatively small objective
- Agent mode is powerful for complex tasks, and it is also a good investigative tool compared with ask mode, where findings are given as a rich document
- Treat it as a pair programmer; explain and ask questions as you would to a human partner
- It is easy to get lost while changing code since Copilot makes it much easier to debug and try things out quickly, so it is worth taking the time to ask yourself whether any changes should be part of another PR

Additional learning points (updated at Week 13):
- Using the CLI version of GitHub Copilot results in a much better experience, as configuring the MCP server and plugins is easier than using the Copilot extensions. Based on my personal experience, it is also more stable than the JetBrains IDE plugin.
- Compared to Claude, Copilot is more likely to follow our instructions literally.
- Use the right model (or effort in Claude) for the right tasks.
  - For simpler and isolated tasks, e.g. fixing a bug in a specific React component or resolving syntactic issues, small models like Haiku are sufficient and cost-effective.
  - For more involved tasks, like a bug that depends on the interaction between many components, or developing a relatively isolated new feature, e.g. making words in a lyric clickable to show their dictionary meaning, the standard GPT Codex or Claude Sonnet is enough.
  - For a task that involves a lot of reasoning, like planning a greenfield app or a major refactor of a fundamental service, e.g. migrating the JSON library from Gson to Jackson in a Java app or planning a new authentication method like OIDC, it is better to use the best model possible so that we can minimise back-and-forth and reduce the token usage incurred in fixing any incorrect implementation or plan.
- A tip I got from one of the mentors, and from my experience vibe-coding an app, is that if we are implementing something big, we should always ask the agent to output its plan, and possibly a list of to-dos or use cases, into a `.md` file. This allows us to implement each sub-goal in a new conversation by referring the agent to this plan file, minimizing token usage.
- If we are dealing with libraries that are relatively new, it is worth checking whether they have an MCP for their documentation. We can add this MCP server so that the models will consult the latest up-to-date documentation and minimise hallucinations.
- Most models have a tendency to over-comment, both in code comments and in user-facing text. For example, when I am vibe-coding an app, Claude often includes implementation-internal details in some user-facing configurations, which could be a security concern and lead to a poor user experience. Adding an instruction against doing this to the agent's base instructions is quite effective in remedying this issue.

Resources used:
- GitHub website
- Gemini and ChatGPT

### Google Cloud Platform (GCP)
These are some points I learnt when setting up my own GCP project to deploy TEAMMATES to a staging server.
1. Google App Engine is a service which allows us to deploy a project (backend and frontend) with automatic instance scaling depending on the current traffic. We only need to provision the correct instance type, that is, the maximum resources each instance can use, and choose the one that is most cost-effective for our app.
2. Services within GCP (App Engine, Cloud SQL, and Compute Engine (VM)) can be set to communicate through an internal network, a service labelled as Virtual Private Connector (VPC). This is safer and perhaps even more efficient compared to wiring up these services to the public network, as the App Engine communicates with the database and the SOLR VM through their local network, which is not exposed to the public internet.
3. Secrets and environment variables can be configured using the Secret Manager and Parameter Manager services, respectively. This is useful when we want to configure continuous deployment using GitHub Actions.
4. Proper IAM (Identity and Access Management) is required if we are working as a team on a GCP project. There are numerous roles that can be given to each user and service account, and ideally we should provide each account the minimum required to accomplish a task based on the principle of least privilege for security.
5. I realised that perhaps profiling with the expected load might give us an idea of which machine to choose, for example, when choosing which DB service tier to provision. Though, perhaps this is dynamic in nature, depending on user-base growth.

### OpenID Connect Authentication
OIDC is built on top of the OAuth2 protocol. It is a way for an application (called a relying party / RP) to verify the identity of a user. Before doing so, we need to set up a secret key associated with our client ID and the identity provider. Let's use Google as an example in the following workflow.
1. When a user clicks "Login", our backend will redirect the browser to the identity provider's login page. The redirect URL will contain our client ID so that the identity provider can identify the RP. This is where the user will log in to their account with the identity provider using their credentials.
   - This involves a **consent screen**. This basically informs the user what kind of user information the RP can access.
2. Once the user agrees, the identity provider will redirect the browser back to our backend, specifically to the OAuth2 callback endpoint.
   - **OAuth2 callback endpoint**: this is an endpoint that the identity provider will redirect the user to after successful authentication. It contains the authorization code, which we can later exchange for an access token and ID token. This authorization code is often embedded as part of the URL query parameter.
3. Our backend then performs a server-to-server request to the authorization-code exchange endpoint of the identity provider. This request contains the authorization code we get from the callback, our client ID, and client secret. If successful, we will get back an access token. If the protocol supports OIDC, we will also get an ID token.
  - **Access token**: This token grants the RP access to retrieve user information from the user info endpoint (sometimes also called the resource endpoint) of the identity provider.
  - **ID token**: This is essentially a key-value pair that contains various "claims", such as `sub`, indicating the subject, which is the user's ID within the identity provider's system, and `iss`, which is the URL representing the identity provider. This token is signed with the identity provider's private key, which we can verify using their public key.
4. OIDC is better than plain OAuth2 as it allows authentication and authorization in one step (step 3). The public key of the identity provider can be downloaded once and used to verify subsequent ID tokens.
5. The backend can then use these claims about a user's identity to associate it with an account in the system.

Note:
  - To prevent replay attacks, before the backend redirects the browser to the identity provider, it will generate a state, for example, based on the current session_id (a cookie) and next URL. This state will be encrypted. Integrity is ensured by signing the state object using a keyed-hash algorithm or using an encryption algorithm that ensures integrity, such as AES/GCM. The freshness of the session_id protects against replay attacks.

### GitHub Actions
- GitHub Actions is a CI/CD system that allows us to run tasks, such as testing and deployment, upon the occurrence of certain actions such as a push to a pull request or a comment on an issue.
- We specify a `.yaml` file to configure parameters such as when the action should be triggered, the name of the action, whether this is a recurring action, and the steps taken. Each action can comprise several steps such as downloading dependencies, compiling the code, and running tests on the code.
- We can write complicated logic using the official action script plugin. This allows us to use JavaScript to program the actual work being done for a particular step. Using JavaScript improves developer experience too, as inlining the script in a `.yaml` file or using CLI tools like `grep`, `sed`, or `echo` might not be as readable as a JavaScript file.
- We can only configure whether to execute several steps sequentially (required if subsequent steps depend on earlier steps, like compiling the code before testing), or run them in parallel if the steps do not depend on one another.

### JSON Handling in Java
- JSON deserialization in Java involves different deserialization methods depending on the choice of library.
- First, the target deserialization object is constructed. For this step, reflection is used to directly set the values of the object attributes. Other methods include specifying public constructors to use.
- Then, deserialization is recursively performed for each field. For two entities that are linked to one another, it is important to handle this, usually by using annotations for the JSON library to ignore one side of the relationship in order to prevent an infinite recursion problem.
- Polymorphic types, in particular, can be handled in several ways. We can write a custom deserializer to check the value of a specific field to know which subtype of a class to construct, or we can use annotations.
  - In Jackson, we can use the `@JsonTypeInfo` annotation to tell Jackson that a particular field in the serialized entity contains information about the subtype of that entity. The `@JsonSubtypes` annotation can then be used to map the value of the field specified through `@JsonTypeInfo` to the subtype information.
  - Ideally, how we design such a subclass relationship impacts how complicated configuring polymorphic relationships can be. For instance, Jackson insists that all subtype entities contain a specific type information field as specified in the superclass, even if we already know what type the serialized entity should be deserialized into. In the case of TEAMMATES, this is solved by overriding the type information annotations in the subclass, but this is certainly not the most elegant solution.
    - Another solution is to always specify the subtype information in the serialized entity.

### Unit Testing

#### A Common Pitfall
This illustrates a mistake I made in testing, which, according to one of my mentors, is a common pitfall.

The point of performing a test on a component (function / method / class) is to confirm that the component is doing what it is supposed to do. This ensures that any future modifications to this component do not break the contract of the component's behaviour. If any such modification is inadvertently made, the test will fail, which means the tests serve their purpose of alerting the developer that something wrong has been done.

In view of this purpose of testing, we should not be too concerned about white-box testing the code to ensure that the code behaves exactly as it is implemented currently. Doing so may distract us from actually ensuring that the requirement / contract is not broken. Also, this requires us to be careful with how we construct the test.

There was this method that I'm testing. Basically, I'm simply testing whether this method would update the internal state of the class properly, given an input. I got too distracted in verifying the actual behaviour of the code (which may not be important in this case), that is, I tried to verify that this method simply sets the internal state using a reference to an object instead of copying the object. This led me to use `toBe` (which verifies referential equality), which is perfect for this case. However, in this case, I failed to actually test that the component behaves this way. Should someone in the future inadvertently modify the input object in some unexpected way (assuming that this method is simply a setter), the test would still pass since we are comparing the same object!

**Simplified Illustration**
```js
// Method to be tested
set(o) {
  this.o = o;
}

// Test code
const expectedObject = {};
component.set(expectedObject);
expect(component.get()).toBe(expectedObject);

// Test will pass even if setter is modified (accidentally) to:
set(o) {
  this.o = o;
  o.someProperty = null;
}
```

The correct way in this case would be to deep-copy the object we provide as input to the component, and then assert that the object we get is still equal by value to the deep-copied object. This way, when someone accidentally changes something in the input object that is not supposed to be done, the test will fail, and it will save the day for everyone!

If we do not deep-copy the object and provide the expected object as the input, even if we compare with `toEqual`, inadvertent modification to the object will still cause the test to pass, since we are again comparing the same object. We are just checking that all the values from the actual result (the object we get from getting it) are equal to what we provide as input, and both are the same object in memory.

#### Testing Only What Matters

Another practice worth considering is not comparing all properties of the objects when they may not be necessary for the behaviour we are testing. For example, if a method is only concerned with parsing data into a user-friendly form and storing it in a field, we should not test the equality of other fields within the objects in our assertions.

There are a few reasons against doing otherwise.
##### 1. High Maintenance Burden
When a new field is added in the future, the expected objects would have to be updated for the test to work properly, and this would be costly if we have many expected objects for the purpose of test assertions.

##### 2. Noise in Test Output
When an assertion fails, the output would show all the fields of the objects being asserted as well as all the fields of the actual object, resulting in poor debugging and developer experience. Instead of a failure message stating `expected <1> but found <2>`, we see something like
```
expected <{field1: a, field2: b, ...}>
but found <{field1: a, field2: c, ...}>
```
In addition, it also adds noise in the code itself, in that a test that tests one specific behaviour should not concern itself with irrelevant fields.
