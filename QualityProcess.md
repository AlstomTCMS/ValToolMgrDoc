# Quality process

## Introduction

### Abstract

This document intends to describe Quality process, on following aspects:
 * how work will be dispatched, 
 * how coordination is done,
 * how and deliveries will be performed.
 
The final intend is to ensure a proper delivery, and moreover ensure that no teams are blocked by others.

### Terminology

	* **Team** : A group of people working together, usually on the same physical place (usually an Alstom site).
	* **CCB** : A meeting to determine what are needs for a specific milestone.
	* **Milestone** : This is a target delivery
	* **Issue** : It is a specific ticket, which describes a modification request.

## Collaborative work

A CCB is organized periodically, in order to discuss which issues should be done by whom for a specific milestone. CCB should determine what is the expected result of this milestone, in order to Teams to anticipate this delivery.

### Workflow

Before CCB:
	1. Define a milestone, by determining needs for the next release;
	2. Each Team review the list of issues which are opened and has not been attributed to any milestone on [Project's issue management tool on Github](https://github.com/AlstomTCMS/ValToolMgr/issues?milestone=none&state=open). 
	3. Each team will determine which issues are wished/mandatory for the next delivery.
	4. List of issues must be reviewed and understandable for everyone.
	5. If possible, a sketch proposal of the tool is prepared and sent by mail.

During CCB:
    1. Open points are discussed, answers to questions are provided.
	2. Delayed issues are taken into account.
	2. CCB determine, based on all Teams and milestone constraints, a list of issues to be done, by whom.
	
After CCB:
	1. Writing of an updated sketch in order to ensure that all sites understand the same thing. 
	2. This sketch is used to validate milestone.

## Issues management

All problems, evolutions requests, questions are written using [Project's issue management tool on Github](https://github.com/AlstomTCMS/ValToolMgr/issues).

### Writing of an anomaly/bug

**Procedure:**
	1. Click on *New Issue* Button;
	1. Add *bug* Label;
	1. Put a relevant *title*. This title has describe precisely enough the problem. A title is relevant enough if we can reliably tell that this title cannot be copied as if for another issue.
	1. Put a relevant *description*. Description should comply with following template : [#65](https://github.com/AlstomTCMS/ValToolMgr/issues/65)

### Writing of an enhancement

**Procedure:**
	1. Click on *New Issue* Button;
	1. Add *enhancement* Label;
	1. Put a relevant *title*. This title has describe precisely enough the enhancement. A title is relevant enough if we can reliably tell that this title cannot be copied as if for another enhancement.
	1. Put a relevant *description*. Description should describe the interest of the modification, explain what is expected.

### Requesting an answer for a specific issue

**Procedure:**
	1. Click on *Issue that you need answer* (For example [#65](https://github.com/AlstomTCMS/ValToolMgr/issues/65));
	1. Add *question* Label;
	1. Go at end of issue, and insert what is your question. Put a relevant *description*, then finish with "?" (because it is a question).

## Modification management

These are mandatory rules:
	* All modifications should be requested by a an issue. 
	* One branch is created for each issue. 
	* The branch merging commit must add following comment on the description of the commit  : "Closes #32"
	* A tag must be created every time you intend to delivery something to someone. It is the only reliable way to track issues efficiently.

## Deliveries management

### Milestone creation

Milestones are used to create what is expected to be delivered in the future, at a particular date, for a specific need.

#### Milestone naming rule

Name of milestone is determined by the version number to be delivered. It is made of a 3 digit number (W.X.Y):
	* **W** : Production release : This version is reviewed by a quality assessor, in order to check that Documentation is updated and reviewed. It is intended to be widely distributed.
	* **X** : Official release : This version is tested, and can be used safely. It can be shared between Teams without troubles.
	* **Y** : unofficial releases : This version is tested, but is mainly used as a step in order to reach an official release. It is used as a synchronization point in order to avoid Teams divergences, and avoid critical merge troubles.
	
A fourth digit **Z** is used internally, in order to eventually have versions for a Team. This version cannot be distributed to other teams.

Description of this milestone should be enough to describe why it is requested at a specific date.