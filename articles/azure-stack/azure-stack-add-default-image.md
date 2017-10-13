---
title: "Добавление образа виртуальной Машины по умолчанию в стек Azure Marketplace | Документы Microsoft"
description: "Добавьте образ виртуальной Машины Windows Server 2016 по умолчанию в стек Azure Marketplace."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 43781cb025865df1d228376f57412f3d482d3ad0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="add-the-windows-server-2016-vm-image-to-the-azure-stack-marketplace"></a>Добавить образ виртуальной Машины Windows Server 2016 в стек Azure Marketplace

По умолчанию отсутствуют все образы виртуальных машин в стек Azure marketplace. Оператор стек Azure необходимо добавить изображение в Marketplace, чтобы пользователи могли использовать их. Образ Windows Server 2016 в стек Azure Marketplace можно добавить с помощью одного из следующих двух способов:

* [Добавить изображение, загрузив его из Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -используйте этот параметр, если вы работаете в сценарии подключенных и если вы зарегистрировали экземпляра Azure стека с помощью Azure.

* [Добавление изображения с помощью PowerShell](#add-the-image-by-using-powershell) -используйте этот параметр, если вы развернули стек Azure в сценарии отсоединения, или в сценариях с ограниченной подключением.

## <a name="add-the-image-by-downloading-it-from-the-azure-marketplace"></a>Добавить изображение, загрузив его из Azure Marketplace

1. После развертывания Azure стека, войдите в ваш пакет средств разработки Azure стека.

2. Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавить из Azure** 

3. Поиск **Windows Server 2016 центра обработки данных — Eval** изображение > щелкните **загрузки**

   ![Загрузите образ из Azure](media/azure-stack-add-default-image/download-image.png)

После завершения загрузки, изображение будет добавлено к **управления Marketplace** колонки и он также доступен из **виртуальные машины** колонку.

## <a name="add-the-image-by-using-powershell"></a>Добавление изображения с помощью PowerShell

### <a name="prerequisites"></a>Предварительные требования 

Выполнить следующие предварительные требования, либо из [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  

* Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).  

* Перейдите к https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 и загрузить ознакомительную версию Windows Server 2016. При появлении запроса выберите **ISO** версию для загрузки. Запишите путь к расположению загрузки, который используется далее в этом пошаговом руководстве. Необходимо подключение к Интернету.  

Теперь выполните следующие действия, чтобы добавить изображение в стек Azure marketplace:
   
1. Импортируйте модули Azure Connect стека и ComputeAdmin с помощью следующих команд:

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. Войдите в среду Azure стека. Выполните следующий сценарий, в зависимости от среды стека Azure развертывается с помощью AAD или AD FS (Убедитесь, что для замены AAD tenantName, GraphAudience конечной точки и ArmEndpoint значения в зависимости от конфигурации вашей среды):  

   а. **Azure Active Directory**, используйте следующий командлет:

   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.windows.net/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"
   
   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience $GraphAudience

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   b. **Службы федерации Active Directory**, используйте следующий командлет:
    
   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.local.azurestack.external/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience $GraphAudience `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. Добавить образ Windows Server 2016 в стек Azure Marketplace (не забудьте заменить *Path_to_ISO* с путем к загруженный ISO WS2016):

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

Чтобы убедиться, что образ виртуальной Машины Windows Server 2016 имеет последний накопительный пакет обновления, включите `IncludeLatestCU` во время выполнения `New-AzsServer2016VMImage` командлета. В разделе [параметры](#parameters) сведения о допустимых параметрах `New-AzsServer2016VMImage` командлета. Опубликовать изображения в магазине Azure стека занимает около часа. 

## <a name="parameters"></a>Параметры

|Параметры нового AzsServer2016VMImage|Обязательный?|Описание|
|-----|-----|------|
|ISOPath|Да|Полный путь к загруженный ISO Windows Server 2016.|
|net35|Нет|Этот параметр позволяет установить среду выполнения .NET 3.5 в образе Windows Server 2016. По умолчанию это значение равным true.|
|Version (версия)|Нет|Этот параметр позволяет выбрать, следует ли добавить **Core** или **полного** или **оба** образы Windows Server 2016. По умолчанию это значение равно «Full».|
|VHDSizeInMB|Нет|Задает размер образа виртуального жесткого диска для добавления в среду Azure стека (в МБ). По умолчанию это значение будет присвоено 40960 МБ.|
|CreateGalleryItem|Нет|Указывает, следует ли создать элемент Marketplace для образа Windows Server 2016. По умолчанию это значение равным true.|
|location |Нет |Указывает расположение, к которому должны публиковаться образа Windows Server 2016.|
|IncludeLatestCU|Нет|Установите этот переключатель, чтобы применить последнее накопительное обновление Windows Server 2016 для нового виртуального жесткого диска.|
|CUUri |Нет |Это значение используется для выбора накопительное обновление Windows Server 2016 из указанного URI. |
|CUPath |Нет |Это значение используется для выбора накопительное обновление Windows Server 2016 из локального пути. Этот параметр полезен, если вы развернули экземпляра Azure стека в отключенной среде.|

## <a name="next-steps"></a>Дальнейшие действия

[Подготовка виртуальной машины](azure-stack-provision-vm.md)
