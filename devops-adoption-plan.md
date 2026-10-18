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

## Proposed Shared Ownership and Collaboration

The team would share responsibility for players being able to understand, complete, and restart the puzzle. Completing an individual task would remain useful, but the shared outcome would be a verified change reaching players and the team responding to its consequences.

Shared ownership does not mean everyone performs every job or that nobody is accountable. Each change or reported problem would have a named coordinator who keeps its information current, brings in the relevant expertise, and follows it through. Design, programming, testing, and release responsibilities remain identifiable within the same small team. These are proposed working agreements for the fictional team, not practices already implemented.

### Agree on Behaviour Together Before Coding

For Restart, the person designing the puzzle, the person implementing the change, and someone contributing testing expertise would discuss a concrete example before work begins. They would agree that the player and puzzle objects return to their starting states, identify unclear details, and record the expectation with the change.

This brings testing knowledge into the decision early, addressing late discovery of misunderstandings. Designers clarify player intent; programmers raise implementation questions; testing expertise helps identify observable outcomes and edge cases. One person may cover multiple capabilities. A brief discussion and recorded example are sufficient for this small change; a formal meeting for every edit is unnecessary.

### Make Small Contributions Visible and Review Them

The team would keep the Restart change focused, share it while feedback is still useful, and ask another member to review its behaviour and relevant code before integration. A pull request is a proposed way to keep the change, discussion, and review together. Changes to puzzle-object state would be discussed with the person working on Restart so their assumptions can be checked together.

Smaller contributions give reviewers less unrelated work to understand and can expose incompatible assumptions sooner. The team would also check the combined version; review alone does not establish that integration works. Pairing could help with a difficult reset interaction or knowledge transfer, without requiring two people on every task. Neither review nor pairing guarantees a defect-free release.

### Share Release Knowledge With a Supported Backup

The member with release expertise would document the essential preparation and verification steps, then work through them with a second team member. The record would identify the intended revision, packaged build, checks performed, and published version. Both would update it when the process changes.

For the Restart correction, another member could check that the build intended for players contains the verified fix. This reduces dependence on memory and one person's availability while preserving release expertise. Backup responsibility would include training and appropriate publishing access, rather than assuming an unprepared colleague can release safely. Detailed release and recovery procedures will be developed in the workflow section.

### Keep Player Reports Available to the Team

The person receiving a report would capture the affected build, expected and actual behaviour, reproduction steps, and investigation status in a shared issue. They would omit private player contact details from any public record. A named coordinator would arrange investigation, acknowledge the report through the appropriate channel, and track verification of any correction.

For a report that Restart leaves an obstacle in place, the team could reproduce the situation and compare it with the agreed reset behaviour. Shared information reduces repeated handoffs and helps colleagues contribute directly. Direct player conversations can continue, with relevant findings recorded for the team.

### Learn From Problems Without Blame

After a significant release problem, the team would examine what happened, which information or checks were missing, and what small improvement to try. For Restart, the inquiry could reveal an unclear expectation, an interaction missed during integration, or the wrong build being published. These possibilities call for different responses; the team should investigate before choosing one.

A learning approach encourages people to report concerns promptly. It still requires accountability: name a follow-up owner, record the agreed action, and review whether it helped. The team would avoid rewarding only individual task counts or treating testing and releases as someone else's concern. A separate DevOps handoff team would add another boundary without resolving these ownership problems.

### Connections to the Delivery Problems

| Current problem | Proposed practice | Intended effect to assess |
|---|---|---|
| Late testing and unclear expectations | Joint behaviour discussion and early testing input | Discover disagreements before substantial implementation |
| Late integration | Small reviewed contributions, early coordination, and checks of combined changes | Discover incompatible changes earlier |
| Release knowledge concentrated in one person | Maintained release instructions and a trained backup | Reduce waiting and missed preparation steps |
| Player feedback shared privately | Shared issue record with a named coordinator | Make reports actionable and follow-up visible |

These intended effects are hypotheses, not achieved improvements. The next sections will develop the small-change examples, delivery workflow, and measurement plan used to assess them.
