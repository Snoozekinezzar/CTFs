# BrokenAzure.cloud CTF Challenge Write-Up

This repository contains a detailed write-up for a challenge found on [BrokenAzure.cloud](https://www.brokenazure.cloud/), focusing on the exploitation of Developer Tools and the Security Pane to enumerate and extract sensitive information from Azure storage containers.

## Challenge Overview

The company named SuperCompany B.V. has been working with IT systems for a while now and have an IT team of a whoppin' 2 people. Because the CEO of the company has heard that 'Cloud' is the new way of working, the CEO has asked the IT team to migrate all IT systems to the Azure cloud platform. Sadly, management does not allow the IT team to take courses or trainings to learn more about Azure cloud and so they have to learn as-they-go

## Tools Utilized

- **`enumerate_containers.py`**: A script designed for enumerating accessible storage containers within a given Azure Storage account.
- **`list_blobs_info.py`**: A script aimed at listing details about blobs within a specific container, including file names, sizes, and modification timestamps.

## Procedure and Discoveries

### Enumerating Storage Containers

The first step involved using the `enumerate_containers.py` script to enumerate storage containers within the `supercompanystorage` account, as showcased below:

```bash
┌──(brokenazure㉿ctf)-[~/Github/Tools]
└─$ ./enumerate_containers.py
Enter the Azure Storage account name: supercompanystorage
Container found: storagecontainer
Found Containers: ['storagecontainer']
```
Listing Blob Information
Upon identifying the container name (storagecontainer), the list_blobs_info.py script was executed to enumerate blobs within this container. This process revealed the names, sizes, and last modified dates of the blobs:

```bash
┌──(brokenazure㉿ctf)-[~/Github/Tools]
└─$ ./list_blobs_info.py supercompanystorage storagecontainer

List of blobs:
- Name: Employee23187.ovpn, Size: 2921 bytes, Last Modified: Mon, 08 Aug 2022 11:09:12 GMT
- Name: SECURA{C3RT1F1C3T3}.pem, Size: 3002 bytes, Last Modified: Mon, 08 Aug 2022 11:08:05 GMT
- Name: logo.png, Size: 10763 bytes, Last Modified: Mon, 08 Aug 2022 11:08:05 GMT
```

## Uncovered Flags
This investigative effort led to the identification of several files, one of which contained a flag:

**1st Flag: SECURA{C3RT1F1C3T3}**
<br>
<br>
This flag was located within the file named SECURA{C3RT1F1C3T3}.pem, marking a successful extraction of sensitive data.

## Conclusion
The challenge underscored the critical need for securing Azure storage accounts and containers against unauthorized access. The successful enumeration and extraction of data from inadequately secured containers highlighted potential vulnerabilities, reinforcing the importance of ethical hacking practices and proper authorization prior to conducting vulnerability assessments.
