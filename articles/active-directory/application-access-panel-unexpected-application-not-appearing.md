---
title: "назначенный aaaAn приложения не отображаются на панели доступа hello | Документы Microsoft"
description: "Устранение неполадок, поэтому приложения не отображаются в панели доступа hello"
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
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="7f7b7-103">Назначенное приложение не отображаются на панели доступа hello</span><span class="sxs-lookup"><span data-stu-id="7f7b7-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="7f7b7-104">Hello панель доступа является Интернет-порталом, который позволяет пользователю с помощью рабочей или рабочую учетную запись в Azure Active Directory (Azure AD) tooview и запуск облачных приложений, hello администратор Azure AD им предоставлен доступ.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="7f7b7-105">Эти приложения настроены от имени пользователя hello hello портала Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="7f7b7-106">Hello приложения должны быть правильно настроены и назначенный toohello пользователя или пользователя hello группы входит toosee приложения hello в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="7f7b7-107">Тип приложения, которые пользователь может видеть Hello, попадают в hello следующие категории:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="7f7b7-108">приложения Office 365;</span><span class="sxs-lookup"><span data-stu-id="7f7b7-108">Office 365 Applications</span></span>

-   <span data-ttu-id="7f7b7-109">приложения Майкрософт и сторонние приложения с единым входом на основе федерации;</span><span class="sxs-lookup"><span data-stu-id="7f7b7-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="7f7b7-110">приложения с единым входом на основе паролей;</span><span class="sxs-lookup"><span data-stu-id="7f7b7-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="7f7b7-111">приложения с существующими решениями единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="7f7b7-112">Общие проблемы toocheck сначала</span><span class="sxs-lookup"><span data-stu-id="7f7b7-112">General issues toocheck first</span></span>

-   <span data-ttu-id="7f7b7-113">Если приложения был только что добавлен tooa пользователя, повторите toosign и выхода из системы в hello пользовательской панели доступа после нескольких минут toosee при добавлении приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="7f7b7-114">Если лицензия только что был удален из пользователь или группа hello пользователь является членом это может занять много времени, в зависимости от hello размера и сложности hello группы для toobe изменения внесены.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="7f7b7-115">Разрешить дополнительное время, прежде чем войти в панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="7f7b7-116">Конфигурации связанных tooapplication проблем</span><span class="sxs-lookup"><span data-stu-id="7f7b7-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="7f7b7-117">Приложение может не отображаться на панели доступа пользователя из-за неправильной настройки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="7f7b7-118">Ниже приведены некоторые способы устранения проблемы связанные tooapplication конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="7f7b7-119">Как tooconfigure федеративного единого входа для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="7f7b7-120">Как tooconfigure федеративного единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="7f7b7-121">Как tooconfigure пароля единого входа приложения для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="7f7b7-122">Как tooconfigure пароля единого входа приложения для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="7f7b7-123">Как tooconfigure федеративного единого входа для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="7f7b7-124">Все приложения в коллекции Azure AD hello включен с возможностью корпоративного единого входа имеет доступные Пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="7f7b7-125">Можно получить доступ к hello [список учебников по toointegrate приложений SaaS в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) Подробное пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="7f7b7-126">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="7f7b7-127">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="7f7b7-128">Настройка значения метаданных приложения hello в Azure AD (вход, URL-адрес ответа URL-адрес, идентификатор)</span><span class="sxs-lookup"><span data-stu-id="7f7b7-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="7f7b7-129">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="7f7b7-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="7f7b7-130">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="7f7b7-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="7f7b7-131">Настройка значения метаданных Azure AD в приложение hello (вход, URL-адрес, издателя, URL-адрес выхода и сертификата)</span><span class="sxs-lookup"><span data-stu-id="7f7b7-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="7f7b7-132">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="7f7b7-133">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-134">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="7f7b7-135">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-136">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-137">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-138">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="7f7b7-139">В hello **введите имя** текстового поля из hello **добавить из галереи hello** раздел, имя типа hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="7f7b7-140">Выберите приложение hello, требуется tooconfigure для единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="7f7b7-141">Перед добавлением приложения hello, можно изменить его имя из hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="7f7b7-142">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="7f7b7-143">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="7f7b7-144">Настройка единого входа для приложения из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="7f7b7-145">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-146">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f7b7-147">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-148">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-149">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-150">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7f7b7-151">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-152">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="7f7b7-153">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-154">Выберите **входа на базе SAML** из hello **режим** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="7f7b7-155">Введите значения требуется hello в **URL-адреса и домена.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="7f7b7-156">Вы должны получить эти значения с поставщиком приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="7f7b7-157">приложение hello tooconfigure как единый вход, инициированные SP, hello входа на URL-адрес является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="7f7b7-158">Для некоторых приложений hello идентификатор также является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="7f7b7-159">приложение hello tooconfigure как инициированный IdP SSO, hello URL-адрес ответа является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="7f7b7-160">Для некоторых приложений hello идентификатор также является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="7f7b7-161">**Необязательно:** щелкните **Показывать дополнительные параметры URL-адреса** Если требуется toosee hello необязательные значения.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="7f7b7-162">В hello **атрибуты пользователя**, выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="7f7b7-163">**Необязательно:** щелкните **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="7f7b7-164">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="7f7b7-165">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-165">click **Add attribute**.</span></span> <span data-ttu-id="7f7b7-166">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="7f7b7-167">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-167">click **Save.**</span></span> <span data-ttu-id="7f7b7-168">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="7f7b7-169">Нажмите кнопку **Настройка &lt;имя_приложения&gt;**  tooaccess документацию по tooconfigure единого входа в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="7f7b7-170">Кроме того имеет URL-адреса метаданных hello и toosetup требуется сертификат для единого входа с помощью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="7f7b7-171">Нажмите кнопку **Сохранить** toosave hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="7f7b7-172">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="7f7b7-173">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="7f7b7-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="7f7b7-174">tooselect hello идентификатор пользователя или добавление атрибутов пользователя, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-175">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f7b7-176">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-177">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-178">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-179">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7f7b7-180">Если hello приложение, tooshow здесь не отображается, используйте hello **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-181">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7f7b7-182">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-183">В разделе hello **атрибуты пользователя** выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="7f7b7-184">Hello выбранного параметра должен toomatch hello ожидаемое значение в tooauthenticate hello hello приложения пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="7f7b7-185">Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="7f7b7-186">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) под hello статьи политики идентификатора имени.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="7f7b7-187">атрибуты пользователя tooadd, нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="7f7b7-188">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="7f7b7-189">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-189">click **Add attribute**.</span></span> <span data-ttu-id="7f7b7-190">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="7f7b7-191">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-191">click **Save.**</span></span> <span data-ttu-id="7f7b7-192">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="7f7b7-193">Загрузка метаданных Azure AD hello или сертификат</span><span class="sxs-lookup"><span data-stu-id="7f7b7-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="7f7b7-194">метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-195">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f7b7-196">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-197">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-198">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-199">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7f7b7-200">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-201">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7f7b7-202">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-203">Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="7f7b7-204">В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="7f7b7-205">Azure AD не предоставляет метаданных hello tooget URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="7f7b7-206">Hello метаданные могут быть получены только как XML-файл.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="7f7b7-207">Как tooconfigure федеративного единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="7f7b7-208">tooconfigure приложения не коллекции требуется toohave Azure AD premium и SAML 2.0 поддерживает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="7f7b7-209">Дополнительные сведения о версиях Azure AD см. в разделе [Цены на Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="7f7b7-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="7f7b7-210">Настройка значения метаданных приложения hello в Azure AD (вход, URL-адрес ответа URL-адрес, идентификатор)</span><span class="sxs-lookup"><span data-stu-id="7f7b7-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="7f7b7-211">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="7f7b7-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="7f7b7-212">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="7f7b7-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="7f7b7-213">Настройка значения метаданных Azure AD в приложение hello (вход, URL-адрес, издателя, URL-адрес выхода и сертификата)</span><span class="sxs-lookup"><span data-stu-id="7f7b7-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="7f7b7-214">Настройка значения метаданных приложения hello в Azure AD (вход, URL-адрес ответа URL-адрес, идентификатор)</span><span class="sxs-lookup"><span data-stu-id="7f7b7-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="7f7b7-215">tooconfigure единого входа для приложения, которое не находится в коллекции hello Azure AD, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-216">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f7b7-217">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-218">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-219">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-220">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="7f7b7-221">Нажмите кнопку **приложения коллекции не** в hello **добавить собственное приложение** раздела.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="7f7b7-222">Введите имя приложения hello hello в hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="7f7b7-223">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="7f7b7-224">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="7f7b7-225">Выберите **входа на базе SAML** в hello **режим** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="7f7b7-226">Введите значения требуется hello в **URL-адреса и домена.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="7f7b7-227">Вы должны получить эти значения с поставщиком приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="7f7b7-228">приложение hello tooconfigure как единый вход, инициированный IdP, введите URL-адрес ответа hello и hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="7f7b7-229">**Необязательно:** tooconfigure приложения hello в виде единого входа, инициированные SP, hello входа на URL-адрес является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="7f7b7-230">В hello **атрибуты пользователя**, выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="7f7b7-231">**Необязательно:** щелкните **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="7f7b7-232">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="7f7b7-233">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-233">click **Add attribute**.</span></span> <span data-ttu-id="7f7b7-234">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="7f7b7-235">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-235">Click **Save.**</span></span> <span data-ttu-id="7f7b7-236">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="7f7b7-237">Нажмите кнопку **Настройка &lt;имя_приложения&gt;**  tooaccess документацию по tooconfigure единого входа в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="7f7b7-238">Кроме того имеет URL-адреса Azure AD и сертификат, необходимый для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="7f7b7-239">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="7f7b7-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="7f7b7-240">tooselect hello идентификатор пользователя или добавление атрибутов пользователя, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-241">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f7b7-242">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-243">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-244">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-245">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="7f7b7-246">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-247">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7f7b7-248">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-249">В разделе hello **атрибуты пользователя** выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="7f7b7-250">Hello выбранного параметра должен toomatch hello ожидаемое значение в tooauthenticate hello hello приложения пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="7f7b7-251">Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="7f7b7-252">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) под hello статьи политики идентификатора имени.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="7f7b7-253">атрибуты пользователя tooadd, нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="7f7b7-254">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="7f7b7-255">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-255">click **Add attribute**.</span></span> <span data-ttu-id="7f7b7-256">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="7f7b7-257">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-257">Click **Save.**</span></span> <span data-ttu-id="7f7b7-258">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="7f7b7-259">Загрузка метаданных Azure AD hello или сертификат</span><span class="sxs-lookup"><span data-stu-id="7f7b7-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="7f7b7-260">метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-261">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f7b7-262">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-263">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-264">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-265">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="7f7b7-266">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-267">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7f7b7-268">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-269">Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="7f7b7-270">В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="7f7b7-271">Azure AD не предоставляет метаданных hello tooget URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="7f7b7-272">Hello метаданные могут быть получены только как XML-файл.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="7f7b7-273">Как tooconfigure пароля единого входа для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="7f7b7-274">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="7f7b7-275">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="7f7b7-276">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="7f7b7-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="7f7b7-277">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="7f7b7-278">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-279">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="7f7b7-280">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-281">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-282">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-283">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="7f7b7-284">В hello **введите имя** текстового поля из hello **добавить из галереи hello** раздел, имя типа hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="7f7b7-285">Выберите приложение hello, требуется tooconfigure для единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="7f7b7-286">Перед добавлением приложения hello, можно изменить его имя из hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="7f7b7-287">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="7f7b7-288">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="7f7b7-289">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="7f7b7-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="7f7b7-290">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-291">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f7b7-292">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-293">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-294">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-295">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="7f7b7-296">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-297">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="7f7b7-298">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-299">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="7f7b7-300">[Назначить пользователей приложения toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="7f7b7-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="7f7b7-301">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="7f7b7-302">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="7f7b7-303">Как tooconfigure пароля единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="7f7b7-304">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="7f7b7-305">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="7f7b7-305">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="7f7b7-306">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="7f7b7-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="7f7b7-307">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="7f7b7-307">Add a non-gallery application</span></span>

<span data-ttu-id="7f7b7-308">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-309">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="7f7b7-310">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-311">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-312">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-313">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="7f7b7-314">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="7f7b7-315">Введите имя приложения hello в hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="7f7b7-316">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-316">Select **Add.**</span></span>

<span data-ttu-id="7f7b7-317">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="7f7b7-318">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="7f7b7-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="7f7b7-319">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-320">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f7b7-321">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-322">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-323">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-324">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="7f7b7-325">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-326">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="7f7b7-327">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-328">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="7f7b7-329">Введите hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="7f7b7-330">Это hello URL-адрес, где пользователи введите свои имя пользователя и пароль toosign в для.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="7f7b7-331">Убедитесь, что вход hello поля отображаются по URL-АДРЕСУ hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="7f7b7-332">[Назначить пользователей приложения toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="7f7b7-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="7f7b7-333">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="7f7b7-334">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="7f7b7-335">Проблемы tooassigning связанных приложений toousers</span><span class="sxs-lookup"><span data-stu-id="7f7b7-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="7f7b7-336">Пользователь не видите приложения на своей панели доступа, так как они не являются назначенными toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="7f7b7-337">Ниже приведены некоторые способы toocheck.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="7f7b7-338">Проверьте, если пользователю назначено toohello приложения</span><span class="sxs-lookup"><span data-stu-id="7f7b7-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="7f7b7-339">Как tooassign пользовательским tooan приложением напрямую</span><span class="sxs-lookup"><span data-stu-id="7f7b7-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="7f7b7-340">Флажок при назначении пользователю лицензии tooa связанные toohello приложения</span><span class="sxs-lookup"><span data-stu-id="7f7b7-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="7f7b7-341">Как tooassign пользователь tooa лицензии</span><span class="sxs-lookup"><span data-stu-id="7f7b7-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="7f7b7-342">Проверьте, если пользователю назначено toohello приложения</span><span class="sxs-lookup"><span data-stu-id="7f7b7-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="7f7b7-343">toocheck, если пользователю назначено toohello приложения, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-344">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7f7b7-345">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-346">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-347">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-348">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="7f7b7-349">**Поиск** для hello имя приложения hello в вопросе.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="7f7b7-350">Выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="7f7b7-351">Проверьте toosee, если пользователю назначено toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="7f7b7-352">В противном случае следуйте инструкциям hello» как tooassign пользовательским tooan приложением напрямую» toodo так.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="7f7b7-353">Как tooassign пользовательским tooan приложением напрямую</span><span class="sxs-lookup"><span data-stu-id="7f7b7-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="7f7b7-354">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-355">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="7f7b7-356">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-357">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-358">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-359">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7f7b7-360">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-361">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="7f7b7-362">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-363">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7f7b7-364">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7f7b7-365">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7f7b7-366">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="7f7b7-367">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="7f7b7-368">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="7f7b7-369">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="7f7b7-370">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="7f7b7-371">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="7f7b7-372">После краткого периода hello пользователей, которые вы выбрали может toolaunch эти приложения в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="7f7b7-373">Проверьте, является ли пользователь по лицензии связанных toohello приложения</span><span class="sxs-lookup"><span data-stu-id="7f7b7-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="7f7b7-374">toocheck пользователя назначить лицензии, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-375">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7f7b7-376">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-377">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-378">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-379">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-379">click **All users**.</span></span>

6.  <span data-ttu-id="7f7b7-380">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="7f7b7-381">Нажмите кнопку **лицензий** toosee hello какие лицензии пользователя в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="7f7b7-382">Здравствуйте, если hello пользователю назначается лицензия Office tooan это включить tooappear приложений первой стороной Office на панели доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="7f7b7-383">Как tooassign лицензию пользователя</span><span class="sxs-lookup"><span data-stu-id="7f7b7-383">How tooassign a user a license</span></span> 

<span data-ttu-id="7f7b7-384">tooassign пользователь tooa лицензии, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-385">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7f7b7-386">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-387">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-388">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-389">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-389">click **All users**.</span></span>

6.  <span data-ttu-id="7f7b7-390">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="7f7b7-391">Нажмите кнопку **лицензий** toosee hello какие лицензии пользователя в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="7f7b7-392">Нажмите кнопку hello **назначить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="7f7b7-393">Выберите **один или несколько продуктов** из списка допустимых продуктов hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="7f7b7-394">**Необязательный** щелкните hello **параметры назначения** toogranularly элемента назначить продукты.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="7f7b7-395">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="7f7b7-396">Нажмите кнопку hello **назначить** кнопку tooassign toothis эти лицензии пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="7f7b7-397">Проблемы tooassigning связанных приложений toogroups</span><span class="sxs-lookup"><span data-stu-id="7f7b7-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="7f7b7-398">Пользователь видите приложения на своей панели доступа, так как они являются частью группы, имеющей разрешение приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="7f7b7-399">Ниже приведены некоторые способы toocheck.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="7f7b7-400">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="7f7b7-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="7f7b7-401">Как tooassign tooa приложения группы напрямую</span><span class="sxs-lookup"><span data-stu-id="7f7b7-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="7f7b7-402">Установите флажок, если пользователь является членом группы, назначает tooa лицензию</span><span class="sxs-lookup"><span data-stu-id="7f7b7-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="7f7b7-403">Как tooassign tooa лицензионной группы</span><span class="sxs-lookup"><span data-stu-id="7f7b7-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="7f7b7-404">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="7f7b7-404">Check a user’s group memberships</span></span>

<span data-ttu-id="7f7b7-405">toocheck членство в группе, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="7f7b7-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-406">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7f7b7-407">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-408">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-409">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-410">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-410">click **All users**.</span></span>

6.  <span data-ttu-id="7f7b7-411">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="7f7b7-412">Щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-412">click **Groups**.</span></span>

8.  <span data-ttu-id="7f7b7-413">Проверка toosee, если пользователь входит в состав группы назначить toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="7f7b7-414">Если требуется, чтобы tooremove hello пользователя из группы hello **щелкните строку hello** hello группы и выберите Удалить.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="7f7b7-415">Как tooassign tooa приложения группы напрямую</span><span class="sxs-lookup"><span data-stu-id="7f7b7-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="7f7b7-416">tooassign один или несколько групп tooan приложению напрямую, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-417">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="7f7b7-418">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-419">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-420">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-421">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7f7b7-422">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7f7b7-423">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="7f7b7-424">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f7b7-425">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7f7b7-426">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7f7b7-427">Тип в hello **имя полного группы** вы заинтересованы в назначение в hello группы hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7f7b7-428">Наведите указатель мыши на hello **группы** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="7f7b7-429">Нажмите кнопку tooadd hello флажок Далее toohello группы профиля фотографию или логотип вашей toohello пользователя **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="7f7b7-430">**Необязательно:** при желании слишком**добавить несколько групп**, тип в другой **имя полного группы** в hello **поиск по имени или адресу электронной почты** поле поиска и нажмите кнопку флажок tooadd hello этой группы toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="7f7b7-431">После завершения выбора групп, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="7f7b7-432">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** вами группах колонке tooselect toohello tooassign роли выбранных.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="7f7b7-433">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранные группы.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="7f7b7-434">После краткого периода hello пользователей, которые вы выбрали может toolaunch эти приложения в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="7f7b7-435">Установите флажок, если пользователь является членом группы, назначает tooa лицензию</span><span class="sxs-lookup"><span data-stu-id="7f7b7-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="7f7b7-436">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7f7b7-437">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-438">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-439">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-440">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-440">click **All users**.</span></span>

6.  <span data-ttu-id="7f7b7-441">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="7f7b7-442">Щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-442">click **Groups**.</span></span>

8.  <span data-ttu-id="7f7b7-443">Щелкните строку hello в определенную группу.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="7f7b7-444">Нажмите кнопку **лицензий** toosee, какую группу лицензий hello назначила tooit.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="7f7b7-445">Здравствуйте, если группа hello назначена лицензия Office tooan, это может включить определенные tooappear приложений первой стороной Office на панели доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="7f7b7-446">Как tooassign tooa лицензионной группы</span><span class="sxs-lookup"><span data-stu-id="7f7b7-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="7f7b7-447">tooassign tooa в лицензионную группу, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="7f7b7-448">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="7f7b7-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7f7b7-449">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f7b7-450">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f7b7-451">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="7f7b7-452">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-452">click **All groups**.</span></span>

6.  <span data-ttu-id="7f7b7-453">**Поиск** для hello группы, которые вас интересуют и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="7f7b7-454">Нажмите кнопку **лицензий** toosee, какую группу hello лицензии в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="7f7b7-455">Нажмите кнопку hello **назначить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="7f7b7-456">Выберите **один или несколько продуктов** из списка допустимых продуктов hello.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="7f7b7-457">**Необязательный** щелкните hello **параметры назначения** toogranularly элемента назначить продукты.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="7f7b7-458">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="7f7b7-459">Нажмите кнопку hello **назначить** кнопку tooassign группы toothis эти лицензии.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="7f7b7-460">Это может занять много времени, в зависимости от hello размера и сложности hello группы.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="7f7b7-461">toodo это быстрее, рассмотрите возможность временно назначение лицензии пользователя toohello напрямую.</span><span class="sxs-lookup"><span data-stu-id="7f7b7-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="7f7b7-462">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f7b7-462">Next steps</span></span>
[<span data-ttu-id="7f7b7-463">Добавить новый tooAzure пользователей Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f7b7-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

