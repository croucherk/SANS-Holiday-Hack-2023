# Phish Detection Agency

This challenge is located in *The Blacklight District* of *Film Noir Island*. Speak to *Fitzy Shortstack* to start the challenge*.

## Situational Awareness

When we open the terminal, we see a menu with 5 options: *Welcom*, *Inbox*, *Phishing*, *DNS*, and *Sponsor*. The Welcome page is the default landing page of the terminal.

![Figure 1: Welcome Screen](/img/phish-detection-menu.png)

The Inbox page contains all of the emails we have received.

![Figure 2: Inbox Screen](/img/phish-inbox.png)

The Phishing page contains all of the emails we have marked as *Phishing*.

![Figure 3: Phishing Screen](/img/phish-phishing.png)

The *Sponsor* page is unimportant, so we will move on to the *DNS* page, which contains all of the records we will use while determining the validity of emails received.

![Figure 4: DNS Heading](/img/phish-dns-header.png)

The first record is the SPF record.

![Figure 5: SPF Record](/img/phish-dns-spf.png)

The second record is the DKIM record. 

![Figure 6: DKIM Record](/img/phish-dns-dkim.png)

The third and final record is the DMARC record.

![Figure 7: DMARC Record](/img/phish-dns-dmarc.png)

## Identifying Phishing Emails

Our methodology for determining whether an email should be marked as a phish begins with us asking three questions about an email?
1. Do the *Return-Path* and/or *Received* headers reference a domain different from the corporate `geeseislands.com` domain?
2. Is the *DKIM-Signature* header missing or referencing a domain different from the corporate `geeseislands.com` domain?
3. Does the email pass the *DMARC* check?

### Phish 1: Invitation to Research Grant Meeting

![Figure 8: Invitation to Research Grant Meeting](/img/phish-unsafe-1.png)

### Phish 2: Urgent IT Security Update

![Figure 9: Urgent IT Security Update](/img/phish-unsafe-2.png)

### Phish 3: Procurement Process Improvements

![Figure 10: Procurement Process Improvements](/img/phish-unsafe-3.png)

### Phish 4: Security Protocol Briefing

![Figure 11: Security Protocol Briefing](/img/phish-unsafe-4.png)

### Phish 5: Public Relations Strategy Meet

![Figure 12: Public Relations Strategy Meet](/img/phish-unsafe-5.png)

### Phish 6: Customer Feedback Analysis Meeting

![Figure 13: Customer Feedback Analysis Meeting](/img/phish-unsafe-6.png)

### Phish 7: Legal Team Expansion Strategy

![Figure 14: Legal Team Expansion Strategy](/img/phish-unsafe-7.png)

### Phish 8: Networking Event Success Strategies

![Figure 15: Networking Event Success Strategies](/img/phish-unsafe-8.png)

### Phish 9: Compliance Training Schedule Announcement

![Figure 16: Compliance Training Schedule Announcement](/img/phish-unsafe-9.png)

### Phish 10: New Research Project Kickoff

![Figure 17: New Research Project Kickoff](/img/phish-unsafe-10.png)

## Conclusion

Once we have marked all 10 phishing emails as *Phishing* and marked the remaining emails as *Safe*, we receive a prompt informing us that the challenge has been completed.

![Figure 18: Challenge Completed](/img/phish-success.png)
