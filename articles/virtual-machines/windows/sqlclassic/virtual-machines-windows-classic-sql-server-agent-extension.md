---
title: "задачи управления aaaAutomate на виртуальных машинах SQL (классические) | Документы Microsoft"
description: "В этом разделе описывается, как toomanage hello расширения агента SQL Server, которое автоматизирует конкретных задач администрирования SQL Server. Эти задачи включают в себя автоматическую архивацию, автоматическую установку исправлений и интеграцию с хранилищем ключей Azure. В этом разделе используется режим классическое развертывание hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Автоматизация задач управления на виртуальных машинах Azure с помощью hello расширение агента SQL Server (классические)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Классический](../classic/sql-server-agent-extension.md)
> 
>
 
Hello расширения агента IaaS SQL Server (SQLIaaSAgent) работает на виртуальных машинах Azure tooautomate административных задач. Здесь представлен обзор служб hello, поддерживаемые расширения hello, а также инструкции по установке, состояния и удаления.

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. tooview hello диспетчера ресурсов версию этой статьи в разделе [расширение агента SQL Server для SQL Server виртуальных машин диспетчера ресурсов](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Поддерживаемые службы
Hello расширения агента IaaS SQL Server поддерживает следующие задачи администрирования hello:

| Функция администрирования | Описание |
| --- | --- |
| **Автоматическая архивация SQL** |Автоматизирует hello планирования резервного копирования для всех баз данных для экземпляра по умолчанию hello объекта SQL Server в hello виртуальной Машины. Дополнительные сведения см. в статье [Автоматическая архивация SQL Server на виртуальных машинах Azure (классическая модель)](../classic/sql-automated-backup.md). |
| **Автоматическая установка исправлений SQL** |Настраивает периода обслуживания, во время обновления, которые размещаются tooyour предпринять виртуальной Машины, чтобы избежать обновления рабочее время для рабочей нагрузки. Дополнительные сведения см. в статье [Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (классическая модель)](../classic/sql-automated-patching.md). |
| **Интеграция с хранилищем ключей Azure** |Включает tooautomatically можно установить и настроить хранилище ключей Azure в вашей виртуальной Машине SQL Server. Дополнительные сведения см. в статье [Настройка интеграции хранилища ключей Azure для SQL Server на виртуальных машинах Azure (классическая модель)](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Предварительные требования
Требования к toouse hello расширение агента IaaS SQL Server на виртуальной Машине:

### <a name="operating-system"></a>Операционная система:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>Версии SQL Server:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Azure PowerShell
[Загрузить и настроить hello последних команд Azure PowerShell](/powershell/azure/overview).

Запустите Windows PowerShell и подключите его tooyour подписки Azure с hello **Add-AzureAccount** команды.

    Add-AzureAccount

Если у вас несколько подписок, используйте **Select-AzureSubscription** tooselect hello подписки, содержащей целевой классической виртуальной Машины.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

На этом этапе можно получить список hello классических виртуальных машин и их имена связанная служба с hello **Get-AzureVM** команды.

    Get-AzureVM

## <a name="installation"></a>Установка
Для классических виртуальных машин необходимо использовать PowerShell tooinstall hello расширения агента IaaS SQL Server и настроить связанные с ними службы. Используйте hello **AzureVMSqlServerExtension набор** расширения hello tooinstall командлета PowerShell. Например hello, следующая команда устанавливает расширение hello на ВМ Windows Server (классические) и называет ее «SQLIaaSExtension».

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

При обновлении toohello последнюю версию агента расширения SQL IaaS hello, необходимо перезапустить виртуальную машину после обновления расширения hello.

> [!NOTE]
> Классических виртуальных машин не имеют параметр tooinstall и настроить hello агента расширения SQL IaaS через портал hello.
> 
> 

## <a name="status"></a>Состояние
Одним из способов tooverify, что расширение hello установлено — состояние агента hello tooview hello портала Azure. Выберите виртуальную машину, перечисленных в колонке hello виртуальной машины и выберите команду **расширения**. Вы увидите hello **SQLIaaSAgent** расширение.

![Расширение агента IaaS для SQL Server на портале Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

Можно также использовать hello **Get AzureVMSqlServerExtension** командлет Azure Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Удаление
В hello портал Azure, можно удалить расширение hello, нажав кнопку многоточия hello hello **расширения** колонку свойств виртуальной машины. Щелкните **Удалить**.

![Удаление hello расширения агента IaaS SQL Server на портале Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

Можно также использовать hello **AzureVMSqlServerExtension удаление** командлета Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Дальнейшие действия
Начать использовать одну из служб hello, поддерживаемого расширением hello. Дополнительные сведения см. в разделе hello разделы, на которые ссылается hello [поддерживается служб](#supported-services) этой статьи.

Подробные сведения о работе SQL Server на виртуальных машинах Azure см. в разделе [Общие сведения об SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

