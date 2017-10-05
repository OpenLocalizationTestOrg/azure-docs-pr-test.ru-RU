---
title: "Настройка проверки подлинности Twitter для приложения служб приложений"
description: "Узнайте, как настроить проверку подлинности Twitter для приложения служб приложений."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: afde020b7817dc58ecea24eb4a09cf93d0986eb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-twitter-login"></a><span data-ttu-id="8d877-103">Как настроить приложение службы приложений для использования имени для входа Twitter</span><span class="sxs-lookup"><span data-stu-id="8d877-103">How to configure your App Service application to use Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="8d877-104">В этом разделе показано, как настроить службу приложений Azure для использования Twitter в качестве поставщика проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8d877-104">This topic shows you how to configure Azure App Service to use Twitter as an authentication provider.</span></span>

<span data-ttu-id="8d877-105">Чтобы выполнить инструкции из этой статьи, вам потребуется номер телефона и учетная запись Twitter с проверенным электронным адресом.</span><span class="sxs-lookup"><span data-stu-id="8d877-105">To complete the procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="8d877-106">Чтобы создать учетную запись Twitter, перейдите по ссылке <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="8d877-106">To create a new Twitter account, go to <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="8d877-107"><a name="register"> </a>Регистрация приложения в Twitter</span><span class="sxs-lookup"><span data-stu-id="8d877-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="8d877-108">Перейдите на [портал Azure]и перейдите к своему приложению.</span><span class="sxs-lookup"><span data-stu-id="8d877-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="8d877-109">Скопируйте свой **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="8d877-109">Copy your **URL**.</span></span> <span data-ttu-id="8d877-110">Он будет использован для настройки приложения Twitter.</span><span class="sxs-lookup"><span data-stu-id="8d877-110">You will use this to configure your Twitter app.</span></span>
2. <span data-ttu-id="8d877-111">Перейдите на веб-сайт [Twitter Developers] (Разработчики Twitter), войдите с помощью учетных данных учетной записи Twitter и щелкните **Create New App**(Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="8d877-111">Navigate to the [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="8d877-112">Введите **имя** и **описание** для нового приложения в соответствующих полях.</span><span class="sxs-lookup"><span data-stu-id="8d877-112">Type in the **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="8d877-113">Вставьте **URL-адрес** приложения в поле **Веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="8d877-113">Paste in your application's **URL** for the **Website** value.</span></span> <span data-ttu-id="8d877-114">Затем в поле **URL-адрес обратного вызова** вставьте **URL-адрес обратного вызова**, скопированный ранее.</span><span class="sxs-lookup"><span data-stu-id="8d877-114">Then, for the **Callback URL**, paste the **Callback URL** you copied earlier.</span></span> <span data-ttu-id="8d877-115">Это шлюз мобильного приложения, дополненный путем */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="8d877-115">This is your Mobile App gateway appended with the path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="8d877-116">Пример: `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="8d877-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="8d877-117">Убедитесь, что используете схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8d877-117">Make sure that you are using the HTTPS scheme.</span></span>
4. <span data-ttu-id="8d877-118">В нижней части страницы прочтите и примите условия.</span><span class="sxs-lookup"><span data-stu-id="8d877-118">At the bottom the page, read and accept the terms.</span></span> <span data-ttu-id="8d877-119">Затем щелкните **Создать приложение Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8d877-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="8d877-120">После этого приложение будет зарегистрировано и появятся сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="8d877-120">This registers the app displays the application details.</span></span>
5. <span data-ttu-id="8d877-121">Откройте вкладку **Параметры**, установите флажок **Allow this application to be used to sign in with Twitter** (Разрешить использовать это приложение для входа в Twitter), а затем щелкните **Обновить параметры**.</span><span class="sxs-lookup"><span data-stu-id="8d877-121">Click the **Settings** tab, check **Allow this application to be used to sign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="8d877-122">Откройте вкладку **Ключи и токены доступа** .</span><span class="sxs-lookup"><span data-stu-id="8d877-122">Select the **Keys and Access Tokens** tab.</span></span> <span data-ttu-id="8d877-123">Запишите значения полей **Consumer Key (API Key)** (Ключ потребителя (ключ API)) и **Consumer secret (API Secret)** (Секрет потребителя (секрет API)).</span><span class="sxs-lookup"><span data-stu-id="8d877-123">Make a note of the values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8d877-124">Секрет клиента — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="8d877-124">The consumer secret is an important security credential.</span></span> <span data-ttu-id="8d877-125">Не сообщайте никому этого секрета и не распространяйте его вместе с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="8d877-125">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="8d877-126"><a name="secrets"> </a>Добавление данных Twitter в приложение</span><span class="sxs-lookup"><span data-stu-id="8d877-126"><a name="secrets"> </a>Add Twitter information to your application</span></span>
1. <span data-ttu-id="8d877-127">Снова вернитесь на [портал Azure]и перейдите к своему приложению.</span><span class="sxs-lookup"><span data-stu-id="8d877-127">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="8d877-128">Щелкните **Параметры**, а затем — **Проверка подлинности или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="8d877-128">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="8d877-129">Если функция аутентификации или авторизации не включена, установите переключатель в положение **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="8d877-129">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="8d877-130">Щелкните **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8d877-130">Click **Twitter**.</span></span> <span data-ttu-id="8d877-131">Вставьте значения идентификатора и секрета приложения, полученные ранее.</span><span class="sxs-lookup"><span data-stu-id="8d877-131">Paste in the App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="8d877-132">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8d877-132">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="8d877-133">По умолчанию служба приложений обеспечивает проверку подлинности, но не ограничивает авторизованный доступ к содержимому сайта и API.</span><span class="sxs-lookup"><span data-stu-id="8d877-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="8d877-134">Авторизация пользователей должна быть включена в код приложения.</span><span class="sxs-lookup"><span data-stu-id="8d877-134">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="8d877-135">(Необязательно.) Чтобы предоставить доступ к сайту только пользователям, прошедшим проверку подлинности в Twitter, установите для параметра **Предпринимаемое действие, если проверка подлинности для запроса не выполнена** значение **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8d877-135">(Optional) To restrict access to your site to only users authenticated by Twitter, set **Action to take when request is not authenticated** to **Twitter**.</span></span> <span data-ttu-id="8d877-136">В этом случае все запросы, не прошедшие проверку подлинности, направляются для проверки подлинности с помощью Twitter.</span><span class="sxs-lookup"><span data-stu-id="8d877-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Twitter for authentication.</span></span>
5. <span data-ttu-id="8d877-137">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8d877-137">Click **Save**.</span></span>

<span data-ttu-id="8d877-138">Теперь вы можете использовать Twitter для проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="8d877-138">You are now ready to use Twitter for authentication in your app.</span></span>

## <span data-ttu-id="8d877-139"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="8d877-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

<span data-ttu-id="8d877-140">[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span><span class="sxs-lookup"><span data-stu-id="8d877-140">[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span></span>
<span data-ttu-id="8d877-141">[портал Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="8d877-141">[Azure portal]: https://portal.azure.com/</span></span>
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
