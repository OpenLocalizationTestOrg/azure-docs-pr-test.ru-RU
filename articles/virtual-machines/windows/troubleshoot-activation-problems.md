---
title: "aaaTroubleshoot проблемы активации виртуальной машины Windows в Azure | Документы Microsoft"
description: "Предоставляет hello устранения шаги по устранению неполадок активации виртуальной машины Windows в Azure"
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
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="119eb-103">Устранение неполадок при активации виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="119eb-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="119eb-104">Если возникли проблемы при активации Azure Windows виртуальной машины (VM), созданной из образа, можно использовать hello сведения, представленные в этом выпуске hello tootroubleshoot документа.</span><span class="sxs-lookup"><span data-stu-id="119eb-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="119eb-105">Симптом</span><span class="sxs-lookup"><span data-stu-id="119eb-105">Symptom</span></span>

<span data-ttu-id="119eb-106">При попытке tooactivate ВМ Windows Azure, появляется сообщение об ошибке сообщений напоминает следующий образец hello:</span><span class="sxs-lookup"><span data-stu-id="119eb-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="119eb-107">**Ошибка: hello 0xC004F074 LicensingService программного обеспечения сообщила, что не удалось активировать этот компьютер hello. Связаться со службой управления ключами (KMS) не удалось. См. в разделе hello журнал событий приложений для получения дополнительных сведений.**</span><span class="sxs-lookup"><span data-stu-id="119eb-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="119eb-108">Причина:</span><span class="sxs-lookup"><span data-stu-id="119eb-108">Cause</span></span>
<span data-ttu-id="119eb-109">Обычно проблемами активации виртуальной Машины Azure выполняться Если hello виртуальной Машины Windows не настроен с помощью hello соответствующий ключ установки клиента KMS или виртуальной Машине Windows hello имеет toohello проблемы подключения службы Azure KMS (kms.core.windows.net, порт 1668).</span><span class="sxs-lookup"><span data-stu-id="119eb-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="119eb-110">Решение</span><span class="sxs-lookup"><span data-stu-id="119eb-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="119eb-111">Если используется сеть сеть VPN и принудительного туннелирования, в разделе [пользовательские используйте Azure направляет tooenable активации KMS с помощью принудительного туннелирования](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="119eb-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="119eb-112">Если вы используете ExpressRoute и опубликован маршрут по умолчанию см. в разделе [ВМ Azure может завершиться ошибкой tooactivate по ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="119eb-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="119eb-113">Шаг 1 Настройка hello соответствующий ключ установки клиента KMS (для Windows Server 2016 и Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="119eb-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="119eb-114">Для hello виртуальной Машины, которая создается на основе пользовательского образа Windows Server 2016 или Windows Server 2012 R2 необходимо настроить hello соответствующий ключ установки клиента KMS для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="119eb-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="119eb-115">Этот шаг не применяется tooWindows 2012 или Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="119eb-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="119eb-116">Она использует функции hello автоматизации активации виртуальной машины (AVMA), которая поддерживается только Windows Server 2016 и Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="119eb-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="119eb-117">В командной строке с повышенными привилегиями выполните команду **slmgr.vbs /dlv**.</span><span class="sxs-lookup"><span data-stu-id="119eb-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="119eb-118">Проверьте значение описания в выходных данных hello hello и определить, является ли он был создан из розничной торговли (РОЗНИЧНОГО канала) или корпоративного (VOLUME_KMSCLIENT) лицензирования:</span><span class="sxs-lookup"><span data-stu-id="119eb-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="119eb-119">Если **slmgr.vbs/dlv** показывает РОЗНИЧНОГО канала, запустите следующие команды tooset hello hello [ключ установки клиента KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) используется для hello версии Windows Server и заставить его tooretry активации:</span><span class="sxs-lookup"><span data-stu-id="119eb-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="119eb-120">Например для Windows Server 2016 центра обработки данных, нужно будет выполнить hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="119eb-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="119eb-121">Шаг 2 Проверьте hello соединение между hello виртуальной Машины и службы Azure KMS</span><span class="sxs-lookup"><span data-stu-id="119eb-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="119eb-122">Загрузите и извлеките hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) средство tooa локальную папку в виртуальной Машине, которая не активирует hello.</span><span class="sxs-lookup"><span data-stu-id="119eb-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="119eb-123">Go tooStart, поиск на основе Windows PowerShell, щелкните правой кнопкой мыши Windows PowerShell и затем выберите Запуск от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="119eb-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="119eb-124">Убедитесь, что этой hello ВМ настроен правильный сервер Azure KMS toouse hello.</span><span class="sxs-lookup"><span data-stu-id="119eb-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="119eb-125">toodo это, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="119eb-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="119eb-126">Команда Hello должен возвращать: tookms.core.windows.net:1688 успешно установлено на имя компьютера службы управления ключами.</span><span class="sxs-lookup"><span data-stu-id="119eb-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="119eb-127">Проверьте с помощью Psping, наличие сервера службы KMS toohello подключения.</span><span class="sxs-lookup"><span data-stu-id="119eb-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="119eb-128">Переключение toohello папку, которую было извлечено hello Pstools.zip загрузки, а затем запустите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="119eb-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="119eb-129">В секунду за последней строку hello hello выходные данные, убедитесь, что вы видите: отправлено = 4, получено = 4, потеряно = 0 (0% потерь).</span><span class="sxs-lookup"><span data-stu-id="119eb-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="119eb-130">Если потерянные больше 0 (ноль), hello виртуальной Машины отсутствует сервер KMS toohello подключения.</span><span class="sxs-lookup"><span data-stu-id="119eb-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="119eb-131">В этом случае если hello виртуальная машина находится в виртуальной сети и имеет пользовательского DNS-сервера указан, убедитесь, что DNS-сервер является может tooresolve kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="119eb-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="119eb-132">Или измените hello DNS server tooone, разрешить kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="119eb-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="119eb-133">Обратите внимание, что при удалении из виртуальной сети всех DNS-серверов виртуальные машины используют внутреннюю службу DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="119eb-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="119eb-134">Эта служба может разрешать kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="119eb-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="119eb-135">Также убедитесь, что гостевой брандмауэром, hello не был настроен таким образом, чтобы заблокирует попытки активации.</span><span class="sxs-lookup"><span data-stu-id="119eb-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="119eb-136">После проверки успешного подключения tookms.core.windows.net, выполните следующую команду в этой строке с повышенными привилегиями Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="119eb-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="119eb-137">Эта команда пытается выполнить активацию несколько раз.</span><span class="sxs-lookup"><span data-stu-id="119eb-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="119eb-138">Успешной активации возвращает сведения, аналогичные hello ниже:</span><span class="sxs-lookup"><span data-stu-id="119eb-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="119eb-139">**Активация Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Активация выполнена успешно.**</span><span class="sxs-lookup"><span data-stu-id="119eb-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="119eb-140">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="119eb-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="119eb-141">Я создал hello Windows Server 2016 из Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="119eb-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="119eb-142">Зачем мне tooconfigure ключ KMS для активации hello Windows Server 2016?</span><span class="sxs-lookup"><span data-stu-id="119eb-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="119eb-143">Нет.</span><span class="sxs-lookup"><span data-stu-id="119eb-143">No.</span></span> <span data-ttu-id="119eb-144">изображение Hello в Azure Marketplace имеет hello соответствующий ключ установки клиента KMS уже настроен.</span><span class="sxs-lookup"><span data-stu-id="119eb-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="119eb-145">Рабочих активации Windows hello одинаково независимо от того, каким образом Если hello виртуальная машина использует преимущество использования гибридной Azure (HUB) или нет?</span><span class="sxs-lookup"><span data-stu-id="119eb-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="119eb-146">Да.</span><span class="sxs-lookup"><span data-stu-id="119eb-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="119eb-147">Что произойдет, если истечет период активации Windows?</span><span class="sxs-lookup"><span data-stu-id="119eb-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="119eb-148">Если hello льготный период уже истек, и по-прежнему не будет выполнена, Windows Server 2008 R2 и более поздних версиях Windows будут выведены дополнительные уведомления об активации.</span><span class="sxs-lookup"><span data-stu-id="119eb-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="119eb-149">Hello стола остается черным, а установит обновления Windows, безопасности и только критические обновления, но не необязательные обновления.</span><span class="sxs-lookup"><span data-stu-id="119eb-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="119eb-150">Видеть уведомления hello раздела внизу hello hello [условия лицензирования](http://technet.microsoft.com/en-us/library/ff793403.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="119eb-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="119eb-151">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="119eb-151">Need help?</span></span> <span data-ttu-id="119eb-152">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="119eb-152">Contact support.</span></span>
<span data-ttu-id="119eb-153">Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="119eb-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
