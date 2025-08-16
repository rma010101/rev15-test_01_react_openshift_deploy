
# React OpenShift Deployment Example

This project demonstrates how to build and deploy a simple React app (using Vite) to OpenShift Sandbox using a custom Dockerfile.

## Features
- Simple React app displaying a message
- Vite for fast development and production builds
- Dockerfile for containerization
- Ready for OpenShift deployment

## Project Structure

- `src/` - React source code
- `public/` - Static assets
- `dist/` - Production build output (created by `npm run build`)
- `Dockerfile` - Container build instructions

## Local Development

1. Install dependencies:
	```sh
	npm install
	```
2. Start the development server:
	```sh
	npm run dev
	```
3. Build for production:
	```sh
	npm run build
	```

## Dockerfile Overview

The Dockerfile builds the React app and serves it using the `serve` package on port 8080 (required by OpenShift):

```
FROM node:20
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
RUN npm install -g serve
EXPOSE 8080
CMD ["serve", "-s", "dist", "-p", "8080"]
```


## Deploying to OpenShift Sandbox

Follow these detailed steps to deploy your React app to OpenShift Sandbox:

1. **Start the Import Wizard**
	- In OpenShift Sandbox, click **“+Add”** in your project.
	- Select **“Import from Git”**.
	- *Snapshot: You’ll see a form asking for your Git repository URL.*

2. **Enter Your GitHub Repo**
	- Paste your repo URL (e.g., `https://github.com/rma010101/rev15-test_01_react_openshift_deploy`).
	- Wait for validation (green checkmark).
	- *Snapshot: A validated URL with a green checkmark, and options for context directory and source secret.*

3. **Set Context Directory**
	- Set **Context dir** to `/` (root of your repo).
	- *Snapshot: A text box labeled “Context dir” with `/` entered.*

4. **Select Build Strategy**
	- Choose **Dockerfile** or **Containerfile** as the build strategy.
	- If prompted, confirm the Dockerfile location (usually at the root).
	- *Snapshot: A section with build strategy options, select “Dockerfile”.*

5. **Configure Application Name and Project**
	- Enter an application name (e.g., `rev15-test-01-react-openshift-deploy`).
	- Select your project/namespace (e.g., `rma010101-dev`).
	- *Snapshot: Fields for application name and project selection.*

6. **Review and Create**
	- Review the summary of your settings.
	- Click **“Create”** or **“Start Build”**.
	- *Snapshot: A summary page with a “Create” or “Start Build” button.*

7. **Monitor Build and Deployment**
	- Watch the build logs for progress.
	- Once complete, OpenShift will create a service and route.
	- *Snapshot: A build log window showing build steps and status.*

8. **Access Your App**
	- After deployment, find the **Route** URL in the application details.
	- Click the link to open your app in the browser.
	- *Snapshot: A route URL (e.g., `https://rev15-test-01-react-openshift-deploy-<namespace>.apps.<cluster>.openshift.com`).*

You can take screenshots during your deployment and add them to this section for visual reference.

## Troubleshooting

- If you hit quota errors, delete unused deployments or apps in your namespace.
- Check build and pod logs for errors if the app does not start.

## License

MIT
