# DevBits: User Stories and Use Cases

Senior Design, Assignment 4
Team: Eli Fouts, Riley Boughner

## Stakeholder Map

- **Primary:** Builder. A developer who posts updates about their own project.
- **Secondary:** Reader. A developer who browses, follows, and comments on other people's projects.
- **Hidden:** Community moderator. Nobody needs this role until reports start coming in, and app stores expect a way to act on reports.

## User Stories

**US-01 (primary, Builder)**
As a solo developer working on a side project,
I want to post progress updates to that project,
so that I have a dated log of what I built and my followers can keep up.

**US-02 (secondary, Reader)**
As a developer choosing tools for my own project,
I want to find other projects by technology tag,
so that I can learn from people using the same stack.

**US-03 (hidden, Moderator)**
As a community moderator,
I want to review reported updates and remove the ones that break the rules,
so that abusive content comes down quickly and the app stays within app store rules.

**INVEST check**

| Story | I | N | V | E | S | T |
|---|---|---|---|---|---|---|
| US-01 | yes | yes | yes | yes | yes | yes |
| US-02 | yes | yes | yes | yes | yes | yes |
| US-03 | yes | yes | yes | yes | yes | yes |

None of the stories name a UI element, and each one states a benefit.

## Use Cases

### UC-01: Publish an update (expands US-01)

**Primary actor:** Builder
**Secondary actors:** API server

**Preconditions**
1. The Builder is signed in with a valid session token.
2. The Builder owns at least one Stream.
3. The phone has a network connection.

**Main success flow**
1. Builder opens the new update screen.
2. System shows the Builder's Streams and a text entry area.
3. Builder picks a Stream and types the update.
4. System shows a preview.
5. Builder confirms.
6. System saves the update and shows a confirmation.
7. Builder opens the Stream.
8. System shows the new update at the top of the timeline.

**Alternate flow (image attached)**
At step 3 the Builder also attaches an image. Before showing the preview, the System checks the file type and size and rejects anything over the limit with a message.

**Exception flow (connection drops)**
At step 6 the connection is lost before the System confirms the save. The System shows an error, posts nothing, and keeps the draft. When the Builder retries later, the same draft posts without retyping.

**Postcondition**
The update is saved to the chosen Stream and visible to followers. If publishing failed, nothing is posted and the draft is still on the phone.

## Acceptance Criteria

**AC-01.1** (main flow)
Given a signed-in Builder who owns a Stream and is online,
When they publish an update of 1 to 500 characters to that Stream,
Then a confirmation appears within 5 seconds and the update is the first item in the Stream timeline with the same text.

**AC-01.2** (exception flow)
Given a signed-in Builder who has confirmed an update,
When the connection drops and no confirmation arrives within 15 seconds,
Then an error says the update was not posted, the update does not appear in the timeline, and the draft text is still there when the Builder retries.
