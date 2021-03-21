Hybrid Games
============

With the advent of Cloud computing, established companies face changing
business models. They are scrambling to transform their IT departments running
on "legacy systems" from cost centers to more customer-focused operations.

Likewise, cloud-first startups grow into sizes where purely relying on AWS
(OpEx), versus building up their own data center (through CapEx) is not as
cost-effective at scale as previously thought.

At both ends of the spectrum, successful transformation is required to maintain
margins. This can be done in a myriad ways, many of which yield only partial
implementation and as such will lean towards half-bakedness.

To follow the first case: A common approach is to dive headfirst into new Cloud
platforms, leveraging quick-to-scale services into a very complex architecture
while bringing "on premise" mindsets (long-running, mutable infrastructure that
requires patchdays).

A more cautious approach uses "On-Premise Cloud" services, provided by big
players like VMware, Oracle, SAP, and the various OpenStack backers. It
involves virtual machines operated through "self service portals". The caveat
nobody talks about is that these are typically operated by a very limited
class of people, so are never actually self-service in practice.

Mindsets consist of intellectual habits - ways of thinking about things - which
take some time to obtain, and are achieved only by deliberate practice. What we
do most often shapes how we think about things ("when all you have is a
hammer"). Hence new paradigms require new mindsets; whether you move from
in-house architecture to the Cloud, or migrate in the reverse direction.

It is absurd to assume that an application written for AIX will be easily
ported to Amazon Linux and will work flawless in auto-scaling groups without a
complete rewrite. Likewise, it is absurd to assume that change management
processes can be ported to the Cloud without redesign.

Similarly, it is absurd to assume that immutable infrastructure works just as
well via KVM over IP. Reimaging a server the cost of a middle-class car still
requires more than ten seconds, and consequently, slighthly more careful
operations.

Growing "on-prem" or "cloud-only" operations into "hybrid operations" can be
done if supplied with helpful management that fully supports the bimodality in
operations models.

Everything else will end in tears.
