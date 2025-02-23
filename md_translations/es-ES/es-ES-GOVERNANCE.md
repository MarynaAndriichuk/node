# Node.js Project Governance

<!-- TOC -->

* [Triagers](#triagers)
* [Collaborators](#collaborators)
  * [Collaborator activities](#collaborator-activities)
* [Technical steering committee](#technical-steering-committee)
  * [TSC meetings](#tsc-meetings)
* [Collaborator nominations](#collaborator-nominations)
  * [Onboarding](#onboarding)
* [Consensus seeking process](#consensus-seeking-process)

<!-- /TOC -->

## Triagers

Triagers assess newly-opened issues in the nodejs/node and nodejs/help repositories. There is no GitHub team for triagers at the moment.

Triagers have:
* ability to label issues
* ability to comment, close, and reopen issues

See:

* [A guide for triagers](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## Collaborators

Node.js Core Collaborators maintain the [nodejs/node][] GitHub repository. The GitHub team for Node.js Core Collaborators is @nodejs/collaborators. Collaborators have:

* Commit access to the [nodejs/node][] repository
* Access to the Node.js continuous integration (CI) jobs

Both Collaborators and non-Collaborators may propose changes to the Node.js source code. The mechanism to propose such a change is a GitHub pull request. Collaborators review and merge (_land_) pull requests.

Two Collaborators must approve a pull request before the pull request can land. (One Collaborator approval is enough if the pull request has been open for more than 7 days.) Approving a pull request indicates that the Collaborator accepts responsibility for the change. Approving a pull request indicates that the Collaborator accepts responsibility for the change. Approval must be from Collaborators who are not authors of the change.

If a Collaborator opposes a proposed change, then the change cannot land. The exception is if the TSC votes to approve the change despite the opposition. Usually, involving the TSC is unnecessary. Often, discussions or further changes result in Collaborators removing their opposition.

See:

* [List of Collaborators](./README.md#current-project-team-members)
* [A guide for Collaborators](./doc/guides/collaborator-guide.md)

### Collaborator activities

* Helping users and novice contributors
* Contributing code and documentation changes that improve the project
* Reviewing and commenting on issues and pull requests
* Participation in working groups
* Merging pull requests

The TSC can remove inactive Collaborators or provide them with _Emeritus_ status. Emeriti may request that the TSC restore them to active status.

## Technical Steering Committee

A subset of the Collaborators forms the Technical Steering Committee (TSC). The TSC has final authority over this project, including:

* Technical direction
* Project governance and process (including this policy)
* Contribution policy
* GitHub repository hosting
* Conduct guidelines
* Maintaining the list of Collaborators

The current list of TSC members is in [the project README](./README.md#current-project-team-members).

The [TSC Charter][] governs the operations of the TSC. All changes to the Charter need approval by the OpenJS Foundation Cross-Project Council (CPC).

### TSC meetings

The TSC meets in a voice conference call. Each year, the TSC elects a chair to run the meetings. The TSC streams its meetings for public viewing on YouTube or a similar service.

The TSC agenda includes issues that are at an impasse. The intention of the agenda is not to review or approve all patches. Collaborators review and approve patches on GitHub.

Any community member can create a GitHub issue asking that the TSC review something. If consensus-seeking fails for an issue, a Collaborator may apply the `tsc-agenda` label. That will add it to the TSC meeting agenda.

Before each TSC meeting, the meeting chair will share the agenda with members of the TSC. TSC members can also add items to the agenda at the beginning of each meeting. The meeting chair and the TSC cannot veto or remove items.

The TSC may invite people to take part in a non-voting capacity.

During the meeting, the TSC chair ensures that someone takes minutes. After the meeting, the TSC chair ensures that someone opens a pull request with the minutes.

The TSC seeks to resolve as many issues as possible outside meetings using [the TSC issue tracker](https://github.com/nodejs/TSC/issues). The process in the issue tracker is:

* A TSC member opens an issue explaining the proposal/issue and @-mentions @nodejs/tsc.
* The proposal passes if, after 72 hours, there are two or more TSC approvals and no TSC opposition.
* If there is an extended impasse, a TSC member may make a motion for a vote.

## Collaborator nominations

Existing Collaborators can nominate someone to become a Collaborator. Nominees should have significant and valuable contributions across the Node.js organization.

To nominate a new Collaborator, open an issue in the [nodejs/node][] repository. Provide a summary of the nominee's contributions. For example:

* Commits in the [nodejs/node][] repository.
  * Use the link `https://github.com/nodejs/node/commits?author=GITHUB_ID`
* Pull requests and issues opened in the [nodejs/node][] repository.
  * Use the link `https://github.com/nodejs/node/issues?q=author:GITHUB_ID`
* Comments on pull requests and issues in the [nodejs/node][] repository
  * Use the link `https://github.com/nodejs/node/issues?q=commenter:GITHUB_ID`
* Reviews on pull requests in the [nodejs/node][] repository
  * Use the link `https://github.com/nodejs/node/pulls?q=reviewed-by:GITHUB_ID`
* Help provided to end-users and novice contributors
* Pull requests and issues opened throughout the Node.js organization
  * Use the link  `https://github.com/search?q=author:GITHUB_ID+org:nodejs`
* Comments on pull requests and issues throughout the Node.js organization
  * Use the link `https://github.com/search?q=commenter:GITHUB_ID+org:nodejs`
* Participation in other projects, teams, and working groups of the Node.js organization
* Other participation in the wider Node.js community

Mention @nodejs/collaborators in the issue to notify other Collaborators about the nomination.

The nomination passes if no Collaborators oppose it after one week. Otherwise, the nomination fails.

There are steps a nominator can take in advance to make a nomination as frictionless as possible. To request feedback from other Collaborators in private, use the [Collaborators discussion page][] (which only Collaborators may view). A nominator may also work with the nominee to improve their contribution profile.

Collaborators might overlook someone with valuable contributions. In that case, the contributor may open an issue or contact a Collaborator to request a nomination.

### Onboarding

After the nomination passes, a TSC member onboards the new Collaborator. See [the onboarding guide](./onboarding.md) for details of the onboarding process.

## Consensus seeking process

The TSC follows a [Consensus Seeking][] decision-making model per the [TSC Charter][].

[Collaborators discussion page]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Consensus Seeking]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[TSC Charter]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[nodejs/node]: https://github.com/nodejs/node
