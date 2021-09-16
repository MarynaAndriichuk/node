# Node.js 项目管理

<!-- TOC -->

* [三角龙座](#triagers)
* [协作者](#collaborators)
  * [协作者活动](#collaborator-activities)
* [技术指导委员会](#technical-steering-committee)
  * [海训方案会议](#tsc-meetings)
* [合作者提名](#collaborator-nominations)
  * [上线](#onboarding)
* [A. 寻求共识的进程](#consensus-seeking-process)

<!-- /TOC -->

## 三角龙座

Triagers assess newly-opened issues in the nodejs/node and nodejs/help repositories. There is no GitHub team for triagers at the moment. 目前没有审判员的GitHub 小组。

三角龙拥有：
* 标记问题的能力
* 评论、关闭和重新打开问题的能力

看：

* [审判员指南](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## 协作者

Node.js 核心协作员维护 [节点/节点][] GitHub 资源库。 Node.js核心合作者的GitHub 团队是 @nodejs/collaborator。 协作者：

* 提交访问 [节点/节点][] 存储库
* 访问 Node.js 持续集成 (CI) 作业

Both Collaborators and non-Collaborators may propose changes to the Node.js source code. The mechanism to propose such a change is a GitHub pull request. Collaborators review and merge (_land_) pull requests. 提议这种改变的机制是GitHub 拉取请求。 协作者审核并合并 (_land_) 拉取请求。

两个协作者必须先批准拉请求才能降落。 (如果拉取请求已经打开超过 天，一个协作者批准就足够了。) 批准拉取请求表明协作者接受 的变更责任。 批准必须来自不是 个变更作者的协作者。

如果协作者反对拟议的更改，那么这种更改就无法降落。 个例外是如果海安会不顾反对意见，投票批准这一修改。 通常没有必要让海训方案参与。 讨论或进一步更改 常常导致协作者消除他们的反对意见。

看：

* [协作者列表](./README.md#current-project-team-members)
* [协作者指南](./doc/guides/collaborator-guide.md)

### 协作者活动

* 帮助用户和新手贡献者
* 改进项目的贡献代码和文档更改
* 审查和评论问题并拉取请求
* 参加工作组
* 合并合并拉取请求

The TSC can remove inactive Collaborators or provide them with _Emeritus_ status. Emeriti may request that the TSC restore them to active status. 紧急情况可要求海安会恢复其现役地位。

## 技术指导委员会

协作者的一个分组组成技术指导委员会。 海训方案对该项目拥有最后权力，包括：

* 技术方向
* 项目治理和进程(包括这项政策)
* 贡献政策
* GitHub repository hosting
* 行为准则
* 保持协作者名单

The current list of TSC members is in [the project README](./README.md#current-project-team-members).

[海安会章程][] 规范了海安会的运作。 The [TSC Charter][] governs the operations of the TSC. All changes to the Charter need approval by the OpenJS Foundation Cross-Project Council (CPC).

### 海训方案会议

海训方案举行了一次语音会议。 海训方案每年选举一名主席， 主持会议。 The TSC meets in a voice conference call. Each year, the TSC elects a chair to run the meetings. The TSC streams its meetings for public viewing on YouTube or a similar service.

海训方案的议程包括陷入僵局的问题。 The TSC agenda includes issues that are at an impasse. The intention of the agenda is not to review or approve all patches. Collaborators review and approve patches on GitHub. 协作者在GitHub 上审核并批准 个补丁。

Any community member can create a GitHub issue asking that the TSC review something. If consensus-seeking fails for an issue, a Collaborator may apply the `tsc-agenda` label. That will add it to the TSC meeting agenda. 如果寻求共识失败，协作者可以使用 `tsc-agenda` 标签。 这将把它列入海安会会议议程。

在每次海训会会议之前，会议主席将与技术支助委员会 个成员分享议程。 Before each TSC meeting, the meeting chair will share the agenda with members of the TSC. TSC members can also add items to the agenda at the beginning of each meeting. The meeting chair and the TSC cannot veto or remove items. 会议主席和海训方案不能否决或删除项目。

海训方案可邀请人们以无表决权的身份参加会议。

在会议期间，海训方案主席确保有人发言时间。 During the meeting, the TSC chair ensures that someone takes minutes. After the meeting, the TSC chair ensures that someone opens a pull request with the minutes.

The TSC seeks to resolve as many issues as possible outside meetings using [the TSC issue tracker](https://github.com/nodejs/TSC/issues). The process in the issue tracker is: 中的问题跟踪程序是：

* A TSC member opens an issue explaining the proposal/issue and @-mentions @nodejs/tsc.
* The proposal passes if, after 72 hours, there are two or more TSC approvals and no TSC opposition.
* 如果出现长期僵局，海安会成员可提出表决动议。

## 合作者提名

现有的协作者可以提名某人担任协作者。 Existing Collaborators can nominate someone to become a Collaborator. Nominees should have significant and valuable contributions across the Node.js organization.

要提名一个新的协作者，请在 [节点/节点][] 仓库中打开一个问题。 请简要说明被提名人的贡献。 例如：

* 在 [节点/节点][] 仓库中提交。
  * 使用链接 `https://github.com/nodejs/node/commits?author=GITHUB_ID`
* 拉取在 [节点/节点][] 仓库中打开的请求和问题。
  * 使用链接 `https://github.com/nodejs/node/issues?q=author:GITHUB_ID`
* 在 [节点/节点][] 仓库中对合并请求和问题的评论
  * 使用链接 `https://github.com/nodejs/node/issues?q=comment:GITHUB_ID`
* 对 [nodejs/节点][] 仓库中的合并请求进行评论
  * 使用链接 `https://github.com/nodejs/node/pulls?q=reviewed-by:GITHUB_ID`
* 向最终用户和新手贡献者提供帮助
* 拉取在Node.js整个组织中打开的请求和问题
  * 使用链接  `https://github.com/search?q=author:GITHUB_ID+org:nodejs`
* 在 Node.js 组织内对合并请求和问题的评论
  * 使用链接 `https://github.com/search?q=commanter:GITHUB_ID+org:nodejs`
* Participation in other projects, teams, and working groups of the Node.js organization
* 更广泛的Node.js社区的其他参与

Mention @nodejs/collaborators in the issue to notify other Collaborators about the nomination.

如果没有合作者在一周后表示反对，提名就会通过。 否则， 提名失败。

提名者可以提前采取步骤提名，尽可能做到 个摩擦。 There are steps a nominator can take in advance to make a nomination as frictionless as possible. To request feedback from other Collaborators in private, use the [Collaborators discussion page][] (which only Collaborators may view). A nominator may also work with the nominee to improve their contribution profile. 提名人也可以与 被提名人合作，改进他们的贡献情况。

合作者可能会忽略某人的宝贵贡献。 Collaborators might overlook someone with valuable contributions. In that case, the contributor may open an issue or contact a Collaborator to request a nomination.

### 上线

提名通过后，海安会的一名成员在新的合作者上岗。 查看 [登机指南](./onboarding.md) 以了解登机 流程的详细信息。

## A. 寻求共识的进程

The TSC follows a [Consensus Seeking][] decision-making model per the [TSC Charter][].

[Collaborators discussion page]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Consensus Seeking]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[海安会章程]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[TSC Charter]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[节点/节点]: https://github.com/nodejs/node
[nodejs/节点]: https://github.com/nodejs/node
