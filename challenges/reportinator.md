# Reportinator

This challenge is located on *Rudolph's Rest Resort* on *Christmas Island* and is managed by *Noel Boetie*.

> *Note*:
> Completing this challenge was made possible thanks to the help of *tw2k* on Discord.

## Challenge Prompt

If we start a conversation with Boetie, we will learn how to approach the challenge.

![Figure 1: Noel Boetie Conversation](/img/boetie-conversation.png)

Boetie used a *Large Language Model* (LLM)[^1] to generate a penetration testing report. Although impressed with the tool, Boetie has noticed some small issues with the report, including AI *hallucinations*[^2]. They have asked us to proofread the report and identify any incorrect findings or hallucinations.

## Reading the Report

### Report Conventions

The first section of this report is the *Report Conventions*.

![Figure 2: Report Conventions](/img/report-conventions.png)

The *Report Conventions* section is a non-standard section, and is specific to this challenge. There are some key takeaways:
* Findings we determine to be valid should be marked with the green checkbox icon.
* Findings we determine to be hallucinated or incorrect should be marked with the red 'X' icon.
* The IP addresses used in this engagement have been anonymized, meaning we do not need to worry about CIDR notation or subnet masking issues appearing as hallucinations.

### Executive Summary

The second section of this report is the *Executive Summary*.

![Figure 3: Executive Summary](/img/executive-summary.png)

The executive summary is an important part of practically every penetration test report.

According to the summary, the penetration testing firm Santa Clause Security, Inc. (SCS) was hired by the client North Pole Systems (NPS) to evaluate their external facing network assets. The authorized techniques of the engagement are considered standard fare for most external penetration testing engagements. 

At the end of the engagement, five high-risk, two medium-risk, and two low-risk findings were identified, and SCS has provided remediation steps for all findings.

### Scope

The third section of this report is the *Scope*.

![Figure 4: Scope](/img/scope.png)

Prior to a penetration test being performed, all participating parties must deliberate and agree upon a set of defined targets and the allowed methods during the engagement. This is known as the scope agreement.

According to the report, SCS was authorized to perform testing on 2,145 Internet-facing servers owned by NPS. An exhaustive list of the allowed methods was also provided.

## Report Findings

### Vulnerable Active Directory Certificate Service-Certificate Template Allows Group/User Privilege Escalation

![Figure 4: Vulnerable Active Directory Certificate Service-Certificate Template Allows Group/User Privilege Escalation](/img/finding-1.png)

**Observations**: 

Certipy is an Active Directory reconnaissance and exploitation tool targeting vulnerable certificate templates.

One noticable mistake with this finding is the description of the `find -vulnerable` command line option. The finding states that this "option identifies certificate templates that allow users to supply their own subject alternative name (SAN) and determine if a client authentication extended key usage (EKU) is set". While technically true, this is also the default behavior of the `find` option without the `-vulnerable` flag. The `-vulnerable` flag filters the output by showing "only vulnerable certificate templates based on nested group memberships...". While this paragraph could likely be revised, it is not sufficient enough to label as incorrect.

**Determination**: Legitimate

### SQL Injection Vulnerability in Java Application

![Figure 5: SQL Injection Vulnerability in Java Application (1)](/img/finding-2-1.png)

![Figure 6: SQL Injection Vulnerability in Java Application (2)](/img/finding-2-2.png)

**Observations**:

*SQL injection* (AKA SQLi) is a vulnerability in web applications that uses user-supplied input to construct a SQL query without sanitization, leading to breaches in database confidentiality, integrity, and under specific circumstances even remote code execution.

The `sqlmap` utility is a SQL injection reconnaissance and automated-exploitation tool.

There is a possible typo in the *Recommendation* subsection. One of the most common defense mechanisms against SQLi is *data sanitization*, which filters user-supplied input for characters typically associated with SQLi. In this subsection, we see usage of the terms "*sanitation routines*" and "*input sanitation*", whereas the colloquially agreed upon terms would be "sanitization routines" and "input sanitization". Given that there is no centralized authority dictating what this procedure should be referred to as, and the words "sanitation" and "sanitization" are used somewhat interchangeably in plain English already, we will not mark this finding as incorrect.

**Determination**: Legitimate

### Remote Code Execution via Java Deserialization of Stored Database Objects

![Figure 7: Remote Code Execution via Java Deserialization of Stored Database Objects](/img/finding-3.png)

**Observations**:

Java deserialization occurs when data objects that have already been converted into a Java-accessible byte stream (AKA serialization) is recreated in its original object format. Vulnerabilities arise when the classes of these objects use 1) loosely or vaguely defined types for object properties, and 2) those properties invoke custom methods. An attacker can abuse this by creating a malicious object in Java that invokes code execution when the custom method of that object is invoked, and passing it as serialized data to a vulnerable application.

In the *Finding* subsection, the report reads that by "*intercepting HTTP request traffic on 88555/TCP, malicious actors can exploit this vulnerability*". However, the valid port range is 1-64435, which is less than 88555. This is because in TCP/IP networking, the object type of the port number is an unsigned 16-bit integer. 2^16 = 65536, and because the bit range is 0-indexed, the upper bounds is 65535.

**Determination**: Hallucination/Incorrect

### Azure Function Application-SSH Configuration Key Signing Vulnerable to Principal Manipulation

![Figure 8: Azure Function Application-SSH Configuration Key Signing Vulnerable to Principal Manipulation (1)](/img/finding-4-1.png)

![Figure 9: Azure Function Application-SSH Configuration Key Signing Vulnerable to Principal Manipulation (2)](/img/finding-4-2.png)

![Figure 10: Azure Function Application-SSH Configuration Key Signing Vulnerable to Principal Manipulation (3)](/img/finding-4-3.png)

**Observations**:

Undocumented functionality can become a serious issue for web applications.

There are no immediate issues identified in this finding, so we will mark it as correct.

**Determination**: Legitimate

### Azure Key Vault-Overly Permissive Access from Azure Virtual Machine Metadata Service/Managed Identity

![Figure 11: Azure Key Vault-Overly Permissive Access from Azure Virtual Machine Metadata Service/Managed Identity (1)](/img/finding-5-1.png)

![Figure 12: Azure Key Vault-Overly Permissive Access from Azure Virtual Machine Metadata Service/Managed Identity (2)](/img/finding-5-2.png)

**Observations**: 

Broken access control can result in a loss of confidentiality for critical infrastructure.

The syntactically correct command in Listing 2 should be `az keyvault shoow --name NPSVault`, according to Microsoft's Azure CLI reference guide for the Key Vault command[^X]. However, as this is a minor issue and possibly an undocumented alias option, we will not mark the finding as incorrect. 

**Determination**: Legitimate

### Stored Cross-Site Scripting Vulnerabilities

![Figure 13: Stored Cross-Site Scripting Vulnerabilities](/img/finding-6.png)

**Observations**: 

Cross-Site Scripting vulnerabilities occur when attackers can inject JavaScript code into a trusted source and induce execution of malicious code.

The *Finding* subsection references a "*HTTP SEND*" command. However, the only valid HTTP/S methods are `GET`, `HEAD`, `POST`, `PUT`, `DELETE`, `CONNECT`, `OPTIONS`, `TRACE`, or `PATCH`. Therefore, this finding is a hallucination.

**Determination**: Hallucination/Incorrect

### Browsable Directory Structure

![Figure 14: Browsable Directory Structure (1)](/img/finding-7-1.png)

![Figure 15: Browsable Directory Structure (2)](/img/finding-7-2.png)

**Observations**: 

When web server software is configured to display browsable file/directory structures, a user landing on an "empty" page of a server should see a listing for the available files/directories they may navigate to. This is fine in some limited use cases, but should generally be avoided for applications facing untrusted environments like the Internet, because it can enable further attacks by malicious actors.

The alternative configuration provided in Listing 6 is a legitimate option for disabling browseable directories. Another option would be to replace the line `Options -Indexes FollowSymLinks` with `Options FollowSymLinks`.

**Determination**: Legitimate

### Deprecated Version of PHP Scripting Language

![Figure 16: Deprecated Version of PHP Scripting Language (1)](/img/finding-8-1.png)

![Figure 17: Deprecated Version of PHP Scripting Language (2)](/img/finding-8-2.png)

**Observations**: 

The last release of PHP 7.4 was 7.4.33, which has been discontinued since November 3rd, 2022. PHP 7.4 suffered from multiple vulnerabilities, including a critical remote code execution by buffer overflow vulnerability, labeled CVE-2021-21708.

There are no immediate issues identified in this finding, so we will mark it as correct.

**Determination**: Legitimate

### Internal IP Address Disclosure

![Figure 18: Internal IP Address Disclosure (1)](/img/finding-9-1.png)

![Figure 19: Internal IP Address Disclosure (1)](/img/finding-9-2.png)

![Figure 20: Internal IP Address Disclosure (1)](/img/finding-9-3.png)

**Observations**: 

By exposing the IP addresses of devices on the internal network of NPS, an attacker could prepare a more sophisticated attack targeting those hosts.

Just like in finding 6, an invalid HTTP method is provided in the *Finding* subsection, this time referencing a `7.4.33` request. This is the same version number of the PHP scripting language identified in finding 8, indicating a "bleed over" of the LLM from the previous finding that was generated.

**Determination**: Hallucination/Incorrect

## Conclusion

The following findings are to be labeled as legitimate:
* Finding 1: *Vulnerable Active Directory Certificate Service-Certificate Template Allows Group/User Privilege Escalation*
* Finding 2: *SQL Injection Vulnerability in Java Application*
* Finding 4: *Azure Function Application-SSH Configuration Key Signing Vulnerable to Principal Manipulation*
* Finding 5: *Azure Key Vault-Overly Permissive Access from Azure Virtual Machine Metadata Service/Managed Identity*
* Finding 7: *Browsable Directory Structure*
* Finding 8: *Deprecated Version of PHP Scripting Language*

The following findings are to be labeled as hallucinations/incorrect:
* Finding 3: *Finding 3: *Remote Code Execution via Java Deserialization of Stored Database Objects*
* Finding 6: *Stored Cross-Site Scripting Vulnerabilities*
* Finding 9: *Internal IP Address Disclosure*

After submitting our selections, we see the success message.

![Figure 21: Report Review Completed](/img/report-success.png)

[^1]: https://en.wikipedia.org/wiki/Large_language_model
[^2]: https://en.wikipedia.org/wiki/Hallucination_(artificial_intelligence)

[^X]: https://learn.microsoft.com/en-us/cli/azure/keyvault?view=azure-cli-latest#az-keyvault-show
