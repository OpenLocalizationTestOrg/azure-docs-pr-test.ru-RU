---
title: "aaaAutomated исправления для виртуальных машин SQL Server (классические) | Документы Microsoft"
description: "Описывается функция автоматического исправления hello для SQL Server виртуальных машин, работающих в Azure с помощью режима hello классического развертывания."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (классическая модель)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Классический](../classic/sql-automated-patching.md)
> 
> 

При автоматической установке исправлений на виртуальных машинах Azure с SQL Server задается период обслуживания. Установка автоматических обновлений возможна только в этот период обслуживания. Для SQL Server это гарантирует, что системные обновления и перезапуски, связанный в hello наиболее сроки для hello базы данных. Автоматические исправления выполняются зависит от hello [расширения агента SQL Server IaaS](../classic/sql-server-agent-extension.md).

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. tooview hello диспетчера ресурсов версию этой статьи в разделе [автоматическое применение исправлений для SQL Server в диспетчере ресурсов Azure виртуальные машины](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a>Предварительные требования
toouse автоматическое применение исправлений, рассмотрите возможность hello следующие предварительные требования:

**Операционная система**

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Версия SQL Server**

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**

* [Установка последних команд Azure PowerShell hello](/powershell/azure/overview).

**Расширение IaaS для SQL Server**

* [Установка расширения SQL Server IaaS hello](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>данных
Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического исправления. Для классических виртуальных машин необходимо использовать PowerShell tooconfigure эти параметры.

| Настройка | Возможные значения | Description (Описание) |
| --- | --- | --- |
| **Автоматическое исправление** |Включено/отключено (отключено) |Включает или отключает автоматическую установку исправлений для виртуальной машины Azure. |
| **Расписание обслуживания** |Каждый день, понедельник, вторник, среда, четверг, пятница, суббота, воскресенье |расписание Hello загрузку и установку обновлений Windows, SQL Server и Microsoft для виртуальной машины. |
| **Время начала обслуживания** |0–24 |Hello локальном запуске время tooupdate hello виртуальной машины. |
| **Длительность периода обслуживания** |30–180 |Hello количество минут, разрешенных toocomplete hello загрузки и установки обновлений. |
| **Категория исправления** |Важно! |Категория Hello toodownload обновлений и установить. |

## <a name="configuration-with-powershell"></a>Настройка с помощью PowerShell
В следующем примере hello, PowerShell — используется tooconfigure автоматического исправления на существующей виртуальной Машины SQL Server. Hello **New-AzureVMSqlServerAutoPatchingConfig** команда настраивает новый период обслуживания для автоматических обновлений.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

На основании этого примера hello следующей таблице описаны результаты применения hello на hello целевой виртуальной Машине Azure.

| Параметр | Результат |
| --- | --- |
| **DayOfWeek** |Исправления устанавливаются каждый четверг. |
| **MaintenanceWindowStartingHour** |Установка обновлений начинается в 11:00. |
| **MaintenanceWindowsDuration** |Обновления должны быть установлены в течение 120 минут. На основании времени начала hello, они должны выполнить с 1:00 pm. |
| **PatchCategory** |Hello только возможных для этого параметра задается значение «Важно!». |

Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.

toodisable автоматического исправления выполнения hello же сценарий, не hello - toohello включить параметр New-AzureVMSqlServerAutoPatchingConfig. Как и установки, может занять несколько минут toodisable автоматических исправлений.

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](../classic/sql-server-agent-extension.md).

Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

