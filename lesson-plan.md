# Reinforcement Learning Unit, TJHSST

*Goal* Students will solve some classic RL problems and learn about exploration vs. exploitation, the Bellman equation, solving with perfect knowledge and solving by exploration.

*Content* The units are: Multi-arm bandit (approximate multiple distributions by random sampling), The Gambler's Problem (optimize the Bellman equation with complete knowledge), Gambler's Problem Exploration (find the optimum value by repeated playout and Monte Carlo sampling. (Note: a better MC problem might be Blackjack -- this is TBD)

*Reference* The excellent text [*Reinforcement Learning, an Introduction*](http://incompleteideas.net/book/RLbook2020.pdf) provides the background for these lessons.

## Multi-arm bandit

In this context, a *bandit* is a random number generator that doles out *rewards* according to a normal distribution $N(\mu,\sigma)$. The *one-arm bandit* problem is to estimate $\mu$ by random sampling. This is a straightforward application of statistics. The *multi-arm* version consists of multiple bandits, each paying rewards according their own $\mu_i$ and $\sigma_i$. The player's goal is to maximize their expected reward by finding the bandit with the highest average payout $\mu_{\mbox{max}}$. The process of finding and then playing the highest-playout bandit is a trade-off between *exploration* and *exploitation*. The *greedy* algorithm for maximizing reward provides an optimal playing strategy: if you know the bandit with the maximum $\mu$, you just play it every time. But you only ever have approximate knowledge of the various $\mu_i$, so as you play you have to spend some time exploring the bandits to get a better approximation of the $\mu_i$ values, but you also want to hit your "best guess" for $\mu_{\mbox{max}}$ as much as you can.

## Specifications

Your environment consists of an array of bandits, each of which are represented by functions which return a reward and take no arguments. Each bandit has a hidden $\mu$ and $\sigma$ which define the underlying normal distribution of rewards. Throughout your algorithm you maintain a **value** array which assigns a value to each bandit. On each step of your algorithm you will select an **action** accoring to a **policy**. The action is simply an integer $i$ specifying which bandit from the array of bandits will be queried for a reward. The policy uses the value array to determine an action. (Examples of policies include random (pick any action), greedy (pick the highest valued action) and constant (always pick the same action))

    e-greedy search

    given: an array of $n$ bandits as functions bandit(i)

    V[i] = 0 for all i in [0,n)
    R[i] = [] for all i in [0,n)

    for each t in [0,num_steps)
      with probability epsilon:
        select an action i from [0,n) uniformly at random
      with probability 1-epsilon:
        select the action i corresponding to the largest value in V[]
      r = bandit[i]
      append r to R[i] array
      V[t] = average of values R[i] array

This algorithm applies the greedy policy to $V$ with probability $1-\epsilon$ and the random policy with probability $\epsilon$. Once the action is chosen, the value entry is updated according to the observed reward. By the law of large numbers we can prove that $V[i]$ will eventually converge to $\mu_i$ for every bandit $i$ if $\epsilon > 0$

