# Sécurité

## Signaler un bug dans Node.js

Signalez des bugs de sécurité dans Node.js via [HackerOne](https://hackerone.com/nodejs).

Your report will be acknowledged within 24 hours, and you’ll receive a more detailed response to your report within 48 hours indicating the next steps in handling your submission.

After the initial reply to your report, the security team will endeavor to keep you informed of the progress being made towards a fix and full announcement, and may ask for additional information or guidance surrounding the reported issue.

### Programme de récompense de bug Node.js

The Node.js project engages in an official bug bounty program for security researchers and responsible public disclosures.  The program is managed through the HackerOne platform. Voir <https://hackerone.com/nodejs> pour plus de détails.

## Signaler un bug dans un module tiers

Security bugs in third party modules should be reported to their respective maintainers and should also be coordinated through the Node.js Ecosystem Security Team via [HackerOne](https://hackerone.com/nodejs-ecosystem).

Details regarding this process can be found in the [Security Working Group repository](https://github.com/nodejs/security-wg/blob/HEAD/processes/third_party_vuln_process.md).

Merci pour l'amélioration de la sécurité de Node.js et de son écosystème. Your efforts and responsible disclosure are greatly appreciated and will be acknowledged.

## Politique de divulgation

Voici la politique de divulgation de sécurité pour Node.js

* Le rapport de sécurité est reçu et reçoit un gestionnaire principal. This person will coordinate the fix and release process. The problem is confirmed and a list of all affected versions is determined. Code is audited to find any potential similar problems. Fixes are prepared for all releases which are still under maintenance. These fixes are not committed to the public repository but rather held locally pending the announcement.

* A suggested embargo date for this vulnerability is chosen and a CVE (Common Vulnerabilities and Exposures (CVE®)) is requested for the vulnerability.

* On the embargo date, the Node.js security mailing list is sent a copy of the announcement. The changes are pushed to the public repository and new builds are deployed to nodejs.org. Within 6 hours of the mailing list being notified, a copy of the advisory will be published on the Node.js blog.

* Typically the embargo date will be set 72 hours from the time the CVE is issued. However, this may vary depending on the severity of the bug or difficulty in applying a fix.

* This process can take some time, especially when coordination is required with maintainers of other projects. Every effort will be made to handle the bug in as timely a manner as possible; however, it’s important that we follow the release process above to ensure that the disclosure is handled in a consistent manner.

## Réception des mises à jour de sécurité

Les notifications de sécurité seront distribuées via les méthodes suivantes.

* <https://groups.google.com/group/nodejs-sec>
* [https://nodejs.org/fr/blog/](https://nodejs.org/en/blog/)

## Commentaires sur cette politique

If you have suggestions on how this process could be improved please submit a [pull request](https://github.com/nodejs/nodejs.org) or [file an issue](https://github.com/nodejs/security-wg/issues/new) to discuss.
