---
title: "tooAzure aaaConnect приложений базы данных MySQL | Документы Microsoft"
description: "Этот документ содержит строки подключения hello в настоящее время поддерживается для приложений tooconnect с базой данных Azure для MySQL, включая ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python и Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a><span data-ttu-id="53dd7-103">Как tooAzure tooconnect приложений базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="53dd7-103">How tooconnect applications tooAzure Database for MySQL</span></span>
<span data-ttu-id="53dd7-104">В этом документе перечислены hello подключения строковые типы, поддерживаемые базы данных Azure для MySQL, а также шаблоны и примеры.</span><span class="sxs-lookup"><span data-stu-id="53dd7-104">This document lists hello connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="53dd7-105">Строка подключения может содержать различные параметры и настройки.</span><span class="sxs-lookup"><span data-stu-id="53dd7-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="53dd7-106">сертификат tooobtain hello, в разделе [как tooconfigure SSL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="53dd7-106">tooobtain hello certificate, see [How tooconfigure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="53dd7-107">{ваш_узел} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="53dd7-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="53dd7-108">{ваш_пользователь}@{имя_сервера} = формат userID для правильной аутентификации.</span><span class="sxs-lookup"><span data-stu-id="53dd7-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="53dd7-109">Использование только hello userID вызовет toofail hello проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="53dd7-109">Using just hello userID will cause hello authentication toofail.</span></span>

## <a name="adonet"></a><span data-ttu-id="53dd7-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="53dd7-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="53dd7-111">В этом примере — имя сервера hello `myserver4demo`, имя базы данных — `wpdb`, имя пользователя — `WPAdmin`, пароль — `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="53dd7-111">In this example, hello server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="53dd7-112">Затем следует hello строка подключения:</span><span class="sxs-lookup"><span data-stu-id="53dd7-112">Then, hello connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="53dd7-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="53dd7-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="53dd7-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="53dd7-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="53dd7-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="53dd7-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="53dd7-116">PHP</span><span class="sxs-lookup"><span data-stu-id="53dd7-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="53dd7-117">Python</span><span class="sxs-lookup"><span data-stu-id="53dd7-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="53dd7-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="53dd7-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a><span data-ttu-id="53dd7-119">Получение подробных сведений о строке подключения hello из hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="53dd7-119">Get hello connection string details from hello Azure portal</span></span>
<span data-ttu-id="53dd7-120">В hello [портал Azure](https://portal.azure.com)go tooyour базы данных Azure для MySQL server и нажмите кнопку **строки подключения** tooget список строки для конкретного экземпляра: ![hello панель строки подключения в hello Портал Azure](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="53dd7-120">In hello [Azure portal](https://portal.azure.com), go tooyour Azure Database for MySQL server, and then click **Connection strings** tooget your string list for your instance: ![hello Connection strings pane in hello Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="53dd7-121">Строка Hello предоставляет такие сведения, как драйвер hello, server и других параметров подключения базы данных.</span><span class="sxs-lookup"><span data-stu-id="53dd7-121">hello string provides details such as hello driver, server, and other database connection parameters.</span></span> <span data-ttu-id="53dd7-122">Измените эти примеры, подставив собственные параметры, такие как имя базы данных, пароль и т. д.</span><span class="sxs-lookup"><span data-stu-id="53dd7-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="53dd7-123">Затем можно использовать этот сервер toohello строка tooconnect из кода и приложений.</span><span class="sxs-lookup"><span data-stu-id="53dd7-123">You can then use this string tooconnect toohello server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53dd7-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53dd7-124">Next steps</span></span>
- <span data-ttu-id="53dd7-125">Дополнительные сведения о библиотеках подключений см. в статье [Библиотеки подключений для базы данных Azure для MySQL](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="53dd7-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
