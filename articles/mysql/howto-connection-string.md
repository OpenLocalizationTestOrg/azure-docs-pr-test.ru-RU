---
title: "Подключение приложений к базе данных Azure для MySQL | Документация Майкрософт"
description: "В этом документе перечислены все строки подключения, которые в настоящее время поддерживаются для подключения приложений к базе данных Azure для MySQL, включая ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python и Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 09/15/2017
ms.openlocfilehash: c9fe0a892bd5e81d2b33987b6ca55ec753550a01
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a>Как подключить приложения к базе данных Azure для MySQL
В этой статье перечислены типы строк подключения, поддерживаемые базой данных Azure для MySQL, а также шаблоны и примеры. Строка подключения может содержать различные параметры и настройки.

- Сведения о получении сертификата см. в статье [Настройка SSL-подключений в приложении для безопасного подключения к базе данных Azure для MySQL](./howto-configure-ssl.md).
- {ваш_узел} = <servername>.mysql.database.azure.com
- {ваш_пользователь}@{имя_сервера} = формат userID для правильной аутентификации.  Если использовать только userID, аутентификация завершится ошибкой.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

В этом примере имя сервера — `myserver4demo`, имя базы данных — `wpdb`, имя пользователя — `WPAdmin`, а пароль — `mypassword!2`. В результате строка подключения будет следующей:

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>Ruby
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a>Получение сведений о строке подключения на портале Azure
На [портале Azure](https://portal.azure.com) перейдите к серверу базы данных Azure для MySQL и щелкните **Строки подключения**, чтобы получить список строк для своего экземпляра. ![Область строк подключения на портале Azure](./media/howto-connection-strings/connection-strings-on-portal.png)

Строка содержит такие сведения, как драйвер, сервер и другие параметры подключения к базе данных. Измените эти примеры, чтобы использовать собственные параметры, такие как имя базы данных, пароль и т. д. Тогда вы сможете использовать эту строку для подключения к серверу из своего кода и приложений.

## <a name="next-steps"></a>Дальнейшие действия
- Дополнительные сведения о библиотеках подключений см. в статье [Библиотеки подключений для базы данных Azure для MySQL](./concepts-connection-libraries.md).
