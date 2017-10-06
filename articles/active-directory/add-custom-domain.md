---
title: "aaaAdd tooAzure пользовательского домена AD | Документы Microsoft"
description: "Объясняет, как tooadd пользовательского домена в Azure Active Directory."
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>Краткое руководство: Добавление tooAzure имя пользовательского домена Active Directory

Каждый каталог Azure AD поставляется с исходное имя домена в форме hello *domainname*. onmicrosoft.com. hello исходное имя домена не может изменить или удалить, но можно добавить к корпоративному домену имя tooAzure AD также. Например организации, вероятно, возникла других доменных имен, используемых toodo бизнеса и пользователи, выполнившие вход в с помощью корпоративной доменного имени. Добавление пользовательского домена имена tooAzure AD позволяет tooassign имена пользователей в каталоге hello знакомый tooyour пользователей, таких как "alice@contoso.com." вместо "alice@*<domain name>*.onmicrosoft.com". Hello процедура проста:

1. Добавьте каталог tooyour имени пользовательского домена hello
2. Добавьте записи DNS для имени домена hello в hello регистратора доменных имен
3. Проверьте имя пользовательского домена hello в Azure AD

## <a name="add-your-custom-domain"></a>Добавление личного домена
1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **Azure Active Directory** в hello текстовое поле, а затем выберите **ввод**.
   
   ![Открытие страницы "Управление пользователями"](./media/active-directory-domains-add-azure-portal/user-management.png)
3. На hello ***имя каталога*** колонке выберите **доменных имен**.
4. На hello  ***имя каталога* -имена домена** колонки, выберите hello **добавить** команды.
   
   ![При выборе команды Добавить hello](./media/active-directory-domains-add-azure-portal/add-command.png)
5. На hello **доменное имя** колонки, введите имя личного домена hello в поле hello, например, «contoso.com», а затем выберите **добавить домен**. Быть убедиться, что tooinclude hello .com, .net или другого расширения верхнего уровня.
6. На hello ***доменное имя*** колонка (с имя пользовательского домена hello заголовок), получить hello DNS запись сведения toouse tooverify, которыми владеет организация hello пользовательское имя домена.
   
   ![Получение сведений о записи DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Если планируется toofederate в локальной среде Windows Server AD с Azure AD, то вы должны tooselect hello **я планирую tooconfigure этот домен для единого входа с моим локальным Active Directory** флажок при запуске средства hello Azure AD Connect toosynchronize каталогов. Необходимо также tooregister hello таким же именем домена, выберите для создания федерации с локальным каталогом в hello **домен Azure AD** шаг мастера hello. Можно увидеть, какие этот шаг мастера hello выглядит как [в этих инструкциях](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Если у вас средства hello Azure AD Connect, вы можете [загрузить ее здесь](http://go.microsoft.com/fwlink/?LinkId=615771).

Добавили hello доменное имя, Azure AD необходимо убедиться, что имя домена hello принадлежат вашей организации. Перед Azure AD можно выполнить эту проверку, необходимо добавить DNS-запись в файл зоны DNS hello hello доменного имени. Эта задача выполняется на веб-сайте hello для регистратора доменных имен для имени домена hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Добавьте запись DNS hello в hello регистратора доменных имен для домена hello
Следующий шаг toouse Hello имя вашего домена с Azure AD — tooupdate hello файла зоны DNS для домена hello. Azure AD затем можно проверить, что hello пользовательское имя домена принадлежат вашей организации.

1. Войдите в toohello регистратора доменных имен для домена hello. Если у вас нет доступа tooupdate hello запись DNS, попросите hello лица или рабочей группы, которым этот доступ toocomplete шаг 2 и toolet известно при ее завершении.
2. Обновление hello файла зоны DNS для домена hello, добавив запись DNS hello tooyou, предоставляемые Azure AD. Эту запись DNS позволяет tooverify Azure AD вашей владельца домена hello. Hello запись DNS не изменяет поведение, например маршрутизации почты или веб-размещения.

Для получения справки по этой Добавление записи DNS hello чтения [инструкции по добавлению DNS-записи на популярных регистраторов DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Проверьте имя домена hello в Azure AD
После добавления записей DNS hello предпринимается готов tooverify hello доменное имя в Azure AD.

Имя домена могут быть проверены только после распространения hello DNS-записей. Как правило, это занимает всего несколько секунд, но иногда — один или несколько часов. Если проверка не работает hello первый раз, повторите попытку позже.

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **Обзор**, введите в текстовом поле hello Управление пользователями и выберите **ввод**.
   
   ![Открытие страницы "Управление пользователями"](./media/active-directory-domains-add-azure-portal/user-management.png)
3. На hello **Управление пользователями - имена домена** колонки, выберите hello непроверенные доменное имя, что требуется tooverify.
4. На hello ***доменное имя*** колонке (то есть hello стоечный модуль, открывается, имеющий имя нового домена в заголовок hello), выберите **проверьте** toocomplete hello проверки.

> [!TIP]
> Можно сложить too900 пользовательские доменные имена, но может быть только одно [задать в качестве hello основное имя домена для вашего каталога Azure AD](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) используется по умолчанию при создании новых учетных записей.

Теперь с помощью имени личного домена вы можете создавать учетные записи пользователей на основе облака или обновлять ранее синхронизированные локальные сведения об учетных записях пользователей. Можно также изменить ранее синхронизированные пользователя учетной записи домена суффикс сведения с помощью [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) или hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Устранение неполадок
Если не удается проверить имя личного домена, попробуйте следующие действия по устранению неполадок hello:

1. **Подождите один час**. DNS-записи должен иметь toopropagate Azure AD можно проверить домен hello. Для этого может понадобиться один или несколько часов.
2. **Убедитесь, hello введено запись DNS, а также правильность**. Выполнение этого действия на веб-сайте hello для hello регистратора доменных имен для домена hello. Azure AD не удается проверить имя домена hello, если hello запись DNS не присутствует в hello файла зоны DNS или если она не в точности совпадать с DNS-запись hello, Azure AD создала для вас. Если у вас доступ tooupdate DNS-записи для домена hello в hello регистратора доменных имен, совместно hello DNS-запись hello пользователя или группы в организации, который имеет этот доступ и попросите его tooadd hello DNS-запись.
3. **Удалить имя домена hello из другого каталога в Azure AD**. Доменное имя можно проверить только в одном каталоге. Если доменное имя ранее было проверено в другом каталоге, его нужно удалить из него. Только после этого имя можно будет проверить в новом каталоге. чтение toolearn об удалении доменных имен [управление пользовательские доменные имена](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Добавление имен других личных доменов
Если ваша организация использует более одного имени пользовательского домена, например «contoso.com» и «contosobank.com», можно добавить копию too900 больше, повторив шаги hello в этой статье для каждого.

### <a name="learn-more"></a>Подробнее
[Общие сведения об именах личных доменов Azure AD](active-directory-add-domain-concepts.md)

[Управление именами пользовательских доменов](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Дальнейшие действия
В этом кратком руководстве вы узнали, как tooadd tooAzure пользовательского домена AD. 

Можно использовать следующую ссылку tooadd новый пользовательский домен в Azure AD из портала Azure hello hello.

> [!div class="nextstepaction"]
> [Добавить личный домен](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 