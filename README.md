# ransomware-KRIs

|Summary|Category|Target|Description|References|
|-|-|-|-|-|
EDR Coverage - Workstations|Detect|100%|Some sort of EDR installed, tested, and alerts enabled for non compliance on all workstations of all OS.	This should not be a panacea of security, but assuming we are talking the best in class options, it will cover low hanging fruit.||
EDR Coverage - Servers|Detect|100%|Some sort of EDR installed, tested, and alerts enabled for non compliance on all workstations of all OS.	This should not be a panacea of security, but assuming we are talking the best in class options, it will cover low hanging fruit.||
|# servers with access to the internet|Protect|0|Many times, for execution of a payload, malware needs to communicate to C2.  This can prevent both infection and communication. Obviously this is very organization specific as well as applciation specific and should be tailored to the need, but erring on the side of less is better.|	
|End user networks restricted from direct access to server networks|Protect|0/Depends|	|
|# daily connections from end user network to server network over unapproved TCP ports|Detect|TRUE|This can contain a lot of the choas from ransomware. Force admin access through bastions, restrict database access, force direct access over HTTPS, etc.	|
|Proxy blocks uncategorized and miscellaneous websites|Protect|TRUE|Know what normal is, and look for deviations.|	
|ID of all missions critical processes complete|Identify|TRUE|This can contain alot of the choas miscellaneous ransomware. Force admin uncategorized through bastions, and misc database uncategorized, force websites over HTTPS, etc.|
|Mission Critical Processes that are reliant on network shares|Identify|TRUE|If we don't have a complete inventory of processes which are critical to the function of an organization, then the ability to measure a number of key indicators is not possible.|	
|Mission critical processes without tested BC|Recover||More important the unrestrictd network shares are the numer of mission critical processes that rely on them.  More than likely Bob's spreadsheet can be reproduced, but if Bob's spreadsheet is critical for the business to generate revenue, then that is another matter entirely.	|
|Complete application depdnenty map of mission critical processes|Identify|0|This means of those processes that have been identified as mission critical, all of them should have recently tested their business continuity procseses. In other words, can they successfully function with loss of technology or degredation of functionality?	|
|Critical apps without recently tested backups|Recover|100%|For each mission critical process, all applications that are required for that procses to function have been identified.|
|# standard user accounts in privileged groups|Identify|0|Of those apps tied to mission critical process, how many have not had their failover or restoration procedures tested recently.|
|# users who are local admins on teir device|Identify|0|Where standard users are defined as user accts used to check email and browse the internet and these users are members of priv groups	|
|LAPS deployed an inuse on workstations and servers OR all systems have unique local admin passwords.|Protect|Depends|Without the ability to install software, malware like ransomeware is much harder to propogate.  Any number higher than 0 starts to increase risk of ransware.|
|# priv users that have login righs to wrokstations|Identify|TRUE|This can reduce he risk of laeral movement if a local admin acct is compromised|	
|# shared local admin accts on workstations|Identify|0|Privileged users shouldn't be logging into workstations (other than PAWS), they usually bring along priv access with them as well the ability to priv ex on a pwnd device.|
|# shared local admin accts on servers|Identify|0|How many tools 'require' local admin rights across all sysetms? (Vulnerability scanners, configuration systems, deployment systems, asset management tools, etc)|
|Restrict network logon for administrators group on workstations enabled|Identify|0|How many tools 'require' local admin rights across all sysetms? (Vulnerability scanners, configuration systems, deployment systems, asset management tools, etc)|
|Systems with SMB listening|Identify|TRUE|This can go a long way to stopping lateral movement, especially if there are shared usernames.|	
|System of vendor to VPN connection mapping exists|Identify|Depends|Possibly the most common way for lateral movement or access to file shares to occur	|
|Completeness of system of vendor to VPN connections|Identify|TRUE|I have seen first hand how a vendor can compromise a network through VPN. It is essential to be able to make a timely and an informed decision to take drastic measures if a vendor has an incident or to protect a vendor if you do.|
|Incoplete review of entries in system of vendor to VPN connnections in last X days|Identify|100%|It is important to know all of these connections, which vendors they tie to, what access they have, and points of contact.|
|Last comprehensive review of Bloodhound results|Identify|0|People leave, vendors are terminated, this needs to be reviewed.|
|IR plan tested at least quarterly|Respond|TRUE|This can be a way APT gets a foot hold.|
|IR plan contains actions for contacting law enforcement, DFIR, Legal, Microsoft|Respond|TRUE|This can be a way APT gets a foot hold.|
|Ransomware tabletop completed within last year|Respond|0|An often overlooked privileged group that can add priv access widely across a Windows network	|
|Escalation pathsuccessfully tested from detection to catastrphic response within minutes|Respond|TRUE|This is the only tool specific (other than Windows) I mention here because it is an instrumental tool in determining paths to priv access which allow far reaching impact.|
|Unrestricted Network Shares : Open Network Shares|Protect||This can be more common than you think if old or merged AD sysetms and can grant hiddent highly privileged rights|
|Kerberoasting detection and response|Detect|0|Fairly self explanatory, but there is no need for anyone to be in this group on a daily basis	|
|Golden Ticket compromise detection and response|Detect|0|This will be a custom list for many orgs, and the numbers will vary.  I suggest making it broad enough to ensure adequaet coverage, but narrow enough so the expected numbers are in the single digits.|
|Members of Administrators global AD group|Identify|0|This is important to understand the stability and recovery capabilities of key sysetms	|
|Priv accts with Sid history|Identify||While this is nto top of mind for many tech focused security experts, it is critical in the recover from a ransomware event, especially for smaller orgs	|
|# domain / enterprise admins|Identify|TRUE|If you detect this, do you know how to respond?	|
|# other priv group members|Identify|TRUE|	If you detect this, do you know how to respond?	|
|Number of incidents impacting ‘key’ systems in last X days by system|Identify|0|This helps to understand the architecture and resiliencyrisk of mission critical systems.	|
|Last cybersecurity insurance review|Identify|0|This should be sysetms where a very low number of hours is expected for downtime, definitely less than 8, probably less than 4. If that is legit the RTO, you should be chaos testing.	|
|Kerberoasting SOP complete and recently reviewed|Identify|0|Any systems who are not meeting their MTTR expectations during incidents and tests	|
|Golden Ticket SOP complete and recently reviewed|Identify|TRUE|	I don’t mean checking a box. If you want to respond to ransomware, this needs to be for real tested.	|
|MC apps with a single point of failure|Recover|TRUE|	Ransomware is going to be an all hands on deck. You don't need to be googling your local FBI office phone number and your forensic consultants sale person.	|
|Apps of dependent process with RTO less than X and no chaos testing|Recover|TRUE|	Again, very specific esting should be taking place.	|
|Non Compliance of MTTR|Recover|TRUE|I know first hand of ransomware taking an organization to its knees in a matter of 10 minutes.  There may be no preventing it if it can spread that fast, but from the point of detection there should be a clear path for anyone involved to get the decision to start drastically shutting down systems and connections within 5-10minutes.	|
