---
title: "aaaGet работы с Azure Active Directory Identity Protection и Microsoft Graph | Документы Microsoft"
description: "Предоставляет введение tooquery Microsoft Graph для списка событий риска и связанные данные из Azure Active Directory."
services: active-directory
keywords: "защита идентификации azure active directory, события риска, уязвимость, политика безопасности, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="9d463-104">Начало работы с защитой идентификации Azure Active Directory и Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="9d463-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="9d463-105">Microsoft Graph является Microsoft unified конечная точка API hello и домашних hello объекта [Azure Active Directory Identity Protection](active-directory-identityprotection.md) API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="9d463-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="9d463-106">Первый API Hello, **identityRiskEvents**, позволяет вам tooquery Microsoft Graph список из [риск события](active-directory-identityprotection-risk-events-types.md) и связанные сведения.</span><span class="sxs-lookup"><span data-stu-id="9d463-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="9d463-107">В статье описывается, как выполнять запросы к этому API.</span><span class="sxs-lookup"><span data-stu-id="9d463-107">This article gets you started querying this API.</span></span> <span data-ttu-id="9d463-108">Подробное введение, Полная документация и toohello доступа Graph Explorer, в разделе hello [сайта Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="9d463-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d463-109">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9d463-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="9d463-110">Существует три действия tooaccessing защиты учетных данных через Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="9d463-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="9d463-111">Добавление приложения с секретом клиента.</span><span class="sxs-lookup"><span data-stu-id="9d463-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="9d463-112">Используйте этот секрет и несколько фрагментов tooMicrosoft tooauthenticate сведения о графике, где происходит получение маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9d463-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="9d463-113">Используйте эту конечную точку token toomake запросов toohello API и возврата защиты учетных данных.</span><span class="sxs-lookup"><span data-stu-id="9d463-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="9d463-114">Перед началом работы вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="9d463-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="9d463-115">Приложение hello toocreate права администратора в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d463-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="9d463-116">Hello имя домена для вашего клиента (например, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="9d463-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="9d463-117">Добавление приложения с секретом клиента</span><span class="sxs-lookup"><span data-stu-id="9d463-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="9d463-118">[Войдите в](https://manage.windowsazure.com) tooyour классический портал Azure с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="9d463-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="9d463-119">На панели навигации слева hello, щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d463-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="9d463-121">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="9d463-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="9d463-122">В меню в верхней части hello hello выберите **приложений**.</span><span class="sxs-lookup"><span data-stu-id="9d463-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="9d463-124">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="9d463-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="9d463-126">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="9d463-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="9d463-128">На hello **Расскажите о своем приложении** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9d463-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="9d463-130">а.</span><span class="sxs-lookup"><span data-stu-id="9d463-130">a.</span></span> <span data-ttu-id="9d463-131">В hello **имя** текстовом поле введите имя для приложения (например: AADIP риск события API приложения).</span><span class="sxs-lookup"><span data-stu-id="9d463-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="9d463-132">b.</span><span class="sxs-lookup"><span data-stu-id="9d463-132">b.</span></span> <span data-ttu-id="9d463-133">В качестве **типа** выберите **Веб-приложение и/или веб-API**.</span><span class="sxs-lookup"><span data-stu-id="9d463-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="9d463-134">В.</span><span class="sxs-lookup"><span data-stu-id="9d463-134">c.</span></span> <span data-ttu-id="9d463-135">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9d463-135">Click **Next**.</span></span>
8. <span data-ttu-id="9d463-136">На hello **свойства приложения** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9d463-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="9d463-138">а.</span><span class="sxs-lookup"><span data-stu-id="9d463-138">a.</span></span> <span data-ttu-id="9d463-139">В hello **URL-адрес входа** введите `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="9d463-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="9d463-140">b.</span><span class="sxs-lookup"><span data-stu-id="9d463-140">b.</span></span> <span data-ttu-id="9d463-141">В hello **URI идентификатора приложения** введите `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="9d463-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="9d463-142">c.</span><span class="sxs-lookup"><span data-stu-id="9d463-142">c.</span></span> <span data-ttu-id="9d463-143">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="9d463-143">Click **Complete**.</span></span>

<span data-ttu-id="9d463-144">Теперь вы можете настроить приложение.</span><span class="sxs-lookup"><span data-stu-id="9d463-144">Your can now configure your application.</span></span>

![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="9d463-146">Предоставьте разрешение hello toouse API вашего приложения</span><span class="sxs-lookup"><span data-stu-id="9d463-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="9d463-147">На странице приложения hello меню в верхней части страницы приветствия щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="9d463-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="9d463-149">В hello **разрешения приложений tooother** щелкните **добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="9d463-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="9d463-151">На hello **tooother разрешения приложений** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9d463-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="9d463-153">а.</span><span class="sxs-lookup"><span data-stu-id="9d463-153">a.</span></span> <span data-ttu-id="9d463-154">Выберите **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="9d463-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="9d463-155">b.</span><span class="sxs-lookup"><span data-stu-id="9d463-155">b.</span></span> <span data-ttu-id="9d463-156">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="9d463-156">Click **Complete**.</span></span>
4. <span data-ttu-id="9d463-157">Щелкните **Разрешения приложения: 0**, а затем выберите **Read all identity risk event information** (Прочитать все сведения о событиях риска идентификации).</span><span class="sxs-lookup"><span data-stu-id="9d463-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="9d463-159">Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="9d463-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="9d463-161">Получение ключа доступа</span><span class="sxs-lookup"><span data-stu-id="9d463-161">Get an access key</span></span>
1. <span data-ttu-id="9d463-162">На странице приложения hello **ключей** выберите год в виде длительности.</span><span class="sxs-lookup"><span data-stu-id="9d463-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="9d463-164">Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="9d463-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="9d463-166">в разделе "ключи" hello скопируйте значение hello созданного ключа и вставьте его в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="9d463-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="9d463-168">При утере этот ключ будет иметь tooreturn toothis раздел и создать новый ключ.</span><span class="sxs-lookup"><span data-stu-id="9d463-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="9d463-169">Не предоставляйте этот ключ никому: с его помощью кто угодно может получить доступ к вашим данным.</span><span class="sxs-lookup"><span data-stu-id="9d463-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="9d463-170">В hello **свойства** раздел, hello копирования **идентификатор клиента**и вставьте его в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="9d463-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="9d463-171">Проверка подлинности tooMicrosoft Graph и hello запроса API событий риска удостоверения</span><span class="sxs-lookup"><span data-stu-id="9d463-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="9d463-172">На этом этапе вам понадобятся:</span><span class="sxs-lookup"><span data-stu-id="9d463-172">At this point, you should have:</span></span>

* <span data-ttu-id="9d463-173">Идентификатор клиента Hello, скопированные выше</span><span class="sxs-lookup"><span data-stu-id="9d463-173">hello client ID you copied above</span></span>
* <span data-ttu-id="9d463-174">ключ Hello, скопированные выше</span><span class="sxs-lookup"><span data-stu-id="9d463-174">hello key you copied above</span></span>
* <span data-ttu-id="9d463-175">Hello имя домена клиента</span><span class="sxs-lookup"><span data-stu-id="9d463-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="9d463-176">tooauthenticate отправляет post запроса слишком`https://login.microsoft.com` с помощью следующих параметров в тексте hello hello:</span><span class="sxs-lookup"><span data-stu-id="9d463-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="9d463-177">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="9d463-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="9d463-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="9d463-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="9d463-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="9d463-179">client_id: <your client ID></span></span>
* <span data-ttu-id="9d463-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="9d463-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="9d463-181">Для hello, требуются значения tooprovide **client_id** и hello **client_secret** параметра.</span><span class="sxs-lookup"><span data-stu-id="9d463-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="9d463-182">В случае успешного выполнения этот метод возвращает маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9d463-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="9d463-183">hello toocall API, создайте заголовок с hello следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="9d463-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="9d463-184">При проверке подлинности, можно найти в hello вернул токен тип токена hello и маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="9d463-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="9d463-185">Отправьте этот заголовок как toohello запроса, URL-адреса API:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="9d463-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="9d463-186">в случае успешного ответа Hello представляет собой коллекцию идентификаторов событий риска и связанные данные в формате OData JSON, который можно проанализировать и обрабатывать по усмотрению hello.</span><span class="sxs-lookup"><span data-stu-id="9d463-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="9d463-187">Ниже приведен пример кода для проверки подлинности и вызова API hello, с помощью Powershell.</span><span class="sxs-lookup"><span data-stu-id="9d463-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="9d463-188">Просто добавьте идентификатор клиента, ключ и домен клиента.</span><span class="sxs-lookup"><span data-stu-id="9d463-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="9d463-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d463-189">Next steps</span></span>
<span data-ttu-id="9d463-190">Итак, вы только что внесли tooMicrosoft вашего первого вызова Graph.</span><span class="sxs-lookup"><span data-stu-id="9d463-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="9d463-191">Теперь можно запрашивать события рисков удостоверений и используют hello данных, однако вам кажется подходящим.</span><span class="sxs-lookup"><span data-stu-id="9d463-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="9d463-192">toolearn Дополнительные сведения о Microsoft Graph и как с помощью приложения toobuild hello Graph API извлечь hello [документации](https://graph.microsoft.io/docs) и многое другое на hello [сайта Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="9d463-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="9d463-193">Кроме того, убедитесь, что hello toobookmark [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) страницы, где перечислены все hello Identity Protection API-интерфейса в граф.</span><span class="sxs-lookup"><span data-stu-id="9d463-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="9d463-194">При добавлении новых способов toowork с защитой удостоверений через API-Интерфейс, вы увидите их на этой странице.</span><span class="sxs-lookup"><span data-stu-id="9d463-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d463-195">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9d463-195">Additional resources</span></span>
* [<span data-ttu-id="9d463-196">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d463-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="9d463-197">Типы событий риска, обнаруживаемые защитой идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d463-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="9d463-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="9d463-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="9d463-199">Overview of Microsoft Graph (Обзор Microsoft Graph)</span><span class="sxs-lookup"><span data-stu-id="9d463-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="9d463-200">Azure AD Identity Protection Service Root (Корень службы защиты идентификации Azure AD)</span><span class="sxs-lookup"><span data-stu-id="9d463-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

