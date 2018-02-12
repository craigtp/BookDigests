# Book Digest: Software Estimation

Title     : Software Estimation: Demystifying the Black Art  
Author(s) : Steve McConnell  
ISBN-10   : 0735605351  
ISBN-13   : 978-0735605350

## Chapter 1 - What is an Estimate?
* Distinguish between estimates, targets and commitments.  An estimate is a prediction of how long some development will take or cost, but a target (i.e. “we need to have version 1.2 ready to demonstrate at a trade show in May”) is independent of the estimate.  Just because targets are desirable (or even mandatory) does not mean they are achievable.
* Estimations are not plans.  Estimates form the foundation for the plans, but the plans don't have to be the same as the estimates.  When different, this indicates a level of risk.
* Estimates are produced with no specific result in mind.  Plans are produced with a specific result in mind (i.e. hitting a specific business target).
* When you're asked to provide an estimate, determine whether you're supposed to be estimating (no specific result) or figuring out how to hit a target (a specific result).
* Estimates should not be a single-point number (i.e. We can have it ready in 4 months) but rather a range (i.e. We can have it ready in 3-6 months).  Further, the points within the range should have probabilities of outcome. (i.e. We are 50% confident that we can deliver in 3 months, and 90% confident with can deliver in 6 months).  Probabilities are implied in a range even if not explicitly stated.
* The definition of a “good” estimate is one that is within 25% of the actual result, 75% of the time.
* Most people's sense of 90% confident is really closer to 30% confident.
* The primary purpose of software estimation is not to predict a project's outcome; it is to determine whether a project's targets are realistic enough to allow the project to be controlled to meet them.
* “A good estimate is an estimate that provides a clear enough view of the project reality to allow the project leadership to make good decisions about how to control the project to hit its targets”

## Chapter 2 - How good an estimator are you?
* Don't provide "percentage confident" estimates (especially "90% confident") unless you have a quantitatively derived basis for doing so.
* Avoid using artificially narrow ranges. Be sure the ranges you use in your estimates don't misrepresent your confidence in your estimates.
* It’s common to feel the necessity to keep your estimates more narrow than wide.  If you’re pressured to narrow your estimates, verify that the pressure is coming from an external source and not yourself!

## Chapter 3 - Value of accurate estimates
* Underestimating can lead to many negative consequences such as: More Status meetings, Frequent re-estimation, Preparing interim releases, fixing bugs from quick-n-dirty implementations etc. Each of these activities do not need to occur at all when a project is meeting its goals, and they drain time from  productive work on the project thus making it take longer than it would if it were estimated and planned accurately.
* Overestimating can lead to Parkinson’s Law (work expands to fill the time allocated to it) or “Student’s Syndrome” (procrastination and leaving things to the last minute).  This is frequently the reason for managers to “squeeze” estimates if they think they’re overestimated.
* Don't intentionally underestimate. The penalty for underestimation is more severe than the penalty for overestimation (parkinson’s law/”student syndrome”). Address concerns about overestimation through planning and control, not by biasing your estimates.
* When asked “We need this software in 4 months” and you believe it will take at least 6 months.  Recognize a mismatch between a project's business target and a project's estimate for what it is: valuable risk information that the project might not be successful. Take corrective action early, when it can do some good such as reducing the scope of the deliverables, increasing team size etc.        
* Many businesses value predictability more than development time, cost, or flexibility. That is, they would rather have a longer estimate with lower variability than a shorter estimate with higher variability (i.e. can deliver between 6 and 12 months vs between 9 and 10 months).  Be sure you understand what your business values the most.

## Chapter 4 - Where does estimation error come from?
* It isn't possible to estimate the amount of work required to build something when that "something" has not been defined.
* At the beginning of the project, less information about how the project will run over time and long it will take is available upon which to make our estimates and decisions.  This means there’s a high level of uncertainty at this stage of the project.  As time passes, more data/information naturally becomes available, uncertainty is reduced  and estimates and decisions can become more accurate.  This narrowing over time of the uncertainty level is known as the “Cone of Uncertainty”.
* Consider the effect of the Cone of Uncertainty on the accuracy of your estimate. Your estimate cannot have more accuracy than is possible at your project's current position within the Cone.
* Don't assume that the Cone of Uncertainty will narrow itself. You must force the Cone to narrow by removing sources of variability from your project.
* Account for the Cone of Uncertainty by using predefined uncertainty ranges in your estimates and by having one person create the "how much" part of the estimate and a different person create the "how uncertain" part of the estimate.
* When applying the Cone of Uncertainty to iterative projects, you'll go through a miniature Cone on each iteration.
* You can't accurately estimate an out-of-control process. As a first step, fixing the chaos is more important than improving the estimates.
* To deal with unstable requirements, consider project control strategies instead of or in addition to estimation strategies.
* Include time in your estimates for stated requirements, implied requirements, and nonfunctional requirements and include all necessary software-development activities in your estimates, not just coding and testing.
* Don't reduce developer estimates—they're probably too optimistic already.
* The more adjustment factors an estimation method provides, the more opportunity there is for subjectivity to creep into the estimate.
* Don't give off-the-cuff estimates. Even a 15-minute estimate will be more accurate.
* Accuracy refers to how close to the real value a number is. Precision refers merely to how exact a number is. A measurement can be precise without being accurate, and it can be accurate without being precise. Match estimate precision to accuracy.

## Chapter 5 - Estimate Influences
* The largest driver in a software estimate is the size of the software being built, because there is more variation in the size than in any other factor.
* Organisations routinely mis-estimate software projects due to size because they often don’t know how big the software will be in advance or they don’t adjust estimates when the software is consciously increased in size (ie.. change requests)
* Projects have an exponential increase in effort as a project size increases due to the exponential increase in communication paths as team members increase. This is known as a diseconomy of scale.
* Normally we talk about economies of scale (individual unit cost falls when larger amounts are produced), but software projects exhibit diseconomies of scale, which is the exact opposite.
* There isn't a simple technique in the art of estimation that will account for a significant difference in the size of two projects. If you're estimating a project of a significantly different size than your organization has done before, you'll need to use estimation software that applies the science of estimation to compute the estimate for the new project based on the results of past projects.
* After project size, the kind of software you're developing is the next biggest influence on the estimate.
* There are variations among individuals performance too. You can't accurately estimate a project if you don't have some idea of who will be doing the work.
* the weakest choice of programming language, tool set and environment will increase total project effort by about 50%
* different scaling factors that can affect a project/estimate need to be weighted differently at different project sizes.

## Chapter 6 - Introduction to Estimation Techniques
* When choosing estimation techniques, consider what you want to estimate, the size of the project, the development stage, the project's development style, and what accuracy you need.
* Estimation by size uses units such as lines of code, function points, user stories etc.  Estimation by features use the number of features that can be delivered.
* Estimates can be “top-down” or “bottom-up”.  Top-down estimates compare the entire project to a similar past project, looking for points of correlation between the two projects in order to estimate at a high-level.  Bottom-up estimates breakdown the project into granular small tasks, estimate each of those and add them all up to arrive at a project estimate.

## Chapter 7 - Count, Compute, Judge
* Count if at all possible (count the units you’re using for size estimation - lines of code, user stories etc.). Compute when you can't count. Use judgment alone only as a last resort.
* Find something to count that's highly correlated with the size of the software you're estimating within your specific environment, and is available sooner rather than later in the project.
* Collect historical data that allows you to compute an estimate from a count.
* Don't discount the power of simple, coarse estimation models such as average effort per defect, average effort per Web page, average effort per story, and average effort per use case.
* Avoid using “expert judgment” to tweak an estimate that has been derived through computation.

## Chapter 8 - Calibration and Historical Data
* Calibration is used to convert counts to estimates (i.e.lines of code to effort, user stories to calendar time). Estimates always involve some sort of calibration, whether explicit or implicit.
* Use historical data as the basis for your productivity assumptions. Your organization's past performance really is your best indicator of future performance.
* Collect a project's historical data as soon as possible, ideally during the project but at least as soon as possible after the end of the project. It's difficult to go back six months after a project has been completed and reconstruct the "fuzzy front end/beginning" of the project to determine when the project began.
* Use data from your current project (project data) to create highly accurate estimates for the remainder of the project.
* If you don't currently have historical data, begin collecting it as soon as possible.

## Chapter 9 - Individual expert judgement
* To create the task-level estimates, have the people who will actually do the work create the estimates.
* If your project is still in the wide part of the Cone of Uncertainty  the estimate should be created by expert estimators.
* When estimating at the task level, decompose estimates into tasks that will require no more than about 2 days of effort.
* Single-point estimates tend to be closer to Best Case estimates that worst case estimates therefore create both Best Case and Worst Case estimates to stimulate thinking about the full range of possible outcomes.  Also add a Most Likely Case and compute using historical data.
* Compute the expected case estimate from worst/best cases thusly:  Expected case = (best case + (4 * most likely case) + worst case) / 6
* Use an estimation checklist to improve your individual estimates. Develop and maintain your own personal checklist to improve your estimation accuracy.
* Compare actual performance to estimated performance so that you can improve your individual estimates over time.

## Chapter 10 - Decomposition and Recomposition
* Decompose large estimates into small pieces so that you can take advantage of the Law of Large Numbers: the errors on the high side and the errors on the low side cancel each other out to some degree.
* Use a generic software-project work breakdown structure (WBS) to avoid omitting common activities.  WBS tables contains the list of categories of work (General Management, Planning, Requirements work, Architecture work, Coding etc.) and show the kinds of work (Create/Do, Plan, Manage, Review, Rework, Report Defects.) required within that category.
* Use the simple standard deviation formula (StandardDeviation = (SumOfWorstCaseEstimates - SumOfBestCaseEstimates) / 6) to compute meaningful aggregate Best Case and Worst Case estimates for estimates containing 10 tasks or fewer.
* Use the complex standard deviation formula (Compute the standard deviation of each task or feature using the preceding formula, Compute the square of each task's standard deviation (variance), Total the variances, Take the square root of the total) to compute meaningful aggregate Best Case and Worst Case estimates when you have about 10 tasks or more
* Don't divide the range from best case to worst case by 6 to obtain standard deviations for individual task estimates. Choose a divisor based on the accuracy of your estimation ranges.
* Focus on making your Expected Case estimates accurate. If the individual estimates are accurate, aggregation will not create problems. If the individual estimates are not accurate, aggregation will be problematic until you find a way to make them accurate (The above aggregations only work if Expected Results are accurate - at least 50% likely).

## Chapter 11 - Estimation by Analogy
* Estimate new projects by comparing them to similar past projects, preferably decomposing the estimate into at least five pieces.
* Do not address estimation uncertainty by biasing the estimate. Address uncertainty by expressing the estimate in uncertain terms.

## Chapter 12 - Proxy-based estimates
* In proxy-based estimation, you first identify a proxy that is correlated with what you really want to estimate and that is easier to estimate or count (or available earlier in the project) than the quantity you're ultimately interested in.
* Use fuzzy logic (group features into v.small, small, medium, large, v.large groups and get average lines of code per group) to estimate program size in lines of code.
* Due to the “law of large numbers”, the rolled-up estimate produced by fuzzy logic can be surprisingly accurate, but you should not overextend the technique to make estimates of sizes of specific features.
* Due to fuzzy logic's aggregate nature, it works best when estimating at least 20 features together.
* Consider using standard components (breaking projects into numbers of components such as dynamic web pages, static web pages, database tables, reports, business rules etc.) as a low-effort technique to estimate size in a project's early stages. This technique also only works with 20 features or more.
* Standard components technically breaks the “count, compute, judge” rule so only use as a last resort.
* Story points are an arbitrary value (usually powers of 2 or fibonacci sequence) which don’t correlate to anything concrete like lines of code but can be used to estimate an iterative project's effort and schedule that is based on data from the same project.
* Exercise caution when calculating estimates that use numeric ratings scales. Be sure that the numeric categories in the scale actually work like numbers, not like verbal categories such as small, medium, and large.
* Use t-shirt sizing to quickly help nontechnical stakeholders rule features in or out while the project is in the wide part of the Cone of Uncertainty.  T-Shirt sizes (Small, Medium, Large) are assigned as “business value” by the business and as “development effort” by developers.  This matrix can be used to determine whether a feature is worth implementing (i.e. a feature with small business value and large development effort may not be worth implementing).
* Use proxy-based techniques to estimate test cases, defects, pages of user documentation, and other quantities that are difficult to estimate directly.
* Count whatever is easiest to count and provides the most accuracy in your environment, collect calibration data on that, and then use that data to create estimates that are well-suited to your environment.

## Chapter 13 - Expert judgement in groups
* Use group reviews to improve estimation accuracy. Have individuals estimate the same work separately but don't just use an average of the estimates. Discuss differences and arrive at a group consensus.
* Use Wideband Delphi (essentially anonymous group estimates with meetings to discuss and  anonymous voting to reach consensus) for early-in-the-project estimates, for unfamiliar systems, and when several diverse disciplines will be involved in the project itself.

## Chapter 14 - Software estimation tools
* Software tools can help with estimation efforts, especially computationally intensive estimation methods that you can't easily do by hand, even with a good calculator.
* Beware of an “objective authority” changing estimates. The stakeholder sometimes proposes a few minor feature cuts (or a slight increase in team size) and then expects disproportionate reductions in the project's cost and schedule.
* Using Estimation software (especially when results are visualised on a graph etc) can serve as an impartial third party in arbitrating the effects of such changes. You can let the tool play the "bad cop" that tells the stakeholder his changes don't reduce schedule or costs as much as he’d hoped.
* Use an estimation software tool to sanity-check estimates created by manual methods. Larger projects should rely more heavily on commercial estimation software.
* You will need to calibrate software tools with data from at least 3 projects using any of effort (man months), schedule (calendar months), or size (lines of code).
* Don't treat the output of a software estimation tool as divine revelation. Sanity check estimation tool outputs just as you would other estimates.

## Chapter 15 - Use of multiple approaches
* Use multiple estimation techniques, and look for convergence (indicating good quality estimates) or spread (indicating possible overlooked factors) among the results.
* If different estimation techniques produce different results, try to find the factors that are making the results different and adjust accordingly until the estimates converge within 5%.
* If multiple estimates agree and the business target disagrees, trust the estimates.

## Chapter 16 - Flow of software estimates on a well-estimated project
* Poorly estimated projects focus on estimating cost, effort, and schedule only, with little or no focus on estimating the size of the software that will be built.  The inputs and the estimation process are usually not well defined and open to debate.
* Poorly estimated projects are reestimated many times, but usually only in response to schedule slippages late in the project. Well estimated projects are reestimated many times based upon new & better information.
* Don't debate the output of an estimate. Take the output as a given. Change the output only by changing the inputs and recomputing.
* Focus on estimating size first. Then compute effort, schedule, cost, and features from the size estimate.
* Because of the Cone of Uncertainty, most projects will benefit from being reestimated several times changing from less accurate to more accurate estimation approaches.
* When you are ready to hand out specific development task assignments, switch to bottom-up estimation.
* When you reestimate in response to a missed deadline, base the new estimate on the project's actual progress, not on the project's planned progress.
* Present your estimates to project stakeholders in a way that allows you to tighten up your estimates as you move further into the project (I.e. always use ranges rather than a single point).

## Chapter 17 - Standardized estimation procedures
* Develop a standardized estimation procedure at the organisational level and use it for all projects to ensure consistency, repeatability and protection from pressures to change an estimate simply because a powerful stakeholder doesn’t like the result.
* Standardized procedures will:  emphasise counting and computing over judgement, use multiple estimation approaches, defines how the estimation approach changes over the course of a project and contains a clear description of any inaccuracies.
* Coordinate your Standardized Estimation Procedure with your SDLC.
* Always perform introspection on your estimates and the procedures that produced them. Check for accuracy, wide enough ranges, high or low bias and which techniques produced the best estimates over time.

## Chapter 18 - Special issues in estimating size
* Measuring anything as multifaceted as software size using a single-dimensional measure will inevitably give rise to anomalies in at least a few circumstances.
* Use lines of code to estimate size, but remember both the general limitations of simple measures and the specific  hazards of the LOC measure. (Diseconomy of scale, differences in programmer productivity, complexity of software type etc.)
* Count function points (number of external inputs, external outputs, unique queries etc. within the program - see www.ifpug.org) to obtain an accurate early-in-the-project size estimate.
* Function point counts, whilst accurate, are time consuming to calculate. Simplified methods exist.
* Use the Dutch Method (indicative function point count = (35 x internal logical files) + (15 x external interface files) ) of counting function points to attain a low-cost ballpark estimate early in the project. (Internal Logical files are major logical groups of end-user data or control information that are completely controlled by the program - i.e. a single flat file or a single table in a relational database.  External Interface Files are files controlled by other programs with which the program being counted interacts)
* Use a count of GUI elements to obtain a low-effort ballpark estimate in the wide part of the Cone of Uncertainty.  Note the lack of accuracy within this method, though.
* With better estimation methods, the size estimate becomes the foundation of all other estimates. The size of the system you're building is the single largest cost driver. Use multiple size-estimation techniques to make your size estimate accurate.

## Chapter 19 - Special issues in estimating effort
* The largest influence on a project's effort is the size of the software being built. The second largest influence is your organization's productivity.
* The type of project being built (operating system, applications software, embedded software) has a major influence on estimates. Use historical data from the same project type when estimating new projects.
* In principle, estimates that are based on industry-average data usually include all technical work, but not management work, and all development work except requirements. Although this must be checked as estimates to do always follow this practice.
* Use software tools based on the science of estimation to most accurately compute effort estimates from your size estimates.
* Use industry-average effort graphs to obtain rough effort estimates in the wide part of the Cone of Uncertainty. For larger projects, remember that more powerful estimation techniques are easily cost-justified.
* The International Software Benchmarking Standards Group (ISBSG) has developed an interesting and useful method of computing effort based on three factors: the size of a project in function points, the kind of development environment, and the maximum team size.
* Not all estimation methods are equal. When looking for convergence or spread among estimates, give more weight to the techniques that tend to produce the most accurate results and to techniques that use your own company's historical data rather than generic industry-wide data.

## Chapter 20 - Special issues in estimating schedule
* You can estimate schedule early in medium & large projects using the Basic Schedule Equation: ScheduleInMonths = 3.0 x staff months (to the power of ⅓).
* Don't use the Basic Schedule Equation for small projects or estimates produced later in a project.
* Use the Informal Comparison to Past Projects formula to estimate schedule early in a small-to-large project: EstimatedSchedule = PastSchedule x (EstimatedEffort / PastEffort).
* Use Jones's First-Order Estimation Practice (function points to the power of approx. 0.40) to produce a low-accuracy (but very low-effort) schedule estimate early in a project.
* Shortening or “compressing” a schedule requires more effort for several reasons: Larger teams require more coordination and management overhead as well as create more communication paths which also increases overhead, More work needs to be done in parallel which increases the chance of work being based upon other defective work.
* The consensus of researchers is that schedule compression of more than 25% from nominal is not possible.
* Reduce costs by lengthening the schedule and conducting the project with a smaller team.
* A team size of 5 to 7 people appears to be both economically and functionally optimal for medium-sized business-systems projects.
* Medium and large projects typically experience some ramp up of team members from the beginning to the middle of the project, and some ramp down in the final stages.
* Use schedule estimation to ensure your plans are plausible. Use detailed planning to produce the final schedule.
* Remove the results of overly generic estimation techniques from your data set before you look for convergence or spread among your estimates.

## Chapter 21 - Estimating planning parameters
* Planning addresses "how" to conduct a project, and estimation addresses "how much" of a quantity to plan for.
* When a project gets to the planning stage, the goals of planning tend to be antagonistic toward the goals of estimation.
* Technical effort should be broken down into architecture, construction & test. Construction should take between 45% (for 500 kloc sized projects) and 70% (for 1 kloc sized projects) of the total time, with ⅓ of the remainder on architecture and ⅔ on test (note this does not include requirements effort!)
* You can quickly define requirements only very loosely, which will then require Herculean effort to implement. Or you can invest more time and define a smaller set of high-quality requirements, which will allow a lower effort implementation.
* You should add 5% (for 1 kloc sized projects) to 10% (for 500 kloc sized projects) of overhead to the effort estimate for requirements.
* You should add 10% (for 1 kloc sized projects) to 17% (for 500 kloc sized projects) of overhead to the effort estimate for management.
* Although developer-to-tester ratios vary greatly, you should aim for a ratio of between 3:1 to 7:1 of developers to testers.
* Consider your project's size, type, and development approach in allocating schedule to different activities.
* It's important to understand the difference between estimated time and planned (real) time and how to convert between the two. 
* The difference between estimated time and planned time is akin to the difference between the minutes on the game clock vs. the minutes on the wall clock in an American football game.
* If a programmer is divided between two projects, it can take two or more calendar months to accomplish one focused project-month of effort.
* On average, technical workers apply about 6 hours of focused project time per day to their assigned projects
* Defect production on a software project is a function of effort and project size, so it's possible to estimate defect production.
* One way of looking at defect production based on a program's size in function points and data suggests that a typical project produces a total of about 5 defects per function point. This works out to about 50 defects per 1,000 lines of code.
* Larger projects tend to produce more defects per line of code, which requires more defect-correction effort
* A typical approach to defect removal is expected to remove only about 84% of defects from the software prior to its release, which is approximately the software industry average.
* Defect-removal practices that include requirements prototyping, formal design inspections, personal desk-checking of code, unit testing, integration testing, system testing, and high-volume beta testing is estimated to remove about 95% of defects prior to the software's release.
* If you want to move from 95% reliability to 99% reliability, you should plan to add 25% to the "main build" part of your schedule. You should plan to add another 25% to your schedule to improve from 99% to 99.9% reliability
* Use your project's total Risk Exposure (RE) as the starting point for buffer planning.
* It’s important to add additional time for non-development tasks when converting from estimated time to real/planned time.  Add:  5-10% for admin, 2-4% for IT Support/Infrastructure and allow a 1-4% increase in requirements per month.  For first-time development in a new/unfamiliar environment allow 20-40% increase in effort.

## Chapter 22 - Estimate presentation styles
* An essential practice in presenting an estimate is to document the assumptions embodied in the estimate, primarily: Which features are required, Availability of key resources, Dependencies on 3rd parties, Major assumptions and Major unknowns.
* The key issue in estimate presentation is documenting the estimate's uncertainty in a way that communicates the uncertainty clearly and that also maximizes the chances that the estimate will be used constructively and appropriately.
* Use plus/minus qualifiers for the various numbers in your estimate and consider how large the qualifiers are.  A typical practice is to make the qualifiers large enough to include one standard deviation on each side.
* Typically the minus qualifier will be smaller than the plus qualifier.
* Be wary that, as an estimate gets passed around an organisation, the plus/minus qualifiers may tend to get stripped down or removed entirely.
* Risk Quantification is a method that can be used on top of plus/minus qualifiers and involves communication of the estimate’s specific assumptions with separate plus/minus qualifiers for each assumption.
* Be sure you understand whether you're presenting uncertainty in an estimate or uncertainty that affects your ability to meet a commitment.
* Don't present project outcomes to other project stakeholders that are only remotely possible.
* Consider graphic presentation of your estimate as an alternative to text presentation.
* Case-based estimates are a variation on confidence-factor (percentage likelihood) estimates. Present your estimates for best case, worst case, and current case combined with your commitment, or planned case.
* Try to present your estimate in units that are consistent with the estimate's underlying accuracy.
* Use an estimate presentation style that reinforces the message you want to communicate about your estimate's accuracy.
* Don't try to express a commitment as a range. A commitment needs to be specific.

## Chapter 23 - Politics, Negotiation and problem solving
* An issue with estimate negotiations often arises from the fact that the estimates are given by technical staff, who tend to be more introvert, to executive staff who tend to be more extroverted and assertive.
* Understand that executives are assertive by nature and by job description, and plan your estimation discussions accordingly.
* Be aware of external influences on the target. Communicate that you understand the business requirements and their importance.
* We don't negotiate questions of fact, we look them up. Similarly, a software estimate is the result of an analytical activity, and it isn't rational to negotiate the estimate. It is rational to negotiate the commitment that is related to the estimate.
* If you want to ensure the success of your software projects, educate your nontechnical project stakeholders about the costs associated with arbitrarily cutting cost and schedule estimates without making corresponding cuts in the work that needs to be done.  Educate them about the Cone of Uncertainty, and about the differences between estimates, targets, and commitments.
* Treat estimation discussions as problem solving, not negotiation. Recognize that all project stakeholders are on the same side of the table. Everyone wins, or everyone loses.
* It’s better to perform problem solving rather than negotiation around estimates.  The negotiation method should consist of:  Separate the people from the problem, Focus on interests not positions, Invent options for mutual gain, Insist on using objective criteria.
* Always focus on interests not positions.  When one side states a position (i.e. “We need the software in 6 months”) try to find why and for what purpose.  If you can’t deliver in the timescale demanded, find out why the timescale exists and look for a creative win-win solution that solves the underlying problem/interest that causes the other side to demand the software in 6 months.
* Generate as many planning options as you can to support your organization's goals and help with the “negotiation”.  Avoid saying, "No, I can't do that"; instead, redirect the discussion toward what you can do.
* As you foster an atmosphere of collaborative problem solving, don't make any commitments based on off-the-cuff estimates.
* Insist on Using Objective Criteria.  Questioning an estimate is a valid and useful practice. Throwing it out the window and replacing it with wishful thinking is not.
* Technical staff should own the estimate.  Stakeholders should own the target.  Both technical staff and stakeholders should jointly own the commitment.
* The commitment is where the targets and the estimates must ultimately be resolved. If you can reach agreement that you are the authority for the estimate and other stakeholders are the authority for the targets, most of the discussion will then naturally focus on the commitment. The overriding principle should be to reach agreement about what commitment will be best for the organization.