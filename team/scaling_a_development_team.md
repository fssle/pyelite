
http://adam.heroku.com/past/2011/4/28/scaling_a_development_team/

How To Scale a Development Team
ORGANIZATIONS
THU APR 28 09:56:38 -0700 2011
As hackers, we’re familiar with the need to scale web servers, databases, and other software systems. An equally important challenge in a growing business is scaling your development team.

Most technology companies hit a wall with dev team scalability somewhere around ten developers. Having navigated this process fairly successfully over the last few years at Heroku, this post will present what I see as the stages of life in a development team, and the problems and potential solutions at each stage.

Stage 1: Homebrewing

In the beginning, your company is 2 - 4 guys/gals working in someone’s living room, a cafe, or a coworking space. Communication and coordination is easy: with just a few people sitting right next to each other, everyone knows what everyone else is working on. Founders and early employees tend to be very self-directed so the need for management is nearly non-existent. Everyone is a generalist and works on a little bit of everything. You have a single group chat channel and a single all@yourcompany.com mailing list. There’s no real need to track any tasks or even bugs. A full copy of the state of the entire company and your product is easily contained within everyone’s brain.

At this stage, you’re trying to create and vet your minimum viable product, which is a fancy way of saying that you’re trying to figure out what you’re even doing here. Any kind of structure or process at this point will be extremely detrimental. Everyone has to be a generalist and able to work on any kind of problem - specialists will be (at best) somewhat bored and (at worst) highly distracting because they want to steer product development into whatever realm they specialize in.

Stage 2: The first hires

Once you’ve gotten a little funding and been able to hire a few more developers, for a total of 5 - 9, you may find that the ad-hoc method of coordination (expecting to overhear everything of importance by sitting near teammates) starts to break down. You have both too much communication (keeping tabs on six other people’s work is time-consuming) and too little communication (you end up colliding on trying to fix the same bug, answer the same support email, or respond to the same Nagios page).

At this point, you want to add just a sprinkle of structure: maybe an iteration planning on Monday, daily standups, and tracking big to-do items and bugs on a whiteboard or in a simple tool like Lighthouse. Perhaps you switch to a support system like Zendesk where incoming support requests can be assigned, and you add a simple on-call rotation for pages via Pagerduty. Your single internal chat and email channels continue to work fine.

Resist the urge to introduce too much structure and process at this point. Some startups, on reaching this stage, declare “we’ve got to grow up and act like a real company now” and immediately try to switch to heavy-handed tactics. For example: full-fledged SCRUM, heavyweight tools like Jira, or hiring a project manager or engineering manager. Don’t do that stuff. You’ve got a team that works well together in an ad-hoc way; you probably have some natural leaders on the team who direct a lot of the work while still being hands-on themselves; and while your product is launched and in the hands of users, in many ways you’re still trying to figure out what your company is really all about. Introducing bureaucracy into this environment is almost guaranteed to block you from doing what you’re really supposed to be doing, which is pivoting in search of your scalable business model.

Focus at this stage is key. Everyone is still a generalist, but the whole development team should be aligned behind a single goal (aka milestone) at a time. If you try to attack multiple battlefronts at once, and you’ll do everything badly. Great companies are more likely to die indigestion from too much opportunity than starvation from too little. Pick your battles carefully and stay focused.

Crisis on the brink of Stage 3

Grow to 10 - 15 developers, and you’re on the verge of a major team structure change. I’ve been told that many promising startups have been killed by failing to weather the transition between these stages.

With this many developers, iteration planning, standups, or any other kind of development-team meeting has become so big that the attendees spend most of their time bored. Any individual developer will find it difficult to find a sense of purpose or shared direction in the midst of trudging through laundry lists of details on other people’s work.

In programming, when a class or sourcefile gets to big, the solution is to break it down into smaller pieces. The same principle holds for scaling a development organization. You need to break into targeted teams.

Stage 3: Breaking into teams

Dividing your single team of generalists is harder than it sounds. Draw the fences in the wrong place, and you’ll create coordination problems that make things even worse. Find the right places to divide and you’ll see a massive increase in focus, happiness, and productivity.

The key to a good team is a well-defined sphere of authority, with clear interfaces to other teams. The team should own the vision and direction for the part of your product that it works on. It should be able to operate with maximum autonomy on everything it owns without having to ask for permission or information from other teams, except for the infrequent case of a feature or bug that crosses team boundaries.

A close mapping between your software architecture and your team architecture will be a big help here. By this time you have probably already converted your monolithic application into a distributed system of multiple components communicating over REST, AMQP, or other RPC mechanism. (And if not, you should strongly consider doing so, coincident with your dev team split.) There should be an obvious mapping between software components - each of which has their own source repository and deployment location/procedure - and your nascent teams.

Deciding what person goes on what team will be somewhat arbitrary at first. My approach was to sit down with each developer and dig in to try to understand what parts of the system they were most passionate about working on. From there I divided up the teams as best I could. Some people found perfect homes on their first team assignment, others were dissatisfied and needed to transfer to another team fairly quickly. Over time, the team territories became very well-defined, so it became much easier to slot new hires in the right place. Let developers follow their own passions and they will gravitate toward the team where they will do the best work.

Separately, you should have found your product/market fit by this point. If you’ve grown to this size and are still figuring out your company’s meaning for existence, you’ve got big problems. If that’s the case, stop growing, and scale back down until you nail product/market fit.

Specialization

Another reason to break into teams is specialization. Types of engineering specialists include ops engineers/sysadmins, infrastructure developers, front-end web developers, back-end web developers, business engineers / data analysts, and developers who focus on a particular language. Language specialists are becoming more common, because many internet-scale companies write high-concurrency components in functional programming like Erlang, Scala, or Clojure, generally handled by a different set of developers than the authors of the Ruby, Python, or PHP web components.

Early on, specialists are rarely desirable. There’s too many different layers to work on in delivering a software product relative to the number of people available to contribute, so the everyone pitches in on everything. This may put a developer doing such far-ranging work such as ops projects like kernel updates on the OS, to front-end projects like writing JQuery effects for the UI.

Once you reach the point where you’ve got a dozen developers, your product has reached a level of usage and maturity where the problems are getting much harder. Scaling the database is something that is not only a full-time job, but requires a deep level of specialized knowledge that can’t be acquired if that person is also simultaneously learning to be a JQuery expert and an iOS expert and an Erlang expert.

You need people who can and are willing to focus on just a few closely related areas so that they can build very deep knowledge in those areas. Some of these will be your existing generalists deciding to specialize, and some will be new hires. You can now hire for the kind of specialist that would not have been appropriate when your company was smaller. Generalists are always useful to have around, and some of them may move into management - filling business owner roles for a team, rather than hands-on development.

Heroku's first teams

Heroku’s initial team breakdown looked like this:

API - Owns our user-facing web app and the matching Heroku client gem.
Data - Builds and runs our PostgreSQL-as-a-service database product.
Ops - Shepherds and protects availability of the production system.
Routing - Manages everything necessary to get HTTP requests routed to user web processes.
Runtime - Handles packaging code for deploy and starting/stopping/managing user processes.
Each of these teams owns between one and five components. For example, the API team owns the Rails app which runs at api.heroku.com and the Heroku client gem. The Data team owns the provisioning and monitoring tool for our database service, as well as all of the individual running databases. (Peter van Hardenburg was the intrapreneur who founded and now leads our Data team. He tells a bit of that story in the later part of this video.)

Team size and roles

For us, the ideal team layout has been two developers and one business owner. One developer is not enough over the long term (they need a second pair of eyes on the code, and besides, one is a lonely number). Three developers works fine as well. Get to four or five and things start to become a bit crowded; there may not be enough surface area for them to all work without stepping on each others’ toes constantly. Almost all of Heroku’s teams have two developers.

“Business owner” is a somewhat clumsy term, but it’s the best we’ve come to describe the person doing some combination of product management, project management, and general management for the team. The business owner fills the important role of knowing the business value of the team’s work to the company and how it fits in with the larger product. They can broker cross-team communication, help prioritize projects and tasks by business value, and may provide status reports on the team’s progress or presentations to the senior executives and/or the entire company to justify the team’s ongoing existence.

I’m a fan of hacker-entrepreneurs in the business owner role: a strong technical background means they have an in-depth understanding of the work being done, and are able to command huge respect from those whose work they are directing. This sort of person is not necessarily available for all teams, but find them when you can. In many cases it involves quite a bit of convincing to get a hacker to give up coding as their primary function.

Avoid having developers belong to more than one team. They are makers and need to be able to focus their full attention on their team’s current projects without distraction or attempts at multitasking. Business owners, however, can sometimes belong to multiple teams. It’s not always a full-time job, and there are benefits to cross-team communication by having one person be a business owner for two or more related teams.

Cohesion

In the earlier stages, you should avoid attacking on multiple battlefronts, and instead keep all developers focused around a single goal for the company. With creation of fiefdoms for each team, this has changed. Now you can and should attack on multiple battlefronts. Each team should be executing independently against its own goals, and not worrying too much about what other teams are doing.

It’s awesome to be able to pursue three, four, five big goals simultaneously. A few months after breaking into teams at Heroku, we had a day where three different teams were all releasing major new features. It’s an incredible feeling.

But now you have a new problem: lack of cohesion. Your decentralized teams are setting their own roadmaps and deciding on features independently. But to avoid fragmentation in your product, someone needs to decide an overall direction and set of product values. More succinctly: you need a strategy.

But this post is long enough as it is. I’ll save discussion of cohesion and strategy for another time.