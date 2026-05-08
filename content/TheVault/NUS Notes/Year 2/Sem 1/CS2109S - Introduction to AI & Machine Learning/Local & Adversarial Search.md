---
title: Local & Adversarial Search
Date Created: 2024-09-01
Last Updated: 2025-09-28
tags:
  - CS2109S
  - AI
  - Searching
---
# Local Search
----
The idea of using a local search is to **build goal/utility based agents**, but more importantly solve solutions that <span style='color:var(--mk-color-yellow)'>involve a very large state space</span>.

Unlike the search algorithms [[Problem Solving by Searching|mentioned previously]], **this and adversarial search** <b>provides a solution that is good enough</b>. It will <span style='color:var(--mk-color-red)'>not bother about the path</span> it took as it is only <span style='color:var(--mk-color-yellow)'>interested in the end state</span> which will be the <span style='color:var(--mk-color-green)'>solution</span>.

**Idea of local search**
- **Start somewhere** in the state space
- Always <span style='color:var(--mk-color-green)'>move to a better state</span>
- **Repeat** until <span style='color:var(--mk-color-red)'>no better states</span> can be moved to then **return the state as the solution**.

> [!info] Local Search Formulation
> Since we are **not interested in the path**, then:
> - Actions
> - Transition model (*Relies on actions*)
> - Action cost function (*No need to get the optimal solution*)
> 
> Are all <span style='color:var(--mk-color-red)'>not needed</span>.
> 
> We will only need the **states, initial states, successor function** (*Get neighbours*) and optionally a **goal test** (*We might not know the goal thus we can't make this function*).

The main component in a local search its is <span style='color:var(--mk-color-turquoise)'>evaluation function</span> (*Objective functions*). Since it looks around to see which neighbour to go to, it <span style='color:var(--mk-color-yellow)'>needs to know which one is the better state to go to</span>.
## Hill Climbing Algorithm

The algorithm works as such:
```Python
def hill_search(initial_state : State):
	current = initial_state
	while True:
		# Get all the neighbours ...
		neighbour = max(evaluation_function(neighbour)) # Get the highest value neighbour
		if value(neighbour) <= value(current): # We have found a peak
			return current
		current = neighbour # Continue searching
```

Essentially, this algorithm will continue to <span style='color:var(--mk-color-yellow)'>search until a peak has been found</span>. However, one issue is that this <span style='color:var(--mk-color-red)'>peak may not be a global maximum</span>.

There are <span style='color:var(--mk-color-turquoise)'>escape techniques</span> to <span style='color:var(--mk-color-orange)'>avoid stopping at a local maximum</span>:
1) **Tabu search**
2) **Random restarts**
3) **Random walk**
4) **Beam search** - Take $k$ branches and then search
## Simulated Annealing

The algorithm works as such:
```Python
def simulated_annealing_search(initial_state : State):
	current = initial_state
	T = 10000 # Some large integer
	while (T > 0):
		# Get all the neighbours ...
		neighbour = rand(neighbours) # Get a random neighbour
		if value(neighbour) > value(current): # A better state
			current = neighbour
		else:
			probability(current, neighbour, T) # Randomly choose to go to the bad state
		decrease(T)
		
	return current
```

The difference is that the next state chosen is a <b>random</b>. If its a better state then good, if its not then with <span style='color:var(--mk-color-yellow)'>some randomness, choose weather to go to that state or not</span>.

> [!important] How to Incorporate Randomness
> A general rule is that **at the start** (When `T` is large), <span style='color:var(--mk-color-green)'>allow randomness</span>, meaning the probability function should return a high value.
> 
> But **after awhile**, <span style='color:var(--mk-color-red)'>disallow randomess</span>, by returning a lower probability.
> 
> In theory, if `T` **decreases slowly enough**, <span style='color:var(--mk-color-turquoise)'>simulated annealing</span> will <span style='color:var(--mk-color-green)'>find the global optimum with high probability</span>.

The principle behind this is, imagine a **local maximum**, <span style='color:var(--mk-color-red)'>both sides will be decreasing</span>. However it is possible that by making bad moves, it can **find another peak** which might be the <span style='color:var(--mk-color-green)'>global maximum</span> or just another local maximum again.
# Adversarial Search
---
This type of search **takes into account another user**, where the neighbours are all possible states after the other user "acts".

This search algorithm is more towards <span style='color:var(--mk-color-orange)'>solving games against an opponent</span> with the <b>following environment</b>:
1) **Fully observable**
2) **Deterministic**
3) **Discrete**
4) **Terminal states exist** (*No infinite graphs*)
5) **2 player, zero sum game** (*Only 1 winner and 1 loser*)
6) **Turn taking**

```ad-info
title: Adversarial Search Formulation
collapse: open

Besides the rest, there will <span style='color:var(--mk-color-red)'>not</span> be any:
- Transition model (*Relies on actions*)
- Action cost function (*No need to get the optimal solution*)

However the 2 will be replaced with:
- **Terminal states** - States where the **game ends** (*End states*)
- **Utility function** - **Evaluate the value** of the state at the <span style='color:var(--mk-color-yellow)'>end of the game</span> (*Win +1, lose -1*)
```
## Minimax

The idea of <span style='color:var(--mk-color-turquoise)'>minimax</span> is to <span style='color:var(--mk-color-yellow)'>maximise</span> the best outcome out of all the <span style='color:var(--mk-color-yellow)'>minimum outcomes given by the other player</span>. This works if the <b>opponent plays optimaly</b>.

>[!question] What does this mean in a game?
>Lets imagine there are 2 players, <span style='color:var(--mk-color-purple)'>player 1 goes first</span> and <span style='color:var(--mk-color-teal)'>player 2 goes second</span>.
>
><span style='color:var(--mk-color-purple)'>Player 1</span> will obviously **want to pick the best move** inorder to win.
>
><span style='color:var(--mk-color-teal)'>Player 2</span> wants to **pick the worst outcome** for <span style='color:var(--mk-color-purple)'>player 1</span> inorder to win.
>
>Both players know this and to <b><mark style='background:var(--mk-color-green)'>play optimaly</mark></b> they will have to <span style='color:var(--mk-color-yellow)'>analyse the best move the other player will make</span> if they were to take this action.

There will be <span style='color:var(--mk-color-orange)'>2 functions</span> a `find_max` and a `find_min` function:
- The `find_max` function will one by one take all successors (*neighbours*) and pass it to the `find_min` (*which will return some **score***) and <span style='color:var(--mk-color-green)'>take the best successor</span> (*Highest score*).
- The `find_min` function will similarly one by one takes all the successors and pass it to the `find_max` but it will <span style='color:var(--mk-color-red)'>take the worst successor</span> instead.
- This *"Ping-pong"* function will stop if the state is a <span style='color:var(--mk-color-turquoise)'>terminal state</span> (*No more neighbours*) at which case it will **return the value of that state**.

**Time Complexity** : <b>O(b<sup>m</sup>)</b>
**Space Complexity** : <b>O(bm)</b> (*Is just [[Problem Solving by Searching#Depth-First Search (DFS)|DFS]]*)
**Optimal** : <b><mark style='background:#20bf6b'>Yes</mark></b> (*As long as the other player plays optimally*)
**Complete** : <b><mark style='background:#20bf6b'>Yes</mark></b> (*As long as it is finite*)

There is also a augment to <span style='color:var(--mk-color-turquoise)'>minimax</span> by **adding a depth limit**, which is called a <span style='color:var(--mk-color-turquoise)'>cutoff</span>. Basically in addition to checking weather a state is a <span style='color:var(--mk-color-turquoise)'>terminal state</span>, it <span style='color:var(--mk-color-yellow)'>checks if the depth has exceeded or not</span>.

If it did, then a heuristic function will be used to <span style='color:var(--mk-color-yellow)'>check how good the state is and return that value</span>.
> Note that <b>there is no correctness or admissibility</b> in this heuristic function, it is just an estimate function.
### Alpha-beta Pruning

It is a <span style='color:var(--mk-color-green)'>optimisation technique</span> for <span style='color:var(--mk-color-turquoise)'>minmax algorithm</span>.

The idea is that **early termination** can happen, <span style='color:var(--mk-color-green)'>resulting in less computation</span> time (*Remove unneeded expansion of the states*).

**Example of the algorithm:**
![[Alpha-beta Pruning Example.png|center|400]]

**Alpha** ($\alpha$) is for the <span style='color:var(--mk-color-purple)'>max player</span>, while **beta** ($\beta$) is for the <span style='color:var(--mk-color-teal)'>min player</span>.

Based on the example above, lets say that after **DFS** on the first state, the score for the <span style='color:var(--mk-color-purple)'>max player</span> is 3, then moving to the next successor, the <span style='color:var(--mk-color-teal)'>min player</span> has found a **successor state that has a value of 2**.

Logically since the <span style='color:var(--mk-color-purple)'>max player</span> will want to **take the higher number**, then there is no point in continuing the search for the <span style='color:var(--mk-color-teal)'>min player</span> since he will pick a state $\le$ 2 but the <span style='color:var(--mk-color-purple)'>max player</span> has found a state which gives him a value of 3.

Therefore there is no point in continuing the search since the the <span style='color:var(--mk-color-purple)'>max player</span> will pick the other state anyways for a higher value.

The other **states that are not evaluated** are <span style='color:var(--mk-color-turquoise)'>pruned</span>. This is known as <span style='color:var(--mk-color-turquoise)'>meta-reasoning</span>, weather <span style='color:var(--mk-color-yellow)'>computations should be done or not</span>.

If a **perfect ordering of the successors** happen then the <span style='color:var(--mk-color-green)'>time complexity can improved</span> to be O($b^{\frac{m}{2}}$).