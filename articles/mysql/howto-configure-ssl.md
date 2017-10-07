---
title: "toosecurely подключения SSL aaaConfigure подключения tooAzure базы данных MySQL | Документы Microsoft"
description: "Инструкции по Настройка базы данных Azure для MySQL и связанные с ними приложения toocorrectly tooproperly использовать подключения SSL"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>Настройка SSL подключение в toosecurely вашего приложения подключения tooAzure базы данных MySQL
База данных Azure для MySQL поддерживает подключение базы данных Azure для MySQL server tooclient приложений, использующих протокол Secure Sockets Layer (SSL). Принудительное SSL-подключений между сервером базы данных и клиентские приложения помогает защитить от атак «злоумышленник в середине hello» путем шифрования hello потока данных между сервером hello и приложения.

## <a name="step-1-obtain-ssl-certificate"></a>Шаг 1. Получение SSL-сертификата
Загрузить сертификат, необходимый toocommunicate hello по протоколу SSL с базой данных Azure для сервера MySQL из [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) и сохраните локального tooyour файл сертификата hello диск (с помощью этого учебника мы для использования c:\ssl).
**Для Microsoft Internet Explorer и Microsoft Edge:** после завершения загрузки hello переименовать tooBaltimoreCyberTrustRoot.crt.pem сертификат hello.

## <a name="step-2-bind-ssl"></a>Шаг 2. Привязка SSL
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>Подключение tooserver помощью hello MySQL Workbench по протоколу SSL
Настройте tooconnect MySQL Workbench безопасно по протоколу SSL. Перейдите toohello **SSL** hello MySQL Workbench на hello диалоговое окно "Настройка нового подключения" на вкладке. Введите расположение файла hello hello **BaltimoreCyberTrustRoot.crt.pem** в hello **файл ЦС SSL:** поля.
![Сохранение настроенного элемента](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>Подключение tooserver помощью hello MySQL CLI по протоколу SSL
С помощью интерфейса командной строки MySQL hello, выполните следующую команду hello:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>Шаг 3. Применение SSL-соединений в Azure 
### <a name="using-azure-portal"></a>Использование портала Azure
С помощью hello портал Azure, посетите вашей базы данных Azure для MySQL server и нажмите кнопку **безопасности подключения**. Используйте tooenable кнопка переключателя hello или отключите hello **применять SSL-соединение** параметр. Нажмите кнопку **Сохранить**. Корпорация Майкрософт рекомендует включить tooalways **применять SSL-соединение** для повышения безопасности.
![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Использование Azure CLI
Можно включить или отключить hello **применения ssl** параметра с помощью значения Enabled или Disabled соответственно в Azure CLI.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Шаг 4. Проверка SSL-соединения
Выполнение hello mysql **состояние** подключение с использованием SSL сервер MySQL tooyour tooverify команды:
```dos
mysql> status
```
Убедитесь, что hello соединение зашифровано, просмотрев hello выходных данных. Должно отображаться следующее: **SSL: Cipher in use is AES256-SHA** (SSL: используется шифр AES256-SHA). 

## <a name="sample-code"></a>Пример кода
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>Дальнейшие действия
Сведения о вариантах подключения приложений см. в статье [Библиотеки подключений для базы данных Azure для MySQL](concepts-connection-libraries.md).
