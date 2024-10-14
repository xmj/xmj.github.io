Systems Ownership
=================

A core point of DevOps deals with systems, and corresponding feedback loops.
Often enough an important part of those systems will be outside of your direct
control, either managed by third party vendors or through layers of management
requirements or other indirections may not be directly amenable to fast
modifications. 

This will ultimately create a number of issues in dealing with the system:
- feedback loops will be less efficient: With systems under your control it is
  trivial to notice the effect of changes, and to allocate responsibility for
  dealing with the fallout. `git blame` provides one such tool to ascertain who
  did what when and, preferably, to what end. More complex change management and
  approval systems may be required due to regulatory compliance requirements.
  Ultimately, teams responsible for maintaining software systems want to
  guarantee their availability, and to fulfil changing user requirements.
- learning will be hindered, and responsibility for error correction may be
  shifted around between various parties. The less obvious to ascertain the
  relationship between changes introduced and their consequences, the more
  difficult for the teams engaged in developing both the software artifacts as
  well as the systems platform to learn about parameters of normal behavior. 
  Even more so when it is not obvious which team should even deal with the
  effects of some change introduced to that platform.

Allocating both ultimate responsibility as well as powers of control within the
same entity and establishing ownership will help alleviate several mismatches:
management gets a single point of contact with respect to the functioning of a
system, and the team responsible gets to guarantee their systems' end to end
functionality.

They'll also get to find ways to improve said system beyond what's previously
been thought possible, and may turn various points of contention into
outstanding features with enough exercise and time spent learning. 

Especially when they get to own all parts of the systems architecture.
