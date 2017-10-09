---
title: "aaaAdd ВМ по умолчанию hello образа marketplace стек Azure toohello | Документы Microsoft"
description: "Добавьте hello виртуальной Машины Windows Server 2016 по умолчанию изображение toohello стека Azure marketplace."
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
ms.openlocfilehash: 9b5a6f4e4c73c706b059e3c3622a968b5eef9a27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-hello-windows-server-2016-vm-image-toohello-azure-stack-marketplace"></a>Добавить hello виртуальной Машины Windows Server 2016 изображения toohello стека Azure marketplace

По умолчанию отсутствуют все образы виртуальных машин в hello стек Azure marketplace. администратору облака Azure стека Hello необходимо добавить toohello образа marketplace, чтобы пользователи могли использовать их. Windows Server 2016 hello изображения toohello стека Azure marketplace можно добавить с помощью одного из следующих двух методов hello:

* [Добавить изображение hello, загрузив его с hello Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -используйте этот параметр, если вы работаете в сценарии подключенных и если вы зарегистрировали экземпляра Azure стека с помощью Azure.

* [Добавить изображение hello с помощью PowerShell](#add-the-image-by-using-powershell) -используйте этот параметр, если вы развернули стек Azure в сценарии отсоединения, или в сценариях с ограниченной подключением.

## <a name="add-hello-image-by-downloading-it-from-hello-azure-marketplace"></a>Добавить изображение hello, загрузив его с hello Azure Marketplace

1. После развертывания Azure стека, войдите в tooyour пакет средств разработки Azure стека.

2. Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавить из Azure** 

3. Поиск или поиск hello **Windows Server 2016 центра обработки данных — Eval** изображение > щелкните **загрузки**

   ![Загрузите образ из Azure](media/azure-stack-add-default-image/download-image.png)

После завершения загрузки hello hello изображение будет добавлено toohello **управления Marketplace** колонки и он также доступен из hello **виртуальные машины** колонку.

## <a name="add-hello-image-by-using-powershell"></a>Добавить изображение hello с помощью PowerShell

### <a name="prerequisites"></a>Предварительные требования 

Запустите hello следующие необходимые компоненты из hello [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  

* Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).  

* Go toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 и загрузка пробной версии Windows Server 2016 hello. При появлении запроса выберите hello **ISO** версии hello загрузки. Путь toohello записей hello загрузите расположение, которое будет использоваться в дальнейшем эти действия. Необходимо подключение к Интернету.  

Теперь выполните следующие шаги tooadd hello изображения toohello стека Azure marketplace hello.
   
1. Импортируйте модули Azure Connect стека и ComputeAdmin hello с помощью hello, следующие команды:

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. Войдите в систему tooyour среды Azure стека. Выполнения hello следующий скрипт в зависимости от того, при развертывании среды стека Azure с помощью AAD или AD FS (Убедитесь, что tooreplace hello AAD имя клиента):  

   а. **Azure Active Directory**, используйте следующий командлет hello:

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   b. **Службы федерации Active Directory**, используйте следующий командлет hello:
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. Добавьте Windows Server 2016 hello изображения toohello стека Azure marketplace (Убедитесь, что hello tooreplace *Path_to_ISO* с toohello путь hello загруженный ISO WS2016):

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

tooensure, hello образ виртуальной Машины Windows Server 2016 имеет hello последний накопительный пакет обновления, включают hello `IncludeLatestCU` при выполнении hello `New-AzsServer2016VMImage` командлета. В разделе hello [параметры](#parameters) сведения о допустимых параметрах hello `New-AzsServer2016VMImage` командлет. Это занимает около часа toopublish hello изображения toohello стека Azure marketplace. 

## <a name="parameters"></a>Параметры

|Параметры нового AzsServer2016VMImage|Обязательный?|Описание|
|-----|-----|------|
|ISOPath|Да|Hello toohello полный путь загрузки Windows Server 2016 ISO.|
|net35|Нет|Этот параметр позволяет среды выполнения .NET 3.5 hello tooinstall в образ Windows Server 2016 hello. По умолчанию это значение имеет значение tootrue. Является обязательным, что это изображение hello содержит hello .NET 3.5 среды выполнения tooinstall hello SQL и MYSQL поставщиков ресурсов. |
|Version (версия)|Нет|Этот параметр позволяет вам toochoose ли tooadd **Core** или **полного** или **оба** образы Windows Server 2016. По умолчанию это значение «Переполнен.»|
|VHDSizeInMB|Нет|Задает hello объем (в МБ) toobe образа виртуального жесткого диска hello добавлен tooyour среду стека Azure. По умолчанию это значение задано too40960 МБ.|
|CreateGalleryItem|Нет|Указывает, следует ли создать элемент Marketplace для образа Windows Server 2016 hello. По умолчанию это значение имеет значение tootrue.|
|location |Нет |Указывает расположение toowhich hello hello-образ Windows Server 2016 должна быть опубликована.|
|IncludeLatestCU|Нет|Установите этот переключатель tooapply hello последнюю Windows Server 2016 накопительное обновление toohello нового виртуального жесткого диска.|
|CUUri |Нет |Задайте значение toochoose hello Windows Server 2016 накопительного обновления от указанного URI. |
|CUPath |Нет |Задайте значение toochoose hello Windows Server 2016 накопительного обновления из локального пути. Этот параметр полезен, если вы развернули экземпляр hello Azure стека в отключенной среде.|

## <a name="next-steps"></a>Дальнейшие действия

[Подготовка виртуальной машины](azure-stack-provision-vm.md)
