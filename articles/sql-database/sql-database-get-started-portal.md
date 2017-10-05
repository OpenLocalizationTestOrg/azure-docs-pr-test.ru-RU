---
title: "Портал Azure: создание базы данных SQL | Документация Майкрософт"
description: "Вы узнаете, как создать логический сервер базы данных SQL, правило брандмауэра на уровне сервера и базы данных на портале Azure, Вы также научитесь отправлять запрос к базе данных SQL Azure с помощью портала Azure."
keywords: "руководство по базам данных SQL, создание базы данных SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: a863cf3ad08040906850f64db6505f30bcfa72eb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-sql-database-in-the-azure-portal"></a><span data-ttu-id="5fa5e-105">Создание базы данных SQL Azure на портале Azure</span><span class="sxs-lookup"><span data-stu-id="5fa5e-105">Create an Azure SQL database in the Azure portal</span></span>

<span data-ttu-id="5fa5e-106">Это краткое руководство содержит пошаговые инструкции по созданию базы данных SQL на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-106">This quick start tutorial walks through how to create a SQL database in Azure.</span></span> <span data-ttu-id="5fa5e-107">База данных SQL Azure — это база данных как услуга, которая позволяет запускать и масштабировать высокодоступные базы данных SQL Server в облаке.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you to run and scale highly available SQL Server databases in the cloud.</span></span> <span data-ttu-id="5fa5e-108">В этом кратком руководстве объясняется, как начать работу, создав базу данных SQL с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-108">This quick start shows you how to get started by creating a SQL database using the Azure portal.</span></span>

<span data-ttu-id="5fa5e-109">Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="5fa5e-110">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-110">Log in to the Azure portal</span></span>

<span data-ttu-id="5fa5e-111">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="5fa5e-112">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="5fa5e-112">Create a SQL database</span></span>

<span data-ttu-id="5fa5e-113">База данных Azure SQL создается с определенным набором [вычислительных ресурсов и ресурсов хранения](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="5fa5e-114">База данных создается в пределах [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) и [логического сервера базы данных SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-114">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="5fa5e-115">Выполните следующие действия, чтобы создать базу данных SQL, содержащую образец данных Adventure Works LT.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-115">Follow these steps to create a SQL database containing the Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="5fa5e-116">Щелкните **Создать** в верхнем левом углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-116">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="5fa5e-117">Выберите **Базы данных** на странице **создания** и щелкните **База данных SQL** на странице **Базы данных**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-117">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span>

   ![Создание базы данных — 1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="5fa5e-119">Заполните форму базы данных SQL, указав следующую информацию, как показано на предыдущем рисунке.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-119">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="5fa5e-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="5fa5e-120">Setting</span></span>       | <span data-ttu-id="5fa5e-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="5fa5e-121">Suggested value</span></span> | <span data-ttu-id="5fa5e-122">Описание</span><span class="sxs-lookup"><span data-stu-id="5fa5e-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="5fa5e-123">**Database name** (Имя базы данных)</span><span class="sxs-lookup"><span data-stu-id="5fa5e-123">**Database name**</span></span> | <span data-ttu-id="5fa5e-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="5fa5e-124">mySampleDatabase</span></span> | <span data-ttu-id="5fa5e-125">Допустимые имена баз данных см. в статье об [идентификаторах базы данных](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="5fa5e-126">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="5fa5e-126">**Subscription**</span></span> | <span data-ttu-id="5fa5e-127">Ваша подписка</span><span class="sxs-lookup"><span data-stu-id="5fa5e-127">Your subscription</span></span>  | <span data-ttu-id="5fa5e-128">Дополнительные сведения о подписках см. [здесь](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="5fa5e-129">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="5fa5e-129">**Resource group**</span></span>  | <span data-ttu-id="5fa5e-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5fa5e-130">myResourceGroup</span></span> | <span data-ttu-id="5fa5e-131">Допустимые имена групп ресурсов см. в статье о [правилах и ограничениях именования](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="5fa5e-132">**Источник**</span><span class="sxs-lookup"><span data-stu-id="5fa5e-132">**Source source**</span></span> | <span data-ttu-id="5fa5e-133">Пример (AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="5fa5e-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="5fa5e-134">Загружает схему и данные AdventureWorksLT в новую базу данных</span><span class="sxs-lookup"><span data-stu-id="5fa5e-134">Loads the AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="5fa5e-135">Необходимо выбрать пример базы данных этой формы, так как она используется в оставшейся части этого руководства.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-135">You must select the sample database on this form because it is used in the remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="5fa5e-136">В разделе **Сервер** щелкните **Настроить необходимые параметры** и заполните форму SQL Server (логический сервер), указав следующую информацию, как показано на указанном ниже изображении.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-136">Under **Server**, click **Configure required settings** and fill out the SQL server (logical server) form with the following information, as shown on the following image:</span></span>   

   | <span data-ttu-id="5fa5e-137">Настройка</span><span class="sxs-lookup"><span data-stu-id="5fa5e-137">Setting</span></span>       | <span data-ttu-id="5fa5e-138">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="5fa5e-138">Suggested value</span></span> | <span data-ttu-id="5fa5e-139">Описание</span><span class="sxs-lookup"><span data-stu-id="5fa5e-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="5fa5e-140">**Server name** (Имя сервера)</span><span class="sxs-lookup"><span data-stu-id="5fa5e-140">**Server name**</span></span> | <span data-ttu-id="5fa5e-141">Любое глобально уникальное имя</span><span class="sxs-lookup"><span data-stu-id="5fa5e-141">Any globally unique name</span></span> | <span data-ttu-id="5fa5e-142">Допустимые имена серверов см. в статье о [правилах и ограничениях именования](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="5fa5e-143">**Имя для входа администратора сервера**</span><span class="sxs-lookup"><span data-stu-id="5fa5e-143">**Server admin login**</span></span> | <span data-ttu-id="5fa5e-144">Любое допустимое имя</span><span class="sxs-lookup"><span data-stu-id="5fa5e-144">Any valid name</span></span> | <span data-ttu-id="5fa5e-145">Допустимые имена входа см. в статье об [идентификаторах базы данных](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="5fa5e-146">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="5fa5e-146">**Password**</span></span> | <span data-ttu-id="5fa5e-147">Любой допустимый пароль</span><span class="sxs-lookup"><span data-stu-id="5fa5e-147">Any valid password</span></span> | <span data-ttu-id="5fa5e-148">Длина пароля должна составлять минимум 8 символов. Пароль должен содержать символы трех категорий из перечисленных: прописные буквы, строчные буквы, цифры и специальные символы.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-148">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="5fa5e-149">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="5fa5e-149">**Subscription**</span></span> | <span data-ttu-id="5fa5e-150">Ваша подписка</span><span class="sxs-lookup"><span data-stu-id="5fa5e-150">Your subscription</span></span> | <span data-ttu-id="5fa5e-151">Дополнительные сведения о подписках см. [здесь](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="5fa5e-152">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="5fa5e-152">**Resource group**</span></span> | <span data-ttu-id="5fa5e-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5fa5e-153">myResourceGroup</span></span> | <span data-ttu-id="5fa5e-154">Допустимые имена групп ресурсов см. в статье о [правилах и ограничениях именования](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="5fa5e-155">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="5fa5e-155">**Location**</span></span> | <span data-ttu-id="5fa5e-156">Любое допустимое расположение</span><span class="sxs-lookup"><span data-stu-id="5fa5e-156">Any valid location</span></span> | <span data-ttu-id="5fa5e-157">Дополнительные сведения о регионах Azure см. [здесь](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="5fa5e-158">Указанные здесь учетные данные и пароль администратора сервера понадобятся позже в этом руководстве, чтобы войти на сервер и в его базу данных.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-158">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="5fa5e-159">Запомните или запишите эту информацию для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-159">Remember or record this information for later use.</span></span> 
   >  

   ![Создание базы данных — сервер](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="5fa5e-161">Заполнив форму, щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-161">When you have completed the form, click **Select**.</span></span>

6. <span data-ttu-id="5fa5e-162">Щелкните **Ценовая категория**, чтобы указать уровень производительности и уровень служб для новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="5fa5e-163">Воспользуйтесь ползунком, чтобы выбрать **20 DTU** и хранилище объемом **250** ГБ.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-163">Use the slider to select **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="5fa5e-164">Дополнительные сведения о DTU см. в статье [Общие сведения об обычных единицах передачи данных (DTU) и единицах передачи данных в эластичной базе данных (eDTU)](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="5fa5e-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![Создание базы данных — s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="5fa5e-166">Выбрав необходимое количество единиц DTU, нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-166">After selected the amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="5fa5e-167">Заполнив форму базы данных SQL, нажмите кнопку **Создать**, чтобы подготовить базу данных.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-167">Now that you have completed the SQL Database form, click **Create** to provision the database.</span></span> <span data-ttu-id="5fa5e-168">Подготовка занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="5fa5e-169">На панели инструментов щелкните **Уведомления**, чтобы отслеживать процесс развертывания.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-169">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![уведомление](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="5fa5e-171">создадим правило брандмауэра на уровне сервера;</span><span class="sxs-lookup"><span data-stu-id="5fa5e-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="5fa5e-172">Служба базы данных SQL создает брандмауэр уровня сервера, который не позволяет внешним приложениям и средствам подключаться к серверу или любой базе данных на сервере, если не создано правило брандмауэра, открывающее брандмауэр для определенных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-172">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="5fa5e-173">Выполните следующие действия, чтобы создать [правило брандмауэра уровня сервера базы данных SQL](sql-database-firewall-configure.md) для IP-адреса вашего клиента и разрешить внешнее подключение через брандмауэр базы данных SQL только с вашего IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-173">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="5fa5e-174">База данных SQL обменивается данными через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="5fa5e-175">Если вы пытаетесь подключиться из корпоративной сети, исходящий трафик через порт 1433 может быть запрещен сетевым брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-175">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5fa5e-176">В таком случае вы не сможете подключиться к серверу базы данных SQL Azure, пока ваш ИТ-отдел не откроет порт 1433.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-176">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="5fa5e-177">По завершении развертывания щелкните раздел **Базы данных SQL** в меню слева и выберите **mySampleDatabase** на странице **баз данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-177">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="5fa5e-178">Откроется страница с общими сведениями о базе данных, где будет указано полное имя сервера (например, **mynewserver20170313.database.windows.net**) и предоставлены параметры для дальнейшей настройки.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-178">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="5fa5e-179">Скопируйте полное имя сервера для использования в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5fa5e-180">Полное имя сервера понадобится вам при работе с последующими руководствами для подключения к серверу и к базам данных.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-180">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![Имя сервера](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="5fa5e-182">Щелкните **Настройка брандмауэра для сервера** на панели инструментов, как показано на предыдущем рисунке.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-182">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="5fa5e-183">Откроется страница **параметров брандмауэра** для сервера базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-183">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![правило брандмауэра для сервера](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="5fa5e-185">На панели инструментов щелкните **Добавить IP-адрес клиента**, чтобы добавить текущий IP-адрес в новое правило брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-185">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="5fa5e-186">С использованием правила брандмауэра можно открыть порт 1433 для одного IP-адреса или диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="5fa5e-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-187">Click **Save**.</span></span> <span data-ttu-id="5fa5e-188">Для текущего IP-адреса будет создано правило брандмауэра уровня сервера, с помощью которого можно открыть порт 1433 логического сервера.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-188">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![Настройка правила брандмауэра для сервера](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="5fa5e-190">Нажмите кнопку **ОК**, а затем закройте страницу **Параметры брандмауэра**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-190">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="5fa5e-191">Теперь можно подключиться с этого IP-адреса к серверу базы данных SQL и его базам данных с помощью SQL Server Management Studio или другого средства по своему усмотрению, используя учетную запись администратора сервера, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-191">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fa5e-192">По умолчанию доступ через брандмауэр базы данных SQL включен для всех служб Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-192">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="5fa5e-193">На этой странице щелкните **Откл.**, чтобы отключить доступ для всех служб Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-193">Click **OFF** on this page to disable for all Azure services.</span></span>
>

## <a name="query-the-sql-database"></a><span data-ttu-id="5fa5e-194">Отправка запросов к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="5fa5e-194">Query the SQL database</span></span>

<span data-ttu-id="5fa5e-195">После создания примера базы данных в Azure можно воспользоваться встроенным средством запроса на портале Azure, чтобы убедится, что вы сможете подключиться к базе данных и выполнить запрос данных.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-195">Now that you have created a sample database in Azure, let’s use the built-in query tool within the Azure portal to confirm that you can connect to the database and query the data.</span></span> 

1. <span data-ttu-id="5fa5e-196">На странице базы данных SQL нажмите кнопку **Средства** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-196">On the SQL Database page for your database, click **Tools** on the toolbar.</span></span> <span data-ttu-id="5fa5e-197">Откроется страница **Средства**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-197">The **Tools** page opens.</span></span>

   ![меню средств](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="5fa5e-199">Щелкните **Редактор запросов (предварительная версия)**, а затем установите флажок напротив пункта **Условия предварительной версии** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-199">Click **Query editor (preview)**, click the **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="5fa5e-200">Откроется страница редактора запросов.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-200">The Query editor page opens.</span></span>

3. <span data-ttu-id="5fa5e-201">Щелкните **Вход** и при появлении запроса выберите **Проверка подлинности SQL Server**, а затем укажите учетные данные и пароль администратора сервера, созданные ранее.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide the server admin login and password that you created earlier.</span></span>

   ![вход](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="5fa5e-203">Нажмите кнопку **ОК**, чтобы выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-203">Click **OK** to log in.</span></span>

5. <span data-ttu-id="5fa5e-204">После проверки подлинности в области редактора запросов введите следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-204">After you are authenticated, type the following query in the query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="5fa5e-205">Щелкните **Выполнить** и просмотрите результаты запроса в области **Результаты**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-205">Click **Run** and then review the query results in the **Results** pane.</span></span>

   ![результаты редактора запросов](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="5fa5e-207">Закройте страницу **редактора запросов** и страницу **Средства**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-207">Close the **Query editor** page and the **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="5fa5e-208">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="5fa5e-208">Clean up resources</span></span>

<span data-ttu-id="5fa5e-209">Если эти ресурсы не требуются для изучения другого руководства (см. раздел [Дальнейшие действия](#next-steps)), их можно удалить, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="5fa5e-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing the following:</span></span>


1. <span data-ttu-id="5fa5e-210">В меню слева на портале Azure щелкните **Группы ресурсов**, а затем выберите **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-210">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="5fa5e-211">На странице группы ресурсов щелкните **Удалить**, в текстовом поле введите **myResourceGroup** и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-211">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fa5e-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5fa5e-212">Next steps</span></span>

<span data-ttu-id="5fa5e-213">Теперь, когда у вас есть база данных, вы можете подключиться и создать запрос, используя привычные средства.</span><span class="sxs-lookup"><span data-stu-id="5fa5e-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="5fa5e-214">См. дополнительные сведения о доступных средствах:</span><span class="sxs-lookup"><span data-stu-id="5fa5e-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="5fa5e-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5fa5e-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="5fa5e-216">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5fa5e-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="5fa5e-217">.NET</span><span class="sxs-lookup"><span data-stu-id="5fa5e-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="5fa5e-218">PHP</span><span class="sxs-lookup"><span data-stu-id="5fa5e-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="5fa5e-219">Node.js</span><span class="sxs-lookup"><span data-stu-id="5fa5e-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="5fa5e-220">Java</span><span class="sxs-lookup"><span data-stu-id="5fa5e-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="5fa5e-221">Python</span><span class="sxs-lookup"><span data-stu-id="5fa5e-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="5fa5e-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="5fa5e-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
