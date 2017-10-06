---
title: "aaaConfigure Secure LDAP (LDAPS) в доменные службы Azure AD | Документы Microsoft"
description: "Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
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


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Задача 3 — включить защищенного протокола LDAP для hello управляемого домена с помощью классического портала Azure hello
tooenable безопасной LDAP, выполните следующие действия по настройке hello.

1. Перейдите toohello  **[классический портал Azure](https://manage.windowsazure.com)**.
2. Выберите hello **Active Directory** узел в левой области hello.
3. Выберите каталог hello Azure AD (также назывались tooas «клиент»), для которого включена доменные службы Azure AD.

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Нажмите кнопку hello **Настройка** вкладки.

    ![Вкладка "Настройка" каталога](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Прокрутите раздел toohello **доменных служб**. Вы увидите параметр под названием **Secure LDAP (LDAPS)** как показано на следующий снимок экрана приветствия:

    ![Раздел настройки доменных служб](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Нажмите кнопку hello **настроить сертификат...**  toobring кнопки вверх hello **Настройка сертификата для безопасного LDAP** диалогового окна.

    ![Настройка сертификата для защищенного LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Нажмите значок следующих hello папку **PFX-ФАЙЛ с СЕРТИФИКАТОМ** toospecify hello PFX файл, содержащий сертификат hello нужно toouse для безопасного toohello доступа LDAP управляемого домена. Также можно ввести пароль hello, указанные при экспорте сертификата toohello hello PFX-файл. Нажмите кнопку сделать кнопку на нижней hello hello.

    ![Указание PFX-файла и пароля защищенного LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Hello **доменных служб** раздел hello **Настройка** вкладка должен получить серым и находится в hello **ожидающие...**  за несколько минут. В течение этого периода hello LDAPS сертификат проверяется для повышения точности и защищенного LDAP настроен для управляемого домена.

    ![Защищенный LDAP — состояние ожидания](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Занимает около 10 минут too15 tooenable защищенный LDAP для управляемого домена. Если hello при условии, что безопасный LDAP сертификат не соответствует hello необходимые условия, защищенного LDAP не включен для каталога, и вы увидите сбоя. Например указано неверное имя домена hello, hello сертификата уже истек, или срок действия скоро истекает.
   >
   >

9. Если защищенного LDAP успешно включена для управляемого домена, hello **ожидающие...**  сообщение должно исчезнуть. Вы увидите hello отпечаток сертификата hello отображается.

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Задача 4 — Включить защищенный доступ LDAP через hello Интернета
**Необязательные задачи** — Если вы не планируете tooaccess hello управляемого домена с помощью LDAPS более Здравствуйте Интернета, пропустить эту задачу конфигурации.

Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. Вы увидите вариант слишком**hello ВКЛЮЧИТЬ SECURE LDAP доступ через Интернет** в hello **доменных служб** раздел hello **Настройка** страницы. Этот параметр имеет значение слишком**нет** по умолчанию, так как управляемые toohello доступа к Интернету домена через безопасный LDAP по умолчанию отключена.

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. Переключить **hello ВКЛЮЧИТЬ SECURE LDAP доступ через Интернет** слишком**Да**. Нажмите кнопку hello **Сохранить** кнопку на нижней панели hello.
    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Hello **доменных служб** раздел hello **Настройка** вкладка должен получить серым и находится в hello **ожидающие...**  за несколько минут. Через некоторое время включены internet access tooyour управляемого домена через безопасный LDAP.

    ![Защищенный LDAP — состояние ожидания](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Занимает около 10 минут tooenable доступ к Интернету через безопасный LDAP для управляемого домена.
   >
   >
4. При безопасной tooyour доступа LDAP управляемого домена через Интернет успешно включен hello, hello **ожидающие...**  сообщение должно исчезнуть. Вы увидите hello внешний IP-адрес, адрес можно использовать tooaccess каталога через LDAPS в поле hello **ВНЕШНИЕ IP адрес для доступа через LDAPS**.

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Задача 5 — Настройка управляемого домена DNS tooaccess hello из hello Интернета
**Необязательные задачи** — Если вы не планируете tooaccess hello управляемого домена с помощью LDAPS более Здравствуйте Интернета, пропустить эту задачу конфигурации.

Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 4](#task-4---enable-secure-ldap-access-over-the-internet).

После включения защищенный доступ LDAP через Интернет Здравствуйте, управляемого домена, необходимо tooupdate DNS, чтобы клиентские компьютеры могли найти этот управляемый домен. В конце задача 4 hello, внешний IP-адрес отображается на hello **Настройка** вкладке **ВНЕШНИЕ IP адрес для доступа через LDAPS**.

Настройте внешнего поставщика DNS, чтобы DNS-имени hello объекта hello управляемого домена (например, «ldaps.contoso100.com») toothis точек внешний IP-адрес. В нашем примере мы должны hello toocreate следующие записи DNS.

    ldaps.contoso100.com  -> 52.165.38.113

Вот и все - теперь теперь вы готовы tooconnect toohello управляемых Здравствуйте, домена, с помощью защищенного LDAP через Интернет.

> [!WARNING]
> Помните, что клиентские компьютеры должны доверять hello издателя может tooconnect сертификата LDAPS toobe hello успешно toohello управляемого домена при использовании LDAPS. Если вы используете центр сертификации предприятия или публично доверенным центром сертификации, необязательно toodo ничего, так как эти издатели сертификатов доверять клиентские компьютеры. Если вы используете самозаверяющий сертификат, необходимо tooinstall hello открытую часть hello самозаверяющий сертификат в хранилище доверенных сертификатов hello на клиентском компьютере hello.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>LDAPS блокировки доступа к управляемому домену tooyour через hello Интернета
> [!NOTE]
> **Необязательные задачи** — Если вы не включили LDAPS управляемого домена toohello доступа более Здравствуйте Интернета, пропустить эту задачу конфигурации.
>
>

Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 4](#task-4---enable-secure-ldap-access-over-the-internet).

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
