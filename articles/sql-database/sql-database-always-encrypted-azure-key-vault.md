---
title: "Always Encrypted: База данных SQL и Azure Key Vault | Документация Майкрософт"
description: "В этой статье показано, как toosecure конфиденциальных данных в базе данных SQL с использованием шифрования данных hello мастер постоянного шифрования в SQL Server Management Studio. Оно также содержит инструкции, которые будет показано, как toostore каждый ключ шифрования в хранилище ключей Azure."
keywords: "шифрование данных, ключ шифрования, шифрование в облаке"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="52eff-105">Always Encrypted: защита конфиденциальных данных в Базе данных SQL и хранение ключей шифрования в хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="52eff-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="52eff-106">В этой статье показано, как базы данных с помощью шифрования данных с помощью hello toosecure конфиденциальных данных в SQL [мастер постоянного шифрования](https://msdn.microsoft.com/library/mt459280.aspx) в [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="52eff-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="52eff-107">Оно также содержит инструкции, которые будет показано, как toostore каждый ключ шифрования в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="52eff-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="52eff-108">Всегда шифрование — это новая технология шифрования данных в базе данных SQL Azure и SQL Server, который помогает защитить конфиденциальные данные хранятся на сервере hello во время перемещения между клиентом и сервером, а также hello данных во время использования.</span><span class="sxs-lookup"><span data-stu-id="52eff-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="52eff-109">Всегда шифрование гарантирует, конфиденциальные данные никогда не отображается как обычный текст внутри hello системы базы данных.</span><span class="sxs-lookup"><span data-stu-id="52eff-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="52eff-110">После настройки шифрования данных только для клиентских приложений или серверов приложений, которые имеют toohello клавиши доступа можно доступ к данным открытым текстом.</span><span class="sxs-lookup"><span data-stu-id="52eff-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="52eff-111">Дополнительные сведения см. в статье [Always Encrypted (ядро СУБД)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="52eff-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="52eff-112">После настройки базы данных toouse hello, постоянное шифрование, вы создадите клиентское приложение на C# с toowork Visual Studio с hello зашифрованные данные.</span><span class="sxs-lookup"><span data-stu-id="52eff-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="52eff-113">Выполните действия hello в этой статье и узнайте, как tooset копирование постоянного шифрования для базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="52eff-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="52eff-114">В этой статье вы узнаете, как hello tooperform следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="52eff-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="52eff-115">Мастер постоянного шифрования используйте hello в SSMS toocreate [ключей постоянного шифрования](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="52eff-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="52eff-116">Создавать [главный ключ столбца (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="52eff-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="52eff-117">Создавать [ключ шифрования столбца (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="52eff-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="52eff-118">Создавать таблицу базы данных и шифровать столбцы.</span><span class="sxs-lookup"><span data-stu-id="52eff-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="52eff-119">Создание приложения, которое вставляет, выбирает и отображает данные из столбцов шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52eff-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="52eff-120">Prerequisites</span></span>
<span data-ttu-id="52eff-121">Для работы с этим руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="52eff-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="52eff-122">Учетная запись и подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="52eff-122">An Azure account and subscription.</span></span> <span data-ttu-id="52eff-123">Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52eff-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="52eff-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) версии 13.0.700.242 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="52eff-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="52eff-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) или более поздней версии (на компьютере клиента hello).</span><span class="sxs-lookup"><span data-stu-id="52eff-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="52eff-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="52eff-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="52eff-127">[Azure PowerShell](/powershell/azure/overview) 1.0.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="52eff-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="52eff-128">Тип **(Get-Module azure - ListAvailable). Версия** toosee управлением какой версии PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52eff-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="52eff-129">Включить службы клиентского приложения tooaccess hello базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="52eff-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="52eff-130">Необходимо включить службы клиентского приложения tooaccess hello базы данных SQL, настроив hello обязательную проверку подлинности и получении hello *ClientId* и *секрет* потребуется tooauthenticate приложение hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="52eff-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="52eff-131">Откройте hello [классический портал Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="52eff-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="52eff-132">Выберите **Active Directory** и щелкните экземпляр Active Directory hello, приложение будет использовать.</span><span class="sxs-lookup"><span data-stu-id="52eff-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="52eff-133">Щелкните **Приложения**, а затем — **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="52eff-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="52eff-134">Введите имя для вашего приложения (например: *myClientApp*), выберите **веб-приложение**и щелкните стрелку toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="52eff-135">Для hello **URL-адрес входа** и **URI идентификатора приложения** можно ввести допустимый URL-адрес (например, *http://myClientApp*) и продолжить.</span><span class="sxs-lookup"><span data-stu-id="52eff-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="52eff-136">Нажмите **НАСТРОИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="52eff-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="52eff-137">Скопируйте значение **ИДЕНТИФИКАТОР КЛИЕНТА**.</span><span class="sxs-lookup"><span data-stu-id="52eff-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="52eff-138">(Оно потребуется в коде позже.)</span><span class="sxs-lookup"><span data-stu-id="52eff-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="52eff-139">В hello **ключей** выберите **1 год** из hello **выберите длительность** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="52eff-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="52eff-140">(Необходимо будет скопировать ключ hello после сохранения на шаге 13.)</span><span class="sxs-lookup"><span data-stu-id="52eff-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="52eff-141">Прокрутите вниз и щелкните **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="52eff-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="52eff-142">Оставить **Показать** значение слишком**приложения Майкрософт** и выберите **API управления службами Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="52eff-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="52eff-143">Щелкните флажок toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="52eff-144">Выберите **Azure службы управления доступом...**  из hello **делегированные разрешения** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="52eff-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="52eff-145">Щелкните **СОХРАНИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="52eff-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="52eff-146">После hello сохранить завершения, скопируйте значение ключа hello в hello **ключей** раздела.</span><span class="sxs-lookup"><span data-stu-id="52eff-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="52eff-147">(Оно потребуется в коде позже.)</span><span class="sxs-lookup"><span data-stu-id="52eff-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="52eff-148">Создание ключей toostore хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="52eff-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="52eff-149">Теперь, клиентское приложение настроено, и у вас есть свой идентификатор клиента, он время toocreate хранилища ключей и настроить ее политику доступа, вы и приложения могут получить доступ hello хранилище секретов (ключи постоянного шифрования hello).</span><span class="sxs-lookup"><span data-stu-id="52eff-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="52eff-150">Hello *создания*, *получить*, *списка*, *входа*, *проверить*, *wrapKey*, и *unwrapKey* требуются разрешения для создания нового главного ключа столбца и настройке шифрования с SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="52eff-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="52eff-151">Можно быстро создать хранилище ключей, выполнив следующий скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="52eff-152">Подробное описание этих командлетов и дополнительные сведения о создании и настройке хранилища ключей см. в статье [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="52eff-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="52eff-153">Создание пустой базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="52eff-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="52eff-154">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="52eff-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="52eff-155">Go слишком**New** > **данные + хранилище** > **базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="52eff-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="52eff-156">Создайте **пустую** базу данных **Clinic** на новом или имеющемся сервере.</span><span class="sxs-lookup"><span data-stu-id="52eff-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="52eff-157">Подробные инструкции о том, как toocreate базы данных в hello портал Azure отображается [первой базы данных Azure SQL](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="52eff-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Создание пустой базы данных](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="52eff-159">Будет необходимо hello строка подключения далее в учебнике hello, поэтому после создания базы данных hello перейдите toohello новую Clinic базы данных и скопируйте hello строку подключения.</span><span class="sxs-lookup"><span data-stu-id="52eff-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="52eff-160">Строка подключения hello можно получить в любое время, но это просто toocopy его в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="52eff-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="52eff-161">Go слишком**баз данных SQL** > **Clinic** > **Показать строки подключения базы данных**.</span><span class="sxs-lookup"><span data-stu-id="52eff-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="52eff-162">Скопируйте строку подключения hello для **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="52eff-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Скопируйте строку подключения hello](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="52eff-164">Подключитесь к SSMS toohello базы данных</span><span class="sxs-lookup"><span data-stu-id="52eff-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="52eff-165">Откройте SSMS и подключите сервер toohello с базой данных Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="52eff-166">Откройте среду SSMS.</span><span class="sxs-lookup"><span data-stu-id="52eff-166">Open SSMS.</span></span> <span data-ttu-id="52eff-167">(Перейдите слишком**Connect** > **компонент Database Engine** tooopen hello **подключения tooServer** окно, если он еще не открыт.)</span><span class="sxs-lookup"><span data-stu-id="52eff-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="52eff-168">Введите имя сервера и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="52eff-168">Enter your server name and credentials.</span></span> <span data-ttu-id="52eff-169">Имя сервера Hello можно найти в колонке базы данных SQL hello и в строке подключения hello скопированное ранее.</span><span class="sxs-lookup"><span data-stu-id="52eff-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="52eff-170">Имя полного сервера hello типа, включая *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="52eff-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![Скопируйте строку подключения hello](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="52eff-172">Если hello **новое правило брандмауэра** откроется окно входа в tooAzure и SSMS позволяют создать новое правило брандмауэра для вас.</span><span class="sxs-lookup"><span data-stu-id="52eff-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="52eff-173">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="52eff-173">Create a table</span></span>
<span data-ttu-id="52eff-174">В этом разделе вы создадите таблицу данных пациента toohold.</span><span class="sxs-lookup"><span data-stu-id="52eff-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="52eff-175">Это не первоначально зашифрованы--вы настроите шифрования в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="52eff-176">Разверните узел **Базы данных**.</span><span class="sxs-lookup"><span data-stu-id="52eff-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="52eff-177">Щелкните правой кнопкой мыши hello **Clinic** базы данных и нажмите кнопку **новый запрос**.</span><span class="sxs-lookup"><span data-stu-id="52eff-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="52eff-178">Вставить hello, следуя Transact-SQL (T-SQL) в новое окно запроса hello и **Execute** его.</span><span class="sxs-lookup"><span data-stu-id="52eff-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="52eff-179">Шифрование столбцов (настройка Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="52eff-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="52eff-180">Среда SSMS предоставляет мастер, который помогает легко настроить постоянного шифрования с помощью настройки главного ключа столбца hello, ключ шифрования столбца и зашифрованных столбцов для вас.</span><span class="sxs-lookup"><span data-stu-id="52eff-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="52eff-181">Разверните узел **Базы данных** > **Clinic** > **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="52eff-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="52eff-182">Щелкните правой кнопкой мыши hello **пациентов** таблицы и выберите **зашифровать столбцы** мастер постоянного шифрования tooopen hello:</span><span class="sxs-lookup"><span data-stu-id="52eff-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Шифрование столбцов…](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="52eff-184">Hello мастер постоянного шифрования включает в себя hello в следующих разделах: **выделенный фрагмент столбца**, **Конфигурация главного ключа**, **проверки**, и **Сводка** .</span><span class="sxs-lookup"><span data-stu-id="52eff-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="52eff-185">Выполните действия на странице Выбор столбцов.</span><span class="sxs-lookup"><span data-stu-id="52eff-185">Column Selection</span></span>
<span data-ttu-id="52eff-186">Нажмите кнопку **Далее** на hello **Введение** страницы приветствия tooopen **выделенный фрагмент столбца** страницы.</span><span class="sxs-lookup"><span data-stu-id="52eff-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="52eff-187">На этой странице будет выбрать столбцы, которые вы хотите tooencrypt, [hello тип шифрования и определите, какой ключ шифрования столбца (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="52eff-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="52eff-188">Для каждого пациента необходимо зашифровать данные в столбцах **SSN** и **BirthDate**.</span><span class="sxs-lookup"><span data-stu-id="52eff-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="52eff-189">столбец SSN Hello будет использовать детерминированного шифрования, поддерживающую равенство, соединения и группировать.</span><span class="sxs-lookup"><span data-stu-id="52eff-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="52eff-190">столбец BirthDate Hello будет использовать при выполнении случайного шифрования не поддерживает операции.</span><span class="sxs-lookup"><span data-stu-id="52eff-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="52eff-191">Набор hello **тип шифрования** для столбца hello SSN слишком**Deterministic** и hello столбца BirthDate слишком**случайное**.</span><span class="sxs-lookup"><span data-stu-id="52eff-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="52eff-192">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="52eff-192">Click **Next**.</span></span>

![Шифрование столбцов…](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="52eff-194">Настройка главного ключа</span><span class="sxs-lookup"><span data-stu-id="52eff-194">Master Key Configuration</span></span>
<span data-ttu-id="52eff-195">Hello **Конфигурация главного ключа** страница является задаются копии базы данных и выберите hello поставщика хранилища ключей CMK hello CMK хранения.</span><span class="sxs-lookup"><span data-stu-id="52eff-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="52eff-196">В настоящее время Главным можно хранить в хранилище сертификатов Windows hello, хранилище ключей или аппаратный модуль безопасности (HSM).</span><span class="sxs-lookup"><span data-stu-id="52eff-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="52eff-197">В этом учебнике показано как toostore ключей в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="52eff-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="52eff-198">Выберите **Хранилище ключей Azure**.</span><span class="sxs-lookup"><span data-stu-id="52eff-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="52eff-199">Выберите нужное хранилище ключей hello hello раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="52eff-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="52eff-200">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="52eff-200">Click **Next**.</span></span>

![Настройка главного ключа](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="52eff-202">Проверка</span><span class="sxs-lookup"><span data-stu-id="52eff-202">Validation</span></span>
<span data-ttu-id="52eff-203">Могут быть зашифрованы hello столбцы сейчас или сохранить сценарий PowerShell toorun позже.</span><span class="sxs-lookup"><span data-stu-id="52eff-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="52eff-204">В этом учебнике выберите **теперь продолжить toofinish** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="52eff-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="52eff-205">Сводка</span><span class="sxs-lookup"><span data-stu-id="52eff-205">Summary</span></span>
<span data-ttu-id="52eff-206">Убедитесь, что hello параметры заданы правильно и нажмите кнопку **Готово** toocomplete hello установки для постоянного шифрования.</span><span class="sxs-lookup"><span data-stu-id="52eff-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Сводка](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="52eff-208">Проверка действий мастера hello</span><span class="sxs-lookup"><span data-stu-id="52eff-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="52eff-209">После завершения работы мастера hello базы данных настроена для постоянного шифрования.</span><span class="sxs-lookup"><span data-stu-id="52eff-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="52eff-210">выполнить мастер hello Hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="52eff-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="52eff-211">Создал главный ключ столбца и сохранил его в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="52eff-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="52eff-212">Создал ключ шифрования столбца и сохранил его в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="52eff-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="52eff-213">Настроенный hello выбранные столбцы для шифрования.</span><span class="sxs-lookup"><span data-stu-id="52eff-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="52eff-214">Таблица сведений о пациентах Hello в настоящее время не содержит данных, но все существующие данные в столбцах выбран hello теперь зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="52eff-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="52eff-215">Можно проверить hello Создание ключей hello в SSMS, развернув **Clinic** > **безопасности** > **ключей постоянного шифрования**.</span><span class="sxs-lookup"><span data-stu-id="52eff-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="52eff-216">Создание клиентского приложения, которое работает с данными зашифрован hello</span><span class="sxs-lookup"><span data-stu-id="52eff-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="52eff-217">Теперь, когда Настройка постоянного шифрования можно построить приложение, выполняющее *вставляет* и *выбирает* на hello зашифрованные столбцы.</span><span class="sxs-lookup"><span data-stu-id="52eff-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="52eff-218">Приложение должно использовать [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) объектов при передаче сервер toohello данных открытого текста с всегда зашифрованным столбцам.</span><span class="sxs-lookup"><span data-stu-id="52eff-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="52eff-219">Передача значений литералов без использования объектов SqlParameter приведет к возникновению исключения.</span><span class="sxs-lookup"><span data-stu-id="52eff-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="52eff-220">Откройте Visual Studio и создайте **консольное приложение** C# (Visual Studio 2015 и более ранней версии) или **консольное приложение (.NET Framework)** (Visual Studio 2017 и более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="52eff-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="52eff-221">Убедитесь, что проект настроен слишком**.NET Framework 4.6** или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="52eff-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="52eff-222">Имя проекта hello **AlwaysEncryptedConsoleAKVApp** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="52eff-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="52eff-223">Установить следующие пакеты NuGet, перейдя слишком hello**средства** > **диспетчера пакетов NuGet** > **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="52eff-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="52eff-224">Запустите эти две строки кода в hello консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="52eff-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="52eff-225">Изменение вашей tooenable строку соединения, постоянное шифрование</span><span class="sxs-lookup"><span data-stu-id="52eff-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="52eff-226">В этом разделе объясняется, как tooenable всегда зашифрованы в строке подключения базы данных.</span><span class="sxs-lookup"><span data-stu-id="52eff-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="52eff-227">tooenable постоянного шифрования, необходимо tooadd hello **параметр шифрования столбца** tooyour соединения ключевое слово строки и задать для него слишком**включено**.</span><span class="sxs-lookup"><span data-stu-id="52eff-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="52eff-228">Это можно задать непосредственно в строке подключения hello или его можно задать с помощью [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="52eff-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="52eff-229">Пример приложения Hello в hello следующем разделе показано как toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="52eff-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="52eff-230">Включить постоянное шифрование в строке подключения hello</span><span class="sxs-lookup"><span data-stu-id="52eff-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="52eff-231">Добавьте следующие строки подключения tooyour ключевое слово hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="52eff-232">Включение функции Always Encrypted с помощью SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="52eff-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="52eff-233">Здравствуйте, как следующий код показывает tooenable постоянное шифрование, задав [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) слишком[включено](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="52eff-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="52eff-234">Регистрация поставщика хранилища ключей Azure hello</span><span class="sxs-lookup"><span data-stu-id="52eff-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="52eff-235">Hello следующий код показывает, как tooregister hello поставщика хранилища ключей Azure с драйвером ADO.NET hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="52eff-236">Пример консольного приложения с функцией постоянного шифрования</span><span class="sxs-lookup"><span data-stu-id="52eff-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="52eff-237">В этом примере показано, как:</span><span class="sxs-lookup"><span data-stu-id="52eff-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="52eff-238">Измените ваш tooenable строку соединения, постоянное шифрование.</span><span class="sxs-lookup"><span data-stu-id="52eff-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="52eff-239">Зарегистрируйте хранилище ключей Azure, так как поставщик хранилища ключей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="52eff-240">Вставка данных в hello зашифрованные столбцы.</span><span class="sxs-lookup"><span data-stu-id="52eff-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="52eff-241">Выбрать запись, выполнив фильтрацию по конкретному значению в зашифрованном столбце.</span><span class="sxs-lookup"><span data-stu-id="52eff-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="52eff-242">Замените содержимое hello **Program.cs** с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="52eff-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="52eff-243">Замените hello строка подключения для hello connectionString глобальной переменной в строку hello, непосредственно предшествующий hello метод Main с вашей допустимую строку соединения из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="52eff-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="52eff-244">Это единственное изменение hello требуется toomake toothis код.</span><span class="sxs-lookup"><span data-stu-id="52eff-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="52eff-245">Запустите toosee приложения hello постоянного шифрования в действии.</span><span class="sxs-lookup"><span data-stu-id="52eff-245">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
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



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="52eff-246">Убедитесь, что hello шифрование</span><span class="sxs-lookup"><span data-stu-id="52eff-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="52eff-247">Вы можете быстро проверить hello фактические данные на сервере hello зашифрован запрос hello пациентов данных с помощью среды SSMS (с использованием текущего подключения где **параметр шифрования столбца** еще не включен).</span><span class="sxs-lookup"><span data-stu-id="52eff-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="52eff-248">Запустите приветствия при следующем запросе в базе данных Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="52eff-249">Вы увидите, что hello зашифрованные столбцы не содержат все зашифрованные данные.</span><span class="sxs-lookup"><span data-stu-id="52eff-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Новое консольное приложение](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="52eff-251">toouse SSMS tooaccess Здравствуйте зашифрованные данные, можно добавить hello *параметр шифрования столбца = включен* параметр toohello соединения.</span><span class="sxs-lookup"><span data-stu-id="52eff-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="52eff-252">В **обозревателе объектов** SSMS щелкните сервер правой кнопкой мыши и выберите пункт **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="52eff-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="52eff-253">Нажмите кнопку **Connect** > **компонент Database Engine** tooopen hello **подключения tooServer** и щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="52eff-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="52eff-254">Щелкните **Дополнительные параметры соединения** и введите **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="52eff-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Новое консольное приложение](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="52eff-256">Запустите приветствия при следующем запросе в базе данных Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="52eff-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="52eff-257">Теперь можно увидеть hello зашифрованные данные в столбцах hello зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="52eff-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Новое консольное приложение](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="52eff-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="52eff-259">Next steps</span></span>
<span data-ttu-id="52eff-260">После создания базы данных, которая использует постоянное шифрование, вы можете toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="52eff-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="52eff-261">[Сменить и очистить ключи](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="52eff-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="52eff-262">[Перенести данные, которые уже зашифрованы с использованием функции Always Encrypted.](https://msdn.microsoft.com/library/mt621539.aspx)</span><span class="sxs-lookup"><span data-stu-id="52eff-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="52eff-263">Связанные сведения</span><span class="sxs-lookup"><span data-stu-id="52eff-263">Related information</span></span>
* [<span data-ttu-id="52eff-264">Always Encrypted (разработка клиентских приложений)</span><span class="sxs-lookup"><span data-stu-id="52eff-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="52eff-265">Прозрачное шифрование данных</span><span class="sxs-lookup"><span data-stu-id="52eff-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="52eff-266">Шифрование SQL Server</span><span class="sxs-lookup"><span data-stu-id="52eff-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="52eff-267">Мастер настройки Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="52eff-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="52eff-268">Блог о функции Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="52eff-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

