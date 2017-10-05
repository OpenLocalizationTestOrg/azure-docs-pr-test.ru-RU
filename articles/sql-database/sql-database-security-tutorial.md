---
title: "Защита базы данных SQL Azure | Документация Майкрософт"
description: "Узнайте о методах и функциях, используемых для защиты Базы данных SQL Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 4bc09ad13ed0c9dc9257e9c75ec6f9ff3d689a0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="cabb4-103">Защита базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cabb4-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="cabb4-104">База данных SQL защищает данные путем ограничения доступа к ним с помощью правил брандмауэра, механизмов проверки подлинности, предусматривающих идентификацию пользователей, и авторизации доступа на основе членства с учетом ролей и разрешений, а также с использованием безопасности на уровне строк и динамического маскирования данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-104">SQL Database secures your data by limiting access to your database using firewall rules, authentication mechanisms requiring users to prove their identity, and authorization to data through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="cabb4-105">Выполнив всего несколько простых действий, можно значительно повысить уровень защиты базы данных от пользователей-злоумышленников или несанкционированного доступа.</span><span class="sxs-lookup"><span data-stu-id="cabb4-105">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="cabb4-106">Из этого руководства вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="cabb4-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cabb4-107">Настройка правил брандмауэра уровня сервера для сервера на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cabb4-107">Set up server-level firewall rules for your server in the Azure portal</span></span>
> * <span data-ttu-id="cabb4-108">Создание правил брандмауэра на уровне базы данных для базы данных с помощью SSMS.</span><span class="sxs-lookup"><span data-stu-id="cabb4-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="cabb4-109">Подключение к базе данных с помощью безопасной строки подключения.</span><span class="sxs-lookup"><span data-stu-id="cabb4-109">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="cabb4-110">Управление доступом пользователей.</span><span class="sxs-lookup"><span data-stu-id="cabb4-110">Manage user access</span></span>
> * <span data-ttu-id="cabb4-111">Защита данных с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="cabb4-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="cabb4-112">Включение аудита базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="cabb4-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="cabb4-113">Включение обнаружения угроз базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="cabb4-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="cabb4-114">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="cabb4-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cabb4-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cabb4-115">Prerequisites</span></span>

<span data-ttu-id="cabb4-116">Для работы с этим руководством вам потребуется следующее.</span><span class="sxs-lookup"><span data-stu-id="cabb4-116">To complete this tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="cabb4-117">Установите последнюю версию [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="cabb4-117">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="cabb4-118">Установите Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="cabb4-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="cabb4-119">Создайте сервер и базу данных SQL Azure. Для этого ознакомьтесь с разделами [Создание базы данных SQL Azure на портале Azure](sql-database-get-started-portal.md), [Создание отдельной базы данных SQL Azure с помощью Azure CLI](sql-database-get-started-cli.md) и [Создание отдельной базы данных SQL Azure с помощью PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cabb4-119">Created an Azure SQL server and database - See [Create an Azure SQL database in the Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using the Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="cabb4-120">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cabb4-120">Log in to the Azure portal</span></span>

<span data-ttu-id="cabb4-121">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cabb4-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="cabb4-122">Создание правила брандмауэра на уровне сервера с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="cabb4-122">Create a server-level firewall rule in the Azure portal</span></span>

<span data-ttu-id="cabb4-123">Базы данных SQL защищены брандмауэром в Azure.</span><span class="sxs-lookup"><span data-stu-id="cabb4-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="cabb4-124">По умолчанию все подключения к серверу и базам данных на сервере отклоняются, за исключением подключений служб Azure.</span><span class="sxs-lookup"><span data-stu-id="cabb4-124">By default, all connections to the server and the databases inside the server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="cabb4-125">Дополнительные сведения см. в разделе [Правила брандмауэра уровня сервера и уровня базы данных SQL Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="cabb4-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="cabb4-126">Чтобы обеспечить наибольшую безопасность, для параметра "Разрешить доступ к службам Azure" следует установить значение "Выключено".</span><span class="sxs-lookup"><span data-stu-id="cabb4-126">The most secure configuration is to set 'Allow access to Azure services' to OFF.</span></span> <span data-ttu-id="cabb4-127">Если необходимо подключаться к базе данных из виртуальной машины Azure или облачной службы, необходимо создать [зарезервированный IP-адрес](../virtual-network/virtual-networks-reserved-public-ip.md) и разрешить доступ через брандмауэр только с этого зарезервированного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="cabb4-127">If you need to connect to the database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only the reserved IP address access through the firewall.</span></span> 

<span data-ttu-id="cabb4-128">Выполните приведенные ниже действия, чтобы создать для сервера [правило брандмауэра уровня сервера базы данных SQL](sql-database-firewall-configure.md), разрешающее подключения с определенного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="cabb4-128">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="cabb4-129">Если вы создали пример базы данных в Azure с помощью одного из предыдущих руководств или кратких руководств и выполняете инструкции данного руководства на компьютере с тем же IP-адресом, что и при выполнении тех руководств, то этот шаг можно пропустить, так как правило брандмауэра уровня сервера уже создано.</span><span class="sxs-lookup"><span data-stu-id="cabb4-129">If you have created a sample database in Azure using one of the previous tutorials or quickstarts and are performing this tutorial on a computer with the same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="cabb4-130">Щелкните **Базы данных SQL** в левом меню, затем на странице **Базы данных SQL** щелкните базу данных, для которой вы хотите настроить правило брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="cabb4-130">Click **SQL databases** from the left-hand menu and click the database you would like to configure the firewall rule for on the **SQL databases** page.</span></span> <span data-ttu-id="cabb4-131">После этого откроется страница обзора базы данных, где будет указано полное имя сервера (например, **mynewserver-20170313.database.windows.net**) и предоставлены параметры для дальнейшей настройки.</span><span class="sxs-lookup"><span data-stu-id="cabb4-131">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![правило брандмауэра для сервера](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="cabb4-133">Щелкните **Настройка брандмауэра для сервера** на панели инструментов, как показано на предыдущем рисунке.</span><span class="sxs-lookup"><span data-stu-id="cabb4-133">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="cabb4-134">Откроется страница **параметров брандмауэра** для сервера базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cabb4-134">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="cabb4-135">Щелкните **Добавить IP-адрес клиента** на панели инструментов, чтобы добавить общедоступный IP-адрес компьютера, подключающегося к порталу, или вручную введите правило брандмауэра. Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-135">Click **Add client IP** on the toolbar to add the public IP address of the computer connected to the portal with or enter the firewall rule manually and then click **Save**.</span></span>

      ![Настройка правила брандмауэра для сервера](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="cabb4-137">Нажмите кнопку **ОК**, а затем щелкните **X**, чтобы закрыть страницу **Параметры брандмауэра**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-137">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="cabb4-138">Теперь можно подключиться к любой базе данных на сервере с указанным IP-адресом или диапазоном IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="cabb4-138">You can now connect to any database in the server with the specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="cabb4-139">База данных SQL обменивается данными через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="cabb4-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="cabb4-140">Если вы пытаетесь подключиться из корпоративной сети, исходящий трафик через порт 1433 может быть запрещен сетевым брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="cabb4-140">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="cabb4-141">В таком случае вы не сможете подключиться к серверу базы данных SQL Azure. Для этого ваш ИТ-отдел должен открыть порт 1433.</span><span class="sxs-lookup"><span data-stu-id="cabb4-141">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="cabb4-142">Создание правила брандмауэра уровня базы данных с помощью SSMS</span><span class="sxs-lookup"><span data-stu-id="cabb4-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="cabb4-143">Правила брандмауэра уровня базы данных позволяют создавать отличающиеся параметры брандмауэра для разных баз данных на одном логическом сервере, а также создавать переносимые правила брандмауэра, то есть правила, которые следуют за базой данных во время [отработки отказа](sql-database-geo-replication-overview.md), а не хранятся на сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cabb4-143">Database-level firewall rules enable you to create different firewall settings for different databases within the same logical server and to create firewall rules that are portable - meaning that they follow the database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on the SQL server.</span></span> <span data-ttu-id="cabb4-144">Правила брандмауэра уровня базы данных можно настроить только с помощью инструкций Transact-SQL и только после настройки первого правила брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="cabb4-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall rule.</span></span> <span data-ttu-id="cabb4-145">Дополнительные сведения см. в разделе [Правила брандмауэра уровня сервера и уровня базы данных SQL Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="cabb4-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="cabb4-146">Ниже приведены инструкции по созданию правила брандмауэра для конкретной базы данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-146">Follows these steps to create a database-specific firewall rule.</span></span>

1. <span data-ttu-id="cabb4-147">Подключитесь к базе данных, например с помощью [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="cabb4-147">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="cabb4-148">В обозревателе объектов щелкните правой кнопкой мыши базу данных, для которой нужно добавить правило брандмауэра, и щелкните **Создать запрос**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-148">In Object Explorer, right-click on the database you want to add a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="cabb4-149">Откроется пустое окно запроса, подключенное к базе данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-149">A blank query window opens that is connected to your database.</span></span>

3. <span data-ttu-id="cabb4-150">В окне запроса измените IP-адрес на свой общедоступный IP-адрес, затем выполните приведенный ниже запрос.</span><span class="sxs-lookup"><span data-stu-id="cabb4-150">In the query window, modify the IP address to your public IP address and then execute the following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="cabb4-151">На панели инструментов щелкните **Выполнить**, чтобы создать правило брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="cabb4-151">On the toolbar, click **Execute** to create the firewall rule.</span></span>

## <a name="view-how-to-connect-an-application-to-your-database-using-a-secure-connection-string"></a><span data-ttu-id="cabb4-152">Просмотр подключения приложения к базе данных с помощью безопасной строки подключения</span><span class="sxs-lookup"><span data-stu-id="cabb4-152">View how to connect an application to your database using a secure connection string</span></span>

<span data-ttu-id="cabb4-153">Чтобы обеспечить защищенное зашифрованное подключение между клиентским приложением и базой данных SQL, строка подключения должна быть настроена таким образом, чтобы:</span><span class="sxs-lookup"><span data-stu-id="cabb4-153">To ensure a secure, encrypted connection between a client application and SQL Database, the connection string has to be configured to:</span></span>

- <span data-ttu-id="cabb4-154">запрашивалось зашифрованное подключение и</span><span class="sxs-lookup"><span data-stu-id="cabb4-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="cabb4-155">сертификат сервера не считался доверенным.</span><span class="sxs-lookup"><span data-stu-id="cabb4-155">To not trust the server certificate.</span></span> 

<span data-ttu-id="cabb4-156">В этом случае устанавливается подключение по протоколу TLS и уменьшается риск атак "злоумышленник в середине".</span><span class="sxs-lookup"><span data-stu-id="cabb4-156">This establishes a connection using Transport Layer Security (TLS) and reduces the risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="cabb4-157">Правильно настроенные строки подключения к базе данных SQL для поддерживаемых драйверов клиента можно получить на портале Azure, как показано для ADO.NET на приведенном снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="cabb4-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from the Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="cabb4-158">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-158">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span>

2. <span data-ttu-id="cabb4-159">На странице **Обзор** для базы данных щелкните **Показать строки подключения к базам данных**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-159">On the **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="cabb4-160">Просмотрите полную строку подключения **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-160">Review the complete **ADO.NET** connection string.</span></span>

    ![Строка подключения по протоколу ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="cabb4-162">Создание пользователей базы данных</span><span class="sxs-lookup"><span data-stu-id="cabb4-162">Creating database users</span></span>

<span data-ttu-id="cabb4-163">Прежде чем создавать пользователей, необходимо выбрать один из двух типов аутентификации, поддерживаемых базой данных SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="cabb4-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="cabb4-164">**Аутентификация SQL**: для имен для входа и пользователей используются имя пользователя и пароль, действительные только в контексте конкретной базы данных на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="cabb4-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in the context of a specific database within a logical server.</span></span> 

<span data-ttu-id="cabb4-165">**Аутентификация Azure Active Directory**: используются удостоверения, управляемые Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cabb4-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="cabb4-166">Если вы хотите использовать [Azure Active Directory](./sql-database-aad-authentication.md) для аутентификации базы данных SQL, должен существовать предварительно заполненный каталог Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cabb4-166">If you want to use [Azure Active Directory](./sql-database-aad-authentication.md) to authenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="cabb4-167">Выполните следующее, чтобы создать пользователя, использующего аутентификацию SQL.</span><span class="sxs-lookup"><span data-stu-id="cabb4-167">Follow these steps to create a user using SQL Authentication:</span></span>

1. <span data-ttu-id="cabb4-168">Подключитесь к базе данных, например с помощью [SQL Server Management Studio](./sql-database-connect-query-ssms.md), с использованием учетных данных администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="cabb4-168">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="cabb4-169">В обозревателе объектов щелкните правой кнопкой мыши базу данных, для которой нужно добавить нового пользователя, и щелкните **Создать запрос**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-169">In Object Explorer, right-click on the database you want to add a new user on and click **New Query**.</span></span> <span data-ttu-id="cabb4-170">Откроется пустое окно запроса, связанное с выбранной базой данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-170">A blank query window opens that is connected to the selected database.</span></span>

3. <span data-ttu-id="cabb4-171">В окне запроса введите следующее:</span><span class="sxs-lookup"><span data-stu-id="cabb4-171">In the query window, enter the following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="cabb4-172">На панели инструментов щелкните **Выполнить**, чтобы создать пользователя.</span><span class="sxs-lookup"><span data-stu-id="cabb4-172">On the toolbar, click **Execute** to create the user.</span></span>

5. <span data-ttu-id="cabb4-173">По умолчанию пользователь может подключаться к базе данных, но не имеет разрешений на чтение и запись данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-173">By default, the user can connect to the database, but has no permissions to read or write data.</span></span> <span data-ttu-id="cabb4-174">Чтобы предоставить эти разрешения только что созданному пользователю, выполните следующие две команды в новом окне запроса.</span><span class="sxs-lookup"><span data-stu-id="cabb4-174">To grant these permissions to the newly created user, execute the following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="cabb4-175">Рекомендуется создавать эти учетные записи без прав администратора на уровне базы данных для подключения к базе данных, если только не требуется выполнять задачи администрирования, например создавать пользователей.</span><span class="sxs-lookup"><span data-stu-id="cabb4-175">It is best practice to create these non-administrator accounts at the database level to connect to your database unless you need to execute administrator tasks like creating new users.</span></span> <span data-ttu-id="cabb4-176">Ознакомьтесь с [руководством по Azure Active Directory](./sql-database-aad-authentication-configure.md), посвященном аутентификации с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cabb4-176">Please review the [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how to authenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="cabb4-177">Защита данных с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="cabb4-177">Protect your data with encryption</span></span>

<span data-ttu-id="cabb4-178">Прозрачное шифрование данных базы данных SQL Azure (TDE) позволяет автоматически шифровать неактивные данные, не внося каких-либо изменений в приложение, обращающееся к зашифрованной базе данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes to the application accessing the encrypted database.</span></span> <span data-ttu-id="cabb4-179">Для новых баз данных прозрачное шифрование данных включено по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cabb4-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="cabb4-180">Чтобы включить прозрачное шифрование данных для базы данных или убедиться, что оно включено, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="cabb4-180">To enable TDE for your database or to verify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="cabb4-181">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-181">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="cabb4-182">Щелкните **Прозрачное шифрование данных**, чтобы открыть страницу настройки TDE.</span><span class="sxs-lookup"><span data-stu-id="cabb4-182">Click on **Transparent data encryption** to open the configuration page for TDE.</span></span>

    ![Прозрачное шифрование данных](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="cabb4-184">Если требуется, для параметра **Шифрование данных** задайте значение "Вкл." и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-184">If necessary, set **Data encryption** to ON and click **Save**.</span></span>

<span data-ttu-id="cabb4-185">Начнется процесс шифрования в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="cabb4-185">The encryption process starts in the background.</span></span> <span data-ttu-id="cabb4-186">Вы можете отслеживать ход выполнения, подключившись к базе данных SQL с помощью [SQL Server Management Studio](./sql-database-connect-query-ssms.md), запросив столбец encryption_state представления `sys.dm_database_encryption_keys`.</span><span class="sxs-lookup"><span data-stu-id="cabb4-186">You can monitor the progress by connecting to SQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying the encryption_state column of the `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="cabb4-187">Включение аудита базы данных SQL (при необходимости)</span><span class="sxs-lookup"><span data-stu-id="cabb4-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="cabb4-188">Аудит базы данных SQL Azure позволяет отслеживать события базы данных и записывать их в журнал аудита в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="cabb4-188">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="cabb4-189">Аудит может помочь вам соблюсти требования нормативов, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на предполагаемые нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="cabb4-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="cabb4-190">Чтобы создать политику аудита по умолчанию для базы данных SQL, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="cabb4-190">Follow these steps to create a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="cabb4-191">В меню слева выберите **Базы данных SQL** и на странице **Базы данных SQL** щелкните имя своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-191">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="cabb4-192">В колонке "Параметры" выберите **Аудит и обнаружение угроз**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-192">In the Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="cabb4-193">Обратите внимание на то, что аудит уровня сервера отключен и в колонке имеется ссылка **Просмотр настроек аудита сервера**, позволяющая просмотреть или изменить настройки аудита сервера в данном контексте.</span><span class="sxs-lookup"><span data-stu-id="cabb4-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![Колонка "Аудит"](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="cabb4-195">Если вы хотите включить тип аудита (или расположение), отличный от указанного на уровне сервера, **включите** аудит и выберите тип аудита **BLOB-объект**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-195">If you prefer to enable an Audit type (or location?) different from the one specified at the server level, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span> <span data-ttu-id="cabb4-196">Если включен аудит BLOB-объектов сервера, настроенный аудит для базы данных будет существовать параллельно с ним.</span><span class="sxs-lookup"><span data-stu-id="cabb4-196">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>

    ![Включение аудита](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="cabb4-198">Выберите **Сведения о хранилище** , чтобы открыть колонку хранилища журналов аудита.</span><span class="sxs-lookup"><span data-stu-id="cabb4-198">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="cabb4-199">Выберите учетную запись хранения Azure, в которой будут сохраняться журналы, и срок хранения, по истечении которого старые журналы будут удалены. Затем нажмите кнопку **ОК** внизу.</span><span class="sxs-lookup"><span data-stu-id="cabb4-199">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="cabb4-200">Для того чтобы в полной мере воспользоваться возможностями шаблонов отчетов об аудите, используйте одну и ту же учетную запись хранения для всех баз данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-200">Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="cabb4-201">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cabb4-202">Если вы хотите настроить события аудита, это можно сделать с помощью PowerShell или REST API. Дополнительные сведения см. в разделе [Автоматизация (PowerShell или REST API)](sql-database-auditing.md#subheading-7).</span><span class="sxs-lookup"><span data-stu-id="cabb4-202">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="cabb4-203">Включение обнаружения угроз базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="cabb4-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="cabb4-204">Благодаря оповещениям безопасности о подозрительной активности система обнаружения угроз формирует дополнительный уровень безопасности, позволяющий клиентам обнаруживать потенциальные угрозы по мере возникновения и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="cabb4-204">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="cabb4-205">Пользователи могут анализировать подозрительные события с помощью аудита базы данных SQL, который позволяет определить причину таких событий (попытка получить доступ к данным в базе данных, нарушить безопасность или использовать их уязвимость).</span><span class="sxs-lookup"><span data-stu-id="cabb4-205">Users can explore the suspicious events using SQL Database Auditing to determine if they result from an attempt to access, breach or exploit data in the database.</span></span> <span data-ttu-id="cabb4-206">Система обнаружения угроз упрощает устранение потенциальных угроз безопасности базы данных, не требуя наличия у пользователя экспертных навыков в сфере безопасности либо умения работать в сложных системах отслеживания угроз.</span><span class="sxs-lookup"><span data-stu-id="cabb4-206">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="cabb4-207">Например, система обнаружения угроз обнаруживает определенную подозрительную активность в базе данных, указывающую на потенциальные попытки внедрения кода SQL.</span><span class="sxs-lookup"><span data-stu-id="cabb4-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="cabb4-208">Внедрение кода SQL — один из распространенных видов угроз безопасности веб-приложений в Интернете, используемый для получения несанкционированного доступа к приложениям, управляемым данными.</span><span class="sxs-lookup"><span data-stu-id="cabb4-208">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="cabb4-209">Взломщики используют уязвимые места приложения, чтобы ввести вредоносные инструкции SQL в поля ввода приложения, чтобы нарушить или изменить данные в базе данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-209">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

1. <span data-ttu-id="cabb4-210">Перейдите к колонке настройки базы данных SQL, которую требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="cabb4-210">Navigate to the configuration blade of the SQL database you want to monitor.</span></span> <span data-ttu-id="cabb4-211">В колонке "Параметры" выберите **Аудит и обнаружение угроз**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-211">In the Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Область навигации](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="cabb4-213">В колонке настроек **Аудит и обнаружение угроз** установите переключатель аудита в положение **Вкл.**, после чего отобразятся настройки обнаружения угроз.</span><span class="sxs-lookup"><span data-stu-id="cabb4-213">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>

3. <span data-ttu-id="cabb4-214">Переведите переключатель обнаружения угроз в положение **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="cabb4-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="cabb4-215">Настройте список электронных адресов, на которые будут приходить оповещения безопасности в случае обнаружения подозрительной активности в базе данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-215">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="cabb4-216">В колонке **Аудит и обнаружение угроз** щелкните **Сохранить**, чтобы сохранить новую или обновленную версию политики аудита и обнаружения угроз.</span><span class="sxs-lookup"><span data-stu-id="cabb4-216">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>

    ![Область навигации](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="cabb4-218">При обнаружении подозрительных действий в базе данных вы получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="cabb4-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="cabb4-219">В электронном сообщении будет содержаться информация о подозрительном событии безопасности, включая характер подозрительной активности, имя базы данных и сервера, а также время, когда произошло событие.</span><span class="sxs-lookup"><span data-stu-id="cabb4-219">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="cabb4-220">Кроме того, в сообщении приводится информация о возможных причинах возникновения события, а также рекомендуемые действия по поиску и устранению потенциальной угрозы безопасности базы данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-220">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span> <span data-ttu-id="cabb4-221">Ниже описывается, что делать, если вы получили приведенное ниже электронное сообщение.</span><span class="sxs-lookup"><span data-stu-id="cabb4-221">The next steps walk you through what to do should you receive such an email:</span></span>

    ![Электронное сообщение об обнаружении угроз](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="cabb4-223">В электронном сообщении щелкните ссылку **Журнал аудита SQL Azure**, после чего откроется портал Azure и будут показаны соответствующие записи аудита, зафиксированные примерно во время возникновения подозрительного события.</span><span class="sxs-lookup"><span data-stu-id="cabb4-223">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant auditing records around the time of the suspicious event.</span></span>

    ![Записи аудита](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="cabb4-225">Щелкните записи аудита, чтобы просмотреть более подробную информацию о подозрительной активности в базе данных, включая инструкции SQL, причины ошибки и IP-адрес клиента.</span><span class="sxs-lookup"><span data-stu-id="cabb4-225">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Сведения о записи](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="cabb4-227">В колонке записей аудита щелкните **Открыть в Excel**, чтобы открыть предварительно настроенный шаблон Excel и импортировать для более детального анализа записи из журнала аудита, зафиксированные примерно во время возникновения подозрительного события.</span><span class="sxs-lookup"><span data-stu-id="cabb4-227">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cabb4-228">В Excel 2010 или более поздней версии требуется Power Query и параметр **Быстрое объединение**.</span><span class="sxs-lookup"><span data-stu-id="cabb4-228">In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>

    ![Открытые записей в Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="cabb4-230">Чтобы настроить параметр **Быстрое объединение**, на вкладке ленты **POWER QUERY** выберите **Параметры**, чтобы открыть диалоговое окно "Параметры".</span><span class="sxs-lookup"><span data-stu-id="cabb4-230">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="cabb4-231">Щелкните раздел «Конфиденциальность» и выберите в нем второй вариант — «Игнорировать уровни конфиденциальности и по возможности повышать производительность»:</span><span class="sxs-lookup"><span data-stu-id="cabb4-231">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>

    ![Быстрое объединение в Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="cabb4-233">Чтобы загрузить записи журнала аудита SQL, убедитесь, что параметры на вкладке настроек установлены правильно, а затем откройте ленту «Данные» и нажмите кнопку «Обновить все».</span><span class="sxs-lookup"><span data-stu-id="cabb4-233">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>

    ![Параметры Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="cabb4-235">Результаты появятся на листе **Записи журнала аудита SQL** , что позволит выполнить более детальный анализ обнаруженной подозрительной активности, а также снизить степень влияния событий безопасности в приложении.</span><span class="sxs-lookup"><span data-stu-id="cabb4-235">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cabb4-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cabb4-236">Next steps</span></span>
<span data-ttu-id="cabb4-237">Выполнив всего несколько простых действий, можно значительно повысить уровень защиты базы данных от пользователей-злоумышленников или несанкционированного доступа.</span><span class="sxs-lookup"><span data-stu-id="cabb4-237">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="cabb4-238">Из этого руководства вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="cabb4-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cabb4-239">Настройка правил брандмауэра для сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="cabb4-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="cabb4-240">Подключение к базе данных с помощью безопасной строки подключения.</span><span class="sxs-lookup"><span data-stu-id="cabb4-240">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="cabb4-241">Управление доступом пользователей.</span><span class="sxs-lookup"><span data-stu-id="cabb4-241">Manage user access</span></span>
> * <span data-ttu-id="cabb4-242">Защита данных с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="cabb4-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="cabb4-243">Включение аудита базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="cabb4-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="cabb4-244">Включение обнаружения угроз базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="cabb4-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
><span data-ttu-id="cabb4-245">[Troubleshoot performance issues and optimize your database](sql-database-performance-tutorial.md) (Устранение проблем с производительностью и оптимизация базы данных)</span><span class="sxs-lookup"><span data-stu-id="cabb4-245">[Improve SQL Database performance](sql-database-performance-tutorial.md)</span></span>

