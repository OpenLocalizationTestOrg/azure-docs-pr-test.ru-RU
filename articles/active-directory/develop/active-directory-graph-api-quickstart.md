---
title: "aaaQuickstart для hello API Azure AD Graph | Документы Microsoft"
description: "Hello Azure Active Directory Graph API обеспечивает программный доступ tooAzure AD через конечные точки API-интерфейса REST OData. Приложения могут использовать Graph API tooperform hello создания, чтения, обновления и удаления (CRUD) с данными и объектами каталогов."
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Краткое руководство по hello API Azure AD Graph
Hello API Graph Azure Active Directory (AD) предоставляет программный доступ tooAzure AD через конечные точки API-интерфейса REST OData. Приложения могут использовать Graph API tooperform hello создания, чтения, обновления и удаления (CRUD) с данными и объектами каталогов. Например можно использовать Graph API hello toocreate нового пользователя, представление или обновления свойств пользователя, изменения пароля пользователя, проверять членство в группе для доступа на основе ролей, отключение или удаление пользователя hello. Дополнительные сведения о функциях Graph API hello и сценарии приложений см. в разделе [API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) и [необходимые компоненты API Azure AD Graph](https://msdn.microsoft.com/library/hh974476.aspx). 

> [!IMPORTANT]
> Мы настоятельно рекомендуем использовать [Microsoft Graph](https://developer.microsoft.com/graph) вместо API Azure AD Graph tooaccess ресурсов Azure Active Directory. В настоящее время усилия наших разработчиков направлены на Microsoft Graph, и дальнейшие усовершенствования API Azure AD Graph не планируются. Существует очень ограниченное количество сценариев, для которых API Azure AD Graph по-прежнему может быть целесообразным; Дополнительные сведения см. в разделе hello [Microsoft Graph или hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) блога в hello центра разработки для Office.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>Как tooconstruct URL-адреса API Graph
В Graph API, tooaccess каталога данных и объектов (другими словами, ресурсы или объекты), для которых нужно tooperform операции CRUD можно использовать URL-адреса по hello протокола Open Data (OData). Hello URL-адреса, используемые в Graph API состоят из четырех основных частей: службы корневой, идентификатор клиента, пути к ресурсу и параметры строки запроса: `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`. Рассмотрим hello примера hello URL-адреса: `https://graph.windows.net/contoso.com/groups?api-version=1.6`.

* **Корень службы**: В Azure AD Graph API корень службы hello — всегда https://graph.windows.net.
* **Идентификатор клиента**: в этом разделе может быть имя проверенного (зарегистрированного) домена в предыдущих примере hello contoso.com. Он также может быть клиента объект ID "или" hello «myorganization» или «me» псевдоним. Дополнительные сведения см. в разделе [адресация сущностей и операций в Graph API hello](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **Путь к ресурсу**: в этом разделе URL-адрес идентифицирует ресурс hello toobe взаимодействовал (пользователей, групп, конкретного пользователя или определенной группы, и т. д.) В приведенном выше примере hello это tooaddress hello верхнего уровня «groups» данного набора ресурсов. Можно также обращаться к конкретной сущности, например users/{objectId} или users/userPrincipalName.
* **Параметры запроса**: знак вопроса (?) отделяет раздел пути ресурса hello от раздела параметров запроса hello. параметр запроса «api-version» Hello необходим для всех запросов в Graph API hello. Hello Graph API также поддерживает следующие параметры запроса OData hello: **$filter**, **$orderby**, **$expand**, **$top**и **$format**. следующие параметры запроса Hello в настоящее время не поддерживаются: **$count**, **$inlinecount**, и **$skip**. Дополнительные сведения см. в статье [Поддерживаемые запросы, фильтры и операции разбиения на страницы в Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options).

## <a name="graph-api-versions"></a>Версии API Graph
Версия hello для запроса Graph API указывается в параметре запроса «api-version» hello. Для версии 1.5 и более поздних используется числовое значение версии: api-version=1.6. Для более ранних версий используйте строку даты, который соответствует toohello формат гггг-мм-дд; Например, api-version = 2013-11-08. Для компонентов предварительной версии используйте строку hello «бета»; Например, api-version = beta. Дополнительные сведения о различиях между версиями API Graph см. в статье об [управлении версиями API Graph Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

## <a name="graph-api-metadata"></a>Метаданные API Graph
hello tooreturn файла метаданных Graph API добавьте сегмент «$metadata» hello после hello идентификатора клиента в hello URL-адрес. Например, hello следующий URL-адрес Возвращает метаданные для демонстрационной компании: `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`. Можно ввести этот URL-адрес в адресную строку hello toosee hello web обозревателя метаданных. Hello возвращаемый документ языка CSDL метаданных описывает hello сущностей и сложные типы, свойства и функции hello и действия, представляемые версии API Graph вы запросили hello. Пропуск параметра api-version hello Возвращает метаданные для hello самой последней версии.

## <a name="common-queries"></a>Стандартные запросы
[Azure AD стандартные запросы API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) представлены стандартные запросы, которые могут использоваться с hello Azure AD Graph, включая запросы, которые могут быть используется tooaccess ресурсы верхнего уровня в каталоге и запросы tooperform операции в каталоге.

Например, `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` возвращает сведения об организации для каталога contoso.com.

Или `https://graph.windows.net/contoso.com/users?api-version=1.6` перечисляет все объекты пользователя в каталоге contoso.com hello.

## <a name="using-hello-graph-explorer"></a>С помощью Graph Explorer hello
Hello Graph Explorer можно использовать для данных каталога Azure AD Graph API tooquery hello hello в процессе разработки приложения.

Hello ниже приведен hello выходных данных будет выведен toonavigate toohello Graph Explorer, вход и введите `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` Здравствуйте, toodisplay все hello пользователей в каталоге выполнившего вход пользователя:

![Обозреватель API Graph Azure AD](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**Hello загрузки Graph Explorer**: tooload hello инструмент, перейдите в слишком[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/). Нажмите кнопку **входа** и войдите в ваш toorun учетные данные учетной записи Azure AD hello Graph Explorer к вашему клиенту. При запуске Graph Explorer в отношении своего собственного клиента пользователь или администратор должен tooconsent при входе в систему. Если у вас есть подписка Office 365, у вас также есть клиент Azure AD. Hello учетные данные, используемые toosign в tooOffice 365, на самом деле, учетные записи Azure AD и использовать эти учетные данные с помощью Graph Explorer.

**Выполнить запрос**: toorun запроса, введите запрос в текстовое поле hello запроса и нажмите кнопку **получить** или нажмите кнопку hello **введите** ключа. Hello результаты отображаются в поле ответа hello. Например `https://graph.windows.net/myorganization/groups?api-version=1.6` список всех объектов группы в каталоге hello выполнившего вход пользователя.

Примечание hello следующие возможности и ограничения hello Graph Explorer:

* Возможность автозаполнения в наборах ресурсов. toosee эта функциональность, если щелкнуть hello запроса (где отображается URL-адрес компании hello) в текстовом поле. Можно выбрать из раскрывающегося списка hello набор ресурсов.
* Поддерживает Здравствуйте, «me» и «myorganization» псевдонимы адресации. Например, можно использовать `https://graph.windows.net/me?api-version=1.6` tooreturn hello объекта, соответствующего пользователя, выполнившего вход hello или `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn всех пользователей в текущем каталоге hello.
* Раздел заголовков ответа. В этом разделе можно использовать toohelp Устранение неполадок, возникающих при выполнении запросов.
* Средство просмотра JSON для hello ответа с возможностью развертывания и свертывания.
* Отображение эскизов фотографий не поддерживается.

## <a name="using-fiddler-toowrite-toohello-directory"></a>С помощью Fiddler toowrite toohello directory
В целях hello этого краткого руководства можно использовать toopractice веб-отладчик Fiddler hello выполнение операций с каталогом Azure AD и «запись». Дополнительные сведения и tooinstall Fiddler см. в разделе [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler).

В следующем примере hello используйте веб-отладчик Fiddler toocreate новую группу безопасности «MyTestGroup» в каталоге Azure AD.

**Получить маркер доступа**: tooaccess Azure AD Graph, клиенты находятся необходимые toosuccessfully сначала проверить подлинность tooAzure AD. Дополнительные сведения см. в статье [Сценарии аутентификации в Azure Active Directory](active-directory-authentication-scenarios.md).

**Составление и выполнение запроса**: полный hello, следующие шаги:

1. Откройте веб-отладчик Fiddler и переключение toohello **Composer** вкладки.
2. Поскольку требуется, чтобы toocreate новую группу безопасности, выберите **Post** как hello метод HTTP hello в раскрывающемся меню. Дополнительные сведения об операциях и разрешениях в объекте группы в разделе [группы](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) внутри hello [Azure AD Graph REST API ссылка](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
3. В hello поле рядом слишком**Post**, введите в следующих hello как hello URL-адрес запроса: `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`.
   
   > [!NOTE]
   > Необходимо заменить mytenantdomain hello доменное имя каталога Azure AD.
   > 
   > 
4. В поле hello непосредственно под методом Post в раскрывающемся списке введите ниже hello:
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > Замена вашей &lt;маркер доступа&gt; hello маркера доступа для каталога Azure AD.
   > 
   > 
5. В hello **текст запроса** введите hello следующее:
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    Дополнительные сведения о создании групп см. в разделе [Создание группы](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup).

Дополнительные сведения о сущностям Azure AD и типов, предоставляемых Graph и сведения об операциях hello, которые могут быть выполнены на них с помощью Graph см. в разделе [Azure AD Graph REST API ссылка](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о hello [API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* Дополнительная информация: [Azure AD Graph API Permission Scopes](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

