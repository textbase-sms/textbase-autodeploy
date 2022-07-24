# Textbase Autodeploy
###### Brought to you by Textbase Open Source Software
---
Textbase uses autodeploy scripts in our repositories to assist in the deployment of our software and services to production and preview. This means we get more time back in developing and don't have to take time deploying the software to production and preview.

We're sharing these scripts with you to allow you to streamline your production and preview pipeline quicker and faster.

### Requirements

- Sufficient GitHub Actions minutes
-- If you're doing **bulk** deployments, we recommend you upgrade your GitHub organisation to an enterprise subscripton to give you more than sufficient minutes for this pipeline
- Access to a code editor
-- Any does fine as long as they support Yet Another Markup Language (YAML), we recommend [Visual Studio Code](https://code.visualstudio.com/) or [Atom](https://atom.io/).
- A GitHub Org and GitHub repository

### Contributing to this Repository

We're open to all contributions to this repository. Please fork it and create a pull request informing us of **all** your changes and then please tag @callumisdumb in the pull request. Nobody else on the team maintains this repository.

---

### How-to

We've included examples of auto-deployment files [in the repository](https://github.com/textbase-sms/textbase-autodeploy/examples) however you'll need to follow these steps to customise it.

##### File placement
Place the YAML files you will be using in **.github/workflows** in your repository.

##### Deployment Scripts

| type | description
| ---- | ---- |
| Password Authentication | authenticates via password

*Find the example file [here](https://github.com/textbase-sms/textbase-autodeploy/blob/main/examples/deploy-password.yml)*

##### Step 1 - copying file to repository

Copy the file within the examples folder into your repository. To ensure spacing is correct and you dont get any errors, click "raw" on the file on the top right of the toolbar in GitHub.

After doing this, go to your repository, create a new file in `.github/workflows` and name it `deploy.yml` and save the file. Your workflow will error until you follow the following steps.

##### Step 2 - setting secret variables

If you use this method, you'll need to set the variables for your servers IP, password and username as a secret to ensure it isn't seen by other people and your server doesn't get breached and overtaken by bad actors. **This is especially important for OSS repositories**.

1. Head into the 'Settings' tab in your repository
![settings tab](https://cdn.upload.systems/uploads/w8dqJ770.png)

2. After your in here, click on the "secrets" dropdown under security in your navigation bar on the left side and then click "Actions". This will bring you into the secrets tab for actions.
![actions secrets tab](https://cdn.upload.systems/uploads/NlgZkFoZ.png)
Your page should look something like the above image.
3. Click on  `New Repository Secret` on the right hand side of the 'Actions secrets' headline. You will be presented with a page like this
![actions secrets](https://cdn.upload.systems/uploads/2ZNLfNnl.png)
4. In "Name" enter `SSH_HOST` and then enter the origin IP of your server. Do not enter a floating IP as it may not work.
5. Repeat step 3 and 4 above for both `SSH_PASSWORD` (being the password to access your server) and `SSH_USERNAME` (being the username you are using to access your server, typically `root`).

Your Actions secrets page should look something like this after you have completed those steps
![actions secrets page](https://cdn.upload.systems/uploads/l5XB8O16.png)

##### Step 3 - customising the deployment script

Customising the deployment script is, possibly, the hardest thing to do as the smallest error could break the entire thing. We recommend you **test the commands you do remotely on your script** on your server before doing them in the script.

1. Head into the YML file you copied over at the start in your repository and head down to `script: |` in the file. This is where we'll customise the script that executes on your server.

You can see we've set a base for the script, making `apt update` and `apt upgrade` run automatically, then echoing "Done". We recommend you **keep these** as it means you will not have to constantly upgrade your server, with the server upgrading itself every deployment.

You can delete `echo "Done!"` if you wish.

![script](https://cdn.upload.systems/uploads/ZpRwYwzq.png)

2. At this point, you can edit the script that runs on your server. **It is imperative** you keep the indentation on this, otherwise it will **not work** and will error.

3. After creating your script, save the file and deploy to GitHub.

##### Step 4 - watching it run!

After you have save your script, your deployment workflow will automatically run on GitHub if setup correctly as GitHub has detected a push to the repository.

If you're using a staging branch on your repository, you'll have to add this to the `branches` section of the YML file. You can do this here:

![staging branch eg](https://cdn.upload.systems/uploads/6KAQsIQn.png)

---

| type | description
| ---- | ---- |
| id_rsa.pub Authentication | authenticates via key

*Find the example file [here](https://github.com/textbase-sms/textbase-autodeploy/blob/main/examples/deploy-key.yml)*

##### Step 1 - copying file to repository

Copy the file within the examples folder into your repository. To ensure spacing is correct and you dont get any errors, click "raw" on the file on the top right of the toolbar in GitHub.

After doing this, go to your repository, create a new file in `.github/workflows` and name it `deploy.yml` and save the file. Your workflow will error until you follow the following steps.

##### Step 2 - setting secret variables

If you use this method, you'll need to set the variables for your servers IP, password and username as a secret to ensure it isn't seen by other people and your server doesn't get breached and overtaken by bad actors. **This is especially important for OSS repositories**.

1. Head into the 'Settings' tab in your repository
![settings tab](https://cdn.upload.systems/uploads/w8dqJ770.png)

2. After your in here, click on the "secrets" dropdown under security in your navigation bar on the left side and then click "Actions". This will bring you into the secrets tab for actions.
![actions secrets tab](https://cdn.upload.systems/uploads/NlgZkFoZ.png)
Your page should look something like the above image.
3. Click on  `New Repository Secret` on the right hand side of the 'Actions secrets' headline. You will be presented with a page like this
![actions secrets](https://cdn.upload.systems/uploads/2ZNLfNnl.png)
4. In "Name" enter `SSH_HOST` and then enter the origin IP of your server. Do not enter a floating IP as it may not work.
5. Repeat step 3 and 4 above for both `SSH_KEY` (being the key to access your server - ensure this is the `.ssh/id_rsa` key or `.pem` key in full) and `SSH_USERNAME` (being the username you are using to access your server, typically `root`).

Your Actions secrets page should look something like this after you have completed those steps
![actions secrets page](https://cdn.upload.systems/uploads/obwvEK3U.png)

##### Step 3 - customising the deployment script

Customising the deployment script is, possibly, the hardest thing to do as the smallest error could break the entire thing. We recommend you **test the commands you do remotely on your script** on your server before doing them in the script.

1. Head into the YML file you copied over at the start in your repository and head down to `script: |` in the file. This is where we'll customise the script that executes on your server.

You can see we've set a base for the script, making `apt update` and `apt upgrade` run automatically, then echoing "Done". We recommend you **keep these** as it means you will not have to constantly upgrade your server, with the server upgrading itself every deployment.

You can delete `echo "Done!"` if you wish.

![script](https://cdn.upload.systems/uploads/ZpRwYwzq.png)

2. At this point, you can edit the script that runs on your server. **It is imperative** you keep the indentation on this, otherwise it will **not work** and will error.

3. After creating your script, save the file and deploy to GitHub.

##### Step 4 - watching it run!

After you have save your script, your deployment workflow will automatically run on GitHub if setup correctly as GitHub has detected a push to the repository.

If you're using a staging branch on your repository, you'll have to add this to the `branches` section of the YML file. You can do this here:

![staging branch eg](https://cdn.upload.systems/uploads/6KAQsIQn.png)