---
id: usage-report
title: Report
sidebar_label: Report
---

```
report:
        report
                [-lang=en|ja]
                [-config=/path/to/config.toml]
                [-results-dir=/path/to/results]
                [-log-dir=/path/to/log]
                [-refresh-cve]
                [-cvss-over=7]
                [-diff]
                [-ignore-unscored-cves]
                [-ignore-unfixed]
                [-to-email]
                [-to-http]
                [-to-slack]
                [-to-stride]
                [-to-hipchat]
                [-to-chatwork]
                [-to-localfile]
                [-to-s3]
                [-to-azure-blob]
                [-format-json]
                [-format-xml]
                [-format-one-email]
                [-format-one-line-text]
                [-format-list]
                [-format-full-text]
                [-gzip]
                [-uuid]
                [-http-proxy=http://192.168.0.1:8080]
                [-debug]
                [-debug-sql]
                [-pipe]
                [-cvedb-type=sqlite3|mysql|postgres|redis]
                [-cvedb-path=/path/to/cve.sqlite3]
                [-cvedb-url=http://127.0.0.1:1323 or DB connection string]
                [-ovaldb-type=sqlite3|mysql|redis]
                [-ovaldb-path=/path/to/oval.sqlite3]
                [-ovaldb-url=http://127.0.0.1:1324 or DB connection string]
                [-gostdb-type=sqlite3|mysql|redis]
                [-gostdb-path=/path/to/gost.sqlite3]
                [-gostdb-url=http://127.0.0.1:1325 or DB connection string]
                [-http="http://vuls-report-server"]


                [RFC3339 datetime format under results dir]
  -config string
        /path/to/toml (default "/Users/kanbe/go/src/github.com/future-architect/vuls/config.toml")
  -cvss-over float
        -cvss-over=6.5 means reporting CVSS Score 6.5 and over (default: 0 (means report all))
  -debug
        debug mode
  -debug-sql
        SQL debug mode
  -diff
        Difference between previous result and current result
  -format-full-text
        Detail report in plain text
  -format-json
        JSON format
  -format-list
        Display as list format
  -format-one-email
        Send all the host report via only one EMail (Specify with -to-email)
  -format-one-line-text
        One line summary in plain text
  -format-xml
        XML format
  -gzip
        gzip compression
  -http-proxy string
        http://proxy-url:port (default: empty)
  -ignore-unfixed
        Don't report the unfixed CVEs
  -ignore-unscored-cves
        Don't report the unscored CVEs
  -lang string
        [en|ja] (default "en")
  -log-dir string
        /path/to/log (default "/var/log/vuls")
  -pipe
        Use args passed via PIPE
  -refresh-cve
        Refresh CVE information in JSON file under results dir
  -results-dir string
        /path/to/results (default "/Users/kanbe/go/src/github.com/future-architect/vuls/results")
  -to-azure-blob
        Write report to Azure Storage blob (container/yyyyMMdd_HHmm/servername.json/xml/txt)
  -to-chatwork
        Send report via chatwork
  -to-email
        Send report via Email
  -to-hipchat
        Send report via hipchat
  -to-http
        Send report via HTTP POST
  -to-localfile
        Write report to localfile
  -to-s3
        Write report to S3 (bucket/yyyyMMdd_HHmm/servername.json/xml/txt)
  -to-slack
        Send report via Slack
  -to-stride
        Send report via Stride
  -to-syslog
        Send report via Syslog
  -uuid
        Auto generate of scan target servers and then write to config.toml and scan result
  -cvedb-sqlite3-path string
        /path/to/sqlite3
  -cvedb-type string
        DB type of go-cve-dictionary (sqlite3, mysql, postgres or redis) (default "sqlite3")
  -cvedb-url string
        http://go-cve-dictionary.com:1323 or DB connection string
  -gostdb-sqlite3-path string
        /path/to/sqlite3
  -gostdb-type string
        DB type of gost (sqlite3, mysql, postgres or redis)
  -gostdb-url string
        http://gost.com:1325 or DB connection string
  -ovaldb-sqlite3-path string
        /path/to/sqlite3
  -ovaldb-type string
        DB type of goval-dictionary (sqlite3, mysql, postgres or redis)
  -ovaldb-url string
        http://goval-dictionary.com:1324 or DB connection string
  -http string
        -to-http http://vuls-report



```

## Example of three format options 

Vuls has three format options.
- format-list(default)
- format-one-line-text
- format-full-text

### format-list

![report-list](/img/docs/report-format-list.png)

```
$ vuls report

c74 (centos7.4.1708)
====================
Total: 294 (High:65 Medium:198 Low:24 ?:7), 93/294 Fixed, 708 installed, 285 updatable

+------------------+------+----------+---------+---------------------------------------------------+
|      CVE-ID      | CVSS |  ATTACK  |  FIXED  |                        NVD                        |
+------------------+------+----------+---------+---------------------------------------------------+
| CVE-2017-11176   | 10.0 |  Network |   Fixed | https://nvd.nist.gov/vuln/detail/CVE-2017-11176   |
| CVE-2017-12762   | 10.0 |  Network | Unfixed | https://nvd.nist.gov/vuln/detail/CVE-2017-12762   |
| CVE-2017-18017   | 10.0 |  Network |   Fixed | https://nvd.nist.gov/vuln/detail/CVE-2017-18017   |
| CVE-2017-1000158 |  9.8 |  Network | Unfixed | https://nvd.nist.gov/vuln/detail/CVE-2017-1000158 |
| CVE-2017-10684   |  9.8 |  Network | Unfixed | https://nvd.nist.gov/vuln/detail/CVE-2017-10684   |
| CVE-2017-10685   |  9.8 |  Network | Unfixed | https://nvd.nist.gov/vuln/detail/CVE-2017-10685   |
... snip ...
```

### format-one-line-text

```
$ vuls report -format-one-line-text

One Line Summary
================
c74     Total: 294 (High:65 Medium:198 Low:24 ?:7)      93/294 Fixed    708 installed, 285 updatable
deb8    Total: 490 (High:62 Medium:158 Low:22 ?:248)    11/490 Fixed    512 installed
```

### format-full-text

![report-list](/img/docs/report-full-text.png)

```
$ vuls report -format-full-text

c74 (centos7.4.1708)
====================
Total: 23 (High:22 Medium:1 Low:0), 9/23 Fixed, 708 installed, 285 updatable

+---------------+----------------------------------------------------------------------------------+
| CVE-2017-9233 |                                                                                  |
+---------------+----------------------------------------------------------------------------------+
| Max Score     | 7.5 HIGH (nvd)                                                                   |
| nvd           | 7.5/CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H HIGH                            |
| redhat_api    | 6.5/CVSS:3.0/AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:N/A:H MODERATE                        |
| nvd           | 5.0/AV:N/AC:L/Au:N/C:N/I:N/A:P MEDIUM                                            |
| Summary       | XML External Entity vulnerability in libexpat 2.2.0 and earlier (Expat XML       |
|               | Parser Library) allows attackers to put the parser in an infinite loop using a   |
|               | malformed external entity definition from an external DTD.                       |
| Mitigation    |  Do not parse untrusted arbitrary XML data using the expat                       |
|               | package.                                                                         |
| CWE           | CWE-835: Loop with Unreachable Exit Condition ('Infinite Loop') (redhat_api)     |
| CWE           | [OWASP Top4] CWE-611: Improper Restriction of XML External Entity Reference      |
|               | ('XXE') (nvd)                                                                    |
| Affected PKG  | expat-2.1.0-10.el7_3 -> Will not fix                                             |
| Confidence    | 100 / RedHatAPIMatch                                                             |
| Source        | https://nvd.nist.gov/vuln/detail/CVE-2017-9233                                   |
| CVSSv2 Calc   | https://nvd.nist.gov/vuln-metrics/cvss/v2-calculator?name=CVE-2017-9233          |
| CVSSv3 Calc   | https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator?name=CVE-2017-9233          |
| RHEL-CVE      | https://access.redhat.com/security/cve/CVE-2017-9233                             |
| CWE           | https://cwe.mitre.org/data/definitions/CWE-835.html                              |
| CWE           | https://cwe.mitre.org/data/definitions/CWE-611.html                              |
| OWASP Top10   | https://github.com/OWASP/Top10/blob/master/2017/en/0xa4-xxe.md                   |
+---------------+----------------------------------------------------------------------------------+

... snip ...
```

```
c74 (centos7.4.1708)
====================
Total: 23 (High:22 Medium:1 Low:0), 9/23 Fixed, 708 installed, 285 updatable
```

- `c74` means that it is a scan report of `servers.c74` defined in cocnfig.toml.
- `(centos7.4.1708)` means that the version of the OS is CentOS 7.4.
- `Total: 23 (High:22 Medium:1 Low:0)` means that a total of 23 vulnerabilities exist, and the distribution of CVSS Severity is displayed.
- `9/23 Fixed`means` that a total of 23 vulnerabilities exist, and 9 is fixed, 14 is not fixed yet.
- `285 updatable packages` means that there are 285 updateable packages on the target server.

```
+---------------+----------------------------------------------------------------------------------+
| CVE-2017-9233 |                                                                                  |
+---------------+----------------------------------------------------------------------------------+
| Max Score     | 7.5 HIGH (nvd)                                                                   |
| nvd           | 7.5/CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H HIGH                            |
| redhat_api    | 6.5/CVSS:3.0/AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:N/A:H MODERATE                        |
| nvd           | 5.0/AV:N/AC:L/Au:N/C:N/I:N/A:P MEDIUM                                            |
| Summary       | XML External Entity vulnerability in libexpat 2.2.0 and earlier (Expat XML       |
|               | Parser Library) allows attackers to put the parser in an infinite loop using a   |
|               | malformed external entity definition from an external DTD.                       |
| Mitigation    |  Do not parse untrusted arbitrary XML data using the expat                       |
|               | package.                                                                         |
| CWE           | CWE-835: Loop with Unreachable Exit Condition ('Infinite Loop') (redhat_api)     |
| CWE           | [OWASP Top4] CWE-611: Improper Restriction of XML External Entity Reference      |
|               | ('XXE') (nvd)                                                                    |
| Affected PKG  | expat-2.1.0-10.el7_3 -> Will not fix                                             |
| Confidence    | 100 / RedHatAPIMatch                                                             |
| Source        | https://nvd.nist.gov/vuln/detail/CVE-2017-9233                                   |
| CVSSv2 Calc   | https://nvd.nist.gov/vuln-metrics/cvss/v2-calculator?name=CVE-2017-9233          |
| CVSSv3 Calc   | https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator?name=CVE-2017-9233          |
| RHEL-CVE      | https://access.redhat.com/security/cve/CVE-2017-9233                             |
| CWE           | https://cwe.mitre.org/data/definitions/CWE-835.html                              |
| CWE           | https://cwe.mitre.org/data/definitions/CWE-611.html                              |
| OWASP Top10   | https://github.com/OWASP/Top10/blob/master/2017/en/0xa4-xxe.md                   |
+---------------+----------------------------------------------------------------------------------+
```

- `Max` Score` means Max CVSS Score.
- `nvd` shows [CVSS Vector](https://nvd.nist.gov/CVSS/Vector-v2.aspx) of  NVD
- `redhat` shows [CVSS Vector](https://nvd.nist.gov/CVSS/Vector-v2.aspx) of Red Hat OVAL
- `jvn` shows [CVSS Vector](https://nvd.nist.gov/CVSS/Vector-v2.aspx) of JVN 
- `CWE` means [CWE - Common Weakness Enumeration](https://nvd.nist.gov/cwe.cfm) of the CVE.
- `[OWASP Top4]` means the CWE is included in [OWASP TOP 10]( https://github.com/OWASP/Top10/blob/master/2017/en/0x05-introduction.md)
- `Affected PKG` shows the package version information including this vulnerability.
- `Confidence` means the reliability of detection.
  - `100` is highly reliable
  - `YumUpdateSecurityMatch` is the method of detecting this vulnerability.
- Item list of `Confidence`

  | Detection Method       | Confidence         |  OS                              |Description|
  |:-----------------------|-------------------:|:---------------------------------|:--|
  | OvalMatch              | 100                | CentOS, RHEL, Oracle, Ubuntu, Debian, SUSE |Detection using OVAL |
  | YumUpdateSecurityMatch | 100                |               RHEL, Amazon, Oracle |Detection using yum-plugin-security|
  | ChangelogExactMatch    | 95                 | CentOS, Ubuntu, Debian, Raspbian |Exact version match between changelog and package version|
  | ChangelogLenientMatch  | 50                 |         Ubuntu, Debian, Raspbian |Lenient version match between changelog and package version| 
  | PkgAuditMatch          | 100                |                          FreeBSD |Detection using pkg audit|
  | CpeNameMatch           | 100                |                              All |Search for NVD information with CPE name specified in config.toml|

## Example: Specify the path of go-cve-dcitionary, goval-dictionary and gost

config.toml

```
[cveDict]
type = "sqlite3"
path = "/path/to/cve.sqlite3"

[ovalDict]
type = "sqlite3"
path = "/path/to/oval.sqlite3"

[gost]
type = "sqlite3"
path = "/path/to/gost.sqlite3"
```

## Example: Send scan results to HipChat

Define HipChat section in [config.toml](https://vuls.io/docs/en/usage-settings.html#hipchat-section)

```
$ vuls report \
      -to-hipchat \
      -cvss-over=7
```

With this sample command, it will ..

- Send scan results to HipChat
- Only Report CVEs that CVSS score is over 7


## Example: Send scan results to Stride

Define stride Section in [config.toml](https://vuls.io/docs/en/usage-settings.html#stride-section)

```
$ vuls report \
      -to-stride \
      -cvss-over=7
```

With this sample command, it will ..

- Send scan results to Stride
- Only Report CVEs that CVSS score is over 7

## Example: Send scan results to ChatWork

Define ChatWork section in [config.toml](https://vuls.io/docs/en/usage-settings.html#chatwork-section)

```
$ vuls report \
      -to-chatwork \
      -cvss-over=7
```

With this sample command, it will ..

- Send scan results to ChatWork
- Only Report CVEs that CVSS score is over 7

## Example: Send scan results to Slack

Define Slack section in [config.toml](https://vuls.io/docs/en/usage-settings.html#slack-section)

```
$ vuls report \
      -to-slack \
      -cvss-over=7
```
With this sample command, it will ..

- Send scan results to slack
- Only Report CVEs that CVSS score is over 7


## Example: Put results in S3 bucket
To put results in S3 bucket, configure following settings in AWS before reporting.

- Create S3 bucket. See [Creating a Bucket](http://docs.aws.amazon.com/AmazonS3/latest/UG/CreatingaBucket.html)  
- Configure access to S3 resources. You can do this in several ways:
  - Configure the environment variables. See [Configuring the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)
  - Configure the security credentials. See [Configuring the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)
  - Create an IAM role for the service and attach it to the service (EC2, AWS Lambda). [Creating a Role to Delegate Permissions to an AWS Service](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html)
- To configure environment variables, security credentials, create an access key. See [Managing Access Keys for IAM Users](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)


Example of IAM policy:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets"
            ],
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::vuls/*"
        }
    ]
}
```


config.toml

```
[aws]
profile = "default"
region = "ap-northeast-1"
s3Bucket = "vuls"
s3ServerSideEncryption = "AES256"
```

reporting

```
$ vuls report \
      -to-s3 \
      -format-json
```

With this sample command, it will ..

Put scan result(JSON) in S3 bucket 
- with AES256 
- bucket name is "vuls" 
- ap-northeast-1
- profile is "default"
- The Server-side encryption algorithm (e.g., AES256, aws:kms).

## Example: Put results in Azure Blob storage

To put results in Azure Blob Storage, configure following settings in Azure before reporting.
- Create a Azure Blob container

config.toml

```
[azure]
accountName = "default"
accountKey = "xxxxxxxxxxxxxx"
containerName "vuls"
```

```
$ vuls report -to-azure-blob
```

With this sample command, it will ..

Put scan result(JSON) in Azure Blob Storage. 
- container name is "vuls"
- storage account is "test" 
- accesskey is "access-key-string"

account and access key can be defined in environment variables.

```
$ export AZURE_STORAGE_ACCOUNT=test
$ export AZURE_STORAGE_ACCESS_KEY=access-key-string
$ vuls report -to-azure-blob
```

## Example: IgnoreCves

Define ignoreCves in config if you don't want to report(Slack, EMail, Text...) specific CVE IDs.

- config.toml

```toml
[default]
ignoreCves = ["CVE-2016-6313"]

[servers.bsd]
host     = "192.168.11.11"
user     = "kanbe"
ignoreCves = ["CVE-2016-6314"]
```

## Example: IgnoreCves of a contianer

- config.toml

```toml
[default]
ignoreCves = ["CVE-2016-6313"]

[servers.cent7]
host     = "192.168.11.11"
user     = "kanbe"

[servers.cent7.containers.romantic_goldberg]
ignoreCves = ["CVE-2016-6314"]
```

## Example: IgnorePkgsRegexp 

Define ignorePkgsRegexp in config if you don't want to report(Slack, EMail, Text...) match against the specific regexp [google/re2](https://github.com/google/re2/wiki/Syntax).

```
[servers.c74]
host     = "192.168.11.11"
user     = "kanbe"
ignorePkgsRegexp = ["^kernel", "^python"]

[servers.c74.containers.romantic_goldberg]
ignorePkgsRegexp = ["^vim"]
```

## Example: Add optional key-value pairs to JSON

Optional key-value can be outputted to JSON.  
The key-value in the default section will be overwritten by servers section's key-value.  
For instance, you can use this field for Azure ResourceGroup name, Azure VM Name and so on.

- config.toml
```toml
[default]
[default.optional]
	key1 = "default_value"
	key3 = val3


[servers.bsd]
host     = "192.168.11.11"
user     = "kanbe"
[servers.bsd.optional]
	key1 = "val1"
	key2 = "val2"
```

- bsd.json
```json
[
  {
    "ServerName": "bsd",
    "Family": "FreeBSD",
    "Release": "10.3-RELEASE",
    .... snip ...
    "Optional": {
        "key1": "val1" ,
        "key2": "val2" ,
        "key3": "val3" 
    }
  }
]
```

## Example: Use MySQL as a DB storage back-end

config.toml
```
[cveDict]
type = "mysql"
url = "user:pass@tcp(localhost:3306)/dbname?parseTime=true"

[ovalDict]
type = "mysql"
url = "user:pass@tcp(localhost:3306)/dbname?parseTime=true"

[gost]
type = "mysql"
url = "user:pass@tcp(localhost:3306)/dbname?parseTime=true"
```

```
$ vuls report
```

If you get below error message while fetching, define `sql_mode`.

```
Error 1292: Incorrect datetime value: '0000-00-00' for column 'issued' at row 1
```

For details, see TODO

## Example: Use PostgreSQL as a DB storage back-end


config.toml
```
[cveDict]
type = "postgres"
url = "host=myhost user=user dbname=dbname sslmode=disable password=password"

[ovalDict]
type = "postgres"
url = "host=myhost user=user dbname=dbname sslmode=disable password=password"

[gost]
type = "postgres"
url = "host=myhost user=user dbname=dbname sslmode=disable password=password"
```

```
$ vuls report
```

## Example: Use Redis as a DB storage back-end

config.toml
```
[cveDict]
type = "redis"
url = "redis://localhost/1"

[ovalDict]
type = "redis"
url = "redis://localhost/1"

[gost]
type = "redis"
url = "redis://localhost/1"
```

```
$ vuls report
```

