---
title: "Конфигурация безопасности слияния aaaSplit | Документы Microsoft"
description: "Настройка сертификатов x409 для шифрования"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Настройка параметров безопасности для службы разделения и объединения
Служба разделения или слияния toouse hello, необходимо правильно настроить безопасность. Hello служба является частью hello возможность гибкого масштабирования базы данных SQL Microsoft Azure. Дополнительные сведения см. в [руководстве по эластичному масштабированию службы разбиения и объединения](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Настройка сертификатов
Сертификаты настраиваются двумя способами. 

1. [hello tooConfigure SSL-сертификата](#to-configure-the-ssl-certificate)
2. [tooConfigure сертификаты клиента](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>сертификаты tooobtain
Сертификаты можно получить из открытых центров сертификации (ЦС) или hello [службы сертификатов Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Это предпочтительный hello методы tooobtain сертификаты.

Если эти варианты недоступны, можно создавать **самозаверяющие сертификаты**.

## <a name="tools-toogenerate-certificates"></a>Средства toogenerate сертификатов
* [makecert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>средства toorun hello
* Сведения о запуске инструментов из командной строки разработчика для Visual Studio см. в статье [Командная строка разработчика для Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx). 
  
    Если ПО установлено, перейдите к:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Получить hello WDK из [Windows 8.1: скачивание комплектов и средств](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>tooconfigure hello SSL-сертификата
SSL-сертификат является обязательным tooencrypt hello связи и проверить подлинность сервера hello. Выберите наиболее применимым из трех сценариев hello ниже hello и выполните все шаги:

### <a name="create-a-new-self-signed-certificate"></a>Создание самозаверяющего сертификата
1. [Создание самозаверяющего сертификата](#create-a-self-signed-certificate)
2. [Создание PFX-файла для самозаверяющего SSL-сертификата](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Отправка tooCloud SSL-сертификата службы](#upload-ssl-certificate-to-cloud-service)
4. [Обновление SSL-сертификата в файле конфигурации службы](#update-ssl-certificate-in-service-configuration-file)
5. [Импорт центра сертификации SSL](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>сохранить существующий сертификат из сертификата hello toouse
1. [Экспорт SSL-сертификата из хранилища сертификатов](#export-ssl-certificate-from-certificate-store)
2. [Отправка tooCloud SSL-сертификата службы](#upload-ssl-certificate-to-cloud-service)
3. [Обновление SSL-сертификата в файле конфигурации службы](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse существующего сертификата в PFX-файла
1. [Отправка tooCloud SSL-сертификата службы](#upload-ssl-certificate-to-cloud-service)
2. [Обновление SSL-сертификата в файле конфигурации службы](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>сертификаты клиентов tooconfigure
В порядке tooauthenticate запросов toohello службы требуются клиентские сертификаты. Выберите наиболее применимым из трех сценариев hello ниже hello и выполните все шаги:

### <a name="turn-off-client-certificates"></a>Отключение сертификатов клиента
1. [Отключение аутентификации на основе сертификата клиента](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Выдача новых самозаверяющих сертификатов клиента
1. [Создание центра самозаверяющей сертификации](#create-a-self-signed-certification-authority)
2. [Загрузить сертификат ЦС tooCloud службы](#upload-ca-certificate-to-cloud-service)
3. [Обновление сертификата ЦС в файле конфигурации службы](#update-ca-certificate-in-service-configuration-file)
4. [Выдача сертификатов клиентов](#issue-client-certificates)
5. [Создание PFX-файлов для сертификатов клиента](#create-pfx-files-for-client-certificates)
6. [Импорт сертификата клиента](#Import-Client-Certificate)
7. [Копирование отпечатков сертификатов клиента](#copy-client-certificate-thumbprints)
8. [Настройка клиентов допускается в hello файл конфигурации службы](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Использование существующих сертификатов клиентов
1. [Find CA Public Key](#find-ca-public-key)
2. [Загрузить сертификат ЦС tooCloud службы](#Upload-CA-certificate-to-cloud-service)
3. [Обновление сертификата ЦС в файле конфигурации службы](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Копирование отпечатков сертификатов клиента](#Copy-Client-Certificate-Thumbprints)
5. [Настройка клиентов допускается в hello файл конфигурации службы](#configure-allowed-clients-in-the-service-configuration-file)
6. [Настройка проверки отзыва сертификата клиента](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Разрешенные IP-адреса
Конечные точки службы toohello доступа может быть ограниченным toospecific диапазоны IP-адресов.

## <a name="tooconfigure-encryption-for-hello-store"></a>шифрование tooconfigure hello хранилища
Сертификат — hello tooencrypt необходимые учетные данные, которые хранятся в хранилище метаданных hello. Выберите наиболее применимым из трех сценариев hello ниже hello и выполните все шаги:

### <a name="use-a-new-self-signed-certificate"></a>Использование нового самозаверяющего сертификата
1. [Создание самозаверяющего сертификата](#create-a-self-signed-certificate)
2. [Создание PFX-файла для самозаверяющего сертификата шифрования](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Отправить сертификат шифрования tooCloud службы](#upload-encryption-certificate-to-cloud-service)
4. [Обновление сертификата шифрования в файле конфигурации службы](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Использовать существующий сертификат из хранилища сертификатов hello
1. [Экспорт сертификата шифрования из хранилища сертификатов](#export-encryption-certificate-from-certificate-store)
2. [Отправить сертификат шифрования tooCloud службы](#upload-encryption-certificate-to-cloud-service)
3. [Обновление сертификата шифрования в файле конфигурации службы](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Использование существующего сертификата в PFX-файле
1. [Отправить сертификат шифрования tooCloud службы](#upload-encryption-certificate-to-cloud-service)
2. [Обновление сертификата шифрования в файле конфигурации службы](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>Конфигурация по умолчанию Hello
Конфигурация по умолчанию Hello запрещает все конечной точки HTTP toohello доступа. Это hello, рекомендуется, поскольку конечные точки toothese запросы hello может содержать конфиденциальные сведения, такие как учетные данные базы данных.
Конфигурация по умолчанию Hello позволяет конечной точки HTTPS все toohello доступа. Этот параметр в дальнейшем может быть ограничен.

### <a name="changing-hello-configuration"></a>Изменение конфигурации hello
Hello группы правил управления доступом, применяемые tooand конечной точки настраиваются в hello  **<EndpointAcls>**  раздела hello **файла конфигурации службы**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

Hello правила в группе управления доступом настраиваются в <AccessControl name=""> раздел файла конфигурации службы hello. 

Формат Hello описан в документации списки управления сетевым доступом.
Например, tooallow только IP-адреса в hello 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS конечная точка диапазона, hello правила может выглядеть следующим образом:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Предотвращение отказа в обслуживании
Существует два разных механизма поддерживается toodetect и предотвратить атаки отказа в обслуживании:

* Ограничение количества одновременных запросов на удаленный узел (по умолчанию отключено)
* Ограничение частоты доступа в расчете на удаленный узел (включено по умолчанию)

Они основаны на функции hello в динамических IP-безопасности в службах IIS. При изменении этой конфигурации Учтите, что hello следующие факторы:

* поведение Hello прокси-серверы и устройства преобразования сетевых адресов над сведениями о hello удаленного узла
* Ресурс tooany каждого запроса в веб-роли hello считается (например загрузки скриптов, изображения, и т.д.)

## <a name="restricting-number-of-concurrent-accesses"></a>Ограничение числа одновременных обращений
Привет, настройки этого поведения следующие значения.

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Измените DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable защиту.

## <a name="restricting-rate-of-access"></a>Ограничение частоты доступа
Привет, настройки этого поведения следующие значения.

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Настройка tooa ответа hello отклонил запрос
Hello следующий параметр настраивает hello ответа tooa отклонил запрос:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
См. документацию toohello динамических IP-безопасности в службах IIS для других поддерживаемых значений.

## <a name="operations-for-configuring-service-certificates"></a>Операции настройки службы сертификатов
Этот раздел предназначен только для справки. Выполните этапы настройки hello, описанные в.

* Настройка SSL-сертификата hello
* Настройка сертификатов клиентов

## <a name="create-a-self-signed-certificate"></a>Создание самозаверяющего сертификата
Выполните:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* URL-адрес службы - n с hello. Поддерживаются подстановочные знаки ("CN=*.cloudapp.net") и альтернативные имена ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").
* -e с датой окончания срока действия сертификата hello создать надежный пароль и укажите его при появлении запроса.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Создание PFX-файла для самозаверяющего SSL-сертификата
Выполните:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Введите пароль, а затем экспортируйте сертификат с этими параметрами.

* Да, экспортировать закрытый ключ hello
* Экспортировать все расширенные свойства.

## <a name="export-ssl-certificate-from-certificate-store"></a>Экспорт SSL-сертификата из хранилища сертификатов
* Поиск сертификата
* Выберите «Действия > Все задачи > Экспортировать…»
* Экспортируйте сертификат в PFX-файл со следующими параметрами.
  * Да, экспортировать закрытый ключ hello
  * Включить по возможности все сертификаты в путь сертификации hello * экспортировать все расширенные свойства

## <a name="upload-ssl-certificate-toocloud-service"></a>Отправить службе toocloud сертификат SSL
Отправьте сертификат с hello существующий или создан. PFX-файл с hello пары ключей SSL:

* Введите пароль hello для защиты информации о закрытом ключе hello

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Обновление SSL-сертификата в файле конфигурации службы
Обновите значения отпечатка hello hello следующий параметр в файле конфигурации службы hello с отпечатком hello hello сертификат, переданный toohello облачной службы:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>Импорт центра сертификации SSL
Выполните следующие действия в все учетной записи или компьютера, которым будет связываться со службой hello.

* Дважды щелкните значок "hello". CER-файл в проводнике Windows
* В диалоговом окне приветствия сертификат нажмите кнопку "установить сертификат"...
* Импортируйте сертификат в хранилище доверенных корневых центров сертификации приветствия

## <a name="turn-off-client-certificate-based-authentication"></a>Отключение аутентификации на основе сертификата клиента
Поддерживается только на основе сертификатов проверки подлинности клиента и его отключение позволит для конечных точек службы toohello общего доступа, если не предусмотрены другие механизмы на месте (например виртуальная сеть Microsoft Azure).

Измените toofalse этих параметров в функции hello tooturn файла конфигурации hello службы из системы:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Затем скопируйте hello же отпечатком, что hello SSL-сертификата в приветствия ЦС сертификата:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Создание центра самозаверяющей сертификации
Выполните следующие шаги toocreate tooact самозаверяющий сертификат, как центр сертификации hello:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize его

* -e с датой окончания срока действия сертификации hello

## <a name="find-ca-public-key"></a>Поиск открытого ключа ЦС
Все сертификаты клиента должен быть выдан центром сертификации, доверенным для службы hello. Найти открытого ключа toohello hello центра сертификации, выдавшего hello клиентских сертификатов, которые будут toobe для проверки подлинности в порядке tooupload его toohello облачной службы.

Если файл hello открытым ключом hello недоступен, экспортируйте его из хранилища сертификатов hello:

* Поиск сертификата
  * Найдите сертификат клиента, выданный hello же центром сертификации
* Дважды щелкните сертификат hello.
* Перейдите на вкладку путь сертификации hello в диалоговом окне приветствия сертификата.
* Дважды щелкните запись ЦС hello в пути hello.
* Запишите свойства сертификата hello.
* Закрыть hello **сертификат** диалогового окна.
* Поиск сертификата
  * Поиск hello ЦС, указанным выше.
* Выберите «Действия > Все задачи > Экспортировать…»
* Экспортируйте сертификат в .CER с этими параметрами:
  * **Нет, не экспортировать закрытый ключ hello**
  * Включить по возможности все сертификаты в путь сертификации hello.
  * Экспортировать все расширенные свойства.

## <a name="upload-ca-certificate-toocloud-service"></a>Отправка службы toocloud сертификата ЦС
Отправьте сертификат с hello существующий или создан. CER-файл с помощью открытого ключа ЦС hello.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Обновление сертификата ЦС в файле конфигурации службы
Обновите значения отпечатка hello hello следующий параметр в файле конфигурации службы hello с отпечатком hello hello сертификат, переданный toohello облачной службы:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Обновите значение hello hello после установки с hello же отпечаток:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Выдача сертификатов клиентов
Каждая служба hello отдельных авторизованным tooaccess должен иметь клиентского сертификата, выданного для his/hers монопольного использования и следует выбрать his/hers владеет закрытым ключом tooprotect надежный пароль. 

следующие шаги Hello должен выполняться в hello же компьютере, где самоподписанный сертификат ЦС hello был автоматически и хранится:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Настройка.

* -n с Идентификатором toohello клиента, который будет проходить проверку подлинности с помощью этого сертификата
* -e с датой окончания срока действия сертификата hello
* MyID.pvk и MyID.cer с уникальными именами файлов для этого сертификата клиента

Эта команда предложит ввести пароль toobe и затем использовать его один раз. Используйте надежный пароль.

## <a name="create-pfx-files-for-client-certificates"></a>Создание PFX-файлов для сертификатов клиента
Для каждого созданного сертификата клиента выполните следующее.

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Настройка.

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Введите пароль, а затем экспортируйте сертификат с этими параметрами.

* Да, экспортировать закрытый ключ hello
* Экспортировать все расширенные свойства.
* toowhom отдельных Hello, этот сертификат необходимо выбрать пароль экспорта hello

## <a name="import-client-certificate"></a>Импорт сертификата клиента
Каждого пользователя, для которого была выполнена клиентский сертификат следует импортировать пару ключей hello в hello машины он будет использоваться toocommunicate со службой hello:

* Дважды щелкните значок "hello". PFX-файла в проводнике Windows
* Импортируйте сертификат в личном хранилище с по крайней мере этот параметр hello:
  * Включить все расширенные свойства проверки

## <a name="copy-client-certificate-thumbprints"></a>Копирование отпечатков сертификатов клиента
Каждого пользователя, которому выдан сертификат клиента необходимо выполнить следующие действия в порядке tooobtain hello отпечаток his/hers сертификат, который будет добавлен файл конфигурации службы toohello:

* Запустите certmgr.exe
* Выберите вкладку личные hello
* Дважды щелкните toobe, используемый для проверки подлинности сертификата клиента hello
* В диалоговом окне сертификата hello, которое открывается перейдите на вкладку сведения hello
* Убедитесь, что в разделе "Показать" выбран вариант "Все"
* Выберите hello поле с именем отпечаток в списке hello
* Скопируйте значение hello отпечаток hello ** удалить неотображаемых символов Юникода перед первой цифры hello ** удалите все пробелы

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Настройка клиентов разрешено в файле конфигурации службы hello
Обновите значение hello hello следующий параметр в файле конфигурации службы hello с запятыми список hello отпечатки сертификатов клиента hello допускается toohello службы доступа к:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Настройка проверки отзыва сертификата клиента
по умолчанию Hello не проверяет с hello центра сертификации для проверки состояния отзыва сертификата клиента. проверяет tooturn на hello, если hello центр сертификации, выдавший сертификаты клиента hello, который поддерживает такие проверки, измените следующий параметр с одним из значений hello, определенные в hello перечисления X509RevocationMode hello.

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Создание PFX-файла для самозаверяющих сертификатов шифрования
Для сертификата шифрования выполните следующую команду:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Настройка.

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Введите пароль, а затем экспортируйте сертификат с этими параметрами.

* Да, экспортировать закрытый ключ hello
* Экспортировать все расширенные свойства.
* Hello пароль будет нужен при передаче hello сертификат toohello облачной службы.

## <a name="export-encryption-certificate-from-certificate-store"></a>Экспорт сертификата шифрования из хранилища сертификатов
* Поиск сертификата
* Выберите «Действия > Все задачи > Экспортировать…»
* Экспортируйте сертификат в PFX-файл со следующими параметрами. 
  * Да, экспортировать закрытый ключ hello
  * Включить по возможности все сертификаты в путь сертификации hello 
* Экспортировать все расширенные свойства.

## <a name="upload-encryption-certificate-toocloud-service"></a>Служба toocloud сертификат шифрования отправки
Отправьте сертификат с hello существующий или создан. PFX-файл с hello пару ключей шифрования:

* Введите пароль hello для защиты информации о закрытом ключе hello

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Обновление сертификата шифрования в файле конфигурации службы
Обновите значения отпечатка hello hello следующие параметры в файле конфигурации службы hello с отпечатком hello hello сертификат, переданный toohello облачной службы:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Стандартные операции сертификата
* Настройка SSL-сертификата hello
* Настройка сертификатов клиентов

## <a name="find-certificate"></a>Поиск сертификата
Выполните следующие действия.

1. Запустите mmc.exe.
2. Файл -> Добавить/удалить оснастку...
3. Выберите **Сертификаты**.
4. Щелкните **Добавить**.
5. Выберите расположение хранилища сертификатов hello.
6. Нажмите кнопку **Готово**
7. Нажмите кнопку **ОК**.
8. Разверните узел **Сертификаты**.
9. Разверните узел хранилища сертификатов hello.
10. Разверните hello сертификат дочерний узел.
11. Выберите сертификат в списке hello.

## <a name="export-certificate"></a>Экспорт сертификата
В hello **мастера экспорта сертификатов**:

1. Щелкните **Далее**.
2. Выберите **Да**, затем **экспорта hello закрытый ключ**.
3. Щелкните **Далее**.
4. Выберите формат файла hello нужный результат.
5. Проверьте параметры требуемого hello.
6. Проверьте **Пароль**.
7. Введите надежный пароль и подтвердите его.
8. Щелкните **Далее**.
9. Введите или выберите имя файла, где toostore hello сертификата (использование. Расширение PFX).
10. Щелкните **Далее**.
11. Нажмите кнопку **Готово**
12. Нажмите кнопку **ОК**.

## <a name="import-certificate"></a>Импорт сертификата
В окне приветствия мастера импорта сертификатов:

1. Выберите расположение хранилища hello.
   
   * Выберите **текущего пользователя** если только для процессов, выполняемых в рамках текущего пользователя будет доступ к службе hello
   * Выберите **локального компьютера** Если другие процессы на этом компьютере будет получить доступ к службе hello
2. Щелкните **Далее**.
3. Если импорт из файла Проверьте путь к файлу hello.
4. При импорте .PFX-файла:
   1. Введите пароль hello, защищающий закрытый ключ hello
   2. Выберите параметры импорта
5. Выберите «Место», сертификаты в следующие хранилища hello
6. Щелкните **Обзор**.
7. Выберите нужное хранилище hello.
8. Нажмите кнопку **Готово**
   
   * Если вы выбрали hello хранилище доверенных корневых центров сертификации, щелкните **Да**.
9. Нажмите кнопку **ОК** во всех диалоговых окнах.

## <a name="upload-certificate"></a>Передача сертификата
В hello [портала Azure](https://portal.azure.com/)

1. Выберите **Облачные службы**.
2. Выберите облачную службу hello.
3. Hello верхнего меню **сертификаты**.
4. На нижней панели hello щелкните **отправить**.
5. Выберите файл сертификата hello.
6. Если это. PFX-ФАЙЛ, введите hello пароль для закрытого ключа hello.
7. После завершения копирования hello отпечаток сертификата из hello новую запись в списке hello.

## <a name="other-security-considerations"></a>Прочие вопросы по безопасности
Параметры SSL Hello, описанные в этом документе шифрования обмена данными между службой hello и клиентами, при использовании конечной точки HTTPS hello. Это важно, так как учетные данные для доступа к базе данных и другие конфиденциальные сведения, содержащиеся в hello связи. Обратите внимание, что служба hello сохраняется внутреннего состояния, включая учетные данные, в его внутренних таблиц в базе данных Microsoft Azure SQL hello, введенным для хранения метаданных в вашей подписке Microsoft Azure. Базы данных был определен как часть hello следующий параметр в файле конфигурации службы (. Файл CSCFG): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

Учетные данные, хранящиеся в этой базе данных, будут зашифрованы. Тем не менее рекомендуется, убедитесь, что веб- и рабочих ролей развертываний службы хранятся копии toodate и безопасно, как они имеют доступ toohello метаданных базы данных и hello сертификат, используемый для шифрования и расшифровки сохраненных учетных данных. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

