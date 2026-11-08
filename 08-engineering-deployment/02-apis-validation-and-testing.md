# Chapter 2: APIs, Validation, and Testing

## 1. What is an API?

An **Application Programming Interface (API)** is a defined way for one program to communicate with another. A web API commonly accepts HTTP requests and returns responses.

Common HTTP methods include:
- GET: retrieve information.
- POST: send information for processing or creation.
- PUT or PATCH: update information.
- DELETE: remove information.

An endpoint is a specific address and method combination that performs an operation, such as `POST /predict`.

## 2. A demonstration API

Install FastAPI and Uvicorn:

```bash
python -m pip install fastapi uvicorn
```

Create `main.py`:

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class PredictionRequest(BaseModel):
    text: str

@app.get("/")
def health_check():
    return {"status": "ok"}

@app.post("/predict")
def predict(request: PredictionRequest):
    cleaned = request.text.strip()
    if not cleaned:
        return {"error": "Text cannot be empty"}

    # Demonstration only: this is not an AI prediction.
    return {"character_count": len(cleaned)}
```

Run it:

```bash
uvicorn main:app --reload
```

The command assumes the code is in `main.py`. The `--reload` option is for local development; it restarts the server when code changes.

This example counts characters. It demonstrates request handling, not model inference. Later, replace the demonstration calculation with a function that calls your trained model.

## 3. Validate inputs

**Validation** checks that incoming data has the expected form and is acceptable for the application.

Examples:
- Ensure text is actually a string.
- Reject empty input when the model requires content.
- Limit input length to protect memory and processing time.
- Check that numerical values fall within sensible ranges.

Do not trust user input simply because it came through your own interface.

## 4. Test the application

A **test** checks whether a piece of software behaves as expected. Unit tests check small functions. Integration tests check that multiple components work together.

For a prediction service, test:
- A normal valid request.
- Empty text.
- Unexpected data types.
- Very long input.
- Model loading failures.
- A response with the expected structure.

A test passing does not prove the entire application is secure or correct, but tests catch regressions and document expected behaviour.

## Check your understanding

1. What is an API?
2. What is an endpoint?
3. When might GET and POST be used?
4. Why validate incoming data?
5. What is the difference between a unit test and an integration test?
6. Is the character-count example a real AI model prediction?

## Practice

Add a test for the demonstration function that checks ordinary text and empty text. Then describe how you would replace the character counter with your model's inference function.

**Next:** [Chapter 3 — Security, deployment, and monitoring](03-security-deployment-and-monitoring.md)
