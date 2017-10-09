---
title: "Azure AD Connect: устранение неполадок подключения | Документация Майкрософт"
description: "Объясняет, как проблемы подключения tootroubleshoot с Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Устранение неполадок подключения в Azure AD Connect
В этой статье объясняется, как работает подключение между Azure AD Connect и Azure AD и как проблемы подключения tootroubleshoot. Эти вопросы, скорее всего, toobe в среде с прокси-сервера.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Устранить неполадки с подключением в мастере установки hello
Azure AD Connect использует современную проверку подлинности (с помощью библиотеки ADAL hello) для проверки подлинности. приветствия мастера установки и подсистема синхронизации hello правильную требуется toobe machine.config правильно настроен, так как эти два приложения .NET.

В этой статье показано, как Fabrikam подключается tooAzure AD через его прокси-сервер. Hello прокси-сервера с именем fabrikamproxy и использует порт 8080.

Сначала мы должны toomake убедиться, что [ **machine.config** ](active-directory-aadconnect-prerequisites.md#connectivity) настроен правильно.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> В некоторых блогах сторонних производителей это предупреждение, изменения необходимо вносить toomiiserver.exe.config вместо него. Тем не менее этот файл будет перезаписан при каждом обновлении поэтому, даже если он работает во время начальной установки, hello система перестает работать при первом обновлении. По этой причине hello рекомендуется tooupdate machine.config вместо него.
>
>

Hello прокси-сервер должен быть URL-адреса hello требуется открыть. Официальный список Hello документирован в [Office 365 URL-адреса и IP-адресов](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

URL-адресов hello абсолютный исходного состояния системы минимальным toobe может tooconnect tooAzure AD вообще — hello в следующей таблице. Этот список не включает дополнительные функции, такие как обратная запись паролей или Azure AD Connect Health. Это документированные здесь toohelp при устранении неполадок для начальной настройки hello.

| URL-адрес | Порт | Описание |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Список используемых toodownload списка отзыва Сертификатов. |
| \*.verisign.com |HTTP/80 |Список используемых toodownload списка отзыва Сертификатов. |
| \*.entrust.com |HTTP/80 |Используется toodownload CRL перечислены многофакторной проверки Подлинности. |
| \*.windows.net |HTTPS/443 |Используется toosign в tooAzure AD. |
| secure.aadcdn.microsoftonline-p.com |HTTPS/443 |Используется для многофакторной проверки подлинности (MFA). |
| \*.microsoftonline.com |HTTPS/443 |Использовать tooconfigure данными каталога и импорта и экспорта Azure AD. |

## <a name="errors-in-hello-wizard"></a>Ошибки в мастере приветствия
Мастер установки Hello использует два разных контекстах безопасности. На странице приветствия **подключения tooAzure AD**, она использует hello момент выполнен вход пользователя. На странице приветствия **Настройка**, он изменяется toohello [учетной записи службы hello для модуля синхронизации hello](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). Если имеется проблема, похоже, скорее всего, уже находящиеся hello **подключения tooAzure AD** страница в мастере hello, так как конфигурация прокси-сервера hello является глобальным.

hello наиболее распространенных ошибок, возникающих в мастере установки hello Hello следующих ситуаций:

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>не был правильно настроен приветствия мастера установки
Эта ошибка появляется, когда самого мастера hello не могут достичь hello прокси-сервера.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Если вы видите эту ошибку, проверьте hello [machine.config](active-directory-aadconnect-prerequisites.md#connectivity) правильно настроен.
* Если все выглядит правильно, выполните действия hello в [Проверьте подключение к прокси-сервера](#verify-proxy-connectivity) toosee при наличии приветствия мастера также проблема hello.

### <a name="a-microsoft-account-is-used"></a>Используется учетная запись Майкрософт
Если использовать **учетную запись Майкрософт** вместо **учебной или рабочей учетной записи**, то возникнет общая ошибка.  
![Используется учетная запись Майкрософт](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>Конечная точка Hello многофакторной проверки Подлинности недоступна
Эта ошибка возникает, если hello конечной точки **https://secure.aadcdn.microsoftonline-p.com** становится недоступной и к глобальным администратором многофакторной проверки Подлинности включена.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Если вы видите эту ошибку, проверьте этой конечной точке hello **secure.aadcdn.microsoftonline p.com** был добавлен toohello прокси-сервера.

### <a name="hello-password-cannot-be-verified"></a>не удалось проверить пароль Hello
При успешном выполнении в подключении tooAzure AD, но собственно пароля hello приветствия мастера установки не удается проверить, что вы видите эту ошибку:  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* Hello пароль временный пароль и необходимо изменить? Является ли он фактически hello правильный пароль? Попробуйте toosign в toohttps://login.microsoftonline.com (другого компьютера от сервера hello Azure AD Connect) и убедитесь, что можно использовать учетную запись hello.

### <a name="verify-proxy-connectivity"></a>Проверка подключения прокси-сервера
tooverify, если hello Azure AD Connect сервер имеет возможность связи с hello прокси и Интернет, использовать некоторые toosee PowerShell, если hello прокси-сервер разрешает веб-запросы или нет. В командной строке PowerShell выполните командлет `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Технически hello сначала вызывается toohttps://login.microsoftonline.com и этот URI также работает, но hello других URI является быстрее toorespond.)

PowerShell использует конфигурацию hello в файле machine.config toocontact hello прокси. Параметры Hello в winhttp/netsh не должен влиять этих командлетов.

Если hello прокси-сервер настроен правильно, вы должны получить состояние выполнения: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

При получении **удаленному серверу не удается tooconnect toohello**, PowerShell пытается toomake прямой вызов без использования прокси-сервера hello или DNS-сервер не настроен правильно. Убедитесь, что hello **machine.config** файл настроен правильно.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Если hello прокси-сервер настроен неправильно, возникает сообщение об ошибке: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Ошибка | Текст сообщения об ошибке | Комментарий |
| --- | --- | --- |
| 403 |Запрещено |Hello прокси-сервера не был открыт для hello запрошенный URL-адрес. Повторное использование hello конфигурация прокси-сервера и убедитесь, что hello [URL-адреса](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) были открыты. |
| 407 |Требуется проверка подлинности прокси-сервера |Hello прокси-сервера требуется вход и не был предоставлен. Если прокси-сервер требует проверки подлинности, убедитесь, что toohave этот параметр настроен в файле machine.config hello. Также убедитесь, что вы используете учетные записи домена для запуска мастера hello пользователя hello и учетной записи службы hello. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>Hello шаблона обмена данными между Azure AD Connect и Azure AD
Если вы выполнили все описанные выше действия, а подключение по-прежнему невозможно, то обратитесь к журналам сети. В этом разделе описан нормальный, работающий шаблон подключения, Он также список общих herrings красным, которые могут игнорироваться при чтении журналы сети hello.

* Существуют toohttps://dc.services.visualstudio.com вызовов. Это не требуется toohave, можно пропустить этот URL-адрес, откройте hello прокси-сервер для установки toosucceed hello и этих вызовов.
* Вы, разрешение dns списков toobe фактических узлов hello в nsatc.net пространства имени DNS hello и других пространств имен не находится в microsoftonline.com см. Однако не все запросы веб-службы на именах сервера hello и у вас tooadd toohello эти URL-адреса прокси.
* конечные точки adminwebservice Hello и provisioningapi обнаружения конечных точек и используются toouse реальная конечная точка toofind hello. Выбор этих конечных точек зависит от вашего региона.

### <a name="reference-proxy-logs"></a>Справочные журналы прокси-сервера
Вот дамп с прокси журнала и hello установки мастер страницы откуда она была сделана (toohello повторяющиеся записи были удалены одной конечной точкой). Этот раздел можно использовать как образец для собственных журналов прокси-сервера и сети. Фактический Hello конечных точек, может отличаться в вашей среде (в частности эти URL-адреса в *курсивом*).

**Подключение tooAzure AD**

| Время | URL-адрес |
| --- | --- |
| 1/11/2016 8:31 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:31 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Настройка**

| Время | URL-адрес |
| --- | --- |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Первоначальная синхронизация**

| Время | URL-адрес |
| --- | --- |
| 1/11/2016 8:48 |connect://login.windows.net:443 |
| 1/11/2016 8:49 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba800-anchor*.microsoftonline.com:443 |

## <a name="authentication-errors"></a>Ошибки проверки подлинности
В этом разделе описываются ошибки, которые могут быть возвращены из ADAL (hello библиотеки проверки подлинности, используемой Azure AD Connect) и PowerShell. Ошибка Hello описано поможет в понять, выполните следующие действия.

### <a name="invalid-grant"></a>Недопустимый набор прав
Недопустимое имя пользователя или пароль. Дополнительные сведения см. в разделе [hello пароль не может быть проверена](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Неизвестный тип пользователя
Невозможно найти или разрешить каталог Azure AD. Может быть попытке toologin с именем пользователя в непроверенном домене?

### <a name="user-realm-discovery-failed"></a>Не удалось выполнить обнаружение области пользователя
Проблемы конфигурации сети или прокси-сервера. Hello сеть становится недоступной. В разделе [устранить неполадки с подключением в мастере установки hello](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>Срок действия пароля пользователя истек
Срок действия ваших учетных данных истек. Измените пароль.

### <a name="authorizationfailure"></a>AuthorizationFailure
Неизвестная проблема.

### <a name="authentication-cancelled"></a>Проверка подлинности отменена
Hello многофакторной проверки подлинности (MFA) запрос был отменен.

### <a name="connecttomsonline"></a>ConnectToMSOnline
Проверка подлинности прошла успешно, но есть проблема с проверкой подлинности в Azure AD PowerShell.

### <a name="azurerolemissing"></a>AzureRoleMissing
Проверка подлинности прошла успешно. Вы не являетесь глобальным администратором.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
Проверка подлинности прошла успешно. Было включено управление привилегированными пользователями, и в настоящее время вы не являетесь глобальным администратором. Дополнительные сведения см. в статье [Приступая к работе с управлением привилегированными пользователями Azure AD](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
Проверка подлинности прошла успешно. Не удалось получить от Azure AD сведения об организации.

### <a name="retrievedomains"></a>RetrieveDomains
Проверка подлинности прошла успешно. Не удалось получить от Azure AD сведения о домене.

### <a name="unexpected-exception"></a>Неожиданное исключение
Показано, как непредвиденная ошибка в мастере установки hello. Может произойти при попытке toouse **учетную запись Майкрософт** вместо **учетной записи учебного заведения или организации**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Действия по устранению неполадок для предыдущих версий.
С версиями, начиная с номера построения 1.1.105.0 (выпущена февраля 2016 г.) было прекращено hello помощника по входу. Этот раздел и hello конфигурации больше не требуется, а также хранится как ссылка.

Hello единого входа в toowork помощника необходимо настроить winhttp. Эту настройку можно сделать с помощью [**netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>не был правильно настроен Hello помощника по входу
Эта ошибка появляется, когда hello помощника по входу не может достичь hello прокси-сервера или прокси-сервера hello не разрешает запроса hello.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Если вы видите эту ошибку, просмотрите hello конфигурация прокси-сервера в [netsh](active-directory-aadconnect-prerequisites.md#connectivity) и проверьте его правильность.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Если все выглядит правильно, выполните действия hello в [Проверьте подключение к прокси-сервера](#verify-proxy-connectivity) toosee при наличии приветствия мастера также проблема hello.

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
