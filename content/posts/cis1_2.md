     1|---
     2|title: CIS 1.2 - Standard Work
     3|excerpt: >-
     4|  There are several standard processes that most organizations will need to keep the inventory healthy and credible.  Some can be integrated with existing processes, but none can be totally eliminated.  CIS 1.2 proscribes the largest and most important kind of standard work: triage.  
     5|date: '2020-12-10'
     6|seo:
     7|  title: CIS 1.2 - Standard Work
     8|  description: >-
     9|    CIS 1.2 proscribes the largest and most important kind of standard work: triage. 
    10|  extra:
    11|    - name: 'og:type'
    12|      value: article
    13|      keyName: property
    14|    - name: 'og:title'
    15|      value: CIS 1.2 - Standard Work
    16|      keyName: property
    17|    - name: 'og:description'
    18|      value: >-
    19|        CIS 1.2 proscribes the largest and most important kind of standard work: triage. 
    20|      keyName: property
    21|    - name: 'og:image'
    22|      value: images/knowing-is-half.webp
    23|      keyName: property
    24|      relativeUrl: true
    25|    - name: 'twitter:card'
    26|      value: summary_large_image
    27|    - name: 'twitter:title'
    28|      value: CIS 1.2 - Standard Work
    29|    - name: 'twitter:description'
    30|      value: >-
    31|        CIS 1.2 proscribes the largest and most important kind of standard work: triage. 
    32|    - name: 'twitter:image'
    33|      value: images/knowing-is-half.webp
    34|      relativeUrl: true
    35|layout: post
    36|---
    37|> Ensure that a process exists to address unauthorized assets on a weekly basis. The enterprise may choose to remove the asset from the network, deny the asset from connecting remotely to the network, or quarantine the asset.
    38|
    39|
    40|There are several standard processes that most organizations will need to keep the inventory healthy and credible.  Some can be integrated with existing processes, but none can be totally eliminated.  CIS 1.2 proscribes the largest and most important kind of standard work: triage.  
    41|
    42|It also implies a new security goal for the **Inventory**: know when a bad thing gets connected.  We usually talk about compromise as the takeover of existing, good assets.  The next most popular option is build or connect new bad things.  This can take many forms: a WiFi exploit box, a new VM, or just a boring old server or workstation pre-loaded with Kali and some scripts.  
    43|
    44|If you're running a IaaS/PaaS like AWS, this is the main way to be infected: new assets (instances) can be almost instantly spun up using the same APIs that make managing AWS so easy, then maintain themselves faster than you can block or delete them.  They can also hide in platforms that you've never used or seen - if a script creates a new Lambda, S3, and EC2 instance - you'd have half a chance of finding those, but what if they spin up an EKS or Beanstalk instance?  You may not even know what those services do!  Finding and eliminating compromise in a cloud environment like AWS or Azure is perhaps the must infuriating game of whack-a-mole you can image.  
    45|
    46|CIS has it right: the best way to fix this situation is to never get into it: automatically learn when new assets are created or attached, then do some standard things when they first show up.  This will require some technical and organizational prep, but gives you great, actionable visibility when bad things happen.  
    47|
    48|# Triage
    49|
    50|Assuming you've also built discovery services per CIS 1.3-1.5, you'll probably have a steady flow of things that show up on your network, but aren't yet in your inventory.  You'll want to triage these to ensure they aren't malicious, especially in IaaS environments.  Strong change management and NAC (see [CIS 13.9](/cis13_9)) can reduce the number.  
    51|
    52|If your network team has a standard process to add new switches and WAPs, it should be easy for them to update your Inventory of IT Stuff at the same time.  Server teams and container teams and desktop teams and manufacturing teams and everyone else can probably do the same.  Some of these teams may do it automatically - Vsphere can be configured to capture a lot of the critical information you decided on in CIS 1.5 during the VM creation process.  An API can then insta-feed it into your Inventory, which then lines up with the next active discovery scan, and everything is wonderful.  
    53|
    54|If you've done this and are lucky, mostly what you'll see are false positives.  Cowboys in your "devops" team will keep spinning up new instances without telling anyone, and [Alexa-enabled séance candles](https://www.kickstarter.com/projects/candletouch/candle-touch-the-first-smart-connected-real-flame-candle) will keep showing up in your CMO's corner office.  
    55|
    56|Somehow, you need to vet each of these things, but you'll need to strike a balance: applying more governance will add friction every time someone needs to create an asset.  Don't waste the time of your internal customers.  If they think your process is useless, they'll figure out ways to avoid it.  
    57|
    58|For most organizations, the best balance assumes that if all the required fields are present the Inventory, the asset is supposed to be there.  The biggest factor is the Owner field, because it functions as a signoff: someone is saying, "yes, this IT asset is supposed to be here; I am responsible if it has problems."  If needed, you can even have reasonableness checks on owner assignment as further assurance:
    59|
    60|*   Is the account that created the asset different from the owner?  
    61|*   If not, maybe it's ok if they are on the same team?  
    62|*   Does the owner's role in the organization appropriate?  
    63|*   Is the owner a contractor?  Maybe you want to assign it to someone a little more permanent?  
    64|
    65|The heaviest approach is to disallow access to anything that isn't explicitly known and provisioned.  This is usually done with a NAC solution like 802.1X or similar.  This makes the vetting easy - new IT assets won't really work until they meet all your requirements.  See the upcoming article on CIS 13.9 NAC for the best ways to do this.  
    66|
    67|# Data Quality Management
    68|
    69|To keep your inventory accurate, it's best to assign someone to get and address regular reports of wrongness in your **Inventory**.  Some popular choices include:
    70|
    71|*   Duplicate (or possibly duplicate) assets
    72|*   Verify owners after role changes or employee departures.  
    73|*   Validate field contents after someone creates an inventory record
    74|*   Deactivate or purge stale assets.  If your active discovery engine hasn't seen something in a while, maybe it's even worth notifying the owner?
    75|*   differences between what the discovery service found and what's in the inventory.  
    76|
    77|I covered approaches for this in [CIS 1.1: The Mission](/cis1_1).  
    78|
    79|See other posts for detailed techniques to build and _maintain_ an accurate and dependable **Inventory of IT Stuff**, including:
    80|
    81|*   [CIS 1: Why?](/cis1/)
    82|*   [The Mission (CIS 1.1)](/cis1_1/)
    83|*   [Discovery (CIS 1.3-1.5)](/cis1_3-5/)
    84|*   [Useful Information (CIS 1.1, part 2)](/cis1_1_2/)
    85|*   [Standard Work (CIS 1.2)](/cis1_2/)