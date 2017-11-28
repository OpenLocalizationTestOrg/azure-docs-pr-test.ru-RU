---
title: "Публикация приложений с помощью прокси приложения Azure AD | Microsoft Azure"
description: "Публикация локальных приложений в облако с помощью прокси приложения Azure AD на портале Azure."
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
ms.openlocfilehash: e00a939f2b20ab8e0a2ddf0ff91e59db440213ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="bf479-103">Публикация приложений с помощью прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf479-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf479-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="bf479-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="bf479-105">классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="bf479-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="bf479-106">Прокси приложения Azure Active Directory помогает организовать удаленную работу сотрудников, публикуя локальные приложения для доступа через Интернет.</span><span class="sxs-lookup"><span data-stu-id="bf479-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="bf479-107">Вы можете опубликовать эти приложения на портале Azure, чтобы предоставить к ним безопасный удаленный доступ из внешних сетей.</span><span class="sxs-lookup"><span data-stu-id="bf479-107">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span></span>

<span data-ttu-id="bf479-108">Эта статья содержит пошаговое описание процесса публикации локальных приложений с помощью прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="bf479-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="bf479-109">После выполнения инструкций в этой статье пользователи смогут подключаться к вашему приложению удаленно.</span><span class="sxs-lookup"><span data-stu-id="bf479-109">After you complete this article, your users will be able to access your app remotely.</span></span> <span data-ttu-id="bf479-110">И вы сможете настроить для приложения такие дополнительные возможности, как единый вход, личные сведения и параметры безопасности.</span><span class="sxs-lookup"><span data-stu-id="bf479-110">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="bf479-111">Если вы еще не знакомы с прокси приложения, узнайте, [как обеспечить безопасный удаленный доступ к локальным приложениям](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bf479-111">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="bf479-112">Публикация локального приложения для удаленного доступа</span><span class="sxs-lookup"><span data-stu-id="bf479-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="bf479-113">Выполните приведенные ниже действия для публикации приложений с помощью прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="bf479-113">Follow these steps to publish your apps with Application Proxy.</span></span> <span data-ttu-id="bf479-114">Если вы еще не скачали и не настроили соединитель для своей организации, сначала перейдите к разделу [Начало работы с прокси приложения и установка соединителя](active-directory-application-proxy-enable.md), после чего опубликуйте приложение.</span><span class="sxs-lookup"><span data-stu-id="bf479-114">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="bf479-115">Если вы впервые тестируете прокси приложения, выберите приложение, для которого настроена аутентификация на основе пароля.</span><span class="sxs-lookup"><span data-stu-id="bf479-115">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="bf479-116">Прокси приложения поддерживает и другие типы аутентификации, но настройка и запуск таких приложений требует меньше ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bf479-116">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span></span> 

1. <span data-ttu-id="bf479-117">Войдите на [портал Azure](https://portal.azure.com/) с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="bf479-117">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bf479-118">Выберите **Azure Active Directory** > **Корпоративные приложения** > **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="bf479-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Добавление корпоративного приложения](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="bf479-120">Выберите **Все** и щелкните **Локальное приложение**.</span><span class="sxs-lookup"><span data-stu-id="bf479-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Добавление собственного приложения](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="bf479-122">Укажите следующие сведения о приложении:</span><span class="sxs-lookup"><span data-stu-id="bf479-122">Provide the following information about your application:</span></span>

   - <span data-ttu-id="bf479-123">**Имя**. Имя приложения, которое будет отображаться на панели доступа и на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bf479-123">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span></span> 

   - <span data-ttu-id="bf479-124">**Внутренний URL-адрес**. Это URL-адрес для доступа к приложению в частной сети.</span><span class="sxs-lookup"><span data-stu-id="bf479-124">**Internal URL**: The URL that you use to access the application from inside your private network.</span></span> <span data-ttu-id="bf479-125">Для публикации можно указать только конкретный адрес на внутреннем сервере; при этом другие адреса сервера не публикуются.</span><span class="sxs-lookup"><span data-stu-id="bf479-125">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="bf479-126">Это позволяет публиковать на одном сервере разные сайты, назначая каждому из них отдельное имя и правила доступа.</span><span class="sxs-lookup"><span data-stu-id="bf479-126">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="bf479-127">Если вы публикуете путь, он должен включать в себя все необходимые изображения, скрипты и таблицы стилей для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="bf479-127">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="bf479-128">Например, если приложение расположено по адресу https://yourapp/app и использует образы, расположенные по адресу https://yourapp/media, следует опубликовать путь https://yourapp/.</span><span class="sxs-lookup"><span data-stu-id="bf479-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span> <span data-ttu-id="bf479-129">Этот внутренний URL-адрес не должен отображаться на целевой странице, которую видят пользователи.</span><span class="sxs-lookup"><span data-stu-id="bf479-129">This internal URL doesn't have to be the landing page your users see.</span></span> <span data-ttu-id="bf479-130">Дополнительные сведения см. в разделе [Настройка пользовательской домашней страницы для опубликованных приложений с помощью прокси приложения Azure AD](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="bf479-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="bf479-131">**Внешний URL-адрес**. Это адрес, на который будут обращаться пользователи для доступа к приложению за пределами локальной сети.</span><span class="sxs-lookup"><span data-stu-id="bf479-131">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span> <span data-ttu-id="bf479-132">Если вы не хотите использовать домен прокси приложения по умолчанию, прочитайте сведения о [личных доменах в прокси приложения Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="bf479-132">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="bf479-133">**Предварительная проверка подлинности**. Здесь указывается метод проверки пользователей, который использует прокси приложения, прежде чем предоставить доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="bf479-133">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="bf479-134">Azure Active Directory — прокси приложения перенаправляет пользователей на страницу входа в Azure AD, где будет выполняться проверка подлинности их разрешений для каталога и приложения.</span><span class="sxs-lookup"><span data-stu-id="bf479-134">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="bf479-135">Рекомендуется оставить значение этого параметра по умолчанию, чтобы воспользоваться преимуществами функций безопасности Azure AD, например условным доступом и Многофакторной Идентификацией.</span><span class="sxs-lookup"><span data-stu-id="bf479-135">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="bf479-136">Сквозной режим. Пользователям для доступа к приложению не нужно выполнять аутентификацию в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf479-136">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="bf479-137">Вы по-прежнему можете настроить требования к аутентификации на серверной стороне.</span><span class="sxs-lookup"><span data-stu-id="bf479-137">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="bf479-138">**Группа соединителей**. Соединители обрабатывают удаленный доступ к приложению, а группы соединителей позволяют сортировать соединители и приложения по регионам, сетям и назначению.</span><span class="sxs-lookup"><span data-stu-id="bf479-138">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="bf479-139">Если вы еще не создали какие-либо группы соединителей, приложение назначается в группу **по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="bf479-139">If you don't have any connector groups created yet, your app is assigned to **Default**.</span></span>

   ![Настройка приложения](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="bf479-141">При необходимости настройте дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="bf479-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="bf479-142">Для большинства приложений следует сохранить значения этих параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bf479-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="bf479-143">**Время ожидания серверного приложения**. Задайте для этого параметра значение **Длинный** только в том случае, если приложение медленно выполняет аутентификацию и подключение.</span><span class="sxs-lookup"><span data-stu-id="bf479-143">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span></span> 
   - <span data-ttu-id="bf479-144">**Translate URLs in Headers** (Преобразование URL-адресов в заголовках). Оставьте значением этого параметра **Да**, если только приложению не требуется исходный заголовок узла в запросе на аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="bf479-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span></span>
   - <span data-ttu-id="bf479-145">**Translate URLs in Application Body** (Преобразование URL-адресов в коде приложения). Только в случае, если вы используете жестко закодированные ссылки HTML на другие локальные приложения и не используете личные домены, следует изменить значение этого параметра по умолчанию **Нет**.</span><span class="sxs-lookup"><span data-stu-id="bf479-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="bf479-146">Дополнительные сведения см. в статье [Перенаправление встроенных ссылок для приложений, опубликованных с помощью прокси приложения Azure AD](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="bf479-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Настройка приложения](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="bf479-148">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bf479-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="bf479-149">Добавление тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bf479-149">Add a test user</span></span> 

<span data-ttu-id="bf479-150">Чтобы проверить, правильно ли опубликовано приложение, добавьте тестовую учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="bf479-150">To test that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="bf479-151">Убедитесь, что у нее имеются разрешения на доступ к приложению из корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="bf479-151">Verify that this account already has permissions to access the app from inside the corporate network.</span></span>

1. <span data-ttu-id="bf479-152">Вернитесь в колонку быстрого запуска и выберите **Assign a user for testing** (Назначить пользователя для тестирования).</span><span class="sxs-lookup"><span data-stu-id="bf479-152">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![Назначение пользователя для тестирования](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="bf479-154">В колонке "Пользователи и группы" выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bf479-154">On the Users and groups blade, select **Add**.</span></span>

  ![Добавление пользователя или группы](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="bf479-156">В колонке добавления выберите вариант **Пользователи и группы**, затем выберите учетную запись, которую хотите добавить.</span><span class="sxs-lookup"><span data-stu-id="bf479-156">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="bf479-157">Выберите **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bf479-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="bf479-158">Тестирование опубликованного приложения</span><span class="sxs-lookup"><span data-stu-id="bf479-158">Test your published app</span></span>

<span data-ttu-id="bf479-159">Откройте в браузере внешний URL-адрес, который вы указали на этапе публикации.</span><span class="sxs-lookup"><span data-stu-id="bf479-159">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="bf479-160">Вы должны увидеть экран приветствия. Войдите в приложение, используя настроенную для тестирования учетную запись.</span><span class="sxs-lookup"><span data-stu-id="bf479-160">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![Тестирование опубликованного приложения](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="bf479-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf479-162">Next steps</span></span>
- <span data-ttu-id="bf479-163">[Скачайте соединители](active-directory-application-proxy-enable.md) и [создайте группы соединителей](active-directory-application-proxy-connectors-azure-portal.md), чтобы публиковать приложения в разных сетях и расположениях.</span><span class="sxs-lookup"><span data-stu-id="bf479-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="bf479-164">[Настройте единый вход](application-proxy-sso-azure-portal.md) для опубликованного приложения.</span><span class="sxs-lookup"><span data-stu-id="bf479-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
