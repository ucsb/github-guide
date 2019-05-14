# Security Risks

## Weak Github Password

The attacker uses a brute force attack to discover a username/password combination for Github.

**Response Classifiction**: Mitigate

### Treatment Plans

* [Require 2FA on All Accounts](https://help.github.com/en/articles/requiring-two-factor-authentication-in-your-organization)
* MFA through github credentials and UCSB SSO.

### Probability: High


* It has already occurred at UCD. It has been [publicly reported in the wild](https://stackoverflow.com/questions/9247961/recover-a-deleted-repository-github-issues)

### Potential Impact: Medium

* Repository Deleted (Loss Scenario)
* The repositories code could be updated with malicious code. If the repository is tied to an automated deployment pipeline there is a chance of the code being deployed to Prod before being detected. (I really need to find a percentage likelihood of this.)

### Decision & Discussion Details

With UCSB's SSO integrated into the login, there is an implicit MFA built into the system. However, their is strong consideration to also require 2FA on all Github accounts that want to be linked to the UCSB organization.



<hr />

## Github Credentials Exposed in Public Source Code

Loss of credentials through accidental check-in in a public repository.

**Response Classification**:

### Treatment Plans

* Scan source control before check-in (ie. [git-secrets](https://github.com/awslabs/git-secrets))

### Probability: Medium

### Potential Impact:

### Decision & Discussion Details

(Question) Would there be a case where both Github credentials and UCSB credentials would both be in source control? (Then again, why would either be in source control?)

<hr />

## Github API Credentials Exposed in Public Source Code

Loss of credentials which would give an attacker access to Github API through accidental check-in in a public repository.

**Response Classification**: 

### Treatment Plans

* Scan source control before check-in (ie. [git-secrets](https://github.com/awslabs/git-secrets))

### Probability: Medium

* It wasn't Github API credential loss, but [this has already happened at UCSB](http://stevenmaglio.blogspot.com/2019/02/aws-api-key-exposed-in-github.html).
* When possible, use [read-only API keys (deploy keys)](https://developer.github.com/v3/guides/managing-deploy-keys/).

### Potential Impact: Medium

* Repository Deleted (Loss Scenario)





<hr />

Loss Scenario | Recovery Plans / Ideas | Probability | Response Classification & Status | Decisiosn & Discussion Details
---|---|---|---|---
_Repository Deleted <br/>All Repositories Deleted_ <br /><br /> Repositories could be completely wiped out. | <ul><li>[An email to Github support](https://stackoverflow.com/questions/9247961/recover-a-deleted-repository-github-issues) could get the repository recovered.</li><li>[Make a backup](https://stackoverflow.com/questions/5578270/fully-backup-a-git-repo) on a schedule or as a part of the check-in process.</li><li>Multiple Origins</li></ul> |  |  |
_Repository Updated with Malicious Code_ <br /><br /> The repositories code could be updated with malicious code. If the repository is tied to an automated deployment pipeline there is a chance of the code being deployed to Prod before being detected. (I really need to find a percentage likelihood of this.) |  |  |  |  |