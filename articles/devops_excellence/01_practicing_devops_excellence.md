# Practicing DevOps Excellence

I’ve been involved with DevOps for more than twelve years, and in that time I’ve seen my fair share of practices both good and bad. Elsewhere I’ve already written about what happens when companies find interesting ways of misusing DevOps – in a series of case-studies called DevOps Done Wrong, which began in 2017 and will presumably receive updates for some time yet.

What I haven’t talked about yet is the common thread all these case-studies share, and — through inversion — how we can arrive at something I would consider DevOps Excellence.

## 1. What DevOps Excellence actually means

My sparring partner of the day, GPT 5.4 Thinking, refers to DevOps Excellence as an interesting organizational property:
It is the ability to change production systems safely, frequently, and knowingly.

This property thus is less a set of checkboxes you can tick off (IaC, cloud, pipelines, a daily scrum, a platform team, …) and more the result of DevOps’ conceptual beginnings (i.e., the infinity loop), and their routine applications.

![Devops Infinity Loop](https://www.slideegg.com/image/pngv2/1280/77427-devops-infinity-loop-01-1280.png)

What all stages must share is feedback loops to surrounding stages:
- a software revision that cannot pass tests must continue development until it does;
- a release that cannot be deployed must be rebuilt (if not redeveloped) until it does;
- a deployment that is hard to operate should be investigated, increasingly with the help of adequate monitoring, etc.

The organizational property relies implicitly on those feedback loops: streamlined processes are necessary to achieve frequent deployments, but should be halted as needed – through quality gates to achieve safety, and developer intent to achieve deliberateness.

Along with developer intent goes responsibility for the outcomes, which we’ll investigate in the next section.

## 2. Reunite responsibility and control

To achieve software that can be developed efficiently, deployed effectively, and operated over the long run, the core insight of “DevOps Excellence” is that operational ownership of software with the team that develops it.

Sounds quite simple, but you’d be surprised by the number of ways non-technical firms try to avoid it.

Here’s how not to do it: Have one team develop the software. Have a system team deploy that software. Have an operations team try to keep it working (at 2am, with no developer in sight).

In our personal life we often understand that the best way to take care of something is to own it – and its outcomes. And eight hours a day, some of us pretend this isn’t necessary for the core function of our business — a truly astonishing insight.

So to empower your software organization, you’d do well to assign ownership of the software with the team in charge of planning, developing and releasing it.

This, coincidentally, helps build faster and more truthful feedback loops, as we’ll see below.

## 3. Build fast, truthful feedback loops

We have already established in the first section that DevOps optimally comes with fast feedback loops. They emerge from best practices developed over six decades of building and operating software and infrastructure. Almost all of those best practices have been codified into a process somewhere, where the main insight is making systems easy to learn from.

When developing software, we do code reviews to identify security flaws, potentially devastating side effects, and more generally undesirable outcomes. They also help your colleagues become familiar with the software change you propose, and spot weaknesses you may not have considered. They can further reveal assumptions made in planning stages that would seem at odds with surrounding software systems. Code reviews thus provide important feedback to both the developers and planners, and preferably help speed up the next iteration.

When deploying release artifacts, we prefer to use one environment for development, another for testing the software, possibly a third for “systems integration testing” with production data, and ultimately the production environment.

What I have seen with various former clients is a process of environment multiplication — ostensibly to help manage internal stakeholders’ concerns — but neither assigning direct control nor making these environments the sole responsibility of those stakeholders.

Simplifying this, it stands to reason, will reduce both your corporate budget needs, as well as help with obtaining more truthful feedback loops. What’s more, it’ll be simpler to manage.

## 4. Keep tools simple and legible

I’ve worked with a few frameworks around Big Data that promised to help simplify setting up Hadoop and similar Big Data tools in the past. Similar tools exist for making Kubernetes simpler to manage. And while they may promise that simplification, in practice you often end up learning to manage the abstraction rather than doing the work you actually care about (store and analyze data; develop and deploy software).

So make sure that the abstractions you add actually help your workflow. The tooling you use should help with judgment around critical infrastructure decisions, not obscure them nor replace understanding.

I’ve found that excellence often looks boring: small tools, where each does one thing well; transparent systems, where each of the moving parts has clear and well-defined interfaces; repeatable procedures, where each iteration helps enhance your grasp of the system.

## 5. Choose coherent operating models

Startups that prototype new software on hyperscalers will organically grow a “cloud-native” mindset. Incumbents that deploy monoliths to their own datacenters have had a long time to grow an “on-prem” mindset. Organizations moving into hybrid environments, meanwhile, often run into tension when their business processes no longer fit the technical reality. What is certain is that bringing the old process to your new environment will bring more contradictions than you anticipate.

A similar tension exists with software development models: organizations that grew out of scrum and have to introduce frameworks to ensure cross-team coordination will face different challenges than organizations that have historically leaned towards waterfall style development, and are now introducing scaled agile frameworks.

Over time, you’ll want to find a way of resolving the contradictions inherent in this change. Chances are it’ll involve deliberate choices that work for your organization, and then aligning process, architecture and governance to those choices.

## 6. Align incentives with system health

“It’s the people who have an incentive to find the problem who usually find the problem.” – Andrew Ross Sorkin

Make sure your organization rewards the right things. As I’ve touched on before, simplicity, legibility, fast and truthful feedback loops, reduced fragility, failure recoverability — and, ultimately, uptime — are all things you would want to reward.

Instead, I’ve seen firms engage in deliberate complexity theater, establishing a mess around their tooling, software stack and architecture, as that would get individual recognition fastest. In those scenarios, long-term maintainability always took a back seat over fast iterations with the latest shiny toolstack.

Consider establishing clear accountability for the continuous improvement of your systems infrastructure, and surround it with a culture around permission to make improvements, especially when they help establish the goals mentioned before.

## 7. A practical test of excellence

A few questions that can help you assess your organization’s path toward DevOps Excellence might look like this:

    • Can the team deploy what it builds?
    • Does the team feel the cost of instability?
    • Are reviews used to think, or just to approve?
    • Does each environment answer a distinct engineering question?
    • Can you explain your operating model in one paragraph?
    • Does your process survive staff turnover without becoming a cargo cult?
    • When incidents happen, is ownership obvious?

Within Xware, we’ve also found it helpful to score our customers before longer-term engagements with a variety of questions regarding the different stages of the DevOps Infinity wheel. We’ve actually turned that into our own 4x4 methodology, with different partners specializing up and down the stack.

Here is an excerpt.

    • Through how many layers (end users – sales organizations – other internal stakeholders, etc.) do you need to communicate between the end user and your DevOps development team?
    • Do you define themes, epics, or high-level requirements, and are these structured in a way that enables a more concrete use case to be utilized afterward?
    • Do you develop a roadmap in which releases, goals, and contents are clearly outlined?
    • For which artifacts is version control used? (requirements, code, configuration, tests, test data)
    • What types of code reviews are used? (pair review before completing a story, pull request policy with mandatory reviewer approval, presentation of enabler stories to the entire team, occasional pair programming, static code analysis)
    • How do you manage staging environments? (fully automated deployments, partially automated deployments, manual maintenance)
    • How do you ensure the quality of the developed applications? (automated tests, performance tests, penetration tests, manual testing, not at all)
    • How do you identify potential problems early? How do you respond to security incidents?
    • How do you measure user behavior and collect feedback?
    • How do you validate your original product hypotheses against the data you collect?

## 8. Conclusion

DevOps Excellence, then, is not a certification, a maturity badge, or a one-off purchase. It is the outcome of an organization learning to keep responsibility close to control, to re-evaluate what works and discard what does not, to shorten and strengthen feedback loops, and to align its stakeholder’s incentives with the ability to change production systems safely, frequently, and knowingly.

This also means that you cannot expect to roll out DevOps Excellence once and consider the work finished. It is an ongoing habit of creating an environment in which good decisions can compound over time.

Those decisions reunite responsibility and control. They improve the speed and honesty of feedback. They favor simplicity and legibility in tooling. They encourage coherence in operating models. And they align incentives with system health.
