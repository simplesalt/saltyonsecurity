---
title: "Lessons from the Vercel Breach"
subtitle: "How to tell if your cloud provider has terrible security; part 37"
date: '2026-05-12'
excerpt: "If your customer data can be stolen because one IT person tried out the wrong software, that is not a 'we got unlucky' failure. That kind of failure says you don't care. You would never know that Vercel had this problem from their cyber marketing. I'm sure their SOC2 is spotless, their pen tests were glowing, and ISO 27k cert is probably written by the most respectable consultant you can imagine. But the laziness that caused this problem is not on any security framework except maybe CIS CSC (which almost nobody audits to). There isn't even a standard industry buzzword for being decent at this."
seo:
  title: "Lessons from the Vercel Breach"
  description: "The core issue is common, easy to fix, but hard for a buyer to detect. Here's how to avoid the next one."
  robots: []
  extra: []
layout: post
thumb_img_path: /images/blanket.webp
thumb_img_alt: your blanket
---

Last month, Vercel announced that sensitive information was stolen by hackers over the course of several months, including API keys, tokens, session tokens, and credentials. 

if you aren't familiar, Vercel is a cloud hosting company much-beloved by the appdev crowd. They wrote next.js, and their ecosystem lets you build SaaS apps fast without messing with servers or infrastructure. It Just Works**(R)**

## What went wrong

Long story, short: A Vercel employee tried out some software (Context AI) and authorized an oauth against their IdP. That software was controlled by criminals and siphoned off everything it could directly access, which was a huge amount of sensitive information including customer data. They sold it on the black market. Other criminals bought it and used it to attack those customers. Vercel publicly acknowledged the breach in mid-April after the crime ring made a ransom demand on a public format. 

## The root cause

Some have said that the employee is to blame: they authorized an overbroad oidc scope. To this, I say hogwash. If your customer data can be stolen because one IT person tried out the wrong software, that is not a "we got unlucky" failure. That kind of failure says Vercel doesn't care. 

IT people are famous for trying new tools. They've got engineery minds and like to tinker and improve things. It's what they're good at. Any reasonable threat model must assume that tech folk will periodically try to run or authorize malicious code. 

The issue was Vercel's decision to give staff direct access to customer data. There is no need or excuse for this in 2026. This is the same root cause that underlaid Okta's big breach several years ago and Azure's most egregious security failures over the last 5 years. There are many more examples, but this article is already too long; go ask your AI if you want more. 

Some have said that the customers are at fault, because in Vercel's ecosystem, information labelled "secret" prevents access from admins. But this designation is not the default. Vercel's threat model must assume that people will store data in the easiest (ie default) place that works.  If Vercel truly wanted to protect customer data, they would protect the easy path. "We _let_ customers restrict access from our admins" just shifts blame.

## Why

I can guarantee you that the IT admin did not need all this access, but I can guess why they had it. Direct access is control, and control makes us feel safe and cozy. They *needed* the access in case something goes wrong. 

![safe and cozy!](/images/blanket.webp) |
|:---:|
| *having control: humanity's blankie since 500k BC.* |

Because IT people are people, they don't see themselves as a source of failure. Problems are usually caused by other people, right? They don't see themselves, their account, or their access as a risk. Worse, they tend to interpret governance as a personal indictment of their character and judgment: if someone tries to take access away from them, they get offended.

This blindness makes the benefit of being in control (even if marginal) seem like the safer option.  

## Vercel's failure is easy to avoid

So easy! Removing access mostly requires adjustments to process and costs influence with the team you impose governance on. 

But there's a hidden benefit: it results in higher-performing teams by forcing them into reliable processes. It's like making your teenager clean their room regularly: they resent you for it in the moment, but they'll thank you for it later. 

## What gets me salty

You would never know that Vercel had this problem from their cyber marketing. I'm sure their SOC2 is spotless, their pen tests were glowing, and ISO 27k cert is probably written by the most respectable consultant you can imagine. 

But the laziness that caused this problem is not on any security framework except maybe CIS CSC (which almost nobody audits to). There isn't even a standard industry buzzword for being decent at this.  

## Takeaways

If you would rather avoid the next breach of this kind, you want cloud vendors that promise either of the following:  

### ZOA (zero operator access)

The gold standard. It's got the base "admins have no scary access" plus some fancy HSM and TPM hardware attestations that don't add much protection but get the nerds excited.  

### ZSP (Zero Standing Privileges) with break-glass governance

This provides 90% of the protection of ZOA. Unfortunately, there is no single term that describes this standard, so must be manually checked for. ZSP is a specific standard for Privileged Access Management, which we've been doing for decades.

ZSP promises that IT has no always-on access to dangerous stuff. However, *it is a tech control*, so doesn't mean much. Lazy IT teams under ZSP can still achieve the same default access-to-everything; they just have to click a button first (see, if they click a button, it's not default!).

To effectively protect customers, ZSP needs to be applied so that dangerous access is only a last resort, break-glass situation: 

- IT admins only do it in case of Big Bad Problems That Need Immediate Fixing,
- pushing the button for access sets off alarms and notifications
- after they fix the problem, there are calls with senior management about How We Should Not Have That Happen Again
- maybe some indication that they actually completed the plans from that meeting?

## So...Who?

The question you've all been waiting for: which cloud providers actually do decently?  

### AWS

At the time of writing, only AWS publicly advertises anything in this space. They have a SOC2 attesting to doing ZOA for their most popular services. This means that AWS commissioned an audit to a standard that nobody else is publicly trying to meet. A+ security for AWS, as usual. 

### Runners up:

Cloudflare, GCP, and Vultr probably do some ZSP-with-break-glass. This is based on inferences from their publicly-available doc, tech blogs, and of past security incident writeups. 

### (dis) Honorable Mention?

Oracle Cloud and IBM Cloud have some marketing copy about ZSP, but given their penchant for grandiose security claims plus years of poor security performance, I doubt they're doing it well. 

### No indication

I looked through the publicly-available security doc for the following companies and did not find any public indication that they apply this standard: 

DigitalOcean, Linode, OVHcloud, Scaleway, Kamatera, Rackspace, fly.io, Hetzner, Alibaba Cloud, Tencent Cloud, Supabase, Render, Railway, Porter, Netlify, Fastly, Civo, UpCloud, Azure
