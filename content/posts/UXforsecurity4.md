     1|---
     2|title: "Better Security through Solid UX 4: Example Two, continued"
     3|subtitle: "We look at an example security capability and write some user stories"
     4|date: '2022-12-06'
     5|excerpt: >-
     6|  Last time, we talked through six user stories across three personas in IT Asset Management. Today, I'll walk through what jumped out at me -- please comment with your thoughts and considerations -- there's a lot going on here.
     7|seo:
     8|  title: "Better Security through solid UX 2: Example 2, part 2"
     9|  description: "We explore the user experience of another common security-relevant task: using a CMDB."
    10|  robots: []
    11|  extra: []
    12|layout: post
    13|thumb_img_path: /images/nobodygottime.jpeg
    14|thumb_img_alt: Nobody got time for that
    15|---
    16|Last time, we talked through six user stories across three personas in IT Asset Management. We ended with several challenges:
    17|
    18|-   What other personas should we consider?
    19|-   What other user stories are worth writing?
    20|-   What common threads, root causes, and opportunities do you see?
    21|-   How would you best fix them?
    22|
    23|Today, I'll walk through what jumped out at me -- please comment with your thoughts and considerations -- there's a lot going on here.
    24|
    25|# Identified opportunities
    26|
    27|If you're doing this as an exercise, discuss the user stories with your team. Often, common threads identify themselves, and a single change can address many stories.
    28|
    29|## Thread 1
    30|
    31|These user stories identify the primary cause that limits the accuracy of the CMDB: contributors see no value in it; mostly they're just trying to follow the rules. Academically, they know some groups may use the information, but it doesn't add value to them individually.
    32|
    33|This can be addressed: for IT teams, CMDBs are usually the best platform for managing work about those systems. Health checks, configuration assurance, alerts, and inter-team change requests are often most easily managed from workflows sitting on a CMDB. The alerting systems Frank uses do not seem to be integrated into the CMDB--perhaps other teams would appreciate the same capabilities.
    34|
    35|You can also communicate existing value: identify the core benefits that the CMDB provides to your organization, and [educate teams about it](https://saltyonsecurity.net/posts/securitymarketing/). If it's not providing solid value yet, maybe that's a first step.
    36|
    37|## Thread 2
    38|
    39|The whole point of a CMDB is centralizing data that other people need already. Done right, your Inventory of IT Asset Stuff shouldn't require any re-keying: you should just slurp it out of the generation systems like AD, VMware, and AWS, then use [discovery services](https://saltyonsecurity.net/posts/cis1_3-5/) to capture the rest.
    40|
    41|Manual re-entry of data maintained in another tool is waste. As we have discussed, avoiding [waste](https://www.lean.org/lexicon-terms/muda-mura-muri/) often increases morale, accuracy, and raw efficiency.
    42|
    43|## Thread 3
    44|
    45|The original CMDB build team seem to have only considered use cases for technical IT staff. Is designing for executives also worthwhile? What are other likely user stories for the Sarah persona? How important are they for your overall goals?
    46|
    47|The answer to these questions depends on your organization, but in my experience, IT teams under-estimate the value of engaging non-IT staff in "internal" processes. Building a black-box IT organization where only IT staff do IT activities contributes strongly to Shadow IT. If IT governance and oversight is easy to start at any stage, fewer IT projects will get far down that divergent path.
    48|
    49|# Lessons
    50|
    51|## No clear value
    52|
    53|The most likely root cause for observed frustration might be that the CMDB's value isn't clear. If there is value to its existence and accuracy, it should be narrowly tailored to deliver that value at the least cost and friction to the organization. That value should also be used to drive investment in accuracy such as automatic data sources. If the data is needed, paying people to manually update records is a poor financial decision; each integration will probably pay for itself in several months. If the data is not worth the cost, discontinue the façade of collecting it.
    54|
    55|
    56|| ![Nobody got time for that!](/images/nobodygottime.jpeg) |
    57||:---:|
    58|| *A fundamental truth of human nature: ain't nobody got time, especially for that.* |
    59|
    60|The value proposition of the CMDB will also inform design decisions about the desired experience. If the intended value of the CMDB is merely IT governance such as configuration, patching, and change management, there's no point to recording SaaS apps like Sarah's. If it's used for security, compliance governance, and informing enterprise risk decisions, the CMDB should include SaaS apps and the forms should be adjusted to enable that intent.
    61|
    62|## Not designed for (internal) customers
    63|
    64|Frequently, teams and departments that don't directly serve external customers implicitly prioritize their own efficiency over the teams they serve. This can be a culture problem or KPI problem or even a making-work-visible problem, and it shows up in lots of places.
    65|
    66|Mandatory fields and phone trees are a common way this happens. Every extra step of granularity on an intake form narrows the solution space it addresses. If your fulfillment teams are not focused on solving customer needs, they will change things to make their work easier at the expense of their customers and value provided.
    67|
    68|Sometimes this manifests as "not my job" or "please refile ticket in X", where any request that isn't a perfect match for the service is rejected. Sometimes it shows up as a steady grind of "improvements" that avoid fulfillment frustrations but overall deliver a bad customer experience.
    69|
    70|The conversations usually happen the same way: imagine a network engineer is trying to parse a server request ticket for what segmentation rules apply. The network engineer feels like the world would be a much better place if server requesters just took a minute to understand the current VLAN design and told him where their server should fit, so he petitions the server request team to add "VLAN ID" to the form and make it mandatory so those lazy architects would actually do their job before coming to him to implement their half-baked plan. The network engineer isn't directly affected by the increased frustration that his change caused to requests that don't need VLAN assignment (most of them), so he still sees the change as beneficial, despite potentially costing hundreds of wasted hours every year while maybe saving him ten.
    71|
    72|
    73|| ![A fence in front of a well-trodden path.](/images/myjobisdone.jpeg) |
    74||:---:|
    75|| *Ineffective attempts to control behavior abound.* |
    76|
    77|
    78|Over the next three years, the server request form accumulates eight other mandatory fields that help other fulfillers solve edge cases, but adds time and friction to the form. More and more customers try to circumvent the form or just develop unsanctioned ways of getting through it with the least pain possible.
    79|
    80|# Takeaways
    81|
    82|Do you see other root causes, threads, or possible fixes? If you were tasked by the CIO to fix CMDB accuracy and these were the results of your initial user story generation, what would you do first? What next?
    83|