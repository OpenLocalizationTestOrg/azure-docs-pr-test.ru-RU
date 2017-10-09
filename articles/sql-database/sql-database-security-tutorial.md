---
title: "aaaSecure базы данных Azure SQL | Документы Microsoft"
description: "Дополнительные сведения о методах и функциях toosecure базы данных Azure SQL."
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
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="3a758-103">Защита базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3a758-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="3a758-104">База данных SQL защищает данные, ограничивая tooyour базы данных access, с помощью правил брандмауэра, требующие tooprove пользователей их идентификации и авторизации toodata через членство в роли и разрешения, а также через механизмы проверки подлинности безопасность на уровне строк и маскирование динамических данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="3a758-105">Можно улучшить защиту hello базы данных на соответствие пользователей-злоумышленников или несанкционированного доступа с помощью нескольких простых шагов.</span><span class="sxs-lookup"><span data-stu-id="3a758-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="3a758-106">Из этого руководства вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="3a758-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="3a758-107">Настройка правил брандмауэра уровня сервера для сервера в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3a758-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="3a758-108">Создание правил брандмауэра на уровне базы данных для базы данных с помощью SSMS.</span><span class="sxs-lookup"><span data-stu-id="3a758-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="3a758-109">Подключиться с помощью строки безопасного подключения базы данных tooyour</span><span class="sxs-lookup"><span data-stu-id="3a758-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="3a758-110">Управление доступом пользователей.</span><span class="sxs-lookup"><span data-stu-id="3a758-110">Manage user access</span></span>
> * <span data-ttu-id="3a758-111">Защита данных с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="3a758-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="3a758-112">Включение аудита базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="3a758-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="3a758-113">Включение обнаружения угроз базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="3a758-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="3a758-114">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="3a758-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a758-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3a758-115">Prerequisites</span></span>

<span data-ttu-id="3a758-116">toocomplete этого учебника, убедитесь в наличии hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3a758-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="3a758-117">Установленные hello новейшую версию [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="3a758-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="3a758-118">Установите Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="3a758-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="3a758-119">Создан на сервер Azure SQL и базы данных — в разделе [создать базу данных Azure SQL в hello портал Azure](sql-database-get-started-portal.md), [создание одной базы данных Azure SQL с помощью Azure CLI hello](sql-database-get-started-cli.md), и [создание единого SQL Azure базы данных с помощью PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3a758-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="3a758-120">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3a758-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="3a758-121">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3a758-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="3a758-122">Создание правила брандмауэра уровня сервера в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3a758-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="3a758-123">Базы данных SQL защищены брандмауэром в Azure.</span><span class="sxs-lookup"><span data-stu-id="3a758-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="3a758-124">По умолчанию все соединения toohello сервера hello базы данных и внутри сервера hello отклоняются, за исключением соединений с другими службами Azure.</span><span class="sxs-lookup"><span data-stu-id="3a758-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="3a758-125">Дополнительные сведения см. в разделе [Правила брандмауэра уровня сервера и уровня базы данных SQL Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3a758-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="3a758-126">Hello наиболее высокий уровень безопасности — tooset tooOFF «Разрешить доступ tooAzure службы».</span><span class="sxs-lookup"><span data-stu-id="3a758-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="3a758-127">Если необходимо настроить базу данных toohello tooconnect из виртуальной Машины Azure или облачные службы, необходимо создать [зарезервированный IP-адрес](../virtual-network/virtual-networks-reserved-public-ip.md) и поддерживает только hello зарезервированные IP адрес доступ через брандмауэр hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="3a758-128">Выполните эти действия toocreate [правила брандмауэра уровня сервера базы данных SQL](sql-database-firewall-configure.md) для tooallow подключений к серверу из конкретного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="3a758-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="3a758-129">Если вы создали образец базы данных в Azure с помощью одного из предыдущих занятий hello или примеры использования и являются этого учебника для выполнения на компьютере с hello же IP-адрес что он имел при рассмотрения этих учебников, можно пропустить этот шаг, вы получите уже создано правило брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="3a758-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="3a758-130">Нажмите кнопку **баз данных SQL** из hello левом меню и выберите пункт hello базы данных следует правило брандмауэра hello tooconfigure для на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="3a758-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="3a758-131">Hello страница общих сведений для вашей базы данных открывается, показывающая вы полностью hello доменное имя сервера (таких как **mynewserver 20170313.database.windows.net**) и предоставляет параметры для дальнейшей настройки.</span><span class="sxs-lookup"><span data-stu-id="3a758-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![правило брандмауэра для сервера](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="3a758-133">Нажмите кнопку **установить брандмауэр сервера** на hello инструментов, как показано на предыдущем рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="3a758-134">Hello **параметры брандмауэра** откроется страница приветствия базы данных SQL server.</span><span class="sxs-lookup"><span data-stu-id="3a758-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="3a758-135">Нажмите кнопку **добавить IP-адрес клиента** на hello инструментов tooadd hello общедоступный IP-адрес портала подключенных toohello hello компьютера с или вручную введите правило брандмауэра hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3a758-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![Настройка правила брандмауэра для сервера](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="3a758-137">Нажмите кнопку **ОК** и нажмите кнопку hello **X** tooclose hello **параметры брандмауэра** страницы.</span><span class="sxs-lookup"><span data-stu-id="3a758-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="3a758-138">Базы данных tooany hello server теперь можно подключиться с hello указан IP-адрес или IP-адрес диапазона.</span><span class="sxs-lookup"><span data-stu-id="3a758-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="3a758-139">База данных SQL обменивается данными через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="3a758-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="3a758-140">Если вы пытаетесь tooconnect из корпоративной сети, исходящий трафик через порт 1433 может оказаться невозможным брандмауэром вашей сети.</span><span class="sxs-lookup"><span data-stu-id="3a758-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="3a758-141">В этом случае нельзя сервера базы данных SQL Azure может tooconnect tooyour Если ИТ-отдел открывает порт 1433.</span><span class="sxs-lookup"><span data-stu-id="3a758-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="3a758-142">Создание правила брандмауэра уровня базы данных с помощью SSMS</span><span class="sxs-lookup"><span data-stu-id="3a758-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="3a758-143">Правила брандмауэра уровня базы данных включить брандмауэр для разных баз данных в пределах hello же логический сервер и toocreate брандмауэра правила, являются переносимыми - это означает, что они следуют hello базы данных во время различных toocreate [перехода на другой ресурс ](sql-database-geo-replication-overview.md) помещения в hello SQL server.</span><span class="sxs-lookup"><span data-stu-id="3a758-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="3a758-144">Правила брандмауэра уровня базы данных можно только настроенные с помощью инструкций Transact-SQL и только после настройки первого правила брандмауэра уровня сервера hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="3a758-145">Дополнительные сведения см. в разделе [Правила брандмауэра уровня сервера и уровня базы данных SQL Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3a758-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="3a758-146">Ниже эти шаги toocreate правило брандмауэра для конкретной базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="3a758-147">Подключение tooyour базы данных, например с помощью [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="3a758-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="3a758-148">В обозревателе объектов щелкните правой кнопкой мыши на hello базы данных, которая tooadd правило брандмауэра и нажмите кнопку **новый запрос**.</span><span class="sxs-lookup"><span data-stu-id="3a758-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="3a758-149">Пустое окно запроса, откроется tooyour подключенной базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="3a758-150">В окне запроса hello измените hello tooyour открытый IP-адрес, а затем выполните приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="3a758-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="3a758-151">На панели инструментов hello, нажмите кнопку **Execute** правило брандмауэра toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="3a758-152">Просматривать как tooconnect tooyour приложения базы данных с помощью строки безопасного подключения</span><span class="sxs-lookup"><span data-stu-id="3a758-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="3a758-153">tooensure защищенное зашифрованное подключение между клиентским приложением и базой данных SQL, строка подключения hello имеет toobe настроен для:</span><span class="sxs-lookup"><span data-stu-id="3a758-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="3a758-154">запрашивалось зашифрованное подключение и</span><span class="sxs-lookup"><span data-stu-id="3a758-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="3a758-155">сертификат сервера hello toonot доверия.</span><span class="sxs-lookup"><span data-stu-id="3a758-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="3a758-156">Это устанавливает соединение с помощью Transport Layer Security (TLS) и снижает риск атак в середине hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="3a758-157">Можно получить строки подключения с правильно настроенной для базы данных SQL для поддерживаемых клиентских драйверов из hello портал Azure как показано для ADO.net в этом снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="3a758-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="3a758-158">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="3a758-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="3a758-159">На hello **Обзор** для базы данных и щелкните **Показать строки подключения базы данных**.</span><span class="sxs-lookup"><span data-stu-id="3a758-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="3a758-160">Просмотрите hello завершения **ADO.NET** строку подключения.</span><span class="sxs-lookup"><span data-stu-id="3a758-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![Строка подключения по протоколу ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="3a758-162">Создание пользователей базы данных</span><span class="sxs-lookup"><span data-stu-id="3a758-162">Creating database users</span></span>

<span data-ttu-id="3a758-163">Прежде чем создавать пользователей, необходимо выбрать один из двух типов аутентификации, поддерживаемых базой данных SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="3a758-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="3a758-164">**Проверка подлинности SQL**, которое использует имя пользователя и пароль для входа и Здравствуйте, пользователи, которые допустимы только в контексте конкретной базы данных в логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="3a758-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="3a758-165">**Аутентификация Azure Active Directory**: используются удостоверения, управляемые Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3a758-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="3a758-166">Если требуется, чтобы toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate с базой данных SQL, заполненных Azure Active Directory должен существовать прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="3a758-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="3a758-167">Выполните эти шаги toocreate пользователя с помощью проверки подлинности SQL.</span><span class="sxs-lookup"><span data-stu-id="3a758-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="3a758-168">Подключение tooyour базы данных, например с помощью [SQL Server Management Studio](./sql-database-connect-query-ssms.md) с помощью свои учетные данные администратора сервера.</span><span class="sxs-lookup"><span data-stu-id="3a758-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="3a758-169">В обозревателе объектов щелкните правой кнопкой мыши в базе данных hello tooadd нового пользователя на и щелкните **новый запрос**.</span><span class="sxs-lookup"><span data-stu-id="3a758-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="3a758-170">Пустое окно запроса, откроется подключенных toohello выбранной базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="3a758-171">В окне запроса hello введите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="3a758-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="3a758-172">На панели инструментов hello, нажмите кнопку **Execute** toocreate hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="3a758-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="3a758-173">По умолчанию hello пользователя могут подключаться toohello базы данных, но не содержит разрешений tooread или записи данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="3a758-174">toogrant toohello эти разрешения только что созданный пользователь, выполните следующие две команды в новое окно запроса hello</span><span class="sxs-lookup"><span data-stu-id="3a758-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="3a758-175">Это лучший подход toocreate, эти учетные записи без прав администратора на уровне tooconnect tooyour hello базы данных базы данных, если только не требуется tooexecute задач администрирования, таких как создание новых пользователей.</span><span class="sxs-lookup"><span data-stu-id="3a758-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="3a758-176">Просмотрите hello [учебник по Azure Active Directory](./sql-database-aad-authentication-configure.md) о том, как tooauthenticate, с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3a758-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="3a758-177">Защита данных с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="3a758-177">Protect your data with encryption</span></span>

<span data-ttu-id="3a758-178">Прозрачное шифрование базы данных SQL Azure (TDE) автоматически шифрует данные при хранении, без необходимости любые изменения toohello приложения доступ к hello зашифрованной базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="3a758-179">Для новых баз данных прозрачное шифрование данных включено по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3a758-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="3a758-180">tooenable прозрачное шифрование данных для базы данных или tooverify, прозрачное шифрование данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3a758-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="3a758-181">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="3a758-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="3a758-182">Щелкните **прозрачное шифрование данных** страницы конфигурации hello tooopen для прозрачного шифрования данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![Прозрачное шифрование данных](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="3a758-184">При необходимости задайте **шифрование данных** tooON и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3a758-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="3a758-185">процесс шифрования Hello запускает в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="3a758-186">Отследить ход выполнения hello с помощью подключения базы данных tooSQL [SQL Server Management Studio](./sql-database-connect-query-ssms.md) путем запроса столбца encryption_state hello hello `sys.dm_database_encryption_keys` представления.</span><span class="sxs-lookup"><span data-stu-id="3a758-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="3a758-187">Включение аудита базы данных SQL (при необходимости)</span><span class="sxs-lookup"><span data-stu-id="3a758-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="3a758-188">Azure SQL Database Auditing отслеживает события базы данных и записывает их tooan журнал аудита вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3a758-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="3a758-189">Аудит может помочь вам соблюсти требования нормативов, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на предполагаемые нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="3a758-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="3a758-190">Выполните эти шаги toocreate политику аудита по умолчанию для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3a758-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="3a758-191">Выберите **баз данных SQL** hello левом меню и выберите базу данных на hello **баз данных SQL** страницы.</span><span class="sxs-lookup"><span data-stu-id="3a758-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="3a758-192">В колонке параметров hello выберите **аудита и обнаружения угроз**.</span><span class="sxs-lookup"><span data-stu-id="3a758-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="3a758-193">Обратите внимание, что аудит на уровне сервера отключено и наличии **проверить параметры сервера** ссылку, которая позволяет вам tooview или изменить параметры аудита сервера hello в данном контексте.</span><span class="sxs-lookup"><span data-stu-id="3a758-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![Колонка "Аудит"](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="3a758-195">При желании tooenable аудита типа (или расположение?) отличается от hello одно указанное на уровне сервера hello, включить **ON** аудита и выберите hello **большой двоичный объект** типа аудита.</span><span class="sxs-lookup"><span data-stu-id="3a758-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="3a758-196">Если включен аудит сервера больших двоичных объектов, hello настроена как база данных аудита будет существовать параллельно с hello server BLOB-объект аудита.</span><span class="sxs-lookup"><span data-stu-id="3a758-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![Включение аудита](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="3a758-198">Выберите **сведения о хранилище** tooopen hello колонке хранения журналов аудита.</span><span class="sxs-lookup"><span data-stu-id="3a758-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="3a758-199">Учетной записи хранилища Azure выберите hello, где будут сохраняться журналы и срок хранения hello, после которого hello старые журналы будут удалены, нажмите кнопку **ОК** внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="3a758-200">Используйте hello же учетная запись хранения для всех hello tooget аудита баз данных, наиболее эффективно использовать аудит hello сообщает шаблонов.</span><span class="sxs-lookup"><span data-stu-id="3a758-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="3a758-201">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3a758-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a758-202">Если требуется toocustomize hello аудиту события, это можно сделать через PowerShell или REST API - разделе hello [автоматизации (PowerShell или REST API)](sql-database-auditing.md#subheading-7) более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="3a758-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="3a758-203">Включение обнаружения угроз базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="3a758-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="3a758-204">Обнаружение угроз обеспечивает новый уровень безопасности, которая позволяет клиентам toodetect и отвечать toopotential угроз, как только они происходят, предоставляя предупреждения системы безопасности о подозрительной активности.</span><span class="sxs-lookup"><span data-stu-id="3a758-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="3a758-205">Пользователи могут анализировать hello подозрительных событий с помощью toodetermine аудита базы данных SQL, если они в результате попытки tooaccess, нарушения или воспользоваться hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="3a758-206">Обнаружение угроз база данных он простой tooaddress потенциальных угроз toohello без необходимости hello toobe специалист по безопасности или управлять повышенной безопасности, контроль различных систем.</span><span class="sxs-lookup"><span data-stu-id="3a758-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="3a758-207">Например, система обнаружения угроз обнаруживает определенную подозрительную активность в базе данных, указывающую на потенциальные попытки внедрения кода SQL.</span><span class="sxs-lookup"><span data-stu-id="3a758-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="3a758-208">Внедрение кода SQL — одно из hello общих Web вопросами безопасности приложений на hello Интернета, используемых tooattack управляемых данными приложений.</span><span class="sxs-lookup"><span data-stu-id="3a758-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="3a758-209">Злоумышленникам воспользоваться преимуществами tooinject уязвимостей приложения злонамеренные инструкции SQL в поля записи приложения, для нарушению или изменение данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="3a758-210">Перейдите в колонку toohello конфигурации из базы данных SQL требуется toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="3a758-211">В колонке параметров hello выберите **аудита и обнаружения угроз**.</span><span class="sxs-lookup"><span data-stu-id="3a758-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Область навигации](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="3a758-213">В hello **аудита и обнаружения угроз** Включение колонке конфигурации **ON** аудита, который будет отображать параметры обнаружения угроз hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="3a758-214">Переведите переключатель обнаружения угроз в положение **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="3a758-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="3a758-215">Настройте hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальные действия базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="3a758-216">Нажмите кнопку **Сохранить** в hello **аудита и угрозы обнаружения** toosave колонке hello новых или обновленных политику аудита и угрозы обнаружения.</span><span class="sxs-lookup"><span data-stu-id="3a758-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![Область навигации](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="3a758-218">При обнаружении подозрительных действий в базе данных вы получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="3a758-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="3a758-219">Hello электронной почты будут представлены сведения события hello подозрительные безопасности, включая характер hello hello аномальных действий, имя базы данных, время события сервера имя и hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="3a758-220">Кроме того он предоставит сведения о возможных причинах и рекомендуется tooinvestigate действия и устранить базы данных toohello hello потенциальных угроз.</span><span class="sxs-lookup"><span data-stu-id="3a758-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="3a758-221">Hello обход далее шаги можно выполнить с помощью какие toodo вы должны получать такие сообщения электронной почты:</span><span class="sxs-lookup"><span data-stu-id="3a758-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![Электронное сообщение об обнаружении угроз](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="3a758-223">В сообщении электронной почты hello, нажмите кнопку hello **журнал аудита SQL Azure** ссылку, которая будет запустите hello портал Azure и показывает соответствующие записи аудита hello вокруг hello время hello подозрительные события.</span><span class="sxs-lookup"><span data-stu-id="3a758-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![Записи аудита](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="3a758-225">Дополнительные сведения о действия hello подозрительных баз данных, такие как инструкции SQL, щелкните tooview записей аудита hello сбоя IP причину и клиента.</span><span class="sxs-lookup"><span data-stu-id="3a758-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Сведения о записи](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="3a758-227">В колонке hello записей аудита, щелкните **открыть в Excel** excel tooopen предварительно настроенный шаблон tooimport и выполнения углубленного анализа журнала аудита hello вокруг hello время hello подозрительные события.</span><span class="sxs-lookup"><span data-stu-id="3a758-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3a758-228">В Excel 2010 или более поздней версии, Power Query и hello **Быстрое объединение** параметр является обязательным.</span><span class="sxs-lookup"><span data-stu-id="3a758-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Открытые записей в Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="3a758-230">tooconfigure hello **Быстрое объединение** параметр - в hello **POWER QUERY** выберите вкладку ленты **параметры** toodisplay диалогового окна параметров hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="3a758-231">Выберите раздел конфиденциальности hello и выберите второй параметр hello - «Игнорировать уровни конфиденциальности hello и повысить производительность»:</span><span class="sxs-lookup"><span data-stu-id="3a758-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Быстрое объединение в Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="3a758-233">журналы аудита tooload SQL, убедитесь, что hello параметры на вкладке Параметры hello установлены правильно, а затем выберите ленту «Данные» hello и нажмите кнопку «Обновить все» hello.</span><span class="sxs-lookup"><span data-stu-id="3a758-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Параметры Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="3a758-235">Hello результаты отображаются в hello **журналы аудита SQL** лист, позволяющий более глубокого анализа toorun hello аномальных действий, которые были обнаружены и сократить влияние hello hello событий безопасности в приложении.</span><span class="sxs-lookup"><span data-stu-id="3a758-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3a758-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a758-236">Next steps</span></span>
<span data-ttu-id="3a758-237">Можно улучшить защиту hello базы данных на соответствие пользователей-злоумышленников или несанкционированного доступа с помощью нескольких простых шагов.</span><span class="sxs-lookup"><span data-stu-id="3a758-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="3a758-238">Из этого руководства вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="3a758-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="3a758-239">Настройка правил брандмауэра для сервера и базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a758-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="3a758-240">Подключиться с помощью строки безопасного подключения базы данных tooyour</span><span class="sxs-lookup"><span data-stu-id="3a758-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="3a758-241">Управление доступом пользователей.</span><span class="sxs-lookup"><span data-stu-id="3a758-241">Manage user access</span></span>
> * <span data-ttu-id="3a758-242">Защита данных с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="3a758-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="3a758-243">Включение аудита базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="3a758-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="3a758-244">Включение обнаружения угроз базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="3a758-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
><span data-ttu-id="3a758-245">[Troubleshoot performance issues and optimize your database](sql-database-performance-tutorial.md) (Устранение проблем с производительностью и оптимизация базы данных)</span><span class="sxs-lookup"><span data-stu-id="3a758-245">[Improve SQL Database performance](sql-database-performance-tutorial.md)</span></span>

