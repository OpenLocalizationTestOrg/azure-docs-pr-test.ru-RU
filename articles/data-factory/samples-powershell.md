---
title: "Примеры Azure PowerShell для фабрики данных Azure | Документация Майкрософт"
description: "Примеры Azure PowerShell — это скрипты для создания фабрик данных и управления ими."
services: data-factory
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: spelluru
ms.openlocfilehash: 9e361f42b25a1b3a97eacfb1ec1bc82900881806
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
---
# <a name="azure-powershell-samples-for-azure-data-factory"></a>Примеры Azure PowerShell для фабрики данных Azure

В следующей таблице содержатся ссылки на примеры скриптов Azure PowerShell для фабрики данных Azure.

> [!NOTE]
> Эта статья относится к версии 2 фабрики данных, которая в настоящее время доступна в предварительной версии. Если вы используете общедоступную версию 1 службы фабрики данных, прочитайте раздел [Фабрика данных Azure — примеры](v1/data-factory-samples.md).

| |  |
|---|---|
|**Копирование данных**||
|[Копирование больших двоичных объектов из одной папки в другую в хранилище BLOB-объектов Azure](scripts/copy-azure-blob-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Скрипт PowerShell копирует большие двоичные объекты из папки в хранилище BLOB-объектов Azure в другую папку в том же хранилище. |
|[Копирование данных из локальной среды SQL Server в хранилище BLOB-объектов Azure](scripts/hybrid-copy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот сценарий PowerShell копирует данные из локальной базы данных SQL Server в хранилище BLOB-объектов Azure. |
|[Массовое копирование](scripts/bulk-copy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| С помощью этого примера сценария PowerShell можно копировать данные из нескольких таблиц в базе данных SQL Azure в хранилище данных SQL Azure. |
|[Добавочное копирование](scripts/incremental-copy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот пример сценария PowerShell загружает в приемник только новые или обновленные записи из исходного хранилища данных после первоначального полного копирования данных из источника в приемник. |
|**Преобразование данных**||
|[Преобразование данных с помощью кластера Spark](scripts/transform-data-spark-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот скрипт PowerShell преобразовывает данные путем запуска программы на кластере Spark. |
|**Перенос пакетов SSIS в Azure**||
|[Создание среды выполнения интеграции Azure SSIS в фабрике данных Azure](scripts/deploy-azure-ssis-integration-runtime-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот сценарий PowerShell подготавливает к работе среду выполнения интеграции Azure и SSIS, которая запускает пакеты служб SQL Server Integration Services (SSIS) в Azure. |



