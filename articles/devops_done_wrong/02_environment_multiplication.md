Environment Multiplication
==========================

Systems development has been cursed recently with the blessings of "DevOps",
making it somewhat cheaper to spin up very large amounts of very similarly
configured servers.

When software developers noticed this, one of the first things they did was to
convince management they need more environments to satisfy different audiences
(other developers - QA & testing - integration - paying clients).

Project management happily agreed, thinking this would introduce some level of
risk management: As the myth goes, what has successfully deployed to both Test
and Integration environments will not cause production outages.

This is probably a sensible measure if you have a piece of software generating
large amounts of dollars: legacy applications running on mainframes.

Yet with the advent of virtual machines, every niche group within a firm now
wants their own environment: There are data integration engineers, electronic
data interchange specialists, pre-sales engineers and managers that need to
present to their bosses bosses, and they couldn't possibly use the same
environment - because one would be fragile to changes made by another.

So to decouple this, some previous projects I had worked on have spun up a
dozen (!!!) different PERMANENT environments, not even counting temporary
containers spun up for test suites.

Which, as you can probably guess, created a lot of make-work in environment
maintenance. To satisfy some niche group's vanity, at the expense of the
system's overall stability.

Incentives matter.
