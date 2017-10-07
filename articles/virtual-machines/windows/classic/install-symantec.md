---
title: "aaaInstall Symantec Endpoint Protection на виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall и настроить модуль безопасности hello Symantec Endpoint Protection на новый или существующей виртуальной Машине Azure hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="16101-103">Как tooinstall и настройка Symantec Endpoint Protection на виртуальной Машине Windows</span><span class="sxs-lookup"><span data-stu-id="16101-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="16101-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="16101-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="16101-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="16101-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="16101-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="16101-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="16101-107">В этой статье показано, как tooinstall и настройки клиента hello Symantec Endpoint Protection на существующей виртуальной машины (VM) под управлением Windows Server.</span><span class="sxs-lookup"><span data-stu-id="16101-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="16101-108">Этот полный клиент включает такие службы, как защита от вирусов и шпионских программ, брандмауэр и система предотвращения вторжений.</span><span class="sxs-lookup"><span data-stu-id="16101-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="16101-109">Клиент Hello устанавливается как расширение безопасности с помощью hello агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="16101-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="16101-110">Если у вас есть подписка от Symantec для решения в локальной среде, можно использовать его tooprotect виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="16101-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="16101-111">Если у вас еще нет подписки, можно зарегистрироваться для получения пробной подписки.</span><span class="sxs-lookup"><span data-stu-id="16101-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="16101-112">Дополнительные сведения об этом решении см. в статье [Symantec Endpoint Protection на платформе Microsoft Azure][Symantec].</span><span class="sxs-lookup"><span data-stu-id="16101-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="16101-113">Эта страница также содержит ссылки toolicensing сведения и инструкции по установке клиента hello, если вы уже клиента Symantec.</span><span class="sxs-lookup"><span data-stu-id="16101-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="16101-114">Установка Symantec Endpoint Protection на существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="16101-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="16101-115">Прежде чем начать, необходимо hello следующее:</span><span class="sxs-lookup"><span data-stu-id="16101-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="16101-116">модуль Azure PowerShell Hello, версии 0.8.2 или более поздней версии на рабочем компьютере.</span><span class="sxs-lookup"><span data-stu-id="16101-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="16101-117">Можно проверить версию hello Azure PowerShell, установленной с hello **Get-Module azure | format-table версии** команды.</span><span class="sxs-lookup"><span data-stu-id="16101-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="16101-118">Инструкции и ссылки toohello последнюю версию, в разделе [как tooInstall и настройка Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="16101-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="16101-119">Вход с использованием подписки Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="16101-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="16101-120">Hello Здравствуйте, агент ВМ, работающий на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="16101-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="16101-121">Сначала проверьте, что hello агент виртуальной Машины уже установлена на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="16101-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="16101-122">Заполните hello имя облачной службы и имя виртуальной машины, а затем запустите следующие команды в командной строке Azure PowerShell администраторские hello.</span><span class="sxs-lookup"><span data-stu-id="16101-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="16101-123">Замените все содержимое в кавычках hello, включая hello < и > символов.</span><span class="sxs-lookup"><span data-stu-id="16101-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="16101-124">Если вы не знаете hello облачной службы и имена виртуальных машин, запустите **Get-AzureVM** toolist hello имена для всех виртуальных машин в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="16101-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="16101-125">Если hello **write-host** команда отображает **True**, hello установлен агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="16101-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="16101-126">Если отображается **False**, см. инструкции hello и toohello ссылку загрузить в Azure в блоге hello [агент ВМ и расширения — часть 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="16101-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="16101-127">Если установлен агент ВМ hello, запустите следующие команды tooinstall hello Symantec Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="16101-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="16101-128">tooverify, hello Symantec модуль безопасности был установлен и обновлен:</span><span class="sxs-lookup"><span data-stu-id="16101-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="16101-129">Войдите в систему виртуальной машины toohello.</span><span class="sxs-lookup"><span data-stu-id="16101-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="16101-130">Инструкции см. в разделе [как tooLog на виртуальной машине под управлением Windows Server tooa][Logon].</span><span class="sxs-lookup"><span data-stu-id="16101-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="16101-131">Для Windows Server 2008 R2: щелкните **Пуск > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="16101-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="16101-132">Для Windows Server 2012 или Windows Server 2012 R2, hello начальном экране введите **Symantec**, а затем нажмите кнопку **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="16101-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="16101-133">Из hello **состояние** вкладка hello **состояние Symantec Endpoint Protection** окна, установки обновлений и при необходимости перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="16101-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="16101-134">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="16101-134">Additional resources</span></span>
<span data-ttu-id="16101-135">[Как tooLog на tooa виртуальной машины под управлением Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="16101-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="16101-136">[Расширения и компоненты виртуальных машин Azure][Ext]</span><span class="sxs-lookup"><span data-stu-id="16101-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
