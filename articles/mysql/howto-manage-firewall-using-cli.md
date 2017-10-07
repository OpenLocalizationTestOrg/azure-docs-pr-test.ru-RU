---
title: "aaaCreate и управления базой данных Azure для MySQL правила брандмауэра, с помощью Azure CLI | Документы Microsoft"
description: "В этой статье описывается как toocreate и управления базой данных Azure для правил брандмауэра MySQL с помощью командной строки Azure CLI."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="ad404-103">Создание правил брандмауэра базы данных Azure для MySQL и управление ими с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ad404-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="ad404-104">Правила брандмауэра уровня сервера включите tooan доступа toomanage администраторы базы данных Azure для сервера MySQL из определенный IP-адрес или диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ad404-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="ad404-105">Командами удобный Azure CLI можно создать, обновить, удалить, а также выполнять их список и Показать toomanage правила брандмауэра сервера.</span><span class="sxs-lookup"><span data-stu-id="ad404-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="ad404-106">Обзор брандмауэров базы данных Azure для MySQL приведен в разделе [Правила брандмауэра сервера базы данных Azure для MySQL](./concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="ad404-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad404-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ad404-107">Prerequisites</span></span>
* <span data-ttu-id="ad404-108">[Установите Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ad404-108">[Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)</span></span>
* <span data-ttu-id="ad404-109">Установите пакет SDK Azure для Python для служб MySQL и PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ad404-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="ad404-110">Установите компонент hello Azure CLI для служб, PostgreSQL и MySQL</span><span class="sxs-lookup"><span data-stu-id="ad404-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="ad404-111">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="ad404-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="ad404-112">Команды для правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="ad404-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="ad404-113">Hello **az mysql правила брандмауэра для сервера —** использовать команду из toocreate Azure CLI, удалить, список, отображения и обновить правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="ad404-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="ad404-114">Команды:</span><span class="sxs-lookup"><span data-stu-id="ad404-114">Commands:</span></span>
- <span data-ttu-id="ad404-115">**create**: создание правила брандмауэра сервера Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="ad404-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="ad404-116">**delete**: удаление правила брандмауэра сервера Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="ad404-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="ad404-117">**список** : перечислить правила брандмауэра сервера Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="ad404-118">**Показать** : Показать подробности hello сервера MySQL в Azure правило брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="ad404-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="ad404-119">**update**: обновление правила брандмауэра сервера Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="ad404-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="ad404-120">TooAzure входа и список вашей базы данных Azure для серверов MySQL</span><span class="sxs-lookup"><span data-stu-id="ad404-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="ad404-121">Безопасно подключитесь к Azure CLI к помощью своей учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="ad404-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="ad404-122">Используйте hello **входа az** команды toodo это.</span><span class="sxs-lookup"><span data-stu-id="ad404-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="ad404-123">Выполните следующую команду из командной строки hello hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="ad404-124">Эта команда будет выдавать toouse кода hello следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="ad404-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="ad404-125">На веб-страницу приветствия tooopen браузера [https://aka.ms/devicelogin](https://aka.ms/devicelogin) и введите код hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="ad404-126">В строке приветствия вход, используя учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="ad404-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="ad404-127">После авторизации имени входа в консоль hello будут выведены список подписок.</span><span class="sxs-lookup"><span data-stu-id="ad404-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="ad404-128">Скопируйте идентификатор hello hello требуемого подписки tooset hello текущей подписки toobe используется продвижение вперед.</span><span class="sxs-lookup"><span data-stu-id="ad404-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="ad404-129">Список hello Azure баз данных MySQL серверов для вашей подписки и группе ресурсов, если вы не уверены приветствия имен.</span><span class="sxs-lookup"><span data-stu-id="ad404-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="ad404-130">Обратите внимание, атрибут имени hello в hello со списком, который будет использоваться toospecify какие toowork сервера MySQL на.</span><span class="sxs-lookup"><span data-stu-id="ad404-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="ad404-131">При необходимости подтверждение hello сведения для этого toousing hello имя атрибута tooconfirm имя сервера указано правильно:</span><span class="sxs-lookup"><span data-stu-id="ad404-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="ad404-132">Вывод списка правил брандмауэра для сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="ad404-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="ad404-133">Используя hello имя сервера и имя группы ресурсов hello, список hello существующего правила брандмауэра для сервера на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="ad404-134">Обратите внимание, атрибут имени сервера hello указывается в hello **--сервер** переключения и не hello **--имя** переключения.</span><span class="sxs-lookup"><span data-stu-id="ad404-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="ad404-135">Hello выходные данные будут отображаться hello правила, если таковая имеется, по умолчанию в формате JSON формата.</span><span class="sxs-lookup"><span data-stu-id="ad404-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="ad404-136">Можно использовать переключатель hello **--выходная таблица** для более удобочитаемый формат таблицы в качестве выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="ad404-137">Создание правила брандмауэра для сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="ad404-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="ad404-138">Используя имя сервера Azure MySQL hello и имя группы ресурсов hello, создайте новое правило брандмауэра на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="ad404-139">Введите имя для правила hello, hello начальный IP-адрес и конечным IP для toocover hello правило доступа tooallow диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ad404-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="ad404-140">Для единственного IP адрес toobe доступ разрешен, предоставляют hello таким же адресом как hello начальный IP- и конечного IP-адресов, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="ad404-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="ad404-141">При успешном завершении hello выходные данные команды будут отображаться сведения hello hello правила брандмауэра, которые вы создали, по умолчанию в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ad404-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="ad404-142">В случае сбоя hello выходные данные вместо этого отображается текст сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="ad404-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="ad404-143">Обновление правила брандмауэра для сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="ad404-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="ad404-144">С помощью hello Azure MySQL имя сервера и имя группы ресурсов hello, обновить существующее правило брандмауэра на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="ad404-145">Укажите имя hello существующее правило брандмауэра, как входные данные и hello начала IP-адресов и конечным IP атрибуты tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="ad404-146">При успешном завершении hello выходные данные команды будут отображаться сведения hello hello правила брандмауэра, которые были обновлены, по умолчанию в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ad404-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="ad404-147">В случае сбоя hello выходные данные вместо этого отображается текст сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="ad404-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="ad404-148">Если правило брандмауэра hello не существует, создается командой обновления hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="ad404-149">Отображение сведения о правиле брандмауэра для сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="ad404-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="ad404-150">Используя имя сервера Azure MySQL hello и имя группы ресурсов hello, подробно hello существующего брандмауэра правило с сервера hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="ad404-151">Предоставить имя hello hello существующее правило брандмауэра в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="ad404-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="ad404-152">При успешном завершении hello выходные данные команды будут отображаться сведения hello hello правила брандмауэра, которые указаны, по умолчанию в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ad404-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="ad404-153">В случае сбоя hello выходные данные вместо этого отображается текст сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="ad404-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="ad404-154">Удаление правила брандмауэра для сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="ad404-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="ad404-155">Используя имя сервера Azure MySQL hello и имя группы ресурсов hello, удалите существующее правило брандмауэра с сервера hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="ad404-156">Укажите имя hello hello существующее правило брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="ad404-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="ad404-157">При успешном выполнении выходные данные отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="ad404-157">Upon success, there is no output.</span></span> <span data-ttu-id="ad404-158">После сбоя будет возвращено сообщение об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="ad404-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad404-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad404-159">Next steps</span></span>
- <span data-ttu-id="ad404-160">Узнайте больше о [правилах брандмауэра сервера базы данных Azure для MySQL](./concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="ad404-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="ad404-161">Создание и управление для MySQL правила брандмауэра, с помощью портала Azure hello базы данных Azure</span><span class="sxs-lookup"><span data-stu-id="ad404-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
