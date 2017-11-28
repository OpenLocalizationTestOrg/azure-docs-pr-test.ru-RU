---
title: "aaaSingle tooapps входа с помощью прокси приложения Azure AD | Документы Microsoft"
description: "Включение единого входа для опубликованных локальных приложений с помощью прокси приложения Azure AD в hello портал Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="3ddcb-103">Хранение паролей для единого входа с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="3ddcb-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="3ddcb-104">Прокси приложения Azure Active Directory помогает повысить производительность путем публикации локальных приложений, чтобы предоставить удаленным сотрудникам безопасный доступ к ним.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="3ddcb-105">В hello портал Azure можно также настроить единого входа (SSO) toothese приложений.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="3ddcb-106">Вашим пользователям требуется только tooauthenticate с Azure AD, и они могут получать корпоративные приложения без toosign еще раз.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="3ddcb-107">Прокси приложения поддерживает несколько [режимов единого входа](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ddcb-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="3ddcb-108">Вход по паролю предназначен для приложений, использующих для аутентификации сочетание имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="3ddcb-109">После завершения настройки паролю единого входа для приложения, пользователей toosign в toohello локального приложения один раз.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="3ddcb-110">После этого Azure Active Directory сохраняет hello входа в систему и автоматически предоставляет ему toohello приложения при пользователей удаленного доступа к нему.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="3ddcb-111">Вы должны были опубликовать и протестировать свое приложение с помощью прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="3ddcb-112">В противном случае выполните действия hello в [публикация приложений с помощью прокси приложения Azure AD](application-proxy-publish-azure-portal.md) возобновить вернитесь сюда.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="3ddcb-113">Настройка хранения пароля для приложения</span><span class="sxs-lookup"><span data-stu-id="3ddcb-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="3ddcb-114">Войдите в toohello [портал Azure](https://portal.azure.com) с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="3ddcb-115">Выберите **Azure Active Directory** > **Корпоративные приложения** > **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="3ddcb-116">Выберите из списка hello приложение hello, что требуется tooset копирование с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="3ddcb-117">Щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-117">Select **Single sign-on**.</span></span>

   ![Выбор пункта "Единый вход"](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="3ddcb-119">Режим единого входа hello, выберите **пароль входа на основе**.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="3ddcb-120">Hello входа URL-адрес введите URL-адрес hello для страницы приветствия ввода toosign свои имя пользователя и пароль в приложении tooyour за пределами корпоративной сети hello.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="3ddcb-121">Это может быть hello внешний URL-адрес, созданный при публикации приложения hello через прокси-сервера приложения.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![Выбор входа по паролю и ввод URL-адрес](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="3ddcb-123">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="3ddcb-124">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="3ddcb-124">Test your app</span></span>

<span data-ttu-id="3ddcb-125">Go tooexternal URL-адрес, который настроен для удаленного доступа tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="3ddcb-126">Вход, учетные данные для этого приложения (hello учетные данные тестовой учетной записи, которую вы настроили доступ).</span><span class="sxs-lookup"><span data-stu-id="3ddcb-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="3ddcb-127">После успешного входа в необходимо будет tooleave приложение hello и возвращаться без повторного ввода учетных данных.</span><span class="sxs-lookup"><span data-stu-id="3ddcb-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3ddcb-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ddcb-128">Next steps</span></span>

- <span data-ttu-id="3ddcb-129">Узнайте, как другие способы tooimplement [единого входа с помощью прокси приложения](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3ddcb-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="3ddcb-130">Изучите [вопросы безопасности при удаленном доступе к приложениям через прокси приложения Azure AD](application-proxy-security-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="3ddcb-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>