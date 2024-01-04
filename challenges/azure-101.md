# Azure 101

This challenge is located at *Rudolph's Rest* on *Christmas Island*, talk to *Sparkle Redberry* to start the challenge.

## Prompts and Answers

1. You may not know this but the Azure cli help messages are very easy to access. First, try typing `az help | less`:

**Answer**:

```bash
az help | less
```

**Explanation**:



![Figure 1: Piping the Results of `az help` into `less`](/img/azure-101-1.png)

2. Next, you've already been configured with credentials. Use 'az' and your 'account' to 'show' your current details and make sure to pipe to less ( | less ).

**Answer**:

```bash
az account show | less
```

**Explanation**:



![Figure 2: Piping the Results of `az account show` into `less`](/img/azure-101-2.png)

3. Excellent! Now get a list of resource groups in Azure. For more information: https://learn.microsoft.com/en-us/cli/azure/group?view=azure-cli-latest

**Answer**:

```bash
az group list
```

**Explanation**:



![Figure 3: Listing Resource Groups in Azure](/img/azure-101-3.png)

4. Ok, now use one of the resource groups to get a list of function apps. For more information: https://learn.microsoft.com/en-us/cli/azure/functionapp?view=azure-cli-latest

**Answer**:

```bash
az functionapp list --resource-group northpole-rg1
```

**Explanation**:



![Figure 4: Listing the Function Apps of the *northpole-rg1* Resource Group](/img/azure-101-4.png)

5. Find a way to list the only VM in one of the resource groups you have access to. For more information: https://learn.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest

**Answer**:

```bash
az vm list --resource-group northpole-rg2
```

**Explanation**:



![Figure 5: Listing the VM that the *northpole-rg1* Resource Group has Access to](/img/azure-101-5.png)

6. Find a way to invoke a run-command against the only Virtual Machine (VM) so you can RunShellScript and get a directory listing to reveal a file on the Azure VM. For more information: https://learn.microsoft.com/en-us/cli/azure/vm/run-command?view=azure-cli-latest#az-vm-run-command-invoke

**Answer**:

```bash
az vm run-command invoke --name NP-VM1 --resource-group northpole-rg2 --command-id RunShellScript --scripts 'ls -al'
```

**Explanation**:



![Figure 6: Running Arbitrary System Commands on the *NP-VM1* Virtual Machine](/img/azure-101-6.png)
