# Mastering the game of Go with deep neural networks and tree search

AlphaGo combines policy and value networks with Monte Carlo tree search. MCTS allows us to constrain # of search states to evaluate and make the problem more tractable.

MCTS: rollout = search to max depth without branching by sampling long action sequences from a policy p. Averaging over rollouts can give good value estimate.

Pipeline:
1. Supervised learning policy network, trained on human expert moves.
2. Fast policy that can rapidly sample actions during rollouts.
3. RL policy network, that improves SL policy by optimizing final outcome of self-play games.
4. Value network that predicts winner of self-play RL games.

## SL human-expert policy network

13-layers, alternating between conv layers and rectifier nonlinearities. Final soft-max layer gives distro over all legal moves.
Input: simple rep of board state.

Expert policy: trained to 57% accuracy
Fast policy: trained to 24.2% accuracy, but much faster to select an action.

## RL policy network

Same network structure as SL, and weights initialized to be same as the SL expert policy network.
Self-play games between current network and a randomly selected previous iteration of the network (prevent overfitting to one policy).
Reward: +1 for winning, -1 for losing.

## RL Value network

Estimate value function that predicts outcome from position s if both players follow policy p (for strongest policy).

## AlphaGo

Combine policy + value nets in an MCTS algo -> select actions by lookahead search.

**MCTS**
- Selection: select edges with argmax(Q + u(P)), where u(P) is proportional to prior probability (from expert SL policy) and decays with visits to encourage exploration. This process ends once traversal reaches a leaf node (a node for which we have not yet run rollouts). 
- Expansion: once a leaf node has been visited n_thresh times, add it to the search tree by initializing from prior P.
- Evaluation: evluate in two ways. First, using the value network and second, by running a rollout to end of game using fast policy network. Combine these two values into V(S_L) with mixing param \lambda. 
- Backup: update Q values and visit counts of all traversed edges. 
