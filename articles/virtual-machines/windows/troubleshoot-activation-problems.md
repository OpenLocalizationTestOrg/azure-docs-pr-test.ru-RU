---
title: "Устранение неполадок при активации виртуальных машин Windows в Azure | Документация Майкрософт"
description: "Приводятся действия по устранению неполадок, возникающих при активации виртуальных машин Windows в Azure."
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 77ef396e0bf75fab56bda2e76516b481d018c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="d4f0c-103">Устранение неполадок при активации виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="d4f0c-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d4f0c-104">Если при активации виртуальной машины Windows, созданной из пользовательского образа, в Azure возникли проблемы, то для их устранения можно воспользоваться сведениями, приведенными в этом документе.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use the information provided in this document to troubleshoot the issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="d4f0c-105">Симптом</span><span class="sxs-lookup"><span data-stu-id="d4f0c-105">Symptom</span></span>

<span data-ttu-id="d4f0c-106">При попытке активировать виртуальную машину Windows в Azure появляется сообщение об ошибке примерно такого содержания:</span><span class="sxs-lookup"><span data-stu-id="d4f0c-106">When you try to activate an Azure Windows VM, you receive an error message resembles the following sample:</span></span>

<span data-ttu-id="d4f0c-107">**Ошибка: 0xC004F074 Служба лицензирования программного обеспечения сообщила, что данный компьютер не удалось активировать. Связаться со службой управления ключами (KMS) не удалось. Дополнительные сведения см. в журнале событий приложений.**</span><span class="sxs-lookup"><span data-stu-id="d4f0c-107">**Error: 0xC004F074 The Software LicensingService reported that the computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see the Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="d4f0c-108">Причина:</span><span class="sxs-lookup"><span data-stu-id="d4f0c-108">Cause</span></span>
<span data-ttu-id="d4f0c-109">Как правило, неполадки при активации виртуальной машины в Azure возникают, если виртуальная машина Windows не настроена с помощью подходящего ключа установки клиента KMS, или если возникает проблема при подключении виртуальной машины Windows к службе Azure KMS (kms.core.windows.net, порт 1668).</span><span class="sxs-lookup"><span data-stu-id="d4f0c-109">Generally, Azure VM activation issues occur if the Windows VM is not configured by using the appropriate KMS client setup key, or the Windows VM has a connectivity problem to the Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="d4f0c-110">Решение</span><span class="sxs-lookup"><span data-stu-id="d4f0c-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="d4f0c-111">Если вы используете VPN типа "сайт — сайт" и принудительное туннелирование, то см. запись блога [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) (Использование настраиваемых маршрутов Azure для активации KMS с помощью принудительного туннелирования).</span><span class="sxs-lookup"><span data-stu-id="d4f0c-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="d4f0c-112">Если вы используете ExpressRoute и опубликованный маршрут по умолчанию, то см. запись блога [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx) (Возможен сбой при активации виртуальной машины Azure с помощью ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="d4f0c-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-the-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="d4f0c-113">Шаг 1. Настройка подходящего ключа установки клиента KMS (для Windows Server 2016 и Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="d4f0c-113">Step 1 Configure the appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="d4f0c-114">На виртуальных машинах, созданных из образа Windows Server 2016 или Windows Server 2012 R2, необходимо настроить подходящий ключ установки клиента KMS для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-114">For the VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure the appropriate KMS client setup key for the VM.</span></span>

<span data-ttu-id="d4f0c-115">Этот шаг не применяется в Windows 2012 и Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-115">This step does not apply to Windows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="d4f0c-116">Он использует функцию автоматической активации виртуальных машин (AVMA), которая поддерживается только в Windows Server 2016 и Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-116">It uses the Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="d4f0c-117">В командной строке с повышенными привилегиями выполните команду **slmgr.vbs /dlv**.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="d4f0c-118">В выходных данных проверьте значение Description (Описание), а затем определите, какой носитель лицензии использовался для создания — розничный (канал RETAIL) или корпоративный (VOLUME_KMSCLIENT):</span><span class="sxs-lookup"><span data-stu-id="d4f0c-118">Check the Description value in the output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="d4f0c-119">Если команда **slmgr.vbs /dlv** отображает канал RETAIL, то выполните следующие команды, чтобы задать [ключ установки клиента KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) для используемой версии Windows Server и принудительно повторить активацию:</span><span class="sxs-lookup"><span data-stu-id="d4f0c-119">If **slmgr.vbs /dlv** shows RETAIL channel, run the following commands to set the [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for the version of Windows Server being used, and force it to retry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="d4f0c-120">Например, для Windows Server 2016 Datacenter необходимо выполнить следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4f0c-120">For example, for Windows Server 2016 Datacenter, you would run the following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-the-connectivity-between-the-vm-and-azure-kms-service"></a><span data-ttu-id="d4f0c-121">Шаг 2. Проверка сетевого подключения между виртуальной машиной и службой Azure KMS</span><span class="sxs-lookup"><span data-stu-id="d4f0c-121">Step 2 Verify the connectivity between the VM and Azure KMS service</span></span>

1. <span data-ttu-id="d4f0c-122">Скачайте инструмент [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) и извлеките его в локальную папку на виртуальной машине, которую не удается активировать.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-122">Download and extract the [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool to a local folder in the VM that does not activate.</span></span> 

2. <span data-ttu-id="d4f0c-123">Перейдите в меню "Пуск", найдите и щелкните правой кнопкой мыши Windows PowerShell, а затем выберите "Запуск от имени администратора".</span><span class="sxs-lookup"><span data-stu-id="d4f0c-123">Go to Start, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="d4f0c-124">Убедитесь, что в настройках виртуальной машины указан правильный сервер Azure KMS.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-124">Make sure that the VM is configured to use the correct Azure KMS server.</span></span> <span data-ttu-id="d4f0c-125">Для этого выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4f0c-125">To do this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="d4f0c-126">Команда должна вернуть такие данные: "Задано имя компьютера со службой управления ключами: kms.core.windows.net:1688".</span><span class="sxs-lookup"><span data-stu-id="d4f0c-126">The command should return: Key Management Service machine name set to kms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="d4f0c-127">С помощью Psping проверьте наличие подключения к серверу KMS.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-127">Verify by using Psping that you have connectivity to the KMS server.</span></span> <span data-ttu-id="d4f0c-128">Перейдите в папку, в которую был извлечен архив Pstools.zip, а затем выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d4f0c-128">Switch to the folder where you extracted the Pstools.zip download, and then run the following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="d4f0c-129">В предпоследней строке выходных данных должно отобразиться следующее: "отправлено = 4, получено = 4, потеряно = 0 (0% потерь)".</span><span class="sxs-lookup"><span data-stu-id="d4f0c-129">In the second-to-last line of the output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="d4f0c-130">Если значение "потеряно" больше ноля, то это значит, что виртуальная машина не имеет подключения к серверу KMS.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-130">If Lost is greater than 0 (zero), the VM does not have connectivity to the KMS server.</span></span> <span data-ttu-id="d4f0c-131">В такой ситуации, если виртуальная машина находится в виртуальной сети и указан пользовательский DNS-сервер, необходимо убедиться, что DNS-сервер способен разрешать адрес kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-131">In this situation, if the VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able to resolve kms.core.windows.net.</span></span> <span data-ttu-id="d4f0c-132">Или укажите такой DNS-сервер, который точно разрешает kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-132">Or, change the DNS server to one that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="d4f0c-133">Обратите внимание, что при удалении из виртуальной сети всех DNS-серверов виртуальные машины используют внутреннюю службу DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="d4f0c-134">Эта служба может разрешать kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="d4f0c-135">Проверьте также, чтобы в гостевом брандмауэре не была настроена блокировка попыток активации.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-135">Also verify that the guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="d4f0c-136">После успешной проверки подключения к kms.core.windows.net выполните в командной строке с повышенными привилегиями Windows PowerShell следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-136">After you verify successful connectivity to kms.core.windows.net, run the following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="d4f0c-137">Эта команда пытается выполнить активацию несколько раз.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="d4f0c-138">Успешная попытка активации возвращает сведения, которые выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d4f0c-138">A successful activation returns information that resembles the following:</span></span>

<span data-ttu-id="d4f0c-139">**Активация Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Активация выполнена успешно.**</span><span class="sxs-lookup"><span data-stu-id="d4f0c-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="d4f0c-140">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="d4f0c-140">FAQ</span></span> 

### <a name="i-created-the-windows-server-2016-from-azure-marketplace-do-i-need-to-configure-kms-key-for-activating-the-windows-server-2016"></a><span data-ttu-id="d4f0c-141">Я создал Windows Server 2016 из Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-141">I created the Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="d4f0c-142">Нужно ли настраивать ключ KMS для активации Windows Server 2016?</span><span class="sxs-lookup"><span data-stu-id="d4f0c-142">Do I need to configure KMS key for activating the Windows Server 2016?</span></span> 
 
<span data-ttu-id="d4f0c-143">Нет.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-143">No.</span></span> <span data-ttu-id="d4f0c-144">В образе из Azure Marketplace уже настроен подходящий ключ установки клиента KMS.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-144">The image in Azure Marketplace has the appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-the-same-way-regardless-if-the-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="d4f0c-145">Процедура активации Windows будет такой же, если виртуальная машина использует программу преимуществ гибридного использования (HUB) Azure?</span><span class="sxs-lookup"><span data-stu-id="d4f0c-145">Does Windows activation work the same way regardless if the VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="d4f0c-146">Да.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="d4f0c-147">Что произойдет, если истечет период активации Windows?</span><span class="sxs-lookup"><span data-stu-id="d4f0c-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="d4f0c-148">Если льготный период истек, а ОС Windows еще не активирована, то в Windows Server 2008 R2 и более поздних версиях Windows отобразятся дополнительные уведомления об активации.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-148">When the grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="d4f0c-149">Фоновый рисунок рабочего стола будет оставаться черным, а Центр обновления Windows будет устанавливать только обновления системы безопасности и критические обновления без возможности установить необязательные обновления.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-149">The desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="d4f0c-150">Ознакомьтесь с разделом "Notifications" (Уведомления) в нижней части страницы [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) (Условия лицензирования).</span><span class="sxs-lookup"><span data-stu-id="d4f0c-150">See  the Notifications section at the bottom of the [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="d4f0c-151">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="d4f0c-151">Need help?</span></span> <span data-ttu-id="d4f0c-152">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-152">Contact support.</span></span>
<span data-ttu-id="d4f0c-153">Если вам все еще нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="d4f0c-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>