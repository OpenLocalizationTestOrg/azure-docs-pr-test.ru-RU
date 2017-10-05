---
title: "Создание веб-приложения Java в Azure с подключением к базе данных MySQL"
description: "Узнайте, как создать приложение Java, которое подключается к службе базы данных MySQL в Azure и работает в службе приложений Azure."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: eb2d59939c4e4486bb14bb143a4a18f9bc1478e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="e336c-103">Создание веб-приложения Java в Azure с подключением к базе данных MySQL</span><span class="sxs-lookup"><span data-stu-id="e336c-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="e336c-104">В этом руководстве показано, как создать веб-приложение Java в Azure и подключить его к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="e336c-104">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="e336c-105">Когда вы выполните инструкции руководства, у вас будет приложение [Spring Boot](https://projects.spring.io/spring-boot/), данные которого хранятся в [базе данных Azure для MySQL](https://docs.microsoft.com/azure/mysql/overview), которая работает в [веб-приложениях службы приложений Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="e336c-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Приложение Java, работающее в службе приложений Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="e336c-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="e336c-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e336c-108">Создание базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="e336c-109">Подключение примера приложения к базе данных</span><span class="sxs-lookup"><span data-stu-id="e336c-109">Connect a sample app to the database</span></span>
> * <span data-ttu-id="e336c-110">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-110">Deploy the app to Azure</span></span>
> * <span data-ttu-id="e336c-111">Обновление и повторное развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="e336c-111">Update and redeploy the app</span></span>
> * <span data-ttu-id="e336c-112">Потоковая передача журналов диагностики из Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e336c-113">Мониторинг приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-113">Monitor the app in the Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e336c-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e336c-114">Prerequisites</span></span>

1. [<span data-ttu-id="e336c-115">Скачайте и установите Git</span><span class="sxs-lookup"><span data-stu-id="e336c-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="e336c-116">Скачайте и установите Java 7 JDK или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="e336c-116">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. <span data-ttu-id="e336c-117">[MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) (этот компонент потребуется запустить)</span><span class="sxs-lookup"><span data-stu-id="e336c-117">[Download, install, and start MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html)</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e336c-118">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e336c-118">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e336c-119">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="e336c-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="e336c-120">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e336c-120">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="e336c-121">Подготовка локальной базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="e336c-121">Prepare local MySQL</span></span> 

<span data-ttu-id="e336c-122">На этом шаге вы создадите базу данных на локальном сервере MySQL. Вы будете использовать ее для тестирования приложения на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e336c-122">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="e336c-123">Подключение к серверу MySQL</span><span class="sxs-lookup"><span data-stu-id="e336c-123">Connect to MySQL server</span></span>

<span data-ttu-id="e336c-124">В окне терминала подключитесь к локальному серверу MySQL.</span><span class="sxs-lookup"><span data-stu-id="e336c-124">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="e336c-125">Используйте это окно терминала для выполнения всех команд в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="e336c-125">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="e336c-126">Если появится предложение ввести пароль, введите пароль для учетной записи `root`.</span><span class="sxs-lookup"><span data-stu-id="e336c-126">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="e336c-127">Если вы не помните пароль учетной записи привилегированного пользователя, ознакомьтесь с разделом [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html) (MySQL: как сбросить пароль привилегированного пользователя).</span><span class="sxs-lookup"><span data-stu-id="e336c-127">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="e336c-128">Если команда выполнена успешно, значит, сервер MySQL уже работает.</span><span class="sxs-lookup"><span data-stu-id="e336c-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="e336c-129">В противном случае обеспечьте запуск локального сервера MySQL, выполнив соответствующие [действия после установки MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="e336c-129">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="e336c-130">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="e336c-130">Create a database</span></span> 

<span data-ttu-id="e336c-131">В командной строке `mysql` создайте базу данных и таблицу для элементов списка дел.</span><span class="sxs-lookup"><span data-stu-id="e336c-131">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="e336c-132">Завершите подключение к серверу, введя команду `quit`.</span><span class="sxs-lookup"><span data-stu-id="e336c-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="e336c-133">Создание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="e336c-133">Create and run the sample app</span></span> 

<span data-ttu-id="e336c-134">На этом шаге вы клонируете пример приложения Spring Boot, настроите его для использования локальной базы данных MySQL и запустите на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e336c-134">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="e336c-135">Клонирования репозитория</span><span class="sxs-lookup"><span data-stu-id="e336c-135">Clone the sample</span></span>

<span data-ttu-id="e336c-136">В окне терминала перейдите в рабочую папку и клонируйте репозиторий.</span><span class="sxs-lookup"><span data-stu-id="e336c-136">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="e336c-137">Настройка приложения для использования базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="e336c-137">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="e336c-138">Замените `spring.datasource.password` и значение в каталоге *spring-boot-mysql-todo/src/main/resources/application.properties* корневым паролем, который вы использовали для открытия строки MySQL:</span><span class="sxs-lookup"><span data-stu-id="e336c-138">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="e336c-139">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="e336c-139">Build and run the sample</span></span>

<span data-ttu-id="e336c-140">Соберите и запустите пример с помощью оболочки Maven, включенной в репозиторий:</span><span class="sxs-lookup"><span data-stu-id="e336c-140">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="e336c-141">Откройте в браузере адрес http://localhost:8080, чтобы увидеть пример в действии.</span><span class="sxs-lookup"><span data-stu-id="e336c-141">Open your browser to http://localhost:8080 to see in the sample in action.</span></span> <span data-ttu-id="e336c-142">По мере добавления задач в список используйте следующие команды SQL в строке MySQL, чтобы просмотреть данные, хранящиеся в базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="e336c-142">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="e336c-143">Остановите приложение, нажав `Ctrl`+`C` в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="e336c-143">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="e336c-144">Создание базы данных MySQL в Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="e336c-145">На этом шаге вы создадите экземпляр [базы данных Azure для MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) с помощью [интерфейса командной строки Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e336c-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="e336c-146">Пример приложения для использования базы данных вы настроите позже в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="e336c-146">You configure the sample application to use this database later on in the tutorial.</span></span>

<span data-ttu-id="e336c-147">Используйте Azure CLI 2.0 в окне терминала, чтобы создать ресурсы, необходимые для размещения приложения Java в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-147">Use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Java application in Azure appservice.</span></span> <span data-ttu-id="e336c-148">Войдите в подписку Azure с помощью команды [az login](/cli/azure/#login) и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="e336c-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="e336c-149">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e336c-149">Create a resource group</span></span>

<span data-ttu-id="e336c-150">Создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md) с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e336c-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e336c-151">Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание и администрирование связанных ресурсов (веб-приложений, баз данных и учетных записей хранения).</span><span class="sxs-lookup"><span data-stu-id="e336c-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="e336c-152">В следующем примере создается группа ресурсов в регионе "Северная Европа".</span><span class="sxs-lookup"><span data-stu-id="e336c-152">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="e336c-153">Чтобы увидеть доступные значения для `--location`, выполните команду [az appservice list-locations](/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="e336c-153">To see the possible values you can use for `--location`, use the [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="e336c-154">Создание сервера MySQL</span><span class="sxs-lookup"><span data-stu-id="e336c-154">Create a MySQL server</span></span>

<span data-ttu-id="e336c-155">Создайте сервер в базе данных Azure для MySQL (предварительная версия), выполнив команду [az mysql server create](/cli/azure/mysql/server#create).</span><span class="sxs-lookup"><span data-stu-id="e336c-155">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="e336c-156">В приведенной команде замените заполнитель `<mysql_server_name>` уникальным именем сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="e336c-156">Substitute your own unique MySQL server name where you see the `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="e336c-157">Это имя является частью имени узла сервера MySQL (`<mysql_server_name>.mysql.database.azure.com`), поэтому оно должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="e336c-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs to be globally unique.</span></span> <span data-ttu-id="e336c-158">Кроме того, замените `<admin_user>` и `<admin_password>` собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="e336c-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="e336c-159">После создания сервера MySQL в Azure CLI отображаются следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="e336c-159">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="e336c-160">Настройка брандмауэра сервера</span><span class="sxs-lookup"><span data-stu-id="e336c-160">Configure server firewall</span></span>

<span data-ttu-id="e336c-161">Создайте правило брандмауэра для сервера MySQL, чтобы разрешить подключения клиентов, выполнив команду [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="e336c-161">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="e336c-162">База данных Azure для MySQL (предварительная версия) пока не поддерживает автоматическое подключение из служб Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="e336c-163">Так как IP-адреса в Azure назначаются динамически, на данный момент рекомендуется включить все IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e336c-163">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses for now.</span></span> <span data-ttu-id="e336c-164">Так как служба находится на этапе предварительной версии, позднее будут добавлены более надежные методы защиты базы данных.</span><span class="sxs-lookup"><span data-stu-id="e336c-164">As the service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="e336c-165">Настройка базы данных MySQL в Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-165">Configure the Azure MySQL database</span></span>

<span data-ttu-id="e336c-166">В окне терминала на своем компьютере подключитесь к серверу MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-166">In the terminal window on your computer, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="e336c-167">Используйте значение, указанное ранее для `<admin_user>` и `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="e336c-167">Use the value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="e336c-168">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="e336c-168">Create a database</span></span> 

<span data-ttu-id="e336c-169">В командной строке `mysql` создайте базу данных и таблицу для элементов списка дел.</span><span class="sxs-lookup"><span data-stu-id="e336c-169">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="e336c-170">Создание пользователя с разрешениями</span><span class="sxs-lookup"><span data-stu-id="e336c-170">Create a user with permissions</span></span>

<span data-ttu-id="e336c-171">Создайте пользователя базы данных и предоставьте ему все привилегии в базе данных `tododb`.</span><span class="sxs-lookup"><span data-stu-id="e336c-171">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="e336c-172">Замените заполнители `<Javaapp_user>` и `<Javaapp_password>` уникальным именем своего приложения.</span><span class="sxs-lookup"><span data-stu-id="e336c-172">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="e336c-173">Завершите подключение к серверу, введя команду `quit`.</span><span class="sxs-lookup"><span data-stu-id="e336c-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="e336c-174">Развертывание примера в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-174">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="e336c-175">Создайте план службы приложений Azure с ценовой категорией **Бесплатный** с помощью команды CLI [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="e336c-175">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="e336c-176">От плана службы приложений зависят физические ресурсы, используемые для размещения приложений.</span><span class="sxs-lookup"><span data-stu-id="e336c-176">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="e336c-177">Все приложения, назначенные плану службы приложений, совместно используют ресурсы, которые позволяют сэкономить при размещении нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="e336c-177">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="e336c-178">После создания плана в Azure CLI отобразится приблизительно такой результат:</span><span class="sxs-lookup"><span data-stu-id="e336c-178">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="e336c-179">Создание веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-179">Create an Azure Web app</span></span>

 <span data-ttu-id="e336c-180">С помощью команды CLI [az webapp create](/cli/azure/appservice/web#create) создайте определение веб-приложения в плане службы приложений `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="e336c-180">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="e336c-181">Определение веб-приложения предоставляет URL-адрес для доступа к приложению и настраивает несколько параметров для развертывания кода в Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-181">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="e336c-182">Замените заполнитель `<app_name>` уникальным именем своего приложения.</span><span class="sxs-lookup"><span data-stu-id="e336c-182">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="e336c-183">Это уникальное имя используется в доменном имени по умолчанию для веб-приложения, поэтому оно должно быть уникальным для всех приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-183">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="e336c-184">Позже можно сопоставить запись личного доменного имени с веб-приложением, прежде чем предоставлять его пользователям.</span><span class="sxs-lookup"><span data-stu-id="e336c-184">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="e336c-185">Когда вы создадите определение веб-приложения, в Azure CLI отобразятся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e336c-185">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="e336c-186">Настройка Java</span><span class="sxs-lookup"><span data-stu-id="e336c-186">Configure Java</span></span> 

<span data-ttu-id="e336c-187">Настройте конфигурацию среды выполнения Java, необходимую для работы приложения, с помощью команды [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="e336c-187">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="e336c-188">Следующая команда настраивает веб-приложение для запуска в Java 8 JDK и [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="e336c-188">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="e336c-189">Настройка приложения для использования базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="e336c-189">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="e336c-190">Перед запуском примера приложения измените параметры веб-приложения, чтобы оно использовало базу данных Azure MySQL, созданную в Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-190">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="e336c-191">Эти свойства доступны для веб-приложения как переменные среды. Они переопределяют значения, заданные в application.properties внутри упакованного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e336c-191">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="e336c-192">Задайте параметры приложения с помощью команды CLI [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings):</span><span class="sxs-lookup"><span data-stu-id="e336c-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in the CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="e336c-193">Получение учетных данных FTP для развертывания</span><span class="sxs-lookup"><span data-stu-id="e336c-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="e336c-194">Для развертывания веб-приложения в службе приложений Azure можно использовать FTP, локальный репозиторий Git, GitHub, Visual Studio Team Services и BitBucket.</span><span class="sxs-lookup"><span data-stu-id="e336c-194">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="e336c-195">В этом примере используется FTP для развертывания WAR-файла, ранее созданного на локальном компьютере в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-195">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="e336c-196">Чтобы определить, какие учетные данные передавать в команде ftp для веб-приложения, выполните команду [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles):</span><span class="sxs-lookup"><span data-stu-id="e336c-196">To determine what credentials to pass along in an ftp command to the Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="e336c-197">Отправка приложения с помощью FTP</span><span class="sxs-lookup"><span data-stu-id="e336c-197">Upload the app using FTP</span></span>

<span data-ttu-id="e336c-198">Используйте любой FTP-клиент для развертывания WAR-файла в папку */site/wwwroot/webapps* по адресу сервера, который получен из поля `URL` в предыдущей команде.</span><span class="sxs-lookup"><span data-stu-id="e336c-198">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="e336c-199">Удалите существующий каталог приложения по умолчанию (ROOT) и замените существующий файл ROOT.war WAR-файлом, созданном ранее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="e336c-199">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="e336c-200">Тестирование веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e336c-200">Test the web app</span></span>

<span data-ttu-id="e336c-201">Перейдите по адресу `http://<app_name>.azurewebsites.net/` и добавьте несколько задач в список.</span><span class="sxs-lookup"><span data-stu-id="e336c-201">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![Приложение Java, работающее в службе приложений Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="e336c-203">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="e336c-203">**Congratulations!**</span></span> <span data-ttu-id="e336c-204">Вы запустили управляемое данными приложение Java в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="e336c-205">Обновление и повторное развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="e336c-205">Update the app and redeploy</span></span>

<span data-ttu-id="e336c-206">Обновите приложение, чтобы включить в список дел дополнительный столбец для дня, когда был создан элемент.</span><span class="sxs-lookup"><span data-stu-id="e336c-206">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="e336c-207">Приложение Spring Boot выполняет обновление схемы базы данных автоматически при изменении модели данных. При этом оно не меняет существующие записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="e336c-207">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="e336c-208">На локальном компьютере, откройте файл *src/main/java/com/example/fabrikam/TodoItem.java* и добавьте в класс следующие операции импорта:</span><span class="sxs-lookup"><span data-stu-id="e336c-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="e336c-209">Добавьте свойство `String` `timeCreated` в файл *src/main/java/com/example/fabrikam/TodoItem.java*, инициализируя его с отметкой времени создания объекта.</span><span class="sxs-lookup"><span data-stu-id="e336c-209">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="e336c-210">Во время редактирования этого файла добавьте методы получения и задания для нового свойства `timeCreated`.</span><span class="sxs-lookup"><span data-stu-id="e336c-210">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="e336c-211">Добавьте в файле *src/main/java/com/example/fabrikam/TodoDemoController.java* строку в метод `updateTodo`, чтобы задать метку времени:</span><span class="sxs-lookup"><span data-stu-id="e336c-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="e336c-212">Добавьте поддержку нового поля в шаблоне Thymeleaf.</span><span class="sxs-lookup"><span data-stu-id="e336c-212">Add support for the new field in the Thymeleaf template.</span></span> <span data-ttu-id="e336c-213">Добавьте в файл *src/main/resources/templates/index.html* новый заголовок таблицы для отметки времени и новое поле для отображения значения отметки времени в каждой строке таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="e336c-213">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="e336c-214">Перестройте приложение:</span><span class="sxs-lookup"><span data-stu-id="e336c-214">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="e336c-215">С помощью FTP удалите существующий каталог *site/wwwroot/webapps/ROOT* и файл *ROOT.war*, а затем отправьте обновленный. WAR-файл как файл ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="e336c-215">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="e336c-216">После обновления приложения будет отображаться столбец **Время создания**.</span><span class="sxs-lookup"><span data-stu-id="e336c-216">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="e336c-217">При добавлении новой задачи приложение заполнит отметку времени автоматически.</span><span class="sxs-lookup"><span data-stu-id="e336c-217">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="e336c-218">Существующие задачи останутся без изменений и будут выполняться приложением, даже если исходная модель данных изменена.</span><span class="sxs-lookup"><span data-stu-id="e336c-218">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![Приложение Java, в которое добавлен новый столбец](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="e336c-220">Потоковая передача журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="e336c-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="e336c-221">При запуске приложения Java в службе приложений Azure можно передавать журналы консоли прямо в свой терминал.</span><span class="sxs-lookup"><span data-stu-id="e336c-221">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="e336c-222">Таким образом, вы будете получать те же диагностические сообщения, которые помогут устранить ошибки приложения.</span><span class="sxs-lookup"><span data-stu-id="e336c-222">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="e336c-223">Чтобы настроить потоки для журналов, выполните команду [az webapp log tail](/cli/azure/appservice/web/log#tail).</span><span class="sxs-lookup"><span data-stu-id="e336c-223">To start log streaming, use the [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="e336c-224">Управление веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-224">Manage your Azure web app</span></span>

<span data-ttu-id="e336c-225">Перейти на портал Azure, чтобы увидеть созданное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e336c-225">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="e336c-226">Для этого войдите на портал [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e336c-226">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="e336c-227">В меню слева выберите **Служба приложений**, а затем щелкните имя своего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-227">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Переход к веб-приложению Azure на портале](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="e336c-229">По умолчанию колонка веб-приложения отображает страницу **обзора**.</span><span class="sxs-lookup"><span data-stu-id="e336c-229">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="e336c-230">Здесь вы можете наблюдать за работой приложения.</span><span class="sxs-lookup"><span data-stu-id="e336c-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="e336c-231">Вы также можете выполнять базовые задачи управления, например завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="e336c-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="e336c-232">На вкладках в левой части колонки отображаются различные страницы конфигурации, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="e336c-232">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![Колонка службы приложений на портале Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="e336c-234">На вкладках в колонке содержится множество полезных функций, которые вы можете добавить в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e336c-234">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="e336c-235">Ниже представлены лишь некоторые из возможностей:</span><span class="sxs-lookup"><span data-stu-id="e336c-235">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="e336c-236">сопоставление настраиваемого DNS-имени;</span><span class="sxs-lookup"><span data-stu-id="e336c-236">Map a custom DNS name</span></span>
* <span data-ttu-id="e336c-237">привязка настраиваемого SSL-сертификата;</span><span class="sxs-lookup"><span data-stu-id="e336c-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="e336c-238">настройка непрерывного развертывания;</span><span class="sxs-lookup"><span data-stu-id="e336c-238">Configure continuous deployment</span></span>
* <span data-ttu-id="e336c-239">вертикальное и горизонтальное масштабирование;</span><span class="sxs-lookup"><span data-stu-id="e336c-239">Scale up and out</span></span>
* <span data-ttu-id="e336c-240">добавление аутентификации пользователей.</span><span class="sxs-lookup"><span data-stu-id="e336c-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="e336c-241">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="e336c-241">Clean up resources</span></span>

<span data-ttu-id="e336c-242">Если эти ресурсы не требуются для изучения другого руководства (см. раздел [Дальнейшие действия](#next)), их можно удалить, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e336c-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="e336c-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e336c-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e336c-244">Создание базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="e336c-245">Подключение примера приложения Java к базе данных MySQL</span><span class="sxs-lookup"><span data-stu-id="e336c-245">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="e336c-246">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-246">Deploy the app to Azure</span></span>
> * <span data-ttu-id="e336c-247">Обновление и повторное развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="e336c-247">Update and redeploy the app</span></span>
> * <span data-ttu-id="e336c-248">Потоковая передача журналов диагностики из Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e336c-249">Управление приложением на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e336c-249">Manage the app in the Azure portal</span></span>

<span data-ttu-id="e336c-250">Перейдите к следующему руководству, чтобы научиться сопоставлять пользовательские DNS-имена с приложением.</span><span class="sxs-lookup"><span data-stu-id="e336c-250">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="e336c-251">Сопоставление существующего настраиваемого DNS-имени с веб-приложениями Azure</span><span class="sxs-lookup"><span data-stu-id="e336c-251">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)