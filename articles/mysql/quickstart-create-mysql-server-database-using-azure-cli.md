---
title: "Краткое руководство. Создание базы данных Azure для сервера MySQL с помощью Azure CLI | Документация Майкрософт"
description: "Это краткое руководство описывает, как toouse hello Azure CLI toocreate базы данных Azure для сервера MySQL в группе ресурсов Azure."
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
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="eb631-103">Создание сервера базы данных Azure для MySQL с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eb631-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="eb631-104">Это краткое руководство описывает, как toouse hello Azure CLI toocreate базы данных Azure для сервера MySQL в группе ресурсов Azure в около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="eb631-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="eb631-105">Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="eb631-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="eb631-106">Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="eb631-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eb631-107">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eb631-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="eb631-108">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="eb631-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="eb631-109">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eb631-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="eb631-110">Если у вас несколько подписок, выберите нужную подписку hello, в котором hello ресурсов существует, или плата за.</span><span class="sxs-lookup"><span data-stu-id="eb631-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="eb631-111">Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="eb631-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="eb631-112">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="eb631-112">Create a resource group</span></span>
<span data-ttu-id="eb631-113">Создание [группы ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) с помощью hello [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="eb631-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="eb631-114">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="eb631-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="eb631-115">Hello следующий пример создает группу ресурсов с именем `myresourcegroup` в hello `westus` расположение.</span><span class="sxs-lookup"><span data-stu-id="eb631-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="eb631-116">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="eb631-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="eb631-117">Создание базы данных Azure для сервера MySQL с hello **создать сервер mysql az** команды.</span><span class="sxs-lookup"><span data-stu-id="eb631-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="eb631-118">Сервер может управлять несколькими базами данных.</span><span class="sxs-lookup"><span data-stu-id="eb631-118">A server can manage multiple databases.</span></span> <span data-ttu-id="eb631-119">Как правило, для каждого проекта и для каждого пользователя используется отдельная база данных.</span><span class="sxs-lookup"><span data-stu-id="eb631-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="eb631-120">Hello следующий пример создает базы данных Azure для MySQL server, расположенный в `westus` в группе ресурсов hello `myresourcegroup` с именем `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="eb631-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="eb631-121">Hello сервер имеет журнал администратора в с именем `myadmin` и пароль `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="eb631-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="eb631-122">сервер Hello создается с **основные** уровня производительности и **50** единиц, общим для всех баз данных hello в hello server вычислительных операций.</span><span class="sxs-lookup"><span data-stu-id="eb631-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="eb631-123">Вычислений и хранилища можно масштабировать вверх или вниз в зависимости от потребностей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="eb631-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="eb631-124">Настройка правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="eb631-124">Configure firewall rule</span></span>
<span data-ttu-id="eb631-125">Создание базы данных Azure для правила брандмауэра уровня сервера MySQL с помощью hello **az mysql правила брандмауэра для сервера — создание** команды.</span><span class="sxs-lookup"><span data-stu-id="eb631-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="eb631-126">Правила брандмауэра уровня сервера позволяет внешнему приложению, например hello **mysql.exe** средство командной строки или MySQL Workbench tooconnect tooyour server через брандмауэр службы MySQL в Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eb631-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="eb631-127">Hello следующий пример создает правило брандмауэра для диапазона предопределенный адрес, который в данном примере — hello все возможные диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="eb631-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="eb631-128">Настройка параметров SSL</span><span class="sxs-lookup"><span data-stu-id="eb631-128">Configure SSL settings</span></span>
<span data-ttu-id="eb631-129">По умолчанию между сервером и клиентскими приложениями применяется SSL-соединение.</span><span class="sxs-lookup"><span data-stu-id="eb631-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="eb631-130">Это гарантирует безопасность «в движения» Здравствуйте, данных с помощью шифрования hello потока данных через Интернет.</span><span class="sxs-lookup"><span data-stu-id="eb631-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="eb631-131">toomake этого быстрого запуска проще, мы отключаем соединений SSL для сервера.</span><span class="sxs-lookup"><span data-stu-id="eb631-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="eb631-132">Мы не рекомендуем так делать для рабочих серверов.</span><span class="sxs-lookup"><span data-stu-id="eb631-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="eb631-133">Дополнительные сведения см. в разделе [Настройка SSL-подключения в toosecurely вашего приложения подключения tooAzure базы данных MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="eb631-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="eb631-134">Hello следующий пример отключает применение SSL для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="eb631-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="eb631-135">Получить сведения о соединении hello</span><span class="sxs-lookup"><span data-stu-id="eb631-135">Get hello connection information</span></span>

<span data-ttu-id="eb631-136">tooconnect tooyour сервера, необходимо иметь учетные данные сведения и доступа узла tooprovide.</span><span class="sxs-lookup"><span data-stu-id="eb631-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="eb631-137">Hello получается в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="eb631-137">hello result is in JSON format.</span></span> <span data-ttu-id="eb631-138">Запишите hello **fullyQualifiedDomainName** и **Имя_входа_администратора**.</span><span class="sxs-lookup"><span data-stu-id="eb631-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="eb631-139">Подключение сервера toohello, с помощью средства командной строки mysql.exe hello</span><span class="sxs-lookup"><span data-stu-id="eb631-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="eb631-140">Подключение с помощью hello сервера tooyour **mysql.exe** средство командной строки.</span><span class="sxs-lookup"><span data-stu-id="eb631-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="eb631-141">MySQL можно скачать [здесь](https://dev.mysql.com/downloads/) и установить на компьютер.</span><span class="sxs-lookup"><span data-stu-id="eb631-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="eb631-142">Вместо этого можно также щелкнуть hello **попробовать** на образцы кода или hello `>_` кнопку hello верхней правой панели инструментов в hello портал Azure и запуска hello **оболочки облако Azure**.</span><span class="sxs-lookup"><span data-stu-id="eb631-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="eb631-143">Введите hello следующей команды:</span><span class="sxs-lookup"><span data-stu-id="eb631-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="eb631-144">Подключение с использованием сервера toohello **mysql** средство командной строки:</span><span class="sxs-lookup"><span data-stu-id="eb631-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="eb631-145">Просмотрите состояние сервера:</span><span class="sxs-lookup"><span data-stu-id="eb631-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="eb631-146">Если все пойдет хорошо, средство командной строки hello должен выводить hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="eb631-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

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
> <span data-ttu-id="eb631-147">Дополнительные команды см. в [разделе 4.5.1 справочного руководства по MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="eb631-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="eb631-148">Подключение сервера toohello, с помощью средства графического интерфейса пользователя MySQL Workbench hello</span><span class="sxs-lookup"><span data-stu-id="eb631-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="eb631-149">Запустите hello MySQL Workbench приложения на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="eb631-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="eb631-150">Скачать и установить MySQL Workbench вы можете [здесь](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="eb631-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="eb631-151">В hello **установки нового подключения** диалогового окна введите следующую информацию hello **параметры** вкладки:</span><span class="sxs-lookup"><span data-stu-id="eb631-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![Настройка нового подключения](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="eb631-153">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="eb631-153">**Setting**</span></span> | <span data-ttu-id="eb631-154">**Рекомендуемое значение**</span><span class="sxs-lookup"><span data-stu-id="eb631-154">**Suggested Value**</span></span> | <span data-ttu-id="eb631-155">**Описание**</span><span class="sxs-lookup"><span data-stu-id="eb631-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="eb631-156">Имя подключения</span><span class="sxs-lookup"><span data-stu-id="eb631-156">Connection Name</span></span> | <span data-ttu-id="eb631-157">Мое подключение</span><span class="sxs-lookup"><span data-stu-id="eb631-157">My Connection</span></span> | <span data-ttu-id="eb631-158">Укажите любую метку для этого подключения.</span><span class="sxs-lookup"><span data-stu-id="eb631-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="eb631-159">Способ подключения</span><span class="sxs-lookup"><span data-stu-id="eb631-159">Connection Method</span></span> | <span data-ttu-id="eb631-160">Выберите стандартный способ (по протоколу TCP/IP).</span><span class="sxs-lookup"><span data-stu-id="eb631-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="eb631-161">Используйте для MySQL tooAzure tooconnect протокола TCP/IP базы данных ></span><span class="sxs-lookup"><span data-stu-id="eb631-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="eb631-162">имя узла;</span><span class="sxs-lookup"><span data-stu-id="eb631-162">Hostname</span></span> | <span data-ttu-id="eb631-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="eb631-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="eb631-164">Имя сервера, которое вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="eb631-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="eb631-165">Порт</span><span class="sxs-lookup"><span data-stu-id="eb631-165">Port</span></span> | <span data-ttu-id="eb631-166">3306</span><span class="sxs-lookup"><span data-stu-id="eb631-166">3306</span></span> | <span data-ttu-id="eb631-167">используется порт по умолчанию Hello для MySQL.</span><span class="sxs-lookup"><span data-stu-id="eb631-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="eb631-168">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="eb631-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="eb631-169">Hello сервера имя входа администратора, указанных выше.</span><span class="sxs-lookup"><span data-stu-id="eb631-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="eb631-170">Пароль</span><span class="sxs-lookup"><span data-stu-id="eb631-170">Password</span></span> | **** | <span data-ttu-id="eb631-171">Используйте пароль учетной записи администратора hello, настроенных ранее.</span><span class="sxs-lookup"><span data-stu-id="eb631-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="eb631-172">Нажмите кнопку **проверить подключение** tootest, если все параметры настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="eb631-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="eb631-173">Теперь можно щелкнуть подключение hello toosuccessfully подключения toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="eb631-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="eb631-174">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="eb631-174">Clean up resources</span></span>
<span data-ttu-id="eb631-175">Если эти ресурсы не требуется для другой учебник, их можно удалить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb631-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="eb631-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb631-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb631-177">Проектирование первой базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="eb631-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
