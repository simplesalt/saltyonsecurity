     1|---
     2|title: CIS 2.4 - Discovery
     3|excerpt: >-
     4|  The biggest risk from software is vulnerabilities and packaged malware. The
     5|  best way to start addressing that is to know what software is out there.  
     6|date: '2021-11-22'
     7|seo:
     8|  title: CIS 2.4 - Discovery
     9|  description: What is more helpful than a list of IT Stuff? Knowing what each thing does!
    10|  extra:
    11|    - name: 'og:type'
    12|      value: article
    13|      keyName: property
    14|    - name: 'og:title'
    15|      value: CIS 2 Explained
    16|      keyName: property
    17|    - name: 'og:description'
    18|      value: >-
    19|        What is more helpful than a list of IT Stuff? Knowing what each thing
    20|        does!
    21|      keyName: property
    22|    - name: 'og:image'
    23|      value: images/messydesktops.png
    24|      keyName: property
    25|      relativeUrl: true
    26|    - name: 'twitter:card'
    27|      value: summary_large_image
    28|    - name: 'twitter:title'
    29|      value: CIS 2 Explained
    30|    - name: 'twitter:description'
    31|      value: >-
    32|        What is more helpful than a list of IT Stuff? Knowing what each thing
    33|        does!
    34|    - name: 'twitter:image'
    35|      value: images/messydesktops.png
    36|      relativeUrl: true
    37|layout: post
    38|thumb_img_path: images/messydesktops.png
    39|thumb_img_alt: Messy desktops
    40|---
    41|> CIS 2.4: Utilize software inventory tools, when possible, throughout the enterprise to automate the discovery and documentation of installed software.
    42|
    43|This one's not too hard if you're not going for perfect. Let's get into it.
    44|
    45|## Why
    46|
    47|Most of the CIS value in governing installed software comes from desktops and laptops. First, they are exposed to far more internet than most other devices, and most compromise comes in from the internet. Second, you have people opening attachments, and clicking on things, often with localadmin. Finally, they are doing risky things: sending payments, typing passwords, and working with secret information.
    48|
    49|The biggest risk from ungoverned software is vulnerabilities. The more software you have on a machine, the more bugs there are in total within that software. The more bugs, the more security-impacting bugs. The more security-impacting bugs, the more opportunities for malware to find a foothold.
    50|
    51|The other major risk is from packaged malware: sometimes free software comes with a virus. This is especially common on poorly governed software sites like fosshub, cnet, and sourceforge. Many virus distributors leverage genuine software to push installs: they download a popular pieces of software, modify the installer to also include their virus, then upload it to a software site other than the official one. People searching for the software are then tricked into installing their version instead and get infected. This method became especially popular within the warez community: illegal copies of software [often come with a virus](https://www.bleepingcomputer.com/news/security/pirated-software-is-all-fun-and-games-until-your-data-s-stolen/).
    52|
    53|Alternately, even the authoritative source for a piece of software can be a source of compromise: if the original author transfers control of the project to someone else, that person could introduce malware in subsequent versions. These supply chain [attacks](https://portswigger.net/daily-swig/supply-chain-attacks-against-the-open-source-ecosystem-soar-by-650-report) are on the rise, and even a [pedigreed, popular program](https://www.bleepingcomputer.com/news/security/filezillas-use-of-bundled-offers-sparks-outrage-from-users/) can be a source of malware.
    54|
    55|Desktops accumulate all sorts of junk. When people need to solve a new problem, their first instinct is to find a program that fixes it.
    56|
    57|![](/images/messydesktops.png)
    58|
    59|As much as we'd like them to care about the indicators of risky software, they won't, and it's unreasonable to expect them to. The specific knowledge that makes for an excellent Manufacturing Quality Engineer has no overlap with the knowledge to assess the risk of downloaded software.
    60|
    61|Knowing what Peggy the QE has installed on her desktop doesn't solve this problem: you'll need some of the other CIS 2 controls as well; they all work together.
    62|
    63|In addition to the larger CIS 2 goals, an inventory delivers two advantages:
    64|
    65|*   It helps you understand the size of your problem and risk. Knowing there are 3 installs of [SVG Viewer](https://adobe.fandom.com/wiki/Adobe_SVG_Viewer), 400 installs of [AutoHotkey](https://www.autohotkey.com/), and 3000 installs of [Teamviewer](https://www.teamviewer.com/en-us/) can give you valuable insight into risk across your organization, allowing you to make a case for resources and to prioritize improvements.
    66|*   It can be a great way to verify that security work had the desired effect. For instance, if Jeff says he patched his server but the discovery engine reports the old version, you may need to check in again.
    67|
    68|## How
    69|
    70|Except for Linux-native tools, you usually need an agent on each machine you're discovering. The manner and strategy of each depends highly on the device type and OS. Authenticated vulnerability scanning engines (CIS 7.5) can often also deliver software discovery, but often end up fronting leveraging native OS capabilities. [Tenable](https://www.tenable.com/plugins/nessus/20811), [Rapid7](https://docs.rapid7.com/insightvm/authenticated-discovery-scans/), and [Qualys](https://www.qualys.com/docs/asset-inventory-datasheet.pdf) are the major players in that space. EDR clients (CIS 12.7 and probably 10.1) also sometimes provide this.
    71|
    72|Like your auto-discovered Inventory of IT Stuff, your discovered software list can be used by other teams. Many tools in this area are actually aimed at other teams. This includes Infrastructure management and licensing management - either defending against licensing audits or detecting whether people actually use software in order to pull it. Popular choices include [Flexera](https://www.flexera.com/flexera-one/it-asset-management/software-asset-management.html) and [Snow](https://www.snowsoftware.com/solutions/software-asset-management) for licensing and [BMC](https://www.bmc.com/it-solutions/bmc-helix-discovery.html), [Track-It](https://www.trackit.com/it-asset-management-software/), and [SolarWinds](https://www.solarwinds.com/-/media/solarwinds/swdcv2/licensed-products/service-desk/resources/datasheets/service-desk-discovery-datasheet.ashx) for infrastructure.
    73|
    74|The data is also frequently used by mature infrastructure teams for patching. Knowing what software is installed on which systems can help them target common or critical combinations of installed software for more rigorous regression testing.
    75|
    76|**Overall Approach** : you do not need to do agent installs everywhere; *you're not going for perfect*. Start with discovering software on your worker endpoints - laptops and desktops first, then maybe phones. If there's an existing software discovery capability in IT, get access and help champion it. If there's no software discovery for servers, don't bother: just push for CIS 4 and pick it up along the way.
    77|
    78|### Linux
    79|
    80|You get a lot of excellent software discovery capabilities built into linux, especially if you're using software managed by your linux publisher. apt and yum maintain libraries of perfectly tagged software, and most of the linux ecosystem even allows proprietary software to be installed through these mechanisms through adding repositories. They also deliver patches this way.
    81|
    82|If you have a lot of software that's manually installed, these tools will not know about it. While you can install software discovery agents, don't spend any effort: such manual installation approaches are usually indicative of low-security capabilities in other ways, and your time would be better spent converting the manual process to a more governed pattern.
    83|
    84|Example: if you run software just as an extracted tarball of code, you probably have a script or procedure for "installing": where to get the tarball (maybe with a hardcoded credential to log into the sftp site), where to extract it, a repermissioning step, etc. Maybe this script was provided by your vendor. Each of these steps runs against the security model for linux, and you'll be better off pushing your vendor to stand up a repo with proper version data and cryptographic code signing that you can just point to.
    85|
    86|Some linux-native development languages and frameworks have other library/package management that come with them: we have composer for PHP and and npm for javascript. These development libraries aren't really software in the CIS 2 sense, and are much better managed within your CI/CD pipeline than directly on each server running that code. As with containers, you should manage library dependencies as part of your software package.
    87|
    88|Because linux does this so naturally, the best configuration management tools (ansible, puppet, chef) hook into apt and yum, governing software everywhere it's installed. If you're invested in linux, it may make more sense to focus on CIS 4 using one of these tools; you'll knock out CIS 2 along the way.
    89|
    90|## Mobile Devices
    91|
    92|In many ways, discovering software on iOS and Android are functionally equivalent to managing linux, but you spend money to do it. The software discovery is usually part of a larger configuration governance solution, with the trade category of Mobile Device Management (colloquially MDM, which is also used to refer to Master Data Management. Too many TLAs, I tell ya.)
    93|
    94|Both iOS and Android have authoritative software repositories. Just like apt and yum, they have excellent package metadata, data/access sandboxing, adding additional repositories for proprietary software, and use the whole system for patching. They call them app stores and I'm not gonna get into [the petty](https://veritasbusinesslaw.com/apple-sued-amazon-over-app-store-trademark-generic-and-descriptive-terms/) trademark squabbles.
    95|
    96|JAMF is popular for Apple products, and MobileIron and Intune can cover both iOS and Android devices. Intune has nice hooks into the rest of the Microsoft ecosystem, including slick integrations into their CASB. You can push device-level and sometimes app configuration per CIS 4 with most such solutions. Apparently, there's also [whole slew of upstarts](https://www.google.com/search?q=mdm+solutions) I haven't heard of. If you've used one and have thoughts, I'd love to hear them.
    97|
    98|## Windows Servers
    99|
   100|Often inventorying server software don't add a lot of useful, actionable information: IT teams usually know what's installed, and know why it needs to be there. In these circumstances, just talking to them and creating manual lists or architectural diagrams will yield better results: independently knowing that SAP is installed on the SAP servers and Sailpoint is installed on the Sailpoint servers isn't gonna help you much. Knowing that there's a parallel install of Java 1.4 on half your sailpoint servers might, but only for the purposes of the vulnerability management in CIS 7.
   101|
   102|Microsoft is working toward an apt/yum approach with Windows. They've had SCCM for a while, which functions as a DIY repo, but is lacking in dependency management, good metadata, and ultimately requires expertise and a team. They've also started creating a response to ansible, chef, and puppet with [DSC](https://docs.microsoft.com/en-us/powershell/scripting/dsc/getting-started/wingettingstarted), but it looks half-built and I'm not sure if it's yet ready to meaningfully manage anything. If you've used it in a production environment, I'd love to talk.
   103|
   104|## Windows desktops
   105|
   106|As discussed, these are usually messy, and we'll explore more about why in other CIS 2 articles. For the purposes of CIS 2.4, just get an agent on them, get the data digestible, and try not to let the mess bother you. Depending on the quality of the scanner you use, it may pick up gray-area software: browser plugins, portable binaries, and apps installed into the user home directory. If it doesn't, don't worry about it too much - other CIS 2 controls will address them.
   107|
   108|**Note** : Microsoft is building a copycat of yum and apt called The Windows Store. It shows promise and has substantial security benefit over the free-for-all of the last 30 years. When possible, you should encourage it over manual installs, especially for simple software that doesn't need bundled config. Still, it covers a minority of your software and is functionally useless for CIS 2.4 or CIS 4.
   109|
   110|## Summary
   111|
   112|I see this control decreasing in importance: every year more functions move to webapps. The only big need is for heavy resource requirements: data crunching, 3D modeling, video editing, compiling code, and gaming. Even [these](https://aws.amazon.com/quicksight/)[ are slowly](https://visualstudio.microsoft.com/services/github-codespaces/) [moving to](https://www.autodesk.com/products/autocad-web-app/overview) [cloud-native](https://www.nvidia.com/en-us/geforce-now/) designs. I admit that Word for Web is way more annoying than regular Word, but that poor experience is solely Microsoft's design decisions; there's no architectural reason why they need to be different experiences.
   113|
   114|This is a good thing, too: webapp architectures permit better resiliency, data segmentation, and patching, and desktops become easier to keep secure and healthy.
   115|
   116|Join me next week as we learn about what to do with all this wonderful data with CIS 2.3.
   117|