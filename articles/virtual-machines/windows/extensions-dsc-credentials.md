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
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="3960f-103">Передача обработчик расширений Azure DSC toohello учетные данные</span><span class="sxs-lookup"><span data-stu-id="3960f-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="3960f-104">В этой статье описаны расширения hello настройки требуемого состояния для Azure.</span><span class="sxs-lookup"><span data-stu-id="3960f-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="3960f-105">Общие сведения о обработчика расширений hello DSC можно найти в [обработчик расширений Azure настройки требуемого состояния введение toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3960f-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="3960f-106">Передача учетных данных</span><span class="sxs-lookup"><span data-stu-id="3960f-106">Passing in credentials</span></span>
<span data-ttu-id="3960f-107">Как часть процесса настройки hello, может потребоваться tooset учетные записи пользователей, доступ к службам, или установить программу в контексте пользователя.</span><span class="sxs-lookup"><span data-stu-id="3960f-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="3960f-108">toodo эти действия необходимо иметь учетные данные tooprovide.</span><span class="sxs-lookup"><span data-stu-id="3960f-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="3960f-109">DSC позволяет параметризованные конфигурации, в которых учетные данные переданные в конфигурации hello и безопасно хранятся в MOF-файлов.</span><span class="sxs-lookup"><span data-stu-id="3960f-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="3960f-110">Hello обработчик расширений Azure упрощает управление учетными данными за счет автоматического управления сертификатами.</span><span class="sxs-lookup"><span data-stu-id="3960f-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="3960f-111">Рассмотрим следующий сценарий конфигурации DSC, который создает учетную запись локального пользователя с указанным паролем hello hello.</span><span class="sxs-lookup"><span data-stu-id="3960f-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="3960f-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="3960f-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="3960f-113">Это важные tooinclude *узла localhost* как часть конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="3960f-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="3960f-114">Если эта инструкция отсутствует, hello следующие шаги не работают как обработчик расширений hello специально ищет hello узла localhost инструкции.</span><span class="sxs-lookup"><span data-stu-id="3960f-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="3960f-115">Также очень важно выполнить приведение tooinclude hello *[PsCredential]*, как hello расширения tooencrypt hello credential триггеры этого типа.</span><span class="sxs-lookup"><span data-stu-id="3960f-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="3960f-116">Опубликуйте это хранилище tooblob сценария:</span><span class="sxs-lookup"><span data-stu-id="3960f-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="3960f-117">Задать расширение Azure DSC hello и hello учетные данные:</span><span class="sxs-lookup"><span data-stu-id="3960f-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="3960f-118">Защита учетных данных</span><span class="sxs-lookup"><span data-stu-id="3960f-118">How credentials are secured</span></span>
<span data-ttu-id="3960f-119">При выполнении этого кода запрашиваются учетные данные.</span><span class="sxs-lookup"><span data-stu-id="3960f-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="3960f-120">Указанные учетные данные кратковременно хранятся в памяти.</span><span class="sxs-lookup"><span data-stu-id="3960f-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="3960f-121">При публикации с `Set-AzureVmDscExtension` командлета, он передается через HTTPS toohello виртуальной Машины, где Azure сохраняется шифроваться на диске, с помощью hello локальный сертификат для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3960f-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="3960f-122">Затем кратко расшифровывается в памяти и повторно зашифровать toopass его tooDSC.</span><span class="sxs-lookup"><span data-stu-id="3960f-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="3960f-123">Это поведение отличается от [с использованием безопасной конфигурации без обработчика расширений hello](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="3960f-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="3960f-124">Hello среды Azure предоставляет как данные конфигурации tootransmit безопасно с помощью сертификатов.</span><span class="sxs-lookup"><span data-stu-id="3960f-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="3960f-125">При использовании обработчика расширений hello DSC, нет нет необходимости tooprovide $CertificatePath или $CertificateID / $Thumbprint записи в ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="3960f-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3960f-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3960f-126">Next steps</span></span>
<span data-ttu-id="3960f-127">Дополнительные сведения о hello обработчик расширений Azure DSC см. в разделе [обработчик расширений Azure настройки требуемого состояния введение toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3960f-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="3960f-128">Изучите hello [шаблона Azure Resource Manager для расширения hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3960f-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="3960f-129">Дополнительные сведения о PowerShell DSC [посетите центр документации PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="3960f-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="3960f-130">Дополнительные функциональные возможности toofind можно управлять с помощью PowerShell DSC [Обзор коллекции PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) дополнительные ресурсы DSC.</span><span class="sxs-lookup"><span data-stu-id="3960f-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

