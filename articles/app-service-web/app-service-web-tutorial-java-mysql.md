---
title: "aaaBuild веб-приложения Java и MySQL в Azure"
description: "Узнайте, как tooget приложения Java, подключается служба базы данных MySQL в Azure toohello, работа в Azure службы приложений."
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
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="ec296-103">Создание веб-приложения Java в Azure с подключением к базе данных MySQL</span><span class="sxs-lookup"><span data-stu-id="ec296-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="ec296-104">Этот учебник показывает, как toocreate Java веб-приложения в Azure и соедините его tooa базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="ec296-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="ec296-105">Когда вы выполните инструкции руководства, у вас будет приложение [Spring Boot](https://projects.spring.io/spring-boot/), данные которого хранятся в [базе данных Azure для MySQL](https://docs.microsoft.com/azure/mysql/overview), которая работает в [веб-приложениях службы приложений Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="ec296-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Приложение Java, работающее в службе приложений Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="ec296-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="ec296-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec296-108">Создание базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="ec296-109">Подключение приложения toohello образца базы данных</span><span class="sxs-lookup"><span data-stu-id="ec296-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="ec296-110">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="ec296-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="ec296-111">Обновить и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="ec296-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="ec296-112">Потоковая передача журналов диагностики из Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="ec296-113">Мониторинг приложения hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ec296-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ec296-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ec296-114">Prerequisites</span></span>

1. [<span data-ttu-id="ec296-115">Скачайте и установите Git</span><span class="sxs-lookup"><span data-stu-id="ec296-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="ec296-116">Загрузите и установите hello Java 7 JDK или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="ec296-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. <span data-ttu-id="ec296-117">[MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) (этот компонент потребуется запустить)</span><span class="sxs-lookup"><span data-stu-id="ec296-117">[Download, install, and start MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html)</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ec296-118">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ec296-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ec296-119">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="ec296-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ec296-120">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ec296-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="ec296-121">Подготовка локальной базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="ec296-121">Prepare local MySQL</span></span> 

<span data-ttu-id="ec296-122">На этом шаге создания базы данных в локальный сервер MySQL для использования в проверочных приложение hello локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ec296-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="ec296-123">Подключение сервера tooMySQL</span><span class="sxs-lookup"><span data-stu-id="ec296-123">Connect tooMySQL server</span></span>

<span data-ttu-id="ec296-124">В окне терминала подключение tooyour локального сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="ec296-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="ec296-125">Можно использовать это окно терминала toorun hello команды в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ec296-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="ec296-126">Если появится запрос пароля, введите пароль hello для hello `root` учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ec296-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="ec296-127">Если вы не помните пароль корневой учетной записи, см. раздел [MySQL: как tooReset hello пароль учетной записи Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="ec296-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="ec296-128">Если команда выполнена успешно, значит, сервер MySQL уже работает.</span><span class="sxs-lookup"><span data-stu-id="ec296-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="ec296-129">Если это не так, убедитесь в том, локальному серверу MySQL запущен из следующих hello [действий после установки MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="ec296-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="ec296-130">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="ec296-130">Create a database</span></span> 

<span data-ttu-id="ec296-131">В hello `mysql` запрос, создайте базу данных и таблицу для hello заданий для выполнения.</span><span class="sxs-lookup"><span data-stu-id="ec296-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="ec296-132">Завершите подключение к серверу, введя команду `quit`.</span><span class="sxs-lookup"><span data-stu-id="ec296-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="ec296-133">Создание и выполнение примера приложения hello</span><span class="sxs-lookup"><span data-stu-id="ec296-133">Create and run hello sample app</span></span> 

<span data-ttu-id="ec296-134">На этом шаге клонировать загрузки Spring пример приложения, задана база данных локальной MySQL toouse hello и запустите его на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ec296-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="ec296-135">Образец hello клонирования</span><span class="sxs-lookup"><span data-stu-id="ec296-135">Clone hello sample</span></span>

<span data-ttu-id="ec296-136">В окне терминала hello перейдите tooa работа каталога и клонирования репозитория образец hello.</span><span class="sxs-lookup"><span data-stu-id="ec296-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="ec296-137">Настройте базу данных MySQL hello toouse приложения hello</span><span class="sxs-lookup"><span data-stu-id="ec296-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="ec296-138">Обновление hello `spring.datasource.password` и значение в *spring-boot-mysql-todo/src/main/resources/application.properties* с hello же корневой пароль, используемый tooopen hello MySQL строки:</span><span class="sxs-lookup"><span data-stu-id="ec296-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="ec296-139">Построение и запуск образца hello</span><span class="sxs-lookup"><span data-stu-id="ec296-139">Build and run hello sample</span></span>

<span data-ttu-id="ec296-140">Построение и запуск образца hello, с помощью программы-оболочки Maven hello, включенных в репозитории hello:</span><span class="sxs-lookup"><span data-stu-id="ec296-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="ec296-141">Откройте ваш браузер toohttp://localhost:8080 toosee в образце hello в действии.</span><span class="sxs-lookup"><span data-stu-id="ec296-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="ec296-142">Добавление toohello список задач, используйте следующие команды SQL, в hello MySQL prompt tooview hello данные, хранящиеся в MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="ec296-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="ec296-143">Остановить приложение hello щелчком `Ctrl` + `C` в hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="ec296-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="ec296-144">Создание базы данных MySQL в Azure</span><span class="sxs-lookup"><span data-stu-id="ec296-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="ec296-145">На этом шаге вы создадите [базы данных Azure для MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) экземпляра, используя hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ec296-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="ec296-146">Настройке toouse приложения образец hello эта база данных позднее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="ec296-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="ec296-147">Используйте hello Azure CLI 2.0 в окно терминала toocreate hello ресурсы, необходимые toohost приложения Java в Azure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="ec296-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="ec296-148">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="ec296-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="ec296-149">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="ec296-149">Create a resource group</span></span>

<span data-ttu-id="ec296-150">Создание [группы ресурсов](../azure-resource-manager/resource-group-overview.md) с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="ec296-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ec296-151">Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание и администрирование связанных ресурсов (веб-приложений, баз данных и учетных записей хранения).</span><span class="sxs-lookup"><span data-stu-id="ec296-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="ec296-152">Hello следующий пример создает группу ресурсов в Северной Европе hello:</span><span class="sxs-lookup"><span data-stu-id="ec296-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="ec296-153">Возможные значения toosee hello можно использовать для `--location`, использовать hello [az appservice список расположений](/cli/azure/appservice#list-locations) команды.</span><span class="sxs-lookup"><span data-stu-id="ec296-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="ec296-154">Создание сервера MySQL</span><span class="sxs-lookup"><span data-stu-id="ec296-154">Create a MySQL server</span></span>

<span data-ttu-id="ec296-155">Создать сервер базы данных Azure для MySQL (Предварительная версия) с hello [создать сервер mysql az](/cli/azure/mysql/server#create) команды.</span><span class="sxs-lookup"><span data-stu-id="ec296-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="ec296-156">Замените собственное уникальное имя сервера MySQL, показывающий hello `<mysql_server_name>` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="ec296-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="ec296-157">Это имя является частью имени узла сервера MySQL, `<mysql_server_name>.mysql.database.azure.com`, поэтому ему toobe глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="ec296-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="ec296-158">Кроме того, замените `<admin_user>` и `<admin_password>` собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="ec296-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="ec296-159">При создании сервера MySQL hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="ec296-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="ec296-160">Настройка брандмауэра сервера</span><span class="sxs-lookup"><span data-stu-id="ec296-160">Configure server firewall</span></span>

<span data-ttu-id="ec296-161">Создать правило брандмауэра для MySQL server tooallow клиентских соединений с помощью hello [az mysql правила брандмауэра для сервера — создание](/cli/azure/mysql/server/firewall-rule#create) команды.</span><span class="sxs-lookup"><span data-stu-id="ec296-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="ec296-162">База данных Azure для MySQL (предварительная версия) пока не поддерживает автоматическое подключение из служб Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="ec296-163">Как динамически назначаются IP-адресов в Azure, это лучше tooenable все IP-адреса теперь.</span><span class="sxs-lookup"><span data-stu-id="ec296-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="ec296-164">По мере его предварительной версии службы hello лучше методы защиты базы данных будет включено.</span><span class="sxs-lookup"><span data-stu-id="ec296-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="ec296-165">Настройка базы данных MySQL в Azure hello</span><span class="sxs-lookup"><span data-stu-id="ec296-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="ec296-166">В окне терминала hello на компьютере подключение toohello MySQL server в Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="ec296-167">Используйте значение hello, указанную ранее `<admin_user>` и `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="ec296-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="ec296-168">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="ec296-168">Create a database</span></span> 

<span data-ttu-id="ec296-169">В hello `mysql` запрос, создайте базу данных и таблицу для hello заданий для выполнения.</span><span class="sxs-lookup"><span data-stu-id="ec296-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="ec296-170">Создание пользователя с разрешениями</span><span class="sxs-lookup"><span data-stu-id="ec296-170">Create a user with permissions</span></span>

<span data-ttu-id="ec296-171">Создание пользователя базы данных и присвойте ему все привилегии в hello `tododb` базы данных.</span><span class="sxs-lookup"><span data-stu-id="ec296-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="ec296-172">Замените заполнители hello `<Javaapp_user>` и `<Javaapp_password>` приложения уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="ec296-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="ec296-173">Завершите подключение к серверу, введя команду `quit`.</span><span class="sxs-lookup"><span data-stu-id="ec296-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="ec296-174">Развертывание образца hello tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="ec296-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="ec296-175">Создать план службы приложений Azure с hello **FREE** ценовой категории с помощью hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команду CLI.</span><span class="sxs-lookup"><span data-stu-id="ec296-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="ec296-176">план служб приложений Hello определяет toohost hello физические ресурсы, используемые приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="ec296-177">Все приложения, назначенный tooan план служб приложений используют эти ресурсы, позволяя toosave затрат при размещении нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="ec296-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="ec296-178">При готовности плана hello hello Azure CLI показывает, как выходной toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="ec296-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="ec296-179">Создание веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="ec296-179">Create an Azure Web app</span></span>

 <span data-ttu-id="ec296-180">Используйте hello [создать веб-приложение az](/cli/azure/appservice/web#create) toocreate команду CLI определение web app в hello `myAppServicePlan` план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="ec296-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="ec296-181">Определение приложения Hello web предоставляет приложению tooaccess URL-адрес и настраивает некоторые параметры toodeploy tooAzure вашего кода.</span><span class="sxs-lookup"><span data-stu-id="ec296-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="ec296-182">Замена hello `<app_name>` заполнитель с именем собственный уникальный приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="ec296-183">Это уникальное имя является частью hello имя домена по умолчанию для веб-приложения hello, поэтому hello имя должно toobe уникальным для всех приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="ec296-184">Перед тем, как он tooyour пользователей можно сопоставить toohello входа пользовательского домена имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="ec296-185">При готовности определение приложения hello web hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="ec296-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="ec296-186">Настройка Java</span><span class="sxs-lookup"><span data-stu-id="ec296-186">Configure Java</span></span> 

<span data-ttu-id="ec296-187">Настройка конфигурации среды выполнения Java hello, необходимый вашему приложению hello [обновление конфигурации web appservice az](/cli/azure/appservice/web/config#update) команды.</span><span class="sxs-lookup"><span data-stu-id="ec296-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="ec296-188">Hello следующая команда настраивает hello web app toorun на последние Java JDK 8 и [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="ec296-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="ec296-189">Настройка базы данных Azure SQL hello toouse приложения hello</span><span class="sxs-lookup"><span data-stu-id="ec296-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="ec296-190">Перед запуском пример приложения hello, настройте параметры приложения на hello веб-приложения toouse hello Azure MySQL база данных, созданные в Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="ec296-191">Эти свойства предоставляется toohello веб-приложение как переменные среды и переопределить hello значения, заданные в application.properties hello внутри hello упакованных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="ec296-192">Задайте параметры приложения с помощью [az webapp конфигурации appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) в hello CLI:</span><span class="sxs-lookup"><span data-stu-id="ec296-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="ec296-193">Получение учетных данных FTP для развертывания</span><span class="sxs-lookup"><span data-stu-id="ec296-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="ec296-194">Вы можете развернуть appservice tooAzure вашего приложения различными способами, включая FTP, локальный Git, GitHub, Visual Studio Team Services и BitBucket.</span><span class="sxs-lookup"><span data-stu-id="ec296-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="ec296-195">В этом примере FTP toodeploy hello. WAR-файла, созданного ранее на ваш локальный компьютер tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="ec296-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="ec296-196">toodetermine, что учетные данные toopass вдоль в ftp команда toohello веб-приложения используйте [az appservice web развертывания списка публикации профили-](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) команды:</span><span class="sxs-lookup"><span data-stu-id="ec296-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="ec296-197">Отправка приложения hello, с помощью протокола FTP</span><span class="sxs-lookup"><span data-stu-id="ec296-197">Upload hello app using FTP</span></span>

<span data-ttu-id="ec296-198">С помощью вашего любимого hello toodeploy средство FTP. Файл toohello WAR */site/wwwroot/webapps* папку на адрес сервера hello, взяты из hello `URL` в предыдущей команде hello.</span><span class="sxs-lookup"><span data-stu-id="ec296-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="ec296-199">Удалите hello существующий каталог приложений по умолчанию (ROOT) и замените существующие ROOT.war с hello hello. WAR-файл, встроенной в hello ранее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="ec296-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a><span data-ttu-id="ec296-200">Веб-приложения hello теста</span><span class="sxs-lookup"><span data-stu-id="ec296-200">Test hello web app</span></span>

<span data-ttu-id="ec296-201">Обзор слишком`http://<app_name>.azurewebsites.net/` и добавьте список toohello несколько задач.</span><span class="sxs-lookup"><span data-stu-id="ec296-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![Приложение Java, работающее в службе приложений Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="ec296-203">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="ec296-203">**Congratulations!**</span></span> <span data-ttu-id="ec296-204">Вы запустили управляемое данными приложение Java в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="ec296-205">Приложение hello обновления и повторного развертывания</span><span class="sxs-lookup"><span data-stu-id="ec296-205">Update hello app and redeploy</span></span>

<span data-ttu-id="ec296-206">Обновление приложения hello tooinclude дополнительный столбец в список todo hello для какой день hello элемент был создан.</span><span class="sxs-lookup"><span data-stu-id="ec296-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="ec296-207">Spring загрузки обрабатывает обновление схемы базы данных hello как hello изменений модели данных без изменения существующей записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="ec296-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="ec296-208">На локальном компьютере, откройте *src/main/java/com/example/fabrikam/TodoItem.java* и добавьте следующие hello импортирует toohello класса:</span><span class="sxs-lookup"><span data-stu-id="ec296-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="ec296-209">Добавить `String` свойство `timeCreated` слишком*src/main/java/com/example/fabrikam/TodoItem.java*, инициализирует его с отметкой времени создания объекта.</span><span class="sxs-lookup"><span data-stu-id="ec296-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="ec296-210">Добавьте методы получения и задания для нового hello `timeCreated` свойство при редактировании этого файла.</span><span class="sxs-lookup"><span data-stu-id="ec296-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="ec296-211">Обновление *src/main/java/com/example/fabrikam/TodoDemoController.java* со строкой в hello `updateTodo` timestamp hello tooset метод:</span><span class="sxs-lookup"><span data-stu-id="ec296-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="ec296-212">Добавлена поддержка нового поля hello в шаблоне Thymeleaf hello.</span><span class="sxs-lookup"><span data-stu-id="ec296-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="ec296-213">Обновление *src/main/resources/templates/index.html* с заголовком таблицы для отметки времени hello и новое значение поля toodisplay hello объекта hello timestamp в каждой строке таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="ec296-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="ec296-214">Повторное построение приложения hello:</span><span class="sxs-lookup"><span data-stu-id="ec296-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="ec296-215">Обновить hello FTP. WAR как до, удалив существующие hello */wwwroot или веб-приложения или корневого КАТАЛОГА сайта* каталога и *ROOT.war*, то передача hello обновлены. WAR-файл как ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="ec296-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="ec296-216">При обновлении приложения hello **время создания** столбца является видимым.</span><span class="sxs-lookup"><span data-stu-id="ec296-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="ec296-217">При добавлении новой задачи, приложение hello будет автоматически заполнять hello отметки времени.</span><span class="sxs-lookup"><span data-stu-id="ec296-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="ec296-218">Существующие задачи остаются без изменений и работать с приложение hello, несмотря на то, что изменилось hello базовой модели данных.</span><span class="sxs-lookup"><span data-stu-id="ec296-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![Приложение Java, в которое добавлен новый столбец](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="ec296-220">Потоковая передача журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="ec296-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="ec296-221">Во время работы приложения Java в службе приложений Azure, можно получить консоли hello журналы по конвейеру непосредственно tooyour терминала.</span><span class="sxs-lookup"><span data-stu-id="ec296-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="ec296-222">Таким образом, можно получить hello же диагностические сообщения toohelp отладке ошибок приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="ec296-223">Журнал toostart потоковой передачи, используйте hello [заключительного фрагмента журнала webapp az](/cli/azure/appservice/web/log#tail) команды.</span><span class="sxs-lookup"><span data-stu-id="ec296-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="ec296-224">Управление веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="ec296-224">Manage your Azure web app</span></span>

<span data-ttu-id="ec296-225">Go toohello hello Azure портала toosee веб-приложения, созданный.</span><span class="sxs-lookup"><span data-stu-id="ec296-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="ec296-226">toodo, вход слишком[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec296-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="ec296-227">Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="ec296-229">По умолчанию колонки веб-приложение отображает hello **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="ec296-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="ec296-230">Здесь вы можете наблюдать за работой приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="ec296-231">Вы также можете выполнять базовые задачи управления, например завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="ec296-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="ec296-232">Hello вкладках hello левой части колонки hello отображаются страницы hello другой конфигурации, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="ec296-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Колонка службы приложений на портале Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="ec296-234">Эти закладки в колонке hello показывают hello множеством замечательных функций, можно добавить tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="ec296-235">После списка Hello предоставляет несколько возможностей hello:</span><span class="sxs-lookup"><span data-stu-id="ec296-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="ec296-236">сопоставление настраиваемого DNS-имени;</span><span class="sxs-lookup"><span data-stu-id="ec296-236">Map a custom DNS name</span></span>
* <span data-ttu-id="ec296-237">привязка настраиваемого SSL-сертификата;</span><span class="sxs-lookup"><span data-stu-id="ec296-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="ec296-238">настройка непрерывного развертывания;</span><span class="sxs-lookup"><span data-stu-id="ec296-238">Configure continuous deployment</span></span>
* <span data-ttu-id="ec296-239">вертикальное и горизонтальное масштабирование;</span><span class="sxs-lookup"><span data-stu-id="ec296-239">Scale up and out</span></span>
* <span data-ttu-id="ec296-240">добавление аутентификации пользователей.</span><span class="sxs-lookup"><span data-stu-id="ec296-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ec296-241">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="ec296-241">Clean up resources</span></span>

<span data-ttu-id="ec296-242">Если эти ресурсы не требуется другой учебник (см. [дальнейшие действия](#next)), их можно удалить, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ec296-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="ec296-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec296-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec296-244">Создание базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="ec296-245">Подключение toohello приложения Java образец MySQL</span><span class="sxs-lookup"><span data-stu-id="ec296-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="ec296-246">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="ec296-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="ec296-247">Обновить и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="ec296-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="ec296-248">Потоковая передача журналов диагностики из Azure.</span><span class="sxs-lookup"><span data-stu-id="ec296-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="ec296-249">Управление приложение hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ec296-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="ec296-250">Переместить следующий учебник toolearn toohello как toomap пользовательские DNS название toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="ec296-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="ec296-251">Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="ec296-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
