---
title: "aaaAdd настраиваемое имя домена и настройка федеративного входа в tooAzure Active Directory | Документы Microsoft"
description: "Как tooadd компании доменных имен tooset Active Directory tooAzure копирование федеративных вход между Azure Active Directory и решения федерации в локальной среде"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>Добавить к tooAzure имя пользовательского домена Active Directory
Вы можете настроить имя личного домена, например contoso.com, чтобы пользователи в этом домене могли использовать федеративный единый вход из корпоративной сети. При наличии служб федерации Active Directory (AD FS) или другой федерации серверы в корпоративной сети, можно настроить Azure AD toouse пользовательское имя домена с помощью средства Azure AD Connect hello. Можно использовать среду Azure AD Connect toodeploy новой службы федерации Active Directory и настройки, для федеративного единого входа tooAzure AD.

Если нет и не планируете toodeploy AD FS или на другом сервере федерации, выполните следующие действия: [добавить tooAzure имя пользовательского домена Active Directory](active-directory-add-domain.md).

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Добавить каталог tooyour имя пользовательского домена
1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) с учетной записью пользователя, который является глобальным администратором каталога Azure AD.
2. В **Active Directory**откройте каталог и выберите hello **домены** вкладки.
3. Выберите на панели команд hello, **добавить**, а затем введите имя hello своего пользовательского домена, например, «contoso.com». Быть убедиться, что tooinclude hello .com, .net или другого расширения верхнего уровня.
4. Выберите hello **я планирую tooconfigure этот домен для единого входа с моим локальным Active Directory** флажок.
5. Выберите **Добавить**.

Запустите запись DNS hello tooget средство hello Azure AD Connect, Azure AD будет использовать tooverify hello домена. Вы увидите hello DNS-запись в hello **домен Azure AD** шаг мастера hello. Можно увидеть, какие этот шаг мастера hello выглядит как [в этих инструкциях](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Если у вас средства hello Azure AD Connect, вы можете [загрузить ее здесь](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Добавьте запись DNS hello в hello регистратора доменных имен для домена hello
Следующий шаг toouse Hello имя вашего домена с Azure AD — tooupdate hello файла зоны DNS для домена hello. Это позволяет tooverify Azure AD, что hello пользовательское имя домена принадлежат вашей организации.

1. Войдите в toohello веб-сайт для регистратора доменных имен для имени домена. Если у вас нет доступа к toodo это, попросите hello пользователя или группы в организации, этот шаг toocomplete доступ 2 и toolet известно при ее завершении.
2. Обновление hello файла зоны DNS для домена hello, добавив запись DNS hello tooyou, предоставляемые Azure AD. Эту запись DNS позволяет tooverify Azure AD вашей владельца домена hello. Hello запись DNS не изменяет поведение, например маршрутизации почты или веб-размещения.

Дополнительные сведения об этом шаге см. в [инструкциях по добавлению DNS-записи на сайтах популярных регистраторов DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/).

## <a name="verify-hello-domain-name-with-azure-ad"></a>Проверьте имя домена hello в Azure AD
После добавления записей DNS hello предпринимается готов tooverify hello доменное имя в Azure AD.

tooverify hello домена, выберите **Далее** на hello **домен Azure AD** шаг мастера hello Azure AD Connect. Azure AD будет искать hello DNS-запись в файл зоны hello DNS для домена hello. Azure AD только проверки hello доменного имени, после распространения hello DNS-записей. Как правило, это занимает всего несколько секунд, но иногда — один или несколько часов. Если проверка не работает hello первый раз, повторите попытку позже.

Продолжите hello, оставшиеся шаги мастера Azure AD Connect hello. Эта команда синхронизирует пользователей из вашего tooAzure Windows Server AD AD. Синхронизированные пользователи в домене hello, настроенного для федерации будет может tooget федеративного единого входа возникают из вашей корпоративной сети tooAzure AD.

## <a name="troubleshooting"></a>Устранение неполадок
Если не удается проверить имя личного домена, попробуйте следующие hello. Мы начнем с hello самые распространенные и работают вниз toohello наименьшее общее.

1. **Подождите один час**. DNS-записи должен иметь toopropagate Azure AD можно проверить домен hello. Для этого может понадобиться один или несколько часов.
2. **Убедитесь, hello введено запись DNS, а также правильность**. Выполнение этого действия на веб-сайте hello для hello регистратора доменных имен для домена hello. Azure AD не удается проверить имя домена hello, если hello запись DNS не присутствует в hello файла зоны DNS или если она не в точности совпадать с DNS-запись hello, Azure AD создала для вас. Если у вас доступ tooupdate DNS-записи для домена hello в hello регистратора доменных имен, совместно hello DNS-запись hello пользователя или группы в организации, который имеет этот доступ и попросите его tooadd hello DNS-запись.
3. **Удалить имя домена hello из другого каталога в Azure AD**. Доменное имя можно проверить только в одном каталоге. Если доменное имя ранее было проверено в другом каталоге, его нужно удалить из него. Только после этого имя можно будет проверить в новом каталоге. чтение toolearn об удалении доменных имен [управление пользовательские доменные имена](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Добавление имен других личных доменов
Если ваша организация использует несколько имен пользовательских доменов, например «contoso.com» и «contosobank.com», их можно сложить tooa до 900 доменных имен. Используйте hello же шаги в этой статье tooadd каждого имен доменов.

## <a name="next-steps"></a>Дальнейшие действия
* [Управление личными доменными именами](active-directory-add-manage-domain-names.md)
* [Общие сведения об управлении доменами в Azure AD](active-directory-add-domain-concepts.md)
* [Добавление фирменной символики компании на страницах входа и панели доступа](active-directory-add-company-branding.md)
* [Использовать PowerShell toomanage доменных имен в Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

