---
title: "aaaManage персональные данные в Microsoft Azure | Документы Microsoft"
description: "рекомендации по как toocorrect, обновление, удаление и Экспорт личных данных в Azure Active Directory и база данных SQL Azure"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="80cda-103">Управление персональными данными в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="80cda-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="80cda-104">Эта статья содержит инструкции о том, как toocorrect, обновление, удаление и Экспорт личных данных в Azure Active Directory и база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="80cda-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="80cda-105">Сценарий</span><span class="sxs-lookup"><span data-stu-id="80cda-105">Scenario</span></span>

<span data-ttu-id="80cda-106">Компании, на основе Dublin предоставляет комплексное для высокопроизводительной назначения свадьбы Ирландии и вокруг hello world для локальных и международных клиента базы.</span><span class="sxs-lookup"><span data-stu-id="80cda-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="80cda-107">Они имеют офисов, клиенты, сотрудников и поставщиков, которые расположены по всему hello world toofully службы hello местоположения они предоставляют.</span><span class="sxs-lookup"><span data-stu-id="80cda-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="80cda-108">Среди множества других товаров hello компания хранит информацию о ответов на приглашение, включающие аллергией пищевых продуктов и предпочтения по запросу.</span><span class="sxs-lookup"><span data-stu-id="80cda-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="80cda-109">Гости свадьбу можно зарегистрировать для выполнения различных действий, таких как boat страниц, horseback «riding», и, в т. д. и даже взаимодействовать друг с другом на центральном веб-странице месяцы hello привели toohello событий.</span><span class="sxs-lookup"><span data-stu-id="80cda-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="80cda-110">Компания Hello собирает личные данные из сотрудников, поставщиков, клиентов и Гости свадьбу.</span><span class="sxs-lookup"><span data-stu-id="80cda-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="80cda-111">Из-за hello международного характер hello бизнеса hello компании должны соответствовать несколько уровней регулирование.</span><span class="sxs-lookup"><span data-stu-id="80cda-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="80cda-112">Проблема</span><span class="sxs-lookup"><span data-stu-id="80cda-112">Problem statement</span></span>

- <span data-ttu-id="80cda-113">Администраторы данных должны быть может toocorrect неточной личных сведений и неполные или изменяющиеся персональные данные.</span><span class="sxs-lookup"><span data-stu-id="80cda-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="80cda-114">Необходимого Администраторы данных должны быть личные данные могут toodelete по запросу hello данных субъекта.</span><span class="sxs-lookup"><span data-stu-id="80cda-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="80cda-115">Администраторы данных требуется tooexport данных и предоставить ему tooa данных субъекта в формате общего, структурированная по запросу или ее.</span><span class="sxs-lookup"><span data-stu-id="80cda-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="80cda-116">Цели компании</span><span class="sxs-lookup"><span data-stu-id="80cda-116">Company goals</span></span>

- <span data-ttu-id="80cda-117">Компания должна реализовать возможность исправлять или обновлять неточные или неполные персональные данные клиентов, гостей свадьбы, сотрудников и поставщиков в Azure Active Directory и базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="80cda-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="80cda-118">Персональные данные должны быть удалены по запросу hello данных субъекта в Azure Active Directory и база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="80cda-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="80cda-119">Персональные данные необходимо экспортировать в формате общего, структурированная по запросу hello данных субъекта.</span><span class="sxs-lookup"><span data-stu-id="80cda-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="80cda-120">Решения</span><span class="sxs-lookup"><span data-stu-id="80cda-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="80cda-121">Изменение неверных или неполных персональных данных и удаление персональных данных и профилей пользователей в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80cda-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="80cda-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) — это мультитенантный облачный каталог и служба управления удостоверениями Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="80cda-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="80cda-123">Исправления, обновления или удаления клиентов и профилей пользователей и информация о работы пользователя, содержат личные данные, такие как имя пользователя, должность, адрес или номер телефона в вашей [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) среды с помощью hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="80cda-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="80cda-124">Необходимо войти с учетной записью глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="80cda-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="80cda-125">Исправление или обновление профиля пользователя и сведений о работе в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80cda-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="80cda-126">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="80cda-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="80cda-127">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="80cda-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="80cda-129">На hello **пользователей и групп** колонке выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="80cda-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="80cda-131">На hello **пользователей и групп - Пользователи** колонке выберите пользователя из списка hello и выберите в колонке hello для выбранного пользователя hello, **профиль** tooview hello сведений профиля, необходимо исправить toobe или обновленный.</span><span class="sxs-lookup"><span data-stu-id="80cda-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="80cda-133">Исправьте или обновить сведения о hello и выберите на панели команд hello, **сохранить.**</span><span class="sxs-lookup"><span data-stu-id="80cda-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="80cda-134">В колонке hello для выбранного пользователя hello, выберите **сведения о работе** tooview пользователя рабочие данные, необходимые toobe Исправлено или обновлен.</span><span class="sxs-lookup"><span data-stu-id="80cda-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="80cda-136">Исправьте или обновить сведения о рабочих пользователя hello и выберите на панели команд hello, **сохранить.**</span><span class="sxs-lookup"><span data-stu-id="80cda-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="80cda-137">Удаление профиля пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80cda-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="80cda-138">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="80cda-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="80cda-139">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="80cda-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="80cda-140">На hello **пользователей и групп** колонке выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="80cda-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="80cda-142">На hello **пользователей и групп — пользователей** колонке выберите пользователя из списка hello.</span><span class="sxs-lookup"><span data-stu-id="80cda-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="80cda-144">В колонке hello для выбранного пользователя hello, выберите **Обзор**и выберите в панели команд hello, **удалить**.</span><span class="sxs-lookup"><span data-stu-id="80cda-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="80cda-145">Удаление, экспорт и изменение неверных или неполных персональных данных в базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="80cda-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="80cda-146">[База данных SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) — это облачная база данных, позволяющая разработчикам создавать приложения и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="80cda-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="80cda-147">Персональные данные в [базе данных SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) можно обновить с помощью стандартных запросов SQL, а также удалить.</span><span class="sxs-lookup"><span data-stu-id="80cda-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="80cda-148">Кроме того персональные данные можно экспортировать из базы данных SQL с помощью различных методов, включая hello импорта Azure SQL Server и мастер экспорта и в различных форматах, включая файл BACPAC.</span><span class="sxs-lookup"><span data-stu-id="80cda-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="80cda-149">Исправление, обновление и удаление персональных данных в базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="80cda-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="80cda-150">toolearn как toocorrect или обновление персональные данные в базе данных SQL, посетите hello [обновления (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [обновить текст](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [обновление обобщенного табличного выражения with](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), или [ Обновление записи текста](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) документации.</span><span class="sxs-lookup"><span data-stu-id="80cda-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="80cda-151">toolearn как toodelete персональные данные в базе данных SQL, посетите hello [удалить (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) документации.</span><span class="sxs-lookup"><span data-stu-id="80cda-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="80cda-152">Экспорт файла BACPAC tooa персональные данные в базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="80cda-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="80cda-153">BACPAC-файл включает hello SQL базы данных и метаданных и ZIP-файл с расширением BACPAC.</span><span class="sxs-lookup"><span data-stu-id="80cda-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="80cda-154">Это можно сделать с помощью hello [портал Azure](https://portal.azure.com/), hello SQLPackage программы командной строки, SQL Server Management Studio (SSMS) или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80cda-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="80cda-155">toolearn как tooexport данных tooa BACPAC-файл, посетите hello [Экспорт файла BACPAC tooa базы данных Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-export) страницу, содержащую подробные инструкции для каждого из перечисленных выше методов.</span><span class="sxs-lookup"><span data-stu-id="80cda-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="80cda-156">Экспорт персональные данные из базы данных SQL с SQL Server Import hello и мастер экспорта</span><span class="sxs-lookup"><span data-stu-id="80cda-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="80cda-157">Этот мастер помогает скопировать данные из источника tooa назначения.</span><span class="sxs-lookup"><span data-stu-id="80cda-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="80cda-158">Общие сведения мастера toohello, включая как tooget ее, сведения о разрешениях и помощь tooget с помощью средства hello посетите hello [и экспорт данных с SQL Server Import hello мастер импорта и экспорта](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="80cda-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="80cda-159">Общие сведения о стадии приветствия мастера посетите hello [шагов в hello импорта SQL Server и мастер экспорта](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="80cda-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80cda-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80cda-160">Next Steps:</span></span>

[<span data-ttu-id="80cda-161">База данных SQL Azure;</span><span class="sxs-lookup"><span data-stu-id="80cda-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="80cda-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80cda-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

