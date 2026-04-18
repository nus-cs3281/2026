### Tool/Technology 1

#### Topic: Windows COM Automation with the PowerPoint API

Aspects learned:

1. What COM is on Windows:
COM (Component Object Model) is a Windows binary standard that allows one program to control another program through exposed interfaces. Microsoft Office apps, including PowerPoint, expose COM objects that can be created and controlled directly.

2. Directly accessing PowerPoint from code:
PowerPoint can be launched and controlled by creating the COM object `PowerPoint.Application`. After that, code can call object members like `Presentations.Open`, `Slides.Add`, and `SaveAs` to automate slide creation and editing.

3. Typical object flow in PowerPoint automation:
`Application -> Presentations -> Presentation -> Slides -> Shapes`
This hierarchy is important because most operations (for example adding text, images, or changing layouts) happen through `Slides` and `Shapes`.

4. Where this is useful:
Windows can typically automate tasks in PowerPoint without much issues however, this approach is not cross-platform and will not work on macOS or Linux. It is best suited for users who are working in a Windows environment and need to automate PowerPoint tasks.



### Tool/Technology 2

#### Topic: AppleScript for Simple Automation (with Limited PowerPoint Access)

Aspects learned:

1. What AppleScript is for:
AppleScript is a macOS automation language designed for simple, human-readable scripting. It is commonly used to automate repetitive desktop tasks across supported Mac applications.

2. AppleScript can automate parts of PowerPoint on macOS:
Microsoft PowerPoint for Mac exposes an AppleScript dictionary, so scripts can do basic operations such as opening presentations, creating slides, and setting some text content.

3. PowerPoint automation through AppleScript is severely limited:
Compared with Windows COM automation, AppleScript support is narrower and less consistent for advanced features. Some operations available in Windows COM are missing, slower, or harder to control in AppleScript.

4. Best use case:
AppleScript is best for lightweight automation workflows on macOS, not for complex or large-scale PowerPoint generation pipelines.



### Tool/Technology 3

#### Topic: Overcoming AppleScript Limits with VBA Macros (`.bas`) and PowerPoint Add-in (`.ppam`) in PowerPoint

Aspects learned:

1. Hybrid automation strategy:
When AppleScript is too limited for advanced PowerPoint operations, a practical workaround is to move complex logic into VBA and use AppleScript only to trigger that macro.

2. Why VBA helps:
VBA has much deeper support for PowerPoint's object model, so it handles complex actions more reliably (for example heavy slide manipulation, shape formatting logic, and batch processing inside a presentation).

3. Typical workflow:
    - Write VBA code in a `.bas` module.
    - Import the module into PowerPoint's VBA project.
    - Save/export the macro project as a PowerPoint add-in (`.ppam`).
    - Use AppleScript to open PowerPoint/presentation and run the VBA macro.

4. Practical benefit:
This keeps a Mac-friendly automation entry point (AppleScript) while still enabling advanced PowerPoint tasks through VBA, which is generally stronger for PPT automation.

Short practical note:
This approach improves capability, but macro security settings and permissions still matter. Ensure trusted macro settings are configured appropriately, and sign macros when required in managed environments.



### Tool/Technology 4

#### Topic: macOS Sandbox Limits and App Groups for Inter-App Communication

Aspects learned:

1. Why communication is restricted on macOS:
Many macOS apps are sandboxed, which means they run with strict file system and system access limits. Because of this isolation, apps generally cannot directly read/write each other's private data or communicate freely.

2. App Groups as a workaround:
To allow controlled data sharing, related apps can be configured with the same App Group entitlement. This gives them access to a shared container directory that both apps can read and write.

3. File-based command passing:
A practical pattern is to exchange commands through text or JSON files in the shared container. One app writes a command payload (for example action type, parameters, timestamp), and another app watches/reads the file and executes the requested action.

4. Why JSON/text is useful:
This method is simple, debuggable, and language-agnostic. It works well for lightweight coordination when direct API calls between sandboxed apps are not possible.



### Tool/Technology 5

#### Topic: macOS Build as an Unsigned DMG for Easier Distribution

Aspects learned:

1. Build output:
This project packages macOS builds as a `.dmg` using Electron Builder, which makes the app easier to distribute and install on macOS.

2. Why signing is not required in this build flow:
The build pipeline is configured to generate a DMG artifact only, without Apple signing or notarization settings such as a developer identity, notarization credentials, or hardened runtime entitlements. Because of that, the build can be produced locally without an Apple Developer certificate.

3. Why macOS users can still use it:
Even though the app is unsigned, macOS users can still open it after download. In many cases they may need to right-click and choose Open, or remove the quarantine attribute before launching.

4. Best use case:
This approach is suitable for internal testing, development builds, and trusted distribution where reducing build friction matters more than a fully notarized release.

Short practical note:
If the app is meant for public release, Apple code signing and notarization are still the better long-term option because they reduce Gatekeeper warnings and improve the install experience.



### Tool/Technology 6

#### Topic: SSML for Fine-Grained Voice Generation Control

Aspects learned:

1. What SSML is:
SSML (Speech Synthesis Markup Language) is a markup format used to control how text-to-speech systems speak text. Instead of sending plain text only, SSML adds instructions for timing, emphasis, pronunciation, and voice style.

2. Why it is useful for voice generation:
SSML gives much finer control over generated speech, making the output sound more natural and easier to understand. It is especially useful when generating narration, assistants, or guided audio where pacing and clarity matter.

3. Common controls:
SSML can adjust speaking rate, pitch, volume, pauses, emphasis, and pronunciation. It can also insert breaks between phrases and help a speech engine read abbreviations, numbers, or special words correctly.

4. Practical value:
This makes it possible to shape the delivery of a voice rather than relying on the default speech style. That is useful when specific words need to stand out, when a sentence needs a pause for readability, or when the speaker should sound more expressive.

Short practical note:
Different speech engines support different SSML tags, so the markup should be tested against the target voice generator to make sure the intended effect is actually supported.

Short note:
Newer TTS systems can also use natural-language prompts to describe tone, which can sound more natural than basic SSML controls, but it is still very expensive right now.



### Tool/Technology 7

#### Topic: AI for Rapid Prototyping and Feature Discovery

Aspects learned:

1. Why AI is useful early:
AI is good for quick prototypes and for identifying the feature set early, because it can help turn ideas into working sketches fast.

2. The main risk:
Without architecture planned from the start, AI-generated code often keeps building on top of what is already there, even if the structure is not good.

3. What to do about it:
It is important to refactor regularly and clean up the code so the prototype does not turn into a messy long-term codebase.

4. Best use case:
This makes AI most useful as a starting point and exploration tool, not as a replacement for proper design and maintenance.

## Knowledge

#### Topic: PowerPoint New Lines and Line Ending Normalization Across OSes

Aspects learned:

1. New line handling can differ by platform:
PowerPoint may treat new lines differently on macOS and other operating systems, so text that looks correct in one environment can appear differently in another.

2. Line endings matter:
Text files can use different line ending styles such as LF or CRLF, and inconsistent endings can affect how text is read, split, or displayed when it is imported into PowerPoint.

3. Why normalization is important:
Normalizing line endings ensures the same text behaves consistently across operating systems, which helps prevent formatting issues and unexpected blank lines.

4. Practical value:
This is especially important when generating slides from external text files or scripts, because consistent line endings make the output more reliable on both Windows and macOS.

Short practical note:
A good workflow is to normalize line endings both before sending text into PowerPoint and when reading it back out, since PowerPoint may rewrite line breaks differently across operating systems.

#### Topic: PUMA Presentation Flow, Punch, and WIIFY

Aspects learned:

1. PUMA as a presentation flow:
PUMA provides a structured way to organise a presentation so the message feels clearer and easier to follow from start to finish.

2. Punch:
The punch is the opening hook that grabs attention quickly and makes the audience want to keep listening.

3. WIIFY:
WIIFY stands for "What's in it for you", which means the presentation should make the audience value obvious and show why the content matters to them.

4. Practical value:
Using PUMA, Punch, and WIIFY together helps make presentations more focused, more engaging, and easier for the audience to connect with.



