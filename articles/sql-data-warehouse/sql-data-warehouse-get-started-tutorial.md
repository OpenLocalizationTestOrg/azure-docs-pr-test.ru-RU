---
title: "Руководство по началу работы с хранилищем данных SQL Azure | Документация Майкрософт"
description: "Из этого руководства вы узнаете, как подготовить и загрузить данные в хранилище данных SQL Azure, а также получите основные сведения о масштабировании, приостановке и настройке."
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
ms.openlocfilehash: 95e14824ba3b705bb909ec983652dd3305b98805
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="339f3-104">Начало работы с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="339f3-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="339f3-105">Из этого руководства вы узнаете, как подготовить и загрузить данные в хранилище данных SQL Azure,</span><span class="sxs-lookup"><span data-stu-id="339f3-105">This tutorial shows how to provision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="339f3-106">а также получите основные сведения о масштабировании, приостановке и настройке.</span><span class="sxs-lookup"><span data-stu-id="339f3-106">You’ll also learn the basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="339f3-107">После завершения работы с документом вы будете уметь использовать запросы и просматривать хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-107">When you’re finished, you’ll be ready to query and explore your data warehouse.</span></span>

<span data-ttu-id="339f3-108"><seg>
  **Предполагаемое время выполнения**. Работа с этим комплексным руководством и примером кода занимает около 30 минут при условии, что все предварительные требования выполнены.</seg></span><span class="sxs-lookup"><span data-stu-id="339f3-108">**Estimated time to complete:** This is an end-to-end tutorial with example code that takes about 30 minutes to complete once you have met the prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="339f3-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="339f3-109">Prerequisites</span></span>

<span data-ttu-id="339f3-110">В руководстве предполагается, что вы уже знакомы с основными понятиями хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="339f3-110">The tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="339f3-111">Если это не так, рекомендуем прочитать статью [Что такое хранилище данных SQL](sql-data-warehouse-overview-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="339f3-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="339f3-112">Зарегистрируйтесь для Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="339f3-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="339f3-113">Если у вас еще нет учетной записи Microsoft Azure, зарегистрируйте ее, чтобы использовать эту службу.</span><span class="sxs-lookup"><span data-stu-id="339f3-113">If you don't already have a Microsoft Azure account, you need to sign up for one to use this service.</span></span> <span data-ttu-id="339f3-114">Если у вас уже есть учетная запись, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="339f3-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="339f3-115">Перейдите на страницу учетной записи [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/).</span><span class="sxs-lookup"><span data-stu-id="339f3-115">Navigate to the account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="339f3-116">Создайте бесплатную учетную запись Azure или купите платную.</span><span class="sxs-lookup"><span data-stu-id="339f3-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="339f3-117">Следуйте указаниям на экране.</span><span class="sxs-lookup"><span data-stu-id="339f3-117">Follow the instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="339f3-118">Установка соответствующих клиентских драйверов и средств SQL</span><span class="sxs-lookup"><span data-stu-id="339f3-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="339f3-119">Большинство клиентских средств SQL могут подключаться к хранилищу данных SQL с помощью JDBC, ODBC или ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="339f3-119">Most SQL client tools can connect to SQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="339f3-120">Из-за большого количества функций T-SQL, которые поддерживает хранилище данных SQL, не все клиентские приложения полностью совместимы с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="339f3-120">Due to the large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="339f3-121">Если вы работаете с ОС Windows, рекомендуем использовать либо [Visual Studio], либо [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="339f3-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="339f3-122">Создание хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="339f3-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="339f3-123">Хранилище данных SQL — это специальный тип базы данных, предназначенный для вычислений массовым параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="339f3-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="339f3-124">База данных распределяется между несколькими узлами и обрабатывает запросы параллельно.</span><span class="sxs-lookup"><span data-stu-id="339f3-124">The database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="339f3-125">У хранилища данных SQL есть управляющий узел, который координирует действия всех узлов.</span><span class="sxs-lookup"><span data-stu-id="339f3-125">SQL Data Warehouse has a control node that orchestrates the activities of all the nodes.</span></span> <span data-ttu-id="339f3-126">Сами же узлы для управления данными используют базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="339f3-126">The nodes themselves use SQL Database to manage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="339f3-127">Создание хранилища данных SQL может привести к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="339f3-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="339f3-128">Дополнительные сведения см. на странице [цен на хранилище данных SQL](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="339f3-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="339f3-129">Создание хранилища данных</span><span class="sxs-lookup"><span data-stu-id="339f3-129">Create a data warehouse</span></span>

1. <span data-ttu-id="339f3-130">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="339f3-130">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="339f3-131">Последовательно выберите **Создать** > **Базы данных** > **Хранилище данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="339f3-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="339f3-132">![Новая колонка](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![Выбор хранилища данных](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="339f3-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="339f3-133">Укажите сведения о развертывании.</span><span class="sxs-lookup"><span data-stu-id="339f3-133">Fill out deployment details</span></span>

    <span data-ttu-id="339f3-134">**Имя базы данных**: выберите любое имя.</span><span class="sxs-lookup"><span data-stu-id="339f3-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="339f3-135">При наличии нескольких хранилищ данных рекомендуется включать в имена такие сведения, как регион и среда, например *mydw-westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="339f3-135">If you have multiple data warehouses, we recommend your names include details such as the region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="339f3-136">**Подписка**: ваша подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="339f3-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="339f3-137">**Группа ресурсов**: создайте группу ресурсов или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="339f3-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="339f3-138">Группы ресурсов можно использовать для администрирования ресурсов, например для определения области управления доступом или развертывания по шаблону.</span><span class="sxs-lookup"><span data-stu-id="339f3-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="339f3-139">Дополнительные сведения о группах ресурсов Azure и рекомендации см. [здесь](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="339f3-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="339f3-140">**Источник**: пустая база данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="339f3-141">**Сервер**: выберите сервер, созданный в разделе [Предварительные требования].</span><span class="sxs-lookup"><span data-stu-id="339f3-141">**Server**: Select the server you created in [Prerequisites].</span></span>

    <span data-ttu-id="339f3-142">**Параметры сортировки**: оставьте параметры сортировки по умолчанию (SQL_Latin1_General_CP1_CI_AS).</span><span class="sxs-lookup"><span data-stu-id="339f3-142">**Collation**: Leave the default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="339f3-143">**Выбор уровня производительности**: рекомендуем начать со стандартного значения 400DWU.</span><span class="sxs-lookup"><span data-stu-id="339f3-143">**Select performance**: We recommend starting with the standard 400DWU.</span></span>

4. <span data-ttu-id="339f3-144">Установите флажок **Закрепить на панели мониторинга** ![Pin To Dashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="339f3-144">Choose **Pin to dashboard** ![Pin To Dashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="339f3-145">Подождите, пока завершится развертывание хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-145">Sit back and wait for your data warehouse to deploy!</span></span> <span data-ttu-id="339f3-146">Обычно этот процесс занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="339f3-146">It's normal for this process to take several minutes.</span></span> <span data-ttu-id="339f3-147">Портал уведомит вас, когда хранилище данных будет готово к использованию.</span><span class="sxs-lookup"><span data-stu-id="339f3-147">The portal notifies you when your data warehouse is ready to use.</span></span> 

## <a name="connect-to-sql-data-warehouse"></a><span data-ttu-id="339f3-148">Подключение к хранилищу данных SQL</span><span class="sxs-lookup"><span data-stu-id="339f3-148">Connect to SQL Data Warehouse</span></span>

<span data-ttu-id="339f3-149">В этом руководстве для подключения к хранилищу данных используется SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="339f3-149">This tutorial uses SQL Server Management Studio (SSMS) to connect to the data warehouse.</span></span> <span data-ttu-id="339f3-150">Подключиться к хранилищу данных SQL можно через следующие поддерживаемые соединители: ADO.NET, JDBC, ODBC и PHP.</span><span class="sxs-lookup"><span data-stu-id="339f3-150">You can connect to SQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="339f3-151">Помните, что функциональные возможности средств, не поддерживаемых Майкрософт, могут быть ограничены.</span><span class="sxs-lookup"><span data-stu-id="339f3-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="339f3-152">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="339f3-152">Get connection information</span></span>

<span data-ttu-id="339f3-153">Подключение к хранилищу данных SQL выполняется через логический сервер SQL Server, созданный в разделе [Предварительные требования].</span><span class="sxs-lookup"><span data-stu-id="339f3-153">To connect to your data warehouse, you need to connect through the logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="339f3-154">Выберите хранилище данных на панели мониторинга или найдите его в списке ресурсов.</span><span class="sxs-lookup"><span data-stu-id="339f3-154">Select your data warehouse from the dashboard or search for it in your resources.</span></span>

    ![Панель мониторинга хранилища данных SQL](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="339f3-156">Найдите полное имя логического сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="339f3-156">Find the full name for the logical SQL server.</span></span>

    ![Выбор имени сервера](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="339f3-158">Откройте SSMS. С помощью обозревателя объектов подключитесь к этому серверу, используя учетные данные администратора сервера, созданные в разделе [Предварительные требования].</span><span class="sxs-lookup"><span data-stu-id="339f3-158">Open SSMS and use object explorer to connect to this server using the server admin credentials you created in [Prerequisites]</span></span>

    ![Подключение с помощью SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="339f3-160">Если все сделано правильно, вы должны подключиться к логическому серверу SQL Server.</span><span class="sxs-lookup"><span data-stu-id="339f3-160">If all goes correctly, you should now be connected to your logical SQL server.</span></span> <span data-ttu-id="339f3-161">Поскольку вы вошли как администратор сервера, вы можете подключиться к любой базе данных, размещенной на этом сервере, включая базу данных master.</span><span class="sxs-lookup"><span data-stu-id="339f3-161">Since you logged in as the server admin, you can connect to any database hosted by the server, including the master database.</span></span> 

<span data-ttu-id="339f3-162">Существует только одна учетная запись администратора сервера, обладающая наибольшими правами.</span><span class="sxs-lookup"><span data-stu-id="339f3-162">There is only one server admin account and it has the most privileges of any user.</span></span> <span data-ttu-id="339f3-163">Следите за тем, чтобы пароль администратора не был известен слишком большому количеству людей в организации.</span><span class="sxs-lookup"><span data-stu-id="339f3-163">Be careful not to allow too many people in your organization to know the admin password.</span></span> 

<span data-ttu-id="339f3-164">Также у вас может быть учетная запись администратора Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="339f3-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="339f3-165">Сведения о ней не входят в объем этой статьи.</span><span class="sxs-lookup"><span data-stu-id="339f3-165">We don't provide the details here.</span></span> <span data-ttu-id="339f3-166">Если вы хотите узнать больше об использовании аутентификации Azure Active Directory, см. статью [Подключение к Базе данных SQL или хранилищу данных SQL c использованием проверки подлинности Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="339f3-166">If you want to learn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="339f3-167">Далее мы рассмотрим создание дополнительных пользователей и имен для входа.</span><span class="sxs-lookup"><span data-stu-id="339f3-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="339f3-168">Создание пользователя базы данных</span><span class="sxs-lookup"><span data-stu-id="339f3-168">Create a database user</span></span>

<span data-ttu-id="339f3-169">На этом шаге мы создадим учетную запись пользователя, который будет подключаться к хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-169">In this step, you create a user account to access your data warehouse.</span></span> <span data-ttu-id="339f3-170">Также мы покажем, как предоставить этому пользователю возможность выполнять запросы с большим объемом памяти и ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="339f3-170">We also show you how to give that user the ability to run queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-to-queries"></a><span data-ttu-id="339f3-171">Примечания о классах ресурсов для выделения ресурсов запросам</span><span class="sxs-lookup"><span data-stu-id="339f3-171">Notes about resource classes for allocating resources to queries</span></span>

- <span data-ttu-id="339f3-172">В целях защиты данных не следует выполнять запросы к производственным базам данных от имени администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="339f3-172">To keep your data safe, don't use the server admin to run queries on your production databases.</span></span> <span data-ttu-id="339f3-173">Эта учетная запись обладает наибольшими правами, и ее использование для выполнения операций с данными пользователей представляет риск для ваших данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-173">It has the most privileges of any user and using it to perform operations on user data puts your data at risk.</span></span> <span data-ttu-id="339f3-174">Кроме того, поскольку учетная запись администратора сервера предназначена для управления, она выполняет операции с выделением только небольшого объема памяти и ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="339f3-174">Also, since the server admin is meant to perform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="339f3-175">В хранилище данных SQL есть предварительно определенные роли базы данных, называемые классами ресурсов. Они используются для выделения пользователям различных объемов памяти, ресурсов ЦП и слотов параллельной обработки.</span><span class="sxs-lookup"><span data-stu-id="339f3-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, to allocate different amounts of memory, CPU resources, and concurrency slots to users.</span></span> <span data-ttu-id="339f3-176">Каждый пользователь может принадлежать к малому, среднему, большому или очень большому классу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="339f3-176">Each user can belong to a small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="339f3-177">Класс ресурсов пользователя определяет ресурсы, которыми располагает пользователь для выполнения запросов и операций загрузки.</span><span class="sxs-lookup"><span data-stu-id="339f3-177">The user's resource class determines the resources the user has to run queries and load operations.</span></span>

- <span data-ttu-id="339f3-178">Чтобы оптимизировать сжатие данных, пользователю, как правило, требуется загрузка с выделением объемных и очень объемных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="339f3-178">For optimal data compression, the user may need to load with large or extra large resource allocations.</span></span> <span data-ttu-id="339f3-179">Дополнительные сведения о классах ресурсов см. [здесь](./sql-data-warehouse-develop-concurrency.md#resource-classes).</span><span class="sxs-lookup"><span data-stu-id="339f3-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="339f3-180">Создание учетной записи, позволяющей управлять базой данных</span><span class="sxs-lookup"><span data-stu-id="339f3-180">Create an account that can control a database</span></span>

<span data-ttu-id="339f3-181">Поскольку вы вошли в качестве администратора сервера, у вас есть разрешения на создание пользователей и имен для входа.</span><span class="sxs-lookup"><span data-stu-id="339f3-181">Since you are currently logged in as the server admin you have permissions to create logins and users.</span></span>

1. <span data-ttu-id="339f3-182">Используя SSMS или другой клиент запросов, откройте новый запрос к базе данных **master**.</span><span class="sxs-lookup"><span data-stu-id="339f3-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Создание запроса к базе данных master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Создание запроса к базе данных master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="339f3-185">В окне запроса выполните следующую команду T-SQL, чтобы создать имя для входа MedRCLogin и пользователя с именем LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="339f3-185">In the query window, run this T-SQL command to create a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="339f3-186">Это имя для входа позволяет подключаться к логическому серверу SQL.</span><span class="sxs-lookup"><span data-stu-id="339f3-186">This login can connect to the logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="339f3-187">Теперь, выполняя запрос к *базе данных хранилища данных SQL*, создайте пользователя базы данных с именем для входа, которое вы создали для доступа к базе данных и выполнения в ней операций.</span><span class="sxs-lookup"><span data-stu-id="339f3-187">Now querying the *SQL Data Warehouse database*, create a database user based on the login you created to access and perform operations on the database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="339f3-188">Предоставьте пользователю базы данных разрешения на управление базой данных с именем NYT.</span><span class="sxs-lookup"><span data-stu-id="339f3-188">Give the database user control permissions to the database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] to LoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="339f3-189">Если имя базы данных содержит дефисы, обязательно заключите его в квадратные скобки!</span><span class="sxs-lookup"><span data-stu-id="339f3-189">If your database name has hyphens in it, be sure to wrap it in brackets!</span></span> 
    >

### <a name="give-the-user-medium-resource-allocations"></a><span data-ttu-id="339f3-190">Выделение для пользователя среднего объема ресурсов</span><span class="sxs-lookup"><span data-stu-id="339f3-190">Give the user medium resource allocations</span></span>

1. <span data-ttu-id="339f3-191">Выполните следующую команду T-SQL, чтобы сделать пользователя членом класса средних ресурсов, который называется mediumrc.</span><span class="sxs-lookup"><span data-stu-id="339f3-191">Run this T-SQL command to make it a member of the medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="339f3-192">Дополнительные сведения о параллелизме и классах ресурсов см. [здесь](sql-data-warehouse-develop-concurrency.md#resource-classes).</span><span class="sxs-lookup"><span data-stu-id="339f3-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) to learn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="339f3-193">Подключитесь к логическому серверу с помощью новых учетных данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-193">Connect to the logical server with the new credentials</span></span>

    ![Вход с помощью новых учетных данных](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="339f3-195">Загрузка данных из хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="339f3-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="339f3-196">Теперь все готово к загрузке данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-196">You are now ready to load data into your data warehouse.</span></span> <span data-ttu-id="339f3-197">В этом шаге мы покажем, как загрузить данные о такси Нью-Йорка из общедоступного BLOB-объекта хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="339f3-197">This step shows you how to load New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="339f3-198">Распространенный способ загрузки данных в хранилище данных SQL заключается в том, чтобы сначала переместить данные в хранилище BLOB-объектов Azure, а затем загрузить их в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-198">A common way to load data into SQL Data Warehouse is to first move the data to Azure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="339f3-199">Чтобы упростить понимание процесса загрузки, мы уже разместили данные о такси Нью-Йорка в общедоступном BLOB-объекте хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="339f3-199">To make it easier to understand how to load, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="339f3-200">Сведения о том, как переместить данные в хранилище BLOB-объектов Azure или загрузить их в хранилище данных SQL непосредственно из источника, см. статью [Загрузка данных в хранилище данных Azure SQL](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="339f3-200">For future reference, to learn how to get your data to Azure blob storage or to load it directly from your source into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="339f3-201">Определение внешних данных</span><span class="sxs-lookup"><span data-stu-id="339f3-201">Define external data</span></span>

1. <span data-ttu-id="339f3-202">Создайте главный ключ.</span><span class="sxs-lookup"><span data-stu-id="339f3-202">Create a master key.</span></span> <span data-ttu-id="339f3-203">Главный ключ создается для каждой базы данных только один раз.</span><span class="sxs-lookup"><span data-stu-id="339f3-203">You only need to create a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="339f3-204">Определите расположение BLOB-объекта Azure, содержащего данные о такси.</span><span class="sxs-lookup"><span data-stu-id="339f3-204">Define the location of the Azure blob that contains the taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="339f3-205">Определите форматы внешних файлов.</span><span class="sxs-lookup"><span data-stu-id="339f3-205">Define the external file formats</span></span>

    <span data-ttu-id="339f3-206">С помощью команды ```CREATE EXTERNAL FILE FORMAT``` можно указать формат файлов, содержащих внешние данные.</span><span class="sxs-lookup"><span data-stu-id="339f3-206">The ```CREATE EXTERNAL FILE FORMAT``` command is used to specify the format of files that contain the external data.</span></span> <span data-ttu-id="339f3-207">Эти файлы содержат текст, разделенный одним или несколькими символами, которые называются разделителями.</span><span class="sxs-lookup"><span data-stu-id="339f3-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="339f3-208">В целях демонстрации данные о такси хранятся как в несжатом виде, так и в виде сжатых данных в формате gzip.</span><span class="sxs-lookup"><span data-stu-id="339f3-208">For demonstration purposes, the taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="339f3-209">Выполните следующие команды T-SQL, чтобы определить два разных формата: несжатый и сжатый.</span><span class="sxs-lookup"><span data-stu-id="339f3-209">Run these T-SQL commands to define two different formats: uncompressed and compressed.</span></span>

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

4.  <span data-ttu-id="339f3-210">Создайте схему для формата внешних файлов.</span><span class="sxs-lookup"><span data-stu-id="339f3-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="339f3-211">Создайте внешние таблицы.</span><span class="sxs-lookup"><span data-stu-id="339f3-211">Create the external tables.</span></span> <span data-ttu-id="339f3-212">Эти таблицы ссылаются на данные, содержащиеся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="339f3-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="339f3-213">Выполните следующие команды T-SQL, чтобы создать несколько внешних таблиц, все из которых будут указывать на BLOB-объект Azure, определенный нами ранее во внешнем источнике данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-213">Run the following T-SQL commands to create several external tables that all point to the Azure blob we defined previously in our external data source.</span></span>

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

### <a name="import-the-data-from-azure-blob-storage"></a><span data-ttu-id="339f3-214">Импорт данных из хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="339f3-214">Import the data from Azure blob storage.</span></span>

<span data-ttu-id="339f3-215">Хранилище данных SQL поддерживает ключевую инструкцию CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="339f3-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="339f3-216">Эта инструкция создает таблицу на основе результатов инструкции Select.</span><span class="sxs-lookup"><span data-stu-id="339f3-216">This statement creates a new table based on the results of a select statement.</span></span> <span data-ttu-id="339f3-217">В новой таблице содержатся те же столбцы и типы данных, которые были выведены инструкцией Select.</span><span class="sxs-lookup"><span data-stu-id="339f3-217">The new table has the same columns and data types as the results of the select statement.</span></span>  <span data-ttu-id="339f3-218">Это элегантный способ импорта данных из хранилища BLOB-объектов Azure в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="339f3-218">This is an elegant way to import data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="339f3-219">Запустите этот скрипт для импорта данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-219">Run this script to import your data.</span></span>

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

2. <span data-ttu-id="339f3-220">Просмотрите данные при загрузке.</span><span class="sxs-lookup"><span data-stu-id="339f3-220">View your data as it loads.</span></span>

   <span data-ttu-id="339f3-221">Вы загружаете несколько гигабайт данных и сжимаете их в высокопроизводительные кластеризованные индексы Columnstore.</span><span class="sxs-lookup"><span data-stu-id="339f3-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="339f3-222">Выполните следующий запрос, использующий динамические административные представления, для отображения состояния загрузки.</span><span class="sxs-lookup"><span data-stu-id="339f3-222">Run the following query that uses a dynamic management views (DMVs) to show the status of the load.</span></span> <span data-ttu-id="339f3-223">После запуска запроса сделайте перерыв, пока хранилище данных SQL выполняет объемное задание обработки.</span><span class="sxs-lookup"><span data-stu-id="339f3-223">After starting the query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
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

3. <span data-ttu-id="339f3-224">Просмотрите все запросы в системе.</span><span class="sxs-lookup"><span data-stu-id="339f3-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="339f3-225">Посмотрите, как данные упорядоченно загружаются в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="339f3-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Просмотр загрузки данных](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="339f3-227">Повышение производительности запросов</span><span class="sxs-lookup"><span data-stu-id="339f3-227">Improve query performance</span></span>

<span data-ttu-id="339f3-228">Существует несколько способов повышения производительности запросов и обеспечения высокоскоростной производительности, заложенной в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="339f3-228">There are several ways to improve query performance and to achieve the high-speed performance that SQL Data Warehouse is designed to provide.</span></span>  

### <a name="see-the-effect-of-scaling-on-query-performance"></a><span data-ttu-id="339f3-229">Влияние масштабирования на производительность запросов</span><span class="sxs-lookup"><span data-stu-id="339f3-229">See the effect of scaling on query performance</span></span> 

<span data-ttu-id="339f3-230">Один из способов повышения производительности запросов заключается в масштабировании ресурсов путем изменения уровня обслуживания DWU для хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="339f3-230">One way to improve query performance is to scale resources by changing the DWU service level for your data warehouse.</span></span> <span data-ttu-id="339f3-231">Каждый уровень обслуживания стоит дороже, но вы можете выполнить обратное масштабирование или приостановить ресурсы в любое время.</span><span class="sxs-lookup"><span data-stu-id="339f3-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="339f3-232">На этом шаге сравнивается производительность при двух различных настройках DWU.</span><span class="sxs-lookup"><span data-stu-id="339f3-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="339f3-233">Сначала давайте уменьшим масштаб до 100 DWU, чтобы получить представление о производительности одного вычислительного узла.</span><span class="sxs-lookup"><span data-stu-id="339f3-233">First, let's scale the sizing down to 100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="339f3-234">Перейдите на портал и выберите хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="339f3-234">Go to the portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="339f3-235">Выберите пункт "Масштаб" в колонке "Хранилище данных SQL".</span><span class="sxs-lookup"><span data-stu-id="339f3-235">Select scale in the SQL Data Warehouse blade.</span></span> 

    ![Масштабирование хранилища данных на портале](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="339f3-237">Уменьшите производительность 100 DWU и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="339f3-237">Scale down the performance bar to 100 DWU and hit save.</span></span>

    ![Масштабирование и сохранение](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="339f3-239">Подождите завершения операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="339f3-239">Wait for your scale operation to finish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="339f3-240">При изменении масштаба запросы не выполняются.</span><span class="sxs-lookup"><span data-stu-id="339f3-240">Queries cannot run while changing the scale.</span></span> <span data-ttu-id="339f3-241">Процедура масштабирования **прерывает** выполняющиеся запросы.</span><span class="sxs-lookup"><span data-stu-id="339f3-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="339f3-242">Вы можете перезапустить их после завершения операции.</span><span class="sxs-lookup"><span data-stu-id="339f3-242">You can restart them when the operation is finished.</span></span>
    >
    
5. <span data-ttu-id="339f3-243">Выполните операцию сканирования данных о поездках, выбрав первый миллион записей для всех столбцов.</span><span class="sxs-lookup"><span data-stu-id="339f3-243">Do a scan operation on the trip data, selecting the top million entries for all the columns.</span></span> <span data-ttu-id="339f3-244">Если вы хотите побыстрее перейти к следующему шагу, выберите меньшее число строк.</span><span class="sxs-lookup"><span data-stu-id="339f3-244">If you're eager to move on quickly, feel free to select fewer rows.</span></span> <span data-ttu-id="339f3-245">Запишите время, затраченное на выполнение этой операции.</span><span class="sxs-lookup"><span data-stu-id="339f3-245">Take note of the time it takes to run this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="339f3-246">Выполните масштабирование хранилища данных обратно до 400 DWU.</span><span class="sxs-lookup"><span data-stu-id="339f3-246">Scale your data warehouse back to 400 DWU.</span></span> <span data-ttu-id="339f3-247">Помните, что каждые 100 DWU — это дополнительный вычислительный узел в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="339f3-247">Remember, each 100 DWU is adding another compute node to your Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="339f3-248">Выполните запрос повторно.</span><span class="sxs-lookup"><span data-stu-id="339f3-248">Run the query again!</span></span> <span data-ttu-id="339f3-249">Вы заметите существенную разницу.</span><span class="sxs-lookup"><span data-stu-id="339f3-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="339f3-250">Так как запрос возвращает большой объем данных, вы можете столкнуться с низкой пропускной способностью компьютера с выполняющейся средой SSMS.</span><span class="sxs-lookup"><span data-stu-id="339f3-250">Because the query returns a lot of data, the bandwidth availability of the machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="339f3-251">Это может привести к тому, что вы вообще не заметите повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="339f3-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="339f3-252">Хранилище данных SQL использует массовую параллельную обработку.</span><span class="sxs-lookup"><span data-stu-id="339f3-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="339f3-253">При сканировании и выполнении аналитических функций в миллионах строк с помощью запросов используется реальная мощность хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="339f3-253">Queries that scan or perform analytic functions on millions of rows experience the true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-the-effect-of-statistics-on-query-performance"></a><span data-ttu-id="339f3-254">Влияние статистики на производительность запросов</span><span class="sxs-lookup"><span data-stu-id="339f3-254">See the effect of statistics on query performance</span></span>

1. <span data-ttu-id="339f3-255">Выполните запрос, который объединит таблицу дат с таблицей поездок.</span><span class="sxs-lookup"><span data-stu-id="339f3-255">Run a query that joins the Date table with the Trip table</span></span>

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

    <span data-ttu-id="339f3-256">Выполнение этого запроса занимает некоторое время, так как прежде чем выполнить соединение, хранилище данных SQL распределяет данные.</span><span class="sxs-lookup"><span data-stu-id="339f3-256">This query takes a while because SQL Data Warehouse has to shuffle data before it can perform the join.</span></span> <span data-ttu-id="339f3-257">Соединениям не нужно распределять данные, если они предназначены для объединения данных тем же образом, которым происходит их распределение.</span><span class="sxs-lookup"><span data-stu-id="339f3-257">Joins do not have to shuffle data if they are designed to join data in the same way it is distributed.</span></span> <span data-ttu-id="339f3-258">Для этого вопроса следует ознакомиться с более подробной информацией.</span><span class="sxs-lookup"><span data-stu-id="339f3-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="339f3-259">Статистика имеет значение.</span><span class="sxs-lookup"><span data-stu-id="339f3-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="339f3-260">Используйте следующий оператор для создания статистики по столбцам соединения.</span><span class="sxs-lookup"><span data-stu-id="339f3-260">Run this statement to create statistics on the join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="339f3-261">Хранилище данных SQL не управляет статистикой автоматически.</span><span class="sxs-lookup"><span data-stu-id="339f3-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="339f3-262">Статистика важна для производительности запросов, поэтому мы настоятельно рекомендуем создавать и обновлять статистику.</span><span class="sxs-lookup"><span data-stu-id="339f3-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="339f3-263">**Статистику рекомендуется вести в столбцах, которые являются частью объединения, используются в предложении WHERE или GROUP BY**.</span><span class="sxs-lookup"><span data-stu-id="339f3-263">**You gain the most benefit by having statistics on columns involved in joins, columns used in the WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="339f3-264">Снова выполните запрос из раздела "Предварительные требования" и понаблюдайте за различиями в производительности.</span><span class="sxs-lookup"><span data-stu-id="339f3-264">Run the query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="339f3-265">Хотя различия в производительности запроса не будут столь значительными, как при масштабировании, вы должны заметить ускорение.</span><span class="sxs-lookup"><span data-stu-id="339f3-265">While the differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="339f3-266">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="339f3-266">Next steps</span></span>

<span data-ttu-id="339f3-267">Теперь можно выполнить запрос и изучить данные.</span><span class="sxs-lookup"><span data-stu-id="339f3-267">You're now ready to query and explore.</span></span> <span data-ttu-id="339f3-268">Ознакомьтесь с нашими советами и рекомендациями.</span><span class="sxs-lookup"><span data-stu-id="339f3-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="339f3-269">Если изучения данных на сегодня достаточно, не забудьте приостановить экземпляр хранилища.</span><span class="sxs-lookup"><span data-stu-id="339f3-269">If you're done exploring for the day, make sure to pause your instance!</span></span> <span data-ttu-id="339f3-270">В рабочей среде вы можете добиться огромной экономии, приостанавливая и масштабируя хранилище в соответствии с потребностями своего бизнеса.</span><span class="sxs-lookup"><span data-stu-id="339f3-270">In production, you can experience enormous savings by pausing and scaling to meet your business needs.</span></span>

![Приостановить](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="339f3-272">Полезные ссылки</span><span class="sxs-lookup"><span data-stu-id="339f3-272">Useful readings</span></span>

<span data-ttu-id="339f3-273">[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][]</span><span class="sxs-lookup"><span data-stu-id="339f3-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="339f3-274">[Рекомендации по использованию хранилища данных SQL Azure][]</span><span class="sxs-lookup"><span data-stu-id="339f3-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="339f3-275">[Мониторинг рабочей нагрузки с помощью динамических административных представлений][]</span><span class="sxs-lookup"><span data-stu-id="339f3-275">[Query Monitoring][]</span></span>

<span data-ttu-id="339f3-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (10 лучших рекомендаций по созданию реляционного хранилища данных большого объема)</span><span class="sxs-lookup"><span data-stu-id="339f3-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="339f3-277">[Migrating data to Azure SQL Data Warehouse in practice][] (Перенос данных в хранилище данных SQL Azure на практике)</span><span class="sxs-lookup"><span data-stu-id="339f3-277">[Migrating Data to Azure SQL Data Warehouse][]</span></span>

[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Рекомендации по использованию хранилища данных SQL Azure]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Мониторинг рабочей нагрузки с помощью динамических административных представлений]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (10 лучших рекомендаций по созданию реляционного хранилища данных большого объема)
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/ (Перенос данных в хранилище данных SQL Azure на практике)



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[Предварительные требования]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
