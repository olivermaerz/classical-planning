# Logs

Results from `run_search.py` on the air cargo problems. 

P1 has **20** actions in the domain.
P2 has **72**.
P3 has **88**.
P4 has **104**.

---

## Problem 1 (20 actions)


| Search | Heuristic   | Expansions | Goal tests | New nodes | Plan length | Time (s) |
| ------ | ----------- | ---------- | ---------- | --------- | ----------- | -------- |
| BFS    |             | 43         | 56         | 178       | 6           | 0.0013   |
| DFS    |             | 21         | 22         | 84        | 20          | 0.00070  |
| UCS    |             | 60         | 62         | 240       | 6           | 0.0020   |
| Greedy | unmet_goals | 7          | 9          | 29        | 6           | 0.00037  |
| Greedy | levelsum    | 6          | 8          | 28        | 6           | 0.027    |
| Greedy | maxlevel    | 6          | 8          | 24        | 6           | 0.019    |
| Greedy | setlevel    | 6          | 8          | 28        | 6           | 0.081    |
| A*     | unmet_goals | 50         | 52         | 206       | 6           | 0.0019   |
| A*     | levelsum    | 28         | 30         | 122       | 6           | 0.067    |
| A*     | maxlevel    | 43         | 45         | 180       | 6           | 0.065    |
| A*     | setlevel    | 33         | 35         | 138       | 6           | 0.182    |


Optimal plan length on P1 is **6**. DFS is the only run that missed it (length 20).

### Example optimal plan (BFS)

```
Load(C1, P1, SFO)
Load(C2, P2, JFK)
Fly(P2, JFK, SFO)
Unload(C2, P2, SFO)
Fly(P1, SFO, JFK)
Unload(C1, P1, JFK)
```



### DFS plan (length 20, not optimal)

```
Fly(P1, SFO, JFK)
Fly(P2, JFK, SFO)
Load(C2, P1, JFK)
Fly(P1, JFK, SFO)
Fly(P2, SFO, JFK)
Unload(C2, P1, SFO)
Fly(P1, SFO, JFK)
Fly(P2, JFK, SFO)
Load(C2, P2, SFO)
Fly(P1, JFK, SFO)
Load(C1, P2, SFO)
Fly(P2, SFO, JFK)
Fly(P1, SFO, JFK)
Unload(C2, P2, JFK)
Unload(C1, P2, JFK)
Fly(P2, JFK, SFO)
Load(C2, P1, JFK)
Fly(P1, JFK, SFO)
Fly(P2, SFO, JFK)
Unload(C2, P1, SFO)
```

---



## Problem 2 (72 actions)


| Search | Heuristic   | Expansions | Goal tests | New nodes | Plan length | Time (s) |
| ------ | ----------- | ---------- | ---------- | --------- | ----------- | -------- |
| BFS    |             | 3,343      | 4,609      | 30,503    | 9           | 0.45     |
| DFS    |             | 624        | 625        | 5,602     | 619         | 0.57     |
| UCS    |             | 5,154      | 5,156      | 46,618    | 9           | 0.67     |
| Greedy | unmet_goals | 17         | 19         | 170       | 9           | 0.0035   |
| Greedy | levelsum    | 9          | 11         | 86        | 9           | 0.59     |
| Greedy | maxlevel    | 27         | 29         | 249       | 9           | 0.88     |
| Greedy | setlevel    | 9          | 11         | 84        | 9           | 1.95     |
| A*     | unmet_goals | 2,467      | 2,469      | 22,522    | 9           | 0.50     |
| A*     | levelsum    | 357        | 359        | 3,426     | 9           | 14.8     |
| A*     | maxlevel    | 2,887      | 2,889      | 26,594    | 9           | 84.4     |
| A*     | setlevel    | 1,037      | 1,039      | 9,605     | 9           | 175.2    |


Optimal plan length on P2 is **9**. DFS returned a 619-step plan (omitted here).

### Example optimal plan (BFS)

```
Load(C1, P1, SFO)
Load(C2, P2, JFK)
Load(C3, P3, ATL)
Fly(P2, JFK, SFO)
Unload(C2, P2, SFO)
Fly(P1, SFO, JFK)
Unload(C1, P1, JFK)
Fly(P3, ATL, SFO)
Unload(C3, P3, SFO)
```

---



## Problem 3 (88 actions)


| Search | Heuristic   | Expansions | Goal tests | New nodes | Plan length | Time (s) |
| ------ | ----------- | ---------- | ---------- | --------- | ----------- | -------- |
| BFS    |             | 14,663     | 18,098     | 129,625   | 12          | 2.21     |
| Greedy | unmet_goals | 25         | 27         | 230       | 15          | 0.0088   |
| Greedy | levelsum    | 14         | 16         | 126       | 14          | 1.32     |
| A*     | unmet_goals | 7,388      | 7,390      | 65,711    | 12          | 1.64     |
| A*     | levelsum    | 369        | 371        | 3,403     | 12          | 27.9     |


BFS and A*+unmet_goals/A*+levelsum plan length **12**. Greedy unmet_goals was 15; greedy levelsum was 14.

### Example plan (BFS, length 12)

```
Load(C1, P1, SFO)
Load(C2, P2, JFK)
Fly(P2, JFK, ORD)
Load(C4, P2, ORD)
Fly(P1, SFO, ATL)
Load(C3, P1, ATL)
Fly(P1, ATL, JFK)
Unload(C1, P1, JFK)
Unload(C3, P1, JFK)
Fly(P2, ORD, SFO)
Unload(C2, P2, SFO)
Unload(C4, P2, SFO)
```

---



## Problem 4 (104 actions)


| Search | Heuristic   | Expansions | Goal tests | New nodes | Plan length | Time (s) |
| ------ | ----------- | ---------- | ---------- | --------- | ----------- | -------- |
| BFS    |             | 99,736     | 114,953    | 944,130   | 14          | 20.3     |
| Greedy | unmet_goals | 29         | 31         | 280       | 18          | 0.014    |
| Greedy | levelsum    | 17         | 19         | 165       | 17          | 2.34     |
| A*     | unmet_goals | 34,330     | 34,332     | 328,509   | 14          | 11.1     |
| A*     | levelsum    | 1,208      | 1,210      | 12,210    | 15          | 156.5    |


BFS and A*+unmet_goals plan length **14**. 
A* + levelsum was 15; greedy levelsum was 17.
Greedy + unmet_goals was 18.

### Example plan (BFS, length 14)

```
Load(C1, P1, SFO)
Fly(P1, SFO, ATL)
Load(C3, P1, ATL)
Fly(P1, ATL, ORD)
Load(C4, P1, ORD)
Load(C5, P1, ORD)
Fly(P1, ORD, JFK)
Load(C2, P1, JFK)
Unload(C1, P1, JFK)
Unload(C3, P1, JFK)
Unload(C5, P1, JFK)
Fly(P1, JFK, SFO)
Unload(C2, P1, SFO)
Unload(C4, P1, SFO)
```
