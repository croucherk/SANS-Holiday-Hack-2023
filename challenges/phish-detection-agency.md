# Phish Detection Agency

This challenge is located in *The Blacklight District* of *Film Noir Island*. Speak to *Fitzy Shortstack* to start the challenge*.

## Situational Awareness

When we open the terminal, we see a menu with 5 options: *Welcom*, *Inbox*, *Phishing*, *DNS*, and *Sponsor*. The Welcome page is the default landing page of the terminal.

![Figure 1: Welcome Screen](/img/phish-detection-menu.png)

The Inbox page contains all of the emails we have received.

![Figure 2: Inbox Screen](/img/phish-inbox.png)

The Phishing page contains all of the emails we have marked as *Phishing*.

![Figure 3: Phishing Screen](/img/phish-phishing.png)

The *Sponsor* page is unimportant, so we will move on to the *DNS* page, which contains all of the DNS records related to phish/spam protection[^1] we will use while determining the validity of emails received.

![Figure 4: DNS Heading](/img/phish-dns-header.png)

The first record is the *Sender Policy Framework* (SPF)[^2] record.

![Figure 5: SPF Record](/img/phish-dns-spf.png)

Let's ask ChatGPT to review what a SPF record does.

![Figure 6: ChatGPT SPF Record Explanation](/img/chatgpt-spf.png)

SPF records list all the IP addresses authorized to send emails from a given domain. If a

The second record is the *DomainKeys Identified Mail* (DKIM)[^3] record. 

![Figure 7: DKIM Record](/img/phish-dns-dkim.png)

Let's ask ChatGPT to review what a DKIM record does.

![Figure 8: ChatGPT DKIM Record Explanation](/img/chatgpt-dkim.png)

DKIM utilize public key *cryptography*[^4]. The organization's private key is stored by the sender, who signs each email that it sends to the mail server. The DKIM record contain the organization's public key, and the DKIM signature of incoming messages are validated by the mail servers receiving the message.

The third and final record is the *Domain-based Message Authentication Reporting and Conformance* (DMARC)[^5] record.

![Figure 9: DMARC Record](/img/phish-dns-dmarc.png)

Let's ask ChatGPT to review what a DMARC record does.

![Figure 10: ChatGPT DMARC Record Explanation](/img/chatgpt-dmarc.png)

DMARC records dictate the domain's policies for mail servers after checking SPF and DKIM records, such as whether to quarantine messages. In this case, the policy of the domain is to *reject* any messages that fail to pass SPF or DKIM checks.

## Identifying Phishing Emails

Our methodology for determining whether an email should be marked as a phish begins with us asking three questions about an email?
1. Do the *Return-Path* and/or *Received* headers reference a domain different from the corporate `geeseislands.com` domain?
2. Is the *DKIM-Signature* header missing or referencing a domain different from the corporate `geeseislands.com` domain?
3. Does the email pass the *DMARC* check?

### Phish 1: Invitation to Research Grant Meeting

![Figure 11: Invitation to Research Grant Meeting](/img/phish-unsafe-1.png)

#### Explanation

This message's DKIM signature identifies it as being sent from another domain, but the message attempts to spoof[^6] the sender address to appear as if it was coming from the `geeseislands.com` domain. It therefore does not pass the DMARC check.

### Phish 2: Urgent IT Security Update

![Figure 12: Urgent IT Security Update](/img/phish-unsafe-2.png)

#### Explanation

This message's DKIM signature is invalid, so it does not pass the DMARC check.

### Phish 3: Procurement Process Improvements

![Figure 13: Procurement Process Improvements](/img/phish-unsafe-3.png)

#### Explanation

This message's DKIM signature fails integrity checks, so it does not pass the DMARC check.

### Phish 4: Security Protocol Briefing

![Figure 14: Security Protocol Briefing](/img/phish-unsafe-4.png)

#### Explanation

This message appears to pass the DMARC check indicating that SPF and DKIM checks were valid, but the *Received* header indicates that the original source of this email was an unauthorized domain. The *From* address does not match the *Received* header.

### Phish 5: Public Relations Strategy Meet

![Figure 15: Public Relations Strategy Meet](/img/phish-unsafe-5.png)

#### Explanation

This message appears to pass the DMARC check indicating that SPF and DKIM checks were valid, but the *Return-Path* and *Received* headers indicate that the original source of this email was an unauthorized domain. The *From* address does not match the *Received* header.

### Phish 6: Customer Feedback Analysis Meeting

![Figure 16: Customer Feedback Analysis Meeting](/img/phish-unsafe-6.png)

#### Explanation

This message's DKIM signature is missing, so it does not pass the DMARC check.

### Phish 7: Legal Team Expansion Strategy

![Figure 17: Legal Team Expansion Strategy](/img/phish-unsafe-7.png)

#### Explanation

This message's DKIM signature appears to come from an unauthorized domain, so it does not pass the DMARC check.

### Phish 8: Networking Event Success Strategies

![Figure 18: Networking Event Success Strategies](/img/phish-unsafe-8.png)

#### Explanation

This message's DKIM signature is invalid, so it does not pass the DMARC check.

### Phish 9: Compliance Training Schedule Announcement

![Figure 19: Compliance Training Schedule Announcement](/img/phish-unsafe-9.png)

#### Explanation

This message appears to pass the DMARC check indicating that SPF and DKIM checks were valid, but the *Return-Path* and *Received* headers indicate that the original source of this email was an unauthorized domain. The *From* address does not match the *Received* header.

### Phish 10: New Research Project Kickoff

![Figure 20: New Research Project Kickoff](/img/phish-unsafe-10.png)

#### Explanation

This message appears to pass the DMARC check indicating that SPF and DKIM checks were valid, but the *Return-Path* and *Received* headers indicate that the original source of this email was an unauthorized domain. The *From* address does not match the *Received* header.

## Conclusion

Once we have marked all 10 phishing emails as *Phishing* and marked the remaining emails as *Safe*, we receive a prompt informing us that the challenge has been completed.

![Figure 21: Challenge Completed](/img/phish-success.png)

[^1]: https://www.cloudflare.com/learning/email-security/dmarc-dkim-spf/
[^2]: https://www.cloudflare.com/learning/dns/dns-records/dns-spf-record/
[^3]: https://www.cloudflare.com/learning/dns/dns-records/dns-dkim-record/
[^4]: https://csrc.nist.gov/glossary/term/public_key_cryptography
[^5]: https://www.cloudflare.com/learning/dns/dns-records/dns-dmarc-record/
[^6]: https://www.cloudflare.com/learning/email-security/what-is-email-spoofing/
