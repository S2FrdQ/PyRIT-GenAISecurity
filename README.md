# Python Risk Identification Tool for generative AI (PyRIT)

The Python Risk Identification Tool for generative AI (PyRIT) is an open source
framework built to empower security professionals and engineers to proactively
identify risks in generative AI systems.

- Check out the [documentation](https://azure.github.io/PyRIT/) for more information
  about how to use, install, or contribute to PyRIT.
- Visit the PyRIT [Discord server](https://discord.gg/9fMpq3tc8u) to chat with the team and community.

## Table of Contents

- [Features](#features)
- [Azure account requirements](#azure-account-requirements)
  - [Cost estimation](#cost-estimation)
- [Getting Started](#getting-started)
  - [GitHub Codespaces](#github-codespaces)
  - [VS Code Dev Containers](#vs-code-dev-containers)
  - [Local environment](#local-environment)
- [Deploying](#deploying)
  - [Deploying again](#deploying-again)
- [Running the development server](#running-the-development-server)
- [Using the app](#using-the-app)
- [Clean up](#clean-up)
- [Guidance](#guidance)


## Getting Started

You have a few options for setting up this project.
The easiest way to get started is GitHub Codespaces, since it will setup all the tools for you,
but you can also [set it up locally](#local-environment) if desired.

### GitHub Codespaces

You can run this repo virtually by using GitHub Codespaces, which will open a web-based VS Code in your browser:

[![Open in GitHub Codespaces](https://img.shields.io/static/v1?style=for-the-badge&label=GitHub+Codespaces&message=Open&color=brightgreen&logo=github)](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=599293758&machine=standardLinux32gb&devcontainer_path=.devcontainer%2Fdevcontainer.json&location=WestUs2)

Once the codespace opens (this may take several minutes), open a terminal window.

### Install PyRIT Library

1. To install `conda`, run the following:
    ```shell
    azd init -t azure-search-openai-demo
    mkdir -p ~/miniconda3 
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh 
    bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3 
    rm ~/miniconda3/miniconda.sh 
    source ~/miniconda3/bin/activate
    conda init --all
    ```
    Close your terminal and re-open it.

2. Next, we will create a conda environment that uses Python 3.11 (recommended for PyRIT).
    ```shell
    conda create -n pyrit-test python=3.11
    ```
3. To use the environment, we need to activate it.
    ```shell
    conda activate pyrit-test
    ```
4. Next, we will install PyRIT. First, we need to install git if you do not already have it.
    ```shell
    sudo apt update && sudo apt install git
    ```
5.  Clone the PyRIT repo locally.
    ```shell
    git clone https://github.com/S2FrdQ/PyRIT-GenAISecurity
    cd PyRIT-GenAISecurity
    ```
6. Now, we will install PyRIT using pip (make sure you do not miss the period at the end).
    ```shell
    pip install .
    ```
    This will install all the packages needed for PyRIT and some other extremely useful tools that we will use in the next step. In particular, we will make use of JupyterLab.

## Deploying

The steps below will provision Azure resources and deploy the application code to Azure Container Apps. To deploy to Azure App Service instead, follow [the app service deployment guide](docs/azure_app_service.md).

1. Login to your Azure account:

    ```shell
    azd auth login
    ```

    For GitHub Codespaces users, if the previous command fails, try:

   ```shell
    azd auth login --use-device-code
    ```

1. Create a new azd environment:

    ```shell
    azd env new
    ```

    Enter a name that will be used for the resource group.
    This will create a new folder in the `.azure` folder, and set it as the active environment for any calls to `azd` going forward.
   1. (Optional) This is the point where you can customize the deployment by setting environment variables, in order to [use existing resources](docs/deploy_existing.md), [enable optional features (such as auth or vision)](docs/deploy_features.md), or [deploy low-cost options](docs/deploy_lowcost.md), or [deploy with the Azure free trial](docs/deploy_freetrial.md).
1. Run `azd up` - This will provision Azure resources and deploy this sample to those resources, including building the search index based on the files found in the `./data` folder.
    - **Important**: Beware that the resources created by this command will incur immediate costs, primarily from the AI Search resource. These resources may accrue costs even if you interrupt the command before it is fully executed. You can run `azd down` or delete the resources manually to avoid unnecessary spending.
    - You will be prompted to select two locations, one for the majority of resources and one for the OpenAI resource, which is currently a short list. That location list is based on the [OpenAI model availability table](https://learn.microsoft.com/azure/cognitive-services/openai/concepts/models#model-summary-table-and-region-availability) and may become outdated as availability changes.
1. After the application has been successfully deployed you will see a URL printed to the console.  Click that URL to interact with the application in your browser.
It will look like the following:

!['Output from running azd up'](docs/images/endpoint.png)

> NOTE: It may take 5-10 minutes after you see 'SUCCESS' for the application to be fully deployed. If you see a "Python Developer" welcome screen or an error page, then wait a bit and refresh the page.

### Deploying again

If you've only changed the backend/frontend code in the `app` folder, then you don't need to re-provision the Azure resources. You can just run:

```shell
azd deploy
```

If you've changed the infrastructure files (`infra` folder or `azure.yaml`), then you'll need to re-provision the Azure resources. You can do that by running:

```shell
azd up
```

## Running the development server

You can only run a development server locally **after** having successfully run the `azd up` command. If you haven't yet, follow the [deploying](#deploying) steps above.

1. Run `azd auth login` if you have not logged in recently.
2. Start the server:

  Windows:

  ```shell
  ./app/start.ps1
  ```

  Linux/Mac:

  ```shell
  ./app/start.sh
  ```

  VS Code: Run the "VS Code Task: Start App" task.

It's also possible to enable hotloading or the VS Code debugger.
See more tips in [the local development guide](docs/localdev.md).

## Using the app

- In Azure: navigate to the Azure WebApp deployed by azd. The URL is printed out when azd completes (as "Endpoint"), or you can find it in the Azure portal.
- Running locally: navigate to 127.0.0.1:50505

Once in the web app:

- Try different topics in chat or Q&A context. For chat, try follow up questions, clarifications, ask to simplify or elaborate on answer, etc.
- Explore citations and sources
- Click on "settings" to try different options, tweak prompts, etc.
