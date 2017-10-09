---
title: "Always Encrypted: База данных SQL Azure и хранилище сертификатов Windows | Документация Майкрософт"
description: "В этой статье показано, как toosecure конфиденциальных данных в базе данных SQL с помощью шифрования базы данных с помощью hello мастер из постоянного шифрования в SQL Server Management Studio (SSMS). Он также показывает, как toostore ключей шифрования в сертификате Windows hello хранения."
keywords: "шифрование данных, шифрование SQL, шифрование базы данных, конфиденциальные данные, постоянное шифрование"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="15cfa-105">Постоянное шифрование: Защита конфиденциальных данных в базе данных SQL и хранение ключей шифрования в хранилище сертификатов Windows hello</span><span class="sxs-lookup"><span data-stu-id="15cfa-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="15cfa-106">В этой статье показано, как toosecure конфиденциальных данных в SQL базы данных с помощью шифрования базы данных с помощью hello [мастер постоянного шифрования](https://msdn.microsoft.com/library/mt459280.aspx) в [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cfa-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="15cfa-107">Он также показывает, как toostore ключей шифрования в сертификате Windows hello хранения.</span><span class="sxs-lookup"><span data-stu-id="15cfa-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="15cfa-108">Постоянное шифрование — новая технология шифрования данных в базе данных SQL Azure и SQL Server, который помогает защитить конфиденциальные данные хранятся на сервере hello во время перемещения между клиентом и сервером и hello данных во время использования, обеспечивая эти конфиденциальные данные никогда не отображается в виде открытого текста внутри системы hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="15cfa-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="15cfa-109">После шифрование данных, только клиентских приложений или серверов приложений, которые имеют toohello клавиши доступа можно использовать данные в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="15cfa-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="15cfa-110">Дополнительные сведения см. в статье [Always Encrypted (ядро СУБД)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cfa-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="15cfa-111">После настройки базы данных toouse hello, постоянное шифрование, вы создадите клиентское приложение на C# с toowork Visual Studio с hello зашифрованные данные.</span><span class="sxs-lookup"><span data-stu-id="15cfa-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="15cfa-112">Выполните действия hello в этой статье toolearn как tooset копирование постоянного шифрования для базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="15cfa-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="15cfa-113">В этой статье вы узнаете, как hello tooperform следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="15cfa-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="15cfa-114">Мастер постоянного шифрования используйте hello в SSMS toocreate [ключей постоянного шифрования](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="15cfa-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="15cfa-115">Создавать [главный ключ столбца](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cfa-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="15cfa-116">Создавать [ключ шифрования столбца](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cfa-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="15cfa-117">Создавать таблицу базы данных и шифровать столбцы.</span><span class="sxs-lookup"><span data-stu-id="15cfa-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="15cfa-118">Создание приложения, которое вставляет, выбирает и отображает данные из столбцов шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="15cfa-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15cfa-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="15cfa-119">Prerequisites</span></span>
<span data-ttu-id="15cfa-120">Для работы с этим руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="15cfa-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="15cfa-121">Учетная запись и подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="15cfa-121">An Azure account and subscription.</span></span> <span data-ttu-id="15cfa-122">Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15cfa-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="15cfa-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) версии 13.0.700.242 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="15cfa-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="15cfa-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) или более поздней версии (на компьютере клиента hello).</span><span class="sxs-lookup"><span data-stu-id="15cfa-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="15cfa-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="15cfa-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="15cfa-126">Создание пустой базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="15cfa-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="15cfa-127">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="15cfa-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="15cfa-128">Выберите **Создать** > **Данные+хранилище** > **База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="15cfa-129">Создайте **пустую** базу данных **Clinic** на новом или имеющемся сервере.</span><span class="sxs-lookup"><span data-stu-id="15cfa-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="15cfa-130">Подробные инструкции о создании базы данных в hello портала Azure см. в разделе [первой базы данных Azure SQL](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15cfa-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Создание пустой базы данных](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="15cfa-132">Строка подключения hello потребуется далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="15cfa-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="15cfa-133">После создания базы данных hello перейдите toohello новую Clinic базы данных и скопируйте hello строку подключения.</span><span class="sxs-lookup"><span data-stu-id="15cfa-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="15cfa-134">Строка подключения hello можно получить в любое время, но это просто toocopy его при работе в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="15cfa-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="15cfa-135">Выберите **Базы данных SQL** > **Clinic** > **Показать строки подключения к базам данных**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="15cfa-136">Скопируйте строку подключения hello для **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Скопируйте строку подключения hello](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="15cfa-138">Подключитесь к SSMS toohello базы данных</span><span class="sxs-lookup"><span data-stu-id="15cfa-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="15cfa-139">Откройте SSMS и подключите сервер toohello с базой данных Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="15cfa-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="15cfa-140">Откройте среду SSMS.</span><span class="sxs-lookup"><span data-stu-id="15cfa-140">Open SSMS.</span></span> <span data-ttu-id="15cfa-141">(Щелкните **Connect** > **компонент Database Engine** tooopen hello **подключения tooServer** окно, если он не открыт).</span><span class="sxs-lookup"><span data-stu-id="15cfa-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="15cfa-142">Введите имя сервера и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="15cfa-142">Enter your server name and credentials.</span></span> <span data-ttu-id="15cfa-143">Имя сервера Hello можно найти в колонке базы данных SQL hello и в строке подключения hello скопированное ранее.</span><span class="sxs-lookup"><span data-stu-id="15cfa-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="15cfa-144">Тип hello полного сервера имя, включая *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="15cfa-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Скопируйте строку подключения hello](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="15cfa-146">Если hello **новое правило брандмауэра** откроется окно входа в tooAzure и SSMS позволяют создать новое правило брандмауэра для вас.</span><span class="sxs-lookup"><span data-stu-id="15cfa-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="15cfa-147">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="15cfa-147">Create a table</span></span>
<span data-ttu-id="15cfa-148">В этом разделе вы создадите таблицу данных пациента toohold.</span><span class="sxs-lookup"><span data-stu-id="15cfa-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="15cfa-149">Это будет обычный стол изначально--вы настроите шифрования в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="15cfa-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="15cfa-150">Разверните узел **Базы данных**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="15cfa-151">Щелкните правой кнопкой мыши hello **Clinic** базы данных и нажмите кнопку **новый запрос**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="15cfa-152">Вставить hello, следуя Transact-SQL (T-SQL) в новое окно запроса hello и **Execute** его.</span><span class="sxs-lookup"><span data-stu-id="15cfa-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="15cfa-153">Шифрование столбцов (настройка Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="15cfa-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="15cfa-154">Мастер предоставляет SSMS tooeasily Настройка постоянного шифрования с помощью настройки hello CMK CEK и зашифрованные столбцы автоматически.</span><span class="sxs-lookup"><span data-stu-id="15cfa-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="15cfa-155">Разверните узел **Базы данных** > **Clinic** > **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="15cfa-156">Щелкните правой кнопкой мыши hello **пациентов** таблицы и выберите **зашифровать столбцы** мастер постоянного шифрования tooopen hello:</span><span class="sxs-lookup"><span data-stu-id="15cfa-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Шифрование столбцов…](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="15cfa-158">Hello мастер постоянного шифрования включает в себя hello в следующих разделах: **выделенный фрагмент столбца**, **Конфигурация главного ключа** (CMK), **проверки**, и  **Сводка**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="15cfa-159">Выполните действия на странице Выбор столбцов.</span><span class="sxs-lookup"><span data-stu-id="15cfa-159">Column Selection</span></span>
<span data-ttu-id="15cfa-160">Нажмите кнопку **Далее** на hello **Введение** страницы приветствия tooopen **выделенный фрагмент столбца** страницы.</span><span class="sxs-lookup"><span data-stu-id="15cfa-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="15cfa-161">На этой странице будет выбрать столбцы, которые вы хотите tooencrypt, [hello тип шифрования и определите, какой ключ шифрования столбца (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="15cfa-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="15cfa-162">Для каждого пациента необходимо зашифровать данные в столбцах **SSN** и **BirthDate**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="15cfa-163">Hello **SSN** столбец будет использоваться детерминированного шифрования, поддерживающую равенство, соединения и группировать.</span><span class="sxs-lookup"><span data-stu-id="15cfa-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="15cfa-164">Hello **BirthDate** столбец будет использоваться при выполнении случайного шифрования не поддерживает операции.</span><span class="sxs-lookup"><span data-stu-id="15cfa-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="15cfa-165">Набор hello **тип шифрования** для hello **SSN** столбец слишком**Deterministic** и hello **BirthDate** столбец слишком **Случайное**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="15cfa-166">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-166">Click **Next**.</span></span>

![Шифрование столбцов…](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="15cfa-168">Настройка главного ключа</span><span class="sxs-lookup"><span data-stu-id="15cfa-168">Master Key Configuration</span></span>
<span data-ttu-id="15cfa-169">Hello **Конфигурация главного ключа** страница является задаются копии базы данных и выберите hello поставщика хранилища ключей CMK hello CMK хранения.</span><span class="sxs-lookup"><span data-stu-id="15cfa-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="15cfa-170">В настоящее время Главным можно хранить в хранилище сертификатов Windows hello, хранилище ключей или аппаратный модуль безопасности (HSM).</span><span class="sxs-lookup"><span data-stu-id="15cfa-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="15cfa-171">В этом учебнике показано, как toostore ключей сертификата Windows hello хранения.</span><span class="sxs-lookup"><span data-stu-id="15cfa-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="15cfa-172">Убедитесь, что параметр **Хранилище сертификатов Windows** выбран, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Настройка главного ключа](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="15cfa-174">Проверка</span><span class="sxs-lookup"><span data-stu-id="15cfa-174">Validation</span></span>
<span data-ttu-id="15cfa-175">Могут быть зашифрованы hello столбцы сейчас или сохранить сценарий PowerShell toorun позже.</span><span class="sxs-lookup"><span data-stu-id="15cfa-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="15cfa-176">В этом учебнике выберите **теперь продолжить toofinish** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="15cfa-177">Сводка</span><span class="sxs-lookup"><span data-stu-id="15cfa-177">Summary</span></span>
<span data-ttu-id="15cfa-178">Убедитесь, что hello параметры заданы правильно и нажмите кнопку **Готово** toocomplete hello установки для постоянного шифрования.</span><span class="sxs-lookup"><span data-stu-id="15cfa-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Сводка](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="15cfa-180">Проверка действий мастера hello</span><span class="sxs-lookup"><span data-stu-id="15cfa-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="15cfa-181">После завершения работы мастера hello базы данных настроена для постоянного шифрования.</span><span class="sxs-lookup"><span data-stu-id="15cfa-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="15cfa-182">выполнить мастер hello Hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="15cfa-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="15cfa-183">создал CMK;</span><span class="sxs-lookup"><span data-stu-id="15cfa-183">Created a CMK.</span></span>
* <span data-ttu-id="15cfa-184">создал CEK;</span><span class="sxs-lookup"><span data-stu-id="15cfa-184">Created a CEK.</span></span>
* <span data-ttu-id="15cfa-185">Настроенный hello выбранные столбцы для шифрования.</span><span class="sxs-lookup"><span data-stu-id="15cfa-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="15cfa-186">Ваш **пациентов** таблицы в настоящее время не содержит данных, но все существующие данные в столбцах выбран hello теперь шифруется.</span><span class="sxs-lookup"><span data-stu-id="15cfa-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="15cfa-187">Создание hello hello ключей в среде SSMS можно проверить, происходит слишком**Clinic** > **безопасности** > **ключей постоянного шифрования**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="15cfa-188">Теперь можно увидеть hello новые ключи, которые hello мастера, созданный для вас.</span><span class="sxs-lookup"><span data-stu-id="15cfa-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="15cfa-189">Создание клиентского приложения, которое работает с данными зашифрован hello</span><span class="sxs-lookup"><span data-stu-id="15cfa-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="15cfa-190">Теперь, когда Настройка постоянного шифрования можно построить приложение, выполняющее *вставляет* и *выбирает* на hello зашифрованные столбцы.</span><span class="sxs-lookup"><span data-stu-id="15cfa-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="15cfa-191">toosuccessfully запустить пример приложения hello, его необходимо запустить на hello же компьютере, где вы запустили мастер постоянного шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="15cfa-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="15cfa-192">приложение hello toorun на другом компьютере, необходимо развернуть постоянное шифрование сертификаты toohello компьютер, запустив приложение hello клиента.</span><span class="sxs-lookup"><span data-stu-id="15cfa-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="15cfa-193">Приложение должно использовать [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) объектов при передаче сервер toohello данных открытого текста с всегда зашифрованным столбцам.</span><span class="sxs-lookup"><span data-stu-id="15cfa-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="15cfa-194">Передача значений литералов без использования объектов SqlParameter приведет к возникновению исключения.</span><span class="sxs-lookup"><span data-stu-id="15cfa-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="15cfa-195">Откройте Visual Studio и создайте консольное приложение на языке C#.</span><span class="sxs-lookup"><span data-stu-id="15cfa-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="15cfa-196">Убедитесь, что проект настроен слишком**.NET Framework 4.6** или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="15cfa-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="15cfa-197">Имя проекта hello **AlwaysEncryptedConsoleApp** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Новое консольное приложение](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="15cfa-199">Изменение вашей tooenable строку соединения, постоянное шифрование</span><span class="sxs-lookup"><span data-stu-id="15cfa-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="15cfa-200">В этом разделе объясняется, как tooenable всегда зашифрованы в строке подключения базы данных.</span><span class="sxs-lookup"><span data-stu-id="15cfa-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="15cfa-201">Вы измените hello консольного приложения, созданный в следующем разделе hello, «Всегда зашифровано пример консольного приложения».</span><span class="sxs-lookup"><span data-stu-id="15cfa-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="15cfa-202">tooenable постоянного шифрования, необходимо tooadd hello **параметр шифрования столбца** tooyour соединения ключевое слово строки и задать для него слишком**включено**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="15cfa-203">Это можно задать непосредственно в строке подключения hello или его можно задать с помощью [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cfa-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="15cfa-204">Пример приложения Hello в hello следующем разделе показано как toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="15cfa-205">Это единственное изменение hello в конкретных tooAlways каталога приложений клиент шифрование требуется.</span><span class="sxs-lookup"><span data-stu-id="15cfa-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="15cfa-206">При наличии существующих приложений, сохраняет извне его строка подключения (то есть, в файле конфигурации), может tooenable постоянного шифрования может быть без изменения кода.</span><span class="sxs-lookup"><span data-stu-id="15cfa-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="15cfa-207">Включить постоянное шифрование в строке подключения hello</span><span class="sxs-lookup"><span data-stu-id="15cfa-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="15cfa-208">Добавьте следующие строки подключения tooyour ключевое слово hello.</span><span class="sxs-lookup"><span data-stu-id="15cfa-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="15cfa-209">Активация функции постоянного шифрования с помощью SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="15cfa-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="15cfa-210">Hello следующий код показывает, как hello tooenable постоянное шифрование, задав [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) слишком[включено](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cfa-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="15cfa-211">Пример консольного приложения с функцией постоянного шифрования</span><span class="sxs-lookup"><span data-stu-id="15cfa-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="15cfa-212">В этом примере показано, как:</span><span class="sxs-lookup"><span data-stu-id="15cfa-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="15cfa-213">Измените ваш tooenable строку соединения, постоянное шифрование.</span><span class="sxs-lookup"><span data-stu-id="15cfa-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="15cfa-214">Вставка данных в hello зашифрованные столбцы.</span><span class="sxs-lookup"><span data-stu-id="15cfa-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="15cfa-215">Выбрать запись, выполнив фильтрацию по конкретному значению в зашифрованном столбце.</span><span class="sxs-lookup"><span data-stu-id="15cfa-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="15cfa-216">Замените содержимое hello **Program.cs** с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="15cfa-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="15cfa-217">Замените строку соединения hello для hello connectionString глобальной переменной в строку hello непосредственно над hello метода Main вашего допустимую строку соединения из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="15cfa-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="15cfa-218">Это единственное изменение hello требуется toomake toothis код.</span><span class="sxs-lookup"><span data-stu-id="15cfa-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="15cfa-219">Запустите toosee приложения hello постоянного шифрования в действии.</span><span class="sxs-lookup"><span data-stu-id="15cfa-219">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="15cfa-220">Убедитесь, что hello шифрование</span><span class="sxs-lookup"><span data-stu-id="15cfa-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="15cfa-221">Вы можете быстро проверить шифрование hello фактических данных на сервере hello, запрашивая hello **пациентов** данных с помощью среды SSMS.</span><span class="sxs-lookup"><span data-stu-id="15cfa-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="15cfa-222">(Использовать текущее соединение где параметр шифрования столбца hello еще не включен).</span><span class="sxs-lookup"><span data-stu-id="15cfa-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="15cfa-223">Запустите приветствия при следующем запросе в базе данных Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="15cfa-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="15cfa-224">Вы увидите, что hello зашифрованные столбцы не содержат все зашифрованные данные.</span><span class="sxs-lookup"><span data-stu-id="15cfa-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Новое консольное приложение](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="15cfa-226">toouse SSMS tooaccess Здравствуйте зашифрованные данные, можно добавить hello **параметр шифрования столбца = включен** параметр toohello соединения.</span><span class="sxs-lookup"><span data-stu-id="15cfa-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="15cfa-227">В **обозревателе объектов** SSMS щелкните сервер правой кнопкой мыши и выберите пункт **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="15cfa-228">Нажмите кнопку **Connect** > **компонент Database Engine** tooopen hello **подключения tooServer** , а затем выбрать **параметры**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="15cfa-229">Щелкните **Дополнительные параметры соединения** и введите **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="15cfa-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Новое консольное приложение](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="15cfa-231">Выполнения hello следующий запрос на hello **Clinic** базы данных.</span><span class="sxs-lookup"><span data-stu-id="15cfa-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="15cfa-232">Теперь можно увидеть hello зашифрованные данные в столбцах hello зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="15cfa-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Новое консольное приложение](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="15cfa-234">При подключении с помощью SSMS (или любого клиента) с другого компьютера, он не будет доступа ключи шифрования toohello и не будет возможности toodecrypt hello данных.</span><span class="sxs-lookup"><span data-stu-id="15cfa-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="15cfa-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="15cfa-235">Next steps</span></span>
<span data-ttu-id="15cfa-236">После создания базы данных, которая использует постоянное шифрование, вы можете toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="15cfa-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="15cfa-237">Запустить этот пример с другого компьютера.</span><span class="sxs-lookup"><span data-stu-id="15cfa-237">Run this sample from a different computer.</span></span> <span data-ttu-id="15cfa-238">Он не будет ключи шифрования toohello доступа, поэтому он не будет иметь доступ к данным открытым текстом toohello и не будут выполняться успешно.</span><span class="sxs-lookup"><span data-stu-id="15cfa-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="15cfa-239">[Сменить и очистить ключи](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cfa-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="15cfa-240">[Перенести данные, которые уже зашифрованы с использованием функции Always Encrypted.](https://msdn.microsoft.com/library/mt621539.aspx)</span><span class="sxs-lookup"><span data-stu-id="15cfa-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="15cfa-241">[Развертывание постоянного шифрования клиентских машин сертификаты tooother](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (см. раздел «Превращение tooApplications доступные сертификаты и пользователей» hello).</span><span class="sxs-lookup"><span data-stu-id="15cfa-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="15cfa-242">Связанные сведения</span><span class="sxs-lookup"><span data-stu-id="15cfa-242">Related information</span></span>
* [<span data-ttu-id="15cfa-243">Always Encrypted (разработка клиентских приложений)</span><span class="sxs-lookup"><span data-stu-id="15cfa-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="15cfa-244">Transparent Data Encryption (Прозрачное шифрование данных)</span><span class="sxs-lookup"><span data-stu-id="15cfa-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="15cfa-245">SQL Server Encryption (Шифрование SQL Server)</span><span class="sxs-lookup"><span data-stu-id="15cfa-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="15cfa-246">Always Encrypted Wizard (Мастер настройки постоянного шифрования)</span><span class="sxs-lookup"><span data-stu-id="15cfa-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="15cfa-247">Блог по функции постоянного шифрования</span><span class="sxs-lookup"><span data-stu-id="15cfa-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

