## V1 Identity 

| #       | Description                                                  | [NIST §](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| ------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| **1.1** | Verify that all associated accounts passwords are at least 12 characters in length ([C6](https://owasp.org/www-project-proactive-controls/#div-numbering)) | 5.1.1.2                                                  |
| **1.2** | Verify that all accounts such as Telegram admins, GitHub, any associated Email accounts all use appropriate multi-factor authentication | 6.1.1                                                    |



## V2 Development

| #       | Description                                                  | [CWE](https://cwe.mitre.org/) |
| ------- | ------------------------------------------------------------ | ----------------------------- |
| **2.1** | Verify that server configuration is hardened as per the recommendations of the application server and frameworks in use | 16                            |
| **2.2** | Verify that all components are up to date, preferably using a dependency checker during build or compile time ([C2](https://owasp.org/www-project-proactive-controls/#div-numbering)) | 1026                          |
| **2.3** | Verify no secrets are within source code, preferably using a secrets scanner in CI environments ([C8](https://owasp.org/www-project-proactive-controls/#div-numbering)) | 798                           |



## V3 Community Administration

| #       | Description                                               |
| ------- | --------------------------------------------------------- |
| **3.1** | Verify Telegram groups have anti-spam protection in place |
| **3.2** | Verify Discord groups have anti-spam protection in place  |





#### Recommendations

| #       | Description                                                  |
| ------- | ------------------------------------------------------------ |
| **2.2** | [Snyk](https://snyk.io/), [DependencyCheck](https://github.com/jeremylong/DependencyCheck) |
| **2.3** | [Semgrep](https://github.com/marketplace/actions/semgrep-action) with [Secrets Policy](https://semgrep.dev/p/secrets) |
| **3.1** | [TgDev](https://tgdev.io/), [Shieldy](https://botostore.com/c/shieldy_bot/) |
| **3.2** | [Captcha.bot](https://top.gg/bot/512333785338216465)         |