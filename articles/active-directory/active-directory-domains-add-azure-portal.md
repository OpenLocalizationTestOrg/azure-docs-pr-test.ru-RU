---
title: "aaaAdd личного домена имя tooAzure Active Directory | Документы Microsoft"
description: "Как tooadd компании доменных имен tooAzure Active Directory, и как tooverify hello доменное имя."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 88d5f443cd10b098a9a9ffb3137f5e1ca33b6aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>Добавить tooAzure имя пользовательского домена Active Directory
> [!div class="op_single_selector"]
> * [Портал Azure](active-directory-domains-add-azure-portal.md)
> * [классическом портале Azure](active-directory-add-domain.md)
> 

С помощью Azure Active Directory (Azure AD), можно добавить к корпоративному домену имя tooAzure AD также. Может потребоваться доменных имен, организация использует toodo бизнеса и пользователи, выполнившие вход в с помощью корпоративной доменного имени. Добавление tooAzure имя домена hello AD позволяет tooassign имена пользователей в каталоге hello знакомый tooyour пользователей, таких как "alice@contoso.com." Hello процедура проста:

1. Добавьте каталог tooyour имени пользовательского домена hello
2. Добавьте записи DNS для имени домена hello в hello регистратора доменных имен
3. Проверьте имя пользовательского домена hello в Azure AD

## <a name="how-do-i-add-a-domain-name"></a>Как можно добавить доменное имя?
1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **Azure Active Directory** в hello текстовое поле, а затем выберите **ввод**.
   
   ![Открытие страницы "Управление пользователями"](./media/active-directory-domains-add-azure-portal/user-management.png)
3. На hello ***имя каталога*** колонке выберите **доменных имен**.
4. На hello  ***имя каталога* -имена домена** колонки, выберите hello **добавить** команды.
   
   ![При выборе команды Добавить hello](./media/active-directory-domains-add-azure-portal/add-command.png)
5. На hello **доменное имя** колонки, введите имя личного домена hello в поле hello, например, «contoso.com», а затем выберите **добавить домен**. Быть убедиться, что tooinclude hello .com, .net или другого расширения верхнего уровня.
6. На hello ***domainname*** колонке (то есть hello стоечный модуль, открывается, имеющий имя нового домена в заголовок hello), получить сведения для записи DNS hello, Azure AD будет использовать tooverify, что ваша организация владеет hello пользовательское имя домена.
   
   ![Получение сведений о записи DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Добавили hello доменное имя, Azure AD необходимо убедиться, что имя домена hello принадлежат вашей организации. Перед Azure AD можно выполнить эту проверку, необходимо добавить DNS-запись в файл зоны DNS hello hello доменного имени. Эта задача выполняется на веб-сайте hello для регистратора доменных имен для имени домена hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Добавьте запись DNS hello в hello регистратора доменных имен для домена hello
Следующий шаг toouse Hello имя вашего домена с Azure AD — tooupdate hello файла зоны DNS для домена hello. Это позволяет tooverify Azure AD, что hello пользовательское имя домена принадлежат вашей организации.

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
4. На hello ***domainname*** колонке (то есть hello стоечный модуль, открывается, имеющий имя нового домена в заголовок hello), выберите **проверьте** toocomplete hello проверки.

Теперь можно [назначить имена пользователей, включающие имя вашего личного домена](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Устранение неполадок
Если не удается проверить имя личного домена, попробуйте следующие hello. Мы начнем с hello самые распространенные и работают вниз toohello наименьшее общее.

1. **Подождите один час**. DNS-записи должен иметь toopropagate Azure AD можно проверить домен hello. Для этого может понадобиться один или несколько часов.
2. **Убедитесь, hello введено запись DNS, а также правильность**. Выполнение этого действия на веб-сайте hello для hello регистратора доменных имен для домена hello. Azure AD не удается проверить имя домена hello, если hello запись DNS не присутствует в hello файла зоны DNS или если она не в точности совпадать с DNS-запись hello, Azure AD создала для вас. Если у вас доступ tooupdate DNS-записи для домена hello в hello регистратора доменных имен, совместно hello DNS-запись hello пользователя или группы в организации, который имеет этот доступ и попросите его tooadd hello DNS-запись.
3. **Удалить имя домена hello из другого каталога в Azure AD**. Доменное имя можно проверить только в одном каталоге. Если доменное имя ранее было проверено в другом каталоге, его нужно удалить из него. Только после этого имя можно будет проверить в новом каталоге. чтение toolearn об удалении доменных имен [управление пользовательские доменные имена](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Добавление имен других личных доменов
Если ваша организация использует несколько имен пользовательских доменов, например «contoso.com» и «contosobank.com», их можно сложить tooa до 900 доменных имен. Используйте hello же шаги в этой статье tooadd каждого имен доменов.

## <a name="next-steps"></a>Дальнейшие действия
[Управление именами пользовательских доменов](active-directory-domains-manage-azure-portal.md)

