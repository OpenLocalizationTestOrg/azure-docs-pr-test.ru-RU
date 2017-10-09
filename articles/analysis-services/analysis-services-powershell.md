---
title: "aaaManage Azure Analysis Services с помощью PowerShell | Документы Microsoft"
description: "Описывается управление службами Azure Analysis Services с помощью PowerShell."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>Управление службами Azure Analysis Services с помощью PowerShell

В этой статье описываются PowerShell командлеты, используемые tooperform Azure Analysis Services сервера и базы данных управления задачи. 

Командлеты диспетчера ресурсов Azure (AzureRM) использовать задач управления сервером, например создание или удаление сервера, приостановка или возобновление работы сервера или изменение уровня службы hello (уровня). Другие задачи для управления базами данных, такие как добавление или удаление членов роли, обработки или секционирование использование командлетов состава hello же модуле SqlServer, что SQL Server Analysis Services.

## <a name="permissions"></a>Разрешения
Большинство задач PowerShell требуется, что у вас есть права администратора на сервере служб Analysis Services hello, которыми вы управляете. Запланированные задачи PowerShell являются автоматическими операциями. Привет, запускающий планировщика hello требуются права администратора на сервере служб Analysis Services hello. 

Для работы сервера с помощью командлетов AzureRm, учетной записи или учетной записи hello планировщик должен принадлежать toohello роль владельца для ресурса hello в [Azure Role-Based управления доступом (RBAC)](../active-directory/role-based-access-control-what-is.md). 

## <a name="server-operations"></a>Операции с сервером 
Командлеты Azure Analysis Services, включаются в hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) компонент модуля. модули командлетов AzureRM tooinstall, в разделе [командлеты диспетчера ресурсов Azure](/powershell/azure/overview) в коллекции PowerShell hello.

|Командлет|Описание| 
|------------|-----------------| 
|[Export-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|Экспорт журнала toofile.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|Возвращает сведения об экземпляре сервера.|  
|[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|Создает экземпляр сервера.|
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|Удаляет экземпляр сервера.|  
|[Suspend-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|Приостанавливает работу экземпляра сервера.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|Возобновляет работу экземпляра сервера.|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|Изменяет экземпляр сервера.|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|Наличие hello тестов экземпляр сервера.| 

## <a name="database-operations"></a>Операции с базой данных

Hello Azure используйте операции с базой данных служб Analysis Services одинаковым [SqlServer](https://www.powershellgallery.com/packages/SqlServer) модуль как SQL Server Analysis Services. Однако для служб Azure Analysis Services поддерживаются не все командлеты. 

модуль SqlServer Hello предоставляет командлеты управления базы данных для определенных задач, а также командлет общего назначения Invoke-ASCmd hello, который принимает табличной модели языка скриптов (TMSL) запроса или скрипта. Hello поддерживаются следующие командлеты в модуле SqlServer hello для служб Azure Analysis Services.

  
|Командлет|Описание|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Добавьте роль члена tooa базы данных.| 
|[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Архивация базы данных Analysis Services.|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Удаление участника из роли базы данных.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Выполнение сценария TMSL.|
|[Invoke-ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|Обработка базы данных.|  
|[Invoke-ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|Обработка секции.| 
|[Invoke-ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|Обработка таблицы.|  
|[Merge-Partition](https://msdn.microsoft.com/library/hh479576.aspx)|Объединение секции.|  
|[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Восстановление базы данных Analysis Services.| 
  

## <a name="related-information"></a>Связанные сведения

* [Скачивание модуля PowerShell SQL Server](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [Скачивание SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [Модуль SqlServer в коллекции PowerShell](https://www.powershellgallery.com/packages/SqlServer)    
* [Tabular Model Programming for Compatibility Level 1200 and higher](https://msdn.microsoft.com/library/mt712541.aspx) (Программирование табличной модели для уровня совместимости 1200 и более высокого)
