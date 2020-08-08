---
title: Uncertainty
date: 2020-08-07
---

I recently read an article titled [Most tech content is bullshit](https://www.aleksandra.codes/tech-content-consumer).
It was a good, short article about asking questions and thinking about why tech tutorials, designs, and patterns are done certain ways because often there are bullshit reasons.
I agree with it wholeheartedly but I think it is more of a symptom of something deeper. 
Something where society praises certainty and shuns uncertainty, that infects not just developers but everyone.

I have rarely been as confident of my opinions as others have been of theirs.
For most of my career, I looked up to those people.
They 'knew' what was going on. 
Only slowly did I realize that they didn't actually 'know'. 
It was often a mixed bag of motivations from not second-guessing themselves, to having unvoiced assumptions, to just not wanting to look bad, to sinisterly wanting others to look bad so they look good.

People who are certain appear confident and everyone loves confidence.
This is doubly true when you are an outsider looking in. Like non-technical business leaders or recruiters. 
This can be a Fake-It-Till-You-Make(i.e. they grow into a 'good' developer) but also it can turn out like the Emperors New Clothes(i.e. a not 'good' but never uncertain developer)
Few want to risk looking dumb when someone seems so sure and that can make mt at least feel crazy.

Once a contractor was asked by my CTO to enable CORS in the nginx layer without any code modification to our services.
The conversation we had after he did this was a little intense.

Contractor: I enabled the CORS headers and CORS should be working

Me: It is not returning the OPTIONS call correctly

Contractor: What does the OPTIONS call have to do with CORS?

Me: The OPTIONS call is part of a preflight for CORS [linked article]

Contractor: I don't see what some call your service cannot handle has to do with CORS

Me: ...but it is part of CORS. Did you read the article?

Contractor: I have done this for companies for several years and I have never had to do anything with OPTION calls. 

In the middle of that conversation I started to doubt myself. Did OPTIONS have anything to do with CORS? I read multiple articles to make sure I was at least somewhat right. Eventually we figured out a solution. What struck me though is that the implication that the contractor didn't know something was meet with some resistance by him. He was certain he understood it better than he really did.

I read somewhere that the goal of the Socratic method wasn't really to find truth but arrive at a state of aporia or puzzlement and causes personal growth.
We all must act somehow, make some decision about technology or pattern or bug fix. 
The problem is we(or at least I) feel like we need to be certain before making a decision.
This often means deluding ourselves or just lying to get to work.
I don't have a clean solution to this crisis. 
I just have some dictums I think of, my favorite of those is 'I might be wrong but I might be right'.
Hopefully being a little more uncertain becomes more in vouge.