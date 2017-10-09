---
title: "aaaAccessing приложений с любого устройства | Документы Microsoft"
description: "Узнайте, какие клиенты поддерживаются для Azure RemoteApp и как tooaccess приложений."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 15985b40d870e3155d4132063bf5b9677ff9afed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="5b465-103">Доступ к приложениям в Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5b465-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5b465-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="5b465-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5b465-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="5b465-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5b465-106">Одно из преимуществ hello среды Azure RemoteApp — что можно доступа к приложениям с любого устройства.</span><span class="sxs-lookup"><span data-stu-id="5b465-106">One of hello beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="5b465-107">Более того можно приступить к работе на одном устройстве и безупречно проводить tooa второго устройства и начнется с места остановки.</span><span class="sxs-lookup"><span data-stu-id="5b465-107">Even better, you can start working on one device and then seamlessly transition tooa second device and pick up right where you left off.</span></span> <span data-ttu-id="5b465-108">tooget работы, вы должны toodownload hello соответствующего клиента для устройства и войти в службе toohello.</span><span class="sxs-lookup"><span data-stu-id="5b465-108">tooget started you need toodownload hello appropriate client for your device and sign in toohello service.</span></span>

<span data-ttu-id="5b465-109">В этом разделе мы рассмотрим hello клиентов, поддерживаемых и как toodownload их до я покажу, как toosign в tooRemoteApp в каждом из клиентов hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-109">In this topic, we'll review hello clients currently supported and how toodownload them before I show you how toosign in tooRemoteApp from each of hello clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="5b465-110">Поддерживаемые клиенты</span><span class="sxs-lookup"><span data-stu-id="5b465-110">Supported clients</span></span>
<span data-ttu-id="5b465-111">Можно получить доступ к приложениям RemoteApp с помощью hello шаги, если устройство работает под управлением одной из этих операционных систем:</span><span class="sxs-lookup"><span data-stu-id="5b465-111">You can access RemoteApp using hello steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="5b465-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="5b465-112">Windows 10</span></span> 
* <span data-ttu-id="5b465-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="5b465-113">Windows 8.1</span></span>
* <span data-ttu-id="5b465-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="5b465-114">Windows 8</span></span>
* <span data-ttu-id="5b465-115">Windows 7 с пакетом обновления 1</span><span class="sxs-lookup"><span data-stu-id="5b465-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="5b465-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="5b465-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="5b465-117">iOS</span><span class="sxs-lookup"><span data-stu-id="5b465-117">iOS</span></span>
* <span data-ttu-id="5b465-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="5b465-118">Mac OS X</span></span>
* <span data-ttu-id="5b465-119">Android</span><span class="sxs-lookup"><span data-stu-id="5b465-119">Android</span></span>

 <span data-ttu-id="5b465-120">Как насчет тонких клиентов? поддерживаются следующие тонких клиентов Windows Embedded Hello:</span><span class="sxs-lookup"><span data-stu-id="5b465-120">What about thin clients? hello following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="5b465-121">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="5b465-121">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="5b465-122">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="5b465-122">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="5b465-123">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="5b465-123">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="5b465-124">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="5b465-124">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-hello-client"></a><span data-ttu-id="5b465-125">Загрузка приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="5b465-125">Downloading hello client</span></span>
<span data-ttu-id="5b465-126">Требуется tooaccess RemoteApp можно найти на приветствия клиента hello, независимо от того, какие платформы используется [загрузки клиента удаленного рабочего стола](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="5b465-126">No matter what platform you are using, hello client you need tooaccess RemoteApp can be found on hello [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="5b465-127">Щелкните ссылки различных hello либо непосредственно начнется загрузка hello клиента или отправит вам toohello страницы скачивания клиента в хранилище приложения hello для данной платформы.</span><span class="sxs-lookup"><span data-stu-id="5b465-127">Clicking hello different links will either directly start downloading hello client or will send you toohello client download page in hello app store for that platform.</span></span> <span data-ttu-id="5b465-128">Установите клиент hello, следуя инструкциям hello на экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="5b465-128">Install hello client by following hello instructions on hello screen.</span></span>

<span data-ttu-id="5b465-129">После установки клиента hello на устройстве и запустить его, как выполняется переход toohello соответствующий раздел ниже toolearn toosign в tooRemoteApp из этого клиента.</span><span class="sxs-lookup"><span data-stu-id="5b465-129">Once you have installed hello client on your device and launched it, jump toohello corresponding section below toolearn how toosign in tooRemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="5b465-130">Android</span><span class="sxs-lookup"><span data-stu-id="5b465-130">Android</span></span>
<span data-ttu-id="5b465-131">После установки приложение hello удаленный рабочий стол Майкрософт из магазина Google Play hello, его можно будет найти в списке приложений под **удаленного рабочего стола**.</span><span class="sxs-lookup"><span data-stu-id="5b465-131">Once you have installed hello Microsoft Remote Desktop app from hello Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="5b465-132">При запуске приложение hello переводит tooan пустой Центр подключений, если только уже использовалось приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-132">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="5b465-133">tooget работы с Azure RemoteApp, tap hello кнопка "Добавить" **««+»»** и коснитесь **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="5b465-133">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Пустой центр подключений](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="5b465-135">Необходимо toosign вход с помощью службы hello tooaccess адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="5b465-135">You need toosign in with your email address tooaccess hello service.</span></span> <span data-ttu-id="5b465-136">Нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="5b465-136">Tap **Get started**.</span></span>
   
    ![Приглашение войти](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="5b465-138">На следующей странице hello, введите в вашей **адрес электронной почты** и коснитесь **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="5b465-138">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="5b465-139">Это начинает hello процесса входа с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b465-139">This begins hello sign-in process using Azure Active Directory.</span></span>
   
    ![Первая страница Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="5b465-141">Следуйте инструкциям hello на toosign экрана приветствия вход с вашей учетной записи Майкрософт (ранее называвшиеся «LiveID») или идентификатор организации.</span><span class="sxs-lookup"><span data-stu-id="5b465-141">Follow hello instructions on hello screen toosign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="5b465-142">После входа может быть предложен страницы со списком всех приглашений hello полученные.</span><span class="sxs-lookup"><span data-stu-id="5b465-142">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="5b465-143">Пользователям, выберите приглашения hello доверия и коснитесь **сделать**.</span><span class="sxs-lookup"><span data-stu-id="5b465-143">If you are, select hello invitations you trust and tap **Done**.</span></span>    
   
    ![Страница с приглашениями](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="5b465-145">После принятия вашего приглашения, hello список приложений, имеют доступ toowill загруженный tooyour устройством и становятся доступными в hello Центр подключений.</span><span class="sxs-lookup"><span data-stu-id="5b465-145">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="5b465-146">Выберите один из его использованием toostart приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-146">Tap one of hello apps toostart using it.</span></span>
   
    ![Центр подключений с веб-каналом](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="5b465-148">Если приглашение еще нет, можно по-прежнему опробовать службу hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-148">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="5b465-149">Таким образом, коснитесь toodo **Go пробной версии toofree** при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="5b465-149">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Приглашение к использованию демонстрационного веб-канала](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="5b465-151">Это позволит получить доступ к tooa базовый набор приложений tooget работы с RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5b465-151">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="5b465-153">iOS</span><span class="sxs-lookup"><span data-stu-id="5b465-153">iOS</span></span>
<span data-ttu-id="5b465-154">После установки приложение hello удаленный рабочий стол Майкрософт из магазина приложений hello, его можно будет найти в списке приложений под **клиента удаленных рабочих Столов**.</span><span class="sxs-lookup"><span data-stu-id="5b465-154">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="5b465-155">При запуске приложение hello переводит tooan пустой Центр подключений, если только уже использовалось приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-155">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="5b465-156">tooget работы с Azure RemoteApp, tap hello кнопка "Добавить" **««+»»** и коснитесь **добавьте Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="5b465-156">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Пустой центр подключений](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="5b465-158">Требуется toosign вход с помощью службы hello tooaccess адрес электронной почты, toostart этого процесса типа в вашей **адрес электронной почты** и коснитесь **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="5b465-158">You need toosign in with your email address tooaccess hello service, toostart that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Приглашение войти](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="5b465-160">Следуйте инструкциям hello на toosign экрана приветствия вход с учетной записью Майкрософт (LiveID) или идентификатор организации.</span><span class="sxs-lookup"><span data-stu-id="5b465-160">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="5b465-161">После входа может быть предложен страницы со списком всех приглашений hello полученные.</span><span class="sxs-lookup"><span data-stu-id="5b465-161">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="5b465-162">Пользователям, выберите приглашения hello доверия и коснитесь **сделать**.</span><span class="sxs-lookup"><span data-stu-id="5b465-162">If you are, select hello invitations you trust and tap **Done**.</span></span>
   
    ![Страница с приглашениями](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="5b465-164">После принятия вашего приглашения, hello список приложений, имеют доступ toowill загруженный tooyour устройством и становятся доступными в hello Центр подключений.</span><span class="sxs-lookup"><span data-stu-id="5b465-164">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="5b465-165">Коснитесь одного из приложений toolaunch hello ее и начать его использование.</span><span class="sxs-lookup"><span data-stu-id="5b465-165">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Центр подключений с веб-каналом](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="5b465-167">Если приглашение еще нет, можно по-прежнему опробовать службу hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-167">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="5b465-168">Таким образом, коснитесь toodo **Go пробной версии toofree** при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="5b465-168">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Приглашение к использованию демонстрационного веб-канала](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="5b465-170">Это позволит получить доступ к tooa базовый набор приложений tooget работы с RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5b465-170">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="5b465-172">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="5b465-172">Mac OS X</span></span>
<span data-ttu-id="5b465-173">После установки приложение hello удаленный рабочий стол Майкрософт из магазина приложений hello, его можно будет найти в списке приложений под **удаленный рабочий стол Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="5b465-173">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="5b465-174">При запуске приложение hello переводит tooan пустой Центр подключений, если только уже использовалось приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-174">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="5b465-175">tooget работы с Azure RemoteApp щелкните hello **Azure RemoteApp** кнопки.</span><span class="sxs-lookup"><span data-stu-id="5b465-175">tooget started with Azure RemoteApp, click hello **Azure RemoteApp** button.</span></span>
   
    ![Пустой центр подключений](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="5b465-177">Требуется toosign вход с помощью службы hello tooaccess адрес электронной почты, toostart, что процесс, коснитесь **начать**.</span><span class="sxs-lookup"><span data-stu-id="5b465-177">You need toosign in with your email address tooaccess hello service, toostart that process, tap **Get Started**.</span></span>
   
    ![Приглашение войти](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="5b465-179">На следующей странице hello, введите в вашей **адрес электронной почты** и коснитесь **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="5b465-179">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="5b465-180">Это действие запустит hello входа в систему, с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b465-180">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Первая страница Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="5b465-182">Следуйте инструкциям hello на toosign экрана приветствия вход с учетной записью Майкрософт (LiveID) или идентификатор организации.</span><span class="sxs-lookup"><span data-stu-id="5b465-182">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="5b465-183">После входа может быть предложен страницы со списком всех приглашений hello полученные.</span><span class="sxs-lookup"><span data-stu-id="5b465-183">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="5b465-184">Если вы являетесь выберите приглашения hello доверия и закрыть диалоговое окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="5b465-184">If you are, select hello invitations you trust and close hello dialog.</span></span>
   
    ![Страница с приглашениями](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="5b465-186">После принятия вашего приглашения, hello список приложений, имеют доступ toowill загруженный tooyour устройством и становятся доступными в hello Центр подключений.</span><span class="sxs-lookup"><span data-stu-id="5b465-186">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="5b465-187">Дважды щелкните одну из toolaunch приложения hello ее и начать его использование.</span><span class="sxs-lookup"><span data-stu-id="5b465-187">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Центр подключений с веб-каналом](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="5b465-189">Если приглашение еще нет, можно по-прежнему опробовать службу hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-189">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="5b465-190">toodo таким образом, нажмите кнопку **Go пробной версии toofree** при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="5b465-190">toodo so, click **Go toofree trial** when prompted.</span></span>
   
    ![Приглашение к использованию демонстрационного веб-канала](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="5b465-192">Это позволит получить доступ к tooa базовый набор приложений tooget работы с RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5b465-192">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="5b465-194">Windows (все поддерживаемые версии, кроме Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="5b465-194">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="5b465-195">Hello клиент запустится автоматически после завершения установки, однако при необходимости tooaccess его позже его можно найти в списке приложений под именем hello **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="5b465-195">hello client launches automatically after it finishes installing, however when you need tooaccess it again later it can be found in your app list under hello name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="5b465-196">Озже запуска клиента hello, отображается первая страница hello приветствует любые tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5b465-196">Ater launching hello client, hello first page you see welcomes you tooAzure RemoteApp.</span></span> <span data-ttu-id="5b465-197">tooproceed, если щелкнуть **начать**.</span><span class="sxs-lookup"><span data-stu-id="5b465-197">tooproceed, click on **Get Started**.</span></span>
   
    ![Страница приветствия клиента hello Azure RemoteApp](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="5b465-199">следующую страницу приветствия запускается в процессе входа hello Azure RemoteApp с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b465-199">hello next page starts hello sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="5b465-200">Этот процесс должна быть знакома, при использовании служб Майкрософт в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-200">This process should look familiar if you have used Microsoft services in hello past.</span></span> <span data-ttu-id="5b465-201">Введите свой **адрес электронной почты** и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="5b465-201">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Первая страница с приглашением к использованию Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="5b465-203">Следуйте инструкциям hello на toosign экрана приветствия вход с учетной записью Майкрософт (LiveID) или идентификатор организации.</span><span class="sxs-lookup"><span data-stu-id="5b465-203">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="5b465-204">После входа может быть предложен страницы со списком всех приглашений hello полученные.</span><span class="sxs-lookup"><span data-stu-id="5b465-204">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="5b465-205">Пользователям, выберите приглашения hello доверять и нажмите кнопку **сделать**.</span><span class="sxs-lookup"><span data-stu-id="5b465-205">If you are, select hello invitations you trust and click **Done**.</span></span>
   
    ![Приглашения на странице клиента hello Azure RemoteApp](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="5b465-207">После принятия вашего приглашения, hello список приложений, имеют доступ toowill загруженный tooyour устройством и становятся доступными в hello Центр подключений.</span><span class="sxs-lookup"><span data-stu-id="5b465-207">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="5b465-208">Дважды щелкните одну из toolaunch приложения hello ее и начать его использование.</span><span class="sxs-lookup"><span data-stu-id="5b465-208">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Центр подключений клиента hello Azure RemoteApp](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="5b465-210">Если вы не получили ни одного приглашения, не беспокойтесь, скоро вам их отправят.</span><span class="sxs-lookup"><span data-stu-id="5b465-210">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="5b465-211">У вас будет по-прежнему коллекции Демонстрация tooa доступа, которые позволяют тестировать службу hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-211">You'll still have access tooa demo collection so you can test out hello service.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="5b465-213">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="5b465-213">Windows Phone 8.1</span></span>
<span data-ttu-id="5b465-214">После установки приложение hello удаленный рабочий стол Майкрософт из магазина Windows Phone 8.1 hello, его можно будет найти в списке приложений под **удаленного рабочего стола**.</span><span class="sxs-lookup"><span data-stu-id="5b465-214">Once you have installed hello Microsoft Remote Desktop app from hello Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="5b465-215">При запуске приложение hello обеспечивает высокую непосредственно tooan пустой Центр подключений, если только уже использовалось приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-215">Launching hello app brings you directly tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="5b465-216">tooget работы с Azure RemoteApp, tap hello кнопка "Добавить" **««+»»** hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="5b465-216">tooget started with Azure RemoteApp, tap hello add button **""+""** at hello bottom of hello screen.</span></span>
   
    ![Пустой центр подключений](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="5b465-218">Затем выберите элемент **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="5b465-218">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Страница с элементом "добавить"](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="5b465-220">Требуется toosign вход с помощью службы hello tooaccess адрес электронной почты, toostart, что процесс, коснитесь **подключения**.</span><span class="sxs-lookup"><span data-stu-id="5b465-220">You need toosign in with your email address tooaccess hello service, toostart that process, tap **connect**.</span></span>
   
    ![Приглашение войти](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="5b465-222">На следующей странице hello, введите в вашей **адрес электронной почты** и коснитесь **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="5b465-222">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="5b465-223">Это действие запустит hello входа в систему, с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b465-223">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Первая страница Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="5b465-225">Следуйте инструкциям hello на toosign экрана приветствия вход с учетной записью Майкрософт (LiveID) или идентификатор организации.</span><span class="sxs-lookup"><span data-stu-id="5b465-225">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="5b465-226">После входа может быть предложен страницы со списком всех приглашений hello полученные.</span><span class="sxs-lookup"><span data-stu-id="5b465-226">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="5b465-227">Пользователям, выберите приглашения hello доверия и коснитесь **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5b465-227">If you are, select hello invitations you trust and tap **save**.</span></span>
   
    ![Страница с приглашениями](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="5b465-229">После принятия вашего приглашения, hello список приложений, имеют доступ toowill загруженный tooyour устройством и становятся доступными в hello Центр подключений.</span><span class="sxs-lookup"><span data-stu-id="5b465-229">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="5b465-230">Коснитесь одного из приложений toolaunch hello ее и начать его использование.</span><span class="sxs-lookup"><span data-stu-id="5b465-230">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Центр подключений с веб-каналом](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="5b465-232">Если приглашение еще нет, можно по-прежнему опробовать службу hello.</span><span class="sxs-lookup"><span data-stu-id="5b465-232">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="5b465-233">Таким образом, коснитесь toodo **Да** при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="5b465-233">toodo so, tap **yes** when prompted.</span></span>
   
    ![Приглашение к использованию демонстрационного веб-канала](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="5b465-235">Это позволит получить доступ к tooa базовый набор приложений tooget работы с RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5b465-235">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/WinPhone8.png)

