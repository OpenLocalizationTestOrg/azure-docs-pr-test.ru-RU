---
title: "коды ошибок aaaTroubleshoot для hello расширения NPS многофакторной проверки Подлинности Azure | Документы Microsoft"
description: "Получить помощь в решении проблемы, связанные с hello NPS расширения для многофакторной проверки подлинности Azure с методы устранения для распространенных сообщений об ошибках"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Разрешить сообщения об ошибках из hello NPS расширения для многофакторной проверки подлинности Azure

При возникновении ошибки, связанные с hello NPS расширения многофакторной проверки подлинности Azure, быстрее используйте tooreach этой статье разрешение. 

## <a name="troubleshooting-steps-for-common-errors"></a>Действия по устранению распространенных ошибок

| Код ошибки | Действия по устранению неполадок |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [Обратитесь в службу поддержки](#contact-microsoft-support)и назовите hello список шагов для сбора журналов. Предоставляет столько информации, а также о произошедшее перед ошибкой hello, включая идентификатор клиента и имя участника-пользователя (UPN). |
| **CLIENT_CERT_INSTALL_ERROR** | Возможно, проблема с как hello клиентский сертификат был установлен или связанные с вашим клиентом. Следуйте инструкциям в разделе hello [Устранение неполадок hello многофакторной проверки Подлинности NPS расширения](multi-factor-authentication-nps-extension.md#troubleshooting) проблемы cert tooinvestigate клиента. |
| **ESTS_TOKEN_ERROR** | Следуйте инструкциям в разделе hello [Устранение неполадок hello многофакторной проверки Подлинности NPS расширения](multi-factor-authentication-nps-extension.md#troubleshooting) сертификата клиента tooinvestigate и ADAL токен проблем. |
| **HTTPS_COMMUNICATION_ERROR** | сервер политики сети Hello — не удается tooreceive ответов от многофакторной проверки Подлинности Azure. Убедитесь, что брандмауэры откройте двух направлениях для трафика tooand из https://adnotifications.windowsazure.com |
| **HTTP_CONNECT_ERROR** | Hello сервер под управлением NPS расширения hello убедитесь, что можно получить доступ к https://adnotifications.windowsazure.com и https://login.microsoftonline.com/. Если эти сайты не загружаются, необходимо устранить неполадки подключения на сервере. |
| **REGISTRY_CONFIG_ERROR** | Отсутствует ключ в реестре hello для приложения hello, которое может быть вызвано hello [сценарий PowerShell](multi-factor-authentication-nps-extension.md#install-the-nps-extension) не было выполнить после установки. сообщение об ошибке Hello должен включать hello отсутствует ключ. Убедитесь, что у вас есть ключ HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa hello. |
| **REQUEST_FORMAT_ERROR** <br> Отсутствует обязательный атрибут userName\Identifier для запроса RADIUS. Убедитесь, что NPS-сервер получает запросы RADIUS. | В этом случае проблема связана с установкой. Hello NPS расширения должны устанавливаться в NPS-серверы, которые могут получать запросы RADIUS. NPS-серверы, установленные как зависимости для таких служб, как RDG и RRAS, запросы RADIUS не получают. Модуль политики сети не работает при установке через такие установок и ошибок, так как его не удается прочитать сведения hello hello запрос проверки подлинности. |
| **REQUEST_MISSING_CODE** | Убедитесь, что протокол шифрования пароля hello между hello сервер политики сети и серверов NAS поддерживает hello дополнительного способа проверки подлинности, которую вы используете. **PAP** поддерживает все методы проверки подлинности hello Azure MFA в облаке hello: телефонный звонок, односторонний текстовое сообщение, уведомление мобильного приложения и код проверки мобильного приложения. **CHAPV2** и **EAP** поддерживают телефонный звонок или уведомление мобильного приложения. |
| **USERNAME_CANONICALIZATION_ERROR** | Убедитесь, что пользователь hello имеется в ваш локальный экземпляр Active Directory и, служба NPS hello имеет каталог hello tooaccess разрешения. Если вы используете отношения доверия между лесами, [обратитесь в службу поддержки](#contact-microsoft-support) для получения дополнительных сведений. |


   

### <a name="alternate-login-id-errors"></a>Ошибки с альтернативным именем пользователя

| Код ошибки | Сообщение об ошибке | Действия по устранению неполадок |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | Ошибка. Сбой поиска userObjectSid. | Убедитесь, что этот пользователь hello существует в вашем экземпляре в локальной среде Active Directory. Если вы используете отношения доверия между лесами, [обратитесь в службу поддержки](#contact-microsoft-support) для получения дополнительных сведений. |
| **ALTERNATE_LOGIN_ID_ERROR** | Ошибка. Сбой поиска альтернативного имени пользователя. | Убедитесь, что LDAP_ALTERNATE_LOGINID_ATTRIBUTE tooa [атрибут допустимым active directory](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx). <br><br> Если LDAP_FORCE_GLOBAL_CATALOG имеет значение tooTrue или LDAP_LOOKUP_FORESTS оснащен непустое значение, убедитесь, что вы настроили глобального каталога и этот атрибут AlternateLoginId hello добавляется tooit. <br><br> Если LDAP_LOOKUP_FORESTS настроен непустое значение, проверьте правильность значения hello. Если имеется более одного имени леса, hello имена должны разделяться точкой с запятой, пробелы не допускаются. <br><br> Если эти шаги не устранит проблему hello, [обратитесь в службу поддержки](#contact-microsoft-support) для получения дополнительных сведений. |
| **ALTERNATE_LOGIN_ID_ERROR** | Ошибка. Пустое значение альтернативного имени пользователя. | Убедитесь, что этот атрибут AlternateLoginId hello настроено для пользователя hello. |


## <a name="errors-your-users-may-encounter"></a>Ошибки, с которыми могут столкнуться пользователи

| Код ошибки | Сообщение об ошибке | Действия по устранению неполадок |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | Вызывающий объект клиента имеет toodo проверки подлинности разрешения доступа для пользователя hello | Проверьте ли hello домен и домен hello hello имя участника-пользователя (UPN) hello таким же. Например, убедитесь, что user@contoso.com пытается tooauthenticate toohello Contoso клиента. Имя участника-пользователя Hello представляет допустимого пользователя для клиента hello в Azure. |
| **AuthenticationMethodNotConfigured** | Hello указан метод проверки подлинности не был настроен для пользователя hello | Hello пользователя добавить или проверить их методов проверки, согласно инструкциям toohello [управления параметрами для двухшаговой проверки](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **AuthenticationMethodNotSupported** | Указанный метод проверки подлинности не поддерживается. | Соберите все журналы, которые содержат эту ошибку, и [обратитесь в службу поддержки](#contact-microsoft-support). При обращении в службу поддержки укажите пользователя hello и метод вторичной проверки hello, запустившего hello ошибки. |
| **BecAccessDenied** | MSODS Bec, возвращенного отказано в доступе, вероятно, hello username не определен в клиенте hello | пользователь Hello присутствует в Active Directory в локальной среде, но не синхронизирована в Azure AD с AD Connect. Или пользователь hello отсутствует для клиента hello. Добавить tooAzure hello пользователя AD и попросите добавить их методов проверки, согласно инструкциям toohello [управления параметрами для двухшаговой проверки](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **InvalidFormat** или **StrongAuthenticationServiceInvalidParameter** | номер телефона Hello находится в неизвестном формате | Быть hello пользователю исправить свои номера телефонов проверки. |
| **InvalidSession** | Hello указанного сеанса является недопустимым, или истек | Hello сеанса было более чем toocomplete три минуты. Проверьте этот пользователь hello ввода кода проверки hello, или отвечает toohello уведомление приложения, в течение трех минут после инициации запроса проверки подлинности hello. Если hello проблема не устраняется, убедитесь, что нет сетевые задержки между клиентом, сервер NAS, сервер политики сети и конечной точки hello многофакторной проверки Подлинности Azure.  |
| **NoDefaultAuthenticationMethodIsConfigured** | Метод проверки подлинности по умолчанию был настроен для пользователя hello | Hello пользователя добавить или проверить их методов проверки, согласно инструкциям toohello [управления параметрами для двухшаговой проверки](./end-user/multi-factor-authentication-end-user-manage-settings.md). Проверьте пользователем hello выбран метод проверки подлинности по умолчанию и настроить этот метод для своей учетной записи. |
| **OathCodePinIncorrect** | Введен неправильный пароль и ПИН-код. | Эта ошибка не ожидается в hello расширения сервера политики сети. В случае возникновения этой ошибки [обратитесь в службу поддержки](#contact-microsoft-support) для получения сведений по устранению проблемы. |
| **ProofDataNotFound** | Проверки данных не была настроена для hello указан метод проверки подлинности. | Hello пользователя повторите проверки другой метод или добавления новых методов проверки, согласно инструкциям toohello [управления параметрами для двухшаговой проверки](./end-user/multi-factor-authentication-end-user-manage-settings.md). Если пользователь hello продолжает toosee ошибки окончании подтверждения правильно настроить свой способ проверки [обратитесь в службу поддержки](#contact-microsoft-support). |
| **SMSAuthFailedWrongCodePinEntered** | Введен неправильный пароль и ПИН-код. (OneWaySMS) | Эта ошибка не ожидается в hello расширения сервера политики сети. В случае возникновения этой ошибки [обратитесь в службу поддержки](#contact-microsoft-support) для получения сведений по устранению проблемы. |
| **TenantIsBlocked** | Клиент заблокирован. | [Обратитесь в службу поддержки](#contact-microsoft-support) с Идентификатором каталога со страницы свойств hello Azure AD в hello портал Azure. |
| **UserNotFound** | Hello указанный пользователь не найден. | Hello клиента больше не отображается как активный в Azure AD. Убедитесь, что подписка активна, и у вас есть hello обязательные первой стороны приложения. Также убедитесь, что клиент hello в субъект сертификата hello — должным образом и hello сертификата истек, а зарегистрированный в разделе hello участника-службы. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>Другие сообщения, с которыми могут столкнуться пользователи

В некоторых случаях пользователи могут получить сообщения от Многофакторной идентификации из-за сбоя запроса проверки подлинности. Эти ограничения не являются ошибок в продукте hello конфигурации, но преднамеренного предупреждения объясняющий, почему был отклонен запрос проверки подлинности.

| Код ошибки | Сообщение об ошибке | Рекомендуемые действия | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | Введен неправильный код. Неправильный OATH-код. | Это не ошибка, просто пользователь ввел неправильный код. | Hello пользователь ввел неправильный код hello. Пользователь должен повторить попытку ввода. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | Достигнуто максимальное число попыток ввода кода. | пользователь Hello не пройдена проверка проверки hello слишком много раз. В зависимости от настроек они может понадобиться toobe теперь разблокирован администратором.  |
| **SMSAuthFailedWrongCodeEntered** | Введен неправильный код. SMS: неверный OTP. | Hello пользователь ввел неправильный код hello. Пользователь должен повторить попытку ввода. |

## <a name="errors-that-require-support"></a>Ошибки, при возникновении которых стоит обратиться в службу поддержки

Если вы столкнулись с ошибками, приведенными ниже, мы советуем [обратиться в службу поддержки](#contact-microsoft-support) для помощи в диагностике. Это нестандартные ошибки, поэтому они требуют отдельного анализа. При обращении в службу поддержки, что tooinclude как можно больше информации о действиях hello, ставших tooan ошибки и информацию о вашем клиенте.

| Код ошибки | Сообщение об ошибке |
| ---------- | ------------- |
| **InvalidParameter** | Запрос не может иметь значение null. |
| **InvalidParameter** | Параметр ObjectId не может иметь значение null или быть пустым для ReplicationScope:{0} |
| **InvalidParameter** | Здравствуйте, длина CompanyName \{0} \ превышает максимально допустимую длину {1} hello |
| **InvalidParameter** | Параметр UserPrincipalName не может иметь значение null или быть пустым. |
| **InvalidParameter** | Hello при условии, что TenantId не находится в правильном формате |
| **InvalidParameter** | Параметр SessionId не может иметь значение null или быть пустым. |
| **InvalidParameter** | Не удалось распознать данные для подтверждения из запроса или MSODS. Hello ProofData неизвестно |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>Дальнейшие действия

### <a name="troubleshoot-user-accounts"></a>Устранение неполадок, связанных с учетными данными пользователей

Если пользователи столкнулись с проблемами [двухфакторной проверки подлинности](./end-user/multi-factor-authentication-end-user-troubleshoot.md), они могут выполнить самостоятельную диагностику. 

### <a name="contact-microsoft-support"></a>Обратиться в службу поддержки Майкрософт

Если вам требуется дополнительная помощь, обратитесь к службе поддержки, используя [поддержку сервера многофакторной идентификации Azure](https://support.microsoft.com/oas/default.aspx?prid=14947). Вы можете облегчить нам задачу, если при обращении предоставите максимально полные сведения о проблеме. Сведения, которые вы можете предоставить включает hello страницы, где можно было увидеть ошибки hello, hello ошибки кода в сеансе с определенным Идентификатором hello, hello идентификатор пользователя hello, видели ошибки hello и отладочный журналы.

журналы отладки toocollect для поддержки диагностики, используйте hello следующие шаги: 

1. Откройте командную строку администратора и выполните следующие команды:

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Воспроизведение проблемы hello

3. Остановите трассировку hello с помощью следующих команд:

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. ZIP-архив hello содержимое папки C:\NPS hello и подключить службу технической поддержки Майкрософт toohello hello ZIP-файл.


