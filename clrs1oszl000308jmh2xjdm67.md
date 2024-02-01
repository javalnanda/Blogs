---
title: "Points which developers should not ignore and take ownership — part 1"
seoTitle: "Developer ownership"
seoDescription: "What ownership should a developer take?"
datePublished: Tue Jan 03 2017 10:54:40 GMT+0000 (Coordinated Universal Time)
cuid: clrs1oszl000308jmh2xjdm67
slug: points-which-developers-should-not-ignore-and-take-ownership-part-1-157655894df6
canonical: https://medium.com/faodail-technology/points-which-developers-should-not-ignore-and-take-ownership-part-1-157655894df6
tags: mobile-app-development, tips, properties, guidelines

---

In a software development firm, specifically in service base company, everyone is in hurry to achieve the milestone before the deadline. Which results in compromising quality or ignoring important concepts which might affect the scalability of the product/application. This article will cover various team members of the process but my main focus will be on what developers need to do as a part of their **responsibility** towards maintaining the **best practices**.

I have observed few areas where developers tend to ignore things and focus only on given task without raising concerns related to best practices or suggesting the alternative solutions and not show participation for the proposition the best possible way to build the **right product**.  
For e.g:

*   **Not questioning or brainstorming with the UX team**

This usually occurs in a design-led environment where UX team plays a major role in research and comes up with a proposal the way they think is correct. Which is fine and this helps client also to visualize the bigger picture before things enter into development mode. But, there is also a need to do technical feasibility check for the User Experience and functionality which UX team drafts. Now, here the conflicts begin to take place. It can be due to various reasons:  
\# Complex UI & UX with lot of micro animations  
\# Proposing things which are not feasible technically or there is no support for it  
\# UI which is not as per the OS design standard or mixing components from different OS like (field of Android style into iOS )  
and there can be many more things…

Here, first thing is definitely UX team needs to educate themselves about various patterns and design guidelines and collaborate with dev team for the technical feasibility.  
Now, as a developer your responsibility is to not blindly follow what is proposed. If you feel that something is not as per the OS standard or the proposed UX will cause an issue when the product scales further, it is your duty to discuss the same with the UX team or involve product lead/owner if required and come up with alternative and better solutions.   
This ignorance may lead to extra efforts or unwanted hiccups when for product scalability.   
For e.g: The MVP of your product does not have multiple options so UX team might have come up with a design of view pager with 2 tabs on top of the screen. But these options will be moving to the navigation drawer in the next release which as a developer you might not have realized and design team might have thought that it is easier to move the menu from view pager to navigation drawer going forward. But, what if the developer asks the UX team to get a brief of proposed design for the next phase? This will help the team to avoid extra efforts of technical refactoring and will help even design team to come up with a better alternative that can scale. Building a product/application is a team effort, everyone needs to propose the right solution as per their expertise & skills and it can always result in a fruitful outcome.

*   **Not taking the security issues in account**

This occurs most of the time in MVP phase specifically for the Mobile Applications as they are small in size and needs to be delivered quickly.   
Things which developer might ignore in terms of security can be:  
\# Using the same token for the user throughout the lifetime while designing API  
\# Not resetting token while changing password  
\# No encryption of passwords  
\# Saving important user details in plain text on device  
etc..  
Again, here it is developer’s duty to execute things in a right manner. Saving efforts of 2–3 days by thinking that it is just MVP will have a bigger impact moving forward when things need to be built on top of MVP and believe me there is no such thing as “refactor later”. You will always be in rush to achieve dead line for next phase to come and will never be able to figure out dedicated time for refactoring.

*   **Compromising on data-modeling and db architecture**

This is again very critical for the application to scale properly. While designing DB, your thought process should always be that the product you are working on will scale. Never assume and implement things just for the current working phase or current MVP.  
For e.g: If your app will have a provision of multiple user access to the same account, design it according to from the very beginning. Even if your current phase requires just single user access per account.

*   **Ignoring the performance of the application**

Performance is one of the biggest factors that will determine whether the user of the application will stay engaged with your application or delete the application due to bad performance.  
If not taken care properly, performance can be compromised in various ways like:  
\# Pulling entire content in single request instead of page based API request  
\# Improper refresh mechanism  
\# Doing network activities on main thread and blocking users where they shouldn’t be blocked

Again, the takeaway here is do not compromise on things to save time for current release that will have a bigger impact later on.

These are some of the areas where things can go wrong and software quality might be compromised when developers don’t take their responsibility of building the right product properly. Stay tuned for my upcoming post where I will be sharing points about why developers do such mistakes and how to prevent it to make sure that each product is crafted to perfection without compromise on quality.