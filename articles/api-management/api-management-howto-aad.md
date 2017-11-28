---
title: "с помощью Azure Active Directory - Azure API управления учетными записями разработчиков aaaAuthorize | Документы Microsoft"
description: "Узнайте, каким образом tooauthorize пользователей с помощью Azure Active Directory в службе управления API."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="f1a58-103">Как разработчик tooauthorize учетных записей с помощью Azure Active Directory в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="f1a58-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="f1a58-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f1a58-104">Overview</span></span>
<span data-ttu-id="f1a58-105">В этом руководстве показано, как tooenable доступ к toohello портал разработчиков для пользователей из Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1a58-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="f1a58-106">В этом руководстве также показано, как группы пользователей Azure Active Directory, добавив внешней группы, содержащие toomanage hello пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1a58-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="f1a58-107">toocomplete hello шаги в этом руководстве сначала нужно Azure Active Directory в какие toocreate приложения.</span><span class="sxs-lookup"><span data-stu-id="f1a58-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="f1a58-108">Как разработчик tooauthorize учетных записей с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1a58-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="f1a58-109">tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для вашей службе управления API.</span><span class="sxs-lookup"><span data-stu-id="f1a58-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="f1a58-110">Откроется портал издателя управления API toohello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-110">This takes you toohello API Management publisher portal.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="f1a58-112">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="f1a58-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="f1a58-113">Нажмите кнопку **безопасности** из hello **API управления** меню hello слева и щелкните **внешних удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![External Identities][api-management-security-external-identities]

<span data-ttu-id="f1a58-115">В меню **Azure Active Directory** (Внешние удостоверения).</span><span class="sxs-lookup"><span data-stu-id="f1a58-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="f1a58-116">Запишите hello **URL-адрес перенаправления** и переключении tooyour Azure Active Directory в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a58-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![External Identities][api-management-security-aad-new]

<span data-ttu-id="f1a58-118">Нажмите кнопку hello **добавить** toocreate новое приложение Azure Active Directory, а кнопку **добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Добавление нового приложения Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="f1a58-120">Введите имя для приложения hello, выберите **веб-приложение или веб-API**и нажмите кнопку Далее hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![Новое приложение Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="f1a58-122">Для **URL-адрес входа**, введите hello URL-адрес входа портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="f1a58-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="f1a58-123">В этом примере hello **URL-адрес входа** — `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="f1a58-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="f1a58-124">Для hello **URL ИД приложения**, введите домен по умолчанию hello или пользовательского домена для hello Azure Active Directory и добавьте tooit уникальная строка.</span><span class="sxs-lookup"><span data-stu-id="f1a58-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="f1a58-125">В этом примере hello домен по умолчанию **https://contoso5api.onmicrosoft.com** используется с суффиксом hello **/api** указанного.</span><span class="sxs-lookup"><span data-stu-id="f1a58-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![Свойства нового приложения Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="f1a58-127">Щелкните toosave кнопку флажок hello и создание приложения hello и переключение toohello **Настройка** вкладке tooconfigure hello нового приложения.</span><span class="sxs-lookup"><span data-stu-id="f1a58-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![Новое приложение Azure Active Directory создано][api-management-new-aad-app-created]

<span data-ttu-id="f1a58-129">Если в нескольких каталогах Azure Active Directory будет toobe, используемый для этого приложения, нажмите кнопку **Да** для **приложение является мультитенантным**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="f1a58-130">по умолчанию Hello — **нет**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-130">hello default is **No**.</span></span>

![Приложение является мультитенантным][api-management-aad-app-multi-tenant]

<span data-ttu-id="f1a58-132">Копировать hello **URL-адрес перенаправления** из hello **Azure Active Directory** раздел hello **внешних удостоверений** вкладку в портале издателю hello и вставьте его в hello **URL-адрес ответа** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="f1a58-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![URL-адрес ответа][api-management-aad-reply-url]

<span data-ttu-id="f1a58-134">Вкладка, выберите hello настройки прокрутки внизу toohello hello **разрешения приложения** раскрывающийся список и проверьте **читать данные каталога**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Разрешения приложения][api-management-aad-app-permissions]

<span data-ttu-id="f1a58-136">Выберите hello **Делегирование разрешений** раскрывающийся список и проверьте **разрешить вход и чтение профилей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Делегированные разрешения][api-management-aad-delegated-permissions]

> <span data-ttu-id="f1a58-138">Дополнительные сведения о приложении и делегированные разрешения см. в разделе [hello доступ к Graph API][Accessing hello Graph API].</span><span class="sxs-lookup"><span data-stu-id="f1a58-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="f1a58-139">Копировать hello **идентификатор клиента** toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="f1a58-139">Copy hello **Client Id** toohello clipboard.</span></span>

![Идентификатор клиента][api-management-aad-app-client-id]

<span data-ttu-id="f1a58-141">Перейдите назад toohello портал издателя и вставьте в hello **идентификатор клиента** копируется из конфигурации приложения hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1a58-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![Идентификатор клиента][api-management-client-id]

<span data-ttu-id="f1a58-143">Перейдите назад toohello конфигурацию Azure Active Directory, а щелкните hello **выберите длительность** раскрывающееся меню в hello **ключей** статьи и указать интервал.</span><span class="sxs-lookup"><span data-stu-id="f1a58-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="f1a58-144">В данном примере используется интервал **1 год**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-144">In this example, **1 year** is used.</span></span>

![Ключ][api-management-aad-key-before-save]

<span data-ttu-id="f1a58-146">Нажмите кнопку **Сохранить** toosave hello конфигурации и отображения hello ключ.</span><span class="sxs-lookup"><span data-stu-id="f1a58-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="f1a58-147">Буфер обмена Копировать hello toohello ключа.</span><span class="sxs-lookup"><span data-stu-id="f1a58-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="f1a58-148">Запишите этот ключ.</span><span class="sxs-lookup"><span data-stu-id="f1a58-148">Make a note of this key.</span></span> <span data-ttu-id="f1a58-149">После закрытия окна конфигурации hello Azure Active Directory hello ключ не будет отображаться в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="f1a58-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Ключ][api-management-aad-key-after-save]

<span data-ttu-id="f1a58-151">Коммутатор задней toohello портала и вставить hello ключ издателя в hello **секрет клиента** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="f1a58-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![Секрет клиента][api-management-client-secret]

<span data-ttu-id="f1a58-153">**Допускается клиентов** указывает, какие каталоги имеют доступ toohello API-интерфейсов экземпляра службы управления API hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="f1a58-154">Укажите домены hello hello вы хотите получить доступ toogrant toowhich экземпляров Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1a58-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="f1a58-155">Несколько доменов можно разделять символами начала новой строки, пробелами или запятыми.</span><span class="sxs-lookup"><span data-stu-id="f1a58-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Allowed Tenants][api-management-client-allowed-tenants]


<span data-ttu-id="f1a58-157">Когда hello требуемого указана конфигурация, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-157">Once hello desired configuration is specified, click **Save**.</span></span>

![Сохранить][api-management-client-allowed-tenants-save]

<span data-ttu-id="f1a58-159">После сохранения изменений hello пользователей hello в hello указан Azure Active Directory можно войти в портал разработчиков toohello, следуя указаниям hello [вход с использованием учетной записи Azure Active Directory портал разработчиков toohello] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="f1a58-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="f1a58-160">Можно указать несколько доменов в hello **клиентам разрешено** раздела.</span><span class="sxs-lookup"><span data-stu-id="f1a58-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="f1a58-161">Перед любой пользователь может входить в систему с разных доменах hello исходного домена, где зарегистрирован приложения hello, является глобальным администратором другого домена hello должен давать разрешение tooaccess приложения hello данных каталога.</span><span class="sxs-lookup"><span data-stu-id="f1a58-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="f1a58-162">разрешение toogrant hello глобальный администратор должен составлять слишком`https://<URL of your developer portal>/aadadminconsent` (например, https://contoso.portal.azure-api.net/aadadminconsent), тип в доменном имени hello hello им нужен доступ tooand toogive клиента Active Directory, нажмите кнопку Отправить.</span><span class="sxs-lookup"><span data-stu-id="f1a58-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="f1a58-163">В следующих hello пример, глобальный администратор `miaoaad.onmicrosoft.com` пытается toogive разрешение toothis определенного портал.</span><span class="sxs-lookup"><span data-stu-id="f1a58-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![Разрешения][api-management-aad-consent]

<span data-ttu-id="f1a58-165">В следующем экране hello hello глобального администратора будет запрашиваемые tooconfirm, предоставление разрешения hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![Разрешения][api-management-permissions-form]

> <span data-ttu-id="f1a58-167">Если веб-глобального администратора toolog в до разрешения предоставляются глобальным администратором, неудачной попытки входа hello и отображается экран ошибки.</span><span class="sxs-lookup"><span data-stu-id="f1a58-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="f1a58-168">Как tooadd внешних Azure Active Directory группы</span><span class="sxs-lookup"><span data-stu-id="f1a58-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="f1a58-169">После включения доступа для пользователей в Azure Active Directory, можно добавить группы Azure Active Directory в API управления toomore легко управлять ассоциации hello разработчиков hello в группе hello с продуктами требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="f1a58-170">Вначале нужно настроить tooconfigure внешней группы Azure Active Directory, hello Azure Active Directory на вкладке hello удостоверения с помощью процедуры hello в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="f1a58-171">Внешние группы Azure Active Directory добавляются из hello **видимость** вкладку hello продукта, для которого вы хотите группу toohello toogrant доступа.</span><span class="sxs-lookup"><span data-stu-id="f1a58-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="f1a58-172">Нажмите кнопку **продуктов**и щелкните имя нужного продукта hello hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Настройка продукта][api-management-configure-product]

<span data-ttu-id="f1a58-174">Переключение toohello **видимость** и нажмите кнопку **Добавление групп из Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Добавление групп][api-management-add-groups]

<span data-ttu-id="f1a58-176">Выберите hello **клиента Azure Active Directory** из hello раскрывающегося списка, а затем имя нужной группы hello в hello типа hello **группы** toobe добавлено текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="f1a58-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![Выбор группы][api-management-select-group]

<span data-ttu-id="f1a58-178">Имя этой группы могут находиться в hello **группы** список для Azure Active Directory, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Список групп Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="f1a58-180">Нажмите кнопку **добавить** toovalidate hello имя группы и добавить группу hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="f1a58-181">В этом примере hello **разработчики 5 Contoso** внешней группы будет добавлен.</span><span class="sxs-lookup"><span data-stu-id="f1a58-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Группа добавлена][api-management-aad-group-added]

<span data-ttu-id="f1a58-183">Нажмите кнопку **Сохранить** toosave hello новое выделение группы.</span><span class="sxs-lookup"><span data-stu-id="f1a58-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="f1a58-184">После настройки группы Azure Active Directory из одного продукта является доступной toobe проверяется для hello **видимость** вкладке hello других продуктов в hello экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="f1a58-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="f1a58-185">tooreview и настроить свойства hello для внешних групп, как только они были добавлены, щелкните имя hello hello группы из hello **группы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f1a58-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![Управление группами][api-management-groups]

<span data-ttu-id="f1a58-187">Здесь можно изменить hello **имя** и hello **описание** hello группы.</span><span class="sxs-lookup"><span data-stu-id="f1a58-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![Изменение группы][api-management-edit-group]

<span data-ttu-id="f1a58-189">Пользователям hello настроенных Azure Active Directory можно войти в портал разработчиков toohello и представление и подписаться tooany группы, для которых они имеют видимость по инструкциям hello в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="f1a58-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="f1a58-190">Как toolog на портале разработчиков toohello, используя учетную запись Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1a58-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="f1a58-191">toolog в портал разработчиков hello, используя учетную запись Azure Active Directory настроен в предыдущих разделах hello, откройте новое окно браузера, используя hello **URL-адрес входа** из конфигурации приложения hello Active Directory и нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Портал разработчика][api-management-dev-portal-signin]

<span data-ttu-id="f1a58-193">Введите учетные данные hello одного из пользователей hello в Azure Active Directory и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![входа][api-management-aad-signin]

<span data-ttu-id="f1a58-195">Может появиться запрос с регистрационной формой, если требуются какие-либо дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="f1a58-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="f1a58-196">Заполните форму регистрации hello и нажмите кнопку **зарегистрироваться**.</span><span class="sxs-lookup"><span data-stu-id="f1a58-196">Complete hello registration form and click **Sign up**.</span></span>

![Регистрация][api-management-complete-registration]

<span data-ttu-id="f1a58-198">Теперь ваш пользователь вошел в портале для разработчиков hello для вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="f1a58-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

![Регистрация завершена][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

