# SWA-TS-POC

This is a Proof-Of-Concept of a Static Web App coded in TypeScript

An extremely easy way to deploy a static website and optional api to Azure.

## How to set everything up from a clean slate

**Prerequisites**:
- Azure subscription
- VSCode
- Azure Static Web Apps VSCode Extension
- GitHub account
- npm

**Steps to create app:**

1. Create a new create-react-app from template `npx create-react-app my-app --template typescript`
2. Open app in VSCode `code my-app`
3. Create repository in GitHub (e.g. my-app)
4. Initialize git repository `git init`
5. Make first commit `git commit -m "first commit"`
6. Create main branch (in case it is not the default for you) `git branch -M main`
7. Set remote origin `git remote add origin git@github.com:username/my-app.git`
8. Push changes `git push -u origin main`
9. Select _Static Web Apps_ extension and press the **+** sign
    1. You will be asked to login to Azure
    2. Select subscription
    3. Select name for static web app (my-app)
    4. Set app folder name. Use default `/`
    5. Set api folder name. Use default `/api`
    6. Login to GitHub when prompted
10. The extension has now setup your static web app in Azure and created the required GitHub Workflows for deploying the code there (can be found under `./github/workflows` in your app folder).
11. The workflow has been automatically committed and run in GitHub, so your app should be accessible in the cloud within a minute or two.
12. Select your static web app from the extension, right click it, and select `Browse`. You are now able to navigate to your web app in Azure.

>**So far, we yet don't have an api!**

**Setting up the API**

1. Install Azure Functions VSCode extension
2. Select _Create new project..._ from the Azure Functions extension
3. Choose `api` as folder for the project
4. Choose TypeScript as language
5. Setup a function using HttpTrigger
6. Choose function name
7. Set Anonymous authorization (at least for now)
8. Finally, go to the folder and run `npm install` and then `npm run build`
9. Ready!

The GitHub Action will automatically deploy the function under the Static Web App when you commit and push your changes to the repository.

## Running in local environment

Since the React part of the app was made using Create React App, you can run it locally by simply using `npm start`. However, if we were to have an api as well and would like to start both the api and the frontend code locally, we could use the [Static Web App CLI tool](https://github.com/Azure/static-web-apps-cli). Follow the installation and execution guides from the website.

The other option would be to run the api using azure functions core tools (which is in fact used here as well, but in the background), but you would have to start both parts separately.

### TL;DR

Due to `swa` only running `func start` in the api folder right away, we first need to run

```sh
cd api
npm run build
```

in order to build the api code. If your api is in plain javascript, this is not required.

After that we can use the command:

`swa start http://localhost:3000 --run "npm start" --api-location api`

to startup both front- end backend in http://localhost:4280

#### Taking things further

To not having to remember all the parameters in the start command we have created a file called `swa-cli.config.json`, which contains hints for the swa cli. The run command, api folder and frontend proxy are all configured there under the name `app`, so now we can achieve the same as above by simply running `swa start app`.

However, building of the api code is still required, since the swa cli runs `func start` in the folder instead of using any configurable commands. I will be posting this is an issue to the cli repository...
## Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
