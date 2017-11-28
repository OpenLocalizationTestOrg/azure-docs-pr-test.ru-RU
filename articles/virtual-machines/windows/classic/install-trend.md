---
title: "aaaInstall Trend Micro Deep Security на виртуальной Машине | Документы Microsoft"
description: "В этой статье описывается как tooinstall и настройка Trend Micro безопасности на виртуальной Машине, созданные hello классической модели развертывания в Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="cee8e-103">Как tooinstall и настройка Trend Micro Deep Security в качестве службы на виртуальной Машине Windows</span><span class="sxs-lookup"><span data-stu-id="cee8e-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cee8e-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cee8e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cee8e-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="cee8e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="cee8e-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cee8e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="cee8e-107">В этой статье показано, как tooinstall и настройка Trend Micro Deep Security как службы на новой или существующей виртуальной машины (VM) под управлением Windows Server.</span><span class="sxs-lookup"><span data-stu-id="cee8e-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="cee8e-108">Deep Security как услуга включает защиту от вредоносных программ, брандмауэр, систему предотвращения вторжений и мониторинг целостности.</span><span class="sxs-lookup"><span data-stu-id="cee8e-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="cee8e-109">Клиент Hello устанавливается как расширение безопасности через hello агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cee8e-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="cee8e-110">На новой виртуальной машины установите hello Deep Security Agent, как hello агент виртуальной Машины автоматически создается по hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cee8e-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="cee8e-111">Существующей виртуальной Машины, созданные с помощью классического портала hello, hello Azure CLI или PowerShell могут не иметь агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cee8e-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="cee8e-112">Для существующей виртуальной машины, у которого нет hello агент виртуальной Машины требуется toodownload и сначала установить.</span><span class="sxs-lookup"><span data-stu-id="cee8e-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="cee8e-113">В данной статье рассматриваются обе ситуации.</span><span class="sxs-lookup"><span data-stu-id="cee8e-113">This article covers both situations.</span></span>

<span data-ttu-id="cee8e-114">При наличии действующей подписки из Trend Micro локального решения, его можно использовать toohelp защиты виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="cee8e-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="cee8e-115">Если у вас еще нет подписки, можно зарегистрироваться для получения пробной подписки.</span><span class="sxs-lookup"><span data-stu-id="cee8e-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="cee8e-116">Дополнительные сведения об этом решении см. в разделе блога hello Trend Micro [Microsoft Azure VM агент расширения для Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="cee8e-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="cee8e-117">Установите hello Deep Security Agent на новой виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="cee8e-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="cee8e-118">Hello [портал Azure](http://portal.azure.com) позволяет устанавливать расширения безопасности Trend Micro hello при использовании образа с hello **Marketplace** toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cee8e-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="cee8e-119">При создании одной виртуальной машины с помощью портала hello является легко tooadd защиту Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="cee8e-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="cee8e-120">С помощью записи из hello **Marketplace** открывает мастер, который помогает настроить hello виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="cee8e-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="cee8e-121">Использовать hello **параметры** колонки, третья панель hello приветствия мастера tooinstall hello Trend Micro модуль безопасности.</span><span class="sxs-lookup"><span data-stu-id="cee8e-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="cee8e-122">Общие инструкции см. в разделе [создать виртуальную машину под управлением Windows в hello портал Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="cee8e-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="cee8e-123">При получении toohello **параметры** колонке мастера hello hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cee8e-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="cee8e-124">Нажмите кнопку **расширения**, нажмите кнопку **добавить расширение** в следующую область hello.</span><span class="sxs-lookup"><span data-stu-id="cee8e-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Приступите к добавлению расширения hello][1]

2. <span data-ttu-id="cee8e-126">Выберите **Deep Security Agent** в hello **новый ресурс** области.</span><span class="sxs-lookup"><span data-stu-id="cee8e-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="cee8e-127">В области hello Deep Security Agent щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="cee8e-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Поиск агента Deep Security][2]

3. <span data-ttu-id="cee8e-129">Введите hello **идентификатор клиента** и **пароль активации клиента** для расширения hello.</span><span class="sxs-lookup"><span data-stu-id="cee8e-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="cee8e-130">При необходимости можно ввести значение **Security Policy Identifier** (Идентификатор политики безопасности).</span><span class="sxs-lookup"><span data-stu-id="cee8e-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="cee8e-131">Нажмите кнопку **ОК** tooadd hello клиента.</span><span class="sxs-lookup"><span data-stu-id="cee8e-131">Then, click **OK** tooadd hello client.</span></span>

   ![Ввод данных расширения][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="cee8e-133">Установите hello Deep Security Agent на существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="cee8e-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="cee8e-134">агент hello tooinstall на существующей виртуальной Машине, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="cee8e-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="cee8e-135">модуль Azure PowerShell Hello, версии 0.8.2 или более новую, установленных на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="cee8e-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="cee8e-136">Можно проверить версию hello Azure PowerShell, установленный с помощью hello **Get-Module azure | format-table версии** команды.</span><span class="sxs-lookup"><span data-stu-id="cee8e-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="cee8e-137">Инструкции и ссылки toohello последнюю версию, в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cee8e-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="cee8e-138">Вход с использованием подписки Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="cee8e-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="cee8e-139">Hello hello целевой виртуальной машине установлен агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cee8e-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="cee8e-140">Сначала проверьте, что приветствия уже установлен агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cee8e-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="cee8e-141">Заполните hello имя облачной службы и имя виртуальной машины, а затем запустите следующие команды в командной строке Azure PowerShell администраторские hello.</span><span class="sxs-lookup"><span data-stu-id="cee8e-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="cee8e-142">Замените все содержимое в кавычках hello, включая hello < и > символов.</span><span class="sxs-lookup"><span data-stu-id="cee8e-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="cee8e-143">Если вы не знаете hello облачной службы и имя виртуальной машины, выполните **Get-AzureVM** toodisplay hello, сведения для всех виртуальных машин в вашей текущей подписки.</span><span class="sxs-lookup"><span data-stu-id="cee8e-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="cee8e-144">Если hello **write-host** возвращает **True**, hello установлен агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cee8e-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="cee8e-145">Если он возвращает **False**, см. инструкции hello и toohello ссылку загрузить в Azure в блоге hello [агент ВМ и расширения — часть 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="cee8e-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="cee8e-146">Если установлен hello агент виртуальной Машины, выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="cee8e-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="cee8e-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cee8e-147">Next steps</span></span>
<span data-ttu-id="cee8e-148">Он занимает несколько минут для hello агента toostart выполняется при его установке.</span><span class="sxs-lookup"><span data-stu-id="cee8e-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="cee8e-149">После этого вам требуется tooactivate Deep Security на виртуальной машине hello, им можно управлять с глубокой диспетчер безопасности.</span><span class="sxs-lookup"><span data-stu-id="cee8e-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="cee8e-150">См. следующие статьи для получения дополнительных инструкций hello.</span><span class="sxs-lookup"><span data-stu-id="cee8e-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="cee8e-151">статья Trend об этом решении, [Мгновенное включение облачной защиты для Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="cee8e-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="cee8e-152">Объект [пример сценария Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cee8e-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="cee8e-153">[Инструкции](http://go.microsoft.com/fwlink/?LinkId=404099) для образца hello</span><span class="sxs-lookup"><span data-stu-id="cee8e-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cee8e-154">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cee8e-154">Additional resources</span></span>
<span data-ttu-id="cee8e-155">[Как toolog на tooa виртуальной машине под управлением Windows Server]</span><span class="sxs-lookup"><span data-stu-id="cee8e-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="cee8e-156">[Расширения и компоненты виртуальных машин Azure]</span><span class="sxs-lookup"><span data-stu-id="cee8e-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Как toolog на tooa виртуальной машине под управлением Windows Server]:connect-logon.md
[Расширения и компоненты виртуальных машин Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
