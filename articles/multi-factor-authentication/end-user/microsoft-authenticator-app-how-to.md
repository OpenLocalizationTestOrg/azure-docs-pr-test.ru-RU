---
title: "Приложение Microsoft Authenticator для мобильных телефонов | Документация Майкрософт"
description: "Узнайте, как выполнить обновление до последней версии Azure Authenticatior."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: 6bcb6d9f7a1e9b241fa70690016b03d6eb5887ab
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="0c16d-103">Начало работы с приложением Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="0c16d-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="0c16d-104">Приложение Microsoft Authenticator обеспечивает дополнительный уровень безопасности для рабочей учетной записи (например, bsimon@contoso.com) или для учетной записи Майкрософт (например, bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="0c16d-104">The Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="0c16d-105">В приложении используется один из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="0c16d-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="0c16d-106">**Уведомление.**</span><span class="sxs-lookup"><span data-stu-id="0c16d-106">**Notification**.</span></span> <span data-ttu-id="0c16d-107">Приложение помогает предотвратить несанкционированный доступ к учетным записям и остановить мошеннические транзакции, отправив уведомление на смартфон или планшетный ПК.</span><span class="sxs-lookup"><span data-stu-id="0c16d-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="0c16d-108">Просто просмотрите уведомление, и если оно подлинное, нажмите кнопку **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="0c16d-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="0c16d-109">В противном случае нажмите кнопку **Отклонить**.</span><span class="sxs-lookup"><span data-stu-id="0c16d-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="0c16d-110">**Код проверки**.</span><span class="sxs-lookup"><span data-stu-id="0c16d-110">**Verification code**.</span></span> <span data-ttu-id="0c16d-111">Приложение можно использовать в качестве программного токена для создания кода проверки OATH.</span><span class="sxs-lookup"><span data-stu-id="0c16d-111">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="0c16d-112">После ввода имени пользователя и пароля на экране входа нужно ввести код, предоставленный приложением.</span><span class="sxs-lookup"><span data-stu-id="0c16d-112">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="0c16d-113">Код проверки выступает вторым методом проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0c16d-113">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="0c16d-114">Теперь вместо приложения Azure Authenticator используется приложение Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="0c16d-114">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span> <span data-ttu-id="0c16d-115">Приложение Azure Authenticator по-прежнему работает. Сведения в этой статье пригодятся вам, когда вы решите перейти к новому приложению Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="0c16d-115">The Azure Authenticator app still works, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="0c16d-116">Выбор двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="0c16d-116">Opt in for two-step verification</span></span>

<span data-ttu-id="0c16d-117">Приложение Microsoft Authenticator не работает само по себе.</span><span class="sxs-lookup"><span data-stu-id="0c16d-117">The Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="0c16d-118">Настройте свои учетные записи для запроса второго способа проверки после входа с использованием имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="0c16d-118">Configure each of your accounts to prompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="0c16d-119">В случае рабочей или учебной учетной записи, как правило, вы не можете выбрать эту функцию самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="0c16d-119">For a work or school account, you don't usually get to choose this feature for yourself.</span></span> <span data-ttu-id="0c16d-120">Администратор безопасности сделает выбор от вашего имени и затем уведомит вас о необходимости регистрации способов аутентификации для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0c16d-120">Instead, a security administrator opts in on your behalf and then notifies you to register verification methods for your account.</span></span> <span data-ttu-id="0c16d-121">Если этот сценарий применим для вас, см. дополнительные сведения в статье [Что для меня означает Azure Multi-Factor Authentication](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="0c16d-121">If this scenario applies to you, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="0c16d-122">При использовании личной учетной записи необходимо настроить двухшаговую проверку самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="0c16d-122">For a personal account, you need to set up two-step verification for yourself.</span></span> <span data-ttu-id="0c16d-123">Если у вас есть учетная запись Майкрософт, это описание этих действий доступно на странице [Сведения о двухшаговой проверке](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="0c16d-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="0c16d-124">Microsoft Authenticator также можно использовать со сторонними учетными записями.</span><span class="sxs-lookup"><span data-stu-id="0c16d-124">You can also use the Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="0c16d-125">Они могут предоставлять доступ к функции, отличной от двухшаговой проверки. Ее можно найти в разделе безопасности или параметров входа.</span><span class="sxs-lookup"><span data-stu-id="0c16d-125">They may call the feature something other than two-step verification, but you should be able to find it under security or sign-in settings.</span></span> 

## <a name="install-the-app"></a><span data-ttu-id="0c16d-126">Установка приложения</span><span class="sxs-lookup"><span data-stu-id="0c16d-126">Install the app</span></span>
<span data-ttu-id="0c16d-127">Приложение Microsoft Authenticator доступно для [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072) и [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="0c16d-127">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="0c16d-128">Добавление учетной записи в приложение</span><span class="sxs-lookup"><span data-stu-id="0c16d-128">Add accounts to the app</span></span>
<span data-ttu-id="0c16d-129">Чтобы добавить учетную запись в приложение Microsoft Authenticator, следуйте одной из приведенных ниже процедур.</span><span class="sxs-lookup"><span data-stu-id="0c16d-129">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="0c16d-130">Добавление личной учетной записи Майкрософт в приложение</span><span class="sxs-lookup"><span data-stu-id="0c16d-130">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="0c16d-131">Чтобы добавить личную учетную запись Майкрософт (используемую для входа в Outlook.com, Xbox, Skype и т. д.), нужно просто войти в нее в приложении Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="0c16d-131">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc.), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="0c16d-132">Добавление рабочей или учебой учетной записи в приложение с использованием сканера QR-кода</span><span class="sxs-lookup"><span data-stu-id="0c16d-132">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="0c16d-133">Перейдите на страницу параметров проверки безопасности.</span><span class="sxs-lookup"><span data-stu-id="0c16d-133">Go to the security verification settings screen.</span></span>  <span data-ttu-id="0c16d-134">Инструкции по переходу на эту страницу см. в статье [Управление параметрами двухфакторной проверки подлинности](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="0c16d-134">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="0c16d-135">Установите флажок **Приложение Authenticator** и нажмите кнопку **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="0c16d-135">Check the box next to **Authenticator app** then select **Configure**.</span></span>

    ![Кнопка "Настроить" на странице параметров проверки безопасности](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="0c16d-137">Откроется страница с QR-кодом.</span><span class="sxs-lookup"><span data-stu-id="0c16d-137">This brings up a screen with a QR code on it.</span></span>

    ![Окно с QR-кодом](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="0c16d-139">Откройте приложение Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="0c16d-139">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="0c16d-140">В окне с **учетными записями** щелкните значок **+**, а затем укажите, что вы хотите добавить рабочую или учебную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="0c16d-140">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="0c16d-141">Отсканируйте QR-код с помощью камеры, а затем нажмите кнопку **Готово** , чтобы закрыть окно с кодом.</span><span class="sxs-lookup"><span data-stu-id="0c16d-141">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="0c16d-142">Если камера не работает должным образом, можно [ввести QR-код и URL-адрес вручную](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="0c16d-142">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="0c16d-143">Когда в приложении отобразится имя пользователя с шестизначным кодом под ним, это означает, что все готово.</span><span class="sxs-lookup"><span data-stu-id="0c16d-143">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Окно с учетными записями](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="0c16d-145">Добавление учетной записи в приложение вручную</span><span class="sxs-lookup"><span data-stu-id="0c16d-145">Add an account to the app manually</span></span>
1. <span data-ttu-id="0c16d-146">Перейдите на страницу параметров проверки безопасности.</span><span class="sxs-lookup"><span data-stu-id="0c16d-146">Go to the security verification settings screen.</span></span>  <span data-ttu-id="0c16d-147">Инструкции по переходу на эту страницу см. в статье [Управление параметрами двухфакторной проверки подлинности](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="0c16d-147">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="0c16d-148">Нажмите кнопку **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="0c16d-148">Select **Configure**.</span></span>

    ![Кнопка "Настроить" на странице параметров проверки безопасности](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="0c16d-150">Откроется страница с QR-кодом.</span><span class="sxs-lookup"><span data-stu-id="0c16d-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="0c16d-151">Запишите код и URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0c16d-151">Note the code and URL.</span></span>

    ![Окно с QR-кодом и URL-адресом](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="0c16d-153">Откройте приложение Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="0c16d-153">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="0c16d-154">В окне с **учетными записями** щелкните значок **+**, а затем укажите, что вы хотите добавить рабочую или учебную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="0c16d-154">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="0c16d-155">В сканере щелкните **Или введите код вручную**.</span><span class="sxs-lookup"><span data-stu-id="0c16d-155">In the scanner, select **enter code manually**.</span></span>

    ![Окно для сканирования QR-кода](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="0c16d-157">Введите код и URL-адрес в соответствующих полях приложения и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="0c16d-157">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![Окно ввода кода и URL-адреса](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="0c16d-159">Когда в приложении отобразится имя пользователя с шестизначным кодом под ним, это означает, что все готово.</span><span class="sxs-lookup"><span data-stu-id="0c16d-159">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Окно с учетными записями](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="0c16d-161">Добавление учетной записи в приложение с использованием Touch ID</span><span class="sxs-lookup"><span data-stu-id="0c16d-161">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="0c16d-162">Приложение Microsoft Authenticator на iOS поддерживает Touch ID.</span><span class="sxs-lookup"><span data-stu-id="0c16d-162">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="0c16d-163">Многофакторная идентификация Azure позволяет организациям запрашивать ПИН-код для устройств.</span><span class="sxs-lookup"><span data-stu-id="0c16d-163">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="0c16d-164">При использовании Touch ID пользователям iOS не нужно вводить ПИН-код.</span><span class="sxs-lookup"><span data-stu-id="0c16d-164">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="0c16d-165">Вместо этого можно просканировать отпечатки пальцев и нажать кнопку **Утвердить**.</span><span class="sxs-lookup"><span data-stu-id="0c16d-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="0c16d-166">Настройка Touch ID в приложении Microsoft Authenticator выполняется очень просто.</span><span class="sxs-lookup"><span data-stu-id="0c16d-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="0c16d-167">Обычная проверка заканчивается вводом ПИН-кода.</span><span class="sxs-lookup"><span data-stu-id="0c16d-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="0c16d-168">Если устройство поддерживает Touch ID, Microsoft Authenticator автоматически настроит его для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0c16d-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Проверка настройки Touch ID](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="0c16d-170">С этого момента для подтверждения входа вместо ввода ПИН-кода вам нужно будет только коснуться полученного push-уведомления и просканировать отпечаток пальца.</span><span class="sxs-lookup"><span data-stu-id="0c16d-170">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![push-уведомление](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-the-app-when-you-sign-in"></a><span data-ttu-id="0c16d-172">Использование приложения при входе</span><span class="sxs-lookup"><span data-stu-id="0c16d-172">Use the app when you sign in</span></span>

<span data-ttu-id="0c16d-173">После того как учетная запись будет добавлена в приложение, может потребоваться пройти тестовую проверку, чтобы убедиться в правильности настройки всех параметров.</span><span class="sxs-lookup"><span data-stu-id="0c16d-173">Once your account is added to the app, you may be prompted to do a test verification to make sure everything was configured correctly.</span></span> <span data-ttu-id="0c16d-174">После этого все будет готово!</span><span class="sxs-lookup"><span data-stu-id="0c16d-174">After that, you're done!</span></span> <span data-ttu-id="0c16d-175">Вам не нужно ничего делать вплоть до следующего входа.</span><span class="sxs-lookup"><span data-stu-id="0c16d-175">You don't need to do anything else until the next time you sign in.</span></span>

<span data-ttu-id="0c16d-176">Если вы решили использовать коды проверки в приложении, они будут отображаться на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="0c16d-176">If you chose to use verification codes in the app, you start to see them on the home page.</span></span> <span data-ttu-id="0c16d-177">Они изменяются каждые 30 секунд, поэтому при необходимости у вас всегда будет новый код.</span><span class="sxs-lookup"><span data-stu-id="0c16d-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="0c16d-178">Ничего не делайте с ними до тех пор, пока не выполните вход и не получите запрос на ввод кода проверки.</span><span class="sxs-lookup"><span data-stu-id="0c16d-178">But you don't need to do anything with them until you sign in and are prompted to enter a verification code.</span></span>  