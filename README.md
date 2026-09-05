Udacity _Classical Planning_ project: a progression-search planner with planning-graph mutexes and heuristics, used to solve air cargo problems and compare search algorithms.

Setup with [uv](https://docs.astral.sh/uv/): `uv venv --python 3.9 venv && source venv/bin/activate`

You can compare search algorithms on the air cargo problems with `python run_search.py -m`, or pick them with `-p` (problems 1–4) and `-s` (search algorithms). For example, `python run_search.py -p 1 2 -s 1 2` runs problems 1 and 2 with breadth-first and depth-first search.

Run the tests with `python -m unittest -v`. Experiment results and analysis are in `report.pdf`.

Udacity also provided a small have-cake example (`python example_have_cake.py`); I left it as-is.

Starter code is from Udacity (MIT License).
