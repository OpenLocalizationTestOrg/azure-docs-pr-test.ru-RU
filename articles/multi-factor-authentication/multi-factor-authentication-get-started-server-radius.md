---
title: "aaaRADIUS проверки подлинности и сервера Azure MFA | Документы Microsoft"
description: "Это является hello Azure многофакторной проверки подлинности, будет полезен при развертывании проверки подлинности RADIUS и сервера Azure Multi-factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>Интеграция аутентификации RADIUS с сервером Многофакторной идентификации Azure
Использовать проверку подлинности RADIUS hello раздел tooenable сервера Azure MFA и настроить проверку подлинности RADIUS. RADIUS является стандартного протокола tooaccept запросы проверки подлинности и tooprocess эти запросы. Hello сервера Azure Multi-factor Authentication выступает в качестве RADIUS-сервера. Вставьте между клиентом RADIUS (устройством VPN) и целевым объектом проверки подлинности, которого может быть Active Directory (AD), каталог LDAP или другой tooadd сервера RADIUS Azure Multi-factor Authentication. Для toofunction многофакторной проверки подлинности Azure (MFA) необходимо настроить hello Azure многофакторной проверки Подлинности сервера, чтобы он мог обмениваться данными серверы клиентского hello и целевой объект проверки подлинности hello. Hello многофакторной проверки Подлинности сервера Azure принимает запросы от клиента RADIUS, проверяет учетные данные с целевым объектом проверки подлинности hello, добавляет Azure Multi-factor Authentication и отправляет ответ назад toohello RADIUS-клиента. запрос проверки подлинности Hello завершается успешно, только если основной проверки подлинности hello и hello Azure Multi-factor Authentication успешно.

> [!NOTE]
> Hello многофакторной проверки Подлинности сервера поддерживает только PAP (протокол проверки пароля) и MSCHAPv2 (протокол проверки подлинности запроса подтверждения корпорации Майкрософт) RADIUS протоколы, действуя как RADIUS-сервер.  Другие протоколы, такие как EAP (extensible authentication protocol), может использоваться, когда сервер многофакторной проверки Подлинности hello действует как сервер RADIUS tooanother прокси-сервера RADIUS, поддерживает этот протокол.
>
> В этой конфигурации односторонних SMS и OATH маркеров не работает, поскольку hello многофакторной проверки Подлинности сервера не может инициировать успешного ответа RADIUS запрос с использованием альтернативных протоколов.

![Проверка подлинности RADIUS](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>Добавление клиента RADIUS
tooconfigure проверку подлинности RADIUS, hello установки сервера Azure Multi-factor Authentication на Windows server. Если у вас есть среда Active Directory, сервер hello должен быть присоединены к домену toohello домена в сети hello. Используйте следующие процедуры tooconfigure hello сервера Azure Multi-factor Authentication hello.

1. В hello Azure многофакторной проверки подлинности сервера щелкните значок проверки подлинности RADIUS hello в левом меню hello.
2. Проверьте hello **включить проверку подлинности RADIUS** флажок.
3. На вкладке "Клиенты" hello измените hello проверки подлинности и порты для учетных данных, если hello многофакторной проверки Подлинности RADIUS Azure служба должна toolisten запросов RADIUS на нестандартные порты.
4. Щелкните **Добавить**.
5. Введите IP-адрес hello hello устройство или сервер, будет выполнена проверка подлинности toohello сервера Azure Multi-factor Authentication, имя приложения (необязательно) и общий секрет.

  Имя приложения Hello отображается в отчетах Azure Multi-factor Authentication и может отображаться в SMS или мобильное приложение проверки подлинности сообщений.

  Hello общего секретного потребностей toobe hello одинаковым на обоих hello Azure многофакторной проверки подлинности сервера и устройство или сервер.

6. Проверьте hello **сопоставление требовать многофакторную проверку подлинности пользователей** поле, если все пользователи были или будут импортированы в сервер hello и toomulti двухфакторной проверки подлинности субъекта. Если значительное число пользователей еще не были импортированы в сервер hello или будут исключены из двухшаговую проверку, не hello флажок.
7. Проверьте hello **включить резервный OATH-токен** поле, если требуется секретные коды OATH toouse подтверждение по мобильному телефону приложений как резервный toohello по каналу телефонный звонок, SMS, или push-уведомлений.
8. Нажмите кнопку **ОК**.

Повторите шаги 4-8 tooadd столько дополнительных клиентов RADIUS, сколько требуется.

## <a name="configure-your-radius-client"></a>Настройка клиента RADIUS

1. Нажмите кнопку hello **целевой** вкладки.
2. Если hello Azure многофакторной проверки Подлинности сервера установлена на сервере, присоединенном к домену в среде Active Directory, выберите домен Windows.
3. Если пользователи должны проходить аутентификацию для каталога LDAP, выберите **привязку LDAP**.

  toouse привязки LDAP, щелкните значок интеграции каталогов hello и изменить hello конфигурации LDAP на вкладке Параметры hello, hello Server можно привязать tooyour каталога. Инструкции по настройке LDAP можно найти в hello [руководство по конфигурации прокси-сервера LDAP](multi-factor-authentication-get-started-server-ldap.md).

4. Если пользователи должны проходить проверку подлинности в отношении другого сервера RADIUS, выберите сервер (серверы) RADIUS.
5. Нажмите кнопку **добавить** запрашивает tooconfigure hello toowhich hello сервера Azure MFA будет прокси приветствие сервера RADIUS.
6. В диалоговом окне Добавление RADIUS-сервера hello введите IP-адрес hello hello сервера RADIUS и общий секрет.

  Hello общего секретного потребностей toobe hello одинаковым на обоих hello Azure многофакторной проверки подлинности сервера и RADIUS-сервер. Измените порт проверки подлинности hello и порт для учетных данных, если hello сервером RADIUS используются другие порты.

7. Нажмите кнопку **ОК**.
8. Добавьте hello Azure многофакторной проверки Подлинности сервера как RADIUS-клиента в hello другого сервера RADIUS, чтобы она может обрабатывать запросы доступа, отправленные tooit из hello Azure многофакторной проверки Подлинности сервера. Используйте hello же общий секрет, настроенный в hello сервера Azure Multi-factor Authentication.

Повторите эти шаги tooadd дополнительные серверы RADIUS и настраивать порядок hello какие hello Azure многофакторной проверки Подлинности сервера должен вызывать их с hello **вверх** и **вниз** кнопки.

На этом завершается hello конфигурации сервера Azure Multi-factor Authentication. Теперь Hello Server прослушивает hello настроить порты для запросов доступа RADIUS от клиентов настроен hello.   

## <a name="radius-client-configuration"></a>Настройка клиента RADIUS
hello tooconfigure клиента RADIUS, воспользуйтесь рекомендациями hello.

* Настройка вашего устройства/сервера tooauthenticate через toohello Azure многофакторной проверки подлинности сервера RADIUS IP-адрес, который будет выступать в качестве сервера RADIUS hello.
* Используйте hello же общий секрет, который был настроен ранее.
* Настройте время ожидания too30 60 hello RADIUS с таким образом, что время toovalidate hello учетные данные пользователя, выполнить двухшаговую проверку, получение ответа и реагирования на запрос доступа RADIUS toohello.
