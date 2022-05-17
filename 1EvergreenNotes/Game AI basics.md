# Game AI basics
https://www.gamedev.net/tutorials/programming/artificial-intelligence/the-total-beginners-guide-to-game-ai-r4942/?utm_source=pocket_mylist
## Game AI
Based on conditions what actions should be made. It is controlling "intelligent agents".
Every agent works in a **Sense/Think/Act cycle**.
In game dev the "sense" part is obsolete, becaouse sensing is entrinsic to the game simulation.

- game AI is not pre-trained (nothing or little data to train on)
- no purpose of making it "optimal" - it should just make game "fun"
- It should feel like agent is controlled by a human. Logic should be understandable to a human. It was not the case with for example a highly optimal AlphaGo program, which made moves completely unobvious to the person due to depth of the computation.
- sometimes it need to run in a realtime - so resources are limited, it cannot halt the whole system until it can reach the goal.
- it is good to have it data driven so non coders can adjust it.

## Basic decision making
 - Hardcoded conditional statements
 - Decision Tree - is fancy conditional statements (+ scripting in order to reduce dependency on a coder) - basically is a block scheme.
 - Finite state machines is a more comples decision tree, where a state changes are bound to conditions too
	![[Pasted image 20220402135537.png]]
 - Hierarchical state machines (in order to elininate duplicating for closely related states)
   ![[Pasted image 20220402135544.png]]
- Concurrent state machines (two states at the same time, if we need to track several states and have some special conditions on them)
- Push down automata ()
- Behavior tree (useful for common not so state dependent decisions). If you want the decision about state taken outside the state. The tree might be trversed top-down left-right and correct decision is taken.
  ![[Pasted image 20220402140400.png]]
	In unreal engine 4 the traversing of the tree is much more complex, you may reevaluate the tree on condition, services might be attached to the nodes, some updates might happen without full reevaluation.
- Utility-based systems (RTS it is usually a priority queue of the objectives). Each action (or objective) is assigned some score based on "senses". And then the action is picked. In WatchDogs fist fight was done using utility based system.

## Movement and navigation
- Steering - just moving towards the desired location.
- Pathfinding. Might be implemented as a A* algorithm (breadth first algorithm with Dijkstra with distance to target heuristics) on a grid location. Then steering is used to move through the "path", from one cell to another. If the game does not have nodes then "NavMeshing" can generate them.
- Planning. Might be used for MtG for example. We can find a path to state which is desirable (for example which is an objective). The plans might be picked utility-based.
- Improved Planning. If we have too many paths to check for the leaf we might do backward chaining - search from the leaf, there should be much less options. Or we might find a metric to evaluate partial plans. Also there is a *Monte Caro Tree Search*. and *goal oriented action planning*.

## Learning and adapting
We still might be OK with using machine learning techniques to find if the player is using the same combo in a fighting game or the same camping spot in a shooter.
 - The game might be gathering the statistics of what the player is using and try to weight higher the counters to player's tactics.
	Also Bayesian classifiers might be used (they are usually used for the spam recognition).
	These methods might be used during the playtesting, because enabling them after release might make the game too predictable or too complicated.
 - Weight based adaptation should be good too - making some predictions based on previous runs.
 - Markov Models. Good for predictions. They predict the chances of a state change. This statistic might be collected about the player and then used against him.
![[Pasted image 20220402175542.png]]
- N-Grams. Word occurrence where word is a state and character is an action.

## Knowledge representation
All these models are based on proper observation of the world. How to turn data into knowledge?
 - Tags. Just tag important objects. Useful for querying the world for specific stuff.
 - Smart objects. The idea is not that an agent is asking for the options in the world, but the world is telling the agents about the options.
 - Response curves. When value can be measured as a continuous value then you may be using response curves (used in watch dogs)
 - Blackboard. Is a place to store the information that an agent has already picked up. Sometimes it is about an arbitrary data.
 - Influence maps. Is a data structure that represents how objects influence the area. Where are the enemies weakest point in defense for example?

## Additional algorithms (find out more about these topics)
 - optimization - hill-climbing, gradient descent, genetic algorithms
 - adversarial search/planning - minimax, alpha-beta pruning
 - classification - perceptron, neural network support vector machine
 - agent perception and memory system
 - AI architectural approach - hybrid system, subsumption architecture, other layered AI systems
 - Performance considerations - level of detail, anytime algorithm, timeslicing


---
status: #🌲
tags: #gamedev/AI #MOCsuggestion/general_programming_knowledge 
related: 