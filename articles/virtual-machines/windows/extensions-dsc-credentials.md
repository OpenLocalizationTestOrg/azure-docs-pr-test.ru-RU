---
title: "aaaPassing учетные данные с помощью DSC tooAzure | Документы Microsoft"
description: "Общие сведения о безопасной передачи учетных данных tooAzure виртуальных машин, с помощью настройки требуемого состояния PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>Передача обработчик расширений Azure DSC toohello учетные данные
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

В этой статье описаны расширения hello настройки требуемого состояния для Azure. Общие сведения о обработчика расширений hello DSC можно найти в [обработчик расширений Azure настройки требуемого состояния введение toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Передача учетных данных
Как часть процесса настройки hello, может потребоваться tooset учетные записи пользователей, доступ к службам, или установить программу в контексте пользователя. toodo эти действия необходимо иметь учетные данные tooprovide. 

DSC позволяет параметризованные конфигурации, в которых учетные данные переданные в конфигурации hello и безопасно хранятся в MOF-файлов. Hello обработчик расширений Azure упрощает управление учетными данными за счет автоматического управления сертификатами. 

Рассмотрим следующий сценарий конфигурации DSC, который создает учетную запись локального пользователя с указанным паролем hello hello.

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

Это важные tooinclude *узла localhost* как часть конфигурации hello. Если эта инструкция отсутствует, hello следующие шаги не работают как обработчик расширений hello специально ищет hello узла localhost инструкции. Также очень важно выполнить приведение tooinclude hello *[PsCredential]*, как hello расширения tooencrypt hello credential триггеры этого типа. 

Опубликуйте это хранилище tooblob сценария:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Задать расширение Azure DSC hello и hello учетные данные:

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>Защита учетных данных
При выполнении этого кода запрашиваются учетные данные. Указанные учетные данные кратковременно хранятся в памяти. При публикации с `Set-AzureVmDscExtension` командлета, он передается через HTTPS toohello виртуальной Машины, где Azure сохраняется шифроваться на диске, с помощью hello локальный сертификат для виртуальной Машины. Затем кратко расшифровывается в памяти и повторно зашифровать toopass его tooDSC.

Это поведение отличается от [с использованием безопасной конфигурации без обработчика расширений hello](https://msdn.microsoft.com/powershell/dsc/securemof). Hello среды Azure предоставляет как данные конфигурации tootransmit безопасно с помощью сертификатов. При использовании обработчика расширений hello DSC, нет нет необходимости tooprovide $CertificatePath или $CertificateID / $Thumbprint записи в ConfigurationData.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello обработчик расширений Azure DSC см. в разделе [обработчик расширений Azure настройки требуемого состояния введение toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Изучите hello [шаблона Azure Resource Manager для расширения hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Дополнительные сведения о PowerShell DSC [посетите центр документации PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

Дополнительные функциональные возможности toofind можно управлять с помощью PowerShell DSC [Обзор коллекции PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) дополнительные ресурсы DSC.

