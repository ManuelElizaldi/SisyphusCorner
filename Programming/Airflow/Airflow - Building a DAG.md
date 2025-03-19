2025-03-19
Tags: [[Airflow]] [[Data Engineering]] [[Programming]] [[DAG]]

## DAG Definition Script

Python Script Block:
- Python library imports
	- DAG Arguments
			- DAG Definition
				- Task Definition - nodes
					- Task pipeline

[[DAG arguments]]: are defined as a python dictionary. The key value pairs define the owner, when the task is going to start, how many retires - this could be empty -, the retries delay and many other arguments that help you build tasks.
	dag_arguments {}

[[DAG Definition]]: initiates your workflow as a DAG. Here you declare the DAG's name, its description, the default arguments - declared in the dag_argument variable - and its schedule - you can define how often it runs.

[[Task Definition]]: Tasks use [[operators]] to determine _how_ they are going to do things. Each has an id, and contain a command. Each task is assigned to the DAG they belong to.
	Task 1>> task2 
		This determines the order of the pipeline



---
### Reference