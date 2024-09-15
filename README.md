# gophercon-2024-talk

Gophercon 2024 Talk Proposal

Gophercon Proposal

## Title

“Maximizing Impact: How Teams Can Leverage Go to Free Up Time and Money”

## Abstract

Are you new to Go or still finding your feet with it? This talk is designed for teams looking to make the most of Go in their projects. We’ll explore practical tips to streamline development, reduce costs, and empower your team, all while keeping the focus on building value for your company.

By the end of this session, you’ll be equipped with practical tools and processes that will help your team work more efficiently, reduce costs, and concentrate on building great products. Whether you’re a new or intermediate team, these insights will help you take your Go projects to the next level.

## Talk Description

This talk is tailored for teams working in startups or within larger enterprises. If you’re still getting to grips with Go or looking to refine your processes, this session will provide you with actionable strategies that are easy to implement and can have a big impact.

We’ll cover several key strategies:

**Leverage the Go Standard Library**: Learn how to minimize dependencies and simplify your maintenance efforts using Go’s rich, built-in functionality. This seems like a no-brainer, but we can delve deeper into this to understand why using the standard library can save you money over the long term by:

* New developers have a better chance of knowing it.
* Battle-tested code. The standard library is tested and hardened across many years and many projects, it may have quirks but it's less likely to have security vulnerabilities.
* It will be here. The standard library isn't going away so you are not reliant on a third-party developer to stick around and maintain a library.
* It's forward compatible. See the Go compatibility guarantee.

How do these things save you time & money? By allowing your code to live longer unchanged.

**Run on Cheaper Hardware**: Use Go’s cross-compilation capabilities to run your applications on cost-effective new hardware, reducing infrastructure costs without sacrificing performance. New architectures are becoming available in the server space, particularly ARM, WebAssembly, and others. By utilizing cross-compilation techniques you can compile your code, targeting a different architecture, e.g., Compile on x86 targeting ARM. In a modern containerized environment, you can go one step better and package a Docker container that embeds images for multiple architectures in a single artifact, and then have your container runtime like Kubernetes choose the appropriate architecture at runtime.

How do these things save you time & money? By allowing your code to run on cheaper hardware as it becomes available. Cloud providers offer significant cost reductions when running on ARM-based systems as compared to x86.

**Automate Dependency Updates**: This section focuses on automating the process of updating dependencies to save time and reduce the risks of outdated software. It's a boring part of the development process that no one tells you about, but all long-lived projects should include a regular process that will update your software to the latest libraries, and provide a rapid reaction to reported vulnerabilities. A regular update process will run `go get -t -d -u ./...` against each `go` repo to automatically update _minor_ and _patch_ versions of your dependencies. By updating this regularly the process can typically be done with almost no human intervention (our process runs monthly, and just has a human check and approve a PR).

How do these things save you time & money? It spreads out the cost of regular maintenance by keeping your repos up to date incrementally. My experience tells me that keeping up to date like this is much cheaper than letting code get very stale and trying to update many versions at once.

If you follow this advice, it helps when a security vulnerability needs to be addressed because your codebases are relatively up to date. Typically you want to react to severe security vulnerabilities quickly, so design a process that informs your team when a CVE affects your projects (our process raises a ticket for the team when dependabot detects a severe issue).

How do these things save you time & money? Because you have regularly kept your dependencies updated, addressing the security vulnerability should be relatively fast.

**Empower the Whole Team**: I believe in sharing your Go knowledge across your entire team, from developers to operations and testers, so that everyone can contribute effectively. I'm from a smaller organization, and I've encouraged and helped my colleagues in the TechOps and testing space to check out Go for their tasks. Adopting a common toolset (which included `go`) across teams has benefits of knowledge sharing and greater assistance when it comes to troubleshooting. It also provides greater opportunities for people to cross the boundaries that sometimes exist between teams. I'm a great believer that if a tester shows the interest in fixing a bug in my API, then I'll do my best to encourage and help them do that. I reckon that it provides a great opportunity to let people grow. It also encourages sharing and trust across teams.

**Focus on your strengths with a small toolset**: For my team, this means focusing on our strengths, which is designing and building high-value APIs for Loyalty systems. We have experimented with lots of tools but chosen just a few. For example, we choose Postgres databases, but we use a lot of features that make sense, for example, we use some of the more advanced features of Postgres like _triggers_ and _table partitions_, where it makes sense for our use case. We choose best-of-breed tools like the `pgx` driver, `sql-migrate` for db migrations. `sqlc` is a code generator that writes all the boilerplate access code giving you a nice typesafe access to your data. These tools together help the team to focus on what's most important to us, designing the correct database structures to support our use cases.

How do these things save you time & money? These tools are familiar, so we know how they work, and we know how to use them correctly, so we can quickly design systems that run on top of them. We have evaluated other databases but we found we have significant disadvantages around, learning to use them effectively, optimization strategies, runtime management, and ongoing costs. So we choose to use Postgres now, and re-evaluate in the future because it lessens our risks on delivering systems on time.

**Outsourcing when it makes sense**: In small teams, you can’t do it all, so we have had to learn how to strategically outsource parts of our infrastructure to experts, allowing us to focus on delivering core value.

We outsource most of our runtime infrastructure including database, file store, and compute. One such system is NATS a messaging platform that provides amongst other things a Microservice framework. This is a newer technology for my team but it aligns well with our requirement for building API servers that support event-driven architectures. We performed extensive "proof of concept" testing to ensure that NATS would meet our requirements for this. A key part of our decision to use NATS was to outsource the management of that to a third party, in this case, Synadia that runs a global NATS service called Synadia Cloud.

How do these things save you time & money? Synadia Cloud hosts our public API endpoints. This means that we are no longer responsible for managing all the components that make for a reliable public API endpoint including certificate management, DNS, routing, authentication, and authorization, etc. By outsourcing all of this, the development team can focus on writing API handlers. Equally as important the TechOps team has a greatly reduced management burden. This translates to less ongoing costs for projects, and reduced midnight callouts for our TechOps team.

Thanks for listening