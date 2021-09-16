# 安全

## 在 Node.js 中报告一个错误

通过 [HackerOne](https://hackerone.com/nodejs) 报告Node.js 中的安全漏洞。

Your report will be acknowledged within 24 hours, and you’ll receive a more detailed response to your report within 48 hours indicating the next steps in handling your submission.

After the initial reply to your report, the security team will endeavor to keep you informed of the progress being made towards a fix and full announcement, and may ask for additional information or guidance surrounding the reported issue.

### Node.js bug bounty 程序

The Node.js project engages in an official bug bounty program for security researchers and responsible public disclosures.  The program is managed through the HackerOne platform. See <https://hackerone.com/nodejs> for further details.  程序通过 HackerOne 平台管理。 更多详情请访问 <https://hackerone.com/nodejs>

## 在第三方模块中报告一个错误

Security bugs in third party modules should be reported to their respective maintainers and should also be coordinated through the Node.js Ecosystem Security Team via [HackerOne](https://hackerone.com/nodejs-ecosystem).

Details regarding this process can be found in the [Security Working Group repository](https://github.com/nodejs/security-wg/blob/HEAD/processes/third_party_vuln_process.md).

感谢你改善Node.js及其生态系统的安全。 您的努力 和负责任的披露非常受欢迎，并将得到承认。

## 披露政策

下面是 Node.js 的安全披露政策

* 安全报告已收到，并被分配给一个主要处理器。 此 人将协调修复和释放过程。 问题已确认 并确定所有受影响的版本列表。 代码被审核以找到 任何潜在的类似问题。 修复是为所有仍在维护中的 版本准备的。 这些修复并不是对公开的 仓库的承诺，而是在发布公告之前在本地持有。

* A suggested embargo date for this vulnerability is chosen and a CVE (Common Vulnerabilities and Exposures (CVE®)) is requested for the vulnerability.

* On the embargo date, the Node.js security mailing list is sent a copy of the announcement. The changes are pushed to the public repository and new builds are deployed to nodejs.org. Within 6 hours of the mailing list being notified, a copy of the advisory will be published on the Node.js blog. 这些更改被推送到公共仓库，新版本 被部署到nodejs.org。 在 通知邮件列表后的 6 小时内，咨询的副本将在 Node.js 博客上发布。

* Typically the embargo date will be set 72 hours from the time the CVE is issued. However, this may vary depending on the severity of the bug or difficulty in applying a fix. 然而，这可能会因错误的严重性或 难度而异。

* 此进程可能需要一些时间，特别是当需要与其他项目的维护者进行协调 时。 This process can take some time, especially when coordination is required with maintainers of other projects. Every effort will be made to handle the bug in as timely a manner as possible; however, it’s important that we follow the release process above to ensure that the disclosure is handled in a consistent manner.

## 接收安全更新

安全通知将通过以下方法分发。

* <https://groups.google.com/group/nodejs-sec>
* <https://nodejs.org/en/blog/>

## 对此政策的评论

If you have suggestions on how this process could be improved please submit a [pull request](https://github.com/nodejs/nodejs.org) or [file an issue](https://github.com/nodejs/security-wg/issues/new) to discuss.
