---
title: "Пошаговое руководство по использованию универсального соединителя SQL | Документация Майкрософт"
description: "В этом документе содержится пошаговое руководство по работе с простой системой отдела кадров с использованием универсального соединителя SQL."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="da892-103">Универсальный соединитель SQL: пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="da892-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="da892-104">Эта статья является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="da892-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="da892-105">Она поможет вам создать простую базу данных для отдела кадров, которая предназначена для импорта некоторых пользователей и их членства в группе.</span><span class="sxs-lookup"><span data-stu-id="da892-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="da892-106">Подготовка образца базы данных</span><span class="sxs-lookup"><span data-stu-id="da892-106">Prepare the sample database</span></span>
<span data-ttu-id="da892-107">На сервере под управлением SQL Server запустите сценарий SQL, который находится в [Приложении A](#appendix-a). Этот сценарий создает пример базы данных с именем GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="da892-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="da892-108">Объектная модель для созданной базы данных выглядит так: </span><span class="sxs-lookup"><span data-stu-id="da892-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="da892-109">![Объектная модель](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="da892-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="da892-110">Также создайте пользователя, который будет использоваться для подключения к базе данных.</span><span class="sxs-lookup"><span data-stu-id="da892-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="da892-111">В этом пошаговом руководстве пользователю присвоено имя FABRIKAM\SQLUser, и он находится в домене.</span><span class="sxs-lookup"><span data-stu-id="da892-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="da892-112">Создание файла подключения ODBC</span><span class="sxs-lookup"><span data-stu-id="da892-112">Create the ODBC connection file</span></span>
<span data-ttu-id="da892-113">Универсальный соединитель SQL использует ODBC для подключения к удаленному серверу.</span><span class="sxs-lookup"><span data-stu-id="da892-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="da892-114">Сначала необходимо создать файл с данными подключения ODBC.</span><span class="sxs-lookup"><span data-stu-id="da892-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="da892-115">Запустите программу управления ODBC на сервере: </span><span class="sxs-lookup"><span data-stu-id="da892-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="da892-117">Откройте вкладку **File DSN**(Файловый DSN).</span><span class="sxs-lookup"><span data-stu-id="da892-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="da892-118">Щелкните **Add...**(Добавить).</span><span class="sxs-lookup"><span data-stu-id="da892-118">Click **Add...**.</span></span>  
   <span data-ttu-id="da892-119">![ODBC 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="da892-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="da892-120">Стандартный драйвер работает нормально, поэтому выберите его и нажмите кнопку **Next>** (Далее>).</span><span class="sxs-lookup"><span data-stu-id="da892-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="da892-121">![ODBC 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="da892-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="da892-122">Укажите имя файла, например **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="da892-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="da892-123">![ODBC 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="da892-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="da892-124">Нажмите кнопку **Finish**(Готово).</span><span class="sxs-lookup"><span data-stu-id="da892-124">Click **Finish**.</span></span>  
   <span data-ttu-id="da892-125">![ODBC 4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="da892-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="da892-126">Теперь нужно настроить подключение.</span><span class="sxs-lookup"><span data-stu-id="da892-126">Time to configure the connection.</span></span> <span data-ttu-id="da892-127">Введите понятное описание источника данных и укажите имя сервера, на котором выполняется SQL Server.</span><span class="sxs-lookup"><span data-stu-id="da892-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC 5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="da892-129">Выберите способ проверки подлинности с помощью SQL.</span><span class="sxs-lookup"><span data-stu-id="da892-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="da892-130">В нашем примере используется проверка подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="da892-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC 6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="da892-132">Укажите имя образца базы данных — **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="da892-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="da892-133">![ODBC 7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="da892-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="da892-134">На этом экране оставьте настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="da892-134">Keep everything default on this screen.</span></span> <span data-ttu-id="da892-135">Нажмите кнопку **Finish**(Готово).</span><span class="sxs-lookup"><span data-stu-id="da892-135">Click **Finish**.</span></span>  
   <span data-ttu-id="da892-136">![ODBC 8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="da892-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="da892-137">Чтобы проверить, все ли работает правильно, нажмите кнопку **Test Data Source**(Проверить источник данных).</span><span class="sxs-lookup"><span data-stu-id="da892-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="da892-138">![ODBC 9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="da892-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="da892-139">Убедитесь, что проверка прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="da892-139">Make sure the test is successful.</span></span>  
    ![ODBC 10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="da892-141">Файл конфигурации ODBC должен появиться на вкладке "File DSN" (Файловый DSN).</span><span class="sxs-lookup"><span data-stu-id="da892-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC 11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="da892-143">Теперь у нас есть нужный файл, и можно приступить к созданию соединителя.</span><span class="sxs-lookup"><span data-stu-id="da892-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="da892-144">Создание универсального соединителя SQL</span><span class="sxs-lookup"><span data-stu-id="da892-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="da892-145">В пользовательском интерфейсе Synchronization Service Manager выберите **Connectors** (Соединители) и нажмите кнопку **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="da892-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="da892-146">Выберите **Generic SQL (Microsoft)** (Универсальный SQL (Майкрософт)) и присвойте описательное имя.</span><span class="sxs-lookup"><span data-stu-id="da892-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="da892-147">![Соединитель 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="da892-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="da892-148">Найдите файл DSN, созданный в предыдущем разделе, и отправьте его на сервер.</span><span class="sxs-lookup"><span data-stu-id="da892-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="da892-149">Укажите учетные данные для подключения к базе данных.</span><span class="sxs-lookup"><span data-stu-id="da892-149">Provide the credentials to connect to the database.</span></span>  
   ![Соединитель 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="da892-151">В этом пошаговом руководстве мы упростим процесс и предположим, что существует два типа объектов: **User** и **Group**.</span><span class="sxs-lookup"><span data-stu-id="da892-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="da892-152">![Соединитель 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="da892-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="da892-153">При поиске атрибутов нам нужно, чтобы соединитель обнаружил их при просмотре таблицы.</span><span class="sxs-lookup"><span data-stu-id="da892-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="da892-154">Так как объект **Users** является зарезервированным словом в SQL, его необходимо заключить в квадратные скобки [].</span><span class="sxs-lookup"><span data-stu-id="da892-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="da892-155">![Соединитель 4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="da892-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="da892-156">Теперь нужно определить атрибут привязки и атрибут различаемого имени.</span><span class="sxs-lookup"><span data-stu-id="da892-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="da892-157">Для **Users**мы используем сочетание двух атрибутов — username и EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="da892-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="da892-158">Для **Group**мы используем GroupName (не слишком реалистично для обычной жизни, но подойдет для этого руководства).</span><span class="sxs-lookup"><span data-stu-id="da892-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="da892-159">![Соединитель 5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="da892-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="da892-160">В базе данных SQL могут быть обнаружены только некоторые типы атрибутов.</span><span class="sxs-lookup"><span data-stu-id="da892-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="da892-161">В частности, нельзя обнаружить тип ссылочного атрибута.</span><span class="sxs-lookup"><span data-stu-id="da892-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="da892-162">Для типа объекта Group необходимо изменить значения OwnerID и MemberID на ссылку.</span><span class="sxs-lookup"><span data-stu-id="da892-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Соединитель 6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="da892-164">Для атрибутов, выбранных как ссылочные атрибуты на предыдущем этапе, теперь требуется тип объекта, ссылкой на который они являются.</span><span class="sxs-lookup"><span data-stu-id="da892-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="da892-165">В нашем случае это тип объекта User.</span><span class="sxs-lookup"><span data-stu-id="da892-165">In our case, the User object type.</span></span>  
   ![Соединитель 7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="da892-167">На странице "Глобальные параметры" выберите **Watermark** (Водяной знак) в качестве стратегии изменений.</span><span class="sxs-lookup"><span data-stu-id="da892-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="da892-168">В поле формата даты и времени введите **гггг-ММ-дд ЧЧ:мм:сс**.</span><span class="sxs-lookup"><span data-stu-id="da892-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="da892-169">![Соединитель 8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="da892-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="da892-170">На странице **Configure Partitions and Hierarchies** (Настройка секций и иерархий) выберите оба типа объектов.</span><span class="sxs-lookup"><span data-stu-id="da892-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="da892-171">![Соединитель 9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="da892-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="da892-172">На странице **Выбор типов объектов** и **Выбор атрибутов** выберите оба типа объектов и все атрибуты.</span><span class="sxs-lookup"><span data-stu-id="da892-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="da892-173">На странице **Configure Anchors** (Настройка привязки) нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="da892-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="da892-174">Создание профилей выполнения</span><span class="sxs-lookup"><span data-stu-id="da892-174">Create Run Profiles</span></span>
1. <span data-ttu-id="da892-175">В пользовательском интерфейсе Synchronization Service Manager выберите **Connectors** (Соединители) и щелкните **Configure Run Profiles** (Настроить профили выполнения).</span><span class="sxs-lookup"><span data-stu-id="da892-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="da892-176">Щелкните **New Profile**(Новый профиль).</span><span class="sxs-lookup"><span data-stu-id="da892-176">Click **New Profile**.</span></span> <span data-ttu-id="da892-177">Мы начнем с профиля **Full Import**(Полный импорт).</span><span class="sxs-lookup"><span data-stu-id="da892-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="da892-178">![Профиль выполнения 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="da892-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="da892-179">Выберите тип **Full Import (Stage Only)**(Полный импорт (только демонстрация)).</span><span class="sxs-lookup"><span data-stu-id="da892-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="da892-180">![Профиль выполнения 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="da892-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="da892-181">Выберите раздел **OBJECT=User**.</span><span class="sxs-lookup"><span data-stu-id="da892-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="da892-182">![Профиль выполнения 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="da892-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="da892-183">Выберите **Table** и введите **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="da892-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="da892-184">Прокрутите вниз до раздела многозначного типа объекта и введите данные, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="da892-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="da892-185">Нажмите кнопку **Finish** (Готово), чтобы сохранить данные на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="da892-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="da892-186">![Профиль выполнения 4а](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="da892-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="da892-187">![Профиль выполнения 4б](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="da892-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="da892-188">Выберите **New Step**(Новый шаг).</span><span class="sxs-lookup"><span data-stu-id="da892-188">Select **New Step**.</span></span> <span data-ttu-id="da892-189">На этот раз выберите **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="da892-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="da892-190">На последней странице используйте конфигурацию, изображенную на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="da892-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="da892-191">Нажмите кнопку **Finish**(Готово).</span><span class="sxs-lookup"><span data-stu-id="da892-191">Click **Finish**.</span></span>  
   <span data-ttu-id="da892-192">![Профиль выполнения 5а](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="da892-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="da892-193">![Профиль выполнения 5б](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="da892-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="da892-194">Можно настроить дополнительные профили выполнения, но это необязательно.</span><span class="sxs-lookup"><span data-stu-id="da892-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="da892-195">В этом пошаговом руководстве используется только профиль "Full Import" (Полный импорт).</span><span class="sxs-lookup"><span data-stu-id="da892-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="da892-196">Нажмите кнопку **ОК** , чтобы завершить изменение профилей выполнения.</span><span class="sxs-lookup"><span data-stu-id="da892-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="da892-197">Добавление некоторых тестовых данных и тестирование импорта</span><span class="sxs-lookup"><span data-stu-id="da892-197">Add some test data and test the import</span></span>
<span data-ttu-id="da892-198">Введите тестовые данные в образец базы данных.</span><span class="sxs-lookup"><span data-stu-id="da892-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="da892-199">Когда будете готовы, щелкните **Run** (Выполнить) и **Full import** (Полный импорт).</span><span class="sxs-lookup"><span data-stu-id="da892-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="da892-200">Здесь мы видим пользователя с двумя телефонными номерами и группу с несколькими участниками.</span><span class="sxs-lookup"><span data-stu-id="da892-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![Пространство соединителя 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![Пространство соединителя 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="da892-203">Приложении A</span><span class="sxs-lookup"><span data-stu-id="da892-203">Appendix A</span></span>
<span data-ttu-id="da892-204">**Сценарий SQL для создания образца базы данных**</span><span class="sxs-lookup"><span data-stu-id="da892-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
