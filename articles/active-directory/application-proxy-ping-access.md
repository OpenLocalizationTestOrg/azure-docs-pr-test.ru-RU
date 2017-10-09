---
title: "aaaHeader проверки подлинности на основе PingAccess для прокси приложения Azure AD | Документы Microsoft"
description: "Публикация приложений с помощью прокси приложения и PingAccess toosupport заголовок проверки подлинности на основе."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="04e64-103">Аутентификация на основе заголовка для единого входа с использованием прокси приложения и PingAccess</span><span class="sxs-lookup"><span data-stu-id="04e64-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="04e64-104">Прокси приложения с Azure Active Directory и PingAccess партнерство вместе tooprovide клиентов Azure Active Directory с tooeven доступа нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="04e64-104">Azure Active Directory Application Proxy and PingAccess have partnered together tooprovide Azure Active Directory customers with access tooeven more applications.</span></span> <span data-ttu-id="04e64-105">PingAccess расширяет hello [существующие предложения прокси приложения](active-directory-application-proxy-get-started.md) tooapplications tooinclude единого входа, использовать заголовки для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="04e64-105">PingAccess expands hello [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) tooinclude single sign-on access tooapplications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="04e64-106">Что такое PingAccess для Azure AD?</span><span class="sxs-lookup"><span data-stu-id="04e64-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="04e64-107">PingAccess для Azure Active Directory — это предложение PingAccess, позволяющий toogive пользователям доступ и один tooapplications входа, использовать заголовки для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="04e64-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you toogive users access and single sign-on tooapplications that use headers for authentication.</span></span> <span data-ttu-id="04e64-108">Прокси приложения обрабатывает эти приложения, как и любой другой с помощью Azure AD tooauthenticate access и затем передачу трафика через службу соединителя hello.</span><span class="sxs-lookup"><span data-stu-id="04e64-108">Application Proxy treats these apps like any other, using Azure AD tooauthenticate access and then passing traffic through hello connector service.</span></span> <span data-ttu-id="04e64-109">PingAccess располагается перед приложения hello и преобразует hello токен доступа из Azure AD в заголовок, чтобы приложение hello получает hello проверки подлинности в формате hello, который может считывать.</span><span class="sxs-lookup"><span data-stu-id="04e64-109">PingAccess sits in front of hello apps and translates hello access token from Azure AD into a header so that hello application receives hello authentication in hello format it can read.</span></span>

<span data-ttu-id="04e64-110">Пользователи не будут Обратите внимание на то что-то иначе при входе в toouse корпоративных приложений.</span><span class="sxs-lookup"><span data-stu-id="04e64-110">Your users won’t notice anything different when they sign in toouse your corporate apps.</span></span> <span data-ttu-id="04e64-111">Они по-прежнему смогут работать в любом расположении и на любом устройстве.</span><span class="sxs-lookup"><span data-stu-id="04e64-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="04e64-112">Поскольку соединителей прокси приложения hello направлять трафик tooall приложения, независимо от их типа проверки подлинности, они автоматически, а также продолжим tooload баланс.</span><span class="sxs-lookup"><span data-stu-id="04e64-112">Since hello Application Proxy connectors direct remote traffic tooall apps regardless of their authentication type, they’ll continue tooload balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="04e64-113">Как мне получить доступ?</span><span class="sxs-lookup"><span data-stu-id="04e64-113">How do I get access?</span></span>

<span data-ttu-id="04e64-114">Так как этот сценарий предоставляется при совместном использовании Azure Active Directory и PingAccess, вам понадобятся лицензии для двух этих служб.</span><span class="sxs-lookup"><span data-stu-id="04e64-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="04e64-115">Однако подписок Azure Active Directory Premium включает основные PingAccess лицензии, которая закрывает too20 приложений.</span><span class="sxs-lookup"><span data-stu-id="04e64-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up too20 applications.</span></span> <span data-ttu-id="04e64-116">Если вам требуется toopublish более 20 приложений на основе заголовка, вы можете приобрести дополнительную лицензию PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-116">If you need toopublish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="04e64-117">Дополнительные сведения см. в разделе [Выпуски Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="04e64-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="04e64-118">Публикация приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="04e64-118">Publish your application in Azure</span></span>

<span data-ttu-id="04e64-119">Эта статья предназначена для тех, кто публикации приложения в этом сценарии для hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="04e64-119">This article is intended for people who are publishing an app with this scenario for hello first time.</span></span> <span data-ttu-id="04e64-120">Он рассматривается как tooget работу с приложением и PingAccess, кроме toohello шаги публикации.</span><span class="sxs-lookup"><span data-stu-id="04e64-120">It walks through how tooget started with both Application and PingAccess, in addition toohello publishing steps.</span></span> <span data-ttu-id="04e64-121">Если вы уже настроены обе службы, но хотите hello публикации действия в памяти, можно пропустить установки соединителя hello и переместить слишком[добавить вашего приложения tooAzure AD с помощью прокси приложения](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="04e64-121">If you’ve already configured both services but want a refresher on hello publishing steps, you can skip hello connector installation and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="04e64-122">Так как этот сценарий предполагает партнерство между Azure AD и PingAccess, некоторые инструкции hello существуют на hello сайта Ping удостоверений.</span><span class="sxs-lookup"><span data-stu-id="04e64-122">Since this scenario is a partnership between Azure AD and PingAccess, some of hello instructions exist on hello Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="04e64-123">Установка соединителя прокси приложения</span><span class="sxs-lookup"><span data-stu-id="04e64-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="04e64-124">Если вы уже есть прокси приложения включен, а также установлен соединитель, можно пропустить этот раздел и перейти слишком[добавить вашего приложения tooAzure AD с помощью прокси приложения](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="04e64-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="04e64-125">Соединитель прокси приложения Hello является сервером Windows служба, которая направляет трафик hello из вашего tooyour удаленные сотрудники опубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="04e64-125">hello Application Proxy connector is a Windows Server service that directs hello traffic from your remote employees tooyour published apps.</span></span> <span data-ttu-id="04e64-126">Более подробные инструкции по установке см. в разделе [включить прокси приложения в Azure portal hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="04e64-126">For more detailed installation instructions, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="04e64-127">Войдите в toohello [портал Azure](https://portal.azure.com) роли глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="04e64-127">Sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="04e64-128">Выберите **Azure Active Directory** > **Прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="04e64-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="04e64-129">Выберите **скачать соединитель** загрузки соединитель прокси приложения hello toostart.</span><span class="sxs-lookup"><span data-stu-id="04e64-129">Select **Download Connector** toostart hello Application Proxy connector download.</span></span> <span data-ttu-id="04e64-130">Следуйте инструкциям по установке hello.</span><span class="sxs-lookup"><span data-stu-id="04e64-130">Follow hello installation instructions.</span></span>

   ![Включите прокси приложения и загрузить соединитель hello](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="04e64-132">Загрузка hello connector автоматически следует включить прокси приложения для каталога, но если не вы можете выбрать **включите прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="04e64-132">Downloading hello connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a><span data-ttu-id="04e64-133">Добавить tooAzure вашего приложения AD с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="04e64-133">Add your app tooAzure AD with Application Proxy</span></span>

<span data-ttu-id="04e64-134">Существуют два действия, необходимые tootake в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="04e64-134">There are two actions you need tootake in hello Azure portal.</span></span> <span data-ttu-id="04e64-135">Во-первых необходимо toopublish приложения с помощью прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="04e64-135">First, you need toopublish your application with Application Proxy.</span></span> <span data-ttu-id="04e64-136">Затем необходимо toocollect некоторые сведения о приложение hello, который можно использовать во время действия PingAccess hello.</span><span class="sxs-lookup"><span data-stu-id="04e64-136">Then, you need toocollect some information about hello app that you can use during hello PingAccess steps.</span></span>

<span data-ttu-id="04e64-137">Выполните эти шаги toopublish приложения.</span><span class="sxs-lookup"><span data-stu-id="04e64-137">Follow these steps toopublish your app.</span></span> <span data-ttu-id="04e64-138">Более подробное пошаговое руководство по этапам 1–8 приведено в разделе [Публикация приложений с помощью прокси приложения Azure AD](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="04e64-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="04e64-139">Если не был в последний раздел hello войдите toohello [портал Azure](https://portal.azure.com) роли глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="04e64-139">If you didn't in hello last section, sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="04e64-140">Выберите **Azure Active Directory** > **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="04e64-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="04e64-141">Выберите **добавить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="04e64-141">Select **Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="04e64-142">Выберите **Локальное приложение**.</span><span class="sxs-lookup"><span data-stu-id="04e64-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="04e64-143">Заполните поля требуется hello со сведениями о нового приложения.</span><span class="sxs-lookup"><span data-stu-id="04e64-143">Fill out hello required fields with information about your new app.</span></span> <span data-ttu-id="04e64-144">Используйте следующие рекомендации для параметров hello hello.</span><span class="sxs-lookup"><span data-stu-id="04e64-144">Use hello following guidance for hello settings:</span></span>
   - <span data-ttu-id="04e64-145">**Внутренний URL-адрес**: обычно предоставляют hello URL-адрес, которое знакомит вас приложения toohello входа на странице при работе на hello корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="04e64-145">**Internal URL**: Normally you provide hello URL that takes you toohello app’s sign in page when you’re on hello corporate network.</span></span> <span data-ttu-id="04e64-146">В этом сценарии hello соединитель должен hello tootreat PingAccess прокси-сервера как hello обложке приложение hello.</span><span class="sxs-lookup"><span data-stu-id="04e64-146">For this scenario hello connector needs tootreat hello PingAccess proxy as hello front page of hello app.</span></span> <span data-ttu-id="04e64-147">Используйте следующий формат: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="04e64-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="04e64-148">порт Hello — 3000 по умолчанию, но его можно настроить в PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-148">hello port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="04e64-149">**Метод предварительной аутентификации** — выберите Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="04e64-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="04e64-150">**Преобразование URL-адреса в заголовок** — выберите значение "Нет".</span><span class="sxs-lookup"><span data-stu-id="04e64-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="04e64-151">Если это первое приложение, используйте порт 3000 toostart и вернуться tooupdate этот параметр при изменении конфигурации PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-151">If this is your first application, use port 3000 toostart and come back tooupdate this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="04e64-152">Если это второй или более поздней версии приложения, это потребуется toomatch hello прослушивателя, настроенного в PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-152">If this is your second or later app, this will need toomatch hello Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="04e64-153">Узнайте больше о [прослушивателях в PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="04e64-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="04e64-154">Выберите **добавить** hello нижней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="04e64-154">Select **Add** at hello bottom of hello blade.</span></span> <span data-ttu-id="04e64-155">Приложение добавляется, и откроется меню быстрого запуска "hello".</span><span class="sxs-lookup"><span data-stu-id="04e64-155">Your application is added, and hello quick start menu opens.</span></span>
7. <span data-ttu-id="04e64-156">Выберите в меню быстрого запуска hello **назначение пользователей для тестирования**и добавьте по крайней мере один пользователь toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="04e64-156">In hello quick start menu, select **Assign a user for testing**, and add at least one user toohello application.</span></span> <span data-ttu-id="04e64-157">Убедитесь, что эта учетная запись теста имеет доступ toohello локального приложения.</span><span class="sxs-lookup"><span data-stu-id="04e64-157">Make sure this test account has access toohello on-premises application.</span></span>
8. <span data-ttu-id="04e64-158">Выберите **назначить** назначение toosave hello тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="04e64-158">Select **Assign** toosave hello test user assignment.</span></span>
9. <span data-ttu-id="04e64-159">На панели управления приложения hello выберите **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="04e64-159">On hello app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="04e64-160">Выберите **входа на базе заголовок** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="04e64-160">Choose **Header-based sign-on** from hello drop-down menu.</span></span> <span data-ttu-id="04e64-161">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="04e64-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="04e64-162">Если вы впервые используете основано на заголовках единого входа необходимо tooinstall PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-162">If this is your first time using header-based single sign-on, you need tooinstall PingAccess.</span></span> <span data-ttu-id="04e64-163">toomake убедитесь, что ваша подписка Azure автоматически связывается с установленной PingAccess использование hello связи на этой странице-toodownload PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-163">toomake sure your Azure subscription is automatically associated with your PingAccess installation, use hello link on this single sign-on page toodownload PingAccess.</span></span> <span data-ttu-id="04e64-164">Теперь откройте сайт загрузки hello или продолжить toothis страницу позже.</span><span class="sxs-lookup"><span data-stu-id="04e64-164">You can open hello download site now, or come back toothis page later.</span></span> 

   ![Выбор единого входа на основе заголовка](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="04e64-166">Закройте колонку приложения hello Enterprise или прокрутить меню "все hello способом toohello левой tooreturn toohello Azure Active Directory".</span><span class="sxs-lookup"><span data-stu-id="04e64-166">Close hello Enterprise applications blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
12. <span data-ttu-id="04e64-167">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="04e64-167">Select **App registrations**.</span></span>

   ![Выбор "Регистрация приложений"](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="04e64-169">Приложения hello выберите только что добавленный, затем **URL-адреса ответа**.</span><span class="sxs-lookup"><span data-stu-id="04e64-169">Select hello app you just added, then **Reply URLs**.</span></span>

   ![Выбор "URL-адреса ответа"](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="04e64-171">Проверьте, toosee ли hello внешний URL-адрес, назначенный tooyour приложение на шаге 5 в списке URL-адреса ответа hello.</span><span class="sxs-lookup"><span data-stu-id="04e64-171">Check toosee if hello external URL that you assigned tooyour app in step 5 is in hello Reply URLs list.</span></span> <span data-ttu-id="04e64-172">В противном случае добавьте этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="04e64-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="04e64-173">В колонке параметров приложения hello, выберите **требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="04e64-173">On hello app settings blade, select **Required permissions**.</span></span>

  ![Выбор "Необходимые разрешения"](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="04e64-175">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="04e64-175">Select **Add**.</span></span> <span data-ttu-id="04e64-176">Hello API, выберите **Windows Azure Active Directory**, затем **выберите**.</span><span class="sxs-lookup"><span data-stu-id="04e64-176">For hello API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="04e64-177">Разрешения hello выберите **чтения и записи всех приложений** и **вход и чтение профиля пользователя**, затем **выберите** и **сделать**.</span><span class="sxs-lookup"><span data-stu-id="04e64-177">For hello permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Выбор разрешений](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a><span data-ttu-id="04e64-179">Собирать сведения о шагах PingAccess hello</span><span class="sxs-lookup"><span data-stu-id="04e64-179">Collect information for hello PingAccess steps</span></span>

1. <span data-ttu-id="04e64-180">В колонке параметров приложения щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="04e64-180">On your app settings blade, select **Properties**.</span></span> 

  ![Выбор "Свойства"](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="04e64-182">Сохранить hello **идентификатор приложения** значение.</span><span class="sxs-lookup"><span data-stu-id="04e64-182">Save hello **Application Id** value.</span></span> <span data-ttu-id="04e64-183">Используется для hello идентификатор клиента при настройке PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-183">This is used for hello client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="04e64-184">В колонке параметров приложения hello, выберите **ключей**.</span><span class="sxs-lookup"><span data-stu-id="04e64-184">On hello app settings blade, select **Keys**.</span></span>

  ![Выбор "Ключи"](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="04e64-186">Создайте ключ, введите описание ключа и выбрав дату окончания срока действия hello раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="04e64-186">Create a key by entering a key description and choosing an expiration date from hello drop-down menu.</span></span>
5. <span data-ttu-id="04e64-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="04e64-187">Select **Save**.</span></span> <span data-ttu-id="04e64-188">Отображается идентификатор GUID в hello **значение** поле.</span><span class="sxs-lookup"><span data-stu-id="04e64-188">A GUID appears in hello **Value** field.</span></span>

  <span data-ttu-id="04e64-189">Сохраните это значение, как будет toosee может его снова после закрыть это окно.</span><span class="sxs-lookup"><span data-stu-id="04e64-189">Save this value now, as you won’t be able toosee it again after you close this window.</span></span>

  ![Создание ключа](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="04e64-191">Закройте колонку регистрации приложения hello или прокрутить меню "все hello способом toohello левой tooreturn toohello Azure Active Directory".</span><span class="sxs-lookup"><span data-stu-id="04e64-191">Close hello App registrations blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
7. <span data-ttu-id="04e64-192">Выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="04e64-192">Select **Properties**.</span></span>
8. <span data-ttu-id="04e64-193">Сохранить hello **каталог с Идентификатором** GUID.</span><span class="sxs-lookup"><span data-stu-id="04e64-193">Save hello **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-toosend-custom-fields"></a><span data-ttu-id="04e64-194">Необязательно: обновление GraphAPI toosend настраиваемые поля</span><span class="sxs-lookup"><span data-stu-id="04e64-194">Optional - Update GraphAPI toosend custom fields</span></span>

<span data-ttu-id="04e64-195">Список маркеров безопасности, отправляемых Azure AD для проверки подлинности, см. в [справочнике по маркерам Azure AD](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="04e64-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="04e64-196">Пользовательское утверждение, отправляющий других токенов, используйте поле приложения hello tooset GraphAPI *acceptMappedClaims* слишком**True**.</span><span class="sxs-lookup"><span data-stu-id="04e64-196">If you need a custom claim that sends other tokens, use GraphAPI tooset hello app field *acceptMappedClaims* too**True**.</span></span> <span data-ttu-id="04e64-197">Эту конфигурацию можно использовать Azure AD Graph Explorer или Microsoft Graph toomake.</span><span class="sxs-lookup"><span data-stu-id="04e64-197">You can use either Azure AD Graph Explorer or MS Graph toomake this configuration.</span></span> 

<span data-ttu-id="04e64-198">В этом примере используется Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="04e64-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="04e64-199">Скачивание PingAccess и настройка приложения</span><span class="sxs-lookup"><span data-stu-id="04e64-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="04e64-200">Теперь, когда вы выполнили все действия установки hello Azure Active Directory, можно переместить на tooconfiguring PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-200">Now that you've completed all hello Azure Active Directory setup steps, you can move on tooconfiguring PingAccess.</span></span> 

<span data-ttu-id="04e64-201">Hello подробное описание процедуры hello PingAccess частью данного сценария продолжить в hello документации удостоверение Ping [PingAccess настройки для Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="04e64-201">hello detailed steps for hello PingAccess part of this scenario continue in hello Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="04e64-202">Эти шаги содержат пошаговые инструкции процессе hello Получение учетной записи PingAccess, если у вас его еще нет, установка hello PingAccess сервера и создание подключение к поставщику Azure AD OIDC с помощью hello каталог с Идентификатором, скопированный из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="04e64-202">Those steps walk you through hello process of getting a PingAccess account if you don't already have one, installing hello PingAccess Server, and creating an Azure AD OIDC Provider connection with hello Directory ID that you copied from hello Azure portal.</span></span> <span data-ttu-id="04e64-203">Затем используйте hello приложения идентификатор и ключ значения toocreate веб-сессию на PingAccess.</span><span class="sxs-lookup"><span data-stu-id="04e64-203">Then, you use hello Application ID and Key values toocreate a Web Session on PingAccess.</span></span> <span data-ttu-id="04e64-204">После этого вы сможете настроить сопоставление удостоверений и создать виртуальный узел, сайт и приложение.</span><span class="sxs-lookup"><span data-stu-id="04e64-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="04e64-205">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="04e64-205">Test your app</span></span>

<span data-ttu-id="04e64-206">Когда вы завершите выполнение этих шагов, ваше приложение будет настроено и запущено.</span><span class="sxs-lookup"><span data-stu-id="04e64-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="04e64-207">tootest, откройте браузер и перейдите toohello внешний URL-адрес, созданный при публикации приложения hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="04e64-207">tootest it, open a browser and navigate toohello external URL that you created when you published hello app in Azure.</span></span> <span data-ttu-id="04e64-208">Войдите с помощью hello тестовой учетной записи, назначенной toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="04e64-208">Sign in with hello test account that you assigned toohello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04e64-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04e64-209">Next steps</span></span>

- [<span data-ttu-id="04e64-210">Настройка PingAccess для Azure AD</span><span class="sxs-lookup"><span data-stu-id="04e64-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="04e64-211">Как прокси приложения Azure AD предоставляет единый вход?</span><span class="sxs-lookup"><span data-stu-id="04e64-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="04e64-212">Устранение неполадок прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="04e64-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
