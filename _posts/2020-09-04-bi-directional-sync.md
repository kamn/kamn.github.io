---
title : Law of Requisite Variety and two-way data sync
date: 2020-09-04
---
Data syncing is a problem that can be underestimated.
It seems very easy on the face of it.
If you have and control System A, it can be easy to ingest data into A from System B.
Then at some point a requirement to bi-directional sync A and B is presented.
The managers or executives think it should be easy as playing a Reverse Uno card!

It is not and the main issue is one of data constraints.
Going back to the controlling System A and integrating with System B.
In any two-way sync of systems, what should happen if System A does something that is 'invalid' in System B.
At that point they are out of sync and what happens after that?
Ignore that difference?
Alert the user?
Do the 'reasonable' thing?
If someone does it different is always unreasonable.

There is also the reverse case. 
What if System B does something that System A(your system) does views as invalid?
The same questions apply but often the result is a hack to allow input into System A.

Then what happens if you have multiple modifications in A and B that don't sync across?
Which system is right at that point?
The last change is the easy answer but often you only have access to when the field was changed only the object.
A modified [Segal's law](https://en.wikipedia.org/wiki/Segal%27s_law) can apply here

> "A man with a system knows what is correct. A man with two systems is never sure"

This boils down to the [Law of Requisite Variety](http://requisitevariety.co.uk/what-is-requisite-variety/).
Basically you need to have System A have as many options, actions and constraints as System B.
For every 'action' of System B there need to be a reaction from System A.
In order words if you want to have "complete" two-way sync that is "seamless" what you are really saying is "I want to recreate System B on top of our System A"
Which can be a major undertaking but there are three ways to deal address this.

## Change Nothing
Actually implement a full bi-directional sync.
You become an expert at understanding System B.
You know everything it can and cannot do.
What the constraints and valid states are.
You subscribe to their changelogs and try to start a business partnership with them. 

I think this would only work if it is a larger company.
There needs to be some buffer or a large enough revenue stream from other places to accomplish this.
I honestly think that just buying the other company would be a better solution then it because an issue of integration of two product to hopefully increase revenue.

## Restrictions
One answer is to restrictions.
Have a set of actions where the reaction is just 'not syncable'.

For example maybe System B had multiple, complex field types like Country.
The Country field has a list of valid options like "France" or "South Korea" and if you try an invalid option then System B will return an error code.
You can exclude Country field from the sync and only sync simple fields like a String or Number.
This way there is less complexity and less responses you have to go through and you are ignore and freeing your program from worrying about a set of reactions.

If you want to sync with something restrict the options.
Maybe only certain data rows or fields are synced.
Maybe you can only read certain field but not write them.

This is actually what most bi-directional and 'seamless' syncs do.
It is sort of seamless if you squint and ignore some gotchas.
It is mainly a marketing tactic which people take too literally.

## Open the APIs
This is really clever since it combines the above two options and offloads the cost to a third-party.
See the issue with Restrictions is that you have to decide what to and a customer might had make a different choice than you. You need good documentation and result code on for System A and they can require more features but only if it makes sense for what System A already does.

## Conclusion

You have three options with bi-directional syncs

- Implement it
- Add Constraints 
- Open up APIs

These can be mixed around of course but it is painful when people assume it is an potential easy problem when it also might potential be very hard.
In any case you can use constraints and open apis to make the code simpler, delivery faster and the overall experiences within the company and for your customers better.