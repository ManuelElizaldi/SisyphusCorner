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
	- The DAG object, is imported from airflow.models, you declare it as follows:
		- dag = DAG()

[[Task Definition]]: Tasks use [[operators]] to determine _how_ they are going to do things. Each has an id, and contain a command. Each task is assigned to the DAG they belong to.
	Task 1>> task2 
		This determines the order of the pipeline

[[Code]] example:
```python
from datetime import timedelta

# Dag object, this will allow us to iniate a DAG object:
from airflow.models import DAG

# Operator, these are needed to write tasks
from airflow.operators.bash_operator import BashOperator

# This makes scheduling easy
from airflow.utils.dates import days_ago

# Defining  DAG argument 
default_args = {
'owner' : 'manuel',
'start_date' : days_ago(0), # this will start it today
'email' : ['manuelelizaldib@gmail.com'], # for some reason, they put it in a list, I imagine this is because you can add more emails.
'retries' : 1, # in int 
'retry_delay' : timedelta (5) # not sure why we do time delta here
}

# Defining the DAG
# DAG object is imported 
dag - DAG(
	'my-first-dag',
	default_args = default_args,
	description = 'My first DAG',
	schedule_interval = timedelta(days = 1)
)

# Defining the first task
# Operators are imported
extract = BashOperator(
	task_id = 'extract',
	bash_command = 'cut -d":" -f1,3,6 etc/passwd > /home/project/airflow',
	dag = dag
)

# Defining the second task
transform_and_load = BashOperator(
	task_id = 'transform_and_load',
	bash_command = 'tr ":" "," < /home/project/airflow/dags/extracted-data.txt > /home/project/airflow/dags/transformed-data.csv',
	dag = dag
) 

# Task pipeline
extract >> transform_and_load
```
## Submitting a DAG
All the python scripts you write, need to be stored in the _dags folder_ inside _AIRFLOW_HOME_ directory. 
	Note: I am assuming, once you install airflow in your computer, this directory will be created.

You also need to run the following command

```shell
export AIRFLOW_HOME=/home/project/airflow
echo $AIRFLOW_HOME
```

Then you run the following command to submit your DAG to airflow

```shell
export AIRFLOW_HOME=/home/project/airflow
cp my_first_dag.py $AIRFLOW_HOME/dags
```


---
### Reference