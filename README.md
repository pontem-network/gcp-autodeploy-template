# Autodeploy from PR's

## To create new deployments and deploy a test app from pull requests (PRs) on Cloud Run, follow these steps:

1. Copy the following two files to your repository:
- `autodeploy.yaml` to `.github/workflows/autodeploy.yaml`
- `cloudbuild.yaml` to `.build/cloudbuild.yaml`

These files contain the necessary configuration for automated deployment workflows

2. Next, reach out to our DevOps team and ask them to enable the required secrets for your repository. 

By setting up these files and configuring the required secrets, your test app can be automatically deployed from PRs on the GCP infrastructure. This approach assumes that your app does not require a database or complex configuration, allowing for a straightforward deployment process.

Make sure to review and customize the contents of the `autodeploy.yaml` and `cloudbuild.yaml` files according to your specific deployment requirements and project structure.

For example, if your app uses a port other than the default port (such as port 3000), you would need to modify the necessary configuration to accommodate this change. Here are some guidelines:

If your app requires environment variables during the build stage, you can set them as an array for the _BUILD_ARGS variable. This allows you to pass specific build-time environment variables to your application during the deployment process.

```
env:
    _BUILD_ARGS: "NODE_ENV=development,SOME_OTHER_KEY=value"
```

If your app requires environment variables during startup, you can set them in the _ENVS variable. This allows you to specify the runtime environment variables that should be available to your application when it starts.

```
env:
    _ENVS: "KEY=value,SOME_OTHER_KEY=value2"
```

Modify the configuration files (`autodeploy.yaml` and `cloudbuild.yaml`) accordingly to reflect the desired changes. Don't hesitate to collaborate with our DevOps team to ensure a smooth and successful deployment. They are there to assist you in making the necessary adjustments and optimizing your deployment process

If all the configurations and modifications are done correctly, you should be able to access your fresh app at the following URL:

```
https://${BRANCH_NAME}.${PROJECT_NAME}.devops.mom
```

Please note that the stands or deployments created for your app are ephemeral and have a TTL of 48 hours since the last commit in the corresponding branch. This means that after 48 hours of inactivity, the deployment will be automatically removed.

If you need to maintain the deployment for a longer duration or require a more permanent environment, you may need to discuss alternative deployment options with our DevOps team.