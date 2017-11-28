---
title: "Azure AD Connect: простой единый вход — быстрый запуск| Документы Майкрософт"
description: "В этой статье описывается, как приступить к работе простым единым входом в Azure Active Directory."
services: active-directory
keywords: "что такое Azure AD Connect, установка Active Directory, необходимые компоненты для Azure AD, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="069c2-104">Простой единый вход Azure Active Directory — быстрый запуск</span><span class="sxs-lookup"><span data-stu-id="069c2-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-to-deploy-seamless-sso"></a><span data-ttu-id="069c2-105">Как развернуть простой единый вход</span><span class="sxs-lookup"><span data-stu-id="069c2-105">How to deploy Seamless SSO</span></span>

<span data-ttu-id="069c2-106">Простой единый вход Azure Active Directory автоматически обеспечивает пользователям вход в систему, когда они работают на корпоративных компьютерах, подключенных к корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="069c2-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected to your corporate network.</span></span> <span data-ttu-id="069c2-107">Данная функция предоставляет пользователям удобный доступ к облачным приложениям и не требует установки каких-либо дополнительных локальных компонентов.</span><span class="sxs-lookup"><span data-stu-id="069c2-107">It provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="069c2-108">Функция простого единого входа находится на этапе предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="069c2-108">The Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="069c2-109">Чтобы развернуть прозрачный единый вход, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="069c2-109">To deploy Seamless SSO, you need to follow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="069c2-110">Шаг 1. Проверка предварительных требований</span><span class="sxs-lookup"><span data-stu-id="069c2-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="069c2-111">Выполните указанные ниже предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="069c2-111">Ensure that the following prerequisites are in place:</span></span>

1. <span data-ttu-id="069c2-112">Настройка сервера Azure AD Connect. Если в качестве метода входа вы используете [сквозную проверку подлинности](active-directory-aadconnect-pass-through-authentication.md), никакие дополнительные действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="069c2-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="069c2-113">Если в качестве метода входа вы используете [синхронизацию хэша паролей](active-directory-aadconnectsync-implement-password-synchronization.md) и между Azure AD Connect и Azure AD существует брандмауэр, убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="069c2-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="069c2-114">Вы используете версию 1.1.484.0 или более позднюю версию Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="069c2-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="069c2-115">Azure AD Connect может взаимодействовать с URL-адресами `*.msappproxy.net` и через порт 443.</span><span class="sxs-lookup"><span data-stu-id="069c2-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="069c2-116">Это предварительное условие применяется только в том случае, если включить функцию, но не для входа в систему пользователей.</span><span class="sxs-lookup"><span data-stu-id="069c2-116">This prerequisite is applicable only when you enable the feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="069c2-117">Azure AD Connect может устанавливать прямые IP-подключения к [диапазонам IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="069c2-117">Azure AD Connect can make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="069c2-118">Это предварительное условие применяется только в том случае, если включить функцию.</span><span class="sxs-lookup"><span data-stu-id="069c2-118">Again, this prerequisite is applicable only when you enable the feature.</span></span>
2. <span data-ttu-id="069c2-119">Вам будут нужны учетные данные администратора домена для каждого леса AD, который синхронизируется с Azure AD (с помощью Azure AD Connect) и для пользователей которого необходимо включить простой единый вход.</span><span class="sxs-lookup"><span data-stu-id="069c2-119">You need Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="069c2-120">Шаг 2. Включение компонента</span><span class="sxs-lookup"><span data-stu-id="069c2-120">Step 2: Enable the feature</span></span>

<span data-ttu-id="069c2-121">Простой единый вход можно включить с помощью [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="069c2-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="069c2-122">В случае выполнения новой установки Azure AD Connect выберите [пользовательский путь установки](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="069c2-122">If you are doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="069c2-123">На странице "Вход пользователя" установите флажок "Включить единый вход".</span><span class="sxs-lookup"><span data-stu-id="069c2-123">At the "User sign-in" page, check the "Enable single sign on" option.</span></span>

![Azure AD Connect: страница "Вход пользователя"](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="069c2-125">Если уже имеется установленный экземпляр Azure AD Connect, выберите страницу "Смена имени пользователя для входа" в Azure AD Connect и нажмите кнопку "Далее".</span><span class="sxs-lookup"><span data-stu-id="069c2-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="069c2-126">Затем установите флажок "Включить единый вход".</span><span class="sxs-lookup"><span data-stu-id="069c2-126">Then check the "Enable single sign on" option.</span></span>

![Azure AD Connect: страница "Смена имени пользователя для входа"](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="069c2-128">Следуйте указаниям мастера, пока не дойдете до страницы "Включение единого входа".</span><span class="sxs-lookup"><span data-stu-id="069c2-128">Continue through the wizard until you get to the "Enable single sign on" page.</span></span> <span data-ttu-id="069c2-129">Введите учетные данные администратора домена для каждого леса AD, который синхронизируется с Azure AD (с помощью Azure AD Connect) и для пользователей которого необходимо включить простой единый вход.</span><span class="sxs-lookup"><span data-stu-id="069c2-129">Provide Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span> 

<span data-ttu-id="069c2-130">После завершения работы мастера на вашем клиенте будет включен простой единый вход.</span><span class="sxs-lookup"><span data-stu-id="069c2-130">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="069c2-131">Учетные данные администратора домена не хранятся в Azure AD Connect или в Azure AD, но используются только для включения функции.</span><span class="sxs-lookup"><span data-stu-id="069c2-131">The Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used to enable the feature.</span></span>

<span data-ttu-id="069c2-132">Выполните следующие инструкции, чтобы проверить, правильно ли включен простой единый вход.</span><span class="sxs-lookup"><span data-stu-id="069c2-132">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="069c2-133">Войдите в [центр администрирования Azure Active Directory](https://aad.portal.azure.com), используя учетные данные глобального администратора для клиента.</span><span class="sxs-lookup"><span data-stu-id="069c2-133">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="069c2-134">В области навигации слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="069c2-134">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="069c2-135">Выберите **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="069c2-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="069c2-136">Убедитесь, что функция **Эффективный единый вход** **включена**.</span><span class="sxs-lookup"><span data-stu-id="069c2-136">Verify that the **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Портал Azure — колонка Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="069c2-138">Шаг 3. Развертывание компонента</span><span class="sxs-lookup"><span data-stu-id="069c2-138">Step 3: Roll out the feature</span></span>

<span data-ttu-id="069c2-139">Чтобы развернуть функцию для пользователей, вам понадобится добавить два URL-адреса Azure AD (https://autologon.microsoftazuread-sso.com и https://aadg.windows.net.nsatc.net) в параметры зоны интрасети пользователей с помощью групповой политики в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="069c2-139">To roll out the feature to your users, you need to add two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) to users' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="069c2-140">Следующие инструкции подходят только для Internet Explorer и Google Chrome Windows (при условии, что этот браузер использует тот же набор URL-адресов доверенных сайтов, что и Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="069c2-140">The following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="069c2-141">В следующем разделе приведены инструкции по настройке Mozilla Firefox и Google Chrome на Mac.</span><span class="sxs-lookup"><span data-stu-id="069c2-141">Read the next section for instructions to set up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="069c2-142">Зачем нужно изменять параметры зоны интрасети пользователей?</span><span class="sxs-lookup"><span data-stu-id="069c2-142">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="069c2-143">По умолчанию браузер автоматически вычисляет соответствующую зону (Интернета или интрасети) по URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="069c2-143">By default, the browser automatically calculates the right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="069c2-144">Например, http://contoso/ сопоставляется с зоной интрасети, а http://intranet.contoso.com/ — с зоной Интернета (так как этот URL-адрес содержит точку).</span><span class="sxs-lookup"><span data-stu-id="069c2-144">For example, http://contoso/ is mapped to the Intranet zone, whereas http://intranet.contoso.com/ is mapped to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="069c2-145">Браузеры не отправляют билеты Kerberos в облачную конечную точку (как два URL-адреса Azure AD), если только ее URL-адрес не добавлен явным образом в зону интрасети в браузере.</span><span class="sxs-lookup"><span data-stu-id="069c2-145">Browsers don't send Kerberos tickets to a cloud endpoint - like the two Azure AD URLs - unless its URL is explicitly added to the browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="069c2-146">Подробные инструкции</span><span class="sxs-lookup"><span data-stu-id="069c2-146">Detailed steps</span></span>

1. <span data-ttu-id="069c2-147">Откройте средства управления групповыми политиками.</span><span class="sxs-lookup"><span data-stu-id="069c2-147">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="069c2-148">Измените групповую политику, которая применяется к некоторым или всем пользователям.</span><span class="sxs-lookup"><span data-stu-id="069c2-148">Edit the Group Policy that is applied to some or all your users.</span></span> <span data-ttu-id="069c2-149">В данном примере используется **политика домена по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="069c2-149">In this example, we use the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="069c2-150">Перейдите в раздел **Конфигурация пользователя\Административные шаблоны\Компоненты Windows\Internet Explorer\Панель управления браузером\Вкладка безопасности** и выберите **Список назначений зоны для веб-сайтов**.</span><span class="sxs-lookup"><span data-stu-id="069c2-150">Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List**.</span></span>
<span data-ttu-id="069c2-151">![Единый вход](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="069c2-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="069c2-152">Включите политику и введите следующие значения (URL-адреса Azure AD, на которые пересылаются билеты Kerberos) и данные (*1* указывает зону интрасети) в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="069c2-152">Enable the policy, and enter the following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in the dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="069c2-153">Если вы хотите запретить отдельным пользователям использовать простой единый вход, например, если эти пользователи выполняют вход на общедоступных киосках, установите для указанных выше параметров значение *4*.</span><span class="sxs-lookup"><span data-stu-id="069c2-153">If you want to disallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set the preceding values to *4*.</span></span> <span data-ttu-id="069c2-154">Это действие добавляет URL-адреса Azure AD в зону с ограниченным доступом и блокирует все попытки прозрачного единого входа.</span><span class="sxs-lookup"><span data-stu-id="069c2-154">This action adds the Azure AD URLs to the Restricted Zone, and fails Seamless SSO all the time.</span></span>

5. <span data-ttu-id="069c2-155">Нажмите кнопку **ОК**, затем нажмите кнопку **ОК** еще раз.</span><span class="sxs-lookup"><span data-stu-id="069c2-155">Click **OK** and **OK** again.</span></span>

![Единый вход](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="069c2-157">Рекомендации для браузера</span><span class="sxs-lookup"><span data-stu-id="069c2-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="069c2-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="069c2-158">Mozilla Firefox</span></span>

<span data-ttu-id="069c2-159">Mozilla Firefox автоматически не выполняет проверку подлинности Kerberos.</span><span class="sxs-lookup"><span data-stu-id="069c2-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="069c2-160">Каждый пользователь должен вручную добавить URL-адреса Azure AD в параметры Firefox, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="069c2-160">Each user has to manually add the Azure AD URLs to their Firefox settings using the following steps:</span></span>
1. <span data-ttu-id="069c2-161">Запустите Firefox и введите `about:config` в адресной строке.</span><span class="sxs-lookup"><span data-stu-id="069c2-161">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="069c2-162">Проигнорируйте все отображаемые уведомления.</span><span class="sxs-lookup"><span data-stu-id="069c2-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="069c2-163">Найдите параметр **network.negotiate-auth.trusted-uris**.</span><span class="sxs-lookup"><span data-stu-id="069c2-163">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="069c2-164">Этот параметр выводит список доверенных сайтов в Firefox для проверки подлинности Kerberos.</span><span class="sxs-lookup"><span data-stu-id="069c2-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="069c2-165">Щелкните правой кнопкой мыши и выберите "Изменить".</span><span class="sxs-lookup"><span data-stu-id="069c2-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="069c2-166">Введите в поле "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net".</span><span class="sxs-lookup"><span data-stu-id="069c2-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in the field.</span></span>
5. <span data-ttu-id="069c2-167">Нажмите кнопку "ОК" и снова откройте браузер.</span><span class="sxs-lookup"><span data-stu-id="069c2-167">Click "OK" and reopen the browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="069c2-168">Safari в Mac OS</span><span class="sxs-lookup"><span data-stu-id="069c2-168">Safari on Mac OS</span></span>

<span data-ttu-id="069c2-169">Убедитесь, что компьютер под управлением Mac OS присоединен к AD.</span><span class="sxs-lookup"><span data-stu-id="069c2-169">Ensure that the machine running Mac OS is joined to AD.</span></span> <span data-ttu-id="069c2-170">Инструкции о том, как это сделать, см. [здесь](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="069c2-170">See instructions on how to do that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="069c2-171">Google Chrome в Mac OS</span><span class="sxs-lookup"><span data-stu-id="069c2-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="069c2-172">Процедуру добавления в белый список URL-адресов Azure AD для встроенной проверки подлинности в Google Chrome на Mac OS и платформах, отличных от Windows, см. в [этой статье](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist).</span><span class="sxs-lookup"><span data-stu-id="069c2-172">For Google Chrome on Mac OS and other non-Windows platforms, refer to [this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="069c2-173">Применение сторонних расширений групповой политики Active Directory для развертывания URL-адресов Azure AD для Firefox и Google Chrome на платформе Mac в этой статье не рассматривается.</span><span class="sxs-lookup"><span data-stu-id="069c2-173">Using third-party Active Directory Group Policy extensions to roll out the Azure AD URLs to Firefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="069c2-174">Известные ограничения</span><span class="sxs-lookup"><span data-stu-id="069c2-174">Known limitations</span></span>

<span data-ttu-id="069c2-175">Простой единый вход не работает в конфиденциальном режиме просмотра в браузерах Firefox и Edge,</span><span class="sxs-lookup"><span data-stu-id="069c2-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="069c2-176">а также в Internet Explorer, если браузер работает в режиме усиленной защиты.</span><span class="sxs-lookup"><span data-stu-id="069c2-176">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="069c2-177">Мы недавно выполнили откат поддержки Edge, чтобы найти причину проблем, о которых сообщили клиенты.</span><span class="sxs-lookup"><span data-stu-id="069c2-177">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="069c2-178">Шаг 4. Тестирование компонента</span><span class="sxs-lookup"><span data-stu-id="069c2-178">Step 4: Test the feature</span></span>

<span data-ttu-id="069c2-179">Чтобы проверить функцию для конкретного пользователя, убедитесь, что соблюдаются _все_ следующие условия:</span><span class="sxs-lookup"><span data-stu-id="069c2-179">To test the feature for a specific user, ensure that _all_ the following conditions are in place:</span></span>
  - <span data-ttu-id="069c2-180">Пользователь выполняет вход на корпоративном устройстве.</span><span class="sxs-lookup"><span data-stu-id="069c2-180">The user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="069c2-181">Это устройство должно быть присоединено к домену Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="069c2-181">The device has been previously joined to your Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="069c2-182">У него должно быть прямое подключение к контроллеру домена по корпоративной проводной или беспроводной сети или через подключение удаленного доступа, например VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="069c2-182">The device has a direct connection to your Domain Controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="069c2-183">Вы [развернули функцию](##step-3-roll-out-the-feature) для этого пользователя с помощью групповой политики.</span><span class="sxs-lookup"><span data-stu-id="069c2-183">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user using Group Policy.</span></span>

<span data-ttu-id="069c2-184">Для тестирования сценария, когда пользователь вводит только имя пользователя, но не пароль.</span><span class="sxs-lookup"><span data-stu-id="069c2-184">To test the scenario where the user enters only the username, but not the password:</span></span>
- <span data-ttu-id="069c2-185">Войдите на *https://myapps.microsoft.com/* в новом частном сеансе браузера.</span><span class="sxs-lookup"><span data-stu-id="069c2-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="069c2-186">Для тестирования сценария, когда пользователю не нужно вводить имя пользователя или пароль.</span><span class="sxs-lookup"><span data-stu-id="069c2-186">To test the scenario where the user doesn't have to enter the username or the password:</span></span> 
- <span data-ttu-id="069c2-187">Войдите на *https://myapps.microsoft.com/contoso.onmicrosoft.com* в новом частном сеансе браузера.</span><span class="sxs-lookup"><span data-stu-id="069c2-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="069c2-188">Введите вместо "*contoso*" имя своего клиента.</span><span class="sxs-lookup"><span data-stu-id="069c2-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="069c2-189">Или войдите на *https://myapps.microsoft.com/contoso.com* в новом частном сеансе браузера.</span><span class="sxs-lookup"><span data-stu-id="069c2-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="069c2-190">Введите вместо "*contoso.com*" проверенный домен (не федеративный домен) в клиенте.</span><span class="sxs-lookup"><span data-stu-id="069c2-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="069c2-191">Шаг 5. Смена ключей</span><span class="sxs-lookup"><span data-stu-id="069c2-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="069c2-192">На шаге 2 Azure AD Connect создает учетные записи компьютеров (представляющие Azure AD) во всех лесах AD, для которых включен простой единый вход.</span><span class="sxs-lookup"><span data-stu-id="069c2-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="069c2-193">Дополнительные сведения см. [здесь](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="069c2-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="069c2-194">Для повышения безопасности мы рекомендуем часто менять ключи расшифровки Kerberos этих учетных записей компьютеров.</span><span class="sxs-lookup"><span data-stu-id="069c2-194">For improved security, it is recommended that  you frequently roll over the Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="069c2-195">Этот шаг не требуется выполнять _немедленно_ после включения функции.</span><span class="sxs-lookup"><span data-stu-id="069c2-195">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="069c2-196">Меняйте ключи расшифровки Kerberos по крайней мере каждые 30 дней.</span><span class="sxs-lookup"><span data-stu-id="069c2-196">Roll over the Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="069c2-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="069c2-197">Next steps</span></span>

- <span data-ttu-id="069c2-198">[**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-sso-how-it-works.md). Сведения о том, как работает эта функция.</span><span class="sxs-lookup"><span data-stu-id="069c2-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="069c2-199">[**Часто задаваемые вопросы**](active-directory-aadconnect-sso-faq.md). Ответы на часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="069c2-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="069c2-200">[**Устранение неполадок**](active-directory-aadconnect-troubleshoot-sso.md). Узнайте, как устранить самые распространенные проблемы с этой функцией.</span><span class="sxs-lookup"><span data-stu-id="069c2-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="069c2-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="069c2-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
