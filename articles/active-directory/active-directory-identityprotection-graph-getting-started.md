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
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Начало работы с защитой идентификации Azure Active Directory и Microsoft Graph
Microsoft Graph является Microsoft unified конечная точка API hello и домашних hello объекта [Azure Active Directory Identity Protection](active-directory-identityprotection.md) API-интерфейсы. Первый API Hello, **identityRiskEvents**, позволяет вам tooquery Microsoft Graph список из [риск события](active-directory-identityprotection-risk-events-types.md) и связанные сведения. В статье описывается, как выполнять запросы к этому API. Подробное введение, Полная документация и toohello доступа Graph Explorer, в разделе hello [сайта Microsoft Graph](https://graph.microsoft.io/).

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.

Существует три действия tooaccessing защиты учетных данных через Microsoft Graph.

1. Добавление приложения с секретом клиента. 
2. Используйте этот секрет и несколько фрагментов tooMicrosoft tooauthenticate сведения о графике, где происходит получение маркера проверки подлинности. 
3. Используйте эту конечную точку token toomake запросов toohello API и возврата защиты учетных данных.

Перед началом работы вам потребуются:

* Приложение hello toocreate права администратора в Azure AD
* Hello имя домена для вашего клиента (например, contoso.onmicrosoft.com)

## <a name="add-an-application-with-a-client-secret"></a>Добавление приложения с секретом клиента
1. [Войдите в](https://manage.windowsazure.com) tooyour классический портал Azure с правами администратора. 
2. На панели навигации слева hello, щелкните **Active Directory**. 
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
4. В меню в верхней части hello hello выберите **приложений**.
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение, разрабатываемое моей организацией**.
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. На hello **Расскажите о своем приложении** диалоговое окно, выполните следующие шаги hello:
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    а. В hello **имя** текстовом поле введите имя для приложения (например: AADIP риск события API приложения).
   
    b. В качестве **типа** выберите **Веб-приложение и/или веб-API**.
   
    В. Щелкните **Далее**.
8. На hello **свойства приложения** диалоговое окно, выполните следующие шаги hello:
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    а. В hello **URL-адрес входа** введите `http://localhost`.
   
    b. В hello **URI идентификатора приложения** введите `http://localhost`.
   
    c. Нажмите **Завершено**.

Теперь вы можете настроить приложение.

![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Предоставьте разрешение hello toouse API вашего приложения
1. На странице приложения hello меню в верхней части страницы приветствия щелкните **Настройка**. 
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. В hello **разрешения приложений tooother** щелкните **добавить приложение**.
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. На hello **tooother разрешения приложений** диалоговое окно, выполните следующие шаги hello:
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    а. Выберите **Microsoft Graph**.
   
    b. Нажмите **Завершено**.
4. Щелкните **Разрешения приложения: 0**, а затем выберите **Read all identity risk event information** (Прочитать все сведения о событиях риска идентификации).
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Получение ключа доступа
1. На странице приложения hello **ключей** выберите год в виде длительности.
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. в разделе "ключи" hello скопируйте значение hello созданного ключа и вставьте его в безопасном месте.
   
    ![Создание приложения](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > При утере этот ключ будет иметь tooreturn toothis раздел и создать новый ключ. Не предоставляйте этот ключ никому: с его помощью кто угодно может получить доступ к вашим данным.
   > 
   > 
4. В hello **свойства** раздел, hello копирования **идентификатор клиента**и вставьте его в безопасном месте. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>Проверка подлинности tooMicrosoft Graph и hello запроса API событий риска удостоверения
На этом этапе вам понадобятся:

* Идентификатор клиента Hello, скопированные выше
* ключ Hello, скопированные выше
* Hello имя домена клиента

tooauthenticate отправляет post запроса слишком`https://login.microsoft.com` с помощью следующих параметров в тексте hello hello:

* grant_type: “**client_credentials**”
* resource: “**https://graph.microsoft.com**”
* client_id: <your client ID>
* client_secret: <your key>

> [!NOTE]
> Для hello, требуются значения tooprovide **client_id** и hello **client_secret** параметра.
> 
> 

В случае успешного выполнения этот метод возвращает маркер проверки подлинности.  
hello toocall API, создайте заголовок с hello следующий параметр:

    `Authorization`=”<token_type> <access_token>"


При проверке подлинности, можно найти в hello вернул токен тип токена hello и маркер доступа.

Отправьте этот заголовок как toohello запроса, URL-адреса API:`https://graph.microsoft.com/beta/identityRiskEvents`

в случае успешного ответа Hello представляет собой коллекцию идентификаторов событий риска и связанные данные в формате OData JSON, который можно проанализировать и обрабатывать по усмотрению hello.

Ниже приведен пример кода для проверки подлинности и вызова API hello, с помощью Powershell.  
Просто добавьте идентификатор клиента, ключ и домен клиента.

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


## <a name="next-steps"></a>Дальнейшие действия
Итак, вы только что внесли tooMicrosoft вашего первого вызова Graph.  
Теперь можно запрашивать события рисков удостоверений и используют hello данных, однако вам кажется подходящим.

toolearn Дополнительные сведения о Microsoft Graph и как с помощью приложения toobuild hello Graph API извлечь hello [документации](https://graph.microsoft.io/docs) и многое другое на hello [сайта Microsoft Graph](https://graph.microsoft.io/). Кроме того, убедитесь, что hello toobookmark [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) страницы, где перечислены все hello Identity Protection API-интерфейса в граф. При добавлении новых способов toowork с защитой удостоверений через API-Интерфейс, вы увидите их на этой странице.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Защита идентификации Azure Active Directory.](active-directory-identityprotection.md)
* [Типы событий риска, обнаруживаемые защитой идентификации Azure Active Directory](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Overview of Microsoft Graph (Обзор Microsoft Graph)](https://graph.microsoft.io/docs)
* [Azure AD Identity Protection Service Root (Корень службы защиты идентификации Azure AD)](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

