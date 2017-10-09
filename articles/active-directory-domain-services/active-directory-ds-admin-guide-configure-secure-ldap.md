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
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD
В этой статье показано, как включить протокол LDAPS для управляемого домена доменных служб Azure AD. Защищенный протокол LDAP также называется "LDAP через SSL или TLS".

## <a name="before-you-begin"></a>Перед началом работы
tooperform hello задачи, перечисленные в этой статье, необходимо:

1. Действующая **подписка Azure**.
2. **Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.
3. **Доменные службы Azure AD** должна быть включена для каталога hello Azure AD. Если вы еще не сделали этого, выполните все действия hello hello [руководство по началу работы](active-directory-ds-getting-started.md).
4. Объект **tooenable toobe используется сертификат защищенный LDAP**.

   * **Рекомендуется** получить сертификат из доверенного общедоступного центра сертификации. Этот параметр конфигурации обеспечивает повышенную безопасность.
   * Кроме того, можно также выбрать слишком[создать самозаверяющий сертификат](#task-1---obtain-a-certificate-for-secure-ldap) как показано далее в этой статье.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Требования для безопасного LDAP сертификата hello
Получить действительный сертификат на hello инструкциями, прежде чем включать защищенного протокола LDAP. Сбой при попытке tooenable защищенный LDAP для управляемого домена с неправильный или недопустимый сертификат.

1. **Надежного издателя** -hello сертификат должен быть выдан центром сертификации, доверенным для компьютеров, подключающихся управляемого домена toohello использование защищенного протокола LDAP. Это может быть общедоступный центр сертификации, который является доверенным для этих компьютеров.
2. **Время существования** -hello сертификат должен быть допустимым для по крайней мере hello следующие 3 – 6 месяцев. Срок действия сертификата hello разрыва безопасного доступа tooyour управляемого домена LDAP.
3. **Имя субъекта** -hello имя субъекта сертификата hello должно быть подстановочный знак для управляемого домена. Для экземпляра, если ваш домен называется «contoso100.com», имя субъекта сертификата hello должен быть "*. contoso100.com". Задать toothis hello DNS-имя (альтернативное имя субъекта) имя подстановочный знак.
4. **Использование ключа** - hello необходимо настроить сертификат для использует следующие hello - цифровые подписи и шифрование ключей.
5. **Назначение сертификата** -hello сертификат должен быть допустимым для проверки подлинности сервера SSL.

> [!NOTE]
> **Центры сертификации предприятия**. Доменные службы Azure AD не поддерживают использование сертификатов защищенного протокола LDAP, выдающихся центром сертификации предприятия. Это ограничение действует, так как служба hello не доверяет центр сертификации в качестве корневого центра сертификации предприятия. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Задача 1. Получение сертификата для защищенного протокола LDAP
Первая задача Hello предполагает получение сертификата, используемого для безопасного доступа toohello управляемого домена LDAP. Существует два варианта.

* Получите сертификат в центре сертификации. Возможно, центр Hello общедоступным центром сертификации.
* Создать самозаверяющий сертификат.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>Вариант А (рекомендуется). Получение сертификата защищенного протокола LDAP из центра сертификации
Если ваша организация получает сертификаты из общедоступного центра сертификации, вам понадобится сертификат hello безопасного tooobtain LDAP из этого общедоступным центром сертификации.

При запросе сертификата, убедиться в выполнении всех hello требованиям, приведенным в [требования для безопасного LDAP сертификата hello](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Клиентские компьютеры, которым требуется управляемый домен tooconnect toohello использование защищенного протокола LDAP должны доверять hello издателя hello безопасный LDAP сертификата.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Вариант Б. Создание самозаверяющего сертификата для защищенного протокола LDAP
Если предполагается, что toouse сертификата из общедоступного центра сертификации, вы можете toocreate самозаверяющего сертификата для защищенного LDAP.

**Создание самозаверяющего сертификата с использованием PowerShell**

На компьютере Windows, откройте окно PowerShell от **администратора** и типа hello следующие команды, toocreate новый самозаверяющий сертификат.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

В предыдущих образец hello, замените "*. contoso100.com" hello DNS-имени домена управляемого домена. Например, при создании управляемого домена с именем «contoso100.onmicrosoft.com» заменить "*. contoso100.com" в hello выше скрипт с "*. contoso100.onmicrosoft.com").

![Выбор каталога Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

самозаверяющий сертификат только что созданный Hello помещается в хранилище сертификатов локального компьютера hello.


## <a name="next-step"></a>Дальнейшие действия
[Задача 2 - сертификат tooa экспорта hello безопасный LDAP. PFX-файла](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
