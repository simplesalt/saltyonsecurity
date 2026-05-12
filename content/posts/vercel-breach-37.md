     1|---
     2|title: "Lessons from the Vercel Breach"
     3|subtitle: "How to tell if your cloud provider has terrible security; part 37"
     4|date: '2026-05-12'
     5|excerpt: "If your customer data can be stolen because one IT person tried out the wrong software, that is not a 'we got unlucky' failure. That kind of failure says you don't care."
     6|seo:
     7|  title: "Lessons from the Vercel Breach"
     8|  description: "Why we keep having the same problem with PAM, ZSP, and how ZOA fixes all of it."
     9|  robots: []
    10|  extra: []
    11|layout: post
    12|---
    13|
    14|Last month, Vercel announced that sensitive customer information was stolen by hackers over the course of several months, including API keys, tokens, session tokens, and credentials. 
    15|
    16|If you aren't familiar, Vercel is a cloud hosting company much-beloved by the hip appdev crowd. They wrote next.js, and their ecosystem lets you build SaaS apps fast without messing with servers or infrastructure. It Just Works**&reg;**
    17|
    18|## What went wrong
    19|
    20|Long story, short: A Vercel employee tried out some software (Context AI). That software was controlled by criminals and siphoned off everything it could access. This included a huge amount of sensitive information including customer data, so it all got sucked out and sold on the black market. Other criminals bought it and used it to attack those customers, who in turn eventually figured out what was going on and told Vercel, probably in irate, all-caps emails. Vercel publicly acknowledged the breach in mid-April after the crime ring made a ransom demand on a popular forum. 
    21|
    22|Wheeee.
    23|
    24|## The root cause
    25|
    26|If your customer data can be stolen because one IT person tried out the wrong software, that is not a "we got unlucky" failure. That kind of failure says you don't care. 
    27|
    28|IT people are famous for trying new tools. They've got engineery minds and like to tinker and improve things. It's what they're good at. Authorizing Context AI was not a big error. 
    29|
    30|The biggest problem was Vercel's decision to give staff direct access to customer data. There is no need or excuse for this in 2026. This is the same root cause that underlaid Okta's big breach several years ago and Azure's most egregious security failures over the last 5 years. There are many more examples, but this article is already too long; go ask your AI if you want more. 
    31|
    32|Vercel tries to disclaim responsibility because they give customers the ability to prevent access. In their ecosystem, information labelled "secret" prevents access from admins. But this designation is not the default and people follow defaults.  "We let customers restrict access from our admins" just tries to shift blame to customers.
    33|
    34|## Why
    35|
    36|I can guarantee you that the IT admin did not need all this access, but I can guess why they had it. Direct access is control, and control makes us feel safe and cozy. They *needed* the access in case something goes wrong. 
    37|
    38|Because IT people are people, they don't see themselves as a source of failure. They don't see themselves, their account, or their access as a risk. Problems are usually caused by other people, right? Worse, they tend to interpret governance as a personal indictment of their character and judgment: if someone tries to take access away from them, they get offended.
    39|
    40|This blindness makes the benefit of being in control (even if marginal) seem like the safer option.  
    41|
    42|## Vercel's failure is easy to avoid
    43|
    44|So easy! Removing access mostly requires adjustments to process and costs influence with the team you impose governance on. 
    45|
    46|But there's a hidden benefit: it results in higher-performing teams. It's like forcing your teenager to keep their room clean: they resent you for it, but it forces them into habits that help long-term. 
    47|
    48|# What gets me salty
    49|
    50|You would never know that Vercel had this problem from their cyber marketing. I'm sure their SOC2 is spotless, their pen tests were glowing, and ISO 27k cert is probably written by the most respectable consultant you can imagine. 
    51|
    52|But the laziness that caused this problem is not on any security framework except maybe CIS CSC (which almost nobody audits to). There isn't even a standard industry buzzword for being decent at this.  
    53|
    54|## Takeaways
    55|
    56|If you would rather avoid the next breach of this kind, you want cloud vendors that promise either of the following:  
    57|
    58|### ZOA (zero operator access)
    59|
    60|The gold standard. It's got the base "admins have no scary access" plus some fancy HSM and TPM hardware attestations that don't add much protection but get the nerds excited.  
    61|
    62|### ZSP (Zero Standing Privileges) with break-glass governance
    63|
    64|This provides 90% of the protection of ZOA. Unfortunately, there is no single term that describes this standard, so must be manually checked for. ZSP is a specific standard for Privileged Access Management, which we've been doing for decades.
    65|
    66|ZSP promises that IT has no always-on access to dangerous stuff. However, *it is a tech control*, so doesn't mean much. Lazy IT teams under ZSP can still achieve the same default access-to-everything; they just have to click a button first (see, if they click a button, it's not default!).
    67|
    68|To effectively protect customers, ZSP needs to be applied so that dangerous access is only a last resort, break-glass situation: 
    69|
    70|- IT admins only do it in case of Big Bad Problems That Need Immediate Fixing,
    71|- pushing the button for access sets off alarms and notifications
    72|- after they fix the problem, there are calls with senior management about How We Should Not Have That Happen Again
    73|- maybe some indication that they actually completed the plans from that meeting?
    74|
    75|## So...Who?
    76|
    77|The question you've all been waiting for: which cloud providers actually do decently?  
    78|
    79|### AWS
    80|
    81|At the time of writing, only AWS publicly advertises anything in this space. They have a SOC2 attesting to doing ZOA for their most popular services. This means that AWS commissioned an audit to a standard that nobody else is publicly trying to meet. A+ security for AWS, as usual. 
    82|
    83|### Runners up:
    84|
    85|Cloudflare, GCP, and Vultr probably do some ZSP-with-break-glass. This is based on inferences from their publicly-available doc, tech blogs, and of past security incident writeups. 
    86|
    87|### (dis) Honorable Mention?
    88|
    89|Oracle Cloud and IBM Cloud have some marketing copy about ZSP, but given their penchant for grandiose security claims plus years of poor security performance, I doubt they're doing it well. 
    90|
    91|### No indication
    92|
    93|I looked through the publicly-available security doc for the following companies and did not find any public indication that they apply this standard: 
    94|
    95|DigitalOcean, Linode, OVHcloud, Scaleway, Kamatera, Rackspace, fly.io, Hetzner, Alibaba Cloud, Tencent Cloud, Supabase, Render, Railway, Porter, Netlify, Fastly, Civo, UpCloud, Azure
    96|