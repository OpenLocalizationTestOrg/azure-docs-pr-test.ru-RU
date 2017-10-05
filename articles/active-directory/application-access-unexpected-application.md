---
title: "Неожиданные приложения в списке приложений | Документация Майкрософт"
description: "Сведения о том, как можно увидеть все приложения, представленные в клиенте, и как приложения попадают в список \"Все приложения\" в разделе корпоративных приложений"
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
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="2ad22-103">Неожиданные приложения в списке приложений</span><span class="sxs-lookup"><span data-stu-id="2ad22-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="2ad22-104">Эта статья поможет разобраться, как приложения попадают в список **Все приложения** в разделе **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="2ad22-105">Как просмотреть все приложения в клиенте</span><span class="sxs-lookup"><span data-stu-id="2ad22-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="2ad22-106">Чтобы просмотреть все приложения в клиенте, используйте элемент управления **Фильтр** и выберите режим отображения **Все приложения** для списка **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="2ad22-107">Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="2ad22-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="2ad22-108">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2ad22-109">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2ad22-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2ad22-110">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2ad22-111">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2ad22-112">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="2ad22-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="2ad22-113">Щелкните элемент управления **Фильтр** в верхней части **списка всех приложений**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="2ad22-114">В колонке **Фильтр** установите для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="2ad22-115">Почему приложение появляется в моем списке всех приложений?</span><span class="sxs-lookup"><span data-stu-id="2ad22-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="2ad22-116">Если выбран режим фильтрации **Все приложения**, то в **списке** **Все приложения** отображаются все объекты участников-служб, существующие в клиенте.</span><span class="sxs-lookup"><span data-stu-id="2ad22-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="2ad22-117">Объекты участников-служб могут попадать в этот список разными способами.</span><span class="sxs-lookup"><span data-stu-id="2ad22-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="2ad22-118">При добавлении любого приложения из коллекции приложений, например:</span><span class="sxs-lookup"><span data-stu-id="2ad22-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="2ad22-119">**Приложения из коллекции Azure AD** — это предварительно интегрированные приложения для единого входа через Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ad22-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="2ad22-120">**Приложения прокси приложения** — приложения, работающее в локальной среде, которым необходимо предоставить безопасный единый вход извне.</span><span class="sxs-lookup"><span data-stu-id="2ad22-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="2ad22-121">**Специально разработанные приложения** — приложения, которые ваша организация намерена разработать на платформе разработки приложений Azure AD, но, возможно, они еще находятся на стадии обсуждения.</span><span class="sxs-lookup"><span data-stu-id="2ad22-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="2ad22-122">**Приложения не из коллекции** — собственные приложения.</span><span class="sxs-lookup"><span data-stu-id="2ad22-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="2ad22-123">Сюда относится любая нужная веб-ссылка или любое приложение, отображающее поле имени пользователя и пароля и поддерживающее протоколы SAML, OpenID Connect или систему SCIM, которое нужно интегрировать для единого входа через Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ad22-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="2ad22-124">При регистрации или входе в систему<sup> в п</sup>риложении стороннего разработчика, интегрированном с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ad22-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="2ad22-125">Примерами таких приложений являются [Smartsheet](https://app.smartsheet.com/b/home) или [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ad22-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="2ad22-126">При регистрации или добавлении лицензии для пользователя или группы в приложении корпорации Майкрософт, например [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="2ad22-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="2ad22-127">При добавлении новой регистрации приложения путем создания собственного приложения с помощью [реестра приложений](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="2ad22-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="2ad22-128">При добавлении новой регистрации приложения путем создания собственного приложения с помощью [портала регистрации приложений 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="2ad22-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="2ad22-129">При добавлении приложения, которое вы разрабатываете с помощью [методов аутентификации ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) или [подключенных служб](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ad22-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="2ad22-130">При создании объекта-участника службы с помощью [модуля Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="2ad22-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="2ad22-131">Когда вы, как администратор, предоставляете приложению [согласие](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) на использование данных в клиенте.</span><span class="sxs-lookup"><span data-stu-id="2ad22-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="2ad22-132">Когда [клиент предоставляет приложению согласие](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) на использование данных в клиенте.</span><span class="sxs-lookup"><span data-stu-id="2ad22-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="2ad22-133">При включении определенных служб, которые хранят данные в клиенте.</span><span class="sxs-lookup"><span data-stu-id="2ad22-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="2ad22-134">Примером может служить служба сброса паролей, которая оформлена как участник-служба для безопасного хранения политики сброса паролей.</span><span class="sxs-lookup"><span data-stu-id="2ad22-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="2ad22-135">Чтобы получить дополнительные сведения о том, как приложения добавляются в каталог, изучите статью [Как и почему приложения добавляются в Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="2ad22-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="2ad22-136">Я хочу отменить доступ к приложению для определенного пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="2ad22-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="2ad22-137">Чтобы удалить доступ к приложению, назначенный пользователю или группе, выполните действия, описанные в статье [Удаление назначения доступа к корпоративному приложению для пользователя или группы в предварительной версии Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="2ad22-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="2ad22-138">Я хочу отключить доступ к приложению для всех пользователей</span><span class="sxs-lookup"><span data-stu-id="2ad22-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="2ad22-139">Чтобы отключить вход в приложение для всех пользователей, выполните действия, описанные в статье [Отключение входа пользователя в корпоративное приложение в предварительной версии Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="2ad22-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="2ad22-140">Я хочу полностью удалить приложение</span><span class="sxs-lookup"><span data-stu-id="2ad22-140">I want to delete an application entirely</span></span>

<span data-ttu-id="2ad22-141">Чтобы **удалить приложение**, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="2ad22-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="2ad22-142">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2ad22-143">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2ad22-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2ad22-144">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2ad22-145">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2ad22-146">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="2ad22-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="2ad22-147">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="2ad22-148">Выберите приложение, которое требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="2ad22-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="2ad22-149">После загрузки приложения щелкните значок **Удалить** в колонке **Обзор** для часто используемых приложений.</span><span class="sxs-lookup"><span data-stu-id="2ad22-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="2ad22-150">Я хочу отключить все будущие операции пользователя по предоставлению согласия для всех приложений</span><span class="sxs-lookup"><span data-stu-id="2ad22-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="2ad22-151">Если вы отключите для всего каталога возможность предоставлять согласие, пользователь не сможет согласиться с условиями использования приложения.</span><span class="sxs-lookup"><span data-stu-id="2ad22-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="2ad22-152">Администратор сохранит возможность предоставлять согласие от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="2ad22-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="2ad22-153">Дополнительные сведения о согласии в приложениях и возможных мотивах для его отключения или предоставления см. в разделе [Получение согласия пользователя и администратора](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="2ad22-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="2ad22-154">Чтобы **отключить все будущие операции по предоставлению согласия пользователя во всем каталоге**, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2ad22-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="2ad22-155">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2ad22-156">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2ad22-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2ad22-157">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2ad22-158">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2ad22-159">Щелкните **Параметры пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-159">click **User settings**.</span></span>

6.  <span data-ttu-id="2ad22-160">Отключите все будущие операции пользователей по предоставлению согласия, установив переключатель **Пользователи могут разрешать приложениям доступ к своим данным** в положение **Нет** и нажав кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2ad22-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ad22-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ad22-161">Next steps</span></span>
[<span data-ttu-id="2ad22-162">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ad22-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
