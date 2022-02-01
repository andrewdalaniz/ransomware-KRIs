# ransomware-KRIs
I was asked how I could provide quantitaive analysis and rationalization to determining the risk of a ransomware attack.  The reality is there isn't one size fits all, but these are the things I would want to look for.  Something I've learned, but had a suprising amount of pushback on, is that it's ok that a metric is always 0. Many of these, once implemented, should never change, but that doesn't change the fact that knowing their position informs risk. 

## prerequisites
- Define Mission Critical apps - those apps that are essential for the business to function and those apps that are required for those apps to function
- Define privileged groups - specifically identity groups (Though parts are a little outdated, there is good reference material [here](https://www.alaniz.io/blog/securing-windows-privileged-access) and [here](https://www.alaniz.io/blog/windows-event-forwarding-resources) that can help with this)

## Primary
|Summary|Category|Target|Description|References|
|-|-|-|-|-|
|MFA coverage for external ingress points|Protect|100%|Without getting into nuances of implementation or the efficacy of technologies, having this is better than not, and if you don't, your risk of ransomware and other compromise is high|
|Management protocols exposed to the internet (MFA or not)|Protect|0|Lets keep it simple. Management interfaces should not be available directly from the internet. Period.|
|EDR Coverage - Workstations|Detect|100%|Some sort of EDR installed, tested, and alerts enabled for non compliance on all workstations of all OS.	This should not be a panacea of security, but assuming we are talking the best in class options, it will cover low hanging fruit.|
|EDR Coverage - Servers|Detect|100%|Some sort of EDR installed, tested, and alerts enabled for non compliance on all workstations of all OS.	This should not be a panacea of security, but assuming we are talking the best in class options, it will cover low hanging fruit.|
|# servers with access to the internet|Protect|0|Many times, for execution of a payload, malware needs to communicate to C2.  This can prevent both infection and communication. Obviously this is very organization specific as well as applciation specific and should be tailored to the need, but erring on the side of less is better.|	
|End user networks restricted from direct access to server networks|Protect|0/Depends|For sure, easier said than done, but the amount of unfettered access from the user networks to server networks has a direct correlation to the risk of malware propogation to server networks. This can contain a lot of the choas from ransomware. Force admin access through bastions, restrict database access, force direct access over HTTPS, etc.|
|# daily connections from end user network to server network over unapproved TCP ports|Detect|TRUE|Know what normal is and look for deviations.|
|Proxy blocks uncategorized and miscellaneous websites|Protect|TRUE|This can go a long way to blocking C2 communication and other 'low hanging fruit' malware connections.|	
|ID of all mission critical processes complete|Identify|TRUE|Just as important as preventing infection is assuming it is going to happen and being prepared to recover.  This is the first step to any other steps related to recovery.|
|Mission Critical Processes that are reliant on network shares|Identify|TRUE|More important than unrestrictd network shares, are the numer of mission critical processes that rely on them.  More than likely Bob's spreadsheet can be reproduced, but if Bob's spreadsheet is critical for the business to generate revenue, then that is another matter entirely if it needs to be available quickly.|	
|Mission critical processes without tested BC/DR|Recover|0|If you haven't tested it, it doesn't work.|
|# standard user accounts in privileged groups|Identify|0|Where standard users are defined as user accts used to check email and browse the internet and these users are members of priv groups - this is a common way for malware to escalate privilege and laterally move.|
|# users who are local admins on their device|Identify|0|Without the ability to install software, malware, like ransomeware, is much harder to propogate.  Any number higher than 0 starts to increase risk of ransomware.|
|LAPS deployed and in use on workstations and servers OR all systems have unique local admin passwords.|Protect|TRUE|This can reduce the risk of lateral movement if a local admin acct is compromised otherwise, memory dumps of local admin credentials can be used to traverse the network.|
|# privileged users that have login righs to workstations|Identify|TRUE|Privileged users shouldn't be logging into workstations (other than PAWS), they usually bring along privileged access with them.  Once privileged credentials are used on a device they can be harvested which allows their use across the network.|	
|# shared local admin accts on workstations|Identify|0|How many tools 'require' local admin rights across all systems? (Vulnerability scanners, configuration systems, deployment systems, asset management tools, etc)|
|# shared local admin accts on servers|Identify|0|How many tools 'require' local admin rights across all systems? (Vulnerability scanners, configuration systems, deployment systems, asset management tools, etc)|
|Restrict network logon for administrators group on workstations enabled|Identify|0|This can go a long way to stopping lateral movement, especially if there are shared usernames.|
|Systems with SMB listening|Identify|TRUE|The more of this that exists, the more likely a ransomware attack will be able to access and encrypt data OR data can be accessed.|	
|System of vendor to VPN connection mapping exists|Identify|Depends|I have seen first hand how a vendor can compromise a network through VPN. It is essential to be able to make a timely and an informed decision to take drastic measures if a vendor has an incident or to protect a vendor if you do.|
|Completeness of system of vendor to VPN connections|Identify|TRUE|This bolsters the previous metric to ensure the system exists.||
|Last comprehensive review of Bloodhound results|Identify|0|This is the only specific vendor product I've mentioned, but it is an essential tool to identify holes in protections against privilege escalation and lateral movement.|[Specterops](https://posts.specterops.io/bloodhound-versus-ransomware-a-defenders-guide-28147dedb73b) and [Bloodhound](https://bloodhoundenterprise.io/)|
|IR plan tested at least quarterly|Respond|TRUE|I don't mean a 'check the box' test, I mean that practice makes perfect, and teams need to know the IR plan like a reflex.||
|IR plan contains actions for contacting law enforcement, DFIR, Legal, Microsoft|Respond|TRUE|Again, if ransomware really does it, no one needs to be spending time researching these things.  This could be a blog post in an of itself, but the processes tied to IR need to be practiced and clear in an event like this.|
|Ransomware tabletop completed within last year|Respond|0|Similar to the other items on the IR plan, ransomware specifically needs to be practiced.||
|Escalation path successfully tested from detection to catastrphic response within minutes|Respond|TRUE|What I mean here is that if ransomware does happen, someone is going to have to very quickly make a decision about cutting off or shutting down key vendors or systems.  Getting to that decision needs to happen very fast.||

## Secondary
|Summary|Category|Target|Description|References|
|-|-|-|-|-|
|Unrestricted Network Shares : Open Network Shares|Protect||||
|Complete application dependenct map of mission critical processes|Identify|0|||
|Kerberoasting detection and response|Detect|0|||
|Golden Ticket compromise detection and response|Detect|0|||
|Members of Administrators global AD group|Identify|0|||
|Priv accts with Sid history|Identify||||
|# domain / enterprise admins|Identify|TRUE|||
|# other priv group members|Identify|TRUE|||
|Number of incidents impacting ‘key’ systems in last X days by system|Identify|0|||
|Kerberoasting SOP complete and recently reviewed|Identify|0|||
|Golden Ticket SOP complete and recently reviewed|Identify|TRUE|||

## Tertiary
|Summary|Category|Target|Description|References|
|-|-|-|-|-|
|MC apps with a single point of failure|Recover|TRUE|||
|Apps of dependent process with RTO less than X and no chaos testing|Recover|TRUE|||
|Non Compliance of MTTR|Recover|TRUE|||
