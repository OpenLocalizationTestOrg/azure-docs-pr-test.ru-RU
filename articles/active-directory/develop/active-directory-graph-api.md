---
title: "aaaAzure Active Directory Graph API | Документы Microsoft"
description: "Общие сведения и примеры использования руководства для hello Graph API, который обеспечивает программный доступ к tooAzure AD через конечные точки REST API."
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>API Graph Azure Active Directory
> [!IMPORTANT]
> Мы настоятельно рекомендуем использовать [Microsoft Graph](https://graph.microsoft.io/) вместо API Azure AD Graph tooaccess ресурсов Azure Active Directory. В настоящее время усилия наших разработчиков направлены на Microsoft Graph, и дальнейшие усовершенствования API Azure AD Graph не планируются. Существует очень ограниченное количество сценариев, для которых API Azure AD Graph по-прежнему может быть целесообразным; Дополнительные сведения см. в разделе hello [Microsoft Graph или hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) блога в hello центра разработки для Office.
> 
> 

Hello Azure Active Directory Graph API обеспечивает программный доступ tooAzure AD через конечные точки REST API. Приложения могут использовать Graph API tooperform hello создания, чтения, обновления и удаления (CRUD) с данными и объектами каталогов. Например hello Graph API поддерживает hello следующих общих действий для объекта-пользователя:

* Создание нового пользователя в каталоге.
* Получение подробных свойств пользователя, например его группы.
* Обновление свойств пользователя, например его расположения и номера телефона, или изменение его пароля.
* Проверка членства в группах для доступа на основе ролей.
* Отключение или полное удаление учетной записи пользователя.

В дополнение toouser объектов можно выполнять подобных операций на другие объекты, такие как группы и приложения. hello toocall API Graph в каталоге приложения hello, должны быть зарегистрированы в Azure AD и быть настроен каталог toohello tooallow доступа. Обычно это делается с помощью потока согласия пользователя или администратора.

с помощью toobegin hello Azure AD Graph API, разделе hello [Graph API краткого руководства](active-directory-graph-api-quickstart.md), или представление hello [интерактивный справочника по Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="features"></a>Функции
Hello Graph API предоставляет hello следующие атрибуты:

* **Конечные точки API REST**: hello Graph API — эта служба состоит из конечных точек, доступных с помощью стандартных HTTP-запросов. Hello Graph API поддерживает типы контента XML или нотации объектов Javascript (JSON) для запросов и ответов. Дополнительные сведения см. в [справочнике по Azure AD Graph REST API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **Проверка подлинности с помощью Azure AD**: каждый toohello запрос Graph API должен пройти проверку подлинности путем добавления JSON Web Token (JWT) в заголовок авторизации hello hello запроса. Этот маркер можно получить путем создания конечной точки маркера запроса tooAzure AD и предоставления действительных учетных данных. Можно использовать поток клиентских учетных данных OAuth 2.0 hello или разрешений кода авторизации hello, tooacquire потока типа маркера toocall hello графа. Дополнительные сведения см. в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Авторизация на основе ролей (RBAC)**: группы безопасности, используемые tooperform RBAC в Graph API hello. Например, если вы хотите toodetermine ли у пользователя есть доступ tooa определенного ресурса, hello приложение может вызвать hello [проверка членства в группе (транзитивно)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) операцию, которая возвращает значение true или false.
* **Разностный запрос**: Если требуется toocheck изменений в каталоге между двумя периодами без toomake частые запросы toohello Graph API, можно сделать разностного запроса. Этот тип запроса возвращает только hello изменения между hello предыдущего разностного запроса и hello текущего запроса. Дополнительные сведения см. в статье [Разностный запрос | Общие понятия API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Расширения каталогов**: Если вы разрабатываете приложение, требующее tooread или запись уникальные свойства для объектов каталога, можно зарегистрировать и использовать значения расширений с помощью Graph API hello. Например если приложению требуется идентификатор Скайп свойство для каждого пользователя, можно зарегистрировать hello новое свойство в каталоге hello, и она будет доступна для каждого объекта пользователя. Дополнительные сведения см. в статье [Расширения схемы каталогов | Общие понятия API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **Защищен области разрешений**: AAD Graph API предоставляет области разрешений, которые позволяют защитить согласие доступа tooAAD данные и поддерживает широкий набор типов клиентских приложений, включая:
  
  * имеющих пользовательский интерфейс, который получают делегированный доступ к toodata через авторизации из hello пользователя, выполнившего вход (делегированы)
  * приложения, использующие контроль доступа основе ролей, например клиенты службы или управляющей программы (роли приложений).
    
    Оба делегируются и области разрешений роли приложения представляют прав доступа, предоставляемые Graph API hello и могут запрашиваться клиентскими приложениями через разрешения для регистрации приложения [возможности hello портал Azure](https://portal.azure.com). Клиенты могут проверить hello области разрешений предоставлен toothem путем проверки утверждений hello области («scp»), полученных в маркере доступа hello для делегирования разрешений и утверждения hello роли («») для разрешения роли приложения. Подробнее об этом: [Azure AD Graph API Permission Scopes](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).

## <a name="scenarios"></a>Сценарии
Hello Graph API поддерживает многие сценарии приложений. следующие сценарии Hello приведены наиболее распространенные hello.

* **Бизнес-приложение (однотенантное)**. В этом сценарии разработчик работает на предприятие, у которого есть подписка Office 365. Hello разработчиком веб-приложения, взаимодействующего с tooperform задачи Azure AD, например назначении пользователю лицензии tooa. Эта задача требует toohello доступа к API Graph, поэтому hello разработчик регистрирует приложение для одного клиента hello в Azure AD и настраивает разрешения чтения и записи для hello Graph API. Затем hello приложения является настроенным toouse свои собственные учетные данные, или те tooacquire вошедшего в систему пользователя hello маркера toocall hello Graph API.
* **Программное обеспечение как приложение-служба (мультитенантное)**. В этом сценарии независимый поставщик программного обеспечения разрабатывает и размещенное мультитенантное веб-приложение, которое предоставляет пользователю функции управления для других организаций, использующих Azure AD. Эти функции требуют доступа к объектам toodirectory, и таким образом приложение hello должен hello toocall Graph API. developer Привет зарегистрирует приложение hello в Azure AD, настраивает его чтения toorequire и разрешение на запись в Graph API hello и затем включает внешний доступ, чтобы другая организация могла согласиться toouse приложения hello в своем каталоге. Когда toohello приложения для hello первый раз проверки подлинности пользователя в другой организации, они отображается диалоговое окно согласия с разрешениями hello, которые запрашивает приложение hello.  Предоставление, что в случае согласия приложения hello предоставляются запрашиваемые разрешения toohello Graph API в каталоге пользователя hello. Дополнительные сведения об инфраструктуре согласия hello см. в разделе [Обзор инфраструктуры согласия hello](active-directory-integrating-applications.md).

## <a name="see-also"></a>См. также
[Краткое руководство по API Graph Azure AD](active-directory-graph-api-quickstart.md)

[Документация REST для Graph AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Руководство разработчика по Azure Active Directory](active-directory-developers-guide.md)

