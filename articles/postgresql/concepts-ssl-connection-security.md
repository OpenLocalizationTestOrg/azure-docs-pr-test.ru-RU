---
title: "подключение SSL aaaConfigure в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "Инструкции и сведения tooconfigure базы данных Azure для PostgreSQL и связанные с ними приложения tooproperly использовать подключения SSL."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>Настройка SSL-соединения в базе данных Azure для PostgreSQL
База данных Azure для PostgreSQL является предпочтительным для подключения к toohello приложения клиента службы PostgreSQL, с помощью Secure Sockets Layer (SSL). Принудительное SSL-подключений между сервером базы данных и клиентские приложения помогает защитить от атак «злоумышленник в середине hello» путем шифрования hello потока данных между сервером hello и приложения.

По умолчанию hello службы базы данных PostgreSQL является настроенным toorequire SSL-подключение. При необходимости можно отключить для соединения tooyour базы данных службы, если клиентское приложение не поддерживает SSL подключение с помощью SSL. 

## <a name="enforcing-ssl-connections"></a>Применение SSL-соединений
Для всех баз данных Azure для подготовки в рамках hello портал Azure и CLI серверов PostgreSQL принудительное выполнение SSL-соединений включен по умолчанию. 

Аналогичным образом строки подключения, предварительно определенные в параметрах «Строки соединения» hello в области сервера в hello портал Azure включают hello необходимые параметры для общий языков tooconnect tooyour сервер баз данных с помощью протокола SSL. Hello SSL параметра различается в зависимости от соединителя hello, например «ssl = true» или «sslmode = требуют» или» sslmode = необходимые» и др..

## <a name="configure-enforcement-of-ssl"></a>Настройка применения SSL
При необходимости применение SSL-соединений можно отключить. Microsoft Azure Корпорация Майкрософт рекомендует включить tooalways **применять SSL-соединение** для повышения безопасности.

### <a name="using-hello-azure-portal"></a>С помощью портала Azure hello
Войдите в сервер базы данных Azure для PostgreSQL и щелкните **Безопасность подключения**. Используйте tooenable кнопка переключателя hello или отключите hello **применять SSL-соединение** параметр. Нажмите кнопку **Сохранить**. 

![Безопасность подключения: отключить применение SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

Приветствия можно проверить, просмотрев hello **Обзор** страницы приветствия toosee **SSL применять состояния** индикатора.

### <a name="using-azure-cli"></a>Использование Azure CLI
Можно включить или отключить hello **применения ssl** с помощью параметра `Enabled` или `Disabled` значения соответственно в Azure CLI.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>Проверка поддержки SSL-соединений в приложении или платформе
Многие распространенные платформы приложений, использующие PostgreSQL для служб базы данных, такие как Drupal и Django, по умолчанию не включают SSL при установке. Включение SSL-подключения должны выполняться после установки или с помощью приложения toohello конкретных команд CLI. Если сервер PostgreSQL вводит SSL-соединений и hello связанное приложение не настроено должным образом, приложение hello может завершиться ошибкой tooconnect tooyour базы данных сервера. Обратитесь к документации toolearn приложения как tooenable SSL-подключения.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>Приложения, требующие проверки сертификата для SSL-соединений
В некоторых случаях приложений требуется наличие файла локального сертификата, созданного из доверенных tooconnect CER-файл сертификата центра сертификации (ЦС), безопасно. См. следующие шаги tooobtain hello CER-файл hello, декодировать сертификат hello и привязать его tooyour приложения.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Загрузить файл сертификата hello hello центра сертификации (ЦС) 
Hello сертификат требуется toocommunicate по протоколу SSL с базой данных Azure для расположен сервер PostgreSQL [здесь](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt). Загрузите hello файл сертификата локально.

### <a name="download-and-install-openssl-on-your-machine"></a>Скачивание и установка OpenSSL на компьютер 
файл сертификата hello toodecode, необходимые для вашего приложения tooconnect безопасно tooyour сервера базы данных, необходимо tooinstall OpenSSL на локальном компьютере.

#### <a name="for-linux-os-x-or-unix"></a>Для Linux, OS X или Unix
библиотеки OpenSSL Hello предоставляются в исходном коде непосредственно из hello [OpenSSL Software Foundation](http://www.openssl.org). Hello следующим инструкциям tooinstall необходимые шаги hello OpenSSL на Компьютере Linux. В этой статье используется команды известные toowork на Ubuntu 12.04 и более поздних версий.

Откройте сеанс терминала и установите OpenSSL.
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Извлеките файлы hello hello пакет
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Введите каталог hello, где были извлечены файлы hello. По умолчанию это должен быть каталог, показанный ниже.

```bash
cd openssl-1.1.0e
```
Настройте OpenSSL, выполнив следующую команду hello. Если требуется hello файлов в папке отличается от /usr/local/openssl, сделайте убедиться, что следующие hello toochange соответствующим образом.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
Теперь, когда OpenSSL настроен правильно, необходимо toocompile его tooconvert свой сертификат. toocompile запуска hello следующую команду:

```bash
make
```
После завершения компиляции вы будете готовы tooinstall OpenSSL как EXE-файл, выполнив следующую команду hello:
```bash
make install
```
tooconfirm, что вы успешно установили OpenSSL в вашей системе, выполнения hello следующую команду и проверьте, что вы получаете hello toomake такие же выходные данные.

```bash
/usr/local/openssl/bin/openssl version
```
В случае успешного выполнения должны появиться следующие сообщения hello.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Для Windows
Установка OpenSSL на ПК с Windows может быть выполнена в hello следующих способов:
1. **(Рекомендуется)**  С помощью встроенных функций Bash Windows hello в Windows 10 и более поздних версий, OpenSSL устанавливается по умолчанию. Инструкции по обнаружение tooenable функциональность Bash Windows в Windows 10 [здесь](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).
2. До загрузки приложения Win32/64, предоставленные сообществом hello. Hello OpenSSL Software Foundation не предоставляют и не утверждает любого конкретного установщиков Windows, они предоставляют список доступных установщики [здесь](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>Декодируйте файл сертификата
Hello загрузить корневой ЦС, файл находится в зашифрованном виде. Используйте файл сертификата hello toodecode OpenSSL. toodo таким образом, выполните следующую команду OpenSSL:

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>Подключение с использованием проверки подлинности сертификата SSL tooAzure базы данных PostgreSQL
Теперь, когда успешно декодировать свой сертификат, вы может теперь tooyour сервера базы данных безопасное подключение по протоколу SSL. проверка сертификатов сервера tooallow, hello сертификат необходимо разместить в ~/.postgresql/root.crt hello файл в корневом каталоге пользователя hello. (В Microsoft Windows hello файл с именем % APPDATA%\postgresql\root.crt.). Hello ниже приведены инструкции по подключению для PostgreSQL tooAzure базы данных.

> [!NOTE]
> В настоящее время имеется известная проблема, если вы используете «sslmode = проверка full» в службе toohello подключение, подключение hello, будут завершаться hello следующая ошибка: _сертификат сервера для "&lt;области&gt;. Control.Database.Windows.NET» (и 7 имена) не соответствует имени узла "&lt;servername&gt;. postgres.database.azure.com»._
> Если «sslmode = проверка полный» — требуется, используйте соглашение об именовании hello server  **&lt;servername&gt;. database.windows.net** как локальное имя строки подключения. Мы планируем tooremove это ограничение в будущем hello. Соединения с использованием других [режимы SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) следует продолжить соглашение об именовании узлов hello предпочитаемый toouse  **&lt;servername&gt;. postgres.database.azure.com**.

#### <a name="using-psql-command-line-utility"></a>Использование служебной программы командной строки psql
Здравствуй, следующий пример показывает, как toosuccessfully подключения сервера tooyour PostgreSQL, с помощью программы командной строки psql hello. Используйте hello `root.crt` файл, созданный и hello `sslmode=verify-ca` или `sslmode=verify-full` параметр.

С помощью интерфейса командной строки hello PostgreSQL, выполните следующую команду hello:
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
В случае успешного выполнения появляется hello следующие выходные данные:
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a>Использование инструмента графического пользовательского интерфейса pgAdmin
Настроить tooconnect pgAdmin 4 безопасно по протоколу SSL, необходимо tooset hello `SSL mode = Verify-CA` или `SSL mode = Verify-Full` следующим образом:

![Снимок экрана pgAdmin: настройка параметра "SSL mode" (Режим SSL) на вкладке "Connection" (Подключение)](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>Дальнейшие действия
Сведения о вариантах подключения приложений см. в статье [Библиотеки подключений для базы данных Azure для PostgreSQL](concepts-connection-libraries.md).
