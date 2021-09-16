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

试听器评估节点/节点和节点/帮助仓库中新出现的问题。 目前没有审判员的GitHub 小组。

三角龙拥有：
* 标记问题的能力
* 评论、关闭和重新打开问题的能力

看：

* [审判员指南](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## 协作者

Node.js 核心协作员维护 [节点/节点][] GitHub 资源库。 Node.js核心合作者的GitHub 团队是 @nodejs/collaborator。 协作者：

* 提交访问 [节点/节点][] 存储库
* 访问 Node.js 持续集成 (CI) 作业

协作者和非协作者都可以提议修改Node.js源代码。 提议这种改变的机制是GitHub 拉取请求。 协作者审核并合并 (_land_) 拉取请求。

两个协作者必须先批准拉请求才能降落。 (如果拉取请求已经打开超过7天，一个协作者批准就足够了。) 批准拉取请求表明协作者接受更改的责任。 批准拉取请求表明协作者接受更改的责任。 合作者必须得到批准，因为他们不是变化的作者。

如果协作者反对拟议的更改，那么这种更改就无法降落。 如果海安会不顾反对意见，投票批准这一更改，则属于例外。 通常没有必要让海训方案参与。 讨论或进一步改变常常导致协作者消除其反对意见。

看：

* [协作者列表](./README.md#current-project-team-members)
* [协作者指南](./doc/guides/collaborator-guide.md)

### 协作者活动

* 帮助用户和新手贡献者
* 改进项目的贡献代码和文档更改
* 审查和评论问题并拉取请求
* 参加工作组
* 合并合并拉取请求

海训方案可以移除不活动的合作者，或者为他们提供 _荣誉_ 状态。 紧急情况可要求海安会恢复其现役地位。

## 技术指导委员会

协作者的一个分组组成技术指导委员会。 海训方案对该项目拥有最后权力，包括：

* 技术方向
* 项目治理和进程(包括这项政策)
* 贡献政策
* GitHub repository hosting
* 行为准则
* 保持协作者名单

当前海训方案成员列表在 [中是README](./README.md#current-project-team-members) 项目。

[海安会章程][] 规范了海安会的运作。 《宪章》的所有修改都需要OpenJS Foundation Cross-Project Council (CPC)批准。

### 海训方案会议

海训方案举行了一次语音会议。 海训方案每年选举一名主席主持会议。 海训方案在YouTube或类似的服务部门安排会议，以供公众观看。

海训方案的议程包括陷入僵局的问题。 议程的用意不是审查或批准所有修补办法。 协作者审查并批准在 GitHub 上的补丁。

任何社区成员都可以创建一个GitHub 问题，要求海训方案审查某些问题。 如果寻求共识失败，协作者可以使用 `tsc-agenda` 标签。 这将把它列入海安会会议议程。

在每次海委会会议之前，会议主席将与海委会成员分享议程。 海安会成员也可在每次会议开始时在议程上增列项目。 会议主席和海训方案不能否决或删除项目。

海训方案可邀请人们以无表决权的身份参加会议。

在会议期间，海训方案主席确保有人发言时间。 会议结束后，海安会主席确保有人用会议记录提出拉动请求。

海训方案力求利用 [海训方案问题跟踪器](https://github.com/nodejs/TSC/issues) 解决尽可能多的会议外面问题。 问题跟踪器中的进程是：

* 海训方案的一名成员开启了一个解释建议/问题的问题，并@-referring @nodejs/tsc。
* 如果在72小时后有两次或更多的海训方案批准，没有海训方案反对，该提案即告通过。
* 如果出现长期僵局，海安会成员可提出表决动议。

## 合作者提名

现有的协作者可以提名某人担任协作者。 被提名者应在诺德.js整个组织中作出重要和宝贵的贡献。

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
* 参与诺德.js组织的其他项目、小组和工作组
* 更广泛的Node.js社区的其他参与

@nodejs/合作者在这个问题上通知其他协作者有关提名。

如果没有合作者在一周后表示反对，提名就会通过。 否则，提名将告失败。

提名者可以事先采取步骤，使提名尽可能不产生摩擦。 若要请其他协作者私下反馈，请使用 [协作者讨论页面][] (只有协作者可以查看)。 提名人也可与被提名人合作，改进他们的提名情况。

合作者可能会忽略某人的宝贵贡献。 在这种情况下，参与者可以开一个问题或联系协作者请求提名。

### 上线

提名通过后，海安会的一名成员在新的合作者上岗。 查看 [登机指南](./onboarding.md) 了解登机过程的详细信息。

## A. 寻求共识的进程

The TSC follows a [Consensus Seeking][] decision-making model per the [TSC Charter][].

[协作者讨论页面]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Consensus Seeking]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[海安会章程]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[TSC Charter]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[节点/节点]: https://github.com/nodejs/node
[nodejs/节点]: https://github.com/nodejs/node
