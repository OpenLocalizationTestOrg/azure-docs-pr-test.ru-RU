---
title: "aaaConfigure Secure LDAP (LDAPS) в доменные службы Azure AD | Документы Microsoft"
description: "Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD

## <a name="before-you-begin"></a>Перед началом работы
Убедитесь в завершении [задача 2 - сертификат tooa экспорта hello безопасный LDAP. PFX-файла](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Выберите toouse hello preview взаимодействие с портала Azure или hello Azure классического портала toocomplete этой задачи.
> [!div class="op_single_selector"]
> * **Портал Azure (Предварительная версия)**: [Включить защищенный LDAP, с помощью портала Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Классический портал Azure**: [Включить защищенный LDAP, с помощью классического портала Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>Задача 3 — включить защищенного протокола LDAP для hello управляемого домена с помощью hello портал Azure (Предварительная версия)
tooenable безопасной LDAP, выполните следующие действия по настройке hello.

1. Перейдите toohello  **[портал Azure](https://portal.azure.com)**.

2. Поиск «доменных служб» hello **Найдите ресурсы** поле поиска. Выберите **доменные службы Azure AD** из результатов поиска hello. Hello **доменные службы Azure AD** колонке перечислены управляемого домена.

    ![Поиск подготавливаемого управляемого домена](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Щелкните имя hello toosee hello управляемого домена (например, «contoso100.com») Дополнительные сведения о домене hello.

    ![Доменные службы — состояние подготовки](./media/getting-started/domain-services-provisioning-state.png)

3. Нажмите кнопку **Secure LDAP** на панели навигации hello.

    ![Доменные службы — колонка "Защищенный протокол LDAP"](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. Безопасный доступ tooyour управляемого домена LDAP отключена по умолчанию. Переключить **Secure LDAP** слишком**включить**.

    ![Включение защищенного протокола LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. По умолчанию безопасного tooyour доступа LDAP управляемого домена через Интернет отключен hello. Переключить **Здравствуйте, разрешить защищенный доступ LDAP через Интернет** слишком**включить**при необходимости. 

6. Нажмите значок следующих hello папку **. PFX-файл с сертификатом безопасности LDAP**. Укажите путь toohello hello PFX-файл с сертификатом hello для безопасного доступа toohello управляемого домена LDAP.

7. Укажите hello **toodecrypt пароль. PFX-файла**. Укажите hello же пароль, используемый при экспорте сертификата toohello hello PFX-файл.

8. Закончив, нажмите кнопку hello **Сохранить** кнопки.

9. Вы увидите уведомление о том, что защищенного LDAP настроена для hello управляемый домен. До завершения этой операции не удается изменить другие параметры для домена hello.

    ![Настройка защищенного протокола LDAP для hello управляемого домена](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Занимает около 10 минут too15 tooenable защищенный LDAP для управляемого домена. Если hello при условии, что безопасный LDAP сертификат не соответствует hello необходимые условия, защищенного LDAP не включен для каталога, и вы увидите сбоя. Например указано неверное имя домена hello, hello сертификата уже истек, или срок действия скоро истекает. В этом случае повторите попытку, указав действительный сертификат.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Задача 4 — Настройка управляемого домена DNS tooaccess hello из hello Интернета
> [!NOTE]
> **Необязательные задачи** — Если вы не планируете tooaccess hello управляемого домена с помощью LDAPS более Здравствуйте Интернета, пропустить эту задачу конфигурации.
>
>

Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

После включения защищенный доступ LDAP через Интернет Здравствуйте, управляемого домена, необходимо tooupdate DNS, чтобы клиентские компьютеры могли найти этот управляемый домен. В конце hello задача 3, внешний IP-адрес отображается на hello **свойства** колонки в **ВНЕШНИЕ IP адрес для доступа через LDAPS**.

Настройте внешнего поставщика DNS, чтобы DNS-имени hello объекта hello управляемого домена (например, «ldaps.contoso100.com») toothis точек внешний IP-адрес. В нашем примере мы должны hello toocreate следующие записи DNS.

    ldaps.contoso100.com  -> 52.165.38.113

Вот и все - теперь теперь вы готовы tooconnect toohello управляемых Здравствуйте, домена, с помощью защищенного LDAP через Интернет.

> [!WARNING]
> Помните, что клиентские компьютеры должны доверять hello издателя может tooconnect сертификата LDAPS toobe hello успешно toohello управляемого домена при использовании LDAPS. Если вы используете публично доверенным центром сертификации, необязательно toodo ничего, так как эти издатели сертификатов доверять клиентские компьютеры. Если вы используете самозаверяющий сертификат, установите hello открытую часть hello самозаверяющий сертификат в хранилище доверенных сертификатов hello на клиентском компьютере hello.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Задача 5 - LDAPS блокировки доступа к tooyour управляемого домена через hello Интернета
> [!NOTE]
> **Необязательные задачи** — Если вы не включили LDAPS управляемого домена toohello доступа более Здравствуйте Интернета, пропустить эту задачу конфигурации.
>
>

Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Предоставления управляемого домена для доступа LDAPS через hello Интернет представляет угрозу безопасности. Hello управляемого домена доступен из hello Интернета с hello порт, используемый для защищенного LDAP (то есть, порт 636). Таким образом вы можете toorestrict доступа toohello управляемого домена toospecific известные IP-адресов. В целях повышения безопасности создайте группу безопасности сети (NSG) и связать его с hello подсети, где вы включили доменные службы Azure AD.

Hello следующей таблице показан пример NSG можно настроить toolock вниз защищенный доступ LDAP через hello Интернета. Hello NSG содержит набор правил, которые разрешают доступ входящего трафика LDAPS через TCP-порт 636 только из указанного набора IP-адресов. Hello «DenyAll» правило по умолчанию применяется tooall других входящий трафик от hello Интернета. Hello доступа LDAPS tooallow правила NSG через hello Интернет с указанных IP-адресов имеет более высокий приоритет, чем правила DenyAll NSG hello.

![Здравствуйте, образец NSG toosecure LDAPS доступ через Интернет](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Дополнительные сведения см. в статье** - [Фильтрация сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>Связанная информация
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
* [Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Администрирование групповой политики в управляемом домене доменных служб Azure AD)
* [Группы безопасности сети](../virtual-network/virtual-networks-nsg.md)
* [Создание группы безопасности сети](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
