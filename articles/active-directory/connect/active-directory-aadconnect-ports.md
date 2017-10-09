---
title: "Порты и протоколы, необходимые для гибридной идентификации в Azure | Документация Майкрософт"
description: "Эта страница является страницей Технический справочник порты, необходимые toobe открыт для Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a>Порты и протоколы, необходимые для гибридной идентификации
Hello следующий документ представляет Технический справочник по hello необходимые порты и протоколы для реализации гибридного решения по идентификации. Используйте следующие иллюстрации hello, toohello соответствующей таблицы.

![Что такое Azure AD Connect?](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a>Таблица 1. Azure AD Connect и локальная служба AD
Эта таблица описывает hello порты и протоколы, которые необходимы для обмена данными между сервером hello Azure AD Connect и локальной AD.

| Протокол | порты; | Описание |
| --- | --- | --- |
| DNS |53 (TCP или UDP) |Уточняющие запросы DNS леса назначения: hello. |
| Kerberos |88 (TCP или UDP) |Лес toohello AD проверки подлинности Kerberos. |
| MS-RPC |135 (TCP или UDP) |Используется во время начальной настройки приветствия мастера Azure AD Connect hello во время привязки toohello AD леса, а также во время синхронизации паролей. |
| LDAP |389 (TCP или UDP) |Используется для импорта данных из AD. Данные шифруются с помощью функции подписи и запечатывания Kerberos. |
| RPC | 445 (TCP/UDP) |Используемый учетной записи компьютера в лесу hello AD toocreate прозрачную единого входа. |
| LDAP или SSL |636 (TCP или UDP) |Используется для импорта данных из AD. Передача данных Hello подписывается и шифруется. Используется только при применении SSL. |
| RPC |49152- 65535 (произвольные верхние порты RPC) (TCP или UDP) |Используется во время начальной настройки Azure AD Connect, во время привязки лесов toohello AD hello, а также во время синхронизации паролей. Дополнительную информацию см. в статьях базы знаний [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017) и [KB224196](https://support.microsoft.com/kb/224196). |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a>Таблица 2. Azure AD Connect и Azure AD
Эта таблица описывает hello порты и протоколы, которые необходимы для обмена данными между сервером Azure AD Connect hello Azure AD.

| Протокол | порты; | Описание |
| --- | --- | --- |
| HTTP |80 (TCP или UDP) |Использовать SSL-сертификатов tooverify toodownload списки отзыва сертификатов (списки отзыва сертификатов). |
| HTTPS |443 (TCP или UDP) |Используется toosynchronize с Azure AD. |

Список URL-адреса и IP-адреса необходимо tooopen через брандмауэр см. [Office 365 URL-адреса и IP-адресов](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a>Таблица 3. Azure AD Connect и серверы федерации AD FS и WAP
Эта таблица описывает hello порты и протоколы, которые необходимы для обмена данными между сервером hello Azure AD Connect и серверами AD FS федерации или WAP AD FS.  

| Протокол | порты; | Описание |
| --- | --- | --- |
| HTTP |80 (TCP или UDP) |Использовать SSL-сертификатов tooverify toodownload списки отзыва сертификатов (списки отзыва сертификатов). |
| HTTPS |443 (TCP или UDP) |Используется toosynchronize с Azure AD. |
| WinRM |5985 |Прослушиватель WinRM |

## <a name="table-4---wap-and-federation-servers"></a>Таблица 4. Серверы WAP и серверы федерации
Эта таблица описывает hello порты и протоколы, которые необходимы для обмена данными между серверами федерации hello и WAP-серверах.

| Протокол | порты; | Описание |
| --- | --- | --- |
| HTTPS |443 (TCP или UDP) |Используется для проверки подлинности. |

## <a name="table-5---wap-and-users"></a>Таблица 5. WAP и пользователи
Эта таблица описывает hello порты и протоколы, которые требуются для взаимодействия между пользователями и hello WAP-серверах.

| Протокол | порты; | Описание |
| --- | --- | --- |
| HTTPS |443 (TCP или UDP) |Используется для проверки подлинности устройств. |
| TCP |49443 (TCP) |Используется для проверки подлинности с помощью сертификата. |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a>Таблицы 6a и 6b. Сквозная аутентификация с помощью единого входа (SSO) и синхронизация хэша паролей с помощью единого входа (SSO)
Hello в следующей таблице описываются hello порты и протоколы, которые необходимы для обмена данными между hello Azure AD Connect и Azure AD.

### <a name="table-6a---pass-through-authentication-with-sso"></a>Таблица 6a. Сквозная аутентификация с помощью SSO
|Протокол|Номер порта|Описание
| --- | --- | ---
|HTTP|80|Разрешение исходящего трафика HTTP для проверки безопасности, например SSL. Также требуется для соединителя hello автоматическое обновление toofunction возможность должным образом.
|HTTPS|443| Разрешите исходящий трафик HTTPS для операции, такие как включение и отключение функции hello, регистрация соединителей, загрузка обновлений соединителя и обработка всех пользователь запросов на вход в.

Кроме того, Azure AD Connect должен toohello подключения прямых IP может toomake toobe [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).

### <a name="table-6b---password-hash-sync-with-sso"></a>Таблица 6b. Синхронизация хэша паролей с помощью SSO

|Протокол|Номер порта|Описание
| --- | --- | ---
|HTTPS|443| Включение регистрации единого входа (требуется только для hello процесс регистрации единого входа).

Кроме того, Azure AD Connect должен toohello подключения прямых IP может toomake toobe [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653). Опять же, это только необходимые для процесса регистрации hello единого входа.

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Таблицы 7а и 7б. Агент Azure AD Connect Health для AD FS и синхронизации и Azure AD
Hello следующие таблицы описывают hello конечных точек, порты и протоколы, необходимые для взаимодействия между агентами Azure AD Connect Health и Azure AD

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Таблица 7а. Порты и протоколы для агента Azure AD Connect Health для AD FS и синхронизации и Azure AD
Эта таблица описывает hello исходящие порты и протоколы, необходимые для взаимодействия между агентами hello Azure AD Connect Health и Azure AD.  

| Протокол | порты; | Описание |
| --- | --- | --- |
| HTTPS |443 (TCP или UDP) |Исходящие |
| Azure Service Bus |5671 (TCP или UDP) |Исходящие |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Таблица 7б. Конечные точки для агента Azure AD Connect Health для AD FS и синхронизации и Azure AD
Список конечных точек см. в разделе [hello в разделе "требования" hello Azure AD Connect Health agent](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements).

