# Azure App Service

**Watch the video [here](https://youtu.be/T97a3DdIeKk)**

## Prerequisites

- Install [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- [Obtain a free Azure Account](https://azure.microsoft.com/en-us/free/)

## Loose Agenda

Set up a free Azure Web App instance hosting a Web API image built previously in the [GitHub Packages Exercise](github-packages.md).

## Step by Step

### Setup Playground

The output of the previous GitHub Packages exercise has been stored as a publicly accessible image at `ghcr.io/boredtweak/non-zero-packages:latest`. We'll be deploying that image to Azure on their free PaaS offering `App Service` for today's exercise.

### Create a Resource Group

Navigate to [portal.azure.com](https://portal.azure.com) and log in with your credentials.

Click the top search bar and enter `resource groups` and select the resulting `resource groups` item.

Click the `+ Create` button at the top left.

In the `Create a resource group` page enter a name such as `rg-non-zero-webapi`.

Select a region near to yourself then select `Create`.

### Create a Web App

In the Resource group browse screen select your new resource group.

In the popout screen for your resource group click the `+ Create` button.

Search `Web App` and select the resulting option labeled `Web App` then click `Create`.

Select your Resource Group created in the previous step.

Enter a name for your web app such as `app-non-zero-webapi`.

For `Publish` select `Docker Container`.

For Operating System select `Linux`.

Select a region near you.

Under App Service Plan, click `Create new` and give it a name such as `sp-non-zero-webapi`.

**IMPORTANT**
Click `Change size`

On the `Spec Picker` screen click `Dev/Test` and select `F1` for a Free pricing tier. Click `Apply`.

Click `Next`. You should now be on the `Docker` tab of the `Create Web App` experience.

We will select `Single Container` for Options and `Private Registry` for the Image Source.

For Server URL enter `https://`

Leave Username and Password blank.

For `Image and Tag` enter `ghcr.io/boredtweak/non-zero-packages:latest` or your own username, image, and tag combination if using your own GitHub Package.

Click `Review + create` then click `Create` on the subsequent page. The portal will inform you that deployment is in progress and updates automatically once the deployment is complete.

### Review the deployed resource

Once the deployment is complete you can click `Go to resource`. Otherwise you can find your resource group from the main page and find the App Service resource within it.

From your App Service resource window in the `Overview` tab select `Browse` from along the header.

This will open a new tab with your deployed resource. Adjust the URL by appending `/swagger`.

### Configuration

Open the Settings > Configuration tab within the App Service.

Click `+ New application setting` and enter the name `NON_ZERO_VALUE` and the value `day`. Click `OK` then click `Save` at the top.

Navigate back to the swagger page and call the `/WeatherForecast/configuration` endpoint. Observe that the App Setting is configured as an environment variable within our container image.

Congratulations on a non-zero day!

## Additional Resources

- [Azure App Service Documentation](https://docs.microsoft.com/en-us/azure/app-service/overview)
- [Azure Free Tier](https://azure.microsoft.com/free)
