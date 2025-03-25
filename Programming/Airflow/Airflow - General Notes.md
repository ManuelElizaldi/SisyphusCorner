**03**/19/2025

Tags: [[Programming]] [[Data Engineering]] [[ETL]] [[Airflow]]

[[DAG]]: Directed Acyclic Graph. This is how workflows are represented in Airflow
	Acyclical means that all nodes have a direction, they don't go back to another node.
	The red line can be done in airflow
	![[Pasted image 20250319153433.png]]

*Airflow*: Workflow manager, not a streaming solution
	Similar to windows task scheduler

_Built in scheduler_ that submits tasks into the executor 

[[Nodes and Edges]]:

[[Nodes]] are tasks
The dependencies between nodes/tasks are the [[Edges]]
- Edges determine order
Both of these are defined by code -> Python

Tasks use [[Operators]] depending on the language that you are using.
- There are SQL, Bash, etc. operators
- Sensor operators look for triggers to start 
- These can also be started on a timer/schedule
![[Pasted image 20250319152805.png]]

*There's different types of DAGs:
- Single directed edge
- Single root and terminal node
	- root node -> starting node
- Trees
	- All trees are dags but not all trees are dags

*Important commands for air flow
- To list all dags in airflow:
	- airflow dags list 
- To list all tasks in a dag:
	- airflow tasks list "dag name"
		- You can also look at the dag's tasks in the web UI when clicking the graph button
- unpausing a dag:
	- airflow dags unpuase tutorial
- Searching for a specific DAG by name
	- airflow dags list | grep "my-first-dag" <- use the name set in the default args dictionary you defined inside your script

*Every dag is made out of tasks:

![[Pasted image 20250319135051.png]]

---
### Reference
From IBM ETL in coursera - course