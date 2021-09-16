# 上线

这份文件概述了我们在新的协作者上岗会议上向他们介绍的情况。

## 在登机会前一周

* 如果新的协作器还不是节点GitHub 组织的成员，确认他们正在使用 [双重身份验证][]。 如果它们不使用双重身份验证，就不可能将它们添加到组织。 如果他们无法从 GitHub 接收短信，请使用 [使用TOTP 移动应用程序][]。
* 在海训方案会议和海训方案邮寄名单中公布接受的提名。
* 建议新的协作器安装 [`node-coere-utils`][] 和 [为此设置了证书][]

## 登机会前15分钟

* 在登机前, 添加新的协作者到 [协作者团队](https://github.com/orgs/nodejs/teams/collaborators)。
* 如果他们想加入任何子系统团队，请询问他们。 查看 [在问题追踪器][who-to-cc] 中谁要抄送。

## 在线寄宿会议

* 本次会议将包括：
  * [本地设置](#local-setup)
  * [项目目标 &](#project-goals--values)
  * [管理问题跟踪器](#managing-the-issue-tracker)
  * [正在审查PRs](#reviewing-prs)
  * [登陆PRs](#landing-prs)

## 本地设置

* git:
  * 请确保您有空格： `git config --global --add
apply.whitspace fix`
  * 总是从你自己的 GitHub 派生来继续PR
    * `节点/节点` 仓库中的分支仅用于发布行
  * 添加规范节点存储库作为 `上游` 远程：
    * `git 远程添加上流 git://github.com/nodejs/node.git`
  * 要从 `上流` 更新：
    * `git 结帐管理员`
    * `git 远程更新 -p` or `git 抓取--all`
    * `git 合并 --ff-only 上游/主` (或 `REMOTENAME/BRANCH`)
  * 为您提交的每一个 PR 创建一个新分支。
  * 成员：考虑公开您在Node.js GitHub 组织中的会员资格。 这使得更容易确定协作者。 关于如何做到这一点的说明在 [公开或隐藏组织成员][]。

* 通知：
  * 使用 [https://github.com/notifications](https://github.com/notifications) 或设置电子邮件
  * 观看主要仓库会淹没您的收件箱 (典型的周日有几百个通知)，所以准备好了

该项目有两个进行实时讨论的地点：
* [`#nodejs-dev`](https://openjs-foundation.slack.com/archives/C019Y2T6STH) 在 [OpenJS 基金会](https://slack-invite.openjsf.org/)
* `#nodev` on [webchat.freenode.net](https://webchat.freenode.net/) 是与TSC和其他协作者交互的一个很好的地方
  * 如果会后还有任何问题，请问的好地方！
  * Presence不是强制性的，但如果强制推送到 `master` 请在那里拖放笔记

## 项目目标 &

* 合作者是该项目的集体所有者。
  * 该项目有其捐助者的目标

* 有一些更高层次的目标和价值
  * 对用户的感受很重要(这部分是我们登陆人员的原因)
  * 一般而言：试图对人民很好！
  * 最好的结果是那些来到我们的问题追踪器的人感到他们能够再次回来。

* 您需要关注 *和* ，使其他人对 [行为守则][] 负责。

## 管理问题跟踪器

* 你有(大多)免费的控制; 如果你确信某个问题应该被关闭, 请不要犹豫关闭.
  * 很高兴关闭问题！ 让人们知道为什么，必要时可以重新讨论问题和PR。

* [**请参阅"标签"**](./doc/guides/onboarding-extras.md#labels)
  * 有 [个机器人](https://github.com/nodejs-github-bot/github-bot) 应用子系统标签(例如， `doc`, `test`, `断言`, 或 `缓存`, 以便我们知道代码的哪些部分是合并请求修改的基础。 当然，这并非十全十美。 请随时应用相关的标签，并从合并请求和问题中删除不相关的标签。
  * `semver-{minor,major}`:
    * 如果更改有远程 *几率* 破坏某些东西，请使用 `半个标签` 标签
    * 当添加 `分*` 标签时，添加一个注释，解释您为什么要添加它。 你不要忘记它就马上走了！
  * 如果适用，请为 PRs 添加 [`作者准备`][] 标签。

* 查看 [在问题追踪器][who-to-cc] 中谁要抄送。
  * 这将随着时间的推移而变得更加自然。
  * 对于列出的许多团队，如果您有兴趣，您可以要求添加。
    * 有些是带有某些添加人的过程的工作区，另一些只在那里进行通知

* 当讨论被加热时， 您可以通过在私有的 [节点/管理](https://github.com/nodejs/moderation) 仓库中打开一个问题来请求其他协作者保持对它的监督。
  * 这是一个 `节点` GitHub 组织的所有成员（不仅仅是Node.js 核心上的协作者）都可以访问的存储库。 其内容不应由外部分享。
  * 您可以在这里找到完整的审核策略 [](https://github.com/nodejs/admin/blob/HEAD/Moderation-Policy.md)。

## 审阅PRs

* 主要目标是改进代码编程。
* 次要（但不远）是提交代码的人成功的。 一个新贡献者的拉请求是一个发展社区的机会。
* 每次审核一下。 不要压倒新的贡献者。
  * 它很想微观优化。 不要屈服于这种诱惑。 我们经常更改 V8。 今天改进业绩的技术在今后可能是没有必要的。
* 清醒：你的意见有很多重要意义！
* Nits (请求进行不重要的小改动)是没有问题的，但试图避免拖动拉请求。
  * 在您评论时将它们识别为nit： `Nit：将foo() 更改为bar。`
  * 如果他们拖动拉请求，请将他们合并为你自己。
* 问题应尽可能由工具而不是由人类审查人员来确定。 如果您留下的评论是关于可以通过工具识别但却没有的问题，请考虑执行必要的工具。
* 最小等待评论时间
  * 我们设法尊重非微不足道的变化的最低等候时间，以便可能对这种分布式项目有重要投入的人能够作出反应。
  * 对于非微不足道的更改，请将拉取请求至少打开48小时。
  * 如果一个拉取请求被放弃，请检查他们是否想要接管它(尤其是如果它只剩下零)。
* 批准修改
  * 协作者表示，他们已经通过使用 GitHub 的批准界面审核并批准拉取请求中的更改
  * 有些人想评论 `LGTM` (“看起来好于我”)
  * 你有权批准任何其他合作者的工作。
  * 您不能批准您自己的拉取请求。
  * 当明确使用 `请求的更改`时，显示同情——评论通常将被处理，即使您不使用它。
    * 如果您这样做，请检查您的评论是否已经被处理。如果您稍后可用，那将是很好
    * 如果您看到请求的更改已经完成，您可以清除另一个合作者 `请求的更改` 审核。
    * 使用 `请求的` 来表明您正在考虑您的一些评论来阻止PR 降落。

* 在 Node.js 中的内容：
  * 意见不一——出于这个原因，拥有一个广泛的合作者基础是好的！
  * 如果Node.js本身需要它(由于历史原因)，它就属于Node.js。
    * 这就是说， `url` 因为 `http`而存在， `自由主义者` 因为 `http`，等等。
  * 无法在核心之外做出的事情，或者只能在严重疼痛的情况下做，如 `异步钩子`。

* 连续集成测试：
  * [https://ci.nodejs.org/](https://ci.nodejs.org/)
    * 它不是自动运行。 您需要手动启动它。
  * 登录CI 与 GitHub 集成。 现在尝试登录！
  * 您将大部分时间使用 `节点测试-拉取请求`。 马上去！
    * 考虑书签： <https://ci.nodejs.org/job/node-test-pull-request/>
  * 若要进入表单来开始工作，请点击 `用参数` 构建。 (如果你看不到，这可能意味着你没有登录！) 现在点击！ 现在点击！
  * 要在此屏幕上开始CI 测试，您需要填写表格上的两个元素：
    * `CERTIFY_SAFE` 框应被选中。 检查它， 你表示你已经审阅了你将要测试的代码，你相信它不包含任何恶意代码。 (我们不想让人劫持我们的 CI 主机来攻击互联网上的其他主机，例如！)
    * `PR_ID` 框应该填写用于识别包含您想要测试的代码的拉取请求的数字。 例如，如果拉取请求的 URL 是 `https://github.com/nodejs/node/issues/7006`, 然后将 `7006` 放入 `PR_ID` 中。
    * 表格上的其余要素一般保持不变。
  * 如果你需要帮助与CI相关的东西：
    * 使用 #node-dev (IRC) 与其他协作者交谈。
    * 使用 #node-build(IRC) 与维护CI 基础设施的构建工作组成员交谈。
    * 使用 [Building WG repo](https://github.com/nodejs/build) 为维护CI 基础设施的 BuildWG 成员提交问题。

## 登陆PRs

查看协作指南： [登陆拉请求][]。

在一个属于一个逻辑变化的 PR 中的提交应该被挤压。 在登机作业中很少出现这种情况，因此在登机时需要单独指出这一点。

<!-- TODO(joyeechueng): provide examples about "one logical change" -->

## 练习：将你自己添加到README

* 例如： <https://github.com/nodejs/node/commit/b58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8>
  * 对于原始提交消息： `git 显示 --format =%Bb58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8`
* 协作者由GitHub 用户名按字母顺序排列。
* 可选，包括您的个人口令。
* 添加 `修复： <collaborator-nomination-issue-url>` 到提交信息，以便当提交土地时，指定的URL将自动关闭。
* 使用 `doc`, `notable-change`, 和 `快轨` 标签来标注您的拉取请求。
* 在 PR上运行 CI 使用 `node-test-pull-request` CI 任务。
* 经过两次合作者批准的变更和两次快速通道合作者批准后，审评被降落。
* 在 PR中留下一个评论： `请👍 此评论以批准快速跟踪`。
* 如果在合理的时间内没有足够的批准，考虑船上船上船的海安会成员的单一批准就足够了，然后让船上船的船上船的船上船上船的船上船上船上船的船上船上船的船上船上船上船的船上船上船上船的船上船上船上船的船上船上船的船上船上船上船上船上船的船上船上船上船的船上船上船上船的船上船上船上船的船上船上船的船上船上船上船的船上船上船上船上船上船的船上船上船上船的船上船上船上船上船的船上船上船上船上船上船上船上船上船上船的船上船上船上船上船上船
  * 请务必添加 `PR-URL： <full-pr-url>` 和适当的 `评论者：` 元数据。
  * [`节点代码utils`][] 自动生成元数据和着陆过程。 查看 [`git-node`][] 的文档。
  * [`核心验证提交`][] 自动验证提交信息。 这将在 `git 节点土地-- <a href="https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md" fo="6">的最终``git-node`</a> 命令期间运行。

## 最后说明

* 不要担心犯错误：每个人都会使他们变得有许多内部化的东西，这需要时间(我们认识到这一点！)
* 几乎你可能犯的任何错误都可以被修复或还原。
* 现有的协作者信任您，并感谢您的帮助！
* 其它仓库：
  * [https://github.com/nodejs/TSC](https://github.com/nodejs/TSC)
  * [https://github.com/nodejs/building](https://github.com/nodejs/build)
  * [https://github.com/nodejs/nodejs.org](https://github.com/nodejs/nodejs.org)
  * [https://github.com/nodejs/readable-streamp](https://github.com/nodejs/readable-stream)
  * [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)
  * [https://github.com/nodejs/citgm](https://github.com/nodejs/citgm)
* OpenJS基金会定期主办首脑会议，积极参加Node.js项目，我们在该项目上面对面地讨论我们的项目工作。 基金会有旅费支付与会者在必要时的开支，包括住宿费、交通费、签证费等。 查看 [Summit](https://github.com/nodejs/summit) 存储库了解详情。

[行为守则]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[登陆拉请求]: doc/guides/collaborator-guide.md#landing-pull-requests
[公开或隐藏组织成员]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[`作者准备`]: doc/guides/collaborator-guide.md#author-ready-pull-requests
[`核心验证提交`]: https://github.com/nodejs/core-validate-commit
[`git-node`]: https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md
[`node-coere-utils`]: https://github.com/nodejs/node-core-utils
[`节点代码utils`]: https://github.com/nodejs/node-core-utils
[为此设置了证书]: https://github.com/nodejs/node-core-utils#setting-up-credentials
[双重身份验证]: https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/
[使用TOTP 移动应用程序]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
