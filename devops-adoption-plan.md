# Lantern Trail DevOps Adoption Plan

An independent case study applying concepts from IBM's [Introduction to DevOps](https://www.coursera.org/learn/intro-to-devops) on Coursera.

Lantern Trail, its team, and the situations below are hypothetical. This analysis establishes a starting scenario for a proposed adoption plan; it does not report an implemented game, actual incidents, or measured improvements.

## Scenario and Player Outcome

Lantern Trail is a small single-player 2D puzzle game for Windows. Players guide a lantern through obstacles to reach an exit. The proposed first playable version contains one short level, movement, one puzzle interaction, an exit, and a Restart action.

The first playable version would test whether players understand the interaction and enjoy solving the puzzle enough to want another level. Observing playtests and discussing player feedback would help the team decide whether to refine the interaction or expand the game. A technically working level alone would not establish that it is enjoyable.

A fictional four-person team collectively covers programming, design, art, testing, and release coordination. Individuals may cover more than one responsibility. The game has no online services: maintaining it means distributing working builds, keeping release information accurate, responding to player reports, and recovering when a published build introduces a serious problem.

For players, the intended outcome is a puzzle they can understand, attempt, and restart reliably. For the team, the delivery challenge is to make useful changes available without losing shared understanding or confidence in the published build.

### Running Example of Restart

After moving puzzle objects into an unsuccessful arrangement, a player selects Restart to try the current level again. The intended behaviour for this case study is that both the player and the puzzle objects return to their starting states for that level.

The current-process example assumes that this expectation was not discussed clearly before coding. A developer interprets Restart as resetting the player's position, while the designer expects the puzzle objects to reset as well. Both interpretations can appear reasonable when the requirement is simply "add Restart."

This difference is a misunderstanding about expected behaviour. A coding defect is different: the team might agree that objects must reset, but the implementation could fail to reset one of them. Both can affect players, but their causes need separate investigation.

## Current Delivery Problems

The scenario assumes four working habits that could delay feedback or make releases less dependable. Their consequences are plausible risks to investigate, not measured findings. The first priority is late testing because it exposes the gap between the team's expectations and the player's ability to retry a puzzle.

### Late Testing and Unclear Expectations

**Current behaviour:** Detailed testing and playtesting occur near release, after most planned changes have been combined. Design, programming, and testing perspectives are not consistently brought together when a feature is first discussed.

**Delivery consequence:** The Restart misunderstanding surfaces late. The team must agree on the expected result, revise the implementation, and check the revised behaviour alongside other accumulated changes. Late discovery leaves less time to make and verify that correction. The release may need to wait; rushing the correction could introduce another defect.

**Player impact:** If the incomplete reset reaches a published build, players could remain stuck with puzzle objects in an unusable arrangement even after restarting. That interrupts experimentation and may make the game feel unfair or unreliable. If the team delays publication instead, players wait longer for the intended update.

**Reasoning:** The issue is not that a particular person failed to "test harder." The process allowed different expectations to remain undiscovered. Later sections will consider how shared examples and earlier verification could address that gap.

### Late Integration of Changes

**Current behaviour:** Developers keep changes separate until several features or fixes are ready, then combine them close to release. Integration means bringing those changes together into a shared version of the game.

**Delivery consequence:** A change to how the level stores puzzle-object positions may not fit the Restart logic developed separately. The combined code might have a visible merge conflict, or it might combine successfully while behaving incorrectly. With several changes arriving together, identifying which interaction caused the problem becomes harder.

**Player impact:** A Restart correction may take longer to reach players while the team investigates integration problems. If an incompatible combination escapes verification, previously working puzzle behaviour could break in the next build.

**Reasoning:** Separate work is not automatically harmful. The concern is the long delay before checking whether the changes work together. The team needs evidence about the combined game, not just confidence in each isolated change.

### Release Knowledge Concentrated in One Person

**Current behaviour:** One team member prepares and publishes builds using steps they remember. Other members cannot readily identify or repeat the complete release process when that person is unavailable.

**Delivery consequence:** Even after the Restart correction has been checked, publication can wait for that person. A remembered step may also be missed, such as confirming that the packaged build contains the intended revision. The team could test one version and accidentally distribute another.

**Player impact:** Players might download a build that still contains the Restart problem or wait unnecessarily for a correction that is otherwise ready. Unclear build information could also make it difficult to tell whether they have the fixed version.

**Reasoning:** Release expertise is valuable. The risk comes from essential knowledge and responsibility being concentrated without a dependable way for others to help. This is a shared delivery concern rather than a reason to blame or remove the release specialist.

### Player Feedback Shared Privately

**Current behaviour:** Players send bug reports directly to the person coordinating releases. The reports are not consistently made available to the rest of the team with the affected build and steps needed to reproduce the problem.

**Delivery consequence:** A report that "Restart does not work" may remain disconnected from the developer and designer who understand the feature. They may receive an incomplete summary later, repeat questions already asked, or investigate a different build. The team loses time connecting the player's experience to a reproducible problem.

**Player impact:** Players may have to explain the same issue more than once or wait longer for a useful response. Without clear acknowledgement or correction information, they may not know whether their report has been understood.

**Reasoning:** Direct contact with a player can be helpful. The delivery problem is that relevant information stays with one person instead of informing the people who can investigate and respond together.

### How the Problems Reinforce One Another

The Restart example illustrates a possible sequence:

```text
Unclear reset expectation
    → misunderstanding discovered during late testing
    → correction meets other changes integrated late
    → checked correction waits for release knowledge
    → player feedback reaches only one person
    → team learning is delayed
```

This sequence is an illustrative explanation, not a record of actual events. It shows why examining the whole delivery process matters: improving one step may leave another source of waiting or lost feedback in place.

The next stage of the adoption plan will connect these problems to shared ownership, collaboration, and earlier feedback. Proposed practices, workflow details, and measurement definitions remain to be developed.
