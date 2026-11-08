# Chapter 1: From Model to Application

## 1. An experiment is not yet an application

An experiment is code used to explore an idea. An application is organised so another person or program can use it consistently.

A useful AI application often contains:
- A trained model that makes predictions.
- Preprocessing that converts incoming data into the expected format.
- Postprocessing that turns model output into a useful result.
- An interface for requests and responses.
- Error handling, tests, documentation, and monitoring.

## 2. Training versus inference

**Training** adjusts model parameters using data. **Inference** uses the trained parameters to produce a prediction.

Users of your application should not need to retrain the model every time they request a prediction. Load the model when the service starts and reuse it for requests, subject to the framework's concurrency and resource requirements.

## 3. Organise the project

One possible structure is:

```text
my-model-app/
    README.md
    requirements.txt
    app/
        __init__.py
        model.py
        service.py
    tests/
        test_service.py
    models/
        model_weights.pth
```

The `app` folder contains application code. The `tests` folder contains automated checks. The `models` folder contains saved weights in this example.

A `requirements.txt` file records dependencies:

```text
fastapi
uvicorn
torch
```

For reproducible work, record tested versions rather than relying indefinitely on whatever the newest version happens to be.

## 4. Keep the interface separate from the model

The model should perform model calculations. A service function should validate input, prepare it, call the model, and format the result. The web interface should handle communication with the user.

This separation makes testing easier. You can test the model or service without needing to start a web server.

## Check your understanding

1. What is the difference between training and inference?
2. Why separate experiments from application code?
3. What is a dependency?
4. What does `requirements.txt` record?
5. Why keep model logic separate from the web interface?

## Practice

Create the folder structure shown above. Add empty Python files and write one sentence in each explaining its intended responsibility.

**Next:** [Chapter 2 — APIs, validation, and testing](02-apis-validation-and-testing.md)
