# Book Digest: The Nature of Software Development

Title     : The Nature of Software Development: Keep It Simple, Make It Valuable, Build It Piece by Piece  
Author(s) : Ron Jeffries  
ISBN-10   : 1941222374  
ISBN-13   : 978-1941222379

## Chapter 1 - The Search For Value
* The point of software development work is value.  Value is defined as “what we want”.
* Value is created by Guiding, Organizing, Planning, Building, Slicing & Quality.
* Guiding - We create teams and guide them to develop the required software.
* Organizing - We organize teams around features which allows us to deliver value most rapidly.
* Planning - We steer our projects by the features most needed.
* Building - We build up our product feature by feature.
* Slicing - We “slice” our features into the smallest possible size that delivers value
* Quality - We apply the necessary practices to ensure the product always has a good design and remains as bug-free as possible.

## Chapter 2 - Value is what we want
* Value is what we want.
* We can want software to help us make money, to help us save money, even to help save lives, but ultimately this is the value that the software brings.
* Projects only deliver value when the software is shipped to the end user.  We can’t deliver everything right away, but we deliver feature by feature as each feature is ready.
* By shipping feature by feature, we allow feedback from the end user.  This feedback is invaluable and helps guide us in the development of the rest of the product.
* Features are really MMF’s (Minimum Marketable Features) - this isn’t measured on a technical level but on a level that makes sense - and delivers real value - to the end user.
* We prioritise features based upon the amount of value delivered and the cost/time to deliver.  We favour high value, low cost features and defer low value, high cost features which may not even be needed eventually.

## Chapter 3 - Guiding goes better feature-by-feature
* The first thing we know about our project is the deadline.
* The customer usually wants everything delivered by the deadline, however, we usually are late or don’t deliver everything the customer wanted.
* Many projects plan with activity-based phases - Analysis, Design, Coding and Testing.  If we don’t do Testing until other phases are complete, we don’t know in advance how the testing phase will perform.
* Until we begin to see and be able to use the software, we really can’t tell how well we’re doing.
* If we only performing certain phases later in the development schedule, by the time we find out where we are, it’s too late to do anything about it.
* Activity-based projects are monoliths.  If we perform all the analysis and design before other phases and we’re too late to perform the coding for all of the features, we’ve wasted time analyzing and designing features that will never be completed.
* Always plan for multiple, small releases.  Each release will have encompassed all of the phases in a single release cycle.
* A flow of visible, released features is easier to manage, maximises value and minimizes project risk and gives better visibility into the progress of the project.
* Growing the project feature-by-feature allows us to respond better and more quickly to changing customer demands.

## Chapter 4 - Organising by feature
* We organise the project by features, not by skill-sets of people within the team.
* If we organize teams by skill-set, each piece of work will need to be passed around among teams and each hand-off requires scheduling and can introduce problems.
* We create “feature teams” which are teams of people with all of the required skills to produce a complete feature (analysis, design, development, testing etc.) that the product champions can understand.
* By using feature teams, scheduling and the potential for problems with hand-offs of work are minimized.
* If you don’t organise by feature teams, the work must be passed from one team to another and requires scheduling and organisation.  Work must be “queued” between teams and will often need to go back and forth between multiple teams many times (i.e. development <---> testing etc.).  This slows you down.
* Although for most companies, organising around feature teams is very different to how they usually work, it’s worth the effort to change due to the benefits it will bring.
* Members of feature teams can change as the project progresses.  Put the best people in each skillset in the team that creates the highest priority feature. Rinse and repeat as the features are delivered and the next priority feature is decided.
* Experts with given skillsets should not only perform work in the team, but also mentor more junior member in order to create better skilled teams.
* When working in feature teams, scaling is easy as teams rarely need to work in “lock-step”. Scaling simply requires more independent feature teams who can work autonomously on complete features.

## Chapter 5 - Planning Feature By Feature
* Our products should be based on visions, which are big, grand ideas, but should be planned by individual features, which are the big ideas broken down into smaller chunks.
* We need to plan, but not to spend lots of time at the beginning of the project planning everything down to the finest detail.  We should make a plan that allows us to defer low value ideas, identify and prioritise the high value ideas and to be able to respond and change quickly.
* Planning is not just something we do at the beginning of the project, but all the time, throughout the lifetime of the project.  We don’t need highly detailed plans for everything, which would waste time, we only need plans for the highest value items that are our immediate priorities.
* We don’t need to produce detailed plans with estimates of all of the features (something that is frequently done today so that managers can sum up hours and costs for the whole project), we should simply  set a time and money budget, produce the most valuable features first, keep the product ready to ship at any time and stop when the clock (or money) runs out.
* We plan during each iteration (i.e. sprint), which will be broken down by one or more features (i.e. user stories)
* We shouldn’t break stories down into technical tasks as these don’t make sense to the business people, but large stories should be broken down into smaller stories.  Keep things at the level of granularity of the story so that project stakeholders can easily see how progress is being made.
* The team should be the ones to decide how much work can be completed in an interation.  You should base this on “yesterday’s weather” - i.e. use the amount you accomplished in the last iteration as a guide to what you’ll accomplish in this iteration.
* The iteration is planned before it begins and the team discusses the work with the product champion, enough to fully understand the feature(s) required.  This way, detailed estimates aren’t required.  The point instead is to do good work at a consistent pace.
* Estimates are risky as there’s often a desire to improve them and compare them.  Estimates focus our attention on the cost of things rather than the value.
* Best results are achieved by focusing on the work to be done and the work to be deferred.  Spending time on detailed estimates detracts from this.
* Attempting to set “stretch goals” or to push for just “one more feature” in a sprint is destructive as the team will attempt to add that extra feature, but will cut corners to achieve it, thus lowering the quality of all work in the sprint.
* If there’s too much work in the sprint, don’t try to complete it all.  It’s far better to do 8 things well, than 10 things badly.

## Chapter 6 - Building the product, feature by feature
* Build a complete tiny product in each iteration/sprint.  This includes going through every aspect of the development lifecycle (analysis, planning, design, development, testing).
* After a number of iterations, we’ll be able to tell how much we can accomplish in a single iteration of 1 or 2 weeks with good accuracy.
* We deliver value that’s quantifiable to the business people involved in the project and they help to break down large, sweeping requirements into smaller steps.  They help everyone sharpen their vision of what the product “must do” and separate it from what’s “nice to have”.
* Work on the highest value features and ensure they’re “done” or “not done” within a sprint.  There’s no middle ground.
* Eliminate the test-and-fix finish phase by ensuring that testing is performed all throughout the iteration and that the software is always kept in a “potentially shippable” state.  The software needs to be as free of defects at all times as is possible.
* We need to perform “design” tasks within each iteration to ensure our software can grow sustainably.  Too little, and new features will get progressively harder to add.  Too much, and we will ship too few features.  By monitoring our “velocity” (the pace at which we ship features) we can learn how to right-size our design effort.

## Chapter 7 - Build features and Foundation in parallel
* If we concentrate on building foundation (ie. architecture) first, we won’t have enough time to build the features that our product needs by the deadline.
* Even if we could build the complete foundation first, we can only correctly guide our project and calculate our velocity when we’re delivering features to the customer.
* We should build simple, but functional versions of our features with just enough foundation (architecture) to be solid - this is our “minimum viable product”
* Refine each feature over multiple iterations.
* Ensuring we have just enough foundation as we go, we help to keep the product in an “always shippable” state.
* This does take great skill, mostly on behalf of the Product Champion, who must be able to effectively select the highest value features within each iteration.  Developers need the skill to build only what’s necessary (with the necessary foundation) for each feature.

## Chapter 8 - Bug Free and Well-Designed
* Our software should be kept as bug-free and as well designed at all times as it can possibly be.  Good technical practices are required in order to achieve this.
* We should avoid the “bug triage” at the end of development work.  We should fix defects all the time and bug-fixing should be a part of the formal software schedule all the way through.
* Because we’re delivering based upon features during our sprints, we need the features to be defect free upon delivery at the end of the iteration.
* In order to help keep the software defect free, we perform testing throughout the iteration also.  We test at two levels, “programmer” tests - which are unit tests and test that individual functions within the program work correctly, and “business” tests which are acceptance tests and test that the feature does what the customer expects it to do (these can be Acceptance test driven development (ATDD) or Behaviour driven development (BDD) tests).
* Although writing tests takes time, paradoxically, having extensive tests makes the whole process go faster as defects are found and fixed much quicker.
* We need to start with minimal design at the beginning and ensure we improve the design as we add features during each iteration.  Remember that good designs go bad one decision at a time, so we amend and enhance the design continually throughout the development, as failing to do so will end up with us having bad design.
* Keeping the design good as the software changes is known as “refactoring” and is an important skill required for developing good software.  Testing and refactoring go hand in hand.  Refactoring can introduce defects and tests allow us to see this and fix it quickly..
* We automate the tests (programmer and business tests) and run the entire suite of tests continuously throughout the iterations and throughout the project lifecycle.  This allow us to know that our software is always potentially shippable.

## Chapter 9 - Full Circle
* Value is what we want. Features deliver value. Delivering features early gives us value sooner.
* Managing by looking at value works better than managing by dates or artifacts that don’t deliver value.
* Planning features is easy enough to do. Estimate if you must. Selecting the work based on “Yesterday’s Weather” works better.
* Building by features requires us to build a small, complete product, every couple of weeks. That product must always work correctly, and it must always be well designed.
* Development must deliver real working features. The product must be well tested. Business-side people and developers contribute to testing. The product must be well designed. Developers keep the design alive all the time.
* All of the above points are all that is required to consistently build and deliver great software.  It’s simple, but it’s not easy!

## Chapter 10 - Value - What is it?
* Value is simply “what we want”. This differs depending upon the needs and requirements of the business. If we're a charity shipping medicines around the world, saving lives is what we value. If we're a corporate looking to maximise profits, making money is what we value. So long as our software helps the business to achieve more of what it values, we're delivering good software.
* A business can value many things. The task of the product owner is to look deeply
at the many things we value, and to choose a sequence of development that gives us the best possible result in return for our time, money and effort in building the product.

## Chapter 11 - Value - How can we measure it?
* The main idea is to concentrate on value and not cost. Therefore,we shouldn't use real, numerical figures on which to base our estimates as we don't really know the exact numbers. We'll always be inaccurate.
* Big differences are more important than small ones, so we must enter examine the features we need and decide what's most important versus what's less important.
* Our valuing of these features will change over time as sometimes we need customer information (will people find this idea useful?) and sometimes we need development information (how long will it take to develop this feature?)
* We decide on the value we need at a given point in time by examining any two tasks and asking which is there more important. If we can't decide between those two, maybe neither should be done at this time. 
* Use the “five whys” technique to help determine which task has more value.

## Chapter 12 - Of course it's hard!
* Software development is hard but we don't need a hard, complex process in order to do it but we do need an increase in our level of skill and we need to continually improve our skill and refine our process as we go.
* When we change our practises to deliver incrementally, feature by feature, and avoid unnecessary hard numerical estimates etc. it can be very painful at first and we can feel like we're not getting as much done. It's very important to carry on! We will get better and the pain will eventually go away - like recovering from an operation on your leg, walking is difficult immediately afterwards but gets easier the more you do it.

## Chapter 13 - Not that simple!
* It's very often not that simple. Frequently, all the complications of real world business will show up, however, we must continue to focus on the value we want, building our product incrementally.

## Chapter 14 - Creating teams that thrive
* Often when managing something, we can feel the need to provide a lot of direction. We should resist this but ensure the teams know what to do but allow the team to decide how to do it.
* We should provide our teams with autonomy, mastery and purpose.
* Purpose comes from the business, identifying what should be done and what should be deferred.
* Autonomy gives the team responsibility. The product champion works with the team to decide upon an amount of work that is to be done during an iteration and the team self-organizes and decides how that work is completed.
* Mastery comes from the iterative process. As we iterate, we reflect on how we did and find ways to improve in the next iteration.

## Chapter 15 - The “Five Card” method to initial forecasting
* If we really must produce an initial estimate of development effort, we can use the five card method to produce just enough detail but not too much.
* Consider the 3 to 5 most important “epics” (the big things that describe the product) and write each one on a card using only a single sentence.
* Take each card in turn, then break it down to 3 to 5 more cards, again using only a single sentence. Be more specific and clear and, of course, smaller.
* Continue until all cards are about the same size which is approx. 1 week of development effort.
* As you do this, make sure all cards make business sense as a feature, not describing some technical widget, and as you break things down try to separate the more important cards from the less important ones to help with prioritisation.

## Chapter 16 - Managing natural software development
* When we develop software using these approaches, there's less need for “traditional” management as the team is more autonomous and self-organizing.
* Management work is still required such as staffing and budgetary decisions, whereas staffing selections should be done by the team.
* Managers sometimes wonder whether they’ll work themselves out of a job by letting go of so much of their work. But if a manager creates an effective team, building a valuable product, visibly and smoothly, that manager is going to get more to do, not less as he will need to build another team, and another!
* If you work for an organisation that requires long-term planning (months or years in advance) at a higher level in the organisation, it’s best to try to convince them to limit the number of products and programs that they take on.  Too many slows everything down.
* High level managers should only need to have a good understanding of the general capabilities needed to complete a large project.  The individual product champions can demonstrate that the capability exists through showing the progress of the working software with each iteration.
* Short term planning (day to day and week to week) is continuous as features are developed and delivered in highest value order first.  Value grows visibly.
* Project Management shouldn’t be about “keeping the project on track”, but instead should be about steering a course for the best possible result rather than rigidly sticking to a predetermined plan.
* Always keep an eye on the value being delivered and at the planning level, always ask what the most valuable next things are.
* Try to push detailed organizational decisions downward as far as possible (i.e. Upper level management can set budgets for staff, but the product champion and team should be responsible for the actual personnel recruited).
* Upper level management shouldn’t be concerned that many decisions are taken at the lower levels of the organisation as product progress is shown regularly and visibly and they can then direct from a higher level.  Big surprises should be nearly impossible when you can see product progress every two-four weeks.

## Chapter 17 - Whip the ponies harder
* When working under pressure, teams compromise on the wrong things (i.e. less tests) and this introduces more defects in the software which directly translates to reduced value.
* Pressure  is caused by attempting to “increase velocity” in order to “get more done” from a (perhaps mistaken) belief that more features are needed more quickly.  Frequently, teams in this position are working on features than are not delivering the highest value.
* If a team genuinely must “go faster”, the best approach is to analyse sources of delay in the process.  Improve team productivity rather than individual productivity and make sure that each team has the correct mix of skills required to perform the work.
* Don’t use measurements of velocity to predict then you’ll be “done”, you should choose when to be done by ensuring the best, most valuable features are delivered by the chosen date.
* The very best way to improve a team’s productivity is to improve skill.  Invest in your team’s education and training.

## Chapter 18 - To speed up, build with skill
* When we first set out to build a complete, but small, product in only two weeks, things will go badly - this is normal.  The key is to continue the process and examine where the delays and issues come from - it’s usually down to build times, integration times and test times.
* We must start from always being able to deliver a fully built, working product at the end of each and every iteration - this requires automating and optimizing our build and deployment process..  Even if we can’t show much new functionality in the early iterations, getting our build and deploy process right will give us the time and space needed to focus on delivering functionality.
* One common bottleneck can be the cycle between development and QA.  We should ensure that the developers test their work as much as they can before handing off to QA to reduce the chance that software will come back from QA with defects.
* If you have delays within the iteration due to waiting on some external resource you should consider having cross-functional teams and having that external resource be an integral part of the team.
* Every iteration should produce software that meets the “definition of done”.  This definition can be fairly loose at the beginning of the project and should be tightened and become more stringent over time as we improve (i.e. early iterations may not require full integration, whilst future ones absolutely should).
* At the beginning, things will feel slow.  This is fine.  As the team gets good at delivering software that is really “done”, they’ll be able to take on more features and deliver more value.

## Chapter 19 - Refactoring
* We need steady progress and in order to keep progress steady, we need a clean design to our software at all times.  To accomplish this, we must continually refactoring our code to keep the design clean.
* Sometimes, though, the pace is not steady and we find ourselves slowing down despite the work items appearing to be around the same size.  This is due to the existing code becoming more difficult to work with over time and the design needs to be improved through refactoring the code.
* Time needed to build a feature is really two-fold:  The inherent difficulty in building the feature and the “accidental” difficulty in getting the new feature to nicely fit into the existing codebase.  It’s increases in this “accidental” difficulty that slows us down.
* Refactoring is simply altering existing code to improve its design - to straighten out some of the twisty little passages that exist within the code.
* Refactoring should be an intrinsic part of every iteration and part of the development of every feature that goes into our software.  Skimping on refactoring (by piling on more pressure to deliver more features more quickly) will eventually slow progress down on the product.  This is often not noticed immediately, but when it’s noticed later on, it’s very difficult to do anything about it at that time.
* It’s always tempting to developers to start over and rewrite. It’s almost never the best plan. Instead, get good at refactoring, and apply the “Campground Rule”: Leave the campground a little better than you found it!  This should be an intrinsic part of all feature development.

## Chapter 20 - Agile Methods
* All current agile methods derive from the Agile Manifesto.  The “Natural Way” of software development detailed here is a distillation of over half a century of software development and over twenty years of agile software development.
* One of the most popular agile methods is “Scrum” by Jeff Sutherland and Ken Schwaber, although Scrum is, by design, not necessarily focused on software development so doesn’t prescribe specific technical practices like acceptance driven testing etc.  If you’re adopting Scrum for software development, you’ll need to add those practices in order to succeed.
* Extreme Programming (aka XP) by Kent Beck is another agile method that does specifically include those technical practices.  Some people consider that Scrum plus technical practices is equivalent to XP.
* Crystal Clear by Alistair Cockburn is another agile framework that is even simpler than Scrum.
* There are other frameworks that a significantly larger and more complex and aimed at a more “enterprise” class of user, such as: Dynamic Systems Development Method (DSDM), Large Scale Scrum (LeSS), Disciplined Agile Development (DAD) and Scaled Agile Framework (SAFe).
* If you’re adopting a framework, it’s better to have too little framework than too much.  Always try to strive to be “process light”.  Too much framework becomes bureaucratic and slow you down.
* Make sure you control the framework, don’t let the framework control you.  Modify your framework to make your projects more effective, but don’t change it just because it asks you to do “difficult” things.  Adjust to your abilities but be sure to also stretch yourself.
* Keep any process changes close to the team.  The team is performing the work, so they need to say what will work best for them.  As a manager, you determine the effectiveness of the team by only observing the results.
* Make learning a priority.  Skills are required at every level and in every role within the team.  Expect to invest in training and support and it will pay off in faster delivery of your software.
* Most of all we need to think and be open to change.   The work of building a valuable product is complex, and it is best accomplished, not by trying to anticipate and control everything, but by observing what happens and responding to events.

## Chapter 21 - Scaling Agile
* Very often, these days, there’s a lot of interest in larger organisations (i.e. “enterprises”) in “scaling” agile to their size of organisation.  In most cases, these companies are wrong to think they need to “scale” agile, they simply need to adopt agile as is.
* Be very wary of companies who will sell such “scaled agile” approaches complete with expensive training and consultancy.  Very often, the only beneficiary of these approaches is the company selling the “solution”, not the company buying it.
* Agile is quite simple, but it isn’t “easy”.  The most popular Agile approach, Scrum, has just three roles, a handful of activities, and one major artifact: running tested software.  Simplicity is the essence of what makes up agile.  Therefore, Scaled Agile must be simple, or else it isn’t agile.
* If you really need scaled agile, it’s best to do it by simply having multiple smaller agile teams.  Each team is a “standard” agile team with all of the same autonomy as any other team.  You scale by simply having more of these teams.  Remember that teams should be organised around product features.
* It’s often necessary to combine the output of multiple teams, so one way to achieve this is to have a less frequent “iteration” that sits on top of the individual teams’ iterations and acts as an integration iteration. (Scrum sometimes calls this a Scrum of Scrums).
* Team avoid stepping on each others toes by having plenty of tests.  Unit tests, integration tests and acceptance tests.  Having a large suite of these tests, shared across all teams will ensure that integration of the different features of the individual teams will go more smoothly.
* Team will be organised around features, but infrastructure is often a cross-cutting concern.  Infrastructure changes can be easily controlled by ensuring they, like application code, are extensively covered by tests.  Infrastructure changes can be performed by either each individual feature team, or by a separate agile infrastructure team.
* If you’re in an organisation building a truly giant product (requiring 100’s even 1000’s of developers), the “scaled” agile approach can still work.  You should build the giant incrementally, then when it gets to sufficient size, split it along features and have those features owned by individual feature teams.
* If there are truly giant efforts out there somewhere that cannot be reduced to smaller component parts, then take comfort that no-one knows how to successfully build these things, agile or not!  The very essence of putting lots of people on an effort is to divide up the work. If we do not know how to divide up the work, adding people will not help.
* If your individual teams cannot work in an Agile fashion, then clearly you’re not ready to “transition” your company or to “scale” Agile.