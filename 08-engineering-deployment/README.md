# 08 — Engineering & Deployment

A model that runs in a notebook is not automatically a useful application. This module teaches how to package a model, expose it through an interface, test it, monitor it, and deploy it responsibly.

**Prerequisites:** [07 — Train Your Own Small Model](../07-training-a-model/README.md), basic Python, and familiarity with files, functions, and virtual environments.

[Back to course home](../README.md)

---

# Lesson 1 — From experiment to application

An experiment is code used to explore an idea. An application is organised so another person or program can use it reliably.

A useful AI application often contains:
- A model that makes predictions.
- Preprocessing that prepares input in the expected format.
- Postprocessing that turns model output into a usable result.
- An interface through which users provide input and receive output.
- Error handling, tests, and documentation.

The **inference** process is using a trained model to make a prediction. Training adjusts parameters; inference uses the trained parameters to produce outputs.

Keep training code separate from inference code where practical. Users of your application should not need to retrain the model every time they ask for a prediction.

### Checkpoint

1. What is the difference between training and inference?
2. Why separate experimentation from the application?
3. What might preprocessing do before inference?

---

# Lesson 2 — Organise a Python project

A clear folder structure makes code easier to understand and maintain.

Example:

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

This is one possible layout, not a rule. The `app` folder contains application code, `tests` contains automated checks, and `models` contains saved model files.

A **dependency** is an external library or package your project needs. A `requirements.txt` file can list dependencies:

```text
torch
fastapi
uvicorn
```

For reproducible projects, record tested package versions. Install with:

```bash
python -m pip install -r requirements.txt
```

Do not commit large model files or private datasets blindly. Check repository size limits, licensing, and whether the file should be stored in a dedicated model or artifact store.

### Checkpoint

1. What is a dependency?
2. What is `requirements.txt` used for?
3. Why should tests live in a separate folder?
4. Why might model weights not belong in a normal source-code repository?

---

# Lesson 3 — Create a prediction function

A prediction function should accept a clearly defined input, prepare it, call the model, and return a predictable result.

A simple example without a real neural network:

```python
def predict_length(text: str) -> dict:
    if not isinstance(text, str):
        raise TypeError("text must be a string")

    cleaned = text.strip()
    if not cleaned:
        raise ValueError("text must not be empty")

    return {
        "character_count": len(cleaned)
    }
```

This example is not AI; it demonstrates the shape of a reliable service function. It validates input and returns a dictionary with a named result.

When connecting a trained model, load the model once when the application starts rather than loading its weights for every request. Put the model in evaluation mode and use the framework's inference mode where appropriate.

### Checkpoint

1. Why validate an input?
2. What is the difference between a TypeError and a ValueError in the example?
3. Why load a model once rather than for every request?
4. Why should a prediction function return a predictable structure?

---

# Lesson 4 — Expose a model with an API

An **API** (Application Programming Interface) is a defined way for one program to communicate with another. A web API commonly accepts HTTP requests and returns responses.

An HTTP request has a method and a destination. Common methods include:
- GET: retrieve information.
- POST: send information for processing or creation.

A simple FastAPI application:

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

    return {"character_count": len(cleaned)}
```

This is a demonstration API, not a model-backed prediction service. It accepts a JSON body with a `text` field and returns a count. Later, replace the example calculation with your model's inference function.

Install and run:

```bash
python -m pip install fastapi uvicorn
uvicorn main:app --reload
```

This assumes the code is saved in `main.py`. The command starts a local development server. The `--reload` option restarts it when code changes; it is for development, not a production setting.

FastAPI provides interactive API documentation while the local server is running, commonly at `/docs`.

### Checkpoint

1. What is an API?
2. What is the difference between GET and POST?
3. What data does the example endpoint accept?
4. Why is `--reload` intended for development?

---

# Lesson 5 — Testing and error handling

A **test** is code that checks whether another piece of code behaves as expected. Tests help catch mistakes when you change the application.

For the example prediction function:

```python
def test_predict_length():
    result = predict_length("  hello  ")
    assert result["character_count"] == 5
```

An **assertion** checks that a condition is true. If it is false, the test fails.

Useful tests include:
- Normal input.
- Empty input.
- Input with spaces.
- Very long input.
- Unexpected input types.
- Model loading failure.
- Model output with an unexpected shape.

Do not return a successful-looking prediction when the model has failed. Return a clear error and log enough detail for developers to investigate, without exposing secrets or private data to users.

### Checkpoint

1. What does a test check?
2. What does an assertion do?
3. Why test empty and unexpected inputs?
4. Why should an application not hide model failures?

---

# Lesson 6 — Security and responsible use

A deployed model can receive untrusted input. Treat user input as data, not as instructions to your server or operating system.

Important practices:
- Never hard-code passwords, API keys, or tokens into source code.
- Store secrets in environment variables or a dedicated secret manager.
- Validate input type, length, and format.
- Limit request size and rate where appropriate.
- Keep dependencies updated.
- Avoid logging private prompts or personal information unnecessarily.
- Restrict access to model files and administrative endpoints.
- Make the model's limitations clear.

A model can produce incorrect, biased, or unsafe outputs. Evaluate the system in the context where it will be used. Add human review and safeguards when the consequences of an error are significant.

### Checkpoint

1. Why should API keys not be committed to Git?
2. Why validate the length of user input?
3. What is one privacy risk of logging every prompt?
4. Why must model limitations be explained?

---

# Lesson 7 — Performance and monitoring

A deployed service should be measured, not guessed about.

Useful measurements include:
- **Latency:** how long a request takes.
- **Throughput:** how many requests can be handled in a period.
- **Error rate:** how often requests fail.
- **Resource use:** CPU, memory, and accelerator usage.

A **cold start** is the delay when an application or model has to initialise before serving a request. Loading a large model can make the first request slower.

A **health check** is an endpoint or test that reports whether a service is running. It does not necessarily prove that predictions are correct.

Monitoring can help detect crashes, slow responses, resource exhaustion, and changes in input patterns. Avoid collecting more user data than necessary.

### Checkpoint

1. What does latency measure?
2. What is throughput?
3. What is a cold start?
4. Does a health check prove the model is accurate?

---

# Lesson 8 — Deployment and documentation

**Deployment** means making an application available in an environment where intended users can access it. This might be a private server, a cloud platform, or a managed application service.

Before deployment:
1. Run automated tests.
2. Check the dependency versions.
3. Confirm that secrets are configured outside source code.
4. Confirm the model file and licence permit the intended use.
5. Test the application using realistic but non-sensitive examples.
6. Set resource and request limits.
7. Document how to start, stop, and update the service.
8. Prepare a rollback plan in case a release fails.

A development server is not automatically production-ready. Production deployment may require a process manager, HTTPS, authentication, monitoring, backups, scaling, and platform-specific configuration.

A good README should explain:
- What the application does.
- What it does not do.
- Installation steps.
- Configuration options.
- How to run tests.
- How to start the service.
- Example requests and responses.
- Known limitations and licence details.

### Checkpoint

1. What is deployment?
2. Why are tests important before deployment?
3. Why is a development server not automatically suitable for production?
4. What should a useful project README explain?

---

## Capstone — Deploy your small model responsibly

Take the small model you trained in Module 07 and create a local application around it.

Required deliverables:
1. A clean project structure.
2. A documented environment and dependencies.
3. A model-loading function.
4. An inference function with input validation.
5. A simple API endpoint.
6. Tests for normal and invalid inputs.
7. A README with setup and usage instructions.
8. A short report on limitations, privacy, and performance.

Start locally. Test the application before considering public deployment. Do not upload secrets, private datasets, or model files you do not have permission to share.

## Vocabulary

| Term | Meaning |
|---|---|
| Application | A program organised for users or other software |
| Inference | Using a trained model to make predictions |
| Dependency | An external package a project needs |
| API | A defined interface for software communication |
| HTTP | A protocol commonly used for web communication |
| Endpoint | A particular API address and operation |
| Request | A message sent to a service |
| Response | A message returned by a service |
| Test | Code that checks expected behaviour |
| Assertion | A check that a condition is true |
| Secret | Sensitive configuration such as an API key |
| Latency | Time taken to complete a request |
| Throughput | Amount of work handled per unit of time |
| Cold start | Initialisation delay before a service is ready |
| Deployment | Making an application available in its target environment |
| Monitoring | Observing a service's health and behaviour |

## You have completed the roadmap

You have moved from basic programming tools through machine learning, neural networks, language processing, transformers, model training, and application deployment.

That does not mean you know everything about AI. It means you now have a foundation and a working project you can improve. Continue by experimenting, reading technical documentation, testing your assumptions, and building increasingly capable systems.

[Back to the course home](../README.md)
