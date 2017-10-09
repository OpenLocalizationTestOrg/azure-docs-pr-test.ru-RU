---
title: "aaaDesign первый Azure базы данных для базы данных MySQL - портал Azure | Документы Microsoft"
description: "В этом учебнике описано как toocreate и управления базой данных Azure для MySQL server и базы данных с помощью портала Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="f4347-103">Проектирование первой базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="f4347-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="f4347-104">База данных Azure для MySQL является управляемой службы, которая позволяет toorun, управлять и масштабировать высокодоступных баз данных MySQL в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="f4347-105">С помощью hello портал Azure, можно легко управлять сервером и разработке базы данных.</span><span class="sxs-lookup"><span data-stu-id="f4347-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="f4347-106">В этом учебнике используется hello Azure портала toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="f4347-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4347-107">создание базы данных Azure для MySQL;</span><span class="sxs-lookup"><span data-stu-id="f4347-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="f4347-108">Настройте брандмауэр сервера hello</span><span class="sxs-lookup"><span data-stu-id="f4347-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="f4347-109">Используйте средство командной строки mysql toocreate базы данных</span><span class="sxs-lookup"><span data-stu-id="f4347-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="f4347-110">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="f4347-110">Load sample data</span></span>
> * <span data-ttu-id="f4347-111">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="f4347-111">Query data</span></span>
> * <span data-ttu-id="f4347-112">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="f4347-112">Update data</span></span>
> * <span data-ttu-id="f4347-113">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="f4347-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="f4347-114">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f4347-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="f4347-115">Откройте избранных веб-браузере и войдите hello [портал Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f4347-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="f4347-116">Введите ваш toosign учетные данные на портале toohello.</span><span class="sxs-lookup"><span data-stu-id="f4347-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="f4347-117">представление по умолчанию Hello, панели мониторинга службы.</span><span class="sxs-lookup"><span data-stu-id="f4347-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="f4347-118">Создание сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="f4347-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="f4347-119">Сервер базы данных Azure для MySQL создается с определенным набором [вычислительных ресурсов и ресурсов хранения](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f4347-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="f4347-120">сервер Hello создается в пределах [группы ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="f4347-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="f4347-121">Перейдите в слишком**баз данных** > **базы данных Azure для MySQL**.</span><span class="sxs-lookup"><span data-stu-id="f4347-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="f4347-122">Если не удается найти сервер MySQL в группе **баз данных** категории, нажмите кнопку **все** tooshow все доступные службы баз данных.</span><span class="sxs-lookup"><span data-stu-id="f4347-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="f4347-123">Можно также ввести **базы данных Azure для MySQL** в tooquickly поле поиска hello найдите службу hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="f4347-124">![Навигатор tooMySQL 2-1](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="f4347-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="f4347-125">Щелкните элемент **База данных Azure для MySQL**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f4347-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="f4347-126">В нашем примере заполните hello базы данных Azure для MySQL формы с hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="f4347-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="f4347-127">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="f4347-127">**Setting**</span></span> | <span data-ttu-id="f4347-128">**Рекомендуемое значение**</span><span class="sxs-lookup"><span data-stu-id="f4347-128">**Suggested value**</span></span> | <span data-ttu-id="f4347-129">**Описание поля**</span><span class="sxs-lookup"><span data-stu-id="f4347-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="f4347-130">*Server name* (Имя сервера)</span><span class="sxs-lookup"><span data-stu-id="f4347-130">*Server name*</span></span> | <span data-ttu-id="f4347-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="f4347-131">myserver4demo</span></span>  | <span data-ttu-id="f4347-132">Имя сервера содержит toobe глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="f4347-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="f4347-133">*Подписка*</span><span class="sxs-lookup"><span data-stu-id="f4347-133">*Subscription*</span></span> | <span data-ttu-id="f4347-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="f4347-134">mysubscription</span></span> | <span data-ttu-id="f4347-135">Выберите подписку из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="f4347-136">*Группа ресурсов*</span><span class="sxs-lookup"><span data-stu-id="f4347-136">*Resource group*</span></span> | <span data-ttu-id="f4347-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="f4347-137">myresourcegroup</span></span> | <span data-ttu-id="f4347-138">Создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="f4347-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="f4347-139">*Имя для входа администратора сервера*</span><span class="sxs-lookup"><span data-stu-id="f4347-139">*Server admin login*</span></span> | <span data-ttu-id="f4347-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="f4347-140">myadmin</span></span> | <span data-ttu-id="f4347-141">Укажите имя учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="f4347-141">Setup admin account name.</span></span> |
| <span data-ttu-id="f4347-142">*Пароль*</span><span class="sxs-lookup"><span data-stu-id="f4347-142">*Password*</span></span> |  | <span data-ttu-id="f4347-143">Укажите надежный пароль для учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="f4347-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="f4347-144">*Подтверждение пароля.*</span><span class="sxs-lookup"><span data-stu-id="f4347-144">*Confirm password*</span></span> |  | <span data-ttu-id="f4347-145">Подтвердите пароль учетной записи администратора hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="f4347-146">*Расположение*</span><span class="sxs-lookup"><span data-stu-id="f4347-146">*Location*</span></span> |  | <span data-ttu-id="f4347-147">Выберите доступный регион.</span><span class="sxs-lookup"><span data-stu-id="f4347-147">Select an available region.</span></span> |
| <span data-ttu-id="f4347-148">*Версия*</span><span class="sxs-lookup"><span data-stu-id="f4347-148">*Version*</span></span> | <span data-ttu-id="f4347-149">5.7</span><span class="sxs-lookup"><span data-stu-id="f4347-149">5.7</span></span> | <span data-ttu-id="f4347-150">Выберите последнюю версию hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="f4347-151">*Настройка производительности*</span><span class="sxs-lookup"><span data-stu-id="f4347-151">*Configure performance*</span></span> | <span data-ttu-id="f4347-152">"Базовый", 50 единиц вычислений, 50 ГБ</span><span class="sxs-lookup"><span data-stu-id="f4347-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="f4347-153">Укажите значения для параметров **Ценовая категория**, **Единицы вычислений**, **Хранилище (ГБ)** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f4347-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="f4347-154">*TooDashboard ПИН-кода*</span><span class="sxs-lookup"><span data-stu-id="f4347-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="f4347-155">Проверка</span><span class="sxs-lookup"><span data-stu-id="f4347-155">Check</span></span> | <span data-ttu-id="f4347-156">Рекомендуется toocheck этот флажок, поэтому может оказаться hello server легко позже на</span><span class="sxs-lookup"><span data-stu-id="f4347-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="f4347-157">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f4347-157">Then, click **Create**.</span></span> <span data-ttu-id="f4347-158">В одну-две минуты в облаке hello выполняется новой базы данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="f4347-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="f4347-159">Можно щелкнуть **уведомления** кнопку на панели инструментов toomonitor hello hello-процесс развертывания.</span><span class="sxs-lookup"><span data-stu-id="f4347-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="f4347-160">Настройка брандмауэра</span><span class="sxs-lookup"><span data-stu-id="f4347-160">Configure firewall</span></span>
<span data-ttu-id="f4347-161">Базы данных Azure для MySQL защищены брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="f4347-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="f4347-162">По умолчанию все соединения toohello сервера hello базы данных и внутри сервера hello, отклоняются.</span><span class="sxs-lookup"><span data-stu-id="f4347-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="f4347-163">Прежде чем подключаться tooAzure базы данных MySQL для hello первый раз, настройте IP-адрес общедоступной сети hello брандмауэра tooadd hello на компьютере клиента (или диапазон IP-адресов).</span><span class="sxs-lookup"><span data-stu-id="f4347-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="f4347-164">Щелкните созданный сервер и выберите **Безопасность подключения**.</span><span class="sxs-lookup"><span data-stu-id="f4347-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="f4347-165">![3.1. Безопасность подключения](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="f4347-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="f4347-166">Здесь вы можете **добавить свой IP-адрес** или настроить правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f4347-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="f4347-167">Помните, tooclick **Сохранить** после создания правила hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="f4347-168">Теперь можно подключиться toohello сервера с помощью средства командной строки mysql или средство графического интерфейса пользователя MySQL рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="f4347-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="f4347-169">Сервер базы данных Azure для MySQL обменивается данными через порт 3306.</span><span class="sxs-lookup"><span data-stu-id="f4347-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="f4347-170">Если вы пытаетесь tooconnect из корпоративной сети, исходящий трафик через порт 3306 может оказаться невозможным брандмауэром вашей сети.</span><span class="sxs-lookup"><span data-stu-id="f4347-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="f4347-171">В этом случае tooAzure MySQL server не удается подключиться, если ИТ-отдел открывает порт 3306.</span><span class="sxs-lookup"><span data-stu-id="f4347-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="f4347-172">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="f4347-172">Get connection information</span></span>
<span data-ttu-id="f4347-173">Полное hello Get **имя сервера** и **имя входа администратора сервера** для базы данных Azure для сервера MySQL из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f4347-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="f4347-174">Можно использовать hello полное имя tooconnect tooyour сервер с помощью средства командной строки mysql.</span><span class="sxs-lookup"><span data-stu-id="f4347-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="f4347-175">В [портал Azure](https://portal.azure.com/), нажмите кнопку **все ресурсы** из левого меню hello, имя типа hello и поиск для базы данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="f4347-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="f4347-176">Выберите данные hello tooview имени сервера hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="f4347-177">В разделе hello параметров щелкните **свойства**.</span><span class="sxs-lookup"><span data-stu-id="f4347-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="f4347-178">Запишите значения параметров **Имя сервера** и **Имя для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="f4347-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="f4347-179">Можно щелкнуть hello скопировать кнопку Далее tooeach поле toocopy toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="f4347-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="f4347-180">![4.2. Свойства сервера](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="f4347-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="f4347-181">В этом примере — имя сервера hello *myserver4demo.mysql.database.azure.com*, и имя входа администратора сервера hello является  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="f4347-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="f4347-182">Подключиться с помощью mysql server toohello</span><span class="sxs-lookup"><span data-stu-id="f4347-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="f4347-183">Используйте [средство командной строки mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish tooyour подключения базы данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="f4347-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="f4347-184">Средство командной строки mysql hello можно запустить hello оболочки облако Azure в обозревателе hello с компьютера с помощью средства mysql установлены локально.</span><span class="sxs-lookup"><span data-stu-id="f4347-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="f4347-185">hello toolaunch оболочки облако Azure, щелкните hello `Try It` на блок кода в этой статье, или посетите портал Azure hello и нажмите кнопку hello `>_` значок в верхней правой панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="f4347-186">Введите команду tooconnect hello:</span><span class="sxs-lookup"><span data-stu-id="f4347-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="f4347-187">Создание пустой базы данных</span><span class="sxs-lookup"><span data-stu-id="f4347-187">Create a blank database</span></span>
<span data-ttu-id="f4347-188">Когда вы будете toohello подключенного сервера, создайте toowork пустую базу данных с.</span><span class="sxs-lookup"><span data-stu-id="f4347-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="f4347-189">В строке приветствия выполните hello, следующая команда tooswitch подключение к только что созданный toothis базе данных:</span><span class="sxs-lookup"><span data-stu-id="f4347-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="f4347-190">Создание таблиц в базе данных hello</span><span class="sxs-lookup"><span data-stu-id="f4347-190">Create tables in hello database</span></span>
<span data-ttu-id="f4347-191">Теперь, когда вы знаете, как tooconnect toohello базы данных Azure для базы данных MySQL, мы можем открыть как toocomplete некоторых базовых задач.</span><span class="sxs-lookup"><span data-stu-id="f4347-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="f4347-192">Сначала можно создать таблицу и заполнить ее некоторыми данными.</span><span class="sxs-lookup"><span data-stu-id="f4347-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="f4347-193">Давайте создадим таблицу, в которой хранятся данные инвентаризации.</span><span class="sxs-lookup"><span data-stu-id="f4347-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="f4347-194">Загрузка данных в таблицы hello</span><span class="sxs-lookup"><span data-stu-id="f4347-194">Load data into hello tables</span></span>
<span data-ttu-id="f4347-195">Теперь, когда таблица создана, мы можем вставить в нее данные.</span><span class="sxs-lookup"><span data-stu-id="f4347-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="f4347-196">Привет открыть окно командной строки запустите следующий запрос tooinsert hello некоторых строк данных.</span><span class="sxs-lookup"><span data-stu-id="f4347-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="f4347-197">Теперь у вас две строки образца данных в таблицу hello, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="f4347-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="f4347-198">Запрашивать и обновлять данные hello в таблицах hello</span><span class="sxs-lookup"><span data-stu-id="f4347-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="f4347-199">Выполните следующую информацию tooretrieve запроса из таблицы базы данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="f4347-200">Можно также обновить данные hello в таблицах hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="f4347-201">Строка Hello обновляется соответствующим образом при извлечении данных.</span><span class="sxs-lookup"><span data-stu-id="f4347-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="f4347-202">Восстановление предыдущей точки tooa базы данных времени</span><span class="sxs-lookup"><span data-stu-id="f4347-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="f4347-203">Представьте, что случайно удалили таблицу важные базы данных, невозможно было легко восстановить данные hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="f4347-204">Базы данных Azure для MySQL позволяет toorestore hello server tooa точки времени, создав копию hello баз данных на новый сервер.</span><span class="sxs-lookup"><span data-stu-id="f4347-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="f4347-205">Можно использовать этот новый сервер toorecover удаленные данные.</span><span class="sxs-lookup"><span data-stu-id="f4347-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="f4347-206">Здравствуйте, следующая точка tooa сервера образец hello действия восстановления перед hello таблица была добавлена.</span><span class="sxs-lookup"><span data-stu-id="f4347-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="f4347-207">Найдите базу данных Azure для MySQL hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f4347-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="f4347-208">На hello **Обзор** щелкните **восстановить** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="f4347-209">Откроется страница приветствия восстановления.</span><span class="sxs-lookup"><span data-stu-id="f4347-209">hello Restore page opens.</span></span>

   ![10.1. Восстановление базы данных](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="f4347-211">Заполните hello **восстановить** формы с hello необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="f4347-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![10.2. Форма восстановления](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="f4347-213">**Точка восстановления**: выберите в момент, которые должны toorestore, в течение периода времени hello в списке.</span><span class="sxs-lookup"><span data-stu-id="f4347-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="f4347-214">Убедитесь, что tooconvert tooUTC ваш локальный часовой пояс.</span><span class="sxs-lookup"><span data-stu-id="f4347-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="f4347-215">**Восстановление сервера toonew**: Введите имя нового сервера требуется toorestore для.</span><span class="sxs-lookup"><span data-stu-id="f4347-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="f4347-216">**Расположение**: hello региона совпадает с исходного сервера hello и не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="f4347-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="f4347-217">**Ценовая категория**: hello ценовой категории — hello таким же, как hello исходный сервер и не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="f4347-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="f4347-218">Нажмите кнопку **ОК** toorestore hello server слишком[моментов времени tooa](./howto-restore-server-portal.md) перед hello таблица была удалена.</span><span class="sxs-lookup"><span data-stu-id="f4347-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="f4347-219">Восстановление сервера создает новую копию hello server, на момент времени, заданного hello.</span><span class="sxs-lookup"><span data-stu-id="f4347-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f4347-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4347-220">Next steps</span></span>
<span data-ttu-id="f4347-221">В этом учебнике используется hello Azure портала toolearned как для:</span><span class="sxs-lookup"><span data-stu-id="f4347-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4347-222">создание базы данных Azure для MySQL;</span><span class="sxs-lookup"><span data-stu-id="f4347-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="f4347-223">Настройте брандмауэр сервера hello</span><span class="sxs-lookup"><span data-stu-id="f4347-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="f4347-224">Используйте средство командной строки mysql toocreate базы данных</span><span class="sxs-lookup"><span data-stu-id="f4347-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="f4347-225">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="f4347-225">Load sample data</span></span>
> * <span data-ttu-id="f4347-226">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="f4347-226">Query data</span></span>
> * <span data-ttu-id="f4347-227">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="f4347-227">Update data</span></span>
> * <span data-ttu-id="f4347-228">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="f4347-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4347-229">Как tooAzure tooconnect приложений базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="f4347-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
