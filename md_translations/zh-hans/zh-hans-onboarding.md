# 上线

This document is an outline of the things we tell new Collaborators at their onboarding session.

## 在登机会前一周

* If the new Collaborator is not yet a member of the nodejs GitHub organization, confirm that they are using [two-factor authentication][]. It will not be possible to add them to the organization if they are not using two-factor authentication. If they cannot receive SMS messages from GitHub, try [using a TOTP mobile app][]. It will not be possible to add them to the organization if they are not using two-factor authentication. 如果他们无法从 GitHub 接收短信，请使用 [使用TOTP 移动应用程序][]
* Announce the accepted nomination in a TSC meeting and in the TSC mailing list.
* Suggest the new Collaborator install [`node-core-utils`][] and [set up the credentials][] for it.

## 登机会前15分钟

* Prior to the onboarding session, add the new Collaborator to [the Collaborators team](https://github.com/orgs/nodejs/teams/collaborators).
* 如果他们想加入任何子系统团队，请询问他们。 Ask them if they want to join any subsystem teams. See [Who to CC in the issue tracker][who-to-cc].

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
  * Membership: Consider making your membership in the Node.js GitHub organization public. This makes it easier to identify Collaborators. Instructions on how to do that are available at [Publicizing or hiding organization membership][]. 这使得更容易确定协作者。 关于如何做到这一点的说明在 [发布或隐藏组织成员][]

* 通知：
  * Use [https://github.com/notifications](https://github.com/notifications) or set up email
  * Watching the main repo will flood your inbox (several hundred notifications on typical weekdays), so be prepared

该项目有两个进行实时讨论的地点：
* [`#nodejs-dev`](https://openjs-foundation.slack.com/archives/C019Y2T6STH) on the [OpenJS Foundation](https://slack-invite.openjsf.org/)
* `#node-dev` on [webchat.freenode.net](https://webchat.freenode.net/) is a great place to interact with the TSC and other Collaborators
  * If there are any questions after the session, a good place to ask is there!
  * Presence is not mandatory, but please drop a note there if force-pushing to `master`

## 项目目标 &

* 合作者是该项目的集体所有者。
  * 该项目有其捐助者的目标

* 有一些更高层次的目标和价值
  * 对用户的感受很重要(这部分是我们登陆人员的原因)
  * 一般而言：试图对人民很好！
  * The best outcome is for people who come to our issue tracker to feel like they can come back again.

* You are expected to follow *and* hold others accountable to the [Code of Conduct][].

## 管理问题跟踪器

* You have (mostly) free rein; don't hesitate to close an issue if you are confident that it should be closed
  * 很高兴关闭问题！ Be nice about closing issues! Let people know why, and that issues and PRs can be reopened if necessary

* [**请参阅"标签"**](./doc/guides/onboarding-extras.md#labels)
  * There is [a bot](https://github.com/nodejs-github-bot/github-bot) that applies subsystem labels (for example, `doc`, `test`, `assert`, or `buffer`) so that we know what parts of the code base the pull request modifies. It is not perfect, of course. Feel free to apply relevant labels and remove irrelevant labels from pull requests and issues. It is not perfect, of course. 请随时应用相关标签，并从合并请求和问题中删除 个不相关的标签。
  * `semver-{minor,major}`:
    * If a change has the remote *chance* of breaking something, use the `semver-major` label
    * When adding a `semver-*` label, add a comment explaining why you're adding it. Do it right away so you don't forget! 你不要忘记它就马上走了！
  * 如果适用，请为 PRs 添加 [`作者准备`][] 标签。

* 查看 [在问题追踪器][who-to-cc] 中谁要抄送。
  * 这将随着时间的推移而变得更加自然。
  * For many of the teams listed there, you can ask to be added if you are interested
    * Some are WGs with some process around adding people, others are only there for notifications

* When a discussion gets heated, you can request that other Collaborators keep an eye on it by opening an issue at the private [nodejs/moderation](https://github.com/nodejs/moderation) repository.
  * This is a repository to which all members of the `nodejs` GitHub organization (not just Collaborators on Node.js core) have access. Its contents should not be shared externally. 它的 内容不应该由外部共享。
  * You can find the full moderation policy [here](https://github.com/nodejs/admin/blob/HEAD/Moderation-Policy.md).

## 审阅PRs

* 主要目标是改进代码编程。
* Secondary (but not far off) is for the person submitting code to succeed. A pull request from a new contributor is an opportunity to grow the community. 一个新贡献者的 拉请求是一个增长社区的机会。
* 每次审核一下。 Review a bit at a time. Do not overwhelm new contributors.
  * 它很想微观优化。 不要屈服于这种诱惑。 我们 经常更改 V8。 Techniques that provide improved performance today may be unnecessary in the future.
* 清醒：你的意见有很多重要意义！
* Nits (requests for small changes that are not essential) are fine, but try to avoid stalling the pull request.
  * 在您评论时将它们识别为nit： `Nit：将foo() 更改为bar。`
  * 如果他们拖动拉请求，请将他们合并为你自己。
* 问题应尽可能由工具而不是人类 审查人员来确定。 Insofar as possible, issues should be identified by tools rather than human reviewers. If you are leaving comments about issues that could be identified by tools but are not, consider implementing the necessary tooling.
* 最小等待评论时间
  * There is a minimum waiting time which we try to respect for non-trivial changes so that people who may have important input in such a distributed project are able to respond.
  * 对于非微不足道的更改，请将拉取请求至少打开48小时。
  * If a pull request is abandoned, check if they'd mind if you took it over (especially if it just has nits left).
* 批准修改
  * Collaborators indicate that they have reviewed and approve of the changes in a pull request using GitHub’s approval interface
  * 有些人想评论 `LGTM` (“看起来好于我”)
  * 你有权批准任何其他合作者的工作。
  * 您不能批准您自己的拉取请求。
  * When explicitly using `Changes requested`, show empathy – comments will usually be addressed even if you don’t use it.
    * If you do, it is nice if you are available later to check whether your comments have been addressed
    * If you see that the requested changes have been made, you can clear another collaborator's `Changes requested` review.
    * Use `Changes requested` to indicate that you are considering some of your comments to block the PR from landing.

* 在 Node.js 中的内容：
  * 意见不一——出于这个原因，拥有一个广泛的合作者基础是好的！
  * If Node.js itself needs it (due to historical reasons), then it belongs in Node.js.
    * That is to say, `url` is there because of `http`, `freelist` is there because of `http`, etc.
  * Things that cannot be done outside of core, or only with significant pain such as `async_hooks`.

* 连续集成测试：
  * [https://ci.nodejs.org/](https://ci.nodejs.org/)
    * 它不是自动运行。 您需要手动启动它。
  * 登录CI 与 GitHub 集成。 现在尝试登录！
  * 您将大部分时间使用 `节点测试-拉取请求`。 马上去！
    * 考虑书签： <https://ci.nodejs.org/job/node-test-pull-request/>
  * 若要进入表单来开始工作，请点击 `用参数` 构建。 (如果你 看不到它，这可能意味着你没有登录！) 现在点击！
  * To start CI testing from this screen, you need to fill in two elements on the form:
    * The `CERTIFY_SAFE` box should be checked. By checking it, you are indicating that you have reviewed the code you are about to test and you are confident that it does not contain any malicious code. (We don't want people hijacking our CI hosts to attack other hosts on the internet, for example!) 检查它， 您是 表示您已经审阅了您将要测试的代码，您的 相信它不包含任何恶意代码。 (我们不想有 个人劫持我们的 CI 主机来攻击互联网上的其他主机, 例如 个例子!)
    * `PR_ID` 框应填写识别拉取 请求的号码，包含您想要测试的代码。 The `PR_ID` box should be filled in with the number identifying the pull request containing the code you wish to test. For example, if the URL for the pull request is `https://github.com/nodejs/node/issues/7006`, then put `7006` in the `PR_ID`.
    * 表格上的其余要素一般保持不变。
  * 如果你需要帮助与CI相关的东西：
    * 使用 #node-dev (IRC) 与其他协作者交谈。
    * Use #node-build (IRC) to talk to the Build WG members who maintain the CI infrastructure.
    * Use the [Build WG repo](https://github.com/nodejs/build) to file issues for the Build WG members who maintain the CI infrastructure.

## 登陆PRs

查看协作指南： [登陆拉请求][]。

Commits in one PR that belong to one logical change should be squashed. It is rarely the case in onboarding exercises, so this needs to be pointed out separately during the onboarding. 在登机练习中很少出现这种情况，因此 需要在登机时单独指出。

<!-- TODO(joyeechueng): provide examples about "one logical change" -->

## 练习：将你自己添加到README

* Example: <https://github.com/nodejs/node/commit/b58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8>
  * For raw commit message: `git show --format=%Bb58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8`
* 协作者由GitHub 用户名按字母顺序排列。
* 可选，包括您的个人口令。
* Add the `Fixes: <collaborator-nomination-issue-url>` to the commit message so that when the commit lands, the nomination issue url will be automatically closed.
* Label your pull request with the `doc`, `notable-change`, and `fast-track` labels.
* 在 PR上运行 CI Run CI on the PR. Use the `node-test-pull-request` CI task.
* After two Collaborator approvals for the change and two Collaborator approvals for fast-tracking, land the PR.
* 在 PR中留下一个评论： `请👍 此评论以批准快速跟踪`。
* If there are not enough approvals within a reasonable time, consider the single approval of the onboarding TSC member sufficient, and land the PR.
  * Be sure to add the `PR-URL: <full-pr-url>` and appropriate `Reviewed-By:` metadata.
  * [`node-core-utils`][] automates the generation of metadata and the landing process. See the documentation of [`git-node`][]. 查看 [`git-node`][] 的文档。
  * [`核心验证提交`][] 自动验证提交信息。 This will be run during `git node land --final` of the [`git-node`][] command.

## 最后说明

* Don't worry about making mistakes: everybody makes them, there's a lot to internalize and that takes time (and we recognize that!)
* 几乎你可能犯的任何错误都可以被修复或还原。
* 现有的协作者信任您，并感谢您的帮助！
* 其它仓库：
  * [https://github.com/nodejs/TSC](https://github.com/nodejs/TSC)
  * [https://github.com/nodejs/building](https://github.com/nodejs/build)
  * [https://github.com/nodejs/nodejs.org](https://github.com/nodejs/nodejs.org)
  * [https://github.com/nodejs/readable-streamp](https://github.com/nodejs/readable-stream)
  * [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)
  * [https://github.com/nodejs/citgm](https://github.com/nodejs/citgm)
* The OpenJS Foundation hosts regular summits for active contributors to the Node.js project, where we have face-to-face discussions about our work on the project. The Foundation has travel funds to cover participants' expenses including accommodations, transportation, visa fees, etc. if needed. Check out the [summit](https://github.com/nodejs/summit) repository for details. 基金会有旅费支付参加者的费用 包括住宿费、交通费、签证费等。 Check out the [summit](https://github.com/nodejs/summit) repository for details.

[Code of Conduct]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[登陆拉请求]: doc/guides/collaborator-guide.md#landing-pull-requests
[Publicizing or hiding organization membership]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[发布或隐藏组织成员]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[`作者准备`]: doc/guides/collaborator-guide.md#author-ready-pull-requests
[`核心验证提交`]: https://github.com/nodejs/core-validate-commit
[`git-node`]: https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md
[`node-core-utils`]: https://github.com/nodejs/node-core-utils
[set up the credentials]: https://github.com/nodejs/node-core-utils#setting-up-credentials
[two-factor authentication]: https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/
[using a TOTP mobile app]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[使用TOTP 移动应用程序]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
