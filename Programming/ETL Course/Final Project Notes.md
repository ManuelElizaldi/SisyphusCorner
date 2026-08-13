2025-4-9
Tags: [[ETL]] [[Project]] [[Apache Kafka]] [[Airflow]]

```python
from datetime import timedelta

# Dag object, this will allow us to iniate a DAG object:

from airflow.models import DAG

# Operator, these are needed to write tasks

from airflow.operators.bash_operator import BashOperator

# This makes scheduling easy

from airflow.utils.dates import days_ago

  
  

dag_arguments = {

    'owner':'Manuel',

    'start_date': days_ago(0),

    'email': ['manuelelizaldib@gmail.com'],

    'retries': 1,

    'retry_delay': timedelta(5)

}

  

dag = DAG(

    'ETL_toll_data',

    default_args = dag_arguments,

    description = 'Apache Airflow Final Assignment',

    schedule_interval = timedelta(days = 1)

)

  

unzip_data = BashOperator(

    task_id = 'unzip_data',

    bash_command = 'tar -xvzf /home/project/airflow/dags/finalassignment/tolldata.tgz -C /home/project/airflow/dags/finalassignment',

    dag = dag

)

  

extract_data_from_csv = BashOperator(

    task_id = 'extract_data_from_csv',

    bash_command = 'cut -d"," -f1,2,3,4 cut -d":" -f1,3,6 /home/project/airflow/dags/finalassignment/vehicle-data.csv > /home/project/airflow/dags/finalassignment/csv_data.csv',

    dag = dag

)
```



---
### Reference