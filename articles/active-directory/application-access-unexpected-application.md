---
title: "aaaUnexpected приложения в списке приложений | Документы Microsoft"
description: "Как toosee все приложения в клиенте и понять, как приложения отображаются в списке всех приложений в группе корпоративных приложений"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="627a7-103">Неожиданные приложения в списке приложений</span><span class="sxs-lookup"><span data-stu-id="627a7-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="627a7-104">В этой статье помогут toounderstand отображением приложений в вашей **все приложения** в разделе **корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="627a7-104">This article help you toounderstand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-toosee-all-applications-in-your-tenant"></a><span data-ttu-id="627a7-105">Как toosee все приложения в клиенте</span><span class="sxs-lookup"><span data-stu-id="627a7-105">How toosee all applications in your tenant</span></span>

<span data-ttu-id="627a7-106">toosee все Здравствуйте приложения в клиенте, необходимо toouse hello **фильтра** управления tooshow **все приложения** под hello **всех приложений** списка.</span><span class="sxs-lookup"><span data-stu-id="627a7-106">toosee all hello applications in your tenant, you need toouse hello **Filter** control tooshow **All Applications** under hello **All Applications** list.</span></span> <span data-ttu-id="627a7-107">toodo это, выполните hello шаги:</span><span class="sxs-lookup"><span data-stu-id="627a7-107">toodo this, follow hello steps below:</span></span>

1.  <span data-ttu-id="627a7-108">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="627a7-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="627a7-109">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="627a7-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="627a7-110">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="627a7-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="627a7-111">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="627a7-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="627a7-112">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="627a7-112">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="627a7-113">Нажмите кнопку hello используйте hello **фильтра** управления вверху hello hello **список всех приложений**.</span><span class="sxs-lookup"><span data-stu-id="627a7-113">click hello use hello **Filter** control at hello top of hello **All Applications List**.</span></span>

7.  <span data-ttu-id="627a7-114">На hello **фильтра** колонки, набор hello **Показать** параметр слишком**всех приложений.**</span><span class="sxs-lookup"><span data-stu-id="627a7-114">On hello **Filter** blade, set hello **Show** option too**All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="627a7-115">Почему приложение появляется в моем списке всех приложений?</span><span class="sxs-lookup"><span data-stu-id="627a7-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="627a7-116">При фильтрации слишком**все приложения**, hello **все приложения** **списка** отображается каждый объект субъекта-службы в клиенте.</span><span class="sxs-lookup"><span data-stu-id="627a7-116">When filtered too**All Applications**, hello **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="627a7-117">Объекты участников-служб могут попадать в этот список разными способами.</span><span class="sxs-lookup"><span data-stu-id="627a7-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="627a7-118">При добавлении любого приложения из галереи приложения hello, включая:</span><span class="sxs-lookup"><span data-stu-id="627a7-118">When you add any application from hello application gallery, including:</span></span>

   1. <span data-ttu-id="627a7-119">**Приложения из коллекции Azure AD** — это предварительно интегрированные приложения для единого входа через Azure AD.</span><span class="sxs-lookup"><span data-stu-id="627a7-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="627a7-120">**Прокси-сервер приложений-приложения** — приложения, работающего в локальной среде, которые должны tooprovide безопасный единый вход в tooexternally.</span><span class="sxs-lookup"><span data-stu-id="627a7-120">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

   3. <span data-ttu-id="627a7-121">**Сторонних разрабатываемых приложений** — приложение, ваша организация хочет toodevelop на hello платформы разработки приложений Azure AD, но который еще не существует.</span><span class="sxs-lookup"><span data-stu-id="627a7-121">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="627a7-122">**Приложения не из коллекции** — собственные приложения.</span><span class="sxs-lookup"><span data-stu-id="627a7-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="627a7-123">Любой веб-ссылка нужные или любого приложения, в которой отображается поле имени пользователя и пароля, поддерживает протокол SAML или OpenID Connect или поддерживает SCIM, который вы хотите toointegrate для единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="627a7-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="627a7-124">При регистрации или входе в систему<sup> в п</sup>риложении стороннего разработчика, интегрированном с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="627a7-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="627a7-125">Примерами таких приложений являются [Smartsheet](https://app.smartsheet.com/b/home) или [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="627a7-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="627a7-126">При регистрации, или добавление tooa лицензии пользователя или группы tooa первой стороной приложения, таких как [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="627a7-126">When signing up for, or adding a license tooa user or a group tooa first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="627a7-127">При добавлении новой записи регистрации приложения, создав сторонних разрабатываемых приложений, с помощью hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="627a7-127">When you add a new application registration by creating a custom-developed application using hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="627a7-128">При добавлении новой записи регистрации приложения, создав сторонних разрабатываемых приложений, с помощью hello [портала регистрации приложения V2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="627a7-128">When you add a new application registration by creating a custom-developed application using hello [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="627a7-129">При добавлении приложения, которое вы разрабатываете с помощью [методов аутентификации ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) или [подключенных служб](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="627a7-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="627a7-130">При создании объекта участника службы с помощью hello [модуля Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="627a7-130">When you create a service principal object using hello [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="627a7-131">Когда вы [согласия приложения tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) виде toouse администратора в клиенте.</span><span class="sxs-lookup"><span data-stu-id="627a7-131">When you [consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator toouse data in your tenant.</span></span>

9.  <span data-ttu-id="627a7-132">Когда [согласии пользователя приложение tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse данных в клиенте.</span><span class="sxs-lookup"><span data-stu-id="627a7-132">When a [user consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse data in your tenant.</span></span>

10. <span data-ttu-id="627a7-133">При включении определенных служб, которые хранят данные в клиенте.</span><span class="sxs-lookup"><span data-stu-id="627a7-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="627a7-134">Примером этого может сбросить пароль, который моделируется как toostore участника службы для сброса пароля политики безопасно.</span><span class="sxs-lookup"><span data-stu-id="627a7-134">One example of this is Password Reset, which is modeled as a service principal toostore your password reset policy securely.</span></span>

<span data-ttu-id="627a7-135">прочитать дополнительные сведения о приложениях способ добавления каталога tooyour tooget [как и почему приложения добавляются tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="627a7-135">tooget more details on how apps are added tooyour directory, read [How and why applications are added tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a><span data-ttu-id="627a7-136">Я хочу tooremove приложения tooan назначения определенного пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="627a7-136">I want tooremove a specific user’s or group’s assignment tooan application</span></span>

<span data-ttu-id="627a7-137">tooremove пользователь или группа назначения tooan приложении, выполните действия hello, перечисленные в hello [удалить назначение пользователя или группу из корпоративного приложения в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) статьи.</span><span class="sxs-lookup"><span data-stu-id="627a7-137">tooremove a user or group assignment tooan application, follow hello steps listed in hello [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a><span data-ttu-id="627a7-138">Я хочу toodisable все приложения tooan доступа для каждого пользователя</span><span class="sxs-lookup"><span data-stu-id="627a7-138">I want toodisable all access tooan application for every user</span></span>

<span data-ttu-id="627a7-139">toodisable все приложение tooan входа в систему пользователя, выполните шаги hello, указанные в hello [отключить пользователя войти в приложение в Azure Active Directory предприятия](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) статьи.</span><span class="sxs-lookup"><span data-stu-id="627a7-139">toodisable all user sign-ins tooan application, follow hello steps listed in hello [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-toodelete-an-application-entirely"></a><span data-ttu-id="627a7-140">Я хочу toodelete приложение полностью</span><span class="sxs-lookup"><span data-stu-id="627a7-140">I want toodelete an application entirely</span></span>

<span data-ttu-id="627a7-141">слишком**удалить приложение**, следуйте приведенным ниже инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="627a7-141">too**delete an application**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="627a7-142">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="627a7-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="627a7-143">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="627a7-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="627a7-144">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="627a7-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="627a7-145">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="627a7-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="627a7-146">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="627a7-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="627a7-147">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="627a7-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="627a7-148">Выберите hello приложение toodelete.</span><span class="sxs-lookup"><span data-stu-id="627a7-148">Select hello application you want toodelete.</span></span>

7.  <span data-ttu-id="627a7-149">После загрузки приложения hello щелкните **удалить** значок в верхнем приложения hello **Обзор** колонку.</span><span class="sxs-lookup"><span data-stu-id="627a7-149">Once hello application loads, click **Delete** icon from hello top application’s **Overview** blade.</span></span>

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a><span data-ttu-id="627a7-150">Я хочу toodisable все будущие пользовательского согласия операций tooany приложения</span><span class="sxs-lookup"><span data-stu-id="627a7-150">I want toodisable all future user consent operations tooany application</span></span>

<span data-ttu-id="627a7-151">Отключение согласие пользователя для конечных пользователей из приложения tooany соглашаетесь предотвратить всего каталога.</span><span class="sxs-lookup"><span data-stu-id="627a7-151">Disabling user consent for your entire directory prevent end users from consenting tooany application.</span></span> <span data-ttu-id="627a7-152">Администратор сохранит возможность предоставлять согласие от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="627a7-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="627a7-153">согласие toolearn Дополнительные сведения о приложении, и почему может или не можете toodo, прочитайте [пользователя понимание и согласие администратора](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="627a7-153">toolearn more about application consent, and why you may or may not wish toodo this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="627a7-154">слишком**отключить все операции согласия будущих пользователя в каталоге всей**, следуйте приведенным ниже инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="627a7-154">too**disable all future user consent operations in your entire directory**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="627a7-155">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="627a7-155">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="627a7-156">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="627a7-156">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="627a7-157">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="627a7-157">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="627a7-158">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="627a7-158">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="627a7-159">Щелкните **Параметры пользователя**.</span><span class="sxs-lookup"><span data-stu-id="627a7-159">click **User settings**.</span></span>

6.  <span data-ttu-id="627a7-160">Отключите все операции согласия пользователя в будущем, установка hello **пользователи разрешают приложениям tooaccess свои данные** переключения слишком**нет** и нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="627a7-160">Disable all future user consent operations by setting hello **Users can allow apps tooaccess their data** toggle too**No** and click hello **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="627a7-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="627a7-161">Next steps</span></span>
[<span data-ttu-id="627a7-162">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="627a7-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
