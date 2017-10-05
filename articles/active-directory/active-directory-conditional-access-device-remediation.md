---
title: "Неполадки с доступом на портале Azure при использовании устройств с Windows | Документация Майкрософт"
description: "Узнайте, почему возникла проблема с доступом и что можно проверить, чтобы избежать такого."
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
ms.openlocfilehash: 16543c7bb7b6b236dcc24093c9963bc218ca1fa6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="b86de-104">Неполадки с доступом на устройстве Windows</span><span class="sxs-lookup"><span data-stu-id="b86de-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="b86de-105">Например, при попытке получить доступ к интрасети SharePoint Online вашей организации может отобразиться страница с сообщением *об отказе в доступе*.</span><span class="sxs-lookup"><span data-stu-id="b86de-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="b86de-106">Так происходит, потому что ваш администратор настроил политику условного доступа, которая запрещает доступ к ресурсам организации при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="b86de-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access to your organization's resources under certain conditions.</span></span> <span data-ttu-id="b86de-107">Зачастую для устранения проблемы необходимо обратиться в службу технической поддержки или к администратору, однако существует несколько способов, которые могут помочь справиться с проблемой самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="b86de-107">While it might be necessary to contact helpdesk or your administrator to get this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="b86de-108">Если вы используете устройство с **Windows**, необходимо проверить следующее:</span><span class="sxs-lookup"><span data-stu-id="b86de-108">If you are using a **Windows** device, you should check the following:</span></span>

- <span data-ttu-id="b86de-109">Используется ли поддерживаемый браузер?</span><span class="sxs-lookup"><span data-stu-id="b86de-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="b86de-110">Поддерживает ли ваше устройство версию Windows?</span><span class="sxs-lookup"><span data-stu-id="b86de-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="b86de-111">Соответствует ли устройство требованиям?</span><span class="sxs-lookup"><span data-stu-id="b86de-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="b86de-112">Поддерживаемый браузер</span><span class="sxs-lookup"><span data-stu-id="b86de-112">Supported browser</span></span>

<span data-ttu-id="b86de-113">Если администратор настроил политику условного доступа, вы можете получить доступ к ресурсам организации с помощью поддерживаемого браузера.</span><span class="sxs-lookup"><span data-stu-id="b86de-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="b86de-114">Устройства с Windows поддерживают только **Internet Explorer** и **Edge**.</span><span class="sxs-lookup"><span data-stu-id="b86de-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="b86de-115">В разделе со сведениями на странице ошибки можно легко определить, используется ли неподдерживаемый браузер для получения доступа к ресурсам:</span><span class="sxs-lookup"><span data-stu-id="b86de-115">You can easily identify whether you can't access a resource due to an unsupported browser by looking at the details section of the error page:</span></span>

<span data-ttu-id="b86de-116">![Сообщения об отказе в доступе для неподдерживаемых браузеров](./media/active-directory-conditional-access-device-remediation/02.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="b86de-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="b86de-117">В этом случае для получения доступа к приложению нужно использовать браузер, поддерживаемый платформой устройства.</span><span class="sxs-lookup"><span data-stu-id="b86de-117">The only remediation is to use a browser that the application supports for your device platform.</span></span> <span data-ttu-id="b86de-118">Полный список поддерживаемых браузеров см. [здесь](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="b86de-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="b86de-119">Поддерживаемые версии Windows</span><span class="sxs-lookup"><span data-stu-id="b86de-119">Supported versions of Windows</span></span>

<span data-ttu-id="b86de-120">Для устройств под управлением операционной системы Windows должны выполняться следующие условия:</span><span class="sxs-lookup"><span data-stu-id="b86de-120">The following must be true about the Windows operating system on your device:</span></span> 

- <span data-ttu-id="b86de-121">Используйте Windows 7 или более позднюю версию для настольных устройств под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="b86de-121">If you are running a Windows desktop operating system on your device, it needs to be Windows 7 or later.</span></span>
- <span data-ttu-id="b86de-122">Используйте Windows 2008 R2 или более позднюю версию для устройств под управлением операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="b86de-122">If you are running a Windows server operating system on your device, it needs to be Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="b86de-123">Устройства, соответствующие требованиям</span><span class="sxs-lookup"><span data-stu-id="b86de-123">Compliant device</span></span>

<span data-ttu-id="b86de-124">Ваш администратор может настроить политику условного доступа, которая разрешает доступ к ресурсам организации только при использовании устройств, соответствующих требованиям.</span><span class="sxs-lookup"><span data-stu-id="b86de-124">Your administrator might have configured a conditional access policy that allows access to your organization's resources only from compliant devices.</span></span> <span data-ttu-id="b86de-125">В соответствии с требованиями устройство нужно присоединить к локальной службе Active Directory или к Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b86de-125">To be compliant, your device must be either joined to your on-premises Active Directory or joined to your Azure Active Directory.</span></span>

<span data-ttu-id="b86de-126">В разделе со сведениями на странице ошибки можно легко определить, используется ли несоответствующее устройство для получения доступа к ресурсам:</span><span class="sxs-lookup"><span data-stu-id="b86de-126">You can easily identify whether you can't access a resource due to a device that is not compliant by looking at the details section of the error page:</span></span>
 
<span data-ttu-id="b86de-127">![Сообщения об отказе в доступе для незарегистрированных устройств](./media/active-directory-conditional-access-device-remediation/01.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="b86de-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="b86de-128">Присоединено ли устройство к локальной службе Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b86de-128">Is your device joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="b86de-129">**Если устройство присоединено к локальной службе Active Directory организации, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b86de-129">**If your device is joined to an on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="b86de-130">Войдите в Windows, используя рабочую учетную запись (учетную запись Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b86de-130">Make sure that you sign in to Windows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="b86de-131">Подключитесь к корпоративной сети через виртуальную частную сеть (VPN) или DirectAccess.</span><span class="sxs-lookup"><span data-stu-id="b86de-131">Connect to your corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="b86de-132">После подключения заблокируйте сеанс Windows, нажав клавиши Windows+L.</span><span class="sxs-lookup"><span data-stu-id="b86de-132">After you are connected, press the Windows logo key + the L key to lock your Windows session.</span></span>
4. <span data-ttu-id="b86de-133">Разблокируйте сеанс Windows, указав учетные данные рабочей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b86de-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="b86de-134">Подождите минуту и попробуйте получить доступ к приложению или службе еще раз.</span><span class="sxs-lookup"><span data-stu-id="b86de-134">Wait for a minute, and then try again to access the application or service.</span></span>
6. <span data-ttu-id="b86de-135">Если отобразится та же страница, щелкните ссылку **Дополнительные сведения**, а затем свяжитесь с администратором и предоставьте ему соответствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="b86de-135">If you see the same page, click the **More details** link, and then contact your administrator with the details.</span></span>


### <a name="is-your-device-not-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="b86de-136">Устройство не присоединено к локальной службе Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b86de-136">Is your device not joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="b86de-137">Если устройство не присоединено к локальной службе Active Directory и работает под управлением Windows 10, у вас есть два варианта доступа:</span><span class="sxs-lookup"><span data-stu-id="b86de-137">If your device is not joined to an on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="b86de-138">Выполнить присоединение к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b86de-138">Run Azure AD Join</span></span>
* <span data-ttu-id="b86de-139">Добавить свою рабочую или учебную учетную запись в Windows.</span><span class="sxs-lookup"><span data-stu-id="b86de-139">Add your work or school account to Windows</span></span>

<span data-ttu-id="b86de-140">Дополнительные сведения о различиях между этими вариантами см. в статье [Устройства под управлением Windows 10 в вашей рабочей области](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="b86de-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="b86de-141">Если ваше устройство:</span><span class="sxs-lookup"><span data-stu-id="b86de-141">If your device:</span></span>

- <span data-ttu-id="b86de-142">принадлежит вашей организации, выполните присоединение к Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b86de-142">Belongs to your organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="b86de-143">является личным или Windows Phone, добавьте свою рабочую или учебную учетную запись в Windows.</span><span class="sxs-lookup"><span data-stu-id="b86de-143">Is a personal device or a Windows phone, you should add your work or school account to Windows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="b86de-144">Присоединение к Azure AD в Windows 10</span><span class="sxs-lookup"><span data-stu-id="b86de-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="b86de-145">Процедура подключения устройства к Azure AD зависит от запущенной версии Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b86de-145">The steps to join your device to Azure AD are tied the version of Windows 10 you are running on it.</span></span> <span data-ttu-id="b86de-146">Чтобы определить версию операционной системы Windows 10, выполните команду **winver**:</span><span class="sxs-lookup"><span data-stu-id="b86de-146">To determine the version of your Windows 10 operating system, run the **winver** command:</span></span> 

![Версия Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="b86de-148">**Юбилейное обновление Windows 10 (версия 1607):**</span><span class="sxs-lookup"><span data-stu-id="b86de-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="b86de-149">Откройте приложение **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="b86de-149">Open the **Settings** app.</span></span>
2. <span data-ttu-id="b86de-150">Щелкните **Учетные записи** > **Доступ к учетной записи места работы или учебного заведения**.</span><span class="sxs-lookup"><span data-stu-id="b86de-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="b86de-151">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="b86de-151">Click **Connect**.</span></span>
4. <span data-ttu-id="b86de-152">Щелкните **Присоединить это устройство к Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b86de-152">Click **Join this device to Azure AD**.</span></span>
5. <span data-ttu-id="b86de-153">Пройдите проверку подлинности в организации, при появлении соответствующего запроса предоставьте подтверждение многофакторной проверки подлинности и выполните описанные действия.</span><span class="sxs-lookup"><span data-stu-id="b86de-153">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
6. <span data-ttu-id="b86de-154">Выйдите из системы и войдите, используя рабочую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="b86de-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="b86de-155">Попробуйте получить доступ к приложению еще раз.</span><span class="sxs-lookup"><span data-stu-id="b86de-155">Try again to access the application.</span></span>

<span data-ttu-id="b86de-156">**Обновление Windows 10 от ноября 2015 г. (версия 1511):**</span><span class="sxs-lookup"><span data-stu-id="b86de-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="b86de-157">Откройте приложение **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="b86de-157">Open the **Settings** app.</span></span>
2. <span data-ttu-id="b86de-158">Щелкните **Система** > **Сведения**.</span><span class="sxs-lookup"><span data-stu-id="b86de-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="b86de-159">Щелкните **Присоединиться к Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="b86de-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="b86de-160">Пройдите проверку подлинности в организации, при появлении соответствующего запроса предоставьте подтверждение многофакторной проверки подлинности и выполните описанные действия.</span><span class="sxs-lookup"><span data-stu-id="b86de-160">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="b86de-161">Выйдите из системы и войдите, используя рабочую учетную запись (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b86de-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="b86de-162">Попробуйте получить доступ к приложению еще раз.</span><span class="sxs-lookup"><span data-stu-id="b86de-162">Try again to access the application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="b86de-163">Присоединение к рабочей области в Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b86de-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="b86de-164">Если устройство не присоединено к домену и работает под управлением Windows 8.1, чтобы подключиться к рабочему месту и зарегистрироваться в Microsoft Intune, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b86de-164">If your device is not domain-joined and runs Windows 8.1, to do a Workplace Join and enroll in Microsoft Intune, do the following steps:</span></span>

1. <span data-ttu-id="b86de-165">Откройте раздел **Параметры ПК**.</span><span class="sxs-lookup"><span data-stu-id="b86de-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="b86de-166">Щелкните **Сеть** > **Рабочее место**.</span><span class="sxs-lookup"><span data-stu-id="b86de-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="b86de-167">Щелкните **Соединить**.</span><span class="sxs-lookup"><span data-stu-id="b86de-167">Click **Join**.</span></span>
4. <span data-ttu-id="b86de-168">Пройдите проверку подлинности в организации, при появлении соответствующего запроса предоставьте подтверждение многофакторной проверки подлинности и выполните описанные действия.</span><span class="sxs-lookup"><span data-stu-id="b86de-168">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="b86de-169">Щелкните **Включить**.</span><span class="sxs-lookup"><span data-stu-id="b86de-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="b86de-170">Попробуйте получить доступ к приложению еще раз.</span><span class="sxs-lookup"><span data-stu-id="b86de-170">Try again to access the application.</span></span>



#### <a name="add-your-work-or-school-account-to-windows"></a><span data-ttu-id="b86de-171">Добавить свою рабочую или учебную учетную запись в Windows.</span><span class="sxs-lookup"><span data-stu-id="b86de-171">Add your work or school account to Windows</span></span> 


<span data-ttu-id="b86de-172">**Юбилейное обновление Windows 10 (версия 1607):**</span><span class="sxs-lookup"><span data-stu-id="b86de-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="b86de-173">Откройте приложение **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="b86de-173">Open the **Settings** app.</span></span>
2. <span data-ttu-id="b86de-174">Щелкните **Учетные записи** > **Доступ к учетной записи места работы или учебного заведения**.</span><span class="sxs-lookup"><span data-stu-id="b86de-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="b86de-175">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="b86de-175">Click **Connect**.</span></span>
4. <span data-ttu-id="b86de-176">Пройдите проверку подлинности в организации, при появлении соответствующего запроса предоставьте подтверждение многофакторной проверки подлинности и выполните описанные действия.</span><span class="sxs-lookup"><span data-stu-id="b86de-176">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="b86de-177">Попробуйте получить доступ к приложению еще раз.</span><span class="sxs-lookup"><span data-stu-id="b86de-177">Try again to access the application.</span></span>


<span data-ttu-id="b86de-178">**Обновление Windows 10 от ноября 2015 г. (версия 1511):**</span><span class="sxs-lookup"><span data-stu-id="b86de-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="b86de-179">Откройте приложение **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="b86de-179">Open the **Settings** app.</span></span>
2. <span data-ttu-id="b86de-180">Щелкните **Учетные записи** > **Ваши учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="b86de-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="b86de-181">Щелкните **Добавить рабочую или учебную учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="b86de-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="b86de-182">Пройдите проверку подлинности в организации, при появлении соответствующего запроса предоставьте подтверждение многофакторной проверки подлинности и выполните описанные действия.</span><span class="sxs-lookup"><span data-stu-id="b86de-182">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="b86de-183">Попробуйте получить доступ к приложению еще раз.</span><span class="sxs-lookup"><span data-stu-id="b86de-183">Try again to access the application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="b86de-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b86de-184">Next steps</span></span>
[<span data-ttu-id="b86de-185">Условный доступ в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b86de-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

