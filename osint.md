# Open Source Intelligence (OSINT)
======
#### Whois Registration Lookup
whois domain.com
#### Arin Whois
<a href="https://whois.arin.net/ui/advanced.jsp">https://whois.arin.net/ui/advanced.jsp</a>
#### Arin Whois
Find other netblocks by throwing in Wildcards to the search.
#### Whois
whois hooperlabs.xyz
#### Wigle
Geolocate MAC Addresses of Wifi Hotspots - <a href="https://wigle.net/">https://wigle.net/</a>
#### Mylnikov (Wigle for Europe)
http://find-wifi.mylnikov.org/
#### Grayhat Warfare
Search publicly-available S3 buckets (useful for borrowing a certificate).
#### Photos of Commercial Buildings
<a href="http://loopnet.com">http://loopnet.com</a>
#### MAC OUI Lookup
curl http://api.macvendors.com/fc-a1-3e-2a-1c-33
#### Shodan
<a href="https://www.shodan.io/"">https://www.shodan.io/</a>
#### Google Dorks

#### List of Subdomains without main page
site:"microsoft.com" -site:"www.microsoft.com" 
#### Web Cams
inurl:"/control/userimage.html" 
#### Useful Operators
filetype,inurl,intitle,
#### Find Directory Listing
intitle:"index of" "parent directory"
#### The Harvester (deprecated?)
theharvester -d cisco.com -b all

## DNS
------
#### Check if DNS resolves (multi-region)
https://dnschecker.org
#### Reverse IP lookup Script
for ip in $(seq 50 100); do host 38.100.193.$ip; done | grep -v "not found"

## Sudomain Enumeration
------
#### SubBrute + MassDNS
python /opt/massdns/scripts/subbrute.py /usr/share/wordlists/dns.top20000.txt domain.com | massdns -r /usr/share/wordlists/dns.resolvers.txt --verify-ip -w massdns.out.txt  -o S
#### MassDNS
massdns -s 15000 -t CNAME -o J -r /usr/share/wordlists/resolvers.txt --flush
#### The Harvester
theharvester -d domain.com -b all -c
#### Sublist3r
sublist3r -d domain.com -b -o outfile.txt
#### Amass
amass enum -passive -include-unresolvable -timeout 10 -d domain.com | tee amass.txt
#### DNScan
dnscan -d domain.com -w /usr/share/wordlists/commonspeak2-subdomains.txt -t 16 -6 -r -o dnscan.txt
#### KnockPy
python knockpy.py domain.com -w /usr/share/wordlists/commonspeak2-subdomains.txt | grep domain.com | cut -d '"' -f2  | tee knockpy.out
#### DNSRecon (not great)
dnsrecon -d domain.com -D /usr/share/wordlists/commonspeak2-subdomains.txt -g -b -k -w -z --threads 16 
#### ALtDNS
altdns  -i subdomains.txt -o altdns.txt -w words.txt -r -s results_outputs.txt
#### ThreatCrowd
+ domain="myDomain.com"
+  curl https://www.threatcrowd.org/domain.php?domain=$domain | grep "$domain'>" | sed "s/$domain.>/\n/g" | grep $domain | cut -d '<' -f1
+  https://www.threatcrowd.org

#### Subdmain Takeover (one-liner)
chaos -d domain.com -silent | nuclei -t nuclei-templates/dns/dead-host-with-cname.yaml
#### Hunt Devs
companyname github linkedin

## Linkedin
------
#### Generate username lists from companies on Linkedin
https://github.com/initstring/linkedin2username

## Git Disclosures
------
#### GitLeaks
https://github.com/zricethezav/gitleaks | docker pull zricethezav/gitleaks
#### GitLeaks Example
docker run --rm --name=gitleaks zricethezav/gitleaks -v -r https://gitlab.com/StraightOuttaCrompton/aws-cdk-static-site
#### Gitrob
https://github.com/michenriksen/gitrob
#### Truffle Hog
https://github.com/dxa4481/truffleHog
#### SHHGit
https://github.com/eth0izzle/shhgit
#### View git log
git log --pretty=oneline
#### Show changes in commit
git show <hash>
#### Fork/Pull Repo
Within UI, fork project; git clone https://github.com/caryhooper/repo.git; git checkout -b new_branch; git remote add upstream https://github.com/username/repo.git; ** make changes and commit **; git push -u origin new_branch
#### Create a new branch
git checkout -b new-feature
#### Delete a branch locally
git checkout -d new-feature
#### Delete a branch remotely
git push origin --delete new-feature
#### Merge branches
git checkout master; git merge branch2
#### Remove added directory
git rm -r --cached .\Scripts\
#### Add a submodule to repo
git submodule add https://example.com/user/repo.git destination_folder
#### Git clone a Branch
git clone --branch recipes git@github.com:caryhooper/hooperlabs
#### Search GitHub for filename
"filename:users"

## Recon-ng
------
#### Search marketplace for modules
marketplace search github
#### Get info about marketplace module
marketplace info recon/domains-hosts/google_site_web
#### Load Module
modules load recon/domains-hosts/google_site_web
#### Get info about current module
info
#### Set Options
options set SOURCE hooperlabs.xyz
#### Go Back a Menu
back
#### Show all hosts discovered
show hosts
#### Install a module
marketplace install recon/hosts-hosts/resolve