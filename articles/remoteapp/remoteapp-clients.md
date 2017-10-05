---
title: "Доступ к приложениям с любого устройства | Документация Майкрософт"
description: "Узнайте, какие клиенты поддерживаются службой Azure RemoteApp, а также как получить доступ к своим приложениям."
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
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="90c2f-103">Доступ к приложениям в Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="90c2f-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="90c2f-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="90c2f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="90c2f-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="90c2f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="90c2f-106">Одним из преимуществ службы Azure RemoteApp является возможность доступа к приложениям с любого устройства.</span><span class="sxs-lookup"><span data-stu-id="90c2f-106">One of the beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="90c2f-107">Более того, вы можете начать работу на одном устройстве, а затем без проблем продолжить ее на другом.</span><span class="sxs-lookup"><span data-stu-id="90c2f-107">Even better, you can start working on one device and then seamlessly transition to a second device and pick up right where you left off.</span></span> <span data-ttu-id="90c2f-108">Чтобы приступить к работе, необходимо загрузить на устройство соответствующий клиент и войти в службу.</span><span class="sxs-lookup"><span data-stu-id="90c2f-108">To get started you need to download the appropriate client for your device and sign in to the service.</span></span>

<span data-ttu-id="90c2f-109">В этом разделе вы найдете список поддерживаемых в настоящий момент клиентов, инструкции по их скачиванию, а также сведения о входе в удаленное приложение RemoteApp с помощью каждого из клиентов.</span><span class="sxs-lookup"><span data-stu-id="90c2f-109">In this topic, we'll review the clients currently supported and how to download them before I show you how to sign in to RemoteApp from each of the clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="90c2f-110">Поддерживаемые клиенты</span><span class="sxs-lookup"><span data-stu-id="90c2f-110">Supported clients</span></span>
<span data-ttu-id="90c2f-111">Если ваше устройство работает под управлением одной из следующих операционных систем, вы можете получить доступ к приложениям RemoteApp, выполнив описанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="90c2f-111">You can access RemoteApp using the steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="90c2f-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="90c2f-112">Windows 10</span></span> 
* <span data-ttu-id="90c2f-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="90c2f-113">Windows 8.1</span></span>
* <span data-ttu-id="90c2f-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="90c2f-114">Windows 8</span></span>
* <span data-ttu-id="90c2f-115">Windows 7 с пакетом обновления 1</span><span class="sxs-lookup"><span data-stu-id="90c2f-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="90c2f-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="90c2f-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="90c2f-117">iOS</span><span class="sxs-lookup"><span data-stu-id="90c2f-117">iOS</span></span>
* <span data-ttu-id="90c2f-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="90c2f-118">Mac OS X</span></span>
* <span data-ttu-id="90c2f-119">Android</span><span class="sxs-lookup"><span data-stu-id="90c2f-119">Android</span></span>

 <span data-ttu-id="90c2f-120">Сведения о тонких клиентах</span><span class="sxs-lookup"><span data-stu-id="90c2f-120">What about thin clients?</span></span> <span data-ttu-id="90c2f-121">Поддерживаются следующие тонкие клиенты Windows Embedded:</span><span class="sxs-lookup"><span data-stu-id="90c2f-121">The following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="90c2f-122">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="90c2f-122">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="90c2f-123">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="90c2f-123">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="90c2f-124">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="90c2f-124">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="90c2f-125">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="90c2f-125">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-the-client"></a><span data-ttu-id="90c2f-126">Загрузка клиента</span><span class="sxs-lookup"><span data-stu-id="90c2f-126">Downloading the client</span></span>
<span data-ttu-id="90c2f-127">Независимо от используемой платформы вы можете найти клиент, необходимый для доступа к приложениям RemoteApp, на странице [загрузки клиента удаленного рабочего стола](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) .</span><span class="sxs-lookup"><span data-stu-id="90c2f-127">No matter what platform you are using, the client you need to access RemoteApp can be found on the [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="90c2f-128">После того как вы щелкните нужную ссылку, либо начнется загрузка клиента, либо вы будете перенаправлены в магазин приложений на страницу загрузки клиента для данной платформы.</span><span class="sxs-lookup"><span data-stu-id="90c2f-128">Clicking the different links will either directly start downloading the client or will send you to the client download page in the app store for that platform.</span></span> <span data-ttu-id="90c2f-129">Установите клиент, следуя инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="90c2f-129">Install the client by following the instructions on the screen.</span></span>

<span data-ttu-id="90c2f-130">После установки и запуска клиента на устройстве перейдите к соответствующему разделу ниже, чтобы узнать, как с помощью этого клиента выполнить вход в службу RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="90c2f-130">Once you have installed the client on your device and launched it, jump to the corresponding section below to learn how to sign in to RemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="90c2f-131">Android</span><span class="sxs-lookup"><span data-stu-id="90c2f-131">Android</span></span>
<span data-ttu-id="90c2f-132">После установки приложения «Удаленный рабочий стол (Майкрософт)» из магазина Google Play его можно найти в списке приложений под именем **Remote Desktop**(Удаленный рабочий стол).</span><span class="sxs-lookup"><span data-stu-id="90c2f-132">Once you have installed the Microsoft Remote Desktop app from the Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="90c2f-133">Если вы ранее не использовали приложение, после его запуска сразу же откроется пустой центр подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-133">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="90c2f-134">Чтобы приступить к работе со службой Azure RemoteApp, нажмите кнопку **+** и выберите **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-134">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Пустой центр подключений](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="90c2f-136">Чтобы получить доступ к службе, выполните вход с использованием своего адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="90c2f-136">You need to sign in with your email address to access the service.</span></span> <span data-ttu-id="90c2f-137">Нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-137">Tap **Get started**.</span></span>
   
    ![Приглашение войти](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="90c2f-139">На следующей странице введите свой **адрес электронной почты** и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-139">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="90c2f-140">Таким образом вы сможете войти в службу с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90c2f-140">This begins the sign-in process using Azure Active Directory.</span></span>
   
    ![Первая страница Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="90c2f-142">Следуя инструкциям на экране, выполните вход с использованием учетной записи Майкрософт (которая раньше называлась LiveID) или идентификатора организации.</span><span class="sxs-lookup"><span data-stu-id="90c2f-142">Follow the instructions on the screen to sign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="90c2f-143">Войдя в службу, вы можете увидеть страницу со списком всех полученных приглашений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-143">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="90c2f-144">В таком случае выберите приглашения, которым вы доверяете, и нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="90c2f-144">If you are, select the invitations you trust and tap **Done**.</span></span>    
   
    ![Страница с приглашениями](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="90c2f-146">После принятия приглашений на устройство будет загружен список приложений, к которым у вас есть доступ. Эти приложения будут доступны в центре подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-146">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="90c2f-147">Выберите одного из приложений, чтобы начать его использовать.</span><span class="sxs-lookup"><span data-stu-id="90c2f-147">Tap one of the apps to start using it.</span></span>
   
    ![Центр подключений с веб-каналом](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="90c2f-149">Даже если у вас нет приглашения, вы все равно можете проверить работу службы.</span><span class="sxs-lookup"><span data-stu-id="90c2f-149">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="90c2f-150">Для этого при появлении запроса выберите элемент **Go to free trial** (Перейти к бесплатной пробной версии).</span><span class="sxs-lookup"><span data-stu-id="90c2f-150">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Приглашение к использованию демонстрационного веб-канала](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="90c2f-152">Вам будет предоставлен доступ к основному набору приложений, с помощью которых вы можете ознакомиться со службой RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="90c2f-152">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="90c2f-154">iOS</span><span class="sxs-lookup"><span data-stu-id="90c2f-154">iOS</span></span>
<span data-ttu-id="90c2f-155">После установки из магазина App Store приложение «Удаленный рабочий стол (Майкрософт)» можно найти в списке приложений под именем **RD Client**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-155">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="90c2f-156">Если вы ранее не использовали приложение, после его запуска сразу же откроется пустой центр подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-156">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="90c2f-157">Чтобы приступить к работе со службой Azure RemoteApp, нажмите кнопку **+** и выберите **Add Azure RemoteApp** (Добавить Azure RemoteApp).</span><span class="sxs-lookup"><span data-stu-id="90c2f-157">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Пустой центр подключений](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="90c2f-159">Чтобы получить доступ к службе, выполните вход, используя свой адрес электронной почты. Для этого введите **адрес электронной почты** и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-159">You need to sign in with your email address to access the service, to start that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Приглашение войти](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="90c2f-161">Следуйте инструкциям на экране, чтобы выполнить вход с использованием учетной записи Майкрософт (LiveID) или идентификатора организации.</span><span class="sxs-lookup"><span data-stu-id="90c2f-161">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="90c2f-162">Войдя в службу, вы можете увидеть страницу со списком всех полученных приглашений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-162">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="90c2f-163">В таком случае выберите приглашения, которым вы доверяете, и нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="90c2f-163">If you are, select the invitations you trust and tap **Done**.</span></span>
   
    ![Страница с приглашениями](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="90c2f-165">После принятия приглашений на устройство будет загружен список приложений, к которым у вас есть доступ. Эти приложения будут доступны в центре подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-165">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="90c2f-166">Выберите нужное приложение, чтобы запустить его и начать с ним работу.</span><span class="sxs-lookup"><span data-stu-id="90c2f-166">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Центр подключений с веб-каналом](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="90c2f-168">Даже если у вас нет приглашения, вы все равно можете проверить работу службы.</span><span class="sxs-lookup"><span data-stu-id="90c2f-168">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="90c2f-169">Для этого при появлении запроса выберите элемент **Go to free trial** (Перейти к бесплатной пробной версии).</span><span class="sxs-lookup"><span data-stu-id="90c2f-169">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Приглашение к использованию демонстрационного веб-канала](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="90c2f-171">Вам будет предоставлен доступ к основному набору приложений, с помощью которых вы можете ознакомиться со службой RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="90c2f-171">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="90c2f-173">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="90c2f-173">Mac OS X</span></span>
<span data-ttu-id="90c2f-174">После установки из магазина App Store приложение "Удаленный рабочий стол (Майкрософт)" можно найти в списке приложений под именем **Microsoft Remote Desktop**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-174">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="90c2f-175">Если вы ранее не использовали приложение, после его запуска сразу же откроется пустой центр подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-175">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="90c2f-176">Чтобы начать работу со службой Azure RemoteApp, нажмите кнопку **Azure RemoteApp** .</span><span class="sxs-lookup"><span data-stu-id="90c2f-176">To get started with Azure RemoteApp, click the **Azure RemoteApp** button.</span></span>
   
    ![Пустой центр подключений](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="90c2f-178">Чтобы получить доступ к службе, выполните вход, используя свой адрес электронной почты. Для этого нажмите кнопку **Начало работы**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-178">You need to sign in with your email address to access the service, to start that process, tap **Get Started**.</span></span>
   
    ![Приглашение войти](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="90c2f-180">На следующей странице введите свой **адрес электронной почты** и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-180">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="90c2f-181">Таким образом вы сможете войти в службу с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90c2f-181">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![Первая страница Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="90c2f-183">Следуйте инструкциям на экране, чтобы выполнить вход с использованием учетной записи Майкрософт (LiveID) или идентификатора организации.</span><span class="sxs-lookup"><span data-stu-id="90c2f-183">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="90c2f-184">Войдя в службу, вы можете увидеть страницу со списком всех полученных приглашений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-184">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="90c2f-185">В таком случае выберите приглашения, которым вы доверяете, и закройте диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="90c2f-185">If you are, select the invitations you trust and close the dialog.</span></span>
   
    ![Страница с приглашениями](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="90c2f-187">После принятия приглашений на устройство будет загружен список приложений, к которым у вас есть доступ. Эти приложения будут доступны в центре подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-187">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="90c2f-188">Дважды щелкните нужное приложение, чтобы запустить его и начать с ним работу.</span><span class="sxs-lookup"><span data-stu-id="90c2f-188">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Центр подключений с веб-каналом](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="90c2f-190">Даже если у вас нет приглашения, вы все равно можете проверить работу службы.</span><span class="sxs-lookup"><span data-stu-id="90c2f-190">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="90c2f-191">Для этого при появлении запроса выберите элемент **Go to free trial** (Перейти к бесплатной пробной версии).</span><span class="sxs-lookup"><span data-stu-id="90c2f-191">To do so, click **Go to free trial** when prompted.</span></span>
   
    ![Приглашение к использованию демонстрационного веб-канала](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="90c2f-193">Вам будет предоставлен доступ к основному набору приложений, с помощью которых вы можете ознакомиться со службой RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="90c2f-193">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="90c2f-195">Windows (все поддерживаемые версии, кроме Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="90c2f-195">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="90c2f-196">После завершения установки клиент запускается автоматически. Чтобы получить доступ к клиенту позже, найдите его в списке приложений под именем **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-196">The client launches automatically after it finishes installing, however when you need to access it again later it can be found in your app list under the name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="90c2f-197">После запуска клиента откроется страница приветствия Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="90c2f-197">Ater launching the client, the first page you see welcomes you to Azure RemoteApp.</span></span> <span data-ttu-id="90c2f-198">Чтобы продолжить, нажмите кнопку **Get Started**(Начало работы).</span><span class="sxs-lookup"><span data-stu-id="90c2f-198">To proceed, click on **Get Started**.</span></span>
   
    ![Страница приветствия клиента Azure RemoteApp](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="90c2f-200">На следующей странице вам будет предложено войти в Azure RemoteApp с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90c2f-200">The next page starts the sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="90c2f-201">Этот процесс будет знакомым для вас, если вы использовали службы Майкрософт ранее.</span><span class="sxs-lookup"><span data-stu-id="90c2f-201">This process should look familiar if you have used Microsoft services in the past.</span></span> <span data-ttu-id="90c2f-202">Введите свой **адрес электронной почты** и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-202">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Первая страница с приглашением к использованию Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="90c2f-204">Следуйте инструкциям на экране, чтобы выполнить вход с использованием учетной записи Майкрософт (LiveID) или идентификатора организации.</span><span class="sxs-lookup"><span data-stu-id="90c2f-204">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="90c2f-205">Войдя в службу, вы можете увидеть страницу со списком всех полученных приглашений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-205">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="90c2f-206">В таком случае выберите приглашения, которым вы доверяете, и нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="90c2f-206">If you are, select the invitations you trust and click **Done**.</span></span>
   
    ![Страница с приглашениями клиента Azure RemoteApp](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="90c2f-208">После принятия приглашений на устройство будет загружен список приложений, к которым у вас есть доступ. Эти приложения будут доступны в центре подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-208">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="90c2f-209">Дважды щелкните нужное приложение, чтобы запустить его и начать с ним работу.</span><span class="sxs-lookup"><span data-stu-id="90c2f-209">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Центр подключений клиента Azure RemoteApp](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="90c2f-211">Если вы не получили ни одного приглашения, не беспокойтесь, скоро вам их отправят.</span><span class="sxs-lookup"><span data-stu-id="90c2f-211">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="90c2f-212">У вас по-прежнему есть возможность доступа к демонстрационной коллекции, с помощью которой вы можете проверить работу службы.</span><span class="sxs-lookup"><span data-stu-id="90c2f-212">You'll still have access to a demo collection so you can test out the service.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="90c2f-214">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="90c2f-214">Windows Phone 8.1</span></span>
<span data-ttu-id="90c2f-215">После установки из магазина Windows Phone 8.1 приложение «Удаленный рабочий стол (Майкрософт)» можно найти в списке приложений под именем **Удаленный рабочий стол**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-215">Once you have installed the Microsoft Remote Desktop app from the Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="90c2f-216">Если вы ранее не использовали приложение, после его запуска сразу же откроется пустой центр подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-216">Launching the app brings you directly to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="90c2f-217">Чтобы начать работу со службой Azure RemoteApp, нажмите кнопку **+** в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="90c2f-217">To get started with Azure RemoteApp, tap the add button **""+""** at the bottom of the screen.</span></span>
   
    ![Пустой центр подключений](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="90c2f-219">Затем выберите элемент **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-219">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Страница с элементом "добавить"](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="90c2f-221">Чтобы получить доступ к службе, выполните вход, используя свой адрес электронной почты. Для этого нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-221">You need to sign in with your email address to access the service, to start that process, tap **connect**.</span></span>
   
    ![Приглашение войти](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="90c2f-223">На следующей странице введите свой **адрес электронной почты** и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-223">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="90c2f-224">Таким образом вы сможете войти в службу с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90c2f-224">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![Первая страница Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="90c2f-226">Следуйте инструкциям на экране, чтобы выполнить вход с использованием учетной записи Майкрософт (LiveID) или идентификатора организации.</span><span class="sxs-lookup"><span data-stu-id="90c2f-226">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="90c2f-227">Войдя в службу, вы можете увидеть страницу со списком всех полученных приглашений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-227">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="90c2f-228">В таком случае выберите приглашения, которым вы доверяете, и нажмите кнопку **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="90c2f-228">If you are, select the invitations you trust and tap **save**.</span></span>
   
    ![Страница с приглашениями](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="90c2f-230">После принятия приглашений на устройство будет загружен список приложений, к которым у вас есть доступ. Эти приложения будут доступны в центре подключений.</span><span class="sxs-lookup"><span data-stu-id="90c2f-230">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="90c2f-231">Выберите нужное приложение, чтобы запустить его и начать с ним работу.</span><span class="sxs-lookup"><span data-stu-id="90c2f-231">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Центр подключений с веб-каналом](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="90c2f-233">Даже если у вас нет приглашения, вы все равно можете проверить работу службы.</span><span class="sxs-lookup"><span data-stu-id="90c2f-233">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="90c2f-234">Для этого нажмите кнопку **да** при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="90c2f-234">To do so, tap **yes** when prompted.</span></span>
   
    ![Приглашение к использованию демонстрационного веб-канала](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="90c2f-236">Вам будет предоставлен доступ к основному набору приложений, с помощью которых вы можете ознакомиться со службой RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="90c2f-236">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Демонстрационный веб-канал с приложениями Azure RemoteApp](./media/remoteapp-clients/WinPhone8.png)

