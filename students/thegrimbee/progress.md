## Week 1
- Prepared for the project by ideating on possible tech stacks and researching benefits and drawbacks of each.

## Week 2
- [Adding UI mockup](https://github.com/thegrimbee/git-visualiser/commit/d4b65ec4e4807dcf77d9c4f7a8d947f998dfe634): Played around with Figma Make to come up with UI mockup for the electron app. Set up initial mockup using React (Typescript) and Tailwind CSS.
- [Added Redux](https://github.com/thegrimbee/git-visualiser/pull/1): Added Redux for state management in the electron app. Set up initial state and actions for fetching and storing git data.
- [Clean up Unused Code](https://github.com/thegrimbee/git-visualiser/pull/2): Figma Make generated some unnecessary code and files for the mockup. Cleaned up the codebase by removing unused files and code to keep the project organized and maintainable.

## Week 3
- [Update Graph](https://github.com/thegrimbee/git-visualiser/pull/3): Added pannability and file type checkbox feature to the graph and fixed several bugs such as height and scrolling issues as well as improving graph structure
- [Added Repository Tab](https://github.com/thegrimbee/git-visualiser/pull/4) and [Allowed Reading Git Data](https://github.com/thegrimbee/git-visualiser/pull/5): Implemented repository tab and backend logic to read git data from the local repository.
- [Update Readme](https://github.com/thegrimbee/git-visualiser/pull/6)

## Week 4
- Set up Github Actions for CI/CD to automatically check lint and build when there is a push to main with a tag starting with v.
- [MVP Release](https://github.com/thegrimbee/git-visualiser/releases/tag/v0.1)

## Week 5
- Added features: [Refresh Button](https://github.com/thegrimbee/git-visualiser/pull/13), [Draggable Graph Elements](https://github.com/thegrimbee/git-visualiser/pull/14/), [Tag Object](https://github.com/thegrimbee/git-visualiser/pull/16/)

## Week 6
- Set up [web version](https://github.com/thegrimbee/git-visualiser-web) of the app using similar UI
- Added features: Graph Icons ([Web](https://github.com/thegrimbee/git-visualiser-web/pull/4), [Electron](https://github.com/thegrimbee/git-visualiser/pull/17/)), Updated Commit Icon([Web](https://github.com/thegrimbee/git-visualiser-web/pull/13), [Electron](https://github.com/thegrimbee/git-visualiser/pull/18/)), Update Graph Object Names ([Web](https://github.com/thegrimbee/git-visualiser-web/pull/15), [Electron](https://github.com/thegrimbee/git-visualiser/pull/19/))
- [Added Priority Labels to Issues](https://github.com/thegrimbee/git-visualiser-web/issues/11)

## Recess Week
- Added features: Commit Message ([Web](https://github.com/thegrimbee/git-visualiser-web/pull/16), [Electron](https://github.com/thegrimbee/git-visualiser/pull/20/))
- [Added Samples](https://github.com/thegrimbee/git-visualiser-web/pull/18): Added samples to the web version to illustrate certain scenarios. For example, scenario of file deletion.
- [Fix UI Bug](https://github.com/thegrimbee/git-visualiser-web/pull/21)

## Week 7
- Added features: Commit Diff ([Web](https://github.com/thegrimbee/git-visualiser-web/pull/22), [Electron](https://github.com/thegrimbee/git-visualiser/pull/21/)), [Export JSON](https://github.com/thegrimbee/git-visualiser/pull/22/), [Custom JSON URL](https://github.com/thegrimbee/git-visualiser-web/pull/27)

## Week 8
- Added features: [Custom Url Handling](https://github.com/git-visor/web-app/pull/27), [Export JSON](https://github.com/git-visor/desktop-app/pull/22)

## Week 9
- Update UI: Change Tag Icon ([Web](https://github.com/git-visor/web-app/pull/28), [Electron](https://github.com/git-visor/desktop-app/pull/23)), [Optimised Layout] (https://github.com/git-visor/web-app/pull/30)
- Added features: Show Line by Line Diff in Commit ([Web](https://github.com/git-visor/web-app/pull/29), [Electron](https://github.com/git-visor/desktop-app/pull/24))
- Release [v0.2](https://github.com/git-visor/desktop-app/releases/tag/v0.2-tested)

## Week 10
- Fix Bugs: Fix Filter Objects Bug ([Web](https://github.com/git-visor/web-app/pull/40), [Electron](https://github.com/git-visor/desktop-app/pull/33))
- Fix up codebase: https://github.com/git-visor/desktop-app/pull/28, https://github.com/git-visor/desktop-app/pull/29
- Update UI: Add Icon ([Web](https://github.com/git-visor/web-app/pull/37), [Electron](https://github.com/git-visor/desktop-app/pull/30)), Move Commit Label to Side ([Web](https://github.com/git-visor/web-app/pull/38), [Electron](https://github.com/git-visor/desktop-app/pull/31))
- Added features: Handle Branches ([Web](https://github.com/git-visor/web-app/pull/39), [Electron](https://github.com/git-visor/desktop-app/pull/32))
- [Make Markbind Page for Documentation](https://github.com/git-visor/git-visor.github.io)
- [Add Mac OS Testing on CI/CD](https://github.com/git-visor/desktop-app/pull/35)
- [Move project to git-visor organization](https://github.com/git-visor)

## Week 11
- Clean Up Codebase and Update Readme ([Web](https://github.com/git-visor/web-app/pull/43), [Electron](https://github.com/git-visor/desktop-app/pull/34))
- Added features: [Handle Packed Objects](https://github.com/git-visor/desktop-app/pull/41), Report Bug ([Web](https://github.com/git-visor/web-app/pull/48), [Electron](https://github.com/git-visor/desktop-app/pull/37))
- Release [v1.0.0](https://github.com/git-visor/desktop-app/releases/tag/v1.0)

## Week 12
- Fix Bugs: Fix Filter Objects Count to be Dependent on Branch ([Web](https://github.com/git-visor/web-app/pull/53), [Electron](https://github.com/git-visor/desktop-app/pull/42)), Fix Commit Sort Order to be Based on Parents Instead of Commit Time ([Web](https://github.com/git-visor/web-app/pull/56), [Electron](https://github.com/git-visor/desktop-app/pull/44)), [Fix Load Url Timing Issue] (https://github.com/git-visor/web-app/pull/55)
- Release [v1.0.1](https://github.com/git-visor/desktop-app/releases/tag/v1.0.1)
