---
title: "вход в веб-сайте панель доступа toohello aaaProblem | Документы Microsoft"
description: "Руководство по tootroubleshoot проблемы, которые могут возникнуть при попытке toosign в toouse hello панели доступа"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="49bde-103">Ошибка при входе на веб-сайте панель доступа toohello</span><span class="sxs-lookup"><span data-stu-id="49bde-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="49bde-104">Hello панель доступа является Интернет-порталом, который дает возможность пользователя, имеющего рабочей или учебной учетной записи в Azure Active Directory (Azure AD) tooview и запуск облачных приложений, администратор hello Azure AD предоставил им доступ к.</span><span class="sxs-lookup"><span data-stu-id="49bde-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="49bde-105">Пользователь, имеющий выпуски Azure AD можно также использовать группы самообслуживания и возможности управления приложениями через панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="49bde-106">Панель доступа Hello отделен от hello портал Azure и не требует toohave пользователей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="49bde-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="49bde-107">Пользователи могут войти в toohello панели доступа, если они имеют рабочей или учебной учетной записи в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49bde-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="49bde-108">Проверку подлинности пользователей можно выполнять с помощью Azure AD напрямую,</span><span class="sxs-lookup"><span data-stu-id="49bde-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="49bde-109">с использованием служб федерации Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="49bde-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="49bde-110">или Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49bde-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="49bde-111">Если пользователю подписки для Azure или Office 365 и использующий hello портал Azure или приложения Office 365, они будут toouse может легко hello панели доступа без необходимости снова toosign в.</span><span class="sxs-lookup"><span data-stu-id="49bde-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="49bde-112">Пользователи не проходят проверку подлинности быть запрашиваемые toosign в с помощью hello имя пользователя и пароль для своей учетной записи в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49bde-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="49bde-113">Если hello организации есть настроенная служба федерации, достаточно ввести имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="49bde-114">Общие проблемы toocheck сначала</span><span class="sxs-lookup"><span data-stu-id="49bde-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="49bde-115">Убедитесь, что пользователь hello, вход toohello **исправьте URL-адрес**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="49bde-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="49bde-116">Убедитесь, что браузер пользователя hello добавил hello URL-адрес tooits **надежные сайты**</span><span class="sxs-lookup"><span data-stu-id="49bde-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="49bde-117">Убедитесь, что учетная запись пользователя hello **включен** для входа.</span><span class="sxs-lookup"><span data-stu-id="49bde-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="49bde-118">Убедитесь, что учетная запись пользователя hello **не заблокирована.**</span><span class="sxs-lookup"><span data-stu-id="49bde-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="49bde-119">Убедитесь, что пользователь hello **не просрочен или забудете пароль.**</span><span class="sxs-lookup"><span data-stu-id="49bde-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="49bde-120">Проверьте, не блокирует ли **Многофакторная Идентификация** доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="49bde-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="49bde-121">Убедитесь, что **политика условного доступа** или политика **защиты идентификации** не блокирует доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="49bde-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="49bde-122">Убедитесь, что пользователь **контактные сведения для проверки подлинности** работает toodate tooallow многофакторной проверки подлинности или условного доступа политики toobe принудительно.</span><span class="sxs-lookup"><span data-stu-id="49bde-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="49bde-123">Убедитесь, что tooalso try очистки файлов cookie в браузере и повторить попытку toosign в.</span><span class="sxs-lookup"><span data-stu-id="49bde-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="49bde-124">Соответствующие требования к браузеру для hello панели доступа</span><span class="sxs-lookup"><span data-stu-id="49bde-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="49bde-125">Hello панели доступа требуется браузер, поддерживающий JavaScript и CSS включена.</span><span class="sxs-lookup"><span data-stu-id="49bde-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="49bde-126">toouse паролю единого входа (SSO) в панели доступа, hello расширение панели доступа hello должны устанавливаться в браузере пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="49bde-127">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="49bde-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="49bde-128">Для единого входа по паролю может быть браузеров hello конечных пользователей:</span><span class="sxs-lookup"><span data-stu-id="49bde-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="49bde-129">Internet Explorer 8, 9, 10, 11 (в Windows 7 или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="49bde-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="49bde-130">Edge в Windows 10 Anniversary Edition или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="49bde-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="49bde-131">Chrome (начиная с Windows 7 и Mac OS X);</span><span class="sxs-lookup"><span data-stu-id="49bde-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="49bde-132">Firefox 26.0 и более поздние версии (начиная с Windows XP с пакетом обновления 2 (SP2) и Mac OS X 10.6).</span><span class="sxs-lookup"><span data-stu-id="49bde-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="49bde-133">Проблемы с учетной записью пользователя hello</span><span class="sxs-lookup"><span data-stu-id="49bde-133">Problems with hello user’s account</span></span>

<span data-ttu-id="49bde-134">Toohello доступа к панели доступа может быть заблокирована из-за tooa проблема с учетной записью пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="49bde-135">Ниже приведены некоторые способы устранения неполадок, связанных с параметрами учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="49bde-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="49bde-136">Проверка существования учетной записи пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49bde-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="49bde-137">Проверка состояния учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="49bde-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="49bde-138">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="49bde-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="49bde-139">Включение самостоятельного сброса пароля</span><span class="sxs-lookup"><span data-stu-id="49bde-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="49bde-140">Проверка состояния службы Многофакторной Идентификации</span><span class="sxs-lookup"><span data-stu-id="49bde-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="49bde-141">Проверка контактной информации для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="49bde-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="49bde-142">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="49bde-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="49bde-143">Проверка назначенных пользователю лицензий</span><span class="sxs-lookup"><span data-stu-id="49bde-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="49bde-144">Назначение лицензии пользователю</span><span class="sxs-lookup"><span data-stu-id="49bde-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="49bde-145">Проверка существования учетной записи пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49bde-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="49bde-146">toocheck, если учетная запись пользователя отсутствует, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="49bde-147">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="49bde-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49bde-148">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="49bde-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49bde-149">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="49bde-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49bde-150">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="49bde-151">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49bde-151">click **All users**.</span></span>

6.  <span data-ttu-id="49bde-152">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="49bde-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="49bde-153">Проверьте свойства hello hello пользователя объекта toobe убедиться, что они выглядят как предполагается, что и данные не отсутствует.</span><span class="sxs-lookup"><span data-stu-id="49bde-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="49bde-154">Проверка состояния учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="49bde-154">Check a user’s account status</span></span>

<span data-ttu-id="49bde-155">toocheck пользователя состояние учетной записи, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="49bde-156">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="49bde-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49bde-157">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="49bde-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49bde-158">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="49bde-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49bde-159">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="49bde-160">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49bde-160">click **All users**.</span></span>

6.  <span data-ttu-id="49bde-161">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="49bde-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="49bde-162">Щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="49bde-162">click **Profile**.</span></span>

8.  <span data-ttu-id="49bde-163">В разделе **параметры** убедитесь, что **входа блока** задано слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="49bde-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="49bde-164">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="49bde-164">Reset a user’s password</span></span>

<span data-ttu-id="49bde-165">tooreset пароль пользователя, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="49bde-166">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="49bde-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49bde-167">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="49bde-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49bde-168">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="49bde-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49bde-169">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="49bde-170">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49bde-170">click **All users**.</span></span>

6.  <span data-ttu-id="49bde-171">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="49bde-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="49bde-172">Нажмите кнопку hello **сброс пароля** кнопку hello верхней части колонки hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="49bde-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="49bde-173">Нажмите кнопку hello **сброс пароля** кнопку на hello **сброс пароля** колонки, отображается.</span><span class="sxs-lookup"><span data-stu-id="49bde-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="49bde-174">Копировать hello **временный пароль** или **ввести новый пароль** для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="49bde-175">Связь этого нового пользователя toohello пароль, они необходимые toochange этот пароль во время следующего входа в tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49bde-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="49bde-176">Включение самостоятельного сброса пароля</span><span class="sxs-lookup"><span data-stu-id="49bde-176">Enable self-service password reset</span></span>

<span data-ttu-id="49bde-177">tooenable пароль самостоятельного сброса, выполните следующие действия развертывания hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="49bde-178">Включение пользователей tooreset свои пароли с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49bde-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="49bde-179">Включить tooreset пользователей или изменить свои пароли в локальной среде Active Directory</span><span class="sxs-lookup"><span data-stu-id="49bde-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="49bde-180">Проверка состояния службы Многофакторной Идентификации</span><span class="sxs-lookup"><span data-stu-id="49bde-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="49bde-181">toocheck пользователь многофакторной проверки подлинности состояние, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="49bde-182">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="49bde-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49bde-183">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="49bde-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49bde-184">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="49bde-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49bde-185">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="49bde-186">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49bde-186">click **All users**.</span></span>

6.  <span data-ttu-id="49bde-187">Нажмите кнопку hello **многофакторной проверки подлинности** кнопку hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="49bde-188">Здравствуйте, один раз **портала администрирования многофакторной проверки подлинности** загрузок, убедитесь в hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="49bde-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="49bde-189">Найти hello пользователя в список пользователей hello, поиск, фильтрацию или сортировку.</span><span class="sxs-lookup"><span data-stu-id="49bde-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="49bde-190">Выберите hello пользователя из списка пользователей hello и **включить**, **отключить**, или **принудительное применение** многофакторной проверки подлинности в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="49bde-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="49bde-191">Если пользователь входит в **принудительно** состоянии, можно установить их слишком**отключено** временно toolet их обратно в свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="49bde-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="49bde-192">После их обратно в, можно изменить свое состояние слишком**включено** снова toorequire их toore-register свои контактные данные во время следующего входа.</span><span class="sxs-lookup"><span data-stu-id="49bde-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="49bde-193">Кроме того, можно выполнить действия hello в hello [проверьте контактные данные для проверки подлинности пользователя](#check-a-users-authentication-contact-info) tooverify или задать для них эти данные.</span><span class="sxs-lookup"><span data-stu-id="49bde-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="49bde-194">Проверка контактной информации для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="49bde-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="49bde-195">toocheck проверку подлинности пользователя с контактные данные, для многофакторной проверки подлинности, условный доступ, защиту учетных данных и сброса пароля, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="49bde-196">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="49bde-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49bde-197">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="49bde-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49bde-198">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="49bde-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49bde-199">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="49bde-200">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49bde-200">click **All users**.</span></span>

6.  <span data-ttu-id="49bde-201">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="49bde-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="49bde-202">Щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="49bde-202">click **Profile**.</span></span>

8.  <span data-ttu-id="49bde-203">Прокрутите список вниз слишком**контактные сведения для проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="49bde-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="49bde-204">**Просмотрите** hello данных, зарегистрированных для пользователя hello и обновление при необходимости.</span><span class="sxs-lookup"><span data-stu-id="49bde-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="49bde-205">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="49bde-205">Check a user’s group memberships</span></span>

<span data-ttu-id="49bde-206">toocheck пользователя членство в группе, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="49bde-207">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="49bde-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49bde-208">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="49bde-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49bde-209">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="49bde-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49bde-210">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="49bde-211">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49bde-211">click **All users**.</span></span>

6.  <span data-ttu-id="49bde-212">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="49bde-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="49bde-213">Нажмите кнопку **группы** toosee, который группирует hello пользователь является членом.</span><span class="sxs-lookup"><span data-stu-id="49bde-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="49bde-214">Проверка назначенных пользователю лицензий</span><span class="sxs-lookup"><span data-stu-id="49bde-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="49bde-215">toocheck пользователя назначить лицензии, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="49bde-216">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="49bde-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49bde-217">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="49bde-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49bde-218">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="49bde-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49bde-219">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="49bde-220">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49bde-220">click **All users**.</span></span>

6.  <span data-ttu-id="49bde-221">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="49bde-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="49bde-222">Нажмите кнопку **лицензий** toosee hello какие лицензии пользователя в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="49bde-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="49bde-223">Назначение лицензии пользователю</span><span class="sxs-lookup"><span data-stu-id="49bde-223">Assign a user a license</span></span> 

<span data-ttu-id="49bde-224">tooassign пользователь tooa лицензии, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="49bde-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="49bde-225">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="49bde-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="49bde-226">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="49bde-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="49bde-227">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="49bde-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="49bde-228">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="49bde-229">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="49bde-229">click **All users**.</span></span>

6.  <span data-ttu-id="49bde-230">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="49bde-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="49bde-231">Нажмите кнопку **лицензий** toosee hello какие лицензии пользователя в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="49bde-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="49bde-232">Нажмите кнопку hello **назначить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="49bde-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="49bde-233">Выберите **один или несколько продуктов** из списка допустимых продуктов hello.</span><span class="sxs-lookup"><span data-stu-id="49bde-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="49bde-234">**Необязательный** щелкните hello **параметры назначения** toogranularly элемента назначить продукты.</span><span class="sxs-lookup"><span data-stu-id="49bde-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="49bde-235">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="49bde-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="49bde-236">Нажмите кнопку hello **назначить** кнопку tooassign toothis эти лицензии пользователя.</span><span class="sxs-lookup"><span data-stu-id="49bde-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="49bde-237">Если эти шаги по устранению неполадок не решат проблему hello</span><span class="sxs-lookup"><span data-stu-id="49bde-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="49bde-238">Откройте запрос в службу поддержки с hello следующую информацию, если они доступны:</span><span class="sxs-lookup"><span data-stu-id="49bde-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="49bde-239">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="49bde-239">Correlation error ID</span></span>

-   <span data-ttu-id="49bde-240">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="49bde-240">UPN (user email address)</span></span>

-   <span data-ttu-id="49bde-241">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="49bde-241">Tenant ID</span></span>

-   <span data-ttu-id="49bde-242">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="49bde-242">Browser type</span></span>

-   <span data-ttu-id="49bde-243">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="49bde-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="49bde-244">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="49bde-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="49bde-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49bde-245">Next steps</span></span>
[<span data-ttu-id="49bde-246">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="49bde-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
