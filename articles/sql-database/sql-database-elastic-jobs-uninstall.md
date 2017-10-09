---
title: "Средство заданий эластичных баз данных toouninstall aaaHow"
description: "Как toouninstall hello средство заданий эластичных баз данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a>Удаление компонентов заданий обработки эластичных баз данных.
**Заданий эластичных баз данных** компоненты можно удалить с помощью портала hello или PowerShell.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Удаление компонентов заданий эластичных баз данных с помощью портала Azure hello
1. Откройте hello [портал Azure](https://portal.azure.com/).
2. Перейдите toohello подписку, содержащую **заданий эластичных баз данных** компоненты, а именно: hello подписки, в какие эластичной базы данных были установлены компоненты заданий.
3. Щелкните **Обзор** и **Группы ресурсов**.
4. Привет, выберите группу ресурсов с именем «__ElasticDatabaseJob».
5. Удалите группу ресурсов hello.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>Удаление компонентов заданий обработки эластичных баз данных с помощью PowerShell
1. Запустите командную строку Microsoft Azure PowerShell и перейдите toohello средства вложенный каталог в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x hello: тип **средства cd**.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools
2. Выполните сценарий PowerShell.\UninstallElasticDatabaseJobs.ps1 hello.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1

Или выполните hello следующий сценарий, при условии, что по умолчанию значения, когда используется для установки компонентов hello:

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a>Дальнейшие действия
заданий toore install эластичной базы данных, в разделе [Установка службы задания hello эластичной базы данных](sql-database-elastic-jobs-service-installation.md)

Общие сведения о заданиях обработки эластичных баз данных см. в статье [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md).

<!--Image references-->


