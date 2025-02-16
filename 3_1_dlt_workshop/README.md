# dlt Homework

### Question 1

```bash
pip install "dlt[duckdb]"

pip --version
```

**Answer:** 1.6.1

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


### Question 2


**Answer:** 4


### Question 3


**Answer:** 10000


### Question 4


**Answer:** 12.3049
