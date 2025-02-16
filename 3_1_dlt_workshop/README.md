# dlt Homework

### Question 1

```bash
pip install "dlt[duckdb]"

pip --version
```

**Answer:** 1.6.1


### Question 2

```python

import dlt
from dlt.sources.helpers.rest_client import RESTClient
from dlt.sources.helpers.rest_client.paginators import PageNumberPaginator


@dlt.resource(name="rides") 
def ny_taxi():
    client = RESTClient(
        base_url="https://us-central1-dlthub-analytics.cloudfunctions.net",
        paginator=PageNumberPaginator(
            base_page=1,
            total_path=None
        )
    )

    for page in client.paginate("data_engineering_zoomcamp_api"):
        yield page 


# define new dlt pipeline
pipeline = dlt.pipeline(destination="duckdb")


pipeline = dlt.pipeline(
    pipeline_name="ny_taxi_pipeline",
    destination="duckdb",
    dataset_name="ny_taxi_data"
)


```

![image](https://github.com/user-attachments/assets/2c427d69-85d5-473e-9e55-bb8ed651f033)


**Answer:** 4


### Question 3

```python
df = pipeline.dataset(dataset_type="default").rides.df()
df
```

![image](https://github.com/user-attachments/assets/f2e79e05-bb67-4df3-ac22-d636d3d8e773)


**Answer:** 10000


### Question 4

```python
with pipeline.sql_client() as client:
    res = client.execute_sql(
            """
            SELECT
            AVG(date_diff('minute', trip_pickup_date_time, trip_dropoff_date_time))
            FROM rides;
            """
        )
    # Prints column values of the first row
    print(res)
```

**Answer:** 12.3049
