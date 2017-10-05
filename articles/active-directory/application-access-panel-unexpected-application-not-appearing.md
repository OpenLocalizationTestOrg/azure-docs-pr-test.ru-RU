---
title: "Назначенное приложение не отображается на панели доступа | Документы Майкрософт"
description: "Устранение неполадки с отображением приложения на панели доступа"
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
ms.openlocfilehash: 9ea5744d77b90929598ea5feb80c7bbdff3772fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="80d08-103">Назначенное приложение не отображается на панели доступа</span><span class="sxs-lookup"><span data-stu-id="80d08-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="80d08-104">Панель доступа — это веб-портал, позволяющий пользователям с рабочей или учебной учетной записью Azure Active Directory (Azure AD) просматривать и запускать облачные приложения, к которым администратор Azure AD предоставил доступ</span><span class="sxs-lookup"><span data-stu-id="80d08-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="80d08-105">Эти приложения настраиваются от имени пользователя на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80d08-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="80d08-106">Чтобы пользователь видел приложение на панели доступа, оно должно быть правильно настроено и назначено пользователю или группе, к которой он относится.</span><span class="sxs-lookup"><span data-stu-id="80d08-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="80d08-107">Типы приложений, которые может видеть пользователь, делятся на следующие категории:</span><span class="sxs-lookup"><span data-stu-id="80d08-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="80d08-108">приложения Office 365;</span><span class="sxs-lookup"><span data-stu-id="80d08-108">Office 365 Applications</span></span>

-   <span data-ttu-id="80d08-109">приложения Майкрософт и сторонние приложения с единым входом на основе федерации;</span><span class="sxs-lookup"><span data-stu-id="80d08-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="80d08-110">приложения с единым входом на основе паролей;</span><span class="sxs-lookup"><span data-stu-id="80d08-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="80d08-111">приложения с существующими решениями единого входа.</span><span class="sxs-lookup"><span data-stu-id="80d08-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="80d08-112">Общие проблемы, которые следует проверить в первую очередь</span><span class="sxs-lookup"><span data-stu-id="80d08-112">General issues to check first</span></span>

-   <span data-ttu-id="80d08-113">Если приложение было только что добавлено для пользователя, попробуйте выйти и снова войти в систему через несколько минут, чтобы увидеть, не появилось ли приложение на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="80d08-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="80d08-114">Если лицензия была только что удалена для пользователя или группы, в которую он входит, внесение изменений может занять много времени в зависимости от размера и сложности группы.</span><span class="sxs-lookup"><span data-stu-id="80d08-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="80d08-115">Подождите некоторое время, прежде чем входить на панель доступа.</span><span class="sxs-lookup"><span data-stu-id="80d08-115">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="80d08-116">Проблемы, связанные с настройкой приложения</span><span class="sxs-lookup"><span data-stu-id="80d08-116">Problems related to application configuration</span></span>

<span data-ttu-id="80d08-117">Приложение может не отображаться на панели доступа пользователя из-за неправильной настройки.</span><span class="sxs-lookup"><span data-stu-id="80d08-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="80d08-118">Ниже описываются некоторые способы устранения неполадок, связанных с настройкой приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="80d08-119">Настройка федеративного единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="80d08-120">Настройка федеративного единого входа для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="80d08-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="80d08-121">Настройка единого входа по паролю для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="80d08-122">Настройка единого входа по паролю для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="80d08-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="80d08-123">Настройка федеративного единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="80d08-124">Для всех приложений в коллекции Azure AD, для которых включен корпоративный единый вход, доступны пошаговые руководства.</span><span class="sxs-lookup"><span data-stu-id="80d08-124">All applications in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="80d08-125">Подробное пошаговое руководство можно найти в [списке учебников по интеграции приложений SaaS с Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="80d08-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="80d08-126">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="80d08-127">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="80d08-128">Указание значений метаданных приложения в Azure AD (URL-адрес для входа, идентификатор, URL-адрес ответа)</span><span class="sxs-lookup"><span data-stu-id="80d08-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="80d08-129">Выбор идентификатора пользователя и добавление атрибутов пользователей, которые будут отправлены в приложение</span><span class="sxs-lookup"><span data-stu-id="80d08-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="80d08-130">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="80d08-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="80d08-131">Указание значений метаданных Azure AD в приложении (URL-адрес для входа, издатель, URL-адрес для выхода и сертификат)</span><span class="sxs-lookup"><span data-stu-id="80d08-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="80d08-132">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="80d08-133">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-134">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="80d08-135">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-136">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-137">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="80d08-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-138">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="80d08-139">Введите имя приложения в текстовом поле **Введите имя** в разделе **Добавить из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="80d08-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="80d08-140">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="80d08-141">Перед добавлением приложения можно изменить его имя в текстовом поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="80d08-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="80d08-142">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="80d08-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="80d08-143">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="80d08-144">Настройка единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="80d08-145">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-146">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80d08-147">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-148">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-149">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-150">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="80d08-151">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-152">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="80d08-153">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-154">В раскрывающемся списке **Режим** выберите пункт **Вход на основе SAML**.</span><span class="sxs-lookup"><span data-stu-id="80d08-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="80d08-155">Введите необходимые значения в поле **Домены и URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="80d08-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="80d08-156">Их можно получить у поставщика приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="80d08-157">Чтобы настроить единый вход, инициированный поставщиком услуг, обязательно укажите URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="80d08-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="80d08-158">Для некоторых приложений также нужно указать идентификатор.</span><span class="sxs-lookup"><span data-stu-id="80d08-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="80d08-159">Чтобы настроить единый вход, инициированный поставщиком удостоверений, введите URL-адрес для ответа.</span><span class="sxs-lookup"><span data-stu-id="80d08-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="80d08-160">Для некоторых приложений также нужно указать идентификатор.</span><span class="sxs-lookup"><span data-stu-id="80d08-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="80d08-161">**Необязательно:** щелкните **Показать дополнительные параметры URL-адресов**, чтобы увидеть необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="80d08-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="80d08-162">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="80d08-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="80d08-163">**Необязательно:** щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="80d08-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="80d08-164">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-164">To add an attribute:</span></span>

   1. <span data-ttu-id="80d08-165">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="80d08-165">click **Add attribute**.</span></span> <span data-ttu-id="80d08-166">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="80d08-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="80d08-167">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-167">click **Save.**</span></span> <span data-ttu-id="80d08-168">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="80d08-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="80d08-169">Щелкните **Настроить &lt;имя приложения&gt;**, чтобы открыть документацию по настройке единого входа для приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="80d08-170">Кроме того, для настройки единого входа для приложения также потребуются URL-адреса метаданных и сертификат.</span><span class="sxs-lookup"><span data-stu-id="80d08-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="80d08-171">Чтобы сохранить конфигурацию, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-171">click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="80d08-172">Назначьте пользователей приложению.</span><span class="sxs-lookup"><span data-stu-id="80d08-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="80d08-173">Выберите идентификатор пользователя и добавьте атрибуты пользователя, которые будут отправлены в приложение.</span><span class="sxs-lookup"><span data-stu-id="80d08-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="80d08-174">Чтобы выбрать идентификатор пользователя или добавить атрибуты пользователя, выполните указанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="80d08-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-175">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80d08-176">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-177">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-178">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-179">Щелкните **Все приложения** для просмотра списка всех приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="80d08-180">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-181">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="80d08-182">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-183">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="80d08-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="80d08-184">Выбранный параметр должен соответствовать ожидаемому значению для проверки подлинности пользователя в приложении.</span><span class="sxs-lookup"><span data-stu-id="80d08-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="80d08-185">Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="80d08-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="80d08-186">Дополнительные сведения см. в разделе NameIDPolicy статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="80d08-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="80d08-187">Чтобы добавить атрибуты пользователя, щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="80d08-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="80d08-188">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-188">To add an attribute:</span></span>

   1. <span data-ttu-id="80d08-189">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="80d08-189">click **Add attribute**.</span></span> <span data-ttu-id="80d08-190">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="80d08-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="80d08-191">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-191">click **Save.**</span></span> <span data-ttu-id="80d08-192">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="80d08-192">You will see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="80d08-193">Скачивание метаданных Azure AD или сертификата</span><span class="sxs-lookup"><span data-stu-id="80d08-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="80d08-194">Чтобы скачать метаданные приложения или сертификат в Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="80d08-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-195">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80d08-196">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-197">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-198">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-199">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="80d08-200">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-201">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="80d08-202">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-203">Перейдите в раздел **Сертификат подписи SAML** и выберите значение в столбце **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="80d08-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="80d08-204">В зависимости от того, что именно требуется для настройки единого входа, вы сможете скачать XML-файл метаданных или сертификат.</span><span class="sxs-lookup"><span data-stu-id="80d08-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="80d08-205">Azure AD не предоставляет URL-адреса для получения метаданных.</span><span class="sxs-lookup"><span data-stu-id="80d08-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="80d08-206">Метаданные можно скачать только в виде XML-файла.</span><span class="sxs-lookup"><span data-stu-id="80d08-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="80d08-207">Настройка федеративного единого входа для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="80d08-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="80d08-208">Чтобы настроить приложение не из коллекции, вам потребуется Azure AD Premium, а приложение должно поддерживать SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="80d08-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="80d08-209">Дополнительные сведения о версиях Azure AD см. в разделе [Цены на Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="80d08-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="80d08-210">Указание значений метаданных приложения в Azure AD (URL-адрес для входа, идентификатор, URL-адрес ответа)</span><span class="sxs-lookup"><span data-stu-id="80d08-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="80d08-211">Выбор идентификатора пользователя и добавление атрибутов пользователей, которые будут отправлены в приложение</span><span class="sxs-lookup"><span data-stu-id="80d08-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="80d08-212">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="80d08-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="80d08-213">Указание значений метаданных Azure AD в приложении (URL-адрес для входа, издатель, URL-адрес для выхода и сертификат)</span><span class="sxs-lookup"><span data-stu-id="80d08-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="80d08-214">Указание значений метаданных приложения в Azure AD (URL-адрес для входа, идентификатор, URL-адрес ответа)</span><span class="sxs-lookup"><span data-stu-id="80d08-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="80d08-215">Чтобы настроить единый вход для приложения, которое не находится в коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-216">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80d08-217">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-218">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-219">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="80d08-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-220">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="80d08-221">В разделе **Добавление собственного приложения** щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="80d08-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="80d08-222">Введите имя приложения в поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="80d08-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="80d08-223">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="80d08-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="80d08-224">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="80d08-225">Выберите **Единый вход на основе SAML** в раскрывающемся списке **Режим**.</span><span class="sxs-lookup"><span data-stu-id="80d08-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="80d08-226">Введите необходимые значения в поле **Домены и URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="80d08-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="80d08-227">Их можно получить у поставщика приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="80d08-228">Чтобы настроить единый вход, инициированный поставщиком удостоверений, введите URL-адрес ответа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="80d08-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="80d08-229">**Необязательно:** чтобы настроить единый вход, инициированный поставщиком услуг, обязательно укажите URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="80d08-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="80d08-230">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="80d08-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="80d08-231">**Необязательно:** щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="80d08-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="80d08-232">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-232">To add an attribute:</span></span>

   1. <span data-ttu-id="80d08-233">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="80d08-233">click **Add attribute**.</span></span> <span data-ttu-id="80d08-234">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="80d08-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="80d08-235">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-235">Click **Save.**</span></span> <span data-ttu-id="80d08-236">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="80d08-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="80d08-237">Щелкните **Настроить &lt;имя приложения&gt;**, чтобы открыть документацию по настройке единого входа для приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="80d08-238">Кроме того, у вас есть URL-адреса Azure AD и сертификат, необходимые для приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="80d08-239">Выберите идентификатор пользователя и добавьте атрибуты пользователя, которые будут отправлены в приложение.</span><span class="sxs-lookup"><span data-stu-id="80d08-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="80d08-240">Чтобы выбрать идентификатор пользователя или добавить атрибуты пользователя, выполните указанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="80d08-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-241">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80d08-242">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-243">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-244">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-245">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="80d08-246">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-247">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="80d08-248">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-249">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="80d08-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="80d08-250">Выбранный параметр должен соответствовать ожидаемому значению для проверки подлинности пользователя в приложении.</span><span class="sxs-lookup"><span data-stu-id="80d08-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="80d08-251">Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="80d08-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="80d08-252">Дополнительные сведения см. в разделе NameIDPolicy статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="80d08-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="80d08-253">Чтобы добавить атрибуты пользователя, щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="80d08-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="80d08-254">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-254">To add an attribute:</span></span>

   1. <span data-ttu-id="80d08-255">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="80d08-255">click **Add attribute**.</span></span> <span data-ttu-id="80d08-256">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="80d08-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="80d08-257">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-257">Click **Save.**</span></span> <span data-ttu-id="80d08-258">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="80d08-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="80d08-259">Скачивание метаданных Azure AD или сертификата</span><span class="sxs-lookup"><span data-stu-id="80d08-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="80d08-260">Чтобы скачать метаданные приложения или сертификат в Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="80d08-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-261">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80d08-262">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-263">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-264">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-265">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="80d08-266">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-267">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="80d08-268">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-269">Перейдите в раздел **Сертификат подписи SAML** и выберите значение в столбце **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="80d08-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="80d08-270">В зависимости от того, что именно требуется для настройки единого входа, вы сможете скачать XML-файл метаданных или сертификат.</span><span class="sxs-lookup"><span data-stu-id="80d08-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="80d08-271">Azure AD не предоставляет URL-адреса для получения метаданных.</span><span class="sxs-lookup"><span data-stu-id="80d08-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="80d08-272">Метаданные можно скачать только в виде XML-файла.</span><span class="sxs-lookup"><span data-stu-id="80d08-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="80d08-273">Настройка единого входа по паролю для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="80d08-274">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="80d08-275">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="80d08-276">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="80d08-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="80d08-277">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d08-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="80d08-278">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-279">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="80d08-280">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-281">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-282">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="80d08-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-283">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="80d08-284">Введите имя приложения в текстовом поле **Введите имя** в разделе **Добавить из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="80d08-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="80d08-285">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="80d08-286">Перед добавлением приложения можно изменить его имя в текстовом поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="80d08-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="80d08-287">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="80d08-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="80d08-288">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="80d08-289">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="80d08-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="80d08-290">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-291">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80d08-292">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-293">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-294">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-295">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="80d08-296">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-297">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="80d08-298">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-299">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="80d08-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="80d08-300">[Назначьте пользователей приложению](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="80d08-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="80d08-301">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="80d08-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="80d08-302">В противном случае пользователям будет предложено ввести учетные данные при запуске.</span><span class="sxs-lookup"><span data-stu-id="80d08-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="80d08-303">Настройка единого входа по паролю для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="80d08-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="80d08-304">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="80d08-305">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="80d08-305">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="80d08-306">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="80d08-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="80d08-307">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="80d08-307">Add a non-gallery application</span></span>

<span data-ttu-id="80d08-308">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-309">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="80d08-310">Откройте **расширение Azure Active Directory**, щелкнув **Дополнительные службы** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-311">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-312">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="80d08-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-313">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="80d08-314">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="80d08-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="80d08-315">Введите имя приложения в текстовое поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="80d08-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="80d08-316">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-316">Select **Add.**</span></span>

<span data-ttu-id="80d08-317">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="80d08-318">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="80d08-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="80d08-319">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-320">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="80d08-321">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-322">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-323">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-324">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="80d08-325">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-326">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="80d08-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="80d08-327">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-328">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="80d08-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="80d08-329">Введите **URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="80d08-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="80d08-330">Это URL-адрес страницы, на которой пользователи вводят имена и пароли для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="80d08-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="80d08-331">Убедитесь, что на странице по этому URL-адресу отображаются поля для ввода учетных данных.</span><span class="sxs-lookup"><span data-stu-id="80d08-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="80d08-332">[Назначьте пользователей приложению](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="80d08-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="80d08-333">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="80d08-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="80d08-334">В противном случае пользователям будет предложено ввести учетные данные при запуске.</span><span class="sxs-lookup"><span data-stu-id="80d08-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="80d08-335">Проблемы, связанные с назначением приложений пользователям</span><span class="sxs-lookup"><span data-stu-id="80d08-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="80d08-336">Пользователь может не видеть приложение на панели доступа из-за того, что приложение не назначено ему.</span><span class="sxs-lookup"><span data-stu-id="80d08-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="80d08-337">Ниже приведены некоторые способы проверки.</span><span class="sxs-lookup"><span data-stu-id="80d08-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="80d08-338">Проверка того, назначено ли приложение пользователю</span><span class="sxs-lookup"><span data-stu-id="80d08-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="80d08-339">Назначение приложения пользователю напрямую</span><span class="sxs-lookup"><span data-stu-id="80d08-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="80d08-340">Проверка того, назначена ли пользователю лицензия, связанная с приложением</span><span class="sxs-lookup"><span data-stu-id="80d08-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="80d08-341">Назначение лицензии пользователю</span><span class="sxs-lookup"><span data-stu-id="80d08-341">How to assign a license to a user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="80d08-342">Проверка того, назначено ли приложение пользователю</span><span class="sxs-lookup"><span data-stu-id="80d08-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="80d08-343">Чтобы проверить, назначено ли приложение пользователю, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="80d08-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-344">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80d08-345">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-346">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-347">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-348">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="80d08-349">Выполните **поиск** по имени нужного приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="80d08-350">Выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="80d08-351">Проверьте, назначено ли приложение пользователю.</span><span class="sxs-lookup"><span data-stu-id="80d08-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="80d08-352">Если нет, назначьте его, выполнив инструкции в разделе "Назначение приложения пользователю напрямую".</span><span class="sxs-lookup"><span data-stu-id="80d08-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="80d08-353">Назначение приложения пользователю напрямую</span><span class="sxs-lookup"><span data-stu-id="80d08-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="80d08-354">Чтобы напрямую назначить одного или нескольких пользователей для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-355">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="80d08-356">Откройте **расширение Azure Active Directory**, щелкнув **Дополнительные службы** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-357">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-358">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-359">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="80d08-360">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-361">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="80d08-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="80d08-362">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-363">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="80d08-364">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="80d08-365">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="80d08-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="80d08-366">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="80d08-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="80d08-367">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="80d08-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="80d08-368">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="80d08-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="80d08-369">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="80d08-370">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="80d08-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="80d08-371">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="80d08-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="80d08-372">Вскоре выбранные пользователи смогут запускать это приложение на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="80d08-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="80d08-373">Проверка того, назначена ли пользователю лицензия, связанная с приложением</span><span class="sxs-lookup"><span data-stu-id="80d08-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="80d08-374">Чтобы проверить назначенные пользователю лицензии, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-375">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80d08-376">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-377">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-378">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="80d08-379">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="80d08-379">click **All users**.</span></span>

6.  <span data-ttu-id="80d08-380">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="80d08-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="80d08-381">Чтобы просмотреть лицензии, которые в настоящее время назначены пользователю, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="80d08-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="80d08-382">Если пользователю назначена лицензия Office, на его панели доступа будут отображаться основные приложения Office.</span><span class="sxs-lookup"><span data-stu-id="80d08-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="80d08-383">Назначение лицензии пользователю</span><span class="sxs-lookup"><span data-stu-id="80d08-383">How to assign a user a license</span></span> 

<span data-ttu-id="80d08-384">Чтобы назначить лицензию пользователю, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-385">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80d08-386">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-387">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-388">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="80d08-389">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="80d08-389">click **All users**.</span></span>

6.  <span data-ttu-id="80d08-390">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="80d08-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="80d08-391">Чтобы просмотреть лицензии, которые в настоящее время назначены пользователю, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="80d08-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="80d08-392">Нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="80d08-393">Выберите **один или несколько продуктов** в списке доступных продуктов.</span><span class="sxs-lookup"><span data-stu-id="80d08-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="80d08-394">**Необязательно:** чтобы назначить отдельные продукты, щелкните элемент **Параметры назначения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="80d08-395">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="80d08-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="80d08-396">Чтобы назначить выбранные лицензии пользователю, нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="80d08-397">Проблемы, связанные с назначением приложений группам</span><span class="sxs-lookup"><span data-stu-id="80d08-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="80d08-398">Пользователь может видеть приложение на панели доступа, если он входит в группу, которой назначено это приложение.</span><span class="sxs-lookup"><span data-stu-id="80d08-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="80d08-399">Ниже приведены некоторые способы проверки.</span><span class="sxs-lookup"><span data-stu-id="80d08-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="80d08-400">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="80d08-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="80d08-401">Назначение приложения группе напрямую</span><span class="sxs-lookup"><span data-stu-id="80d08-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="80d08-402">Проверка вхождения пользователя в группу, которой назначена лицензия</span><span class="sxs-lookup"><span data-stu-id="80d08-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="80d08-403">Назначение лицензии группе</span><span class="sxs-lookup"><span data-stu-id="80d08-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="80d08-404">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="80d08-404">Check a user’s group memberships</span></span>

<span data-ttu-id="80d08-405">Чтобы проверить членство в группе, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-406">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80d08-407">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-408">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-409">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="80d08-410">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="80d08-410">click **All users**.</span></span>

6.  <span data-ttu-id="80d08-411">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="80d08-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="80d08-412">Щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-412">click **Groups**.</span></span>

8.  <span data-ttu-id="80d08-413">Проверьте, входит ли пользователь в группу, которой назначено приложение.</span><span class="sxs-lookup"><span data-stu-id="80d08-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="80d08-414">Чтобы удалить пользователя из группы, **щелкните строку** группы и выберите команду удаления.</span><span class="sxs-lookup"><span data-stu-id="80d08-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="80d08-415">Назначение приложения группе напрямую</span><span class="sxs-lookup"><span data-stu-id="80d08-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="80d08-416">Чтобы напрямую назначить приложение одной или нескольким группам, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-417">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="80d08-418">Откройте **расширение Azure Active Directory**, щелкнув **Дополнительные службы** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-419">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-420">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80d08-421">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="80d08-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="80d08-422">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80d08-423">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="80d08-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="80d08-424">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80d08-425">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="80d08-426">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="80d08-427">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя группы**, которой требуется назначить приложение.</span><span class="sxs-lookup"><span data-stu-id="80d08-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="80d08-428">Наведите указатель мыши на **группу** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="80d08-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="80d08-429">Чтобы добавить группу в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этой группы.</span><span class="sxs-lookup"><span data-stu-id="80d08-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="80d08-430">**Необязательно.** Если вы хотите **добавить более одной группы**, в поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя группы** и установите флажок, чтобы добавить группу в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="80d08-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="80d08-431">Выбрав все группы, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="80d08-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="80d08-432">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным группам.</span><span class="sxs-lookup"><span data-stu-id="80d08-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="80d08-433">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным группам.</span><span class="sxs-lookup"><span data-stu-id="80d08-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="80d08-434">Вскоре выбранные пользователи смогут запускать это приложение на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="80d08-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="80d08-435">Проверка вхождения пользователя в группу, которой назначена лицензия</span><span class="sxs-lookup"><span data-stu-id="80d08-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="80d08-436">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80d08-437">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-438">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-439">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="80d08-440">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="80d08-440">click **All users**.</span></span>

6.  <span data-ttu-id="80d08-441">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="80d08-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="80d08-442">Щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-442">click **Groups**.</span></span>

8.  <span data-ttu-id="80d08-443">Щелкните строку определенной группы.</span><span class="sxs-lookup"><span data-stu-id="80d08-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="80d08-444">Чтобы просмотреть лицензии, которые назначены группе, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="80d08-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="80d08-445">Если группе назначена лицензия Office, на панели доступа пользователя могут отображаться некоторые основные приложения Office.</span><span class="sxs-lookup"><span data-stu-id="80d08-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="80d08-446">Назначение лицензии группе</span><span class="sxs-lookup"><span data-stu-id="80d08-446">How to assign a license to a group</span></span>

<span data-ttu-id="80d08-447">Чтобы назначить лицензию группе, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80d08-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="80d08-448">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="80d08-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80d08-449">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="80d08-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80d08-450">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80d08-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80d08-451">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="80d08-452">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="80d08-452">click **All groups**.</span></span>

6.  <span data-ttu-id="80d08-453">**Найдите** нужную группу и выберите ее, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="80d08-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="80d08-454">Чтобы просмотреть лицензии, которые в настоящее время назначены группе, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="80d08-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="80d08-455">Нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="80d08-456">Выберите **один или несколько продуктов** в списке доступных продуктов.</span><span class="sxs-lookup"><span data-stu-id="80d08-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="80d08-457">**Необязательно:** чтобы назначить отдельные продукты, щелкните элемент **Параметры назначения**.</span><span class="sxs-lookup"><span data-stu-id="80d08-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="80d08-458">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="80d08-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="80d08-459">Чтобы назначить выбранные лицензии группе, нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="80d08-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="80d08-460">Это действие может занять много времени в зависимости от размера и сложности группы.</span><span class="sxs-lookup"><span data-stu-id="80d08-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="80d08-461">Чтобы ускорить процесс, можно временно назначить лицензию пользователю напрямую.</span><span class="sxs-lookup"><span data-stu-id="80d08-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="80d08-462">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80d08-462">Next steps</span></span>
[<span data-ttu-id="80d08-463">Добавление новых пользователей в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80d08-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

