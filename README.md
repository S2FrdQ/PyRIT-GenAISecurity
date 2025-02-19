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

2. Next, we will create a conda environment that uses Python 3.11 (recommended).
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

## Populate Azure OpenAI variables on `.env`

Nearly all of PyRIT’s targets require secrets to interact with. PyRIT primarily uses these by putting them in a local `.env` file. In this lab, we are dealing with Azure OpenAI, you need to have an Azure account and a subscription. Populate the `.env` file in your repo with the correct Azure OpenAI Keys, deployment names, and endpoints.
For Azure OpenAI, you can find these in `Azure Portal > Azure AI Services > Azure OpenAI > Your OpenAI Resource > Resource Management > Keys and Endpoint`

1. Login to your Azure account:


### Authenticate on Azure with Azure Subscription

Since we are using a Azure OpenAI target(which interacts using AAD auth), you must authenticate to your Azure subscription. Depending on your operating system, download the appropriate Azure CLI tool from the links provided below:

- Windows OS: [Download link](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli)
- Linux: [Download link](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)
- Mac OS: [Download link](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-macos)

After downloading and installing the Azure CLI, open your terminal and run the following command to log in:
```shell
az login
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
