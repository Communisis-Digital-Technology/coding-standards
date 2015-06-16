/* 
Title: Information Security
Sort: 4
*/

We follow [OWASP](https://www.owasp.org/index.php/Main_Page) standards for information security in all our work, alongside client side Digital Standards.

Project definitions MUST include a data catalogue and risk assessment and be clearly identified in any technical documentation.

Pen testing of any Communisis Digital hosted system SHOULD be built into the project lifecycle, particularly in the case of any product carrying a data risk.  The QA process in these instances should test against the OWASP top ten where appropriate.

## Personally Identifiable Information (PII)

For the purposes of this document PII is as defined by US Privacy Law, and can be summarised from the [Wikipedia definition][pii-wiki] (accessed 30 June 2014)

> information that can be used on its own or with other information to identify, contact, or locate a single person, or to identify an individual in context.

Personally identifiable information should be stored on a networked resource for only as long as absolutely required by the needs of a project. It should not be sent over email unless absolutely necessary, and at any time it is stored or transferred it **MUST** be encrypted, at the very least by using a password protected zip file. Once data is no longer required it should be deleted, no later than 2 weeks after it has ended use.

As responsible users and handlers of personal information on the part of our clients we MUST confirm to legal data requirements.

* **DO NOT** store PII on your PC desktop or file system
* **DO NOT** make more duplicates of a file containing PII than necessary
* **DO NOT** transfer PII unencrypted
* **DO NOT** keep data longer than required
* **DO NOT** send a file (or reference to the location of a file) and a password in the same email

* **DO** encrypt all PII
* **DO** inform your manager of any breach 
* **DO** inform your manager of any request which goes outside the requirements outlined here
* **DO** share passwords and encrypted data on different channels 

[pii-wiki]: http://en.wikipedia.org/wiki/Personally_identifiable_information
