     1|---
     2|title: CIS 1 Explained
     3|excerpt: >-
     4|  The CIS Controls say the most important thing to do to secure your computers is to have a list of all your stuff. They're a little unclear by what this means and how it helps.
     5|date: '2020-12-10'
     6|seo:
     7|  title: CIS 1 Explained
     8|  description: >-
     9|    The CIS Controls say the most important thing to do to secure your computers is to have a list of all your stuff.
    10|  extra:
    11|    - name: 'og:type'
    12|      value: article
    13|      keyName: property
    14|    - name: 'og:title'
    15|      value: CIS 1 Explained
    16|      keyName: property
    17|    - name: 'og:description'
    18|      value: >-
    19|        The CIS Controls say the most important thing to do to secure your computers is to have a list of all your stuff.
    20|      keyName: property
    21|    - name: 'og:image'
    22|      value: images/knowing-is-half.webp
    23|      keyName: property
    24|      relativeUrl: true
    25|    - name: 'twitter:card'
    26|      value: summary_large_image
    27|    - name: 'twitter:title'
    28|      value: CIS 1 Explained
    29|    - name: 'twitter:description'
    30|      value: >-
    31|        The CIS Controls say the most important thing to do to secure your computers is to have a list of all your stuff.
    32|    - name: 'twitter:image'
    33|      value: images/knowing-is-half.webp
    34|      relativeUrl: true
    35|layout: post
    36|---
    37|The [CIS Controls](https://www.cisecurity.org/controls/cis-controls-list/) (formerly known as the Critical Security Controls and the CIS Top 20) say the most important thing to do to secure your computers is to have a list of all your stuff.
    38|
    39|They're a little unclear by what this means and how it helps.
    40|
    41|The title tries to be specific: "Inventory and Control of Hardware Assets." Per Merriam Webster, _asset_ means an owned item of value. Even if we add "hardware," this could include lots of things: pizza boxes, mice, cables, radios, floppy diskettes, CNC lathes, security cameras, and monitors.
    42|
    43|This is not what CIS is after.
    44|
    45|# Why?
    46|
    47|There are four big benefits to knowing what stuff you have.
    48|
    49|*   Almost every subsequent CIS control relies on this inventory in some way.
    50|*   All the subsequent controls that rely on this inventory need owners.
    51|*   Security is only as strong as your weakest link. A complete inventory is the starting point to completely applying some control to your environment.
    52|*   You want to know when new things show up on the network.
    53|
    54|With these goals in mind, it's clear that your inventory shouldn't just have hardware assets - it should have everything that could be broken into.
    55|
    56|Some may argue that at its core, all computing is actually done on physical hardware, so maybe it's enough to only track those. This is a bad plan; here are three examples:
    57|
    58|*   Containering - If an application is containered and moving around on nodes in a cluster with 30 other containered apps, it's not very helpful to say that one of the physical nodes had an out-of-date version of Java last Thursday - the vulnerability was probably within the container, and should be addressed by the container owner/publisher.
    59|*   Virtualization - It's not uncommon for a machine with a hypervisor to host hundreds of virtual machines, each with unique vulnerabilities.
    60|*   Web hosting - a single webserver can host thousands of websites, and serves the correct one based on the url listed in an incoming request.
    61|
    62|# So what?
    63|
    64|It is difficult to formulate a single explanation describing all and only the things that should be in your inventory.
    65|
    66|Prioritizing our asset inventory by the capabilities that need it can help narrow things down. Most of those processes depend on two pieces of information about each asset:
    67|
    68|*   Where to find it ("address")
    69|*   Who can fix problems on it ("owner")
    70|
    71|Those processes also don't care much about components - mice and monitors and northbridges and cables.
    72|
    73|# What counts?
    74|
    75|In our age of layered computing abstractions, what does it mean to "act like a computer"?
    76|
    77|Coupled with the above priorities, we get:
    78|
    79|> _A thing that stores and processes data accessible from a primary address and accountable to a single unique person._
    80|
    81|It doesn't really matter how you define "thing" - owner is often the best place to start.
    82|
    83|There are some good rules of thumb.
    84|
    85|# Owners
    86|
    87|Ownership can also get complicated. Often teams will divide computings by layer:
    88|
    89|*   Bob and his team might own an ESX cluster and its component rackmounts and SAN.
    90|*   Jane and her team manage the 10 Linux VMs (all hosted on Bob's cluster)
    91|*   Edith's team develops and supports 4 JVMs hosted on 10 of those Linux VMs using Tomcat
    92|*   Sanjay owns the reverse proxy, caching server, and WAF that present those web applications at a public address (all hosted on Bob's cluster).
    93|*   Gloria manages the customer service team that help the Sales Reps and customers that use a CRM hosted by each of the IT teams above.
    94|*   Chad is the Executive VP of Sales, sponsored the CRM buildout, and manages the sales team.
    95|
    96|Who "owns" the resulting CRM application or overall capability it helps deliver?
    97|
    98|Many security teams will ignore the way teams have organized ownership and blindly assign security problems to those who maintain the bottom or top of the stack. Security teams need to educate themselves on how their IT customers organize themselves and engage them only in areas they can affect.
    99|
   100|If devices have never had an owner, it usually means that ownership doesn't take a lot of time, which means that it's not a big deal to assign someone to it.  Across the whole organization, there's no downside to assigning owners.  When deciding who should own something, err on the side of lower on the totem pole.  If an IP clock is assigned to the CIO, there's no way that CIO will practically do anything to manage it.  
   101|
   102|Assigning ownership can reduce blind spots in an organization.
   103|
   104|See other posts for detailed techniques to build and _maintain_ an accurate and dependable **Inventory of IT Stuff**, including:
   105|
   106|*   [CIS 1: Why?](/cis1/)
   107|*   [The Mission (CIS 1.1)](/cis1_1/)
   108|*   [Discovery (CIS 1.3-1.5)](/cis1_3-5/)
   109|*   [Useful Information (CIS 1.1, part 2)](/cis1_1_2/)
   110|*   [Standard Work (CIS 1.2)](/cis1_2/)