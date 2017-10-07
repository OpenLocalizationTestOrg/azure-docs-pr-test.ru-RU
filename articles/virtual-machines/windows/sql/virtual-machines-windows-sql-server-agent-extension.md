---
title: "задачи управления aaaAutomate на виртуальных машинах SQL (диспетчера ресурсов) | Документы Microsoft"
description: "В этом разделе описывается, как toomanage hello расширения агента SQL Server, которое автоматизирует конкретных задач администрирования SQL Server. Эти задачи включают в себя автоматическую архивацию, автоматическую установку исправлений и интеграцию с хранилищем ключей Azure. В этом разделе используется режим развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>Автоматизация задач управления на виртуальных машинах Azure с помощью hello расширение агента SQL Server (диспетчер ресурсов)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](virtual-machines-windows-sql-server-agent-extension.md)
> * [Классический](../classic/sql-server-agent-extension.md)
> 
> 

Hello расширения агента IaaS SQL Server (SQLIaaSExtension) работает на виртуальных машинах Azure tooautomate административных задач. Здесь представлен обзор служб hello, поддерживаемые расширения hello, а также инструкции по установке, состояния и удаления.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview hello классической версии данной статьи, в разделе [расширение агента SQL Server для классических виртуальных машин SQL Server](../classic/sql-server-agent-extension.md).

## <a name="supported-services"></a>Поддерживаемые службы
Hello расширения агента IaaS SQL Server поддерживает следующие задачи администрирования hello:

| Функция администрирования | Описание |
| --- | --- |
| **Автоматическая архивация SQL** |Автоматизирует hello планирования резервного копирования для всех баз данных для экземпляра по умолчанию hello объекта SQL Server в hello виртуальной Машины. Дополнительные сведения см. в статье [Автоматическая архивация SQL Server на виртуальных машинах Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md). |
| **Автоматическая установка исправлений SQL** |Настраивает периода обслуживания, во время обновления, которые размещаются tooyour предпринять виртуальной Машины, чтобы избежать обновления рабочее время для рабочей нагрузки. Дополнительные сведения см. в статье [Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md). |
| **Интеграция с хранилищем ключей Azure** |Включает tooautomatically можно установить и настроить хранилище ключей Azure в вашей виртуальной Машине SQL Server. Дополнительные сведения см. в статье [Настройка интеграции хранилища ключей Azure для SQL Server на виртуальных машинах Azure (диспетчер ресурсов)](virtual-machines-windows-ps-sql-keyvault.md). |

После установки и запуска, hello расширения агента IaaS SQL Server создает эти функции администрирования на панели SQL Server hello hello виртуальной машины в hello портала Azure и Azure PowerShell для SQL Server marketplace образов и через Azure PowerShell для установки в ручном режиме hello расширения. 

## <a name="prerequisites"></a>Предварительные требования
Требования к toouse hello расширение агента IaaS SQL Server на виртуальной Машине:

**Операционная система**

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Версии SQL Server**

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**

* [Загрузить и настроить hello последних команд Azure PowerShell](/powershell/azure/overview)

## <a name="installation"></a>Установка
Расширения агента SQL Server IaaS Hello устанавливается автоматически при подготовке образов коллекции виртуальных машин SQL Server hello. Если расширение hello tooreinstall вручную на одном из этих виртуальных машин SQL Server требуется, используйте следующую команду PowerShell hello:

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

Это также возможно tooinstall hello расширения агента IaaS SQL Server на виртуальной машине только для ОС Windows Server. Это возможно, если вы вручную установили SQL Server на этом компьютере. А затем установить расширение hello вручную с помощью hello же **AzureVMSqlServerExtension набор** командлета PowerShell.

> [!NOTE]
> При установке вручную hello расширения агента IaaS SQL Server на виртуальной Машине Windows Server только для операционной системы, вы можете управлять не hello параметров конфигурации SQL Server через портал Azure hello. В этом случае все изменения нужно вносить с помощью PowerShell.

## <a name="status"></a>Состояние
Одним из способов tooverify, что расширение hello установлено — состояние агента hello tooview hello портала Azure. Выберите **все параметры** в hello колонке виртуальной машины и выберите команду **расширения**. Вы увидите hello **SQLIaaSExtension** расширение.

![Расширение агента IaaS для SQL Server на портале Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

Можно также использовать hello **Get AzureVMSqlServerExtension** командлет Azure Powershell.

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

Предыдущая команда Hello подтверждает hello агент установлен и предоставляет общие сведения о состоянии сведения. Также можно получить сведения о состоянии автоматического резервного копирования и исправления с hello, следующие команды.

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>Удаление
В hello портал Azure, можно удалить расширение hello, нажав кнопку многоточия hello hello **расширения** колонку свойств виртуальной машины. Затем щелкните **Удалить**.

![Удаление hello расширения агента IaaS SQL Server на портале Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

Можно также использовать hello **AzureRmVMSqlServerExtension удаление** командлета Powershell.

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>Дальнейшие действия
Начать использовать одну из служб hello, поддерживаемого расширением hello. Дополнительные сведения см. в разделе hello разделы, на которые ссылается hello [поддерживается служб](#supported-services) этой статьи.

Подробные сведения о работе SQL Server на виртуальных машинах Azure см. в разделе [Общие сведения об SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).

