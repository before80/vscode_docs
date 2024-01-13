+++
title = "Deploy Python Apps"
date = 2024-01-12T22:36:24+08:00
weight = 120
type = "docs"
description = ""
isCJKLanguage = true
draft = false
+++

> 原文: [https://code.visualstudio.com/docs/python/python-on-azure](https://code.visualstudio.com/docs/python/python-on-azure)

# Deploy Python Web Apps 部署 Python Web 应用



The [Azure Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) extensions for Visual Studio Code make it easy to deploy Python applications (including containers) to [Azure App Service](https://azure.microsoft.com/services/app-service) and to deploy serverless code to [Azure Functions](https://azure.microsoft.com/services/functions).

&zeroWidthSpace;Visual Studio Code 的 Azure 工具扩展可轻松将 Python 应用程序（包括容器）部署到 Azure 应用服务，并将无服务器代码部署到 Azure Functions。

![Azure Tools extension](./DeployPythonApps_img/azure-tools.png)

## [Deployment tutorials 部署教程](https://code.visualstudio.com/docs/python/python-on-azure#_deployment-tutorials)

The following tutorials on the [Python Azure Developer's Center](https://learn.microsoft.com/azure/developer/python) walk you though the details.

&zeroWidthSpace;Python Azure 开发者中心上的以下教程将引导您了解详细信息。

| Tutorial 教程                                                | Description 说明                                             | Related Tools 相关工具                                       |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Deploy Python web app to Azure App Service 将 Python Web 应用部署到 Azure 应用服务](https://learn.microsoft.com/azure/app-service/quickstart-python) | Deploy a simple web app 部署简单的 Web 应用                  | [Django](https://www.djangoproject.com/) [Flask](https://flask.palletsprojects.com/) [Azure CLI](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azurecli) [Azure App Service Azure 应用服务](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice) [Azure Tools Azure 工具](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) |
| [Deploy Python web app with database to Azure App Service 将带有数据库的 Python Web 应用部署到 Azure 应用服务](https://learn.microsoft.com/azure/app-service/tutorial-python-postgresql-app) | Deploy a web app with PostgreSQL database 部署带有 PostgreSQL 数据库的 Web 应用 | [Django](https://www.djangoproject.com/) [Flask](https://flask.palletsprojects.com/) [PostgreSQL](https://www.postgresql.org/download/) [Azure App Service Azure 应用服务](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice) [Azure Tools Azure 工具](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) |
| [Deploy Python containers to Azure App Service 将 Python 容器部署到 Azure 应用服务](https://learn.microsoft.com/azure/developer/python/tutorial-deploy-containers-01) | Deploy a Docker container 部署 Docker 容器                   | [Docker 部署网站Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) [Azure App Service Azure 应用服务](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice) [Azure Tools Azure 工具](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) |
| [Deploy Python to Azure Functions 将 Python 部署到 Azure Functions](https://learn.microsoft.com/azure/azure-functions/create-first-function-vs-code-python) | Deploy serverless code with Azure Functions 使用 Azure Functions 部署无服务器代码 | [Azure Functions Core Tools](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local#install-the-azure-functions-core-tools) [Azure Functions Azure 数据库](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) [Azure Tools Azure 工具](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) |
