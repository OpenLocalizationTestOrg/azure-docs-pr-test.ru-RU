---
title: "aaaYou невозможно добраться отсюда туда на hello Azure портала на устройстве Windows | Документы Microsoft"
description: "Узнайте, где вы не можете здесь наступает от get и что можно было проверить tooavoid, работающие в этом диалоговом окне."
services: active-directory
keywords: "условный доступ на основе устройств, регистрация устройств, включить регистрацию устройств, регистрация устройств и MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="540be-104">Неполадки с доступом на устройстве Windows</span><span class="sxs-lookup"><span data-stu-id="540be-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="540be-105">Например, при попытке получить доступ к интрасети SharePoint Online вашей организации может отобразиться страница с сообщением *об отказе в доступе*.</span><span class="sxs-lookup"><span data-stu-id="540be-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="540be-106">Вы видите эту страницу, так как администратор настроил политику условного доступа, которая предотвращает tooyour организации доступа к ресурсам при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="540be-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="540be-107">Возможно, необходимые toocontact службы технической поддержки или ваш администратор tooget, решить эту проблему, существуют некоторые моменты, которые можно опробовать самостоятельно, сначала.</span><span class="sxs-lookup"><span data-stu-id="540be-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="540be-108">Если вы используете **Windows** устройства, необходимо проверить следующие hello:</span><span class="sxs-lookup"><span data-stu-id="540be-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="540be-109">Используется ли поддерживаемый браузер?</span><span class="sxs-lookup"><span data-stu-id="540be-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="540be-110">Поддерживает ли ваше устройство версию Windows?</span><span class="sxs-lookup"><span data-stu-id="540be-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="540be-111">Соответствует ли устройство требованиям?</span><span class="sxs-lookup"><span data-stu-id="540be-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="540be-112">Поддерживаемый браузер</span><span class="sxs-lookup"><span data-stu-id="540be-112">Supported browser</span></span>

<span data-ttu-id="540be-113">Если администратор настроил политику условного доступа, вы можете получить доступ к ресурсам организации с помощью поддерживаемого браузера.</span><span class="sxs-lookup"><span data-stu-id="540be-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="540be-114">Устройства с Windows поддерживают только **Internet Explorer** и **Edge**.</span><span class="sxs-lookup"><span data-stu-id="540be-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="540be-115">Можно легко определить ли нет доступа к ресурсу из-за tooan Неподдерживаемый браузер, просмотрев раздел сведения hello hello страницы ошибок.</span><span class="sxs-lookup"><span data-stu-id="540be-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="540be-116">![Сообщения об отказе в доступе для неподдерживаемых браузеров](./media/active-directory-conditional-access-device-remediation/02.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="540be-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="540be-117">только исправления Hello — toouse браузер, поддерживающий приложения hello для вашей платформы устройств.</span><span class="sxs-lookup"><span data-stu-id="540be-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="540be-118">Полный список поддерживаемых браузеров см. [здесь](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="540be-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="540be-119">Поддерживаемые версии Windows</span><span class="sxs-lookup"><span data-stu-id="540be-119">Supported versions of Windows</span></span>

<span data-ttu-id="540be-120">о операционной системы Windows hello на устройстве должны выполняться следующие Hello:</span><span class="sxs-lookup"><span data-stu-id="540be-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="540be-121">При запуске операционной системы Windows на устройстве должен toobe Windows 7 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="540be-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="540be-122">При запуске операционной системы Windows на устройстве, он должен toobe Windows Server 2008 R2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="540be-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="540be-123">Устройства, соответствующие требованиям</span><span class="sxs-lookup"><span data-stu-id="540be-123">Compliant device</span></span>

<span data-ttu-id="540be-124">Системный администратор может настроить политику условного доступа, которая позволяет организации доступа tooyour ресурсы только из совместимых устройств.</span><span class="sxs-lookup"><span data-stu-id="540be-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="540be-125">совместимые устройства должен быть либо присоединены к домену tooyour toobe локальной Active Directory или объединить tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="540be-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="540be-126">Можно легко определить ли невозможно доступ к ресурсу из-за tooa устройство, которое не соответствует требованиям, просмотрев раздел сведения hello hello страницы ошибок.</span><span class="sxs-lookup"><span data-stu-id="540be-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="540be-127">![Сообщения об отказе в доступе для незарегистрированных устройств](./media/active-directory-conditional-access-device-remediation/01.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="540be-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="540be-128">Такое вашего устройства присоединены tooan локальной Active Directory?</span><span class="sxs-lookup"><span data-stu-id="540be-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="540be-129">**Если ваше устройство присоединяется tooan локальной Active Directory в вашей организации:**</span><span class="sxs-lookup"><span data-stu-id="540be-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="540be-130">Убедитесь, что вход tooWindows с помощью рабочей учетной записью (учетной записи Active Directory).</span><span class="sxs-lookup"><span data-stu-id="540be-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="540be-131">Подключение tooyour корпоративной сети через DirectAccess или виртуальной частной сети (VPN).</span><span class="sxs-lookup"><span data-stu-id="540be-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="540be-132">После подключения, нажмите клавишу с эмблемой Windows hello + hello L ключа toolock сеанса работы с Windows.</span><span class="sxs-lookup"><span data-stu-id="540be-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="540be-133">Разблокируйте сеанс Windows, указав учетные данные рабочей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="540be-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="540be-134">Подождите около минуты и повторите попытку tooaccess hello приложения или службы.</span><span class="sxs-lookup"><span data-stu-id="540be-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="540be-135">Если вы видите hello же щелкните hello **Дополнительные сведения** связь, а затем обратитесь к администратору и сообщите подробности hello.</span><span class="sxs-lookup"><span data-stu-id="540be-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="540be-136">Такое вашего устройства не присоединены tooan локальной Active Directory?</span><span class="sxs-lookup"><span data-stu-id="540be-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="540be-137">Если ваше устройство не присоединяется tooan локальной Active Directory и работает под управлением Windows 10, имеются две возможности:</span><span class="sxs-lookup"><span data-stu-id="540be-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="540be-138">Выполнить присоединение к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="540be-138">Run Azure AD Join</span></span>
* <span data-ttu-id="540be-139">Добавить рабочую или учебную учетную запись tooWindows</span><span class="sxs-lookup"><span data-stu-id="540be-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="540be-140">Дополнительные сведения о различиях между этими вариантами см. в статье [Устройства под управлением Windows 10 в вашей рабочей области](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="540be-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="540be-141">Если ваше устройство:</span><span class="sxs-lookup"><span data-stu-id="540be-141">If your device:</span></span>

- <span data-ttu-id="540be-142">Принадлежит организации tooyour, необходимо выполнять присоединения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="540be-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="540be-143">Личное устройство или Windows phone, следует добавить рабочую или учебную учетную запись tooWindows</span><span class="sxs-lookup"><span data-stu-id="540be-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="540be-144">Присоединение к Azure AD в Windows 10</span><span class="sxs-lookup"><span data-stu-id="540be-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="540be-145">Hello toojoin шаги являются вашего устройства tooAzure AD привязанным hello версия Windows 10, которые запущены на нем.</span><span class="sxs-lookup"><span data-stu-id="540be-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="540be-146">toodetermine hello версии операционной системы Windows 10, запустите hello **winver** команды:</span><span class="sxs-lookup"><span data-stu-id="540be-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Версия Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="540be-148">**Юбилейное обновление Windows 10 (версия 1607):**</span><span class="sxs-lookup"><span data-stu-id="540be-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="540be-149">Откройте hello **параметры** приложения.</span><span class="sxs-lookup"><span data-stu-id="540be-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="540be-150">Щелкните **Учетные записи** > **Доступ к учетной записи места работы или учебного заведения**.</span><span class="sxs-lookup"><span data-stu-id="540be-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="540be-151">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="540be-151">Click **Connect**.</span></span>
4. <span data-ttu-id="540be-152">Нажмите кнопку **присоединить это устройство tooAzure AD**.</span><span class="sxs-lookup"><span data-stu-id="540be-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="540be-153">Выполнить проверку подлинности tooyour организации, обеспечения многофакторной проверки подлинности, если запрос и выполните действия hello, которые отображаются.</span><span class="sxs-lookup"><span data-stu-id="540be-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="540be-154">Выйдите из системы и войдите, используя рабочую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="540be-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="540be-155">Повторите попытку tooaccess приложения hello.</span><span class="sxs-lookup"><span data-stu-id="540be-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="540be-156">**Обновление Windows 10 от ноября 2015 г. (версия 1511):**</span><span class="sxs-lookup"><span data-stu-id="540be-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="540be-157">Откройте hello **параметры** приложения.</span><span class="sxs-lookup"><span data-stu-id="540be-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="540be-158">Щелкните **Система** > **Сведения**.</span><span class="sxs-lookup"><span data-stu-id="540be-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="540be-159">Щелкните **Присоединиться к Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="540be-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="540be-160">Выполнить проверку подлинности tooyour организации, обеспечения многофакторной проверки подлинности, если запрос и выполните действия hello, которые отображаются.</span><span class="sxs-lookup"><span data-stu-id="540be-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="540be-161">Выйдите из системы и войдите, используя рабочую учетную запись (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="540be-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="540be-162">Повторите попытку tooaccess приложения hello.</span><span class="sxs-lookup"><span data-stu-id="540be-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="540be-163">Присоединение к рабочей области в Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="540be-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="540be-164">Если устройство не присоединенных к домену и запускается Windows 8.1, toodo к рабочему месту и зарегистрироваться в Microsoft Intune, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="540be-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="540be-165">Откройте раздел **Параметры ПК**.</span><span class="sxs-lookup"><span data-stu-id="540be-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="540be-166">Щелкните **Сеть** > **Рабочее место**.</span><span class="sxs-lookup"><span data-stu-id="540be-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="540be-167">Щелкните **Соединить**.</span><span class="sxs-lookup"><span data-stu-id="540be-167">Click **Join**.</span></span>
4. <span data-ttu-id="540be-168">Выполнить проверку подлинности tooyour организации, обеспечения многофакторной проверки подлинности, если запрос и выполните действия hello, которые отображаются.</span><span class="sxs-lookup"><span data-stu-id="540be-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="540be-169">Щелкните **Включить**.</span><span class="sxs-lookup"><span data-stu-id="540be-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="540be-170">Повторите попытку tooaccess приложения hello.</span><span class="sxs-lookup"><span data-stu-id="540be-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="540be-171">Добавить рабочую или учебную учетную запись tooWindows</span><span class="sxs-lookup"><span data-stu-id="540be-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="540be-172">**Юбилейное обновление Windows 10 (версия 1607):**</span><span class="sxs-lookup"><span data-stu-id="540be-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="540be-173">Откройте hello **параметры** приложения.</span><span class="sxs-lookup"><span data-stu-id="540be-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="540be-174">Щелкните **Учетные записи** > **Доступ к учетной записи места работы или учебного заведения**.</span><span class="sxs-lookup"><span data-stu-id="540be-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="540be-175">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="540be-175">Click **Connect**.</span></span>
4. <span data-ttu-id="540be-176">Выполнить проверку подлинности tooyour организации, обеспечения многофакторной проверки подлинности, если запрос и выполните действия hello, которые отображаются.</span><span class="sxs-lookup"><span data-stu-id="540be-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="540be-177">Повторите попытку tooaccess приложения hello.</span><span class="sxs-lookup"><span data-stu-id="540be-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="540be-178">**Обновление Windows 10 от ноября 2015 г. (версия 1511):**</span><span class="sxs-lookup"><span data-stu-id="540be-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="540be-179">Откройте hello **параметры** приложения.</span><span class="sxs-lookup"><span data-stu-id="540be-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="540be-180">Щелкните **Учетные записи** > **Ваши учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="540be-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="540be-181">Щелкните **Добавить рабочую или учебную учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="540be-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="540be-182">Выполнить проверку подлинности tooyour организации, обеспечения многофакторной проверки подлинности, если запрос и выполните действия hello, которые отображаются.</span><span class="sxs-lookup"><span data-stu-id="540be-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="540be-183">Повторите попытку tooaccess приложения hello.</span><span class="sxs-lookup"><span data-stu-id="540be-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="540be-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="540be-184">Next steps</span></span>
[<span data-ttu-id="540be-185">Условный доступ в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="540be-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

