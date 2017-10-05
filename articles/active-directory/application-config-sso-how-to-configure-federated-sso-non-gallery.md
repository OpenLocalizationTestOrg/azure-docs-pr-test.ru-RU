---
title: "Как настроить федеративный единый вход для приложения не из коллекции | Документы Майкрософт"
description: "Как настроить федеративный единый вход для пользовательского приложения не из коллекции, которое вы хотите интегрировать с Azure AD"
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
ms.openlocfilehash: da7bc05c6452cde4d0236806f249559f178dd4e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9f17e-103">Настройка федеративного единого входа для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="9f17e-103">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9f17e-104">Чтобы настроить приложение не из коллекции, вам потребуется Azure AD Premium, а приложение должно поддерживать SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="9f17e-104">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="9f17e-105">Дополнительные сведения о версиях Azure AD см. в разделе [Цены на Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="9f17e-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="9f17e-106">Обзор необходимых действий</span><span class="sxs-lookup"><span data-stu-id="9f17e-106">Overview of steps required</span></span>
<span data-ttu-id="9f17e-107">Ниже приведен общий обзор действий, необходимых для настройки федеративного единого входа для приложения не из коллекции (например, пользовательского приложения).</span><span class="sxs-lookup"><span data-stu-id="9f17e-107">Below is a high level overview of the steps required to configure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="9f17e-108">Указание значений метаданных приложения в Azure AD (URL-адрес для входа, идентификатор, URL-адрес ответа)</span><span class="sxs-lookup"><span data-stu-id="9f17e-108">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="9f17e-109">Выбор идентификатора пользователя и добавление атрибутов пользователей, которые будут отправлены в приложение</span><span class="sxs-lookup"><span data-stu-id="9f17e-109">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="9f17e-110">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="9f17e-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="9f17e-111">Указание значений метаданных Azure AD в приложении (URL-адрес для входа, издатель, URL-адрес для выхода и сертификат)</span><span class="sxs-lookup"><span data-stu-id="9f17e-111">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="9f17e-112">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="9f17e-112">Assign users to the application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-to-non-gallery-applications"></a><span data-ttu-id="9f17e-113">Настройка единого входа для приложений не из коллекции</span><span class="sxs-lookup"><span data-stu-id="9f17e-113">Configuring single sign-on to non-gallery applications</span></span>

<span data-ttu-id="9f17e-114">Чтобы настроить единый вход для приложения, которое не находится в коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9f17e-114">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9f17e-115">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-115">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9f17e-116">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="9f17e-116">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f17e-117">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-117">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f17e-118">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="9f17e-118">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f17e-119">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-119">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="9f17e-120">Щелкните **Приложение не из коллекции** в разделе **Добавление собственного приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-120">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="9f17e-121">Введите имя приложения в поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-121">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="9f17e-122">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="9f17e-122">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="9f17e-123">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-123">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="9f17e-124">Выберите **Единый вход на основе SAML** в раскрывающемся списке **Режим**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-124">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="9f17e-125">Введите необходимые значения в поле **Домены и URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-125">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="9f17e-126">Их можно получить у поставщика приложения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-126">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="9f17e-127">Чтобы настроить единый вход, инициированный поставщиком удостоверений, введите URL-адрес ответа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9f17e-127">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2. <span data-ttu-id="9f17e-128">**Необязательно:** чтобы настроить единый вход, инициированный поставщиком услуг, обязательно укажите URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="9f17e-128">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="9f17e-129">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-129">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="9f17e-130">**Необязательно:** щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="9f17e-130">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9f17e-131">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9f17e-131">To add an attribute:</span></span>

   1. <span data-ttu-id="9f17e-132">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-132">click **Add attribute**.</span></span> <span data-ttu-id="9f17e-133">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="9f17e-133">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9f17e-134">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-134">Click **Save.**</span></span> <span data-ttu-id="9f17e-135">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="9f17e-135">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="9f17e-136">Щелкните **Настроить &lt;имя приложения&gt;**, чтобы открыть документацию по настройке единого входа для приложения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-136">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="9f17e-137">Кроме того, у вас есть URL-адреса Azure AD и сертификат, необходимые для приложения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-137">Also, you has Azure AD URLs and certificate required for the application.</span></span>

15. [<span data-ttu-id="9f17e-138">Назначение пользователей для приложения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-138">Assign users to the application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="9f17e-139">Выберите идентификатор пользователя и добавьте атрибуты пользователя, которые будут отправлены в приложение.</span><span class="sxs-lookup"><span data-stu-id="9f17e-139">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="9f17e-140">Чтобы выбрать идентификатор пользователя или добавить атрибуты пользователя, выполните указанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="9f17e-140">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="9f17e-141">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-141">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9f17e-142">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="9f17e-142">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f17e-143">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-143">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f17e-144">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-144">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f17e-145">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="9f17e-145">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9f17e-146">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-146">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9f17e-147">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="9f17e-147">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9f17e-148">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-148">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9f17e-149">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-149">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="9f17e-150">Выбранный параметр должен соответствовать ожидаемому значению для проверки подлинности пользователя в приложении.</span><span class="sxs-lookup"><span data-stu-id="9f17e-150">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

 ><span data-ttu-id="9f17e-151">[!Примечание} Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="9f17e-151">[!NOTE} Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="9f17e-152">Дополнительные сведения см. в разделе NameIDPolicy статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="9f17e-152">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="9f17e-153">Чтобы добавить атрибуты пользователя, щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="9f17e-153">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9f17e-154">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9f17e-154">To add an attribute:</span></span>

   1. <span data-ttu-id="9f17e-155">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-155">click **Add attribute**.</span></span> <span data-ttu-id="9f17e-156">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="9f17e-156">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9f17e-157">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-157">Click **Save.**</span></span> <span data-ttu-id="9f17e-158">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="9f17e-158">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="9f17e-159">Скачивание метаданных Azure AD или сертификата</span><span class="sxs-lookup"><span data-stu-id="9f17e-159">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="9f17e-160">Чтобы скачать метаданные приложения или сертификат в Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9f17e-160">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="9f17e-161">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-161">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9f17e-162">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="9f17e-162">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f17e-163">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-163">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f17e-164">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-164">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f17e-165">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="9f17e-165">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9f17e-166">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-166">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9f17e-167">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="9f17e-167">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9f17e-168">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-168">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9f17e-169">Перейдите в раздел **Сертификат подписи SAML** и выберите значение в столбце **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-169">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9f17e-170">В зависимости от того, что именно требуется для настройки единого входа, вы сможете скачать XML-файл метаданных или сертификат.</span><span class="sxs-lookup"><span data-stu-id="9f17e-170">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="9f17e-171">Azure AD не предоставляет URL-адреса для получения метаданных.</span><span class="sxs-lookup"><span data-stu-id="9f17e-171">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="9f17e-172">Метаданные можно скачать только в виде XML-файла.</span><span class="sxs-lookup"><span data-stu-id="9f17e-172">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="9f17e-173">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="9f17e-173">Assign users to the application</span></span>

<span data-ttu-id="9f17e-174">Чтобы напрямую назначить одного или нескольких пользователей для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9f17e-174">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9f17e-175">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9f17e-176">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="9f17e-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f17e-177">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f17e-178">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f17e-179">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="9f17e-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9f17e-180">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-180">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9f17e-181">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="9f17e-181">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9f17e-182">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-182">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9f17e-183">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-183">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9f17e-184">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-184">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9f17e-185">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="9f17e-185">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9f17e-186">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-186">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9f17e-187">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="9f17e-187">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9f17e-188">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="9f17e-188">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9f17e-189">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-189">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9f17e-190">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="9f17e-190">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9f17e-191">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="9f17e-191">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="9f17e-192">Через некоторое время выбранные пользователи смогут запускать эти приложения с помощью методов, приведенных в описании решения.</span><span class="sxs-lookup"><span data-stu-id="9f17e-192">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="9f17e-193">Настройка утверждений SAML, отправляемых в приложение</span><span class="sxs-lookup"><span data-stu-id="9f17e-193">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="9f17e-194">Чтобы узнать, как настроить атрибут утверждений SAML, отправляемых в приложение, ознакомьтесь с разделом [Сопоставление утверждений в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping).</span><span class="sxs-lookup"><span data-stu-id="9f17e-194">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f17e-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f17e-195">Next steps</span></span>
[<span data-ttu-id="9f17e-196">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="9f17e-196">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
