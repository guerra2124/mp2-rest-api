# MP2 REST API

This project is a FastAPI application that turns my MP1 data pipeline into a REST API. `GET /health` reports the app's status and version, `POST /upload` accepts a CSV file and stores it in memory with an integer ID, and `GET /datasets/{dataset_id}` returns up to `limit` rows along with the dataset's total row count. `POST /datasets/{dataset_id}/process` validates and cleans a stored dataset by reusing my MP1 modules in `data_pipeline/` (validation, duplicate removal, missing-value handling, and optional outlier removal), then returns a cleaning report and replaces the stored data only after processing succeeds. A logging middleware records each request's ID, method, path, status code, and duration, and adds an `X-Request-ID` header to every response. Tests in `tests/` use pytest and FastAPI's TestClient.

## Run

    python -m pip install -r requirements.txt
    python -m uvicorn main:app --reload

Then open http://127.0.0.1:8000/docs.

## Test

    python -m pytest tests -v