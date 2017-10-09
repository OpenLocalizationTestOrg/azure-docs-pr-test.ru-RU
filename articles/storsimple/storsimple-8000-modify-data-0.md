---
title: "aaaModify DATA 0 параметры устройства серии StorSimple 8000 | Документы Microsoft"
description: "Узнайте, как toouse Windows PowerShell для StorSimple tooreconfigure hello сетевого интерфейса DATA 0 на устройстве StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="8d182-103">Изменить параметры hello данных 0 сетевого интерфейса на устройстве серии StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="8d182-103">Modify hello DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="8d182-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8d182-104">Overview</span></span>

<span data-ttu-id="8d182-105">Устройство Microsoft Azure StorSimple имеет шесть сетевых интерфейсов: DATA 0 tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="8d182-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="8d182-106">Здравствуйте, DATA 0 всегда настраивается через интерфейс Windows PowerShell hello или последовательной консоли hello интерфейс и автоматически облаком.</span><span class="sxs-lookup"><span data-stu-id="8d182-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="8d182-107">Обратите внимание, что невозможно настроить сетевого интерфейса DATA 0 через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8d182-107">Note that you cannot configure DATA 0 network interface through hello Azure portal.</span></span>

<span data-ttu-id="8d182-108">Здравствуйте, интерфейс сначала настраивается с помощью мастера установки hello во время первоначального развертывания устройства StorSimple hello DATA 0.</span><span class="sxs-lookup"><span data-stu-id="8d182-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="8d182-109">При hello устройство находится в рабочем режиме, может возникнуть необходимость tooreconfigure DATA 0 параметров.</span><span class="sxs-lookup"><span data-stu-id="8d182-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="8d182-110">Этот учебник содержит два метода toomodify настроек сети DATA 0, как с помощью Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8d182-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="8d182-111">После изучения этого учебника вы сможете сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="8d182-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="8d182-112">Изменение данных 0 сетевой параметр через приветствия мастера установки</span><span class="sxs-lookup"><span data-stu-id="8d182-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="8d182-113">Изменение настроек сети DATA 0 через hello `Set-HcsNetInterface` командлета</span><span class="sxs-lookup"><span data-stu-id="8d182-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="8d182-114">Изменение сетевых параметров DATA 0 с помощью мастера установки</span><span class="sxs-lookup"><span data-stu-id="8d182-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="8d182-115">За счет подключения toohello интерфейс Windows PowerShell устройства StorSimple и запуск сеанса мастера установки можно перенастроить настроек сети DATA 0.</span><span class="sxs-lookup"><span data-stu-id="8d182-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="8d182-116">Выполните следующие шаги toomodify DATA 0 hello параметры:</span><span class="sxs-lookup"><span data-stu-id="8d182-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="8d182-117">toomodify настроек сети DATA 0 через мастер установки</span><span class="sxs-lookup"><span data-stu-id="8d182-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="8d182-118">В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="8d182-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="8d182-119">При появлении запроса укажите hello **пароль администратора устройства**.</span><span class="sxs-lookup"><span data-stu-id="8d182-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="8d182-120">пароль по умолчанию Hello — `Password1`.</span><span class="sxs-lookup"><span data-stu-id="8d182-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="8d182-121">Hello командной строки введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8d182-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="8d182-122">Мастер установки отображается toohelp Настройка hello DATA 0 интерфейс устройства.</span><span class="sxs-lookup"><span data-stu-id="8d182-122">A setup wizard appears toohelp configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="8d182-123">Укажите новые значения для hello IP-адрес шлюза и маска подсети.</span><span class="sxs-lookup"><span data-stu-id="8d182-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="8d182-124">Hello фиксированной контроллеров, IP-адреса потребуется перенастроить через hello toobe **сетевые параметры** колонке hello устройства StorSimple в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d182-124">hello fixed controllers IPs will need toobe reconfigured through hello **Network settings** blade of hello StorSimple device in hello Azure portal.</span></span> <span data-ttu-id="8d182-125">Дополнительные сведения см. слишком[изменить сетевые интерфейсы](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="8d182-125">For more information, go too[Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="8d182-126">Изменение сетевых параметров DATA 0 с помощью командлета Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="8d182-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="8d182-127">Альтернативный способ tooreconfigure DATA 0 сетевой интерфейс является использование hello hello `Set-HcsNetInterface` командлета.</span><span class="sxs-lookup"><span data-stu-id="8d182-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="8d182-128">командлет Hello выполняется из hello в интерфейсе Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8d182-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="8d182-129">При использовании этой процедуры, фиксированные IP-адреса контроллера hello также здесь можно настроить.</span><span class="sxs-lookup"><span data-stu-id="8d182-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="8d182-130">Выполните следующие шаги toomodify hello DATA 0 hello параметры:</span><span class="sxs-lookup"><span data-stu-id="8d182-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="8d182-131">toomodify настроек сети DATA 0 через командлет Set-HcsNetInterface hello</span><span class="sxs-lookup"><span data-stu-id="8d182-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="8d182-132">В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="8d182-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="8d182-133">При появлении запроса укажите пароль администратора устройства hello.</span><span class="sxs-lookup"><span data-stu-id="8d182-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="8d182-134">пароль по умолчанию Hello — `Password1`.</span><span class="sxs-lookup"><span data-stu-id="8d182-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="8d182-135">Hello командной строки введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8d182-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="8d182-136">В квадратных скобках hello под углом введите следующие значения для DATA 0 hello:</span><span class="sxs-lookup"><span data-stu-id="8d182-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="8d182-137">IPv4-адреса;</span><span class="sxs-lookup"><span data-stu-id="8d182-137">IPv4 address</span></span>
   * <span data-ttu-id="8d182-138">шлюза IPv4;</span><span class="sxs-lookup"><span data-stu-id="8d182-138">IPv4 gateway</span></span>
   * <span data-ttu-id="8d182-139">маски подсети IPv4;</span><span class="sxs-lookup"><span data-stu-id="8d182-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="8d182-140">фиксированного IPv4-адреса для контроллера 0;</span><span class="sxs-lookup"><span data-stu-id="8d182-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="8d182-141">фиксированного IPv4-адреса для контроллера 1.</span><span class="sxs-lookup"><span data-stu-id="8d182-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="8d182-142">Дополнительные сведения об использовании hello этот командлет go слишком[Windows PowerShell для StorSimple Справочник по командлетам](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d182-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d182-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d182-143">Next steps</span></span>
* <span data-ttu-id="8d182-144">tooconfigure сетевые интерфейсы, отличные от DATA 0, могут использовать hello [Настройка параметров сети на портал Azure hello](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="8d182-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure network settings in hello Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="8d182-145">Если возникают проблемы при настройке сетевых интерфейсов, см. слишком[устранения проблем развертывания](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="8d182-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

