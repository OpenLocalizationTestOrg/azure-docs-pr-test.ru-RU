---
title: "Приступая к работе aaaAzure хранилище данных SQL - учебник | Документы Microsoft"
description: "В этом учебнике показано как tooprovision и загрузка данных в хранилище данных SQL Azure. Вы также узнаете hello основные сведения о масштабировании, приостановка и настройке."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="1f4df-104">Начало работы с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="1f4df-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="1f4df-105">В этом учебнике показано как tooprovision и загрузка данных в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="1f4df-106">Вы также узнаете hello основные сведения о масштабировании, приостановка и настройке.</span><span class="sxs-lookup"><span data-stu-id="1f4df-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="1f4df-107">После завершения вам быть готовы tooquery и просмотр хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="1f4df-108">**Предполагаемое время toocomplete:** это учебник законченный пример кода, принимающий toocomplete около 30 минут после выполнены необходимые условия hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1f4df-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1f4df-109">Prerequisites</span></span>

<span data-ttu-id="1f4df-110">Hello учебнике предполагается, что вы знакомы с основными понятиями хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1f4df-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="1f4df-111">Если это не так, рекомендуем прочитать статью [Что такое хранилище данных SQL](sql-data-warehouse-overview-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="1f4df-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="1f4df-112">Зарегистрируйтесь для Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1f4df-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="1f4df-113">Если у вас еще нет учетной записи Microsoft Azure, вы должны toosign для использования одного toouse этой службы.</span><span class="sxs-lookup"><span data-stu-id="1f4df-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="1f4df-114">Если у вас уже есть учетная запись, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="1f4df-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="1f4df-115">Переходить по страницам учетной записи toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="1f4df-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="1f4df-116">Создайте бесплатную учетную запись Azure или купите платную.</span><span class="sxs-lookup"><span data-stu-id="1f4df-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="1f4df-117">Следуйте инструкциям hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="1f4df-118">Установка соответствующих клиентских драйверов и средств SQL</span><span class="sxs-lookup"><span data-stu-id="1f4df-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="1f4df-119">Большая часть клиентских средств SQL можно подключаться tooSQL хранилища данных с помощью JDBC, ODBC или ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="1f4df-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="1f4df-120">Из-за toohello большое количество функций T-SQL, которые поддерживает хранилище данных SQL для некоторых клиентских приложений не полностью совместимы с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1f4df-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="1f4df-121">Если вы работаете с ОС Windows, рекомендуем использовать либо [Visual Studio], либо [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="1f4df-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="1f4df-122">Создание хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="1f4df-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="1f4df-123">Хранилище данных SQL — это специальный тип базы данных, предназначенный для вычислений массовым параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="1f4df-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="1f4df-124">Hello базы данных, распределенные по нескольким узлам и обрабатывает запросы параллельно.</span><span class="sxs-lookup"><span data-stu-id="1f4df-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="1f4df-125">Хранилище данных SQL имеет узел элемента управления, который координирует действия hello всех узлов hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="1f4df-126">сами по себе узлы Hello использования базы данных SQL toomanage данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="1f4df-127">Создание хранилища данных SQL может привести к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="1f4df-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="1f4df-128">Дополнительные сведения см. на странице [цен на хранилище данных SQL](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="1f4df-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="1f4df-129">Создание хранилища данных</span><span class="sxs-lookup"><span data-stu-id="1f4df-129">Create a data warehouse</span></span>

1. <span data-ttu-id="1f4df-130">Вход в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f4df-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1f4df-131">Последовательно выберите **Создать** > **Базы данных** > **Хранилище данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="1f4df-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="1f4df-132">![Новая колонка](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![Выбор хранилища данных](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="1f4df-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="1f4df-133">Укажите сведения о развертывании.</span><span class="sxs-lookup"><span data-stu-id="1f4df-133">Fill out deployment details</span></span>

    <span data-ttu-id="1f4df-134">**Имя базы данных**: выберите любое имя.</span><span class="sxs-lookup"><span data-stu-id="1f4df-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="1f4df-135">При наличии нескольких хранилищ данных, рекомендуется в именах включают сведения, например по региону hello, среда, например *mydw-westus-1-тестирование*.</span><span class="sxs-lookup"><span data-stu-id="1f4df-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="1f4df-136">**Подписка**: ваша подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="1f4df-137">**Группа ресурсов**: создайте группу ресурсов или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="1f4df-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="1f4df-138">Группы ресурсов можно использовать для администрирования ресурсов, например для определения области управления доступом или развертывания по шаблону.</span><span class="sxs-lookup"><span data-stu-id="1f4df-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="1f4df-139">Дополнительные сведения о группах ресурсов Azure и рекомендации см. [здесь](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="1f4df-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="1f4df-140">**Источник**: пустая база данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="1f4df-141">**Сервер**: выберите hello сервера, созданный в [необходимых компонентов].</span><span class="sxs-lookup"><span data-stu-id="1f4df-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="1f4df-142">**Параметры сортировки**: оставьте параметры сортировки по умолчанию hello SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="1f4df-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="1f4df-143">**Выберите «производительность»**: рекомендуется начинать с Стандартная 400DWU hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="1f4df-144">Выберите **toodashboard ПИН-код** ![tooDashboard ПИН-кода](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="1f4df-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="1f4df-145">Получайте и подождите, пока ваш toodeploy хранилища данных!</span><span class="sxs-lookup"><span data-stu-id="1f4df-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="1f4df-146">Это нормально, этот процесс tootake несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1f4df-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="1f4df-147">Hello портала уведомляет о готовности toouse является хранилищем данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="1f4df-148">Подключение tooSQL хранилища данных</span><span class="sxs-lookup"><span data-stu-id="1f4df-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="1f4df-149">В этом учебнике используется хранилище данных SQL Server Management Studio (SSMS) tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="1f4df-150">TooSQL хранилища данных могут подключаться через эти поддерживаемые соединители: ADO.NET, JDBC, PHP и ODBC.</span><span class="sxs-lookup"><span data-stu-id="1f4df-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="1f4df-151">Помните, что функциональные возможности средств, не поддерживаемых Майкрософт, могут быть ограничены.</span><span class="sxs-lookup"><span data-stu-id="1f4df-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="1f4df-152">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="1f4df-152">Get connection information</span></span>

<span data-ttu-id="1f4df-153">хранилище данных tooyour tooconnect, требуется tooconnect посредством hello логических SQL server был создан в [необходимых компонентов].</span><span class="sxs-lookup"><span data-stu-id="1f4df-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="1f4df-154">Выберите хранилище данных из панели мониторинга hello или выполните поиск в файлы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1f4df-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![Панель мониторинга хранилища данных SQL](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="1f4df-156">Найти hello полное имя для логического сервера SQL hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-156">Find hello full name for hello logical SQL server.</span></span>

    ![Выбор имени сервера](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="1f4df-158">Откройте SSMS и использовать объект explorer tooconnect toothis сервер с использованием учетных данных администратора сервера hello вы создали в [необходимых компонентов]</span><span class="sxs-lookup"><span data-stu-id="1f4df-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![Подключение с помощью SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="1f4df-160">Если все сделано правильно, должна появиться подключенных tooyour логического сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="1f4df-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="1f4df-161">Так как вы вошли в как Здравствуйте, администратор сервера, можно подключить tooany базы данных, размещенные на сервере hello, включая базы данных master hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="1f4df-162">Учетная запись администратора только один сервер, и имеет hello большинство права пользователя.</span><span class="sxs-lookup"><span data-stu-id="1f4df-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="1f4df-163">Будьте внимательны не tooallow слишком много пользователей в вашей организации пароль администратора hello tooknow.</span><span class="sxs-lookup"><span data-stu-id="1f4df-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="1f4df-164">Также у вас может быть учетная запись администратора Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1f4df-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="1f4df-165">Мы не предоставляем hello здесь сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="1f4df-165">We don't provide hello details here.</span></span> <span data-ttu-id="1f4df-166">Дополнительные сведения об использовании проверки подлинности Azure Active Directory toolearn см [проверки подлинности Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="1f4df-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="1f4df-167">Далее мы рассмотрим создание дополнительных пользователей и имен для входа.</span><span class="sxs-lookup"><span data-stu-id="1f4df-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="1f4df-168">Создание пользователя базы данных</span><span class="sxs-lookup"><span data-stu-id="1f4df-168">Create a database user</span></span>

<span data-ttu-id="1f4df-169">На этом шаге создается tooaccess учетной записи пользователя хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="1f4df-170">Мы также показано, как toogive toorun возможность hello этот пользователь запрашивает с большим объемом памяти и ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="1f4df-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="1f4df-171">Заметки о классах ресурсов при выделении ресурсов tooqueries</span><span class="sxs-lookup"><span data-stu-id="1f4df-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="1f4df-172">tookeep safe, данные не используются hello сервера администрирования toorun запросы на производственных баз данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="1f4df-173">Он имеет hello большинство привилегий любой пользователь, и с помощью tooperform операции с данными пользователя помещает данные под угрозой.</span><span class="sxs-lookup"><span data-stu-id="1f4df-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="1f4df-174">Кроме того поскольку Здравствуйте, администратор сервера должен tooperform операций управления, он выполняет операции с небольшой выделения памяти и ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="1f4df-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="1f4df-175">Хранилище данных SQL использует роли предварительно определенные базы данных, вызывается классами ресурсов, tooallocate различного объема памяти, ресурсы ЦП и toousers слоты параллелизма.</span><span class="sxs-lookup"><span data-stu-id="1f4df-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="1f4df-176">Каждый пользователь может принадлежать tooa небольшой, средний, большой или очень большой ресурсов класса.</span><span class="sxs-lookup"><span data-stu-id="1f4df-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="1f4df-177">Hello класс ресурсов пользователя определяет hello ресурсы hello пользователя toorun запросов и операций загрузки.</span><span class="sxs-lookup"><span data-stu-id="1f4df-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="1f4df-178">При использовании сжатия данных оптимальной hello пользователя, необходимо tooload с большими или очень больших выделений.</span><span class="sxs-lookup"><span data-stu-id="1f4df-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="1f4df-179">Дополнительные сведения о классах ресурсов см. [здесь](./sql-data-warehouse-develop-concurrency.md#resource-classes).</span><span class="sxs-lookup"><span data-stu-id="1f4df-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="1f4df-180">Создание учетной записи, позволяющей управлять базой данных</span><span class="sxs-lookup"><span data-stu-id="1f4df-180">Create an account that can control a database</span></span>

<span data-ttu-id="1f4df-181">Поскольку вы выполнили вход в Здравствуйте, администратор сервера имеется разрешения toocreate входа и пользователей.</span><span class="sxs-lookup"><span data-stu-id="1f4df-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="1f4df-182">Используя SSMS или другой клиент запросов, откройте новый запрос к базе данных **master**.</span><span class="sxs-lookup"><span data-stu-id="1f4df-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Создание запроса к базе данных master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Создание запроса к базе данных master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="1f4df-185">В окне запроса hello запустите этот toocreate команды T-SQL, имя MedRCLogin входа и пользователя с именем LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="1f4df-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="1f4df-186">Это имя входа можно подключиться toohello логического сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="1f4df-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="1f4df-187">Теперь запрос hello *базы данных хранилища данных SQL*, создание пользователя базы данных, на hello входа, созданного tooaccess и выполнять операции над hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="1f4df-188">Дать hello базы данных пользовательского элемента управления разрешения toohello базы данных называется NYT.</span><span class="sxs-lookup"><span data-stu-id="1f4df-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="1f4df-189">Если имя базы данных содержит дефисы, быть toowrap убедиться, что его в квадратные скобки.</span><span class="sxs-lookup"><span data-stu-id="1f4df-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="1f4df-190">Предоставьте hello пользователя средний выделений</span><span class="sxs-lookup"><span data-stu-id="1f4df-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="1f4df-191">Запустите этот toomake команды T-SQL ИТ член класса средний ресурсов hello, которая называется mediumrc.</span><span class="sxs-lookup"><span data-stu-id="1f4df-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="1f4df-192">Нажмите кнопку [здесь](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn Дополнительные сведения о классах параллелизма и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1f4df-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="1f4df-193">Подключение toohello логическом сервере с новыми учетными данными hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-193">Connect toohello logical server with hello new credentials</span></span>

    ![Вход с помощью новых учетных данных](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="1f4df-195">Загрузка данных из хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="1f4df-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="1f4df-196">Теперь вы находитесь tooload готовности данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="1f4df-197">Этот шаг показывает, как tooload Нью-Йорк такси CAB-файла данных из открытых хранилища Azure BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="1f4df-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="1f4df-198">Чаще всего tooload данных в хранилище данных SQL является toofirst переместить хранилище больших двоичных объектов tooAzure данных hello и затем загрузить в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="1f4df-199">toomake его проще toounderstand как tooload, у нас есть Нью-Йорк такси CAB-файла данных, уже размещенные в большой двоичный объект открытого хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="1f4df-200">Для дальнейшего использования, toolearn как tooget вашей tooAzure данные больших двоичных объектов хранилища или tooload его непосредственно из источника в хранилище данных SQL, в разделе hello [Общие сведения о загрузке](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="1f4df-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="1f4df-201">Определение внешних данных</span><span class="sxs-lookup"><span data-stu-id="1f4df-201">Define external data</span></span>

1. <span data-ttu-id="1f4df-202">Создайте главный ключ.</span><span class="sxs-lookup"><span data-stu-id="1f4df-202">Create a master key.</span></span> <span data-ttu-id="1f4df-203">Требуется только toocreate главного ключа, чем один раз в базе данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="1f4df-204">Определение расположения hello hello Azure BLOB-объект, содержащий hello такси CAB-файла данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="1f4df-205">Определение hello внешние форматы файлов</span><span class="sxs-lookup"><span data-stu-id="1f4df-205">Define hello external file formats</span></span>

    <span data-ttu-id="1f4df-206">Hello ```CREATE EXTERNAL FILE FORMAT``` команда является toospecify используется формат файлов, содержащих hello внешних данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="1f4df-207">Эти файлы содержат текст, разделенный одним или несколькими символами, которые называются разделителями.</span><span class="sxs-lookup"><span data-stu-id="1f4df-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="1f4df-208">В целях демонстрации hello такси CAB-файла данных хранится как несжатых данных и как gzip сжатых данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="1f4df-209">Выполнение этих двух различных форматов toodefine команды T-SQL: распаковки и сжатые.</span><span class="sxs-lookup"><span data-stu-id="1f4df-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="1f4df-210">Создайте схему для формата внешних файлов.</span><span class="sxs-lookup"><span data-stu-id="1f4df-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="1f4df-211">Создание внешних таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-211">Create hello external tables.</span></span> <span data-ttu-id="1f4df-212">Эти таблицы ссылаются на данные, содержащиеся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="1f4df-213">Запустите hello, следуя toocreate команды T-SQL несколько внешних таблиц, что все точки toohello BLOB-объектов Azure мы определили ранее в нашем внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="1f4df-214">Импорт данных hello из хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="1f4df-215">Хранилище данных SQL поддерживает ключевую инструкцию CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="1f4df-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="1f4df-216">Эта инструкция создает новую таблицу на основе результатов hello инструкции select.</span><span class="sxs-lookup"><span data-stu-id="1f4df-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="1f4df-217">Hello новая таблица содержит hello же столбцы и типы данных, как инструкция select hello результаты hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="1f4df-218">Это данные может надлежащим образом tooimport из хранилища BLOB-объектов Azure в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1f4df-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="1f4df-219">Запустите этот скрипт tooimport данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-219">Run this script tooimport your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="1f4df-220">Просмотрите данные при загрузке.</span><span class="sxs-lookup"><span data-stu-id="1f4df-220">View your data as it loads.</span></span>

   <span data-ttu-id="1f4df-221">Вы загружаете несколько гигабайт данных и сжимаете их в высокопроизводительные кластеризованные индексы Columnstore.</span><span class="sxs-lookup"><span data-stu-id="1f4df-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="1f4df-222">Выполните следующий запрос, использующий hello динамические административные представления (DMV) tooshow состояние загрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="1f4df-223">После запуска запроса hello, захватите кофе и перекусить, а хранилище данных SQL некоторых сложных задач.</span><span class="sxs-lookup"><span data-stu-id="1f4df-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="1f4df-224">Просмотрите все запросы в системе.</span><span class="sxs-lookup"><span data-stu-id="1f4df-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="1f4df-225">Посмотрите, как данные упорядоченно загружаются в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Просмотр загрузки данных](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="1f4df-227">Повышение производительности запросов</span><span class="sxs-lookup"><span data-stu-id="1f4df-227">Improve query performance</span></span>

<span data-ttu-id="1f4df-228">Существует несколько способов tooimprove производительность и tooachieve hello высокоскоростной производительность хранилище данных SQL — предназначен tooprovide.</span><span class="sxs-lookup"><span data-stu-id="1f4df-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="1f4df-229">В разделе hello влияние на производительность запросов</span><span class="sxs-lookup"><span data-stu-id="1f4df-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="1f4df-230">Одним из способов tooimprove производительность запросов является tooscale ресурсы, изменив hello DWU уровня обслуживания хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="1f4df-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="1f4df-231">Каждый уровень обслуживания стоит дороже, но вы можете выполнить обратное масштабирование или приостановить ресурсы в любое время.</span><span class="sxs-lookup"><span data-stu-id="1f4df-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="1f4df-232">На этом шаге сравнивается производительность при двух различных настройках DWU.</span><span class="sxs-lookup"><span data-stu-id="1f4df-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="1f4df-233">Во-первых, давайте масштабировать изменения размера hello вниз too100 DWU, поэтому мы можем получить представление о влиянии одного вычислительного узла может выполняться самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="1f4df-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="1f4df-234">Портал toohello перейти и выбрать хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1f4df-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="1f4df-235">Выберите масштаб в колонке hello хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1f4df-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![Масштабирование хранилища данных на портале](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="1f4df-237">Масштабировать производительность hello панели too100 DWU и нажмите Сохранить.</span><span class="sxs-lookup"><span data-stu-id="1f4df-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![Масштабирование и сохранение](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="1f4df-239">Подождите, пока ваш toofinish операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="1f4df-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1f4df-240">Запросы, не может выполняться при изменении масштаба hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="1f4df-241">Процедура масштабирования **прерывает** выполняющиеся запросы.</span><span class="sxs-lookup"><span data-stu-id="1f4df-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="1f4df-242">Вы можете перезапустить их после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="1f4df-243">Выполните операцию просмотра данных trip hello и выборе hello top миллионов записей для всех столбцов hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="1f4df-244">Если вы упреждающая toomove на быстро, вы бесплатно tooselect меньшее число строк.</span><span class="sxs-lookup"><span data-stu-id="1f4df-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="1f4df-245">Запишите hello время, затрачиваемое toorun этой операции.</span><span class="sxs-lookup"><span data-stu-id="1f4df-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="1f4df-246">Масштабировать хранилища данных обратно too400 DWU.</span><span class="sxs-lookup"><span data-stu-id="1f4df-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="1f4df-247">Помните, что каждый 100 DWU состоит в добавлении другой вычислительный узел tooyour хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="1f4df-248">Снова запустите запрос hello!</span><span class="sxs-lookup"><span data-stu-id="1f4df-248">Run hello query again!</span></span> <span data-ttu-id="1f4df-249">Вы заметите существенную разницу.</span><span class="sxs-lookup"><span data-stu-id="1f4df-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="1f4df-250">Поскольку hello запрос возвращает большое количество данных, доступной пропускной способности hello машины hello SSMS может быть узким местом производительности.</span><span class="sxs-lookup"><span data-stu-id="1f4df-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="1f4df-251">Это может привести к тому, что вы вообще не заметите повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="1f4df-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="1f4df-252">Хранилище данных SQL использует массовую параллельную обработку.</span><span class="sxs-lookup"><span data-stu-id="1f4df-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="1f4df-253">Запросы, которые сканирования или выполнять аналитические функции на миллионы строк использовать hello true возможности хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="1f4df-254">Увидеть эффект hello статистики по производительности запросов</span><span class="sxs-lookup"><span data-stu-id="1f4df-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="1f4df-255">Выполнить запрос, что соединения hello таблицы дат с таблицей Trip hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-255">Run a query that joins hello Date table with hello Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="1f4df-256">Этот запрос требует некоторое время, так как хранилище данных SQL имеет tooshuffle данных, прежде чем выполнить hello соединения.</span><span class="sxs-lookup"><span data-stu-id="1f4df-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="1f4df-257">Соединения не содержат данных tooshuffle одинаковых данных спроектированный toojoin в hello так же, как он распространяется.</span><span class="sxs-lookup"><span data-stu-id="1f4df-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="1f4df-258">Для этого вопроса следует ознакомиться с более подробной информацией.</span><span class="sxs-lookup"><span data-stu-id="1f4df-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="1f4df-259">Статистика имеет значение.</span><span class="sxs-lookup"><span data-stu-id="1f4df-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="1f4df-260">Запустите toocreate этой инструкции статистику по столбцам соединения hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="1f4df-261">Хранилище данных SQL не управляет статистикой автоматически.</span><span class="sxs-lookup"><span data-stu-id="1f4df-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="1f4df-262">Статистика важна для производительности запросов, поэтому мы настоятельно рекомендуем создавать и обновлять статистику.</span><span class="sxs-lookup"><span data-stu-id="1f4df-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="1f4df-263">**Вы получите hello максимальную выгоду, наличие статистики для столбцов, участвующих в соединениях, столбцов, используемых в hello обнаружено предложение и столбцы в GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="1f4df-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="1f4df-264">Снова запустите запрос hello необходимых компонентов и понаблюдайте за разницу в производительности.</span><span class="sxs-lookup"><span data-stu-id="1f4df-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="1f4df-265">При hello различия в производительности запросов не будет как радикальных как вертикальное масштабирование, вы заметите, что индексацию.</span><span class="sxs-lookup"><span data-stu-id="1f4df-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1f4df-266">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f4df-266">Next steps</span></span>

<span data-ttu-id="1f4df-267">Теперь вы готовы tooquery и исследование.</span><span class="sxs-lookup"><span data-stu-id="1f4df-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="1f4df-268">Ознакомьтесь с нашими советами и рекомендациями.</span><span class="sxs-lookup"><span data-stu-id="1f4df-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="1f4df-269">После завершения работы изучение день hello, сделать toopause убедиться, что экземпляр!</span><span class="sxs-lookup"><span data-stu-id="1f4df-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="1f4df-270">В рабочей среде, то могут экономить огромные путем приостановки и масштабирование toomeet потребностям бизнеса.</span><span class="sxs-lookup"><span data-stu-id="1f4df-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![Приостановить](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="1f4df-272">Полезные ссылки</span><span class="sxs-lookup"><span data-stu-id="1f4df-272">Useful readings</span></span>

<span data-ttu-id="1f4df-273">[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][]</span><span class="sxs-lookup"><span data-stu-id="1f4df-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="1f4df-274">[Рекомендации по использованию хранилища данных SQL Azure][]</span><span class="sxs-lookup"><span data-stu-id="1f4df-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="1f4df-275">[Мониторинг рабочей нагрузки с помощью динамических административных представлений][]</span><span class="sxs-lookup"><span data-stu-id="1f4df-275">[Query Monitoring][]</span></span>

<span data-ttu-id="1f4df-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (10 лучших рекомендаций по созданию реляционного хранилища данных большого объема)</span><span class="sxs-lookup"><span data-stu-id="1f4df-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="1f4df-277">[Миграция данных tooAzure хранилище данных SQL][]</span><span class="sxs-lookup"><span data-stu-id="1f4df-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Рекомендации по использованию хранилища данных SQL Azure]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Мониторинг рабочей нагрузки с помощью динамических административных представлений]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (10 лучших рекомендаций по созданию реляционного хранилища данных большого объема)
[Миграция данных tooAzure хранилище данных SQL]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[необходимых компонентов]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
