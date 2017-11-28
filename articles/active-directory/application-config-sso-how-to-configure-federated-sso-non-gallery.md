---
title: "aaaHow tooconfigure федеративного единого входа для приложения не коллекции | Документы Microsoft"
description: "Как tooconfigure федеративного единого входа для пользовательского приложения без коллекции, которые должны toointegrate с Azure AD"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e14f9-103">Как tooconfigure федеративного единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="e14f9-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e14f9-104">tooconfigure приложения не коллекции требуется toohave Azure AD premium и SAML 2.0 поддерживает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="e14f9-105">Дополнительные сведения о версиях Azure AD см. в разделе [Цены на Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="e14f9-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="e14f9-106">Обзор необходимых действий</span><span class="sxs-lookup"><span data-stu-id="e14f9-106">Overview of steps required</span></span>
<span data-ttu-id="e14f9-107">Ниже приведен общий обзор hello действия требуется tooconfigure федеративного единого входа для не коллекции (например, пользовательские) приложения.</span><span class="sxs-lookup"><span data-stu-id="e14f9-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="e14f9-108">Настройка значения метаданных приложения hello в Azure AD (вход, URL-адрес ответа URL-адрес, идентификатор)</span><span class="sxs-lookup"><span data-stu-id="e14f9-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="e14f9-109">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="e14f9-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="e14f9-110">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="e14f9-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="e14f9-111">Настройка значения метаданных Azure AD в приложение hello (вход, URL-адрес, издателя, URL-адрес выхода и сертификата)</span><span class="sxs-lookup"><span data-stu-id="e14f9-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="e14f9-112">Назначить пользователей toohello приложения</span><span class="sxs-lookup"><span data-stu-id="e14f9-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="e14f9-113">Настройка единого входа toonon коллекции приложений</span><span class="sxs-lookup"><span data-stu-id="e14f9-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="e14f9-114">tooconfigure единого входа для приложения, которое не находится в коллекции hello Azure AD, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e14f9-115">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="e14f9-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e14f9-116">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="e14f9-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e14f9-117">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="e14f9-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e14f9-118">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e14f9-119">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="e14f9-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="e14f9-120">Нажмите кнопку **приложения коллекции не** в hello **добавить собственное приложение** раздела</span><span class="sxs-lookup"><span data-stu-id="e14f9-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="e14f9-121">Введите имя приложения hello hello в hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="e14f9-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="e14f9-122">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e14f9-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="e14f9-123">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="e14f9-124">Выберите **входа на базе SAML** в hello **режим** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="e14f9-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="e14f9-125">Введите значения требуется hello в **URL-адреса и домена.**</span><span class="sxs-lookup"><span data-stu-id="e14f9-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="e14f9-126">Вы должны получить эти значения с поставщиком приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="e14f9-127">приложение hello tooconfigure как единый вход, инициированный IdP, введите URL-адрес ответа hello и hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="e14f9-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="e14f9-128">**Необязательно:** tooconfigure приложения hello в виде единого входа, инициированные SP, hello входа на URL-адрес является обязательным.</span><span class="sxs-lookup"><span data-stu-id="e14f9-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="e14f9-129">В hello **атрибуты пользователя**, выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="e14f9-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="e14f9-130">**Необязательно:** щелкните **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="e14f9-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="e14f9-131">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="e14f9-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="e14f9-132">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="e14f9-132">click **Add attribute**.</span></span> <span data-ttu-id="e14f9-133">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="e14f9-134">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e14f9-134">Click **Save.**</span></span> <span data-ttu-id="e14f9-135">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="e14f9-136">Нажмите кнопку **Настройка &lt;имя_приложения&gt;**  tooaccess документацию по tooconfigure единого входа в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="e14f9-137">Кроме того имеет URL-адреса Azure AD и сертификат, необходимый для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="e14f9-138">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="e14f9-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="e14f9-139">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="e14f9-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="e14f9-140">tooselect hello идентификатор пользователя или добавление атрибутов пользователя, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e14f9-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="e14f9-141">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="e14f9-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e14f9-142">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="e14f9-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e14f9-143">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="e14f9-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e14f9-144">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e14f9-145">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="e14f9-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e14f9-146">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="e14f9-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e14f9-147">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="e14f9-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e14f9-148">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e14f9-149">В разделе hello **атрибуты пользователя** выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="e14f9-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="e14f9-150">Hello выбранного параметра должен toomatch hello ожидаемое значение в tooauthenticate hello hello приложения пользователя.</span><span class="sxs-lookup"><span data-stu-id="e14f9-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="e14f9-151">[! Обратите внимание,} Azure AD выберите формат hello для атрибута NameID hello (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="e14f9-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="e14f9-152">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) под hello статьи политики идентификатора имени.</span><span class="sxs-lookup"><span data-stu-id="e14f9-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="e14f9-153">атрибуты пользователя tooadd, нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="e14f9-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="e14f9-154">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="e14f9-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="e14f9-155">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="e14f9-155">click **Add attribute**.</span></span> <span data-ttu-id="e14f9-156">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="e14f9-157">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e14f9-157">Click **Save.**</span></span> <span data-ttu-id="e14f9-158">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="e14f9-159">Загрузка метаданных Azure AD hello или сертификат</span><span class="sxs-lookup"><span data-stu-id="e14f9-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="e14f9-160">метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="e14f9-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="e14f9-161">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="e14f9-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e14f9-162">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="e14f9-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e14f9-163">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="e14f9-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e14f9-164">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e14f9-165">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="e14f9-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="e14f9-166">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="e14f9-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e14f9-167">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="e14f9-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e14f9-168">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e14f9-169">Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца.</span><span class="sxs-lookup"><span data-stu-id="e14f9-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="e14f9-170">В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="e14f9-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="e14f9-171">Azure AD не предоставляет метаданных hello tooget URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e14f9-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="e14f9-172">Hello метаданные могут быть получены только как XML-файл.</span><span class="sxs-lookup"><span data-stu-id="e14f9-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="e14f9-173">Назначить пользователей toohello приложения</span><span class="sxs-lookup"><span data-stu-id="e14f9-173">Assign users toohello application</span></span>

<span data-ttu-id="e14f9-174">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e14f9-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="e14f9-175">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="e14f9-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e14f9-176">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="e14f9-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e14f9-177">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="e14f9-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e14f9-178">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e14f9-179">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="e14f9-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e14f9-180">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="e14f9-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e14f9-181">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="e14f9-182">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e14f9-183">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="e14f9-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e14f9-184">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="e14f9-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e14f9-185">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="e14f9-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e14f9-186">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="e14f9-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="e14f9-187">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="e14f9-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="e14f9-188">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="e14f9-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="e14f9-189">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="e14f9-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="e14f9-190">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="e14f9-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="e14f9-191">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="e14f9-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="e14f9-192">После краткого периода времени hello пользователей, которые вы выбрали быть может toolaunch эти приложения используют hello методов, описанных в разделе описания решений hello.</span><span class="sxs-lookup"><span data-stu-id="e14f9-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="e14f9-193">Настройка утверждений SAML, hello отправлено tooan приложения</span><span class="sxs-lookup"><span data-stu-id="e14f9-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="e14f9-194">toolearn toocustomize hello SAML атрибут отправлять утверждений приложения tooyour разделе [утверждения сопоставления в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="e14f9-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e14f9-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e14f9-195">Next steps</span></span>
[<span data-ttu-id="e14f9-196">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="e14f9-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
