---
title: "Аутентификация в хранилище данных SQL Azure | Документация Майкрософт"
description: "Применение аутентификации Azure Active Directory (AAD) и SQL Server для подключения к хранилищу данных SQL Azure."
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
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="3b83a-103">Аутентификация в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3b83a-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b83a-104">Обзор безопасности</span><span class="sxs-lookup"><span data-stu-id="3b83a-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="3b83a-105">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="3b83a-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="3b83a-106">Шифрование (портал)</span><span class="sxs-lookup"><span data-stu-id="3b83a-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="3b83a-107">Шифрование (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="3b83a-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="3b83a-108">Для подключения к хранилищу данных SQL необходимо передавать учетные данные безопасности для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="3b83a-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="3b83a-109">После установки подключения некоторые его параметры настраиваются при установке сеанса запроса.</span><span class="sxs-lookup"><span data-stu-id="3b83a-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="3b83a-110">Дополнительные сведения о безопасности и разрешении подключений к хранилищу данных см. в статье [Защита базы данных в хранилище данных SQL][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="3b83a-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="3b83a-111">Аутентификация SQL</span><span class="sxs-lookup"><span data-stu-id="3b83a-111">SQL authentication</span></span>
<span data-ttu-id="3b83a-112">Для подключения к хранилищу данных SQL необходимо предоставить следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="3b83a-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="3b83a-113">Полное имя сервера</span><span class="sxs-lookup"><span data-stu-id="3b83a-113">Fully qualified servername</span></span>
* <span data-ttu-id="3b83a-114">Тип проверки подлинности SQL</span><span class="sxs-lookup"><span data-stu-id="3b83a-114">Specify SQL authentication</span></span>
* <span data-ttu-id="3b83a-115">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="3b83a-115">Username</span></span>
* <span data-ttu-id="3b83a-116">Пароль</span><span class="sxs-lookup"><span data-stu-id="3b83a-116">Password</span></span>
* <span data-ttu-id="3b83a-117">База данных по умолчанию (необязательно)</span><span class="sxs-lookup"><span data-stu-id="3b83a-117">Default database (optional)</span></span>

<span data-ttu-id="3b83a-118">По умолчанию устанавливается подключение к базе данных *master* , а не к пользовательской базе данных.</span><span class="sxs-lookup"><span data-stu-id="3b83a-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="3b83a-119">Для подключения к пользовательской базе данных можно выполнить одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="3b83a-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="3b83a-120">Укажите базу данных по умолчанию при регистрации сервера в обозревателе объектов SQL Server в SSDT, SSMS или в строке подключения приложения.</span><span class="sxs-lookup"><span data-stu-id="3b83a-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="3b83a-121">Например, добавьте параметр InitialCatalog для подключения ODBC.</span><span class="sxs-lookup"><span data-stu-id="3b83a-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="3b83a-122">Выделите пользовательскую базу данных перед созданием сеанса в SSDT.</span><span class="sxs-lookup"><span data-stu-id="3b83a-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="3b83a-123">Использование инструкции Transact-SQL **USE MyDatabase;** для изменения базы данных, к которой осуществляется подключение, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3b83a-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="3b83a-124">Инструкции по подключению к хранилищу данных SQL с помощью Visual Studio и SSDT см. в [этой статье][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="3b83a-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="3b83a-125">Аутентификация Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="3b83a-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="3b83a-126">Проверка подлинности [Azure Active Directory][What is Azure Active Directory] — это механизм подключения к хранилищу данных SQL Microsoft Azure с помощью удостоверений в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3b83a-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3b83a-127">С помощью аутентификации Azure Active Directory можно централизованно управлять удостоверениями пользователей базы данных и другими службами Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3b83a-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="3b83a-128">Централизованное управление удостоверениями позволяет использовать единое расположение для управления пользователями хранилища данных SQL и упрощает управление разрешениями.</span><span class="sxs-lookup"><span data-stu-id="3b83a-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="3b83a-129">Преимущества</span><span class="sxs-lookup"><span data-stu-id="3b83a-129">Benefits</span></span>
<span data-ttu-id="3b83a-130">Преимущества Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="3b83a-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="3b83a-131">наличие альтернативы аутентификации SQL Server;</span><span class="sxs-lookup"><span data-stu-id="3b83a-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="3b83a-132">возможность остановить увеличение количества пользователей на серверах баз данных;</span><span class="sxs-lookup"><span data-stu-id="3b83a-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="3b83a-133">изменение паролей в одном расположении;</span><span class="sxs-lookup"><span data-stu-id="3b83a-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="3b83a-134">управление разрешениями базы данных с помощью внешних групп (AAD);</span><span class="sxs-lookup"><span data-stu-id="3b83a-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="3b83a-135">возможность исключить хранение паролей с помощью встроенной проверки подлинности Windows и других видов аутентификации, поддерживаемых Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="3b83a-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="3b83a-136">для проверки подлинности удостоверений на уровне базы данных используются данные пользователей автономной базы данных;</span><span class="sxs-lookup"><span data-stu-id="3b83a-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="3b83a-137">поддержка аутентификации на основе маркеров для приложений, подключающихся к хранилищу данных SQL;</span><span class="sxs-lookup"><span data-stu-id="3b83a-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="3b83a-138">поддержка Многофакторной Идентификации с помощью универсальной аутентификации Active Directory для SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="3b83a-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="3b83a-139">Описание Multi-Factor Authentication см. в статье [Поддержка SSMS в Azure AD MFA для базы данных SQL и хранилища данных SQL](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3b83a-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3b83a-140">Azure Active Directory является сравнительно новым компонентом и имеет некоторые ограничения.</span><span class="sxs-lookup"><span data-stu-id="3b83a-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="3b83a-141">Чтобы убедиться, что Azure Active Directory подходит для вашей среды, ознакомьтесь с разделом [Функции и ограничения Azure AD][Azure AD features and limitations], в частности с его подразделом "Дополнительные замечания".</span><span class="sxs-lookup"><span data-stu-id="3b83a-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="3b83a-142">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="3b83a-142">Configuration steps</span></span>
<span data-ttu-id="3b83a-143">Следуйте приведенным ниже инструкциям, чтобы настроить аутентификацию Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3b83a-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="3b83a-144">Создание и заполнение каталога Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b83a-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="3b83a-145">Связывание каталога Active Directory с подпиской Azure или изменение каталога, который сейчас связан с этой подпиской (этот шаг можно пропустить)</span><span class="sxs-lookup"><span data-stu-id="3b83a-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="3b83a-146">Создание администратора Azure Active Directory для хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3b83a-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="3b83a-147">Настройка клиентских компьютеров</span><span class="sxs-lookup"><span data-stu-id="3b83a-147">Configure your client computers</span></span>
5. <span data-ttu-id="3b83a-148">Создание пользователей автономной базы данных в базе данных, сопоставленной с удостоверениями Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b83a-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="3b83a-149">Подключение к хранилищу данных с помощью удостоверений Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b83a-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="3b83a-150">Сейчас пользователи Azure Active Directory не отображаются в обозревателе объектов SSDT.</span><span class="sxs-lookup"><span data-stu-id="3b83a-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="3b83a-151">Сведения о пользователях можно просмотреть в файле [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b83a-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="3b83a-152">Поиск подробных сведений</span><span class="sxs-lookup"><span data-stu-id="3b83a-152">Find the details</span></span>
* <span data-ttu-id="3b83a-153">Процедуры настройки и использования аутентификации Azure Active Directory практически идентичны для базы данных SQL Azure и хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3b83a-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="3b83a-154">Выполните действия, описанные в разделе [Подключение к Базе данных SQL или хранилищу данных SQL c использованием проверки подлинности Azure Active Directory](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3b83a-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="3b83a-155">Создайте пользовательские роли базы данных и назначьте их пользователям.</span><span class="sxs-lookup"><span data-stu-id="3b83a-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="3b83a-156">Затем предоставьте ролям управляемые разрешения.</span><span class="sxs-lookup"><span data-stu-id="3b83a-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="3b83a-157">Дополнительные сведения см. в разделе [Приступая к работе с разрешениями Database Engine](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b83a-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b83a-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b83a-158">Next steps</span></span>
<span data-ttu-id="3b83a-159">Чтобы приступить к отправке запросов к хранилищу данных с помощью Visual Studio и других приложений, см. статью [Подключение к хранилищу данных SQL с помощью Visual Studio и SSDT][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="3b83a-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
