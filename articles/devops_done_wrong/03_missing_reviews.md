Missing Code Reviews
====================

In most industries where lives are on the line, not using process checklists
and multiple reviewers is considered unthinkable. In those, reviewers are often
actively encouraged to criticize people of much senior status when they fail to
perform basic duties.

Meanwhile, in corporate IT: Most firms use file hosting systems with built in
code review functionality. Thankfully, changes often require at least another
pair of eyes to approve them. And yet, these are more often than not a
formality.  Approval is given without actively engaging with the difference in
functionality before and after, often within seconds of opening the code
review's URL.

Some of this might be understandable. A junior developer new to a codebase might
not think they are in any way qualified to actually approve anything. A senior
developer may have a reputation for good work. Other human factors might come
into play.

And all of it at one point or another will generate excess cost. Sooner or later,
some not well thought out code will go into production, and cause outages[1].

Something that might prevent these is to encourage everyone, no matter how
experienced, to participate actively in code reviews. This means, at a minimum,
asking questions:

- Often enough, code that produces negative side-effects has a certain "funky
  look" to it. If something seems unclear, unnecessary, out of line, or in some
  way dubious, this is an easy way in to leaving a comment along the lines of
  "What's this do?"

- "Clever hacks" - that is, anything that takes longer than expected to
  understand - should have comments documenting intended behavior. If they are
  missing, here is another way in.

- Last but not least, when you see someone using a pattern you are not yet
  familiar with, you could ask where (which language, perhaps) this comes from.

This document will give you some ideas. But first and foremost, it gives you
the license to question. At the price of a duty to perform code review.


[1] The author of these lines has produced these effects often enough, "for
research purposes."
