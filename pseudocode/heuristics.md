# Overview

Heuristics derived from the planning graph are defined in Chapter 10 of Artificial Intelligence: a Modern Approach (AIMA) 3rd edition (Chapter 11 in the 2nd edition–linked in the project readme).  The pseudocode below provides functional descriptions of the three planning graph heuristics that must be implemented for this project.

Note that the pseudocode is *accurate*, but it isn't necessarily *efficient* to compute them this way.  The most significant inefficiency is that each function starts by building a *complete* planning graph until it levels off.  However, in many cases the heuristics can be computed before the full planning graph is built.  See the last section below for an example of changing the pseudocode for the MaxLevel heuristic so that it incrementally constructs the planning graph, cutting the runtime for that heuristic on most problems in half.  You should discuss the other heuristics below with your peers to look for more efficient implementations.

## LevelCost

The level cost is a helper function used by MaxLevel and LevelSum. The level cost of a goal is equal to the level number of the first literal layer in the planning graph where the goal literal appears.

---

**function** LevelCost(*graph*, *goal*) **returns** a value  
&emsp;**inputs:**  
&emsp;&emsp;*graph*, a leveled planning graph  
&emsp;&emsp;*goal*, a literal that is a goal in the planning graph  

&emsp;**for each** *layeri* in *graph.literalLayers* **do**  
&emsp;&emsp;**if** *goal* in *layeri* **then return** i  

---



## MaxLevel

> The max-level heuristic simply takes the maximum level cost of any of the goals; this is admissible, but not necessarily accurate.

&emsp;—AIMA Chapter 10

---

**function** MaxLevel(*graph*) **returns** a value  
&emsp;**inputs:**  
&emsp;&emsp;*graph*, an initialized (unleveled) planning graph  

&emsp;*costs* = []  
&emsp;*graph*.fill()  */* fill the planning graph until it levels off */*  
&emsp;**for each** *goal* in *graph.goalLiterals* **do**  
&emsp;&emsp;*costs*.append(**LevelCost**(*graph*, *goal*))  
&emsp;**return max**(*costs*)  

---



## LevelSum

> The level sum heuristic, following the subgoal independence assumption, returns the sum of the level costs of the goals; this can be inadmissible but works well in practice for problems that are largely decomposable.

&emsp;—AIMA Chapter 10

---

**function** LevelSum(*graph*) **returns** a value  
&emsp;**inputs:**  
&emsp;&emsp;*graph*, an initialized (unleveled) planning graph  

&emsp;*costs* = []  
&emsp;*graph*.fill()  */* fill the planning graph until it levels off */*  
&emsp;**for each** *goal* in *graph.goalLiterals* **do**  
&emsp;&emsp;*costs*.append(**LevelCost**(*graph*, *goal*))  
&emsp;**return sum**(*costs*)  

---



## SetLevel

> The set-level heuristic finds the level at which all the literals in the conjunctive goal appear in the planning graph without any pair of them being mutually exclusive.

&emsp;—AIMA Chapter 10

---

**function** SetLevel(*graph*) **returns** a value  
&emsp;**inputs:**  
&emsp;&emsp;*graph*, an initialized (unleveled) planning graph  

&emsp;*graph*.fill()  */* fill the planning graph until it levels off */*  
&emsp;**for** *layeri* in *graph.literalLayers* **do**  
&emsp;&emsp;*allGoalsMet* <- *true*  
&emsp;&emsp;**for each** *goal* in *graph.goalLiterals* **do**  
&emsp;&emsp;&emsp;**if** *goal* not in *layeri* **then** *allGoalsMet* <- *false*  
&emsp;&emsp;**if** not *allGoalsMet* **then** continue  

&emsp;&emsp;*goalsAreMutex* <- *false*  
&emsp;&emsp;**for each** *goalA* in *graph.goalLiterals* **do**  
&emsp;&emsp;&emsp;**for each** *goalB* in *graph.goalLiterals* **do**  
&emsp;&emsp;&emsp;&emsp;**if** *layeri*.isMutex(*goalA*, *goalB*) **then** *goalsAreMutex* <- *true*  
&emsp;&emsp;**if** not *goalsAreMutex* **then return** *i*

---

