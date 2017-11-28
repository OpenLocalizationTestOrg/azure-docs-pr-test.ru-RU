---
title: "списки управления aaaManage доступ к конечной точке Azure | PowerShell | Классический | Документы Microsoft"
description: "Узнайте, как toomanage списки управления доступом с помощью PowerShell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="e0b01-103">Управление списками управления доступом конечной точки, с помощью PowerShell в hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="e0b01-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="e0b01-104">Можно создать и управлять сети списки управления доступом (ACL) для конечных точек с помощью Azure PowerShell или в hello портала управления.</span><span class="sxs-lookup"><span data-stu-id="e0b01-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="e0b01-105">В этом разделе мы расскажем о том, как выполнять наиболее распространенные действия со списками ACL с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0b01-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="e0b01-106">Список hello Azure PowerShell командлеты разделе [командлеты управления Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="e0b01-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="e0b01-107">Дополнительные сведения о списках ACL см. в статье [Список управления доступом (ACL) конечной точки](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="e0b01-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="e0b01-108">Если toomanage списками ACL с помощью портала управления hello, см. [как tooa tooSet Настройка конечных точек виртуальной машины](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0b01-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="e0b01-109">Управление сетевыми списками ACL с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0b01-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="e0b01-110">Можно использовать toocreate командлетов Azure PowerShell, удаления и настройки (set) сети списки управления доступом (ACL).</span><span class="sxs-lookup"><span data-stu-id="e0b01-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="e0b01-111">Мы включили несколько примеров некоторых hello способов настройки ACL с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0b01-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="e0b01-112">tooretrieve полный список командлетов ACL PowerShell hello, воспользуйтесь одним из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="e0b01-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="e0b01-113">Создание сетевого списка ACL с правилами, которые разрешают доступ из удаленной подсети</span><span class="sxs-lookup"><span data-stu-id="e0b01-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="e0b01-114">в следующем примере Hello иллюстрируется способ toocreate новый список, который содержит правила.</span><span class="sxs-lookup"><span data-stu-id="e0b01-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="e0b01-115">Этот список затем применяется tooa конечной точки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e0b01-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="e0b01-116">правила списков ACL Hello в приведенном ниже примере hello разрешают доступ из удаленной подсети.</span><span class="sxs-lookup"><span data-stu-id="e0b01-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="e0b01-117">toocreate нового списка управления Доступом с разрешающими правилами для удаленной подсети, откройте Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="e0b01-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="e0b01-118">Скопируйте и вставьте ниже, настройка сценария hello собственными значениями hello сценарий и затем запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="e0b01-119">Создайте новый объект и список управления Доступом по сети hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="e0b01-120">Настройте правило, разрешающее доступ из удаленной подсети.</span><span class="sxs-lookup"><span data-stu-id="e0b01-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="e0b01-121">В следующем примере hello, задать правило *100* (имеющее приоритет выше правила 200 и более поздние версии) удаленной подсети hello tooallow *10.0.0.0/8* доступ к конечной точке виртуальной машины toohello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="e0b01-122">Замените значения hello свои собственные требования к конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e0b01-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="e0b01-123">Hello имя «SharePoint ACL config» следует заменить понятным именем hello требуется toocall это правило.</span><span class="sxs-lookup"><span data-stu-id="e0b01-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="e0b01-124">Для дополнительных правил повторите hello командлета, заменив значения hello свои собственные требования к конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e0b01-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="e0b01-125">Убедиться, что toochange hello правило номера заказа tooreflect hello порядок будет которой требуется применить toobe правила hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="e0b01-126">чем меньше номер правила Hello имеет приоритет над hello большее число.</span><span class="sxs-lookup"><span data-stu-id="e0b01-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="e0b01-127">После этого можно создать новую конечную точку (Добавить) или задать hello ACL для существующей конечной точки (Set).</span><span class="sxs-lookup"><span data-stu-id="e0b01-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="e0b01-128">В этом примере мы добавим новую конечную точку виртуальной машины под названием «web» и обновление hello конечной точки виртуальной машины с hello параметры списка управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="e0b01-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="e0b01-129">Затем совместить командлеты hello и запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="e0b01-130">В этом примере hello объединенные командлеты будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e0b01-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="e0b01-131">Удаление из сетевого списка ACL правила, разрешающего доступ из удаленной подсети</span><span class="sxs-lookup"><span data-stu-id="e0b01-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="e0b01-132">в следующем примере Hello иллюстрируется способ tooremove Сетевые правила списка управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="e0b01-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="e0b01-133">tooremove правило списка управления Доступом с разрешающими правилами для удаленной подсети, откройте Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="e0b01-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="e0b01-134">Скопируйте и вставьте ниже, настройка сценария hello собственными значениями hello сценарий и затем запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="e0b01-135">Первым шагом является объект списка управления Доступом hello tooget для конечной точки виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="e0b01-136">Затем необходимо удалить правило списка управления Доступом hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="e0b01-137">В этом случае мы удаляем правило по его идентификатору.</span><span class="sxs-lookup"><span data-stu-id="e0b01-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="e0b01-138">Только идентификатор правила hello 0 будут удалены из hello ACL.</span><span class="sxs-lookup"><span data-stu-id="e0b01-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="e0b01-139">Не удаляет hello объекта списка управления Доступом из конечной точки виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="e0b01-140">Далее необходимо применить конечной точки виртуальной машины toohello объект списка управления Доступом hello и обновить hello виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e0b01-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="e0b01-141">Удаление сетевого списка ACL с конечной точки виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e0b01-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="e0b01-142">В некоторых сценариях может потребоваться tooremove объект списка управления Доступом из конечной точки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e0b01-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="e0b01-143">toodo, откройте Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="e0b01-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="e0b01-144">Скопируйте и вставьте ниже, настройка сценария hello собственными значениями hello сценарий и затем запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="e0b01-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="e0b01-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0b01-145">Next steps</span></span>
[<span data-ttu-id="e0b01-146">Сетевой список управления доступом</span><span class="sxs-lookup"><span data-stu-id="e0b01-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

