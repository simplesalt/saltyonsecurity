     1|---
     2|title: Why CIS
     3|excerpt: >-
     4|  The Critical Security Controls (CIS, aka CIS Top 20) is a great framework.  Many other people think so too; it's exploded in popularity in the last 10 years.  There are 4 big reasons why.
     5|date: '2020-12-10'
     6|seo:
     7|  title: Why CIS
     8|  description: >-
     9|    The CIS Controls say the most important thing to do to secure your computers is to have a list of all your stuff.
    10|  extra:
    11|    - name: 'og:type'
    12|      value: article
    13|      keyName: property
    14|    - name: 'og:title'
    15|      value: Why CIS
    16|      keyName: property
    17|    - name: 'og:description'
    18|      value: >-
    19|        The CIS Controls say the most important thing to do to secure your computers is to have a list of all your stuff.
    20|      keyName: property
    21|    - name: 'twitter:card'
    22|      value: summary_large_image
    23|    - name: 'twitter:title'
    24|      value: Why CIS
    25|    - name: 'twitter:description'
    26|layout: post
    27|---
    28|The Critical Security Controls (CIS, aka CIS Top 20) is a great framework.  Many other people think so too; it's exploded in popularity in the last 10 years.  There are 4 big reasons why. 
    29|
    30|# 1\. Timing
    31|
    32|When it came out, the CIS essentially said, "The best way to be more secure is to do DevOps, and here's how."  At the time, DevOps was the New Hot Thing, and the existing dominant frameworks (NIST 800-53 and ISO 27001) didn't address DevOps approaches.  People jumped on, and continue to jump as they embrace DevOps. 
    33|
    34|# 2\. Marketing
    35|
    36|The ideas and structure of the CIS are the easiest to understand and communicate.  There are many examples. 
    37|
    38|For example, the first CIS control is "know what computers you use."   CIS provides built-in education and explanation: CIS 1 is the most important because, "You can't protect what you don't know about."  This idea makes sense to everyone, and connects to similar ideas in culture:
    39|
    40|*   "Knowing is half the battle"
    41|*   "The first step is admitting you have a problem"
    42|*   The Dunning-Kruger Effect
    43|
    44|![Dunning Kruger effect graph](/images/dunning-kruger.webp)
    45|
    46|Another example: CIS is structured to start with the easiest wins.  It advertises that, "80% of compromises would have been prevented by doing the top 4 controls."   By starting with the most important ideas, it naturally gives priority and makes security less overwhelming: "If you do nothing else, do this".  It reinforces this by explaining that lower controls often depend on doing higher controls: "If you do pen tests but haven't patched your vulnerabilities, you are wasting your time."
    47|
    48|3\. It's hard and fast
    49|
    50|The ideas in CIS Top 20 are specific and easy for technical people to understand and apply.  Consider CIS 8.5:
    51|
    52|<pre>Configure devices to not auto-run content from removable media.</pre>
    53|
    54|![autoplay GPO](/images/autoplayGPO.png)
    55|Most IT administrators know exactly how to do this.  For Windows computers, it's a setting that they can go click, and is also available by GPO.  In Linux, it's a setting within a configuration file, and enforceable with Ansible.  This idea boils down to, "make sure all the computers have the right box checked" in their settings.  Either it's checked or it's not.  
    56|
    57|By contrast, consider ISO 27002 control 6.3f:
    58|
    59|> When designing a backup plan, the following items should be taken into consideration:
    60|>
    61|>...
    62|>
    63|> f.  in situations where confidentiality is of importance, backups should be protected by means of encryption.
    64|
    65|If you're a backup admin and asked to do this control, there's a lot of subjective decisions you need to make:
    66|
    67|*   For which backups does "confidentiality is of importance" apply?  You don't have the time to go analyze the data stored in every backup.  
    68|*   What if some boring application changes purpose and starts storing deep secrets?  How would you know that now it needs encryption?
    69|*   How strong does the encryption need to be?
    70|*   Should you just encrypt all the backups?  Is that worth the extra cost in processing power?
    71|*   Should you just follow the vendor default setting for encryption and then later say, "Yeah, I considered encryption." 
    72|
    73|In any case, these decisions mean meetings, which you hate.  And you know that because they're subjective, any auditors or change in leadership may question those decisions, which means revisiting this whole stupid exercise again and another set of meetings, with no guarantee that the next set of auditors or leaders won't change direction again. 
    74|
    75|There are several judgement calls in CIS, but substantially fewer than in other frameworks. 
    76|
    77|# 4\. It's Cheap
    78|
    79|Access to the CIS is free - just go to the website and download it.  Commercial frameworks like ISO, SSAE18, or HITRUST can cost hundreds in licensing to use.  Compared to the cost of doing all the ideas, that is not a big deal.  However, a lot of people looking for a framework are going to go with the free option because of the lower effort to just look at it. 
    80|
    81|Most importantly, it doesn't cost much time to read and use the CIS.  The whole thing is about 5000 words, of which 1000 are headings.  Compare this to ISO 27002 with 32,000 words or NIST 800-53 with 93,000 words.  And they have subject-specific addendums!