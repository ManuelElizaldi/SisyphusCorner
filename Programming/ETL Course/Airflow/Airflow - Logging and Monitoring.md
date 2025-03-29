2025-03-25
Tags:# [[Airflow]] [[Data Engineering]] [[Programming]] [[Monitoring]]

## Logging
Logging allows for debugging and tracking down issues. 

Log files are saved as local files by default.

Airflow production log files can be sent to cloud storage.

Logs can also be sent to search engines and dashboards.
	Airflow recommends [[Elasticsearch]] and [[Splunk]]

Airflow saves logs of DAGs that have been executed. You can also access DAG status in the Web UI.

Every log will have a dag_id, run_id, task_id and an attempt value.
	note: attempt value is determined by how many attempts/retries you set on your [[DAG arguments]]

![[Pasted image 20250325214200.png]]

## Monitoring

- Counters: They are always increasing
	- Number of successful DAGs
	- Number of failed DAGs

- Gauges: These may fluctuate
	- Number of current running DAGs
	- DAG bag size -> number of DAGs that the scheduler loads into memory at once. A big bag size can slow down performance.

- Timers: Metrics related to time duration.
	- Milliseconds to finish a task
	- Milliseconds to reach a successful or failed state

Airflow recommends using a specialized [[software]] to store metrics.
	Examples: [[StatsD]] or [[Prometheus]]





---
### Reference
IBM ETL Course Module 3