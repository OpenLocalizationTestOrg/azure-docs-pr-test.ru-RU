---
title: "перенаправление aaaUsing в Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooconfigure и использование перенаправления для удаленных приложений RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="ac309-103">Использование перенаправления в удаленном приложении Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ac309-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ac309-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="ac309-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ac309-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="ac309-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ac309-106">Перенаправление устройств пользователи могут взаимодействовать с удаленными приложениями с помощью hello устройств вложенного tootheir локального компьютера, телефон или планшет.</span><span class="sxs-lookup"><span data-stu-id="ac309-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="ac309-107">Например при указании Скайп через Azure RemoteApp пользователю необходимо установлен на их ПК toowork с Скайп камеры hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="ac309-108">Это также касается принтеров, динамиков, мониторов и периферийных устройств, подключенных через порт USB.</span><span class="sxs-lookup"><span data-stu-id="ac309-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="ac309-109">RemoteApp использует hello удаленного рабочего стола (RDP) и RemoteFX tooprovide перенаправление.</span><span class="sxs-lookup"><span data-stu-id="ac309-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="ac309-110">Какое перенаправление включено по умолчанию?</span><span class="sxs-lookup"><span data-stu-id="ac309-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="ac309-111">При использовании удаленных приложений RemoteApp, по умолчанию включены следующие перенаправлений hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="ac309-112">сведения Hello в скобках указывают на приветствия протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="ac309-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="ac309-113">Воспроизведение звуков на локальном компьютере hello (**проигрывать на этом компьютере**).</span><span class="sxs-lookup"><span data-stu-id="ac309-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="ac309-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="ac309-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="ac309-115">Запись звука с локального компьютера hello и отправки toohello удаленного компьютера (**записать с этого компьютера**).</span><span class="sxs-lookup"><span data-stu-id="ac309-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="ac309-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="ac309-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="ac309-117">Печать toolocal принтеры (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="ac309-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="ac309-118">COM-порты (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="ac309-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="ac309-119">Устройства чтения смарт-карт (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="ac309-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="ac309-120">Буфер обмена (возможность toocopy и вставить) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="ac309-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="ac309-121">Очистить сглаживания шрифтов (allow font smoothing:i:1)</span><span class="sxs-lookup"><span data-stu-id="ac309-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="ac309-122">Перенаправление всех поддерживаемых самонастраивающихся устройств.</span><span class="sxs-lookup"><span data-stu-id="ac309-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="ac309-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="ac309-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="ac309-124">Какие еще перенаправления доступны?</span><span class="sxs-lookup"><span data-stu-id="ac309-124">What other redirection is available?</span></span>
<span data-ttu-id="ac309-125">Два параметра перенаправления по умолчанию отключены:</span><span class="sxs-lookup"><span data-stu-id="ac309-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="ac309-126">Перенаправление дисков (сопоставление дисков): диски локального компьютера становятся подключенные сетевые диски в удаленном сеансе hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="ac309-127">Это позволяет при сохранении или файлы, открытые на локальных дисках, при работе в удаленном сеансе hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="ac309-128">USB-перенаправления: hello устройства USB вложенного tooyour локального компьютера можно использовать в рамках удаленного сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="ac309-129">Изменение настроек перенаправления в удаленном приложении RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ac309-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="ac309-130">Параметры перенаправления hello устройств для коллекции можно изменить с помощью hello Microsoft Azure PowerShell с помощью пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="ac309-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="ac309-131">После установки hello новый PowerShell и пакет SDK, настроить его toomanage вашей подписки, как описано в [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac309-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="ac309-132">Выполните команду аналогичные toohello, следующие пользовательские свойства протокола удаленного рабочего СТОЛА tooset hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="ac309-133">(Обратите внимание, что  *\`n*  используется в качестве разделителя между отдельными свойствами.)</span><span class="sxs-lookup"><span data-stu-id="ac309-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="ac309-134">tooget список настроены какие настраиваемые свойства протокола удаленного рабочего СТОЛА, запустите следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="ac309-135">Обратите внимание, что только пользовательские свойства отображаются в виде выходных результатов не hello свойства по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="ac309-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="ac309-136">При установке пользовательских свойств необходимо указать все пользовательские свойства каждый раз; в противном случае приветствия возвращается toodisabled.</span><span class="sxs-lookup"><span data-stu-id="ac309-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="ac309-137">Распространенные примеры</span><span class="sxs-lookup"><span data-stu-id="ac309-137">Common examples</span></span>
<span data-ttu-id="ac309-138">Используйте следующий командлет перенаправление дисков tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="ac309-139">Используйте этот командлет tooenable USB и диск перенаправление:</span><span class="sxs-lookup"><span data-stu-id="ac309-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="ac309-140">Используйте этот командлет toodisable совместное использование буфера обмена:</span><span class="sxs-lookup"><span data-stu-id="ac309-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="ac309-141">Быть toocompletely убедиться, что выход из системы всех пользователей в коллекции hello (и не только их отключения) перед началом тестирования изменений hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="ac309-142">Пользователи tooensure полностью вышли из системы, последовательно выберите toohello **сеансы** в коллекции hello в hello портал Azure и выйдите из системы все пользователи, не отключены и не выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="ac309-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="ac309-143">Иногда может потребоваться несколько секунд, tooshow hello локальные диски в проводнике в рамках сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="ac309-144">Изменение настроек перенаправления USB на клиенте Windows</span><span class="sxs-lookup"><span data-stu-id="ac309-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="ac309-145">Следует toouse USB-перенаправления на компьютере, который подключается tooRemoteApp существует 2 действия, которые должны toohappen.</span><span class="sxs-lookup"><span data-stu-id="ac309-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="ac309-146">1 — администратор должен tooenable USB-перенаправления на уровне коллекции hello с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac309-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="ac309-147">2 — на каждом устройстве, где требуется toouse USB-перенаправления необходимо tooenable групповой политики, которая позволяет использовать его.</span><span class="sxs-lookup"><span data-stu-id="ac309-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="ac309-148">Этот шаг потребуется выполнить для каждого пользователя, который хочет toouse USB-перенаправления toobe.</span><span class="sxs-lookup"><span data-stu-id="ac309-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="ac309-149">Перенаправление USB с помощью удаленного приложения Azure RemoteApp поддерживается только на компьютерах под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="ac309-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="ac309-150">Разрешить USB-перенаправления для hello коллекции RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ac309-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="ac309-151">Используйте следующий командлет tooenable USB-перенаправления на уровне коллекции hello hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="ac309-152">Разрешить USB-перенаправления для hello клиентского компьютера</span><span class="sxs-lookup"><span data-stu-id="ac309-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="ac309-153">Параметры перенаправления tooconfigure USB на компьютере:</span><span class="sxs-lookup"><span data-stu-id="ac309-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="ac309-154">Привет открыть редактор локальных групповых политик (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="ac309-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="ac309-155">(Из командной строки запустите команду gpedit.msc.)</span><span class="sxs-lookup"><span data-stu-id="ac309-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="ac309-156">Откройте папку **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span><span class="sxs-lookup"><span data-stu-id="ac309-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="ac309-157">Дважды щелкните **Разрешить перенаправление RDP других поддерживаемых устройств RemoteFX USB на этом компьютере**.</span><span class="sxs-lookup"><span data-stu-id="ac309-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="ac309-158">Выберите **включено**, а затем выберите **администраторов и пользователей в hello права доступа для перенаправления USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="ac309-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="ac309-159">Откройте командную строку с правами администратора и выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ac309-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="ac309-160">Перезагрузите компьютер hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-160">Restart hello computer.</span></span>

<span data-ttu-id="ac309-161">Можно также использовать toocreate средство управления групповой политикой hello и применить политику перенаправления hello USB для всех компьютеров в домене:</span><span class="sxs-lookup"><span data-stu-id="ac309-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="ac309-162">Войдите на контроллер домена hello в качестве администратора домена hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="ac309-163">Здравствуйте, откройте консоль управления групповыми политиками.</span><span class="sxs-lookup"><span data-stu-id="ac309-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="ac309-164">(Щелкните **Пуск > Администрирование > Управление групповой политикой**.)</span><span class="sxs-lookup"><span data-stu-id="ac309-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="ac309-165">Перейдите toohello домен или подразделение, для которого требуется политика toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="ac309-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="ac309-166">Щелкните правой кнопкой мыши **Default Domain Policy** (Политика домена по умолчанию), а затем нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="ac309-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="ac309-167">Откройте папку **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span><span class="sxs-lookup"><span data-stu-id="ac309-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="ac309-168">Дважды щелкните **Разрешить перенаправление RDP других поддерживаемых устройств RemoteFX USB на этом компьютере**.</span><span class="sxs-lookup"><span data-stu-id="ac309-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="ac309-169">Выберите **включено**, а затем выберите **администраторов и пользователей в hello права доступа для перенаправления USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="ac309-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="ac309-170">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ac309-170">Click **OK**.</span></span>  

