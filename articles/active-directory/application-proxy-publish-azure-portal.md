---
title: "aaaPublish приложений с помощью прокси приложения Azure AD | Документы Microsoft"
description: "Опубликуйте облако toohello локальных приложений с помощью прокси приложения Azure AD в hello портал Azure."
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
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="f8d24-103">Публикация приложений с помощью прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8d24-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8d24-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="f8d24-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="f8d24-105">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="f8d24-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="f8d24-106">Прокси приложения Azure Active Directory (AD) поможет поддерживать удаленные работники путем публикации toobe локальных приложений, доступны через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="f8d24-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="f8d24-107">Вы можете опубликовать этих приложений с помощью hello Azure портала tooprovide безопасный удаленный доступ из вне сети.</span><span class="sxs-lookup"><span data-stu-id="f8d24-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="f8d24-108">В этой статье рассматриваются действия hello toopublish приложение локально с помощью прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="f8d24-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="f8d24-109">После завершения этой статье, пользователи будут быть приложения может tooaccess удаленно.</span><span class="sxs-lookup"><span data-stu-id="f8d24-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="f8d24-110">И вы будете готовы tooconfigure дополнительных компонентов для приложения hello, как единый вход, личные сведения и требования к безопасности.</span><span class="sxs-lookup"><span data-stu-id="f8d24-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="f8d24-111">Если вы tooApplication новый прокси-сервера, Дополнительные сведения об этой функции в статье hello [как tooprovide безопасный удаленный доступ tooon локальные приложения](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f8d24-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="f8d24-112">Публикация локального приложения для удаленного доступа</span><span class="sxs-lookup"><span data-stu-id="f8d24-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="f8d24-113">Выполните эти шаги toopublish приложений с помощью прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="f8d24-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="f8d24-114">Если еще не уже загрузили и настройки соединителя для организации, перейдите в слишком[Приступая к работе с прокси-сервера приложений и установить соединитель hello](active-directory-application-proxy-enable.md) первой и опубликуйте приложение.</span><span class="sxs-lookup"><span data-stu-id="f8d24-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="f8d24-115">Если вы тестируете исходящий прокси приложения для hello первый раз, выберите приложение, которое настроено для проверки подлинности на основе пароля.</span><span class="sxs-lookup"><span data-stu-id="f8d24-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="f8d24-116">Прокси-сервер приложения поддерживает другие типы проверки подлинности, но приложения на основе пароля hello простой tooget вверх и быстрый запуск.</span><span class="sxs-lookup"><span data-stu-id="f8d24-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="f8d24-117">Войдите как администратор в hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f8d24-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f8d24-118">Выберите **Azure Active Directory** > **Корпоративные приложения** > **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="f8d24-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Добавление корпоративного приложения](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="f8d24-120">Выберите **Все** и щелкните **Локальное приложение**.</span><span class="sxs-lookup"><span data-stu-id="f8d24-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Добавление собственного приложения](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="f8d24-122">Укажите следующую информацию о своем приложении hello:</span><span class="sxs-lookup"><span data-stu-id="f8d24-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="f8d24-123">**Имя**: hello имя приложения hello, которое будет отображаться на панели доступа hello и в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f8d24-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="f8d24-124">**Внутренний URL-адрес**: hello URL-адрес, используйте приложение hello tooaccess из частной сети.</span><span class="sxs-lookup"><span data-stu-id="f8d24-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="f8d24-125">Вы можете предоставить определенный путь в hello внутреннего сервера toopublish, пока hello rest сервера hello не опубликован.</span><span class="sxs-lookup"><span data-stu-id="f8d24-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="f8d24-126">Таким образом, вы можете опубликовать разные сайты в hello же сервере, что различные приложения и присвойте каждой из них собственного имени и правила доступа.</span><span class="sxs-lookup"><span data-stu-id="f8d24-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="f8d24-127">При публикации путь, убедитесь, что он включает все необходимые изображения hello, сценариев и стилей для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f8d24-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="f8d24-128">Например если приложение находится на https://yourapp/app и использует образы, расположенный в https://yourapp/media, https://yourapp/ следует опубликовать как путь hello.</span><span class="sxs-lookup"><span data-stu-id="f8d24-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="f8d24-129">Это внутренний URL-адрес не имеет toobe hello целевая страница, которые видят пользователи.</span><span class="sxs-lookup"><span data-stu-id="f8d24-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="f8d24-130">Дополнительные сведения см. в разделе [Настройка пользовательской домашней страницы для опубликованных приложений с помощью прокси приложения Azure AD](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="f8d24-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="f8d24-131">**Внешний URL-адрес**: hello адрес пользователи переходят tooin порядок tooaccess приложение hello из за пределов вашей сети.</span><span class="sxs-lookup"><span data-stu-id="f8d24-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="f8d24-132">Если вы не хотите домен прокси приложения по умолчанию hello toouse, прочтите сведения о [пользовательских доменов в прокси приложения Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="f8d24-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="f8d24-133">**Предварительной проверки подлинности**: как прокси-сервер приложения проверяет пользователей до предоставления им доступа tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="f8d24-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="f8d24-134">Azure Active Directory: Прокси-сервер приложения перенаправляет пользователей toosign вход с помощью Azure AD, который выполняет проверку подлинности их разрешения для каталога hello и приложения.</span><span class="sxs-lookup"><span data-stu-id="f8d24-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="f8d24-135">Рекомендуется оставить этот параметр по умолчанию hello, чтобы воспользоваться преимуществами функции безопасности Azure AD, например условного доступа и многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f8d24-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="f8d24-136">Passthrough: Пользователи не имеют tooauthenticate для приложения hello tooaccess Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f8d24-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="f8d24-137">По-прежнему можно настроить требования к проверке подлинности hello серверную часть.</span><span class="sxs-lookup"><span data-stu-id="f8d24-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="f8d24-138">**Группы соединителей**: приложение hello tooyour удаленного доступа для соединителей процесса и позволяют упорядочить соединители и приложения по регионам, сети или Назначение группы соединителей.</span><span class="sxs-lookup"><span data-stu-id="f8d24-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="f8d24-139">При отсутствии любой группы соединителей еще создан приложения назначается слишком**по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="f8d24-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![Настройка приложения](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="f8d24-141">При необходимости настройте дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="f8d24-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="f8d24-142">Для большинства приложений следует сохранить значения этих параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f8d24-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="f8d24-143">**Истекло время ожидания внутреннего приложения**: это значение слишком**длинные** только в том случае, если ваше приложение медленно tooauthenticate и подключения.</span><span class="sxs-lookup"><span data-stu-id="f8d24-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="f8d24-144">**Перевод URL-адресов в заголовках**: задавать это значение как **Да** , если только приложение hello исходный заголовок узла в запросе проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="f8d24-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="f8d24-145">**Перевод URL-адреса в основной части приложения**: задавать это значение как **нет** не жестко закодировано HTML ссылки tooother локальных приложений и не использовать пользовательские домены.</span><span class="sxs-lookup"><span data-stu-id="f8d24-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="f8d24-146">Дополнительные сведения см. в статье [Перенаправление встроенных ссылок для приложений, опубликованных с помощью прокси приложения Azure AD](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="f8d24-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Настройка приложения](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="f8d24-148">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f8d24-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="f8d24-149">Добавление тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f8d24-149">Add a test user</span></span> 

<span data-ttu-id="f8d24-150">tootest правильно, публикации приложения добавьте тестовую учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="f8d24-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="f8d24-151">Убедитесь, что эта учетная запись уже есть приложение hello tooaccess разрешения из внутри корпоративной сети hello.</span><span class="sxs-lookup"><span data-stu-id="f8d24-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="f8d24-152">Назад на панели быстрого запуска hello выберите **назначение пользователей для тестирования**.</span><span class="sxs-lookup"><span data-stu-id="f8d24-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![Назначение пользователя для тестирования](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="f8d24-154">На hello пользователей и групп колонке выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="f8d24-154">On hello Users and groups blade, select **Add**.</span></span>

  ![Добавление пользователя или группы](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="f8d24-156">В колонке назначения добавить hello, выберите **пользователей и групп** выберите hello счета, tooadd.</span><span class="sxs-lookup"><span data-stu-id="f8d24-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="f8d24-157">Выберите **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f8d24-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="f8d24-158">Тестирование опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="f8d24-158">Test your published app</span></span>

<span data-ttu-id="f8d24-159">В браузере перейдите toohello внешний URL-адрес, заданные во время hello публикации шаг.</span><span class="sxs-lookup"><span data-stu-id="f8d24-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="f8d24-160">Вы увидите hello начальном экране и может toosign вход с учетной записью hello теста можно настроить.</span><span class="sxs-lookup"><span data-stu-id="f8d24-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![Тестирование опубликованного приложения](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="f8d24-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8d24-162">Next steps</span></span>
- <span data-ttu-id="f8d24-163">[Загрузите соединители](active-directory-application-proxy-enable.md) и [создать соединитель группы](active-directory-application-proxy-connectors-azure-portal.md) toopublish приложений на отдельные сети и расположения.</span><span class="sxs-lookup"><span data-stu-id="f8d24-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="f8d24-164">[Настройте единый вход](application-proxy-sso-azure-portal.md) для опубликованного приложения.</span><span class="sxs-lookup"><span data-stu-id="f8d24-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
