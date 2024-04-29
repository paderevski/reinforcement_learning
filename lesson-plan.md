# Reinforcement Learning Unit, TJHSST

*Goal* Students will solve some classic RL problems and learn about exploration vs. exploitation, the Bellman equation, solving with perfect knowledge and solving by exploration.

*Content* The units are: Multi-arm bandit (approximate multiple distributions by random sampling), The Gambler's Problem (optimize the Bellman equation with complete knowledge), Gambler's Problem Exploration (find the optimum value by repeated playout and Monte Carlo sampling. (Note: a better MC problem might be Blackjack -- this is TBD)

## Multi-arm bandit

In this context, a *bandit* is a random number generator that doles out *rewards* according to a normal distribution $N(\mu,\sigma)$. The *one-arm bandit* problem is to estimate $\mu$ by random sampling. This is a straightforward application of statistics. The *multi-arm* version consists of multiple bandits, each paying rewards according their own $\mu$ and $\sigma$. The player's goal is to maximize their expected reward by finding the bandit with the highest average payout. The process of finding and then playing the highest-playout bandit is a trade-off between *exploration* and *exploitation*

