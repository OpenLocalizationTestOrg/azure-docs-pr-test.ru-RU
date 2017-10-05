---
title: "Краткое руководство. Создание базы данных Azure для сервера MySQL с помощью Azure CLI | Документация Майкрософт"
description: "В этом кратком руководстве описывается создание сервера базы данных Azure для MySQL в группе ресурсов Azure с помощью Azure CLI."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 04fc441aee7a4c8adc4f02d5e51b2d9e64400f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="650e3-103">Создание сервера базы данных Azure для MySQL с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="650e3-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="650e3-104">В этом кратком руководстве описывается создание сервера базы данных Azure для MySQL в группе ресурсов Azure с помощью Azure CLI за 5 минут.</span><span class="sxs-lookup"><span data-stu-id="650e3-104">This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="650e3-105">Azure CLI используется для создания ресурсов Azure и управления ими из командной строки или с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="650e3-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span>

<span data-ttu-id="650e3-106">Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="650e3-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="650e3-107">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="650e3-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="650e3-108">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="650e3-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="650e3-109">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="650e3-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="650e3-110">Если вы используете несколько подписок, выберите соответствующую подписку, в которой находится ресурс либо в которой за него взимается плата.</span><span class="sxs-lookup"><span data-stu-id="650e3-110">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="650e3-111">Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="650e3-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="650e3-112">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="650e3-112">Create a resource group</span></span>
<span data-ttu-id="650e3-113">Создайте [группу ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) с помощью команды [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="650e3-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="650e3-114">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="650e3-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="650e3-115">В следующем примере создается группа ресурсов с именем `myresourcegroup` в расположении `westus`.</span><span class="sxs-lookup"><span data-stu-id="650e3-115">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="650e3-116">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="650e3-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="650e3-117">Создайте сервер базы данных Azure для MySQL, выполнив команду **az mysql server create**.</span><span class="sxs-lookup"><span data-stu-id="650e3-117">Create an Azure Database for MySQL server with the **az mysql server create** command.</span></span> <span data-ttu-id="650e3-118">Сервер может управлять несколькими базами данных.</span><span class="sxs-lookup"><span data-stu-id="650e3-118">A server can manage multiple databases.</span></span> <span data-ttu-id="650e3-119">Как правило, для каждого проекта и для каждого пользователя используется отдельная база данных.</span><span class="sxs-lookup"><span data-stu-id="650e3-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="650e3-120">В следующем примере в группе ресурсов `myresourcegroup` создается сервер базы данных Azure для MySQL с именем `myserver4demo`, который расположен в `westus`.</span><span class="sxs-lookup"><span data-stu-id="650e3-120">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="650e3-121">Для сервера указано имя администратора для входа `myadmin` и пароль `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="650e3-121">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="650e3-122">Он создается с уровнем производительности **Базовый** и **50** единицами вычислений, которые совместно используются всеми базами данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="650e3-122">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="650e3-123">В зависимости от потребностей приложения можно увеличить или уменьшить масштаб вычислительных ресурсов и ресурсов хранилища.</span><span class="sxs-lookup"><span data-stu-id="650e3-123">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="650e3-124">Настройка правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="650e3-124">Configure firewall rule</span></span>
<span data-ttu-id="650e3-125">Создайте правило брандмауэра на уровне сервера базы данных Azure для MySQL, выполнив команду **az mysql server firewall-rule create**.</span><span class="sxs-lookup"><span data-stu-id="650e3-125">Create an Azure Database for MySQL server-level firewall rule using the **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="650e3-126">Правило брандмауэра на уровне сервера позволяет внешним приложениям, таким как программа командной строки **mysql.exe** или MySQL Workbench, подключаться к серверу через брандмауэр службы Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="650e3-126">A server-level firewall rule allows an external application, such as the **mysql.exe** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="650e3-127">В примере ниже показано создание правила брандмауэра для предопределенного диапазона адресов, который в этом примере представляет наиболее полный диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="650e3-127">The following example creates a firewall rule for a predefined address range, which in this example is the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="650e3-128">Настройка параметров SSL</span><span class="sxs-lookup"><span data-stu-id="650e3-128">Configure SSL settings</span></span>
<span data-ttu-id="650e3-129">По умолчанию между сервером и клиентскими приложениями применяется SSL-соединение.</span><span class="sxs-lookup"><span data-stu-id="650e3-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="650e3-130">Это гарантирует безопасное перемещение данных за счет шифрования потока данных через Интернет.</span><span class="sxs-lookup"><span data-stu-id="650e3-130">This ensures security of "in-motion" data by encrypting the data stream over the internet.</span></span>  <span data-ttu-id="650e3-131">Чтобы упростить работу с этим руководством, необходимо отключить SSL-соединения для вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="650e3-131">To make this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="650e3-132">Мы не рекомендуем так делать для рабочих серверов.</span><span class="sxs-lookup"><span data-stu-id="650e3-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="650e3-133">Дополнительные сведения см. в статье [Настройка SSL-подключений в приложении для безопасного подключения к базе данных Azure для MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="650e3-133">For more information, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="650e3-134">В следующем примере показано, как отключить SSL-соединение на сервере MySQL.</span><span class="sxs-lookup"><span data-stu-id="650e3-134">The following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a><span data-ttu-id="650e3-135">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="650e3-135">Get the connection information</span></span>

<span data-ttu-id="650e3-136">Чтобы подключиться к серверу, необходимо указать сведения об узле и учетные данные для доступа.</span><span class="sxs-lookup"><span data-stu-id="650e3-136">To connect to your server, you need to provide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="650e3-137">Результаты выводятся в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="650e3-137">The result is in JSON format.</span></span> <span data-ttu-id="650e3-138">Запишите значения **fullyQualifiedDomainName** и **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="650e3-138">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a><span data-ttu-id="650e3-139">Подключение к серверу с помощью программы командной строки mysql.exe</span><span class="sxs-lookup"><span data-stu-id="650e3-139">Connect to the server using the mysql.exe command-line tool</span></span>
<span data-ttu-id="650e3-140">Подключитесь к серверу с помощью программы командной строки **mysql.exe**.</span><span class="sxs-lookup"><span data-stu-id="650e3-140">Connect to your server using the **mysql.exe** command-line tool.</span></span> <span data-ttu-id="650e3-141">MySQL можно скачать [здесь](https://dev.mysql.com/downloads/) и установить на компьютер.</span><span class="sxs-lookup"><span data-stu-id="650e3-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="650e3-142">Вместо этого можно также нажать кнопку **Попробуйте!** в примерах кода или кнопку `>_` на панели инструментов в правом верхнем углу портала Azure и запустить **Azure Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="650e3-142">Instead you may also click the **Try It** button on code samples, or the  `>_` button from the upper right toolbar in the Azure portal, and launch the **Azure Cloud Shell**.</span></span>

<span data-ttu-id="650e3-143">Введите следующие команды.</span><span class="sxs-lookup"><span data-stu-id="650e3-143">Type the next commands:</span></span> 

1. <span data-ttu-id="650e3-144">Подключитесь к серверу с помощью программы командной строки **mysql**:</span><span class="sxs-lookup"><span data-stu-id="650e3-144">Connect to the server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="650e3-145">Просмотрите состояние сервера:</span><span class="sxs-lookup"><span data-stu-id="650e3-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="650e3-146">Если все работает правильно, в программе командной строки должен отобразиться следующий текст:</span><span class="sxs-lookup"><span data-stu-id="650e3-146">If everything goes well, the command-line tool should output the following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="650e3-147">Дополнительные команды см. в [разделе 4.5.1 справочного руководства по MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="650e3-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a><span data-ttu-id="650e3-148">Подключение к серверу с помощью инструмента графического пользовательского интерфейса MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="650e3-148">Connect to the server using the MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="650e3-149">Запустите приложение MySQL Workbench на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="650e3-149">Launch the MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="650e3-150">Скачать и установить MySQL Workbench вы можете [здесь](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="650e3-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="650e3-151">В диалоговом окне **настройки нового подключения** на вкладке **Параметры** введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="650e3-151">In the **Setup New Connection** dialog box, enter the following information on **Parameters** tab:</span></span>

   ![Настройка нового подключения](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="650e3-153">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="650e3-153">**Setting**</span></span> | <span data-ttu-id="650e3-154">**Рекомендуемое значение**</span><span class="sxs-lookup"><span data-stu-id="650e3-154">**Suggested Value**</span></span> | <span data-ttu-id="650e3-155">**Описание**</span><span class="sxs-lookup"><span data-stu-id="650e3-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="650e3-156">Имя подключения</span><span class="sxs-lookup"><span data-stu-id="650e3-156">Connection Name</span></span> | <span data-ttu-id="650e3-157">Мое подключение</span><span class="sxs-lookup"><span data-stu-id="650e3-157">My Connection</span></span> | <span data-ttu-id="650e3-158">Укажите любую метку для этого подключения.</span><span class="sxs-lookup"><span data-stu-id="650e3-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="650e3-159">Способ подключения</span><span class="sxs-lookup"><span data-stu-id="650e3-159">Connection Method</span></span> | <span data-ttu-id="650e3-160">Выберите стандартный способ (по протоколу TCP/IP).</span><span class="sxs-lookup"><span data-stu-id="650e3-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="650e3-161">Используйте протокол TCP/IP для подключения к базе данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="650e3-161">Use TCP/IP protocol to connect to Azure Database for MySQL></span></span> |
| <span data-ttu-id="650e3-162">имя узла;</span><span class="sxs-lookup"><span data-stu-id="650e3-162">Hostname</span></span> | <span data-ttu-id="650e3-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="650e3-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="650e3-164">Имя сервера, которое вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="650e3-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="650e3-165">Порт</span><span class="sxs-lookup"><span data-stu-id="650e3-165">Port</span></span> | <span data-ttu-id="650e3-166">3306</span><span class="sxs-lookup"><span data-stu-id="650e3-166">3306</span></span> | <span data-ttu-id="650e3-167">Для MySQL используется порт по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="650e3-167">The default port for MySQL is used.</span></span> |
| <span data-ttu-id="650e3-168">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="650e3-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="650e3-169">Имя для входа администратора сервера, которое вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="650e3-169">The server admin login you previously noted.</span></span> |
| <span data-ttu-id="650e3-170">Пароль</span><span class="sxs-lookup"><span data-stu-id="650e3-170">Password</span></span> | **** | <span data-ttu-id="650e3-171">Используйте пароль учетной записи администратора, настроенный ранее.</span><span class="sxs-lookup"><span data-stu-id="650e3-171">Use the admin account password you configured earlier.</span></span> |

<span data-ttu-id="650e3-172">Щелкните **Проверить подключение**, чтобы проверить, все ли параметры верно настроены.</span><span class="sxs-lookup"><span data-stu-id="650e3-172">Click **Test Connection** to test if all parameters are correctly configured.</span></span>
<span data-ttu-id="650e3-173">Теперь можно щелкнуть только что созданное подключение, чтобы успешно подключиться к серверу.</span><span class="sxs-lookup"><span data-stu-id="650e3-173">Now, you can click the connection to successfully connect to the server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="650e3-174">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="650e3-174">Clean up resources</span></span>
<span data-ttu-id="650e3-175">Если эти ресурсы не требуются для изучения другого руководства, вы можете их удалить. Для этого выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="650e3-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing the following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="650e3-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="650e3-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="650e3-177">Проектирование первой базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="650e3-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
