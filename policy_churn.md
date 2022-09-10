## The Phenomenon of Policy Churn

Rapid churn of greedy policy in value based RL -> more "churn" than expected.

Also argue that this policy churn is beneficial because it promotes more exploration.

Average policy change W ~ 10% (of states change) _per update_. This is ~1000x times more change than "experts" would have guessed. 10^7 updates means agent changes greedy action
a million times in each state across training.

$$ \epsilon---greedy $$
