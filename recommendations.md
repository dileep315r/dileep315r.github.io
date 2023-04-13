### Recommendation systems
1. Recommendation systems are built to predict what users might like, especially when there are lots of choices available.
2. Recommendation systems can be built using a variety of techniques, from simple (e.g., based only on other rated items from the same user) to extremely complex. Complex recommendation systems leverage a variety of different data sources (one challenge is using unstructured data, especially images, as the input) and machine learning (including deep learning) techniques.
3. Thus, they are well suited for the world of artificial intelligence and more specifically unsupervised learning; as users continue to consume content and provide more data, these systems can be built to provide better and better recommendations.
4. There are two primary types of recommendation systems
   1. Collaborative Filtering
      1. It primarily makes recommendations based on inputs or actions from other people (rather than only the user for whom a recommendation is being made)
      2. types
         1. By User Similarity: This strategy involves creating user groups by comparing users’ activities and providing recommendations that are popular among other members of the group. It is useful on sites with a strong but versatile audience to quickly provide recommendations for a user on which little information is available.
         2. By Association: This is a specific type of the one mentioned above, otherwise known as “Users who looked at X also looked at Y.” Implementing this type of recommendation system is a matter of looking at purchasing sequences or purchasing groups.
   2. Content-Based
      1. Content-based systems make recommendations based on the user’s purchase or consumption history and generally become more accurate the more actions (inputs) the user takes.
      2. By Content Similarity: As the most basic type of content-based recommendation system, this strategy involves recommending content that is close based on its metadata. 
      3. By Latent Factor Modeling: Going one step further than the content similarity approach, the crux of this strategy is inferring individuals’ inherent interests by assuming that previous choices are indicative of certain tastes or hobbies.
      4. By Topic Modeling: This is a variant of the Latent Factor Modeling strategy, whereby instead of considering users’ larger actions, one would infer interests by analyzing unstructured text to detect particular topics of interest. 
      5. By Popular Content Promotion: This involves highlighting product recommendations based on the product’s intrinsic features that may make it interesting to a wide audience: price, feature, popularity, etc.
5. Steps in building
   1. 1 — Understand the Business
      1. What is the end goal of the project?
      2. Is a recommendation really necessary? Can the business achieve its end goal by driving discovery via a static set of content instead (like staff/editor picks or most popular content)?
      3. At what point will recommendations occur?
      4. What data is available on which to base recommendations? logged-in vs anonymous
      5. Are there product changes that must be made first? Ex: Login sooner
      6. Should all content or products be treated equally?
      7. How can users with similar tastes be segmented?
   2. 2 — Get the Data
      1. If you have a business where most users are unknown, you may need to rely on external data sources or general data not explicitly tied to preferences, like demographics, browsing history, etc.
      2. The best recommendation systems use terabyte(s) of data. 
      3. When it comes to user preferences, there are two kinds of feedback: explicit and implicit
         1. Implicit: For example, past purchase history, time spent looking at certain offers, products, or content, data from social networks, etc.
            1. On the other hand, implicit feedback can be more complicated to interpret; just because a user spent time on a given item doesn’t mean that (s)he likes it, so it’s best to rely on a combination of implicit signals to determine preference.
         2. Explicit like return, complaints, ratings
            1. Explicit: it’s inherently biased; a user doesn’t know what he doesn’t know (in other words, he might like something but has never tried it and therefore wouldn’t list it as a preference or interact with that type of item or content normally).
   3. Explore, Clean, and Augment the Data
      1. Consider only looking at features that are more likely to represent the user’s current tastes and removing older data that might no longer be relevant or adding a weight factor to give more importance to recent actions compared to older ones.
      2. Datasets for recommendation systems can be challenging to work with because they are commonly high dimensional, but at the same time, it’s also common that many of the features don’t have any values, which can make clustering and outlier detection difficult.
   4. 4 — Predict the Ranking
      1. simply by ranking those scores by users and you’ll have products to recommend. This strategy doesn’t use machine learning or a predictive element, but that’s totally fine.
      2. But if you do want to build something more complex, there are lots of subtasks that can be done after users consume recommended content that can be used to further refine the system. There are several ways to leverage the hybrid approach to try for the highest-quality recommendations
         1. Presenting recommendations from different types of systems together side-by-side.
         2. Maintaining multiple algorithms in parallel where the decision of which algorithm is preferred over another is itself subject to machine learning (e.g., multi-armed bandit).
         3. Using a pure machine learning approach to combine multiple recommendation systems (logistic regression or other weighted regression methods). One specific example would be using a weighted average of two (or more) recommendations using different techniques.
      3. It’s also possible that different models will work better in different parts of the product or website. For example, the homepage where the user has yet to take action vs. after the user has clicked or consumed content in some way.
   5. 5 — Visualize the Data
      1. When still in the exploration phases, visualizations can help reveal things about the data set or give feedback on model performance that would otherwise be difficult to see.
      2. After putting the recommendation system in place, visualizations can help convey useful information to the business or product teams (e.g., which content does well but isn’t being discovered, similarities between users’ tastes, content or products commonly consumed together, etc.) so they can make changes or decisions based on this information.
      3. But by the same token, a good visualization will help make sense out of lots of data from which it would be otherwise difficult to derive meaningful insights.
   6. 6 — Iterate and Deploy Models
      1. it’s critical to evaluate performance and continue to fine-tune, like adding new data sources to see if they have a positive effect.
      2. In fact, making sure your recommendation system is built to adapt and evolve by regularly monitoring its performance is one of the most important parts of the process
      3. a recommendation system that isn’t properly adjusting to tastes or new data over time likely will not help you ultimately achieve your initial project goal, even if the system performed well at first. Building a feedback loop to understand whether or not users care about recommendations will be helpful and provide a good metric for making refinements and decisions going forward.
      4. If recommendations are core to your business, constantly trying new things and evolving the initial model you’ve created will be an ongoing task; recommendation systems are not something you can create and cast aside.
6. Challenges
   1. It’s important to create a recommendation system that will scale with the amount of data you have. If it’s built for a limited dataset and that dataset grows, computation costs grow exponentially, and the system will be unable to handle the amount of data. To avoid having to rebuild your recommendation system later on, you must ensure from the beginning it is built to scale to expected data volumes.
   2. that the recommendation system only makes very obvious recommendations despite all the hard work. Go back and check your business goals.
   3. A recommendation system not agile enough to continue to adapt can quickly become obsolete and won’t serve its purpose. 
7. Context-aware recommendation systems represent an emerging area of experimentation and research, aiming to provide even more precise content given the context of the user in a particular moment in time. For example, is the user at home, or on the go? Using a larger or smaller screen? Is it morning or night? Given the data available on a certain user, context-aware systems may be able to provide recommendations a user is more likely to take in those scenarios.
8. Deep learning is already in use by some of the biggest and most powerful recommendation systems in the world (like YouTube and Spotify). But as the amount of data continues to skyrocket and more businesses find themselves up against a huge corpus of content and struggling to scale, deep learning will become the de facto methodology for not only recommendation systems but all learning problems.
9. Solving the cold-start problem is also something that cutting-edge researchers are starting to look at so that recommendations can be made for items on which there is little data.
   1. they can successfully push items that will sell well (even before they know how that item will perform).


