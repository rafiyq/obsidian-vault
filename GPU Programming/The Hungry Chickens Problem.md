What if you don’t care about philosophers and their strange need for two forks? Or if you just use a Flobbie or a pair of hair clippers to trim your own hair?

Well most people either eat chicken or want to see them live a happy life. So we are going to use my layman’s understanding of chicken eating habits and feeding practices to demonstrate similar pitfalls as other canonical problems.

## What Do Chickens Need in Order to Lay Eggs?

Let’s presume that we want to have some eggs for our dining philosophers to eat later or to create a meringue pie to feed to our favorite slumbering barber.

We need our chickens to lay eggs, so a sufficient amount of light, according to the Michigan State University Extension they need between 14-16 for minimum to maximum egg laying. Water is needed in general, so we will need open access to water.  They tend to not fight over this and drink at their leisure, but for our sake they like to drink immediately after they eat.

The main concern is food. They will fight over any scrap of food, especially when they see another chicken going for food. As a side note, this is why chickens are given scratch food (lower grade and usually corn), thrown in a large area so they expend their energy on scratching at the ground to get the food and not fighting each other over it.

So the goal of this problem is to have chickens eating, drinking, and not fighting, as that wastes energy and causes each other harm/disharmony.

## Feeders

So here are some devices for feeding your chickens.

![[feeder_hungry_chicken.webp]]

They all have issues related to how the chickens use them but in my mind from left to right they go from meh to wow!

The leftmost one is very common, allowing free access as long as the bottle has food in it.

The downside is that chickens will fight a lot over the food and they will throw the food out and waste more food.

The middle feeder handles much of the fighting problem since chicken heads will be blocked by plastic dividers, but it will still be a mess.

The feeder on the right is my one of choice.

The top image with a chicken eating in it and the bottom image shows the dividers (my version has four sections instead of 3.

A limited number of chickens can eat at the same time based on the number of “windows” and its general shape keeps fighting from happening and is the least wasteful option.

## The problem as a race condition

So let’s say we have two chickens and they need to eat and then drink.

![[race_condition_hungry_chicken.webp]]

This can be thought of as a possible race condition.

Each chicken needs to eat and then drink,

The feeder and the chicken’s greed will only let them eat one chicken at a time.

The waterer is a similar situation, one chicken at a time.

If a chicken needs to eat and then drink and let’s say there is a limited amount of food say 2 pellets.

If each chicken needs one pellet but can and will eat two pellets then the order that the chickens attempt to eat and drink may make one chicken starve, since the 1st chicken might have its one pellet and seeing the other chicken it eats the second.

The waterer could be the same situation enough food for 2 chickens but not so much that the chicken that gets to it first doesn’t drink it all.

So it can happen that both chickens eat and drink equally, one or the other chicken eats and drinks all of the supplies, or one chicken eats everything and the other chicken drinks everything and they are both worse off for it.

## The problem as a resource contention

Now let’s think about the case where chickens have the same basic instructions but they will fight if another chicken tries to take whatever they want/need.

![[resource_contention_hungry_chicken.webp]]

This is similar to a race condition, but if the chickens keep trying to get what they don’t have and the other chicken always fights their contention for either water or food may make them waste all of their energy trying to get their fill.

## The problem as a Deadlock or Livelock

In the case when chickens always think they need both feed and water simultaneously or at least no other chicken is trying to eat/drink at the same time, you will have either live or deadlock.

![[deadlock_hungry_chicken.webp]]

If the chicken will not eat until they have unfettered access to water and vice-versa the two chickens could arrive at the feeder or waterer and decide to stay until the other goes away, which neither will do.

This means deadlock, each chicken will die rather than relent.

To have the livelock case happen, chickens must act in an eager fashion, always trying to get what they don’t have.

This would mean if two chickens are each at a feeder or waterer and they start alternating between the two resources but never taking advantage of what they have in front of them.

## Bibliography 

[1] Ockert, Katie. Michigan State University Extension. 2019. Decreasing daylight and its effect on laying hens. Retrieved from https://www.canr.msu.edu/news/decreasing-daylight-and-its-effect-on-laying-hens.
[2] Chewy.com 2021. chewy.com
[3] Amazon.com 2021. amazon.com