---
title: Set up a local development environment for Azure SQL Database
description: How to set up a local development environment for Azure SQL Database.
author: croblesm
ms.author: roblescarlos
ms.reviewer: mathoma
ms.date: 04/01/2024
ms.service: azure-sql-database
ms.topic: how-to
---

# Set up a local development environment for Azure SQL Database
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

This article teaches you to set up the [local development experience for Azure SQL Database](local-dev-experience-overview.md). The local development experience for Azure SQL Database enables developers and database professionals to design, edit, build/validate, publish, and run database schemas for databases in Azure SQL Database using a containerized environment.

> [!IMPORTANT]
> Set up a development environment with an [Azure SQL Database dev container template](local-dev-experience-dev-containers.md). To get started, [set up an Azure SQL Database local development environment with an dev container template](local-dev-experience-dev-containers-quickstart.md). Dev container templates are a superior alternative and replacement to the Azure SQL Database emulator for local development.

## Prerequisites

Before you configure the local development environment for Azure SQL Database, make sure you meet the following hardware and software requirements:

- Software requirements:
    - Currently supported on Windows 10 or later release, macOS Mojave or later release, and Linux (preferably Ubuntu 18.04 or later release)
    - [Azure Data Studio](/azure-data-studio/download-azure-data-studio) or [Visual Studio Code](https://code.visualstudio.com/Docs)
- Minimum hardware requirements:
    - 8-GB RAM
    - 10-GB available disk space

## Install Docker Desktop

The local development environment for Azure SQL Database uses the [Azure SQL Database emulator](local-dev-experience-sql-database-emulator.md), a containerized database with close fidelity to the Azure SQL Database public service. The Azure SQL Database emulator is implemented as a [Docker](https://www.docker.com/) container.

Install [Docker Desktop](https://www.docker.com/products/docker-desktop/). If you're using Windows, set up [Docker Desktop for Windows with WSL 2](/windows/wsl/tutorials/wsl-containers).

Ensure that Docker Desktop is running before using your local development environment for Azure SQL Database.

## Install extension

There are different extensions to install depending on your preferred development tool. 

| Extension | Visual Studio Code | Azure Data Studio |
|--|--|--|
| The [mssql extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) | Install the `mssql` extension. | Installation isn't necessary. The mssql extension as the functionality is natively available. |
| [SQL Database Projects extension (Preview)](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sql-database-projects-vscode) | Installation isn't necessary. The SQL Database Projects extension is bundled with the `mssql` extension, and is automatically installed and updated when the `mssql` extension is installed or updated. | Install the SQL Database Projects extension. |

# [Visual Studio Code](#tab/vscode)

If you're using [Visual Studio Code](https://code.visualstudio.com/Docs), install the [mssql extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).

The `mssql` extension enables you to connect and run queries and test scripts against a database. The database can run in the Azure SQL Database emulator locally, or in the global Azure SQL Database service.

To install the extension:

1. In Visual Studio Code, select **View** > **Command Palette**, or press **Ctrl**+**Shift**+**P**, or press **F1** to open the **Command Palette**.

1. In the **Command Palette**, select **Extensions: Install Extensions** from the dropdown.

1. In the **Extensions** pane, type `mssql`.

1. Select the **SQL Server (mssql)** extension, and then select **Install**.

1. After the installation completes, select **Reload** to enable the extension.

1. There's no need to run the docker container with a SQL image manually, it is deployed and run when you [Build and Publish a Project](/azure-data-studio/extensions/sql-database-project-extension-build#publish-a-database-project).

# [Azure Data Studio](#tab/ads)

If you're using [Azure Data Studio](/azure-data-studio/download-azure-data-studio), install the [SQL Database Projects extension (Preview)](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sql-database-projects-vscode). The SQL Database Projects extension enables you to capture an existing database schema and/or design new database objects using a declarative database design model. You can commit a database schema to version control. You can also publish a database schema to a database running in the Azure SQL Database emulator, or to a database running in the global Azure SQL Database service. You can publish an entire database, or incremental changes to a database.

To install the SQL Database Projects extension:

1. In Azure Data Studio, select **View** > **Command Palette**, or press **Ctrl**+**Shift**+**P**, or press **F1** to open the **Command Palette**.

1. In the **Command Palette**, select **Extensions: Install Extensions** from the dropdown.

1. In the **Extensions** pane, type **SQL Database Projects**.

1. Select the **SQL Database Projects** extension, and then select **Install**.

1. After the installation completes, select **Reload** to enable the extension.

1. There's no need to run the docker container with a SQL image manually, as it gets deployed and run in the subsequent step: [Build and Publish a Project](/azure-data-studio/extensions/sql-database-project-extension-build#publish-a-database-project).

---

## Begin using your local development environment

You have now set up your local development environment for Azure SQL Database.

## Next step

> [!div class="nextstepaction"]
> [Create a database project for a local Azure SQL Database development environment](local-dev-experience-create-database-project.md)

## Related content

Learn more about the local development experience for Azure SQL Database:

- [What is the local development experience for Azure SQL Database?](local-dev-experience-overview.md)
- [Create a database project for a local Azure SQL Database development environment](local-dev-experience-create-database-project.md)
- [Publish a database project for Azure SQL Database to the local emulator](local-dev-experience-publish-emulator.md)
- [Quickstart: Create a local development environment for Azure SQL Database](local-dev-experience-quickstart.md)
- [Introducing the Azure SQL Database emulator](local-dev-experience-sql-database-emulator.md)
