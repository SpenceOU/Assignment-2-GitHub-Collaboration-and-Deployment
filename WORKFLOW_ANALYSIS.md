# Workflow Analysis

## 1. What triggers this workflow to run?
This workflow runs when code is pushed to the `main` branch, or when a pull request targeting `main` is opened or updated.

## 2. What are the four main steps this workflow performs?
1. Checkout code
2. Validate HTML
3. Check links
4. Upload artifact

## 3. What does the "Checkout code" step do and why is it necessary?
It downloads the repository's files onto the runner so the workflow has access to the actual code. Without this step, none of the later steps would have any files to validate, test, or deploy.

## 4. What is the purpose of the environment configuration?
The environment block tells GitHub this job deploys to the github-pages environment, which connects the run to GitHub Pages for tracking deployment status and exposing the live site URL as an output.

## 5. How does this automated deployment improve reliability compared to manual deployment?
It runs the same validation and deployment steps the same way every time, removing the chance of a human skipping a step, forgetting to test, or deploying broken code. It also eliminates "works on my machine" issues, since every deployment runs in the same clean Ubuntu environment regardless of what's installed on a developer's own computer. Because the pipeline runs automatically on every push, deployment doesn't depend on someone being available or remembering to do it manually, which also means fixes and updates can go live at any time, not just during work hours.

## 6. What would happen if you pushed code to a different branch (not main)?
The build-and-test job would only run if that push also triggered a pull request targeting main; a direct push to another branch wouldn't trigger the workflow at all, and even if it did, the deploy job explicitly only runs when github.ref == 'refs/heads/main', so nothing would deploy.