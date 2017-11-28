---
title: "aaaAuthentication tooAzure хранилище данных SQL | Документы Microsoft"
description: "Azure Active Directory (AAD) и SQL Server authentication tooAzure хранилище данных SQL."
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="ba633-103">Проверка подлинности tooAzure хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="ba633-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba633-104">Обзор безопасности</span><span class="sxs-lookup"><span data-stu-id="ba633-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="ba633-105">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="ba633-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="ba633-106">Шифрование (портал)</span><span class="sxs-lookup"><span data-stu-id="ba633-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="ba633-107">Шифрование (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="ba633-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="ba633-108">tooSQL tooconnect хранилища данных, необходимо передать в учетных данных безопасности для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ba633-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="ba633-109">После установки подключения некоторые его параметры настраиваются при установке сеанса запроса.</span><span class="sxs-lookup"><span data-stu-id="ba633-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="ba633-110">Дополнительные сведения о безопасности и как хранилище данных tooyour tooenable соединения, в разделе [защиты базы данных в хранилище данных SQL][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="ba633-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="ba633-111">Аутентификация SQL</span><span class="sxs-lookup"><span data-stu-id="ba633-111">SQL authentication</span></span>
<span data-ttu-id="ba633-112">tooSQL tooconnect хранилища данных, необходимо предоставить hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ba633-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="ba633-113">Полное имя сервера</span><span class="sxs-lookup"><span data-stu-id="ba633-113">Fully qualified servername</span></span>
* <span data-ttu-id="ba633-114">Тип проверки подлинности SQL</span><span class="sxs-lookup"><span data-stu-id="ba633-114">Specify SQL authentication</span></span>
* <span data-ttu-id="ba633-115">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="ba633-115">Username</span></span>
* <span data-ttu-id="ba633-116">Пароль</span><span class="sxs-lookup"><span data-stu-id="ba633-116">Password</span></span>
* <span data-ttu-id="ba633-117">База данных по умолчанию (необязательно)</span><span class="sxs-lookup"><span data-stu-id="ba633-117">Default database (optional)</span></span>

<span data-ttu-id="ba633-118">По умолчанию соединения toohello *master* базы данных и не пользовательскую базу данных.</span><span class="sxs-lookup"><span data-stu-id="ba633-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="ba633-119">tooconnect tooyour пользовательской базы данных, вы можете toodo одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="ba633-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="ba633-120">Укажите базу данных по умолчанию hello, при регистрации сервера в обозревателе объектов SQL Server в SSDT и SSMS, или в строке подключения приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ba633-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="ba633-121">Например включать параметр InitialCatalog hello для подключения ODBC.</span><span class="sxs-lookup"><span data-stu-id="ba633-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="ba633-122">Выделите hello пользовательской базы данных перед созданием сеанса в SSDT.</span><span class="sxs-lookup"><span data-stu-id="ba633-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="ba633-123">Здравствуйте, инструкции Transact-SQL **используйте MyDatabase;** не поддерживается для изменения hello базы данных для подключения.</span><span class="sxs-lookup"><span data-stu-id="ba633-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="ba633-124">Рекомендации при подключении tooSQL хранилища данных с помощью SSDT, см. в разделе toohello [запроса с помощью Visual Studio] [ Query with Visual Studio] статьи.</span><span class="sxs-lookup"><span data-stu-id="ba633-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="ba633-125">Аутентификация Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="ba633-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="ba633-126">[Azure Active Directory] [ What is Azure Active Directory] проверка подлинности — это механизм подключения tooMicrosoft хранилище данных SQL Azure с помощью удостоверений в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba633-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ba633-127">С помощью проверки подлинности Azure Active Directory можно централизованно управлять hello удостоверений пользователей базы данных и другие службы Майкрософт, в одном централизованном месте.</span><span class="sxs-lookup"><span data-stu-id="ba633-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="ba633-128">Централизованное управление идентификатор представляет собой единое место пользователей toomanage хранилище данных SQL и упрощает управление разрешениями.</span><span class="sxs-lookup"><span data-stu-id="ba633-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="ba633-129">Преимущества</span><span class="sxs-lookup"><span data-stu-id="ba633-129">Benefits</span></span>
<span data-ttu-id="ba633-130">Преимущества Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="ba633-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="ba633-131">Предоставляет альтернативные tooSQL проверки подлинности сервера.</span><span class="sxs-lookup"><span data-stu-id="ba633-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="ba633-132">Позволяет остановить hello увеличением числа пользователей на серверах базы данных.</span><span class="sxs-lookup"><span data-stu-id="ba633-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="ba633-133">изменение паролей в одном расположении;</span><span class="sxs-lookup"><span data-stu-id="ba633-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="ba633-134">управление разрешениями базы данных с помощью внешних групп (AAD);</span><span class="sxs-lookup"><span data-stu-id="ba633-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="ba633-135">возможность исключить хранение паролей с помощью встроенной проверки подлинности Windows и других видов аутентификации, поддерживаемых Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="ba633-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="ba633-136">Использует содержатся идентификаторы tooauthenticate пользователей базы данных на уровне базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="ba633-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="ba633-137">Поддерживает проверку подлинности на основе токена для приложений, соединяющихся tooSQL хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="ba633-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="ba633-138">поддержка Многофакторной Идентификации с помощью универсальной аутентификации Active Directory для SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="ba633-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="ba633-139">Описание Multi-Factor Authentication см. в статье [Поддержка SSMS в Azure AD MFA для базы данных SQL и хранилища данных SQL](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ba633-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ba633-140">Azure Active Directory является сравнительно новым компонентом и имеет некоторые ограничения.</span><span class="sxs-lookup"><span data-stu-id="ba633-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="ba633-141">tooensure, что Azure Active Directory, подходит для вашей среды. в разделе [функции Azure AD и ограничения][Azure AD features and limitations], в частности hello Дополнительные соображения.</span><span class="sxs-lookup"><span data-stu-id="ba633-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="ba633-142">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="ba633-142">Configuration steps</span></span>
<span data-ttu-id="ba633-143">Выполните эти шаги tooconfigure Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="ba633-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="ba633-144">Создание и заполнение каталога Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba633-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="ba633-145">Необязательно: Связать или изменение hello active directory, который сейчас связан с подпиской Azure</span><span class="sxs-lookup"><span data-stu-id="ba633-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="ba633-146">Создание администратора Azure Active Directory для хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ba633-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="ba633-147">Настройка клиентских компьютеров</span><span class="sxs-lookup"><span data-stu-id="ba633-147">Configure your client computers</span></span>
5. <span data-ttu-id="ba633-148">Создать пользователей автономной базы данных в вашей базы данных сопоставлен tooAzure удостоверений AD</span><span class="sxs-lookup"><span data-stu-id="ba633-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="ba633-149">Подключение tooyour хранилища данных с помощью удостоверений Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba633-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="ba633-150">Сейчас пользователи Azure Active Directory не отображаются в обозревателе объектов SSDT.</span><span class="sxs-lookup"><span data-stu-id="ba633-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="ba633-151">Чтобы избежать этого, просмотра сведений о пользователях hello в [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba633-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="ba633-152">Найти сведения о hello</span><span class="sxs-lookup"><span data-stu-id="ba633-152">Find hello details</span></span>
* <span data-ttu-id="ba633-153">Hello действия tooconfigure и использовать Azure Active Directory authentication практически идентичны для базы данных SQL Azure и хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ba633-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ba633-154">Выполните hello подробные инструкции в разделе hello [tooSQL подключение базы данных или SQL данные хранилища с использованием Azure Active Directory проверки подлинности](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ba633-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="ba633-155">Создание пользовательских ролей базы данных и Добавление ролей toohello пользователей.</span><span class="sxs-lookup"><span data-stu-id="ba633-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="ba633-156">Предоставьте роли toohello Гранулярные разрешения.</span><span class="sxs-lookup"><span data-stu-id="ba633-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="ba633-157">Дополнительные сведения см. в разделе [Приступая к работе с разрешениями Database Engine](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba633-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba633-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba633-158">Next steps</span></span>
<span data-ttu-id="ba633-159">toostart запросов хранилищ данных в Visual Studio и других приложений, в разделе [запроса с помощью Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="ba633-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
