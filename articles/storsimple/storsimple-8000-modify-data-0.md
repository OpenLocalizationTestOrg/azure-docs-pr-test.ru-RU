---
title: "Изменение параметров DATA 0 на устройстве StorSimple серии 8000 | Документация Майкрософт"
description: "Узнайте, как перенастроить сетевой интерфейс DATA 0 на устройстве StorSimple с помощью Windows PowerShell для StorSimple."
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
ms.openlocfilehash: 90df43e22f17fd32fe642514df098b72700e77af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="b2886-103">Изменение параметров сетевого интерфейса DATA 0 на устройстве StorSimple серии 8000</span><span class="sxs-lookup"><span data-stu-id="b2886-103">Modify the DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="b2886-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b2886-104">Overview</span></span>

<span data-ttu-id="b2886-105">Устройство Microsoft Azure StorSimple имеет шесть сетевых интерфейсов, от DATA 0 до DATA 5.</span><span class="sxs-lookup"><span data-stu-id="b2886-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="b2886-106">Интерфейс DATA 0 всегда настраивается с помощью интерфейса Windows PowerShell или последовательной консоли и располагает автоматическим подключением к облаку.</span><span class="sxs-lookup"><span data-stu-id="b2886-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="b2886-107">Обратите внимание на то, что сетевой интерфейс DATA 0 невозможно настроить через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b2886-107">Note that you cannot configure DATA 0 network interface through the Azure portal.</span></span>

<span data-ttu-id="b2886-108">Интерфейс DATA 0 изначально настраивается через мастер установки во время первоначального развертывания устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b2886-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="b2886-109">Если устройство находится в рабочем режиме, может потребоваться перенастроить параметры DATA 0.</span><span class="sxs-lookup"><span data-stu-id="b2886-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="b2886-110">В этом учебнике приведены два метода изменения сетевых параметров DATA 0. В обоих используется Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b2886-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="b2886-111">После изучения этого учебника вы сможете сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="b2886-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="b2886-112">Изменить сетевые параметры DATA 0 с помощью мастера установки.</span><span class="sxs-lookup"><span data-stu-id="b2886-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="b2886-113">Изменить сетевые параметры DATA 0 с помощью командлета `Set-HcsNetInterface` .</span><span class="sxs-lookup"><span data-stu-id="b2886-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="b2886-114">Изменение сетевых параметров DATA 0 с помощью мастера установки</span><span class="sxs-lookup"><span data-stu-id="b2886-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="b2886-115">Можно перенастроить сетевые параметры DATA 0 путем подключения к интерфейсу Windows PowerShell устройства StorSimple и запуска сеанса мастера установки.</span><span class="sxs-lookup"><span data-stu-id="b2886-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="b2886-116">Чтобы изменить параметры DATA 0, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b2886-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="b2886-117">Изменение сетевых параметров DATA 0 с помощью мастера установки</span><span class="sxs-lookup"><span data-stu-id="b2886-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="b2886-118">В меню последовательной консоли выберите вариант 1 **Войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="b2886-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="b2886-119">При выводе запроса введите **пароль администратора устройства**.</span><span class="sxs-lookup"><span data-stu-id="b2886-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="b2886-120">Пароль по умолчанию: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="b2886-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="b2886-121">В командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b2886-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="b2886-122">Отобразится мастер установки, который поможет настроить интерфейс DATA 0 устройства.</span><span class="sxs-lookup"><span data-stu-id="b2886-122">A setup wizard appears to help configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="b2886-123">Введите новые значения для IP-адреса, шлюза и маски подсети.</span><span class="sxs-lookup"><span data-stu-id="b2886-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="b2886-124">Фиксированные IP-адреса контроллеров необходимо будет перенастроить в колонке **Параметры сети** устройства StorSimple на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b2886-124">The fixed controllers IPs will need to be reconfigured through the **Network settings** blade of the StorSimple device in the Azure portal.</span></span> <span data-ttu-id="b2886-125">Дополнительные сведения см. в статье [Изменение сетевых интерфейсов](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="b2886-125">For more information, go to [Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="b2886-126">Изменение сетевых параметров DATA 0 с помощью командлета Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="b2886-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="b2886-127">Альтернативный способ перенастроить сетевой интерфейс DATA 0 — воспользоваться командлетом `Set-HcsNetInterface` .</span><span class="sxs-lookup"><span data-stu-id="b2886-127">An alternate way to reconfigure DATA 0 network interface is through the use of the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="b2886-128">Командлет выполняется из интерфейса Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b2886-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="b2886-129">При использовании этой процедуры здесь также можно настроить статические IP-адреса контроллера.</span><span class="sxs-lookup"><span data-stu-id="b2886-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="b2886-130">Чтобы изменить параметры DATA 0, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b2886-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="b2886-131">Изменение сетевых параметров DATA 0 с помощью командлета Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="b2886-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="b2886-132">В меню последовательной консоли выберите вариант 1 **Войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="b2886-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="b2886-133">При выводе запроса введите пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="b2886-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="b2886-134">Пароль по умолчанию: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="b2886-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="b2886-135">В командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b2886-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="b2886-136">В угловых скобках введите следующие значения для DATA 0:</span><span class="sxs-lookup"><span data-stu-id="b2886-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="b2886-137">IPv4-адреса;</span><span class="sxs-lookup"><span data-stu-id="b2886-137">IPv4 address</span></span>
   * <span data-ttu-id="b2886-138">шлюза IPv4;</span><span class="sxs-lookup"><span data-stu-id="b2886-138">IPv4 gateway</span></span>
   * <span data-ttu-id="b2886-139">маски подсети IPv4;</span><span class="sxs-lookup"><span data-stu-id="b2886-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="b2886-140">фиксированного IPv4-адреса для контроллера 0;</span><span class="sxs-lookup"><span data-stu-id="b2886-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="b2886-141">фиксированного IPv4-адреса для контроллера 1.</span><span class="sxs-lookup"><span data-stu-id="b2886-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="b2886-142">Дополнительные сведения об использовании этого командлета см. в [справочнике по командлетам Windows PowerShell для StorSimple](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2886-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2886-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b2886-143">Next steps</span></span>
* <span data-ttu-id="b2886-144">Сетевые интерфейсы, отличные от DATA 0, можно [настроить на портале Azure](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="b2886-144">To configure network interfaces other than DATA 0, you can use the [Configure network settings in the Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="b2886-145">Если у вас возникли проблемы при настройке сетевых интерфейсов, см. статью [Устранение неполадок в развертывании устройства StorSimple](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="b2886-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

