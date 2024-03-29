# ICACLS
======
#### Fact
icacls preserves the canonical order of ACE entries as explicit denials, explicit grants, inherit denials, inherited grants.
#### Set ACLs to default inherited ACL for all ma(T)ching files in (Q)uiet mode and (C)ontinue on errors
echo,Y|icacls C:\Windows\Fonts\*.exe /T /Q /C /RESET
#### Grant everyone read access to file
echo,Y|cacls C:\Windows\Fonts\conhost.exe /G everyone:r
#### Add System and Hidden attributes to file
attrib +s +h "C:\Windows\Fonts\d1lhots.exe"

## Permissions (Simple Rights)
------
#### F
full access (create+delete+read+write+edit)
#### M
modify access (create+delete+read+write)
#### RX
read and execute
#### R
read-only
#### W
write-only
#### N
no access
#### D
delete access

##  Permissions (Specific Rights)
------
#### D{E}
delete
#### RC
read control
#### WDAC
write DAC
#### WO
write owner
#### S
synchronize
#### AS
access system security
#### MA
maximum allowed
#### GR
generic read
#### GW
generic write
#### GE
generic execute
#### GA
generic all
#### RD
read data/list directory
#### WD
write data/add file
#### AD
append data/add subdirectory
#### REA
read extended attributes
#### WEA
write extended attributes
#### X
execute/traverse
#### DC
delete child
#### RA
read attributes
#### WA
write attributes

## Permissions - (Inheritance Rights / directories only)
------
#### (OI)
object inherit (ACE inherited by this folder and files)
#### (CI)
container inherit (ACE inherited by this folder and subfolders)
#### (IO)
inherit only (ACE will be inherited, but does not apply to object itself)
#### (NP)
do not propagate inherit (ACE only inherited one level deep)
#### (I)
permission inherited from parent container
#### Grant all users control
icacls C:\folder /grant "everyone":(OI)(CI)M