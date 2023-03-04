## The Phenomenon of Policy Churn

Rapid churn of greedy policy in value based RL -> more "churn" than expected.

Also argue that this policy churn is beneficial because it promotes more exploration.

Average policy change W ~ 10% (of states change) _per update_. This is ~1000x times more change than "experts" would have guessed. 10^7 updates means agent changes greedy action a million times in each state across training.

Policy churn gave comparable amount of exploration as $\epsilon$-greedy, removing both led to performance collapse.

Proposed explanation for the phenomenon: "The rapid policy change dubbed churn is the symptom of high-variance updates to a
global function approximator".

Policy change does not necessarily mean change in performance. Many states may have actions with the same outcome (e.g. moving left or right while falling).
