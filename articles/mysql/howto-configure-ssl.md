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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="3a546-103">Настройка SSL подключение в toosecurely вашего приложения подключения tooAzure базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="3a546-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="3a546-104">База данных Azure для MySQL поддерживает подключение базы данных Azure для MySQL server tooclient приложений, использующих протокол Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="3a546-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="3a546-105">Принудительное SSL-подключений между сервером базы данных и клиентские приложения помогает защитить от атак «злоумышленник в середине hello» путем шифрования hello потока данных между сервером hello и приложения.</span><span class="sxs-lookup"><span data-stu-id="3a546-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="3a546-106">Шаг 1. Получение SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="3a546-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="3a546-107">Загрузить сертификат, необходимый toocommunicate hello по протоколу SSL с базой данных Azure для сервера MySQL из [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) и сохраните локального tooyour файл сертификата hello диск (с помощью этого учебника мы для использования c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="3a546-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="3a546-108">**Для Microsoft Internet Explorer и Microsoft Edge:** после завершения загрузки hello переименовать tooBaltimoreCyberTrustRoot.crt.pem сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="3a546-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="3a546-109">Шаг 2. Привязка SSL</span><span class="sxs-lookup"><span data-stu-id="3a546-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="3a546-110">Подключение tooserver помощью hello MySQL Workbench по протоколу SSL</span><span class="sxs-lookup"><span data-stu-id="3a546-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="3a546-111">Настройте tooconnect MySQL Workbench безопасно по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="3a546-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="3a546-112">Перейдите toohello **SSL** hello MySQL Workbench на hello диалоговое окно "Настройка нового подключения" на вкладке.</span><span class="sxs-lookup"><span data-stu-id="3a546-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="3a546-113">Введите расположение файла hello hello **BaltimoreCyberTrustRoot.crt.pem** в hello **файл ЦС SSL:** поля.</span><span class="sxs-lookup"><span data-stu-id="3a546-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="3a546-114">![Сохранение настроенного элемента](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="3a546-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="3a546-115">Подключение tooserver помощью hello MySQL CLI по протоколу SSL</span><span class="sxs-lookup"><span data-stu-id="3a546-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="3a546-116">С помощью интерфейса командной строки MySQL hello, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="3a546-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="3a546-117">Шаг 3. Применение SSL-соединений в Azure</span><span class="sxs-lookup"><span data-stu-id="3a546-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="3a546-118">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="3a546-118">Using Azure portal</span></span>
<span data-ttu-id="3a546-119">С помощью hello портал Azure, посетите вашей базы данных Azure для MySQL server и нажмите кнопку **безопасности подключения**.</span><span class="sxs-lookup"><span data-stu-id="3a546-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="3a546-120">Используйте tooenable кнопка переключателя hello или отключите hello **применять SSL-соединение** параметр.</span><span class="sxs-lookup"><span data-stu-id="3a546-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="3a546-121">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3a546-121">Then click **Save**.</span></span> <span data-ttu-id="3a546-122">Корпорация Майкрософт рекомендует включить tooalways **применять SSL-соединение** для повышения безопасности.</span><span class="sxs-lookup"><span data-stu-id="3a546-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="3a546-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="3a546-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="3a546-124">Использование Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3a546-124">Using Azure CLI</span></span>
<span data-ttu-id="3a546-125">Можно включить или отключить hello **применения ssl** параметра с помощью значения Enabled или Disabled соответственно в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3a546-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="3a546-126">Шаг 4. Проверка SSL-соединения</span><span class="sxs-lookup"><span data-stu-id="3a546-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="3a546-127">Выполнение hello mysql **состояние** подключение с использованием SSL сервер MySQL tooyour tooverify команды:</span><span class="sxs-lookup"><span data-stu-id="3a546-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="3a546-128">Убедитесь, что hello соединение зашифровано, просмотрев hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3a546-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="3a546-129">Должно отображаться следующее: **SSL: Cipher in use is AES256-SHA** (SSL: используется шифр AES256-SHA).</span><span class="sxs-lookup"><span data-stu-id="3a546-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="3a546-130">Пример кода</span><span class="sxs-lookup"><span data-stu-id="3a546-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="3a546-131">PHP</span><span class="sxs-lookup"><span data-stu-id="3a546-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="3a546-132">Python</span><span class="sxs-lookup"><span data-stu-id="3a546-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="3a546-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a546-133">Next steps</span></span>
<span data-ttu-id="3a546-134">Сведения о вариантах подключения приложений см. в статье [Библиотеки подключений для базы данных Azure для MySQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="3a546-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
