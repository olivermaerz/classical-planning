# Classical Planning Report

## Table 1 (Problems 1 and 2, all 11 searches)

Actions, expansions, plan length, time in seconds.


| Problem | Actions | Search | Heuristic   | Expansions | Plan length | Time (s) |
| ------- | ------- | ------ | ----------- | ---------- | ----------- | -------- |
| P1      | 20      | BFS    |             | 43         | 6           | 0.0013   |
| P1      | 20      | DFS    |             | 21         | 20          | 0.00070  |
| P1      | 20      | UCS    |             | 60         | 6           | 0.0020   |
| P1      | 20      | Greedy | unmet_goals | 7          | 6           | 0.00037  |
| P1      | 20      | Greedy | levelsum    | 6          | 6           | 0.027    |
| P1      | 20      | Greedy | maxlevel    | 6          | 6           | 0.019    |
| P1      | 20      | Greedy | setlevel    | 6          | 6           | 0.081    |
| P1      | 20      | A*     | unmet_goals | 50         | 6           | 0.0019   |
| P1      | 20      | A*     | levelsum    | 28         | 6           | 0.067    |
| P1      | 20      | A*     | maxlevel    | 43         | 6           | 0.065    |
| P1      | 20      | A*     | setlevel    | 33         | 6           | 0.182    |
| P2      | 72      | BFS    |             | 3,343      | 9           | 0.45     |
| P2      | 72      | DFS    |             | 624        | 619         | 0.57     |
| P2      | 72      | UCS    |             | 5,154      | 9           | 0.67     |
| P2      | 72      | Greedy | unmet_goals | 17         | 9           | 0.0035   |
| P2      | 72      | Greedy | levelsum    | 9          | 9           | 0.59     |
| P2      | 72      | Greedy | maxlevel    | 27         | 9           | 0.88     |
| P2      | 72      | Greedy | setlevel    | 9          | 9           | 1.95     |
| P2      | 72      | A*     | unmet_goals | 2,467      | 9           | 0.50     |
| P2      | 72      | A*     | levelsum    | 357        | 9           | 14.8     |
| P2      | 72      | A*     | maxlevel    | 2,887      | 9           | 84.4     |
| P2      | 72      | A*     | setlevel    | 1,037      | 9           | 175.2    |


S indices: 1 BFS, 2 DFS, 3 UCS, 4–7 greedy (unmet_goals / levelsum / maxlevel / setlevel), 8–11 A* (unmet_goals / levelsum / maxlevel / setlevel)

<div style="page-break-after: always;"></div>

### My picks for P3 and P4:


| Role       | Pick           | Why                                                                          |
| ---------- | -------------- | ---------------------------------------------------------------------------- |
| Uninformed | S1 BFS         | Fastest optimal uninformed search on P1/P2 (DFS is faster but not optimal)   |
| Greedy     | S4 unmet_goals | Greedy is by far the fastest on P2.                                          |
| Greedy     | S5 levelsum    | Fewest greedy expansions but still much faster than setlevel.                |
| A*         | S8 unmet_goals | Fastest A* on P1 and P2, and still found the short plans.                    |
| A*         | S9 levelsum    | Fewest A* expansions. A lot faster than maxlevel and setlevel on P2          |




## Table 2 (Problems 3 and 4)

P3 has **88** actions; P4 has **104**. Runs: S1 BFS, S4 greedy + unmet_goals, S5 greedy + levelsum, S8 A* + unmet_goals, S9 A* + levelsum.


| Problem | Actions | Search | Heuristic   | Expansions | Plan length | Time (s) |
| ------- | ------- | ------ | ----------- | ---------- | ----------- | -------- |
| P3      | 88      | BFS    |             | 14,663     | 12          | 2.21     |
| P3      | 88      | Greedy | unmet_goals | 25         | 15          | 0.0088   |
| P3      | 88      | Greedy | levelsum    | 14         | 14          | 1.32     |
| P3      | 88      | A*     | unmet_goals | 7,388      | 12          | 1.64     |
| P3      | 88      | A*     | levelsum    | 369        | 12          | 27.9     |
| P4      | 104     | BFS    |             | 99,736     | 14          | 20.3     |
| P4      | 104     | Greedy | unmet_goals | 29         | 18          | 0.014    |
| P4      | 104     | Greedy | levelsum    | 17         | 17          | 2.34     |
| P4      | 104     | A*     | unmet_goals | 34,330     | 14          | 11.1     |
| P4      | 104     | A*     | levelsum    | 1,208      | 15          | 156.5    |

BFS and A* + unmet_goals both found a length of 12 (P3) and 14 (P4). Both greedys were longer. A* + levelsum matched 12 on P3 but returned 15 on P4.

<div style="page-break-after: always;"></div>

### Chart 1 (Expansions):

![image](images/Expansions%20by%20Actions.svg)

Expansions grow almost exponentially as actions go from 20 to 104, except greedy, which stays almost flat. BFS and A* + unmet_goals grow exponentially (BFS is about 100k on P4). A* + levelsum grows much less. Greedy levelsum and setlevel both have 6 expansions on P1 and 9 on P2, so those two lines overlap.

<div style="page-break-after: always;"></div>

### Chart 2 (Time in s):

![image](images/Time_s%20by%20Actions.svg)

Greedy + unmet_goals stays around 0.01 seconds even on P4. A* + levelsum grows exponentially and hits 156 seconds on P4; BFS ~20 seconds and A* + unmet_goals ~11 seconds.

<div style="page-break-after: always;"></div>

### Chart 3 (Plan Length):

![image](images/Plan_length%20by%20Actions.svg)

DFS plan length blows up (20 on P1, 619 on P2). On P1/P2 most other searches are length 6 then 9, so those lines overlap (greedy levelsum and setlevel included).

<div style="page-break-after: always;"></div>

### Chart 4 (Plan Length DFS omitted for clarity):

![image](images/Plan_length%20by%20Actions%20no%20DFS.svg)

With DFS omitted the other algorithms stay close together on P1 and P2 (length 6 and 9). On P3/P4: BFS and A* + unmet_goals are the shortest lengths (12 and 14). Greedy has a longer plan length, and A* + levelsum did not find the shortest plan on P4 (15 instead of 14).

<div style="page-break-after: always;"></div>

## Questions


### Which algorithm or algorithms would be most appropriate for planning in a very restricted domain (i.e., one that has only a few actions) and needs to operate in real time?

I would pick Greedy + unmet_goals. On P1 with 20 actions it was the fastest with 0.00037 seconds and still returned a length of 6. This is almost realtime for a restricted domain. 

### Which algorithm or algorithms would be most appropriate for planning in very large domains (e.g., planning delivery routes for all UPS drivers in the U.S. on a given day)

For planning the UPS delivery routes I would use Greedy + unmet_goals. It performed well on P4 with only 29 expansions and 0.014 seconds. While it did not find the shortest plan it is the algorithm best suited for our largest problem P4.

### Which algorithm or algorithms would be most appropriate for planning problems where it is important to find only optimal plans?

For finding the optimal plan I would use BFS (found optimal plans 6, 9, 12, 14) and UCS (found optimal plans 6, 9). Both do not use heuristics. For the algorithms with heuristics I would use A* + maxlevel and A* + setlevel. The maxlevel and setlevel heuristics are admissible so A* is guaranteed to find the optimal plan.







