# Cloud Pentesting
======
#### SME
<a href="https://twitter.com/dafthack">@dafthack</a>

## Cloud Pentest Authorization
------
#### Cloud vs On-Prem
+ Traditional attacks, but a difference angle
+  Post-compromise results in new challenges
+  More room for misconfiguration
+  Higher risk to organizations because services used by employees are now public-facing.

#### Getting a Shell
Once you get a shell, you can query the metadata service (in AWS).
#### Things To Consider
```
What are you allowed to test?
Check each cloud provider's rules before testing.
Refrain from: DoS, intense fuzzing, phishing cloud providers, testing other company's assets.
Report platform vulnerabilities to cloud platforms.
```

## Cloud Authentication Methods
------
#### First Step
Find Authentication Points (APIs, certificates, MFA, etc.)
#### List
+ Password Hash Synchronization
+  Pass Through Authentication
+  Active Directory Federation Services (ADFS)
+  Certificate-based auth
+  Conditional access policies
+  Long-term access tokens
+  Legacy authentication portals

#### Azure: Password Hash Synchronization
Azure AD Connect Service constantly synchronizes AD passwords to cloud.  This allows users to directly authenticate to Azure services like O365 with their internal domain credential.  
#### Azure: Pass-Through Authentication
Credentials only stored on prem.  On-prem agent validates authentication requests to Azure AD (no creds stored in cloud).  
#### Azure: Active Directory Federation Services
Federated trust between Azure and on-prem ADFS server 
#### Azure: Certificate-based Authentication
Client certs for authentication to API.  Certificates are managed in legacy Azure Service Management (impossible to know who created a cert).  
#### Azure: Access Tokens
Authenticate to Azure with oAuth tokens, which may be re-used on other MS endpoints.  Desktop CLI tools that can be used to auth store access to tokens on disk.
#### AWS: Progammatic Access - Access + Secret Keys
SecretAccessKey and Access Key ID for authenticating via scripts and CLI.
#### AWS: Management Console Access

#### GoogleAuthentication Methods
+ Web Access
+  API - OAuth 2.0 protocol
+  Access Tokens (short-lived access tokens for service accounts)
+  JSON Key Files (long-lived key-pairs)
+  Credentials can be federated


## Reconnaissance
------
#### Asset Discovery (find what services are in use)
Examples: AD connectivity, mail gateways, web apps, file storage, etc. (traditional host discovery still applies).
#### WhoIs
Use Whois to determine where they are hosted.  (Microsoft, Amazon, Google IP space usually indicates cloud service).  
#### MX Records
Can show cloud-hosted mail providers (also proofpoint).  O365 - target-domain.mail.protection.outlook.com.  G-Suite - google.com | googlemail.com.  Proofpoint - pphosted.com.
#### Tools
recon-NG, OWASP Amass, spiderfoot, gobuster, sublist3r.
#### Search Engines
Use Google (or whatever dorks)
#### Certificate Transparency
Monitors/Logs Digital certificates.  Cert.sh allows search of certificate transparency logs.  Check out ctfr.py.
#### Internet-Wide Scans
massscan, Shodan.io, Censys.io
#### DNS Brute Forcing
Be creative, use good lists.
#### Compare Footprint to Cloud Netblocks
Azure (https://www.microsoft.com/en-us/download/details.aspx?id=ID: Public 56519, US Gov 57063, Germany 57064, China 57062.  AWS Netblocks - https://ip-ranges.amazonaws.com/ip-ranges.json.  Google Netblocks (change often and there is a Google script for that).  
#### O365 Usage (check 1)
Authenticate with target domain name.
#### O365 Usage (check 2)
https://login.microsoftonline.com/getuserrealm.srf?login=username@company.com&xml=1 (federated = ADFS, isfederated=true) | https://outlook.office265.com/autodiscover/autodiscover.json/v1.0/test@company.com?Protocol=Autodiscoverv1
#### Google Cloud Mail Usage
Sign in to google with the account and if you're prompted for a password, you're good.  
#### AWS S3 Buckets
Web Application Pentests... in scope!

## Exploiting Misconfigured Cloud Assets
------
#### S3 Buckets
stands for Amazon Simple Storage Service (https://bucketname.s3.amazonaws.com | https://s3-[region].amazonaws.com/OrgName)
#### Data in Public Azure Blobs 
 Microburst
#### Data in Public Google Storage Buckets
Cloud_Enum @initstring, scans all three cloud services for buckets and enumerates.
#### AWS Exploitation Framework (Rhino Security)
https://github.com/RhinoSecurityLabs/pacu
#### Import Keys into AWS CLI
sudo aws configure
#### List all Modules
pacu> list
#### Run Module
pacu> run s3__bucket_finder -d glitchcloud
#### List AWS S3 Bucket
pacu> aws s3 ls  s3://glitchcloud
#### Download AWS S3 Bucket
pacu> aws s3 sync  s3://glitchcloud s3-files-dir (https://glitchcloud.s3.amazonaws.com/index.html)
#### Data in Public Azure Blogs
Microburst (NetSPI), Invoke-EnumerateAzureBlobs

## Gaining a Foothold
------
#### Secrets in GitHub Repos
https://github.com/eth0izzle/shhgit

## Password Spraying
------
#### Microsoft Online (Azure/O365)
```
POST /common/oauth2/token HTTP/1.1
Accept: application/json
Content Type: application/x www form urlencoded
Host: login.microsoftonline.com
Content Length: 195
Expect: 100 continue
Connection: close
resource=https%3A%2F%2Fgraph.windows.net&client_id=1b730954 1685 4b74 9bfd
dac224a7b894&client_info=1&grant_type= password&username =user%40targetdomain.com&passwor
d=Winter2020&scope= openid
```
#### Azure Password Protection
Prevents users from picking certain words/seasons/company names.
#### Azure Smart Lockout
Locks out auth attempts whenever brute force or spray attempts are detected (bypassed with https://www.github.com/ustayready/fireprox + MSOLSpray)

## Phishing
------
#### Targets
Cloud Engineers, Developers, DevOps
#### Strategies
Credential Harvesting, Session Hijacking
#### 2FA Session Hijack
Use Evilginx2 and Modlishka.  Hijack Session? Move fast.
#### Phishing G-Suite
Silently inject events into target calendars w/reminder

## Post-Compromise Recon
------
#### Web Server Exploitation
Creds in Metadata service, certificates, environment variables, storage accounts.  
#### Steal Access Tokens
On a web server, look in ~/.config/gcloud/credentials.db
#### Cloud Keys in Files
"\bin
#### Azure Publish Settings files
.publishsettings may contain Base64-encoded ManagementCertificate (no password)
#### Web Config & App Config Files
Include cleartext credentials & frequently need read/write access to cloud storage or DBs.  
#### Steal Access Tokes (.azure file)
Check %USERPROFILE%\.azure\ for authentication tokens.  Also search .json context files and for "TokenCache.dat"

## Difference Between Cloud Services
------
#### AWS vs Azure vs Google Cloud Platform
</pre><img src="img/cloudservices.png"><pre>
#### Azure Subscriptions
An Organization can be an Azure tenant and have Azure users without any subscriptions.  Subscriptions are basically like software licenses.  
#### Azure Hierarchy
Management Groups >> Subscriptions >> Resource Groups >> Resources
#### Azure - User Information (Roles)
Built-In Roles include Owner, Contributor, Reader, User Access Administrator
#### Get current user's role assignment
Get-AzRoleAssignment
#### Enumerate All Users and Groups
Get-MSolUser -All; Get-MSolGroup -All; Get-MSolGroupMember -GroupObjectId <GUID> | gl
#### Azure Runbooks
How to automate tasks in Azure.  Get-AzAutomationAccount; Get-AzAutomationRunbook -AutomationAccountName <name> -ResourceGroupName <groupname>
#### Export an Azure Runbook
Export-AzAutomationRunbook -AutomationAccountName <name> -ResourceGroupName <name> -Name <name> -OutputFolder .\Desktop\
#### User Powershell's Get-Credential
$cred = Get-Credential
#### Azure Privilege Escalation
O365 customer?  That service sets up 200+ service principals (ex. Microsoft Graph, SharePoint, etc).  If you have an application administrator account, it can change passwords for service principals that has more privileges.  

## Cloud Server Administration
------
#### Export EC2 Instance as VMDK
aws ec2 create-instance-export-task --instance-id i-0ea3fb1f63fd5d3ec --target-environment vmware --export-to-s3-task "file://C:\Temp\aws.json"
