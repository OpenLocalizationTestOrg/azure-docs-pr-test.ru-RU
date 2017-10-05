---
title: "Авторизация учетных записей разработчиков с помощью Azure Active Directory в службе управления API Azure | Документация Майкрософт"
description: "Узнайте, как авторизовать пользователей с помощью Azure Active Directory в управлении API"
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
ms.openlocfilehash: 7637e6419d17a2d75904fbe63df5f27d4be4bbe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="8fe4d-103">Авторизация учетных записей разработчиков с помощью Azure Active Directory в управлении API Azure</span><span class="sxs-lookup"><span data-stu-id="8fe4d-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="8fe4d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8fe4d-104">Overview</span></span>
<span data-ttu-id="8fe4d-105">В этом руководстве показывается, как включить доступ к порталу разработчика для пользователей из каталога Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="8fe4d-106">В этом руководстве также показано, как управлять группами пользователей Azure Active Directory путем добавления внешних групп, содержащих пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span></span>

> <span data-ttu-id="8fe4d-107">Для выполнения шагов в этом руководстве вам сначала потребуется Azure Active Directory для создания приложения.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span></span>
> 
> 

## <a name="how-to-authorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="8fe4d-108">Авторизация учетных записей разработчиков с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fe4d-108">How to authorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="8fe4d-109">Чтобы начать работу, щелкните **Портал издателя** на портале Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="8fe4d-110">Будет открыт портал издателя службы управления API.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-110">This takes you to the API Management publisher portal.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="8fe4d-112">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8fe4d-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="8fe4d-113">В меню **Управление API** слева выберите пункт **Безопасность**, а затем перейдите на вкладку **Внешние удостоверения**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span></span>

![External Identities][api-management-security-external-identities]

<span data-ttu-id="8fe4d-115">В меню **Azure Active Directory** (Внешние удостоверения).</span><span class="sxs-lookup"><span data-stu-id="8fe4d-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="8fe4d-116">Запишите **URL-адрес перенаправления** и переключитесь в Azure Active Directory на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span></span>

![External Identities][api-management-security-aad-new]

<span data-ttu-id="8fe4d-118">Нажмите кнопку **Добавить**, чтобы создать приложение Azure Active Directory, а затем установите флажок **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Добавление нового приложения Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="8fe4d-120">Введите понятное имя для приложения, установите флажок **Веб-приложение и/или веб-API**и нажмите кнопку «Далее».</span><span class="sxs-lookup"><span data-stu-id="8fe4d-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span></span>

![Новое приложение Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="8fe4d-122">В поле **URL-адрес входа**введите URL-адрес входа на свой портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span></span> <span data-ttu-id="8fe4d-123">В данном примере **URL-адрес входа** — `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="8fe4d-124">Для **URL-адреса ИД приложения**введите домен по умолчанию или пользовательский домен для Azure Active Directory и добавьте к нему уникальную строку.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span></span> <span data-ttu-id="8fe4d-125">В данном примере используется домен по умолчанию **https://contoso5api.onmicrosoft.com** с суффиксом **/api**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span></span>

![Свойства нового приложения Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="8fe4d-127">Нажмите кнопку с галочкой, чтобы сохранить и создать приложение, и переключитесь на вкладку **Настройка**, чтобы настроить новое приложение.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span></span>

![Новое приложение Azure Active Directory создано][api-management-new-aad-app-created]

<span data-ttu-id="8fe4d-129">Если для этого приложения будут использоваться несколько служб каталогов Azure Active Directory, нажмите кнопку **Да** для параметра **Приложение является мультитенантным**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="8fe4d-130">По умолчанию используется значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-130">The default is **No**.</span></span>

![Приложение является мультитенантным][api-management-aad-app-multi-tenant]

<span data-ttu-id="8fe4d-132">Скопируйте **URL-адрес перенаправления** в разделе **Azure Active Directory** на вкладке **Внешние удостоверения** портала издателя и вставьте его в текстовое поле **URL-адрес ответа**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span></span> 

![URL-адрес ответа][api-management-aad-reply-url]

<span data-ttu-id="8fe4d-134">Прокрутите вкладку настройки вниз, выберите раскрывающийся список **Разрешения приложения** и установите флажок **Чтение данных каталога**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Разрешения приложения][api-management-aad-app-permissions]

<span data-ttu-id="8fe4d-136">Выберите раскрывающийся список **Делегирование разрешений** и установите флажок **Включить вход и чтение профилей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Делегированные разрешения][api-management-aad-delegated-permissions]

> <span data-ttu-id="8fe4d-138">Дополнительные сведения о приложении и делегированных разрешениях см. в разделе, посвященном [доступу к API Graph][Accessing the Graph API].</span><span class="sxs-lookup"><span data-stu-id="8fe4d-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
> 
> 

<span data-ttu-id="8fe4d-139">Скопируйте **идентификатор клиента** в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-139">Copy the **Client Id** to the clipboard.</span></span>

![идентификатор клиента][api-management-aad-app-client-id]

<span data-ttu-id="8fe4d-141">Вернитесь на портал издателя и вставьте **идентификатор клиента** , скопированный из конфигурации приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span></span>

![Идентификатор клиента][api-management-client-id]

<span data-ttu-id="8fe4d-143">Вернитесь в конфигурацию Azure Active Directory, щелкните раскрывающийся список **Выбрать длительность** в разделе **Ключи** и укажите интервал.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="8fe4d-144">В данном примере используется интервал **1 год**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-144">In this example, **1 year** is used.</span></span>

![Ключ][api-management-aad-key-before-save]

<span data-ttu-id="8fe4d-146">Нажмите кнопку **Сохранить** , чтобы сохранить конфигурацию и отобразить ключ.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-146">Click **Save** to save the configuration and display the key.</span></span> <span data-ttu-id="8fe4d-147">Скопируйте этот ключ в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-147">Copy the key to the clipboard.</span></span>

> <span data-ttu-id="8fe4d-148">Запишите этот ключ.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-148">Make a note of this key.</span></span> <span data-ttu-id="8fe4d-149">После закрытия окна конфигурации Azure Active Directory нельзя будет снова отобразить ключ.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

![Ключ][api-management-aad-key-after-save]

<span data-ttu-id="8fe4d-151">Вернитесь на портал издателя и вставьте скопированный ключ в текстовое поле **Секрет клиента** .</span><span class="sxs-lookup"><span data-stu-id="8fe4d-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

![Секрет клиента][api-management-client-secret]

<span data-ttu-id="8fe4d-153">**Allowed Tenants** (Разрешенные клиенты) указывается, какие каталоги имеют доступ к API экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="8fe4d-154">Укажите домены экземпляров Azure Active Directory, к которым требуется предоставить доступ.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span></span> <span data-ttu-id="8fe4d-155">Несколько доменов можно разделять символами начала новой строки, пробелами или запятыми.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Allowed Tenants][api-management-client-allowed-tenants]


<span data-ttu-id="8fe4d-157">После указания требуемой конфигурации нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-157">Once the desired configuration is specified, click **Save**.</span></span>

![Сохранить][api-management-client-allowed-tenants-save]

<span data-ttu-id="8fe4d-159">После сохранения изменений пользователи в указанной Azure Active Directory могут входить на портал разработчика, выполняя действия, приведенные в разделе [Вход на портал разработчика с помощью учетной записи Azure Active Directory][Log in to the Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="8fe4d-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="8fe4d-160">В разделе **Разрешенные клиенты** можно указывать несколько доменов.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-160">Multiple domains can be specified in the **Allowed Tenants** section.</span></span> <span data-ttu-id="8fe4d-161">Прежде чем какой-либо пользователь сможет выполнить вход из домена, отличного от домена, в котором было зарегистрировано приложение, глобальный администратор этого другого домена должен предоставить разрешение для доступа приложения к данным каталога.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="8fe4d-162">Чтобы предоставить разрешение, глобальный администратор должен перейти по адресу `https://<URL of your developer portal>/aadadminconsent` (например, https://contoso.portal.azure-api.net/aadadminconsent), ввести имя домена клиента Active Directory, доступ к которому требуется предоставить, и щелкнуть "Отправить".</span><span class="sxs-lookup"><span data-stu-id="8fe4d-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span></span> <span data-ttu-id="8fe4d-163">В следующем примере глобальный администратор `miaoaad.onmicrosoft.com` пытается предоставить разрешение определенному порталу разработчика.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span></span> 

![Разрешения][api-management-aad-consent]

<span data-ttu-id="8fe4d-165">На следующем экране глобальному администратору будет предложено подтвердить предоставление разрешения.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span></span> 

![Разрешения][api-management-permissions-form]

> <span data-ttu-id="8fe4d-167">Если администратор, не являющийся глобальным, попытается выполнить вход до того, как глобальный администратор предоставит разрешения, то попытка входа завершится неудачно и появится экран сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-to-add-an-external-azure-active-directory-group"></a><span data-ttu-id="8fe4d-168">Добавление внешней группы Active Directory Azure</span><span class="sxs-lookup"><span data-stu-id="8fe4d-168">How to add an external Azure Active Directory Group</span></span>
<span data-ttu-id="8fe4d-169">После включения доступа для пользователей в Azure Active Directory вы можете добавлять группы Azure Active Directory в управление API, чтобы упростить управление связью разработчиков в такой группе с требуемыми продуктами.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span></span>

> <span data-ttu-id="8fe4d-170">Чтобы настроить внешнюю группу Azure Active Directory, необходимо сначала настроить Azure Active Directory на вкладке удостоверений, выполнив процедуру, описанную в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span></span> 
> 
> 

<span data-ttu-id="8fe4d-171">Внешние группы Azure Active Directory добавляются на вкладке **Видимость** продукта, к которому вы хотите предоставить доступ группе.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span></span> <span data-ttu-id="8fe4d-172">Щелкните пункт **Продукты**, а затем щелкните имя нужного продукта.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-172">Click **Products**, and then click the name of the desired product.</span></span>

![Настройка продукта][api-management-configure-product]

<span data-ttu-id="8fe4d-174">Переключитесь на вкладку **Видимость** и нажмите **Добавить группы из Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Добавление групп][api-management-add-groups]

<span data-ttu-id="8fe4d-176">Выберите в раскрывающемся списке пункт **Клиент Azure Active Directory**, а затем введите имя группы, которую нужно добавить, в текстовом поле **Группы**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span></span>

![Выбор группы][api-management-select-group]

<span data-ttu-id="8fe4d-178">Имя этой группы можно найти в списке **Группы** для Azure Active Directory, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span></span>

![Список групп Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="8fe4d-180">Нажмите кнопку **Добавить** , чтобы проверить имя группы и добавить ее.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-180">Click **Add** to validate the group name and add the group.</span></span> <span data-ttu-id="8fe4d-181">В данном примере добавляется внешняя группа **Разработчики Contoso 5**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-181">In this example, the **Contoso 5 Developers** external group is added.</span></span> 

![Группа добавлена][api-management-aad-group-added]

<span data-ttu-id="8fe4d-183">Нажмите кнопку **Сохранить** , чтобы сохранить выбор новой группы.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-183">Click **Save** to save the new group selection.</span></span>

<span data-ttu-id="8fe4d-184">После настройки группы Azure Active Directory в одном продукте ее можно включать на вкладке **Видимость** для других продуктов в этом экземпляре службы управления API.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span></span>

<span data-ttu-id="8fe4d-185">Чтобы просмотреть и настроить свойства внешних групп после их добавления, щелкните имя группы на вкладке **Группы**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span></span>

![Управление группами][api-management-groups]

<span data-ttu-id="8fe4d-187">Здесь можно изменить **имя** и **описание** группы.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-187">From here you can edit the **Name** and the **Description** of the group.</span></span>

![Изменение группы][api-management-edit-group]

<span data-ttu-id="8fe4d-189">Пользователи из настроенных служб каталогов Azure Active Directory могут входить на портал разработчика, а затем просматривать и подписываться на любые группы, которые они могут видеть, выполняя инструкции из следующего раздела.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span></span>

## <a name="how-to-log-in-to-the-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="8fe4d-190">Вход на портал разработчика с помощью учетной записи Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fe4d-190">How to log in to the Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="8fe4d-191">Чтобы войти на портал разработчика с помощью учетной записи Azure Active Directory, настроенной в предыдущих разделах, откройте новое окно браузера с помощью **URL-адреса входа** из конфигурации приложения Active Directory и нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Портал разработчика][api-management-dev-portal-signin]

<span data-ttu-id="8fe4d-193">Введите учетные данные одного из пользователей в Azure Active Directory и нажмите кнопку **Вход**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span></span>

![Вход][api-management-aad-signin]

<span data-ttu-id="8fe4d-195">Может появиться запрос с регистрационной формой, если требуются какие-либо дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="8fe4d-196">Заполните эту регистрационную форму и нажмите кнопку **Регистрация**.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-196">Complete the registration form and click **Sign up**.</span></span>

![Регистрация][api-management-complete-registration]

<span data-ttu-id="8fe4d-198">Теперь этот пользователь вошел на портал разработчика для вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="8fe4d-198">Your user is now logged into the developer portal for your API Management service instance.</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

