03/19/2025

Tags: [[Programming]] [[Data Engineering]] [[ETL]] [[Airflow]]

[[DAG]]: Directed Acyclic Graph. This is how workflows are represented in Airflow

Airflow: Workflow manager, not a streaming solution
	Similar to windows task scheduler

Built in scheduler that submits tasks into the executor 

Important commands for air flow
- To list all dags in airflow:
	- airflow dags list 
- To list all tasks in a dag:
	- airflow tasks list "dag name"
		- You can also look at the dag's tasks in the web UI when clicking the graph button
- unpausing a dag:
	- airflow dags unpuase tutorial

Every dag is made out of tasks:

![[Pasted image 20250319135051.png]]

---
### Reference
From ETL course