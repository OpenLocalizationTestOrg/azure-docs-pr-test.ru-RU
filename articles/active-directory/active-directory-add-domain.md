---
title: "aaaAdd личного домена имя tooAzure Active Directory | Документы Microsoft"
description: "Как tooadd компании доменных имен tooAzure Active Directory, и как tooverify hello доменное имя."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
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
> 

У вас есть один или несколько доменных имен, ваша организация использует toodo бизнес и вход пользователей в tooyour корпоративной сети с помощью корпоративной доменного имени. Теперь, когда вы используете Azure Active Directory (Azure AD), можно добавить к корпоративному домену имя tooAzure AD также. Это позволяет tooassign имена пользователей в каталоге hello знакомый tooyour пользователей, таких как "alice@contoso.com." Hello процедура проста:

1. Добавьте каталог tooyour имени пользовательского домена hello
2. Добавьте записи DNS для имени домена hello в hello регистратора доменных имен
3. Проверьте имя пользовательского домена hello в Azure AD

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье. Для tooadd имени домена компании в центре администрирования hello Azure AD, в статье [назначение ролей администратора в Azure Active Directory](active-directory-domains-add-azure-portal.md).

Если планируется tooconfigure toobe имя вашего личного домена, при использовании служб федерации Active Directory (AD FS) или другой службы маркеров безопасности (STS) в корпоративной сети, следуйте инструкциям hello [Установка и Настройка домена для федерации с Azure Active Directory](active-directory-add-domain-federated.md). Это полезно, если планируется toosynchronize пользователей из вашего каталога организации tooAzure AD, и [синхронизация хэшей паролей](active-directory-aadconnectsync-implement-password-synchronization.md) не соответствует вашим требованиям.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Добавить каталог tooyour имя пользовательского домена
1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) с учетной записью пользователя, который является глобальным администратором каталога Azure AD.
2. В **Active Directory**откройте каталог и выберите hello **домены** вкладки.
3. Выберите на панели команд hello, **добавить**. Введите имя hello свой домен, например, «contoso.com». Убедитесь, что tooinclude hello .com, .net или другого расширения верхнего уровня и оставьте флажок hello «single sign-on» снят (федерации).
4. Выберите **Добавить**.
5. На hello второй странице мастера добавления домена hello получите hello, Azure AD будет использовать tooverify, что ваша организация владеет hello пользовательское доменное имя DNS-запись.

Добавили hello доменное имя, Azure AD необходимо убедиться, что имя домена hello принадлежат вашей организации. Перед Azure AD можно выполнить эту проверку, необходимо добавить DNS-запись в файл зоны DNS hello hello доменного имени. Эта задача выполняется на веб-сайте hello для регистратора доменных имен для имени домена hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Добавьте запись DNS hello в hello регистратора доменных имен для домена hello
Следующий шаг toouse Hello имя вашего домена с Azure AD — tooupdate hello файла зоны DNS для домена hello. Это позволяет tooverify Azure AD, что hello пользовательское имя домена принадлежат вашей организации.

1. Войдите в toohello регистратора доменных имен для домена hello. Если у вас нет доступа tooupdate hello запись DNS, попросите hello лица или рабочей группы, которым этот доступ toocomplete шаг 2 и toolet известно при ее завершении.
2. Обновление hello файла зоны DNS для домена hello, добавив запись DNS hello tooyou, предоставляемые Azure AD. Эту запись DNS позволяет tooverify Azure AD вашей владельца домена hello. Hello запись DNS не изменяет поведение, например маршрутизации почты или веб-размещения.

Для получения справки по этой Добавление записи DNS hello чтения [инструкции по добавлению DNS-записи на популярных регистраторов DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Проверьте имя домена hello в Azure AD
После добавления записей DNS hello предпринимается готов tooverify hello доменное имя в Azure AD.

При наличии hello **добавить домен** мастера открыт, щелкните **проверьте** на третьей странице мастера hello hello. При выборе **проверьте**, Azure AD будет осуществлять поиск hello DNS-запись в файл зоны hello DNS для домена hello. Azure AD можно проверить имя домена hello только после распространения hello DNS-записей. Как правило, это занимает всего несколько секунд, но иногда — один или несколько часов. Если проверка не работает hello первый раз, повторите попытку позже.

Если hello **добавить домен** мастер не все еще открыто, можно проверить домен hello в hello [классический портал Azure](https://manage.windowsazure.com/):

1. Войдите в каталог Azure AD с правами глобального администратора.
2. Откройте ваш каталог и выберите hello **домены** вкладки.
3. Имя домена выберите hello tooverify и выберите **проверьте** на панели команд hello.
4. Выберите **проверьте** hello диалогового окна поле toocomplete hello верификации.

Теперь можно [назначить имена пользователей, включающие имя вашего личного домена](active-directory-add-domain-add-users.md).

## <a name="troubleshooting"></a>Устранение неполадок
Если не удается проверить имя личного домена, попробуйте следующие hello. Мы начнем с hello самые распространенные и работают вниз toohello наименьшее общее.

1. **Подождите один час**. DNS-записи должен иметь toopropagate Azure AD можно проверить домен hello. Для этого может понадобиться один или несколько часов.
2. **Убедитесь, hello введено запись DNS, а также правильность**. Выполнение этого действия на веб-сайте hello для hello регистратора доменных имен для домена hello. Azure AD не удается проверить имя домена hello, если hello запись DNS не присутствует в hello файла зоны DNS или если она не в точности совпадать с DNS-запись hello, Azure AD создала для вас. Если у вас доступ tooupdate DNS-записи для домена hello в hello регистратора доменных имен, совместно hello DNS-запись hello пользователя или группы в организации, который имеет этот доступ и попросите его tooadd hello DNS-запись.
3. **Удалить имя домена hello из другого каталога в Azure AD**. Доменное имя можно проверить только в одном каталоге. Если доменное имя ранее было проверено в другом каталоге, его нужно удалить из него. Только после этого имя можно будет проверить в новом каталоге. чтение toolearn об удалении доменных имен [управление пользовательские доменные имена](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Добавление имен других личных доменов
Если ваша организация использует несколько имен пользовательских доменов, например «contoso.com» и «contosobank.com», их можно сложить tooa до 900 доменных имен. Используйте hello же шаги в этой статье tooadd каждого имен доменов.

## <a name="next-steps"></a>Дальнейшие действия
* [Сведения о назначении имен пользователей, которые содержат имя пользовательского домена](active-directory-add-domain-add-users.md)
* [Управление именами пользовательских доменов](active-directory-add-manage-domain-names.md)
* [Общие сведения об управлении доменами в Azure AD](active-directory-add-domain-concepts.md)
* [Добавление фирменной символики компании на страницах входа и панели доступа](active-directory-add-company-branding.md)
* [Использовать PowerShell toomanage доменных имен в Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

