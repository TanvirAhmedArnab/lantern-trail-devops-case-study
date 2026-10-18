# Lantern Trail — DevOps Adoption Case Study

An independent learning project applying concepts from IBM's [Introduction to DevOps](https://www.coursera.org/learn/intro-to-devops) on Coursera.

## Overview

This case study explores how a small game team could improve collaboration, shorten feedback loops, and share responsibility for quality and releases. It focuses on a practical adoption plan grounded in the course's introductory concepts.

Lantern Trail and its team are fictional. The project is a proposed process improvement study, not an official course assignment or a report of an implemented DevOps transformation.

## Game Scenario

**Lantern Trail** is a small single-player 2D puzzle game for Windows. Players guide a lantern through obstacles to reach an exit.

The proposed first playable version contains one short level, movement, one puzzle interaction, an exit, and a Restart action. Its purpose is to learn whether players understand the interaction and enjoy solving the puzzle before the team expands the game.

A hypothetical four-person team collectively covers programming, design, art, testing, and release coordination. The game has no online services; release responsibilities concern distributing working builds, maintaining release information, responding to player feedback, and recovering from broken releases.

## Delivery Problems

The scenario assumes that:

- Changes accumulate separately and are integrated late.
- Testing happens near release, allowing misunderstandings to surface late.
- One person prepares releases using steps they remember.
- Player reports reach that person privately, delaying feedback to the team.

The initial focus is **earlier testing and agreement on expected behaviour**. The Restart feature provides a concrete example: the team needs to agree whether restarting resets both the player and the puzzle objects before implementation begins.

## Version 1 Scope

The adoption plan will address:

- Shared ownership, collaboration, and learning from failure.
- Small batches, reviewed contributions, and early player feedback.
- Behaviour Driven Development and Test Driven Development at a conceptual level.
- A proposed integration, verification, release, recovery, and feedback workflow.
- Clearly defined delivery measures and a gradual adoption approach.

Version 1 is a documentation project. Game implementation, pipeline configuration, and cloud deployment are outside its scope. Proposed practices and hypothetical examples will be distinguished from measured results.

## Current Status

The [adoption case study](devops-adoption-plan.md) documents the fictional scenario, current delivery problems, and proposed shared ownership and collaboration practices. Restart connects team practices to possible player impact. Detailed small-change examples, the delivery workflow, measurement definitions, and final review are pending.

The deliverables are this README and the companion case study, which will develop through subsequent revisions.

## Project History

| Date | Milestone |
|---|---|
| October 18, 2026 | Created the repository and documented the scenario, delivery problems, and version 1 scope. |
| October 18, 2026 | Added the scenario and delivery problem analysis, including possible player impact and the Restart example. |
| October 18, 2026 | Proposed collaboration, clear follow-up responsibilities, shared release knowledge, and learning practices linked to the delivery problems. |
