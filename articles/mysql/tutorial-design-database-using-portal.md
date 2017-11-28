---
title: "Проектирование первой базы данных Azure для MySQL с помощью портала Azure | Документация Майкрософт"
description: "Это руководство содержит сведения о создании базы данных и сервера базы данных Azure для MySQL и управлении ими с помощью портала Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="0f205-103">Проектирование первой базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="0f205-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="0f205-104">База данных Azure для MySQL — это управляемая служба, которая позволяет вам запускать, администрировать и масштабировать высокодоступные базы данных MySQL в облаке.</span><span class="sxs-lookup"><span data-stu-id="0f205-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="0f205-105">С помощью портала Azure можно легко управлять сервером и проектировать базы данных.</span><span class="sxs-lookup"><span data-stu-id="0f205-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="0f205-106">Из этого руководства вы узнаете, как с помощью портала Azure выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="0f205-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0f205-107">создание базы данных Azure для MySQL;</span><span class="sxs-lookup"><span data-stu-id="0f205-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="0f205-108">настройка брандмауэра сервера;</span><span class="sxs-lookup"><span data-stu-id="0f205-108">Configure the server firewall</span></span>
> * <span data-ttu-id="0f205-109">использование программы командной строки MySQL для создания базы данных;</span><span class="sxs-lookup"><span data-stu-id="0f205-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="0f205-110">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="0f205-110">Load sample data</span></span>
> * <span data-ttu-id="0f205-111">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="0f205-111">Query data</span></span>
> * <span data-ttu-id="0f205-112">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="0f205-112">Update data</span></span>
> * <span data-ttu-id="0f205-113">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="0f205-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="0f205-114">Выполните вход на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0f205-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="0f205-115">Откройте предпочитаемый веб-браузер и перейдите на [портал Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0f205-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="0f205-116">Введите свои учетные данные для входа на портал.</span><span class="sxs-lookup"><span data-stu-id="0f205-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="0f205-117">Панель мониторинга службы является представлением по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0f205-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="0f205-118">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="0f205-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="0f205-119">Сервер базы данных Azure для MySQL создается с определенным набором [вычислительных ресурсов и ресурсов хранения](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0f205-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="0f205-120">Он создается в [группе ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="0f205-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="0f205-121">Выберите **Базы данных** > **База данных Azure для MySQL**.</span><span class="sxs-lookup"><span data-stu-id="0f205-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="0f205-122">Если сервер MySQL не отображается в категории **Базы данных**, щелкните **Показать все**, чтобы просмотреть все доступные службы баз данных.</span><span class="sxs-lookup"><span data-stu-id="0f205-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="0f205-123">Для быстрого поиска службы вы можете также ввести в поле поиска **База данных Azure для MySQL**.</span><span class="sxs-lookup"><span data-stu-id="0f205-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="0f205-124">![2.1. Переход к службе MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="0f205-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="0f205-125">Щелкните элемент **База данных Azure для MySQL**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0f205-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="0f205-126">В нашем примере мы заполним форму базы данных Azure для MySQL, указав следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="0f205-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="0f205-127">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="0f205-127">**Setting**</span></span> | <span data-ttu-id="0f205-128">**Рекомендуемое значение**</span><span class="sxs-lookup"><span data-stu-id="0f205-128">**Suggested value**</span></span> | <span data-ttu-id="0f205-129">**Описание поля**</span><span class="sxs-lookup"><span data-stu-id="0f205-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="0f205-130">*Server name* (Имя сервера)</span><span class="sxs-lookup"><span data-stu-id="0f205-130">*Server name*</span></span> | <span data-ttu-id="0f205-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="0f205-131">myserver4demo</span></span>  | <span data-ttu-id="0f205-132">Имя сервера должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="0f205-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="0f205-133">*Подписка*</span><span class="sxs-lookup"><span data-stu-id="0f205-133">*Subscription*</span></span> | <span data-ttu-id="0f205-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="0f205-134">mysubscription</span></span> | <span data-ttu-id="0f205-135">Выберите подписку в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="0f205-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="0f205-136">*Группа ресурсов*</span><span class="sxs-lookup"><span data-stu-id="0f205-136">*Resource group*</span></span> | <span data-ttu-id="0f205-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="0f205-137">myresourcegroup</span></span> | <span data-ttu-id="0f205-138">Создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="0f205-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="0f205-139">*Имя для входа администратора сервера*</span><span class="sxs-lookup"><span data-stu-id="0f205-139">*Server admin login*</span></span> | <span data-ttu-id="0f205-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="0f205-140">myadmin</span></span> | <span data-ttu-id="0f205-141">Укажите имя учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="0f205-141">Setup admin account name.</span></span> |
| <span data-ttu-id="0f205-142">*Пароль*</span><span class="sxs-lookup"><span data-stu-id="0f205-142">*Password*</span></span> |  | <span data-ttu-id="0f205-143">Укажите надежный пароль для учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="0f205-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="0f205-144">*Подтверждение пароля.*</span><span class="sxs-lookup"><span data-stu-id="0f205-144">*Confirm password*</span></span> |  | <span data-ttu-id="0f205-145">Подтвердите пароль учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="0f205-145">Confirm the admin account password.</span></span> |
| <span data-ttu-id="0f205-146">*Расположение*</span><span class="sxs-lookup"><span data-stu-id="0f205-146">*Location*</span></span> |  | <span data-ttu-id="0f205-147">Выберите доступный регион.</span><span class="sxs-lookup"><span data-stu-id="0f205-147">Select an available region.</span></span> |
| <span data-ttu-id="0f205-148">*Версия*</span><span class="sxs-lookup"><span data-stu-id="0f205-148">*Version*</span></span> | <span data-ttu-id="0f205-149">5.7</span><span class="sxs-lookup"><span data-stu-id="0f205-149">5.7</span></span> | <span data-ttu-id="0f205-150">Выберите последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="0f205-150">Choose the latest version.</span></span> |
| <span data-ttu-id="0f205-151">*Настройка производительности*</span><span class="sxs-lookup"><span data-stu-id="0f205-151">*Configure performance*</span></span> | <span data-ttu-id="0f205-152">"Базовый", 50 единиц вычислений, 50 ГБ</span><span class="sxs-lookup"><span data-stu-id="0f205-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="0f205-153">Укажите значения для параметров **Ценовая категория**, **Единицы вычислений**, **Хранилище (ГБ)** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0f205-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="0f205-154">*Закрепить на панели мониторинга*</span><span class="sxs-lookup"><span data-stu-id="0f205-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="0f205-155">Проверка</span><span class="sxs-lookup"><span data-stu-id="0f205-155">Check</span></span> | <span data-ttu-id="0f205-156">Рекомендуем установить этот флажок, чтобы ускорить поиск сервера позже</span><span class="sxs-lookup"><span data-stu-id="0f205-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="0f205-157">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0f205-157">Then, click **Create**.</span></span> <span data-ttu-id="0f205-158">Через несколько минут в облаке будет создан сервер базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f205-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="0f205-159">На панели инструментов выберите **Уведомления**, чтобы отслеживать процесс развертывания.</span><span class="sxs-lookup"><span data-stu-id="0f205-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="0f205-160">Настройка брандмауэра</span><span class="sxs-lookup"><span data-stu-id="0f205-160">Configure firewall</span></span>
<span data-ttu-id="0f205-161">Базы данных Azure для MySQL защищены брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="0f205-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="0f205-162">По умолчанию все подключения к серверу и базам данных на сервере отклоняются.</span><span class="sxs-lookup"><span data-stu-id="0f205-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="0f205-163">Перед первым подключением к базе данных Azure для MySQL настройте брандмауэр, чтобы добавить IP-адрес общедоступной сети клиентского компьютера (или диапазон IP-адресов).</span><span class="sxs-lookup"><span data-stu-id="0f205-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="0f205-164">Щелкните созданный сервер и выберите **Безопасность подключения**.</span><span class="sxs-lookup"><span data-stu-id="0f205-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="0f205-165">![3.1. Безопасность подключения](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="0f205-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="0f205-166">Здесь вы можете **добавить свой IP-адрес** или настроить правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="0f205-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="0f205-167">Не забудьте щелкнуть **Сохранить** после создания правил.</span><span class="sxs-lookup"><span data-stu-id="0f205-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="0f205-168">Теперь вы можете подключиться к серверу с помощью программы командной строки MySQL или с помощью инструмента с графическим пользовательским интерфейсом MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="0f205-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="0f205-169">Сервер базы данных Azure для MySQL обменивается данными через порт 3306.</span><span class="sxs-lookup"><span data-stu-id="0f205-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="0f205-170">Если вы пытаетесь подключиться из корпоративной сети, исходящий трафик через порт 3306 может быть запрещен сетевым брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="0f205-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="0f205-171">В таком случае вы не сможете подключиться к серверу MySQL Azure, пока ваш отдел ИТ не откроет порт 3306.</span><span class="sxs-lookup"><span data-stu-id="0f205-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0f205-172">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="0f205-172">Get connection information</span></span>
<span data-ttu-id="0f205-173">Полное **имя сервера** и **имя для входа администратора сервера** для базы данных Azure для сервера MySQL можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0f205-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="0f205-174">Полное имя сервера используется для подключения к серверу с помощью программы командной строки MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f205-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="0f205-175">На [портале Azure](https://portal.azure.com/) в меню слева щелкните **Все ресурсы**, введите имя и найдите свой сервер базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f205-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="0f205-176">Выберите имя сервера, чтобы просмотреть сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="0f205-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="0f205-177">В разделе "Параметры" щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0f205-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="0f205-178">Запишите значения параметров **Имя сервера** и **Имя для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="0f205-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="0f205-179">Вы можете нажать кнопку "Копировать" рядом с каждым полем, чтобы скопировать его значение в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="0f205-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="0f205-180">![4.2. Свойства сервера](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="0f205-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="0f205-181">В этом примере серверу присвоено имя *myserver4demo.mysql.database.azure.com*, а имя для входа администратора сервера имеет значение *myadmin@myserver4demo*.</span><span class="sxs-lookup"><span data-stu-id="0f205-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="0f205-182">Подключение к серверу с помощью MySQL</span><span class="sxs-lookup"><span data-stu-id="0f205-182">Connect to the server using mysql</span></span>
<span data-ttu-id="0f205-183">Используйте [программу командной строки MySQL](https://dev.mysql.com/doc/refman/5.7/en/mysql.html), чтобы подключиться к серверу базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f205-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="0f205-184">Можно запустить программу командной строки MySQL из Azure Cloud Shell в браузере или на собственном компьютере, используя локальные инструменты MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f205-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="0f205-185">Для запуска Azure Cloud Shell нажмите кнопку `Try It` в блоке кода в этой статье или перейдите на портал Azure и щелкните значок `>_` на панели инструментов справа вверху.</span><span class="sxs-lookup"><span data-stu-id="0f205-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="0f205-186">Введите команду для подключения:</span><span class="sxs-lookup"><span data-stu-id="0f205-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="0f205-187">Создание пустой базы данных</span><span class="sxs-lookup"><span data-stu-id="0f205-187">Create a blank database</span></span>
<span data-ttu-id="0f205-188">Подключившись к серверу, создайте пустую базу данных для работы.</span><span class="sxs-lookup"><span data-stu-id="0f205-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="0f205-189">Выполните следующую команду в командной строке, чтобы подключиться к созданной базе данных:</span><span class="sxs-lookup"><span data-stu-id="0f205-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="0f205-190">Создание таблиц в базе данных</span><span class="sxs-lookup"><span data-stu-id="0f205-190">Create tables in the database</span></span>
<span data-ttu-id="0f205-191">Теперь, когда вы знаете, как подключиться к базе данных Azure для MySQL, рассмотрим, как выполнить некоторые основные задачи.</span><span class="sxs-lookup"><span data-stu-id="0f205-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="0f205-192">Сначала можно создать таблицу и заполнить ее некоторыми данными.</span><span class="sxs-lookup"><span data-stu-id="0f205-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="0f205-193">Давайте создадим таблицу, в которой хранятся данные инвентаризации.</span><span class="sxs-lookup"><span data-stu-id="0f205-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="0f205-194">Загрузка данных в таблицу</span><span class="sxs-lookup"><span data-stu-id="0f205-194">Load data into the tables</span></span>
<span data-ttu-id="0f205-195">Теперь, когда таблица создана, мы можем вставить в нее данные.</span><span class="sxs-lookup"><span data-stu-id="0f205-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="0f205-196">Чтобы вставить некоторые строки данных, в открытом окне командной строки выполните следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="0f205-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="0f205-197">Итак, в созданной ранее таблице содержится две строки данных.</span><span class="sxs-lookup"><span data-stu-id="0f205-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="0f205-198">Запрос и обновление данных в таблицах</span><span class="sxs-lookup"><span data-stu-id="0f205-198">Query and update the data in the tables</span></span>
<span data-ttu-id="0f205-199">Чтобы извлечь сведения из таблицы базы данных, выполните приведенный ниже запрос.</span><span class="sxs-lookup"><span data-stu-id="0f205-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="0f205-200">Вы можете также обновить данные в таблицах, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0f205-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="0f205-201">При извлечении данных строка будет обновляться соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="0f205-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="0f205-202">Восстановление базы данных до предыдущей точки во времени</span><span class="sxs-lookup"><span data-stu-id="0f205-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="0f205-203">Предположим, вы случайно удалили важную таблицу из базы данных и вам не удается легко восстановить данные.</span><span class="sxs-lookup"><span data-stu-id="0f205-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="0f205-204">База данных Azure для MySQL позволяет восстановить сервер до точки во времени, создав копии баз данных на новом сервере.</span><span class="sxs-lookup"><span data-stu-id="0f205-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="0f205-205">Вы можете восстановить удаленные данные с помощью нового сервера.</span><span class="sxs-lookup"><span data-stu-id="0f205-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="0f205-206">Указанные ниже шаги позволяют восстановить сервер до точки во времени, когда была создана таблица.</span><span class="sxs-lookup"><span data-stu-id="0f205-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="0f205-207">На портале Azure найдите базу данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f205-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="0f205-208">На странице **Обзор** на панели инструментов щелкните **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="0f205-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="0f205-209">Откроется страница "Восстановление".</span><span class="sxs-lookup"><span data-stu-id="0f205-209">The Restore page opens.</span></span>

   ![10.1. Восстановление базы данных](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="0f205-211">Заполните форму **Восстановление**, указав следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="0f205-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10.2. Форма восстановления](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="0f205-213">**Точка восстановления**. Выберите точку во времени, до которой требуется восстановить данные, в пределах указанного периода времени.</span><span class="sxs-lookup"><span data-stu-id="0f205-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="0f205-214">Обязательно преобразуйте свое местное время в формат UTC.</span><span class="sxs-lookup"><span data-stu-id="0f205-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="0f205-215">**Восстановить на новом сервере**. Укажите имя нового сервера, на который нужно восстановить данные.</span><span class="sxs-lookup"><span data-stu-id="0f205-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="0f205-216">**Расположение**. Регион совпадает с исходным сервером и не может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="0f205-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="0f205-217">**Ценовая категория**. Ценовая категория совпадает с исходным сервером и не может быть изменена.</span><span class="sxs-lookup"><span data-stu-id="0f205-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="0f205-218">Чтобы [восстановить сервер до точки во времени](./howto-restore-server-portal.md) перед удалением таблицы, нажмите кнопку **OК**.</span><span class="sxs-lookup"><span data-stu-id="0f205-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="0f205-219">Восстановление сервера приведет к созданию новой копии сервера на заданный момент времени.</span><span class="sxs-lookup"><span data-stu-id="0f205-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0f205-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f205-220">Next steps</span></span>
<span data-ttu-id="0f205-221">Из этого руководства вы узнали, как с помощью портала Azure выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="0f205-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0f205-222">создание базы данных Azure для MySQL;</span><span class="sxs-lookup"><span data-stu-id="0f205-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="0f205-223">настройка брандмауэра сервера;</span><span class="sxs-lookup"><span data-stu-id="0f205-223">Configure the server firewall</span></span>
> * <span data-ttu-id="0f205-224">использование программы командной строки MySQL для создания базы данных;</span><span class="sxs-lookup"><span data-stu-id="0f205-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="0f205-225">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="0f205-225">Load sample data</span></span>
> * <span data-ttu-id="0f205-226">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="0f205-226">Query data</span></span>
> * <span data-ttu-id="0f205-227">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="0f205-227">Update data</span></span>
> * <span data-ttu-id="0f205-228">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="0f205-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f205-229">Как подключить приложения к базе данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="0f205-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
