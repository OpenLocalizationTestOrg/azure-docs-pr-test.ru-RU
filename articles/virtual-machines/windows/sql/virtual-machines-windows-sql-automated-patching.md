---
title: "aaaAutomated исправления для виртуальных машин SQL Server (диспетчер ресурсов) | Документы Microsoft"
description: "Описывается функция автоматического исправления hello для SQL Server виртуальных машин, работающих в Azure с помощью диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](virtual-machines-windows-sql-automated-patching.md)
> * [Классический](../classic/sql-automated-patching.md)
> 
> 

При автоматической установке исправлений на виртуальных машинах Azure с SQL Server задается период обслуживания. Установка автоматических обновлений возможна только в этот период обслуживания. Для SQL Server это rescriction гарантирует, что системные обновления и перезапуски, связанный в hello наиболее сроки для hello базы данных. Автоматические исправления выполняются зависит от hello [расширения агента SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview hello классической версии данной статьи, в разделе [автоматическое применение исправлений для SQL Server в виртуальных машин Azure Classic](../classic/sql-automated-patching.md).

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

* [Установка последних команд Azure PowerShell hello](/powershell/azure/overview) при планировании tooconfigure автоматических исправлений с помощью PowerShell.

> [!NOTE]
> Автоматические исправления выполняются полагается на hello расширения агента IaaS SQL Server. В текущей коллекции образов виртуальных машин SQL это расширение присутствует по умолчанию. Дополнительные сведения см. в статье [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) (Расширение агента SQL Server IaaS).
> 
> 

## <a name="settings"></a>данных
Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического исправления. Hello фактические шаги настройки отличаются в зависимости от того, используются ли hello портал Azure или команд Windows PowerShell для Azure.

| Настройка | Возможные значения | Description (Описание) |
| --- | --- | --- |
| **Автоматическое исправление** |Включено/отключено (отключено) |Включает или отключает автоматическую установку исправлений для виртуальной машины Azure. |
| **Расписание обслуживания** |Каждый день, понедельник, вторник, среда, четверг, пятница, суббота, воскресенье |расписание Hello загрузку и установку обновлений Windows, SQL Server и Microsoft для виртуальной машины. |
| **Время начала обслуживания** |0–24 |Hello локальном запуске время tooupdate hello виртуальной машины. |
| **Длительность периода обслуживания** |30–180 |Hello количество минут, разрешенных toocomplete hello загрузки и установки обновлений. |
| **Категория исправления** |Важно! |Категория Hello toodownload обновлений и установить. |

## <a name="configuration-in-hello-portal"></a>Конфигурация в hello портала
Можно использовать hello Azure портала tooconfigure автоматических исправлений во время инициализации или для существующих виртуальных машин.

### <a name="new-vms"></a>Новые виртуальные машины
Используйте hello Azure портала tooconfigure автоматических исправлений при создании новой виртуальной машины SQL Server в модели развертывания диспетчера ресурсов hello.

В hello **параметры SQL Server** колонке выберите **автоматическую установку исправлений**. Hello следующие Azure портала снимке экрана показано hello **автоматических исправлений SQL** колонку.

![Автоматизированная установка исправлений SQL на портале Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

Контекст, в разделе hello полный на [подготовку виртуальной машины SQL Server в Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Существующие виртуальные машины
Выберите существующую виртуальную машину SQL Server. Затем выберите hello **конфигурации SQL Server** раздел hello **параметры** колонку.

![Автоматизированная установка исправлений SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

В hello **конфигурации SQL Server** колонка, щелкните hello **изменить** кнопку в hello автоматического исправления раздела.

![Настройка автоматизированной установки исправлений SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

По завершении нажмите кнопку hello **ОК** кнопку внизу hello hello **конфигурации SQL Server** toosave колонке изменения.

При включении автоматического исправления для hello первый раз, Azure настраивает hello агента SQL Server IaaS в фоновом режиме hello. В течение этого времени hello портал Azure может показывать, что выполняется настройка автоматического исправления. Подождите несколько минут для hello агента toobe установлены, настроены. После этого hello Azure portal отражает hello новые параметры.

> [!NOTE]
> Можно также настроить автоматизированную установку исправлений с помощью шаблона. Чтобы получить дополнительные сведения, ознакомьтесь с [шаблоном быстрого запуска Azure для автоматизированной установки исправлений](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).
> 
> 

## <a name="configuration-with-powershell"></a>Настройка с помощью PowerShell
После подготовки виртуальной Машины SQL, используйте PowerShell tooconfigure автоматических исправлений.

В следующем примере hello, PowerShell — используется tooconfigure автоматического исправления на существующей виртуальной Машины SQL Server. Hello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** команда настраивает новый период обслуживания для автоматических обновлений.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

На основании этого примера hello следующей таблице описаны результаты применения hello на hello целевой виртуальной Машине Azure.

| Параметр | Результат |
| --- | --- |
| **DayOfWeek** |Исправления устанавливаются каждый четверг. |
| **MaintenanceWindowStartingHour** |Установка обновлений начинается в 11:00. |
| **MaintenanceWindowsDuration** |Обновления должны быть установлены в течение 120 минут. На основании времени начала hello, они должны выполнить с 1:00 pm. |
| **PatchCategory** |Здравствуйте, единственное возможное значение для этого параметра можно **важно**. |

Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.

toodisable автоматического исправления выполнения hello же сценарий, не hello **-включить** toohello параметр **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**. Здравствуйте, отсутствие hello **-включить** функции hello toodisable команда hello параметров сигналы.

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).

