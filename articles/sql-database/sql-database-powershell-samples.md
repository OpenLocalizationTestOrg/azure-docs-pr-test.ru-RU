---
title: "Примеры сценариев PowerShell aaaAzure для базы данных SQL | Документы Microsoft"
description: "Azure PowerShell скрипт примеры toohelp создавать и управлять серверами базы данных SQL Azure, эластичные пулы, баз данных и брандмауэры."
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: overview-samples
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1130ffb0e1c2b94c676d564ad5c4eb3b86374dbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a>Примеры Azure PowerShell для базы данных SQL Azure

Hello Следующая таблица содержит ссылки toosample Azure скрипты PowerShell для базы данных SQL Azure.

| |  |
|---|---|
|**Создание отдельной базы данных и эластичного пула**||
| [Создание отдельной базы данных и настройка правила брандмауэра](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Этот скрипт PowerShell создает отдельную базу данных SQL Azure и настраивает правило брандмауэра на уровне сервера. |
| [Создание эластичных пулов и перемещение баз данных в составе пулов](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Этот скрипт PowerShell создает эластичные пулы базы данных SQL Azure и перемещает базы данных в составе пулов, а также изменяет уровни производительности.|
|**Настройка георепликации и отработка отказа**||
| [Настройка активной георепликации для отдельной базы данных SQL Azure с помощью PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот сценарий PowerShell настраивает активную георепликацию для одной базы данных Azure SQL и отказа toohello вторичной реплики. |
| [Настройка активной георепликации для базы данных SQL Azure в составе пула с помощью PowerShell](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот сценарий PowerShell настраивает активной георепликации для базы данных Azure SQL в пуле эластичных БД SQL и отказа toohello вторичной реплики. |
| [Use PowerShell to configure an active geo-replication failover group for a single Azure SQL database](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) (Использование PowerShell для настройки группы отработки отказа активной георепликации для отдельной базы данных SQL Azure (предварительная версия)) | Этот сценарий PowerShell настраивает отработки отказа группой для экземпляра сервера базы данных SQL Azure добавляет группу базы данных toohello перехода на другой ресурс и переключается toohello сервера-получателя |
|**Масштабирование отдельных баз данных и эластичного пула**||
| [Масштабирование отдельной базы данных](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Этот сценарий PowerShell отслеживает hello метрики производительности базы данных Azure SQL, выполняет масштабирование tooa высокий уровень производительности и создает правило генерации оповещений на одном hello метрики производительности. |
| [Масштабирование эластичного пула](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Этот сценарий PowerShell отслеживает hello показателей производительности пула эластичной базы данных SQL Azure, выполняет масштабирование tooa высокий уровень производительности и создает правило генерации оповещений на одном hello метрики производительности.  |
| **Аудит и обнаружение угроз** |
| [Настройка аудита и обнаружения угроз](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот скрипт PowerShell настраивает политики аудита и обнаружения угроз для базы данных SQL Azure. |
| **Восстановление, копирование и импорт базы данных**||
| [Восстановление базы данных](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот сценарий PowerShell восстанавливает базу данных Azure SQL из геоизбыточной резервной копии и восстановление удаленных Azure SQL toohello последней резервной копии базы данных. |
| [Скопируйте toonew сервера базы данных](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот скрипт PowerShell создает копию существующей базы данных SQL Azure на новом сервере SQL Azure. |
| [Импорт базы данных из BACPAC-файла](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Этот сценарий PowerShell импортирует сервер Azure SQL tooan базы данных из bacpac-файл. |
| **Синхронизация данных между базами данных**||
| [Синхронизация данных между базами данных SQL](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Этот сценарий PowerShell настраивает toosync синхронизации данных между несколькими базами данных Azure SQL. |
| [Синхронизация данных между базой данных SQL и локальной базой данных SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Этот сценарий PowerShell настраивает toosync синхронизации данных между базой данных Azure SQL и локальной базы данных SQL Server. |
|||
|||
