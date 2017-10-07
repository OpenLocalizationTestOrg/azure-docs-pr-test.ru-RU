---
title: "проблем при подключении к Azure точки сайтами aaaTroubleshoot | Документы Microsoft"
description: "Узнайте, как tootroubleshoot проблем при подключении точки сайтами."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Устранение неполадок подключения типа "точка — сеть" Azure

В этой статье перечисляются распространенные проблемы подключения типа "точка — сеть", которые могут возникнуть. Кроме того, здесь рассматриваются возможные причины этих проблем и способы их устранения.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>Ошибка VPN-клиента: не удалось найти сертификат

### <a name="symptom"></a>Симптом

При попытке tooconnect tooan виртуальная сеть Azure с помощью VPN-клиента hello появляется hello следующие сообщение об ошибке:

**Не удалось найти сертификат, который был бы использован с протоколом расширенной проверки подлинности (EAP). (Ошибка 798.)**

### <a name="cause"></a>Причина:

Эта проблема возникает, если отсутствует сертификат клиента hello **Сертификаты — текущий пользователь\личные\сертификаты**.

### <a name="solution"></a>Решение

Убедитесь, что этот сертификат клиента hello установлен в расположение хранилища сертификатов hello (Certmgr.msc) после hello:
 
**Certificates - Current User\Personal\Certificates**

Дополнительные сведения о как tooinstall hello сертификата клиента см. в разделе [Создание и экспорт сертификатов для соединений точка сеть](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> При импорте hello сертификат клиента, не устанавливайте hello **Включить усиленную защиту закрытого ключа** параметр.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>Ошибка клиента VPN: получено сообщение hello был неверным или оно имеет неправильный формат

### <a name="symptom"></a>Симптом

При попытке tooconnect tooan виртуальная сеть Azure с помощью VPN-клиента hello появляется hello следующие сообщение об ошибке:

**Полученное сообщение Hello был неверным или оно имеет неправильный формат. (Ошибка 0x80090326.)**

### <a name="cause"></a>Причина:

Эта проблема возникает, если hello корневого сертификата открытый ключ не был загружен на шлюз Azure VPN hello. Он также может возникать, если ключ hello повреждена или истек срок действия.

### <a name="solution"></a>Решение

tooresolve эту проблему, проверьте состояние hello hello корневого сертификата в hello Azure портала toosee ли он отозван. Если он не был отозван, попробуйте toodelete hello корневой сертификат и reupload. Дополнительные сведения см. в разделе [Создание сертификатов](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>Ошибка VPN-клиента: цепочка сертификатов обработана, но обработка прервана 

### <a name="symptom"></a>Симптом 

При попытке tooconnect tooan виртуальная сеть Azure с помощью VPN-клиента hello появляется hello следующие сообщение об ошибке:

**Цепочка сертификатов обработана, но обработка прервана на корневом сертификате, который не доверяет поставщик доверия hello.**

### <a name="solution"></a>Решение

1. Убедитесь что hello следующие сертификаты в правильном расположении hello.

    | Сертификат | Расположение |
    | ------------- | ------------- |
    | AzureClient.pfx  | Current User\Personal\Certificates |
    | Azuregateway-*GUID*.cloudapp.net  | Current User\Trusted Root Certification Authorities|
    | AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer    | Local Computer\Trusted Root Certification Authorities|

2. Hello сертификаты, в расположении hello, попробуйте toodelete hello сертификаты и установите их заново. Hello  **azuregateway -*GUID*. cloudapp.net** сертификат находится в пакет конфигурации клиента VPN hello, загруженный с портала Azure hello. Можно использовать файл archivers tooextract hello файлы из пакета hello.

## <a name="file-download-error-target-uri-is-not-specified"></a>Произошла ошибка скачивания файла. Целевой URI не указан

### <a name="symptom"></a>Симптом

Появляется сообщение об ошибке после hello:

**Ошибка скачивания файла. Не указан целевой URI.**

### <a name="cause"></a>Причина: 

Эта проблема возникает из-за неправильного типа шлюза. 

### <a name="solution"></a>Решение

должен быть тип шлюза VPN Hello **VPN**, и должен быть тип VPN hello **routebased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>Ошибка VPN-клиента: сбой настраиваемого сценария VPN Azure 

### <a name="symptom"></a>Симптом

При попытке tooconnect tooan виртуальная сеть Azure с помощью VPN-клиента hello появляется hello следующие сообщение об ошибке:

**Пользовательский сценарий (tooupdate маршрут таблица) не удалось. (Error 8007026f)** (Произошел сбой настраиваемого сценария (для обновления таблицы маршрутизации). (Ошибка 8007026f)).

### <a name="cause"></a>Причина:

Эта проблема может возникнуть, если вы пытаетесь tooopen hello сайта в точке VPN-подключение с помощью ярлыка.

### <a name="solution"></a>Решение 

Откройте пакет VPN hello напрямую, вместо открытия его с помощью ярлыка hello.

## <a name="cannot-install-hello-vpn-client"></a>Не удается установить VPN-клиента hello

### <a name="cause"></a>Причина: 

Дополнительный сертификат является обязательным tootrust hello VPN-шлюз для виртуальной сети. Hello сертификат включается в пакет конфигурации клиента VPN hello, созданный из hello портал Azure.

### <a name="solution"></a>Решение

Извлеките пакет конфигурации VPN-клиента hello и найти hello CER-файл. tooinstall hello сертификатов, выполните следующие действия:

1. Запустите mmc.exe.
2. Добавить hello **сертификаты** оснастки.
3. Выберите hello **компьютера** учетной записи для hello локального компьютера.
4. Щелкните правой кнопкой мыши hello **доверенные корневые центры сертификации** узла. Нажмите кнопку **все задачи** > **импорта**и обзор toohello CER-файл, извлеченный из пакета конфигурации клиента VPN hello.
5. Перезагрузите компьютер hello. 
6. Попробуйте tooinstall hello VPN-клиента.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Azure портала ошибка: не удалось выполнить toosave hello VPN-шлюз и hello данные являются недопустимыми

### <a name="symptom"></a>Симптом

При попытке изменения hello toosave для шлюза VPN hello в hello портал Azure, появляется сообщение об ошибке после hello:

**Шлюз виртуальной сети не удалось toosave &lt;* имя шлюза*&gt;. Недействительные данные для сертификата &lt;*идентификатор сертификата*&gt;**.

### <a name="cause"></a>Причина: 

Эта проблема может возникнуть, если hello корневого сертификата открытый ключ, который вы отправили содержит недопустимый символ, например пробел.

### <a name="solution"></a>Решение

Убедитесь, что данные hello в сертификате hello не содержит недопустимые символы, такие как разрывы строки (возврат каретки). Hello всего должно содержать одну строку. После текста Hello приведен образец hello сертификата.

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Azure портала ошибка: не удалось выполнить toosave hello VPN-шлюз и недопустимое имя ресурса hello

### <a name="symptom"></a>Симптом

При попытке изменения hello toosave для шлюза VPN hello в hello портал Azure, появляется сообщение об ошибке после hello: 

**Шлюз виртуальной сети не удалось toosave &lt;* имя шлюза*&gt;. Имя ресурса &lt; *имя сертификата, попробуйте tooupload* &gt; является недопустимым **.

### <a name="cause"></a>Причина:

Эта проблема возникает, поскольку имя hello hello сертификата содержит недопустимый символ, например пробел. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Ошибка портала Azure: ошибка 503 при скачивании файла пакета VPN

### <a name="symptom"></a>Симптом

При запуске пакета конфигурации клиента VPN toodownload hello, появляется сообщение об ошибке после hello:

**Не удалось выполнить файл toodownload hello. Сведения об ошибке: ошибки 503. Hello сервер занят.**
 
### <a name="solution"></a>Решение

Эта ошибка может быть вызвана временным сбоем сети. Пакет VPN toodownload hello, повторите попытку через несколько минут.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>Обновление VPN-шлюз Azure: P2S все клиенты, не удается tooconnect

### <a name="cause"></a>Причина:

Если сертификат hello более 50 процентов через своего времени существования, будут перезаписаны hello сертификата.

### <a name="solution"></a>Решение

tooresolve эту проблему, создавать и распространять новые сертификаты toohello VPN-клиентов. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Слишком много одновременно подключенных VPN-клиентов

Для каждого шлюза VPN hello максимальное число разрешенных подключений — 128. Вы увидите hello общее количество подключенных клиентов в hello портал Azure.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>Точка сеть VPN неправильно добавляет маршрут для таблицы маршрутов toohello 10.0.0.0/8

### <a name="symptom"></a>Симптом

При наборе hello VPN-подключения на клиенте точки сайтами hello hello VPN-клиента следует добавить маршрут к hello виртуальной сети Azure. Служба модуля поддержки IP Hello следует добавить маршрут для подсети hello hello VPN-клиентов. 

Hello диапазон клиентов VPN принадлежит меньшее подсети 10.0.0.0/8, например 10.0.12.0/24 tooa. Вместо маршрута для 10.0.12.0/24 добавляется маршрут для 10.0.0.0/8, который имеет более высокий приоритет. 

Этот маршрут неверные разрывает связь с других локальных сетях может принадлежать tooanother подсети в пределах диапазона 10.0.0.0/8 hello, такие как 10.50.0.0/24, у которых нет определенных конкретного маршрута. 

### <a name="cause"></a>Причина:

Это сделано намеренно для клиентов Windows. Когда клиент hello использует протокол PPP IPCP hello, он получает hello IP-адрес интерфейса туннеля hello сервере hello (шлюз VPN hello в данном случае). Однако из-за ограничений в протокол hello, hello клиента нет hello маску подсети. Так как нет других tooget способом, клиент hello предпринимается на основе класса hello hello туннельный интерфейс IP-адреса, маски подсети hello tooguess. 

Таким образом маршрут добавляется основании hello после статического сопоставления: 

Если адрес принадлежит tooclass A--> Применить/8 больше

Если адрес относится tooclass--> B применить /16

Если адрес относится C--> tooclass применить /24

## <a name="vpn-client-cannot-access-network-file-shares"></a>VPN-клиент не может получить доступ к сетевым файловым ресурсам

### <a name="symptom"></a>Симптом

Виртуальная сеть Azure toohello подключен клиент VPN Hello. Однако hello клиента нет доступа к сетевым папкам.

### <a name="cause"></a>Причина:

Hello протокол SMB используется для общий доступ к файлам. При инициации подключения hello hello VPN-клиент добавляет учетные данные сеанса hello и происходит сбой hello. После установления соединения hello hello клиента принудительного toouse hello кэширование учетных данных для проверки подлинности Kerberos. Этот процесс инициирует запросы toohello центр распространения ключей (контроллер домена) tooget маркер. Так как из Интернета hello подключается клиент hello, может оказаться контроллер домена может tooreach hello. Таким образом клиент hello не может перенести нагрузку с Kerberos tooNTLM. 

Hello только время, этот клиент hello предлагается для учетных данных — когда в ней имеется действительный сертификат (с использованием SAN = имя участника-пользователя) выдан hello toowhich домена, он присоединен. Hello клиент также должен быть физически подключен toohello доменной сети. В этом случае клиент hello пытается toouse hello сертификата и достигает toohello контроллера домена. Затем hello центр распространения ключей возвращает ошибку «KDC_ERR_C_PRINCIPAL_UNKNOWN». Клиент Hello — Принудительная toofail через tooNTLM. 

### <a name="solution"></a>Решение

toowork проблемы hello отключить hello кэширование учетных данных домена из hello следующий подраздел реестра: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>Не удается найти hello точка сеть VPN-подключения в Windows после переустановки hello VPN-клиента

### <a name="symptom"></a>Симптом

Удалить hello точка сеть VPN-подключения, а затем переустановить hello VPN-клиента. В этом случае hello VPN-подключение не настроен успешно. Вы не видите hello VPN-подключение в hello **сетевые подключения** параметров в Windows.

### <a name="solution"></a>Решение

проблема tooresolve hello, delete hello старого VPN файлах конфигурации клиента из **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, а затем снова запустите установщик клиента VPN hello.
