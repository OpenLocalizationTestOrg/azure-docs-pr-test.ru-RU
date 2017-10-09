---
title: "Azure AD Connect: простой единый вход — быстрый запуск| Документы Майкрософт"
description: "В этой статье описывается, как tooget работу с Azure Active Directory прозрачную единого входа."
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="63f64-104">Простой единый вход Azure Active Directory — быстрый запуск</span><span class="sxs-lookup"><span data-stu-id="63f64-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="63f64-105">Как toodeploy прозрачную единого входа</span><span class="sxs-lookup"><span data-stu-id="63f64-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="63f64-106">Azure Active Directory прозрачную единого входа (Azure AD, эффективная SSO) автоматически подписывает пользователей они находятся в своей корпоративной сети подключенных tooyour рабочих станций в организации.</span><span class="sxs-lookup"><span data-stu-id="63f64-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="63f64-107">Он предоставляет удобного доступа пользователей tooyour облачные приложения без необходимости какие-либо дополнительные локальные компоненты.</span><span class="sxs-lookup"><span data-stu-id="63f64-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="63f64-108">компонент Hello прозрачную единого входа в настоящий момент в режиме предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="63f64-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="63f64-109">toodeploy прозрачную единого входа требуется toofollow следующие действия:</span><span class="sxs-lookup"><span data-stu-id="63f64-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="63f64-110">Шаг 1. Проверка предварительных требований</span><span class="sxs-lookup"><span data-stu-id="63f64-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="63f64-111">Убедитесь, что hello следующие необходимые компоненты будут на месте:</span><span class="sxs-lookup"><span data-stu-id="63f64-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="63f64-112">Настройка сервера Azure AD Connect. Если в качестве метода входа вы используете [сквозную проверку подлинности](active-directory-aadconnect-pass-through-authentication.md), никакие дополнительные действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="63f64-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="63f64-113">Если в качестве метода входа вы используете [синхронизацию хэша паролей](active-directory-aadconnectsync-implement-password-synchronization.md) и между Azure AD Connect и Azure AD существует брандмауэр, убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="63f64-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="63f64-114">Вы используете версию 1.1.484.0 или более позднюю версию Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="63f64-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="63f64-115">Azure AD Connect может взаимодействовать с URL-адресами `*.msappproxy.net` и через порт 443.</span><span class="sxs-lookup"><span data-stu-id="63f64-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="63f64-116">Это предварительное условие применимо только в том случае, если включена функция hello, а не для входа в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="63f64-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="63f64-117">Azure AD Connect можно сделать toohello подключения прямых IP [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="63f64-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="63f64-118">Опять же это предварительное условие применимо только в том случае, если включена функция hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="63f64-119">Необходимо иметь учетные данные администратора домена для каждого леса AD синхронизации tooAzure AD (с помощью Azure AD Connect) и для пользователей, для которого требуется tooenable прозрачную единого входа.</span><span class="sxs-lookup"><span data-stu-id="63f64-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="63f64-120">Шаг 2: Включение функции hello</span><span class="sxs-lookup"><span data-stu-id="63f64-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="63f64-121">Простой единый вход можно включить с помощью [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="63f64-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="63f64-122">При выполнении новой установки Azure AD Connect выберите hello [пользовательский путь установки](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="63f64-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="63f64-123">На странице «Вход пользователей» hello установите флажок «Включить единый вход» hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect: страница "Вход пользователя"](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="63f64-125">Если уже имеется установленный экземпляр Azure AD Connect, выберите страницу "Смена имени пользователя для входа" в Azure AD Connect и нажмите кнопку "Далее".</span><span class="sxs-lookup"><span data-stu-id="63f64-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="63f64-126">Затем установите флажок «Включить единый вход» hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect: страница "Смена имени пользователя для входа"](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="63f64-128">Продолжайте работу приветствия мастера, пока не будет получен toohello страницы «Включить единый вход».</span><span class="sxs-lookup"><span data-stu-id="63f64-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="63f64-129">Учетные данные администратора домена для каждого леса AD синхронизации tooAzure AD (с помощью Azure AD Connect) и для пользователей, для которого требуется tooenable прозрачную единого входа.</span><span class="sxs-lookup"><span data-stu-id="63f64-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="63f64-130">После завершения работы мастера hello прозрачную единого входа включена для клиента.</span><span class="sxs-lookup"><span data-stu-id="63f64-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="63f64-131">учетные данные администратора домена Hello не хранятся в Azure AD Connect или в Azure AD, но являются только используемые tooenable функции hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="63f64-132">Выполните эти инструкции tooverify, правильно включено прямое единого входа.</span><span class="sxs-lookup"><span data-stu-id="63f64-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="63f64-133">Войдите в toohello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с hello учетные данные глобального администратора для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="63f64-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="63f64-134">Выберите **Azure Active Directory** на левой навигационной hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="63f64-135">Выберите **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="63f64-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="63f64-136">Убедитесь, что hello **прозрачную Single Sign-On** показано, как функция **включено**.</span><span class="sxs-lookup"><span data-stu-id="63f64-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Портал Azure — колонка Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="63f64-138">Шаг 3: Развертывание функции hello</span><span class="sxs-lookup"><span data-stu-id="63f64-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="63f64-139">tooroll hello функция tooyour пользователей необходимо tooadd два Azure AD URL-адреса (https://autologon.microsoftazuread-sso.com и https://aadg.windows.net.nsatc.net) toousers настроек зоны посредством групповой политики в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="63f64-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="63f64-140">Здравствуйте, следующие инструкции работают, только для Internet Explorer и Google Chrome в Windows (если он использует набор URL-адресов в список надежных узлов с Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="63f64-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="63f64-141">Чтение hello следующего раздела приведены инструкции tooset Mozilla Firefox и Google Chrome на Mac.</span><span class="sxs-lookup"><span data-stu-id="63f64-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="63f64-142">Зачем нужен настроек зоны toomodify пользователей?</span><span class="sxs-lookup"><span data-stu-id="63f64-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="63f64-143">По умолчанию hello браузер автоматически вычисляет hello правой зоны (Интернет или интрасеть) с URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="63f64-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="63f64-144">Например http://contoso/ является сопоставленных toohello интрасеть, тогда как http://intranet.contoso.com/ находится сопоставленных toohello зоны Интернета (hello URL-адрес содержит точку).</span><span class="sxs-lookup"><span data-stu-id="63f64-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="63f64-145">Браузеры не отправлять конечную точку облака билеты Kerberos с tooa - как hello двух Azure AD URL - Если явно добавлен зоны интрасети toohello браузера его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="63f64-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="63f64-146">Подробные инструкции</span><span class="sxs-lookup"><span data-stu-id="63f64-146">Detailed steps</span></span>

1. <span data-ttu-id="63f64-147">Откройте средство управления групповой политикой hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="63f64-148">Измените hello групповой политики, примененные toosome или всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="63f64-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="63f64-149">В этом примере мы используем hello **политика домена по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="63f64-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="63f64-150">Перейдите в слишком**пользователя Конфигурация компьютера\Административные шаблоны\Компоненты Components\Internet пользователи управления Panel\Security страницы** и выберите **сайта tooZone список назначений**.</span><span class="sxs-lookup"><span data-stu-id="63f64-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="63f64-151">![Единый вход](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="63f64-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="63f64-152">Включить политику hello и введите следующие значения (Azure AD URL-адреса, которые пересылаются билеты Kerberos) hello и данные (*1* указывает интрасеть) в диалоговое окно «hello».</span><span class="sxs-lookup"><span data-stu-id="63f64-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="63f64-153">Toodisallow некоторые пользователи из с использованием прозрачную SSO - например, если эти пользователи входят на общей киосках - задайте hello, предшествующий значения слишком*4*.</span><span class="sxs-lookup"><span data-stu-id="63f64-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="63f64-154">Это действие добавляет toohello URL-адреса Azure AD hello ограниченной зоны и происходит сбой прозрачную единый вход постоянно hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="63f64-155">Нажмите кнопку **ОК**, затем нажмите кнопку **ОК** еще раз.</span><span class="sxs-lookup"><span data-stu-id="63f64-155">Click **OK** and **OK** again.</span></span>

![Единый вход](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="63f64-157">Рекомендации для браузера</span><span class="sxs-lookup"><span data-stu-id="63f64-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="63f64-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="63f64-158">Mozilla Firefox</span></span>

<span data-ttu-id="63f64-159">Mozilla Firefox автоматически не выполняет проверку подлинности Kerberos.</span><span class="sxs-lookup"><span data-stu-id="63f64-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="63f64-160">Каждый пользователь имеет toomanually добавить hello Azure AD URL-адреса tootheir Firefox параметры с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="63f64-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="63f64-161">Запустите Firefox и введите `about:config` в адресную строку hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="63f64-162">Проигнорируйте все отображаемые уведомления.</span><span class="sxs-lookup"><span data-stu-id="63f64-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="63f64-163">Поиск hello **network.negotiate auth.trusted идентификаторы URI** предпочтения.</span><span class="sxs-lookup"><span data-stu-id="63f64-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="63f64-164">Этот параметр выводит список доверенных сайтов в Firefox для проверки подлинности Kerberos.</span><span class="sxs-lookup"><span data-stu-id="63f64-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="63f64-165">Щелкните правой кнопкой мыши и выберите "Изменить".</span><span class="sxs-lookup"><span data-stu-id="63f64-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="63f64-166">Введите «https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net» в поле hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="63f64-167">Нажмите кнопку «ОК» и снова откройте браузер hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="63f64-168">Safari в Mac OS</span><span class="sxs-lookup"><span data-stu-id="63f64-168">Safari on Mac OS</span></span>

<span data-ttu-id="63f64-169">Убедитесь, что этого hello компьютера под управлением Mac OS tooAD присоединены к домену.</span><span class="sxs-lookup"><span data-stu-id="63f64-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="63f64-170">См. инструкции о том, как toodo, [здесь](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="63f64-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="63f64-171">Google Chrome в Mac OS</span><span class="sxs-lookup"><span data-stu-id="63f64-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="63f64-172">Google Chrome в Mac OS и других платформах, отличных от Windows, см. в разделе слишком[в этой статье](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) сведения о как toowhitelist hello URL-адреса Azure AD для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="63f64-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="63f64-173">С помощью групповой политики Active Directory сторонних расширений tooroll tooFirefox hello URL-адреса Azure AD и Google Chrome на пользователям Mac не рассматривается в этой статье.</span><span class="sxs-lookup"><span data-stu-id="63f64-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="63f64-174">Известные ограничения</span><span class="sxs-lookup"><span data-stu-id="63f64-174">Known limitations</span></span>

<span data-ttu-id="63f64-175">Простой единый вход не работает в конфиденциальном режиме просмотра в браузерах Firefox и Edge,</span><span class="sxs-lookup"><span data-stu-id="63f64-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="63f64-176">Он также не работает в Internet Explorer, если браузер hello работает в режиме усиленной защиты.</span><span class="sxs-lookup"><span data-stu-id="63f64-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="63f64-177">Мы недавно откат поддержка Edge tooinvestigate устранения проблем клиента.</span><span class="sxs-lookup"><span data-stu-id="63f64-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="63f64-178">Шаг 4: Тестирование функции hello</span><span class="sxs-lookup"><span data-stu-id="63f64-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="63f64-179">функция hello tootest для конкретного пользователя, убедитесь, что _все_ предусмотрены hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="63f64-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="63f64-180">вход пользователя Hello на корпоративных устройств.</span><span class="sxs-lookup"><span data-stu-id="63f64-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="63f64-181">Hello устройства был ранее объединенные tooyour домена Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="63f64-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="63f64-182">Hello устройство имеет прямое подключение tooyour контроллеру домена (DC), hello корпоративной проводной или беспроводной сети или посредством подключения удаленного доступа, таких как VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="63f64-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="63f64-183">У вас есть [распространен функции hello](##step-3-roll-out-the-feature) toothis пользователя, с помощью групповой политики.</span><span class="sxs-lookup"><span data-stu-id="63f64-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="63f64-184">сценарий tootest hello, где hello пользователь вводит только имя пользователя hello, но не hello пароль.</span><span class="sxs-lookup"><span data-stu-id="63f64-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="63f64-185">Войдите на *https://myapps.microsoft.com/* в новом частном сеансе браузера.</span><span class="sxs-lookup"><span data-stu-id="63f64-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="63f64-186">сценарий tootest hello, где hello пользователь не имеет пароля имя пользователя или hello hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="63f64-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="63f64-187">Войдите на *https://myapps.microsoft.com/contoso.onmicrosoft.com* в новом частном сеансе браузера.</span><span class="sxs-lookup"><span data-stu-id="63f64-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="63f64-188">Введите вместо "*contoso*" имя своего клиента.</span><span class="sxs-lookup"><span data-stu-id="63f64-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="63f64-189">Или войдите на *https://myapps.microsoft.com/contoso.com* в новом частном сеансе браузера.</span><span class="sxs-lookup"><span data-stu-id="63f64-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="63f64-190">Введите вместо "*contoso.com*" проверенный домен (не федеративный домен) в клиенте.</span><span class="sxs-lookup"><span data-stu-id="63f64-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="63f64-191">Шаг 5. Смена ключей</span><span class="sxs-lookup"><span data-stu-id="63f64-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="63f64-192">На шаге 2 Azure AD Connect создает учетные записи компьютеров (представляющий Azure AD) во всех лесах hello AD, для которых была включена прозрачную единого входа.</span><span class="sxs-lookup"><span data-stu-id="63f64-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="63f64-193">Дополнительные сведения см. [здесь](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="63f64-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="63f64-194">В целях повышения безопасности рекомендуется, можно часто, наведите курсор на ключи расшифровки Kerberos hello этих учетных записей компьютеров.</span><span class="sxs-lookup"><span data-stu-id="63f64-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="63f64-195">Этот шаг не требуется по toodo _немедленно_ после включения функции hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="63f64-196">Наведите курсор на ключи расшифровки Kerberos hello каждые 30 дней.</span><span class="sxs-lookup"><span data-stu-id="63f64-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63f64-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63f64-197">Next steps</span></span>

- <span data-ttu-id="63f64-198">[**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-sso-how-it-works.md). Сведения о том, как работает эта функция.</span><span class="sxs-lookup"><span data-stu-id="63f64-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="63f64-199">[**Часто задаваемые вопросы** ](active-directory-aadconnect-sso-faq.md) -ответы на вопросы и ответы toofrequently.</span><span class="sxs-lookup"><span data-stu-id="63f64-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="63f64-200">[**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-sso.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.</span><span class="sxs-lookup"><span data-stu-id="63f64-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="63f64-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="63f64-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
