* Freeze and define the domain nouns, verbs/operations terminology properly. Stick to the terminology while adding new features in code.

*  Use as minimal external services interaction as possible in build systems for local development. The external services should be super robust.
* Avoid writing lousy/lazy conditions, they might become the cause of problems. Always write full condition and do not assume things in writing conditions. Remember the following condition. Omitting 'fba_adjustment_items.FNSKU is null’ check caused duplicate rows and unique constraint violation.”” “(FBA_order_items.order_id = fba_adjustment_items.distributor_order_id AND                             FBA_order_items.ASIN = fba_adjustment_items.ASIN and ((previous_day_fba_adjustment_items.FNSKU is null and fba_adjustment_items.FNSKU is null) or             (previous_day_fba_adjustment_items.FNSKU = fba_adjustment_items.FNSKU)))"
* When doing bulk copy/ bulk operations think about performance
* Null column values in database queries are dangerous and cause mysterious errors.
* Test sub functionality and use secondary tools for testing sub-functionality while debugging issues in system integration. Take special care to log important values so that they help in debugging integration errors.
* Always assume data inconsistencies. Handle possible null cases carefully. The billion dollar mistske makes the programmer bite the dust. Choose languages with null safety, ex: Kotlin
*  Always use logs to track the bulk processing records status. It saves time. Log useful information to verify the correctness
* Always run the report/scripts that access database/resource in the same location. It speeds up processing by 10x.
* Always be careful while copying your own code. Copy mistakes result in waste of time.
* Force product owners/authors to write down the requirements for the task clearly. Create tickets according to the changing requirements. Use this data to convince managers and product owners.
* The strategy/technology you chose might not be enough for the task. You may find that the software is missing the functionality you expected. This could happen and you might need to rollback. Ask, experienced people who used the tools to gather feedback and their problems with the technology.
* Name the columns of the tables carefully, they are gonna stick around for a long time. It’s difficult to rename the column values after the release of the software to production. Though this is not an idea way we would expect, that’s the way it is right now.
* Writing down or documenting is beneficial as it refines our thought process.
* Keep the develop env as close to the production env as possible. It reduces the trail and errors to make it work in the actual production env.
* Use idemotent API’s that doesn’t perform the op again if already done so that any extra additional API calls either due to parallization issues or extra events issue are safe
* By default detection of config and library classes is bad, since it makes debugging painful
* Understanding the nature of the data is key to design scalable and self healing systems. Focus more on the entities relationships and the metrics about the data in a new team/project. Remember the no of invoices items an invoice can contain. Asummed to be 100’s at max. There are 1000’s in actual data.
* Evaluate the performance of all the database queries all the time before deployment. Use the datawarehouse when there is a need to process bulk data.
* When building development tools UI, never forget to have a way to navigate linked items from the UI. It saves lot of development time. Show all the times in a single timezone in a UI page
* Look at the code and perform the low hanging fruits optimisation. Discussing or thinking about it just by hanging on to the outline/bottleneck of the function might not uncover the optimisation opportunities. Simple optimisations like not processing the already processed items, processing the items in batches or right data structure hash/set/list might make a big difference.
* Never keep the blind spot towards the common components of the project you’re delivering if the common components are being developed by other developers. Respect everyone, almost trust no one in bigger components that might have higher impact on the project delivery. This rule is applicable for developers.  Be careful to change the common components, missing constraints in common components might impact downstream systems. Remember the case of due date plus thirty five days check. Basically avoid sloppy/no validations.
* Deployment should not impact the processing of the existing items. They should get retried automatically for background task work items. For customer requests, customers should not get impacted mostly and retry should make the operation successful.
* Root causes might manifest in symptoms which make the root cause sideline. Consider the sockets overload results in connection refusals and timeouts. Disk space unavailability manifests in memory bloat since logging daemon keeps items in memory when disk space is not available. It's difficult to reason about complex systems.
* Development feedback loop should be pretty quick. Build-deploy-test-build loop. \

