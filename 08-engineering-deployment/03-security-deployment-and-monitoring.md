# Chapter 3: Security, Deployment, and Monitoring

## 1. Protect secrets

A **secret** is sensitive information such as an API key, password, or private token. Do not hard-code secrets into source files or commit them to Git.

Use environment variables or a dedicated secrets manager. Keep local secret files out of version control with `.gitignore`. If a secret is exposed, revoke or rotate it; deleting the visible line from a later commit does not erase it from the repository's history.

## 2. Think about user data

An AI application may receive private text, documents, or other personal information. Collect only what is needed. Explain how data is used and stored. Set sensible retention limits and protect stored data.

Do not train on user submissions without a clear, appropriate permission and policy. Protect logs too: they can accidentally contain private prompts or credentials.

## 3. Development and production

A **development environment** is where you build and test changes. **Production** is the environment used by real users.

A development server is not automatically ready for public use. Before deployment:
- Disable development-only settings.
- Configure secrets securely.
- Set request and file-size limits.
- Add authentication when needed.
- Use HTTPS for traffic.
- Test failure handling.
- Plan how to update and roll back releases.

## 4. Monitoring

**Monitoring** means observing a running service to understand its health and behaviour.

Useful signals include:
- Request count and response time.
- Error rates.
- Memory and CPU usage.
- Model loading failures.
- Input sizes and resource consumption.
- Model quality indicators, where they can be measured responsibly.

Avoid logging sensitive user content unless there is a justified, protected process for doing so.

## 5. Model limitations

A deployed model can fail when real-world inputs differ from training data. This is often called **distribution shift**. Monitor performance and provide a way to report problems.

A model should not be treated as correct merely because the API returns a successful response. Technical availability and prediction quality are different things.

## Check your understanding

1. Why should secrets not be committed to Git?
2. What is the difference between development and production?
3. Why use HTTPS?
4. Name three signals that monitoring can track.
5. What is distribution shift?
6. Why is an HTTP success response not proof that a prediction is correct?

## Final project

Turn your small trained model into a documented service. Include:
- A clear installation guide.
- A model-loading function.
- An input-validation layer.
- A prediction endpoint.
- Automated tests.
- Secure configuration for secrets.
- A deployment guide.
- A section describing limitations and monitoring.

Do not publish private datasets, credentials, or model files unless you have checked their rights and security implications.

## Course completion

You have followed the path from programming tools to a small trained model and an application that can serve predictions. Building a production-quality AI system takes further work: stronger evaluation, security reviews, data governance, infrastructure, and ongoing monitoring. Keep learning by improving one part of your project at a time.
