---
title: "шаг aaaGeneric шаг по соединителя SQL | Документы Microsoft"
description: "В этой статье пошагового прохода через простую систему HR пошаговые с помощью hello универсальный соединитель SQL."
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
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="b698b-103">Универсальный соединитель SQL: пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="b698b-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="b698b-104">Эта статья является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="b698b-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="b698b-105">Она поможет вам создать простую базу данных для отдела кадров, которая предназначена для импорта некоторых пользователей и их членства в группе.</span><span class="sxs-lookup"><span data-stu-id="b698b-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="b698b-106">Подготовка базы данных образец hello</span><span class="sxs-lookup"><span data-stu-id="b698b-106">Prepare hello sample database</span></span>
<span data-ttu-id="b698b-107">На сервер SQL Server, выполните сценарий SQL hello в [приложение A](#appendix-a). Этот скрипт создает образец базы данных с именем hello GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="b698b-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="b698b-108">Hello объектная модель для hello создания базы данных выглядит на этом рисунке:</span><span class="sxs-lookup"><span data-stu-id="b698b-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="b698b-109">![Объектная модель](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="b698b-110">Также можно создайте пользователя базы данных toohello tooconnect toouse.</span><span class="sxs-lookup"><span data-stu-id="b698b-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="b698b-111">В этом пошаговом руководстве пользователя hello вызывается FABRIKAM\SQLUser и находиться в домене, hello.</span><span class="sxs-lookup"><span data-stu-id="b698b-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="b698b-112">Создание файла соединения ODBC hello</span><span class="sxs-lookup"><span data-stu-id="b698b-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="b698b-113">Hello универсальный соединитель SQL использует ODBC tooconnect toohello удаленного сервера.</span><span class="sxs-lookup"><span data-stu-id="b698b-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="b698b-114">Сначала нужно toocreate файл, содержащий сведения о соединении ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="b698b-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="b698b-115">Запуск программы управления hello ODBC на сервере:</span><span class="sxs-lookup"><span data-stu-id="b698b-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="b698b-117">Выберите hello вкладку **файловый DSN**.</span><span class="sxs-lookup"><span data-stu-id="b698b-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="b698b-118">Щелкните **Add...**(Добавить).</span><span class="sxs-lookup"><span data-stu-id="b698b-118">Click **Add...**.</span></span>  
   <span data-ttu-id="b698b-119">![ODBC 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="b698b-120">Hello работает драйвер out-of-box прекрасная, поэтому выберите его и щелкните **Далее >**.</span><span class="sxs-lookup"><span data-stu-id="b698b-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="b698b-121">![ODBC 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="b698b-122">Имя файла hello, таких как **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="b698b-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="b698b-123">![ODBC 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="b698b-124">Нажмите кнопку **Finish**(Готово).</span><span class="sxs-lookup"><span data-stu-id="b698b-124">Click **Finish**.</span></span>  
   <span data-ttu-id="b698b-125">![ODBC 4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="b698b-126">Соединения hello tooconfigure времени.</span><span class="sxs-lookup"><span data-stu-id="b698b-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="b698b-127">Укажите источник данных hello Хорошее описание и укажите имя hello hello сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b698b-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC 5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="b698b-129">Выбор метода tooauthenticate с SQL.</span><span class="sxs-lookup"><span data-stu-id="b698b-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="b698b-130">В нашем примере используется проверка подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="b698b-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC 6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="b698b-132">Укажите имя hello hello образца базы данных, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="b698b-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="b698b-133">![ODBC 7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="b698b-134">На этом экране оставьте настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b698b-134">Keep everything default on this screen.</span></span> <span data-ttu-id="b698b-135">Нажмите кнопку **Finish**(Готово).</span><span class="sxs-lookup"><span data-stu-id="b698b-135">Click **Finish**.</span></span>  
   <span data-ttu-id="b698b-136">![ODBC 8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="b698b-137">Щелкните tooverify все работает, как ожидалось, **тестового источника данных**.</span><span class="sxs-lookup"><span data-stu-id="b698b-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="b698b-138">![ODBC 9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="b698b-139">Убедитесь, что hello проверка прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="b698b-139">Make sure hello test is successful.</span></span>  
    ![ODBC 10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="b698b-141">файл конфигурации ODBC Hello, теперь должны быть видимыми в файловый DSN.</span><span class="sxs-lookup"><span data-stu-id="b698b-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC 11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="b698b-143">Теперь у нас есть файл hello нам нужна и можно приступить к созданию hello соединителя.</span><span class="sxs-lookup"><span data-stu-id="b698b-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="b698b-144">Создать hello универсальный соединитель SQL</span><span class="sxs-lookup"><span data-stu-id="b698b-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="b698b-145">В hello пользовательского интерфейса диспетчера службы синхронизации, выберите **соединители** и **создать**.</span><span class="sxs-lookup"><span data-stu-id="b698b-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="b698b-146">Выберите **Generic SQL (Microsoft)** (Универсальный SQL (Майкрософт)) и присвойте описательное имя.</span><span class="sxs-lookup"><span data-stu-id="b698b-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="b698b-147">![Соединитель 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="b698b-148">Найдите файл DSN hello, созданный в предыдущем разделе hello и выгрузить его toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="b698b-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="b698b-149">Укажите учетные данные tooconnect hello toohello-базы данных.</span><span class="sxs-lookup"><span data-stu-id="b698b-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Соединитель 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="b698b-151">В этом пошаговом руководстве мы упростим процесс и предположим, что существует два типа объектов: **User** и **Group**.</span><span class="sxs-lookup"><span data-stu-id="b698b-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="b698b-152">![Соединитель 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="b698b-153">атрибуты toofind hello, мы хотим hello соединитель toodetect те атрибуты, посмотрев на саму таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="b698b-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="b698b-154">Поскольку **пользователей** является зарезервированным словом в SQL, нам нужно tooprovide его в квадратные скобки [].</span><span class="sxs-lookup"><span data-stu-id="b698b-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="b698b-155">![Соединитель 4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="b698b-156">Время toodefine hello привязки атрибута и атрибута DN hello.</span><span class="sxs-lookup"><span data-stu-id="b698b-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="b698b-157">Для **пользователей**, мы используем hello сочетание имени пользователя hello двух атрибутов и EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="b698b-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="b698b-158">Для **Group**мы используем GroupName (не слишком реалистично для обычной жизни, но подойдет для этого руководства).</span><span class="sxs-lookup"><span data-stu-id="b698b-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="b698b-159">![Соединитель 5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="b698b-160">В базе данных SQL могут быть обнаружены только некоторые типы атрибутов.</span><span class="sxs-lookup"><span data-stu-id="b698b-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="b698b-161">в частности невозможно Hello ссылочного типа атрибута.</span><span class="sxs-lookup"><span data-stu-id="b698b-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="b698b-162">Тип объекта группы hello нам нужна toochange hello OwnerID и MemberID tooreference.</span><span class="sxs-lookup"><span data-stu-id="b698b-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Соединитель 6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="b698b-164">атрибуты Hello мы выбрали как атрибуты этих ссылок на предыдущем шаге hello требуются эти значения являются ссылку на объект типа hello.</span><span class="sxs-lookup"><span data-stu-id="b698b-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="b698b-165">В нашем случае hello тип объекта пользователя.</span><span class="sxs-lookup"><span data-stu-id="b698b-165">In our case, hello User object type.</span></span>  
   ![Соединитель 7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="b698b-167">На странице приветствия глобальные параметры, выберите **водяной знак** в рамках стратегии дельта hello.</span><span class="sxs-lookup"><span data-stu-id="b698b-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="b698b-168">Также вводить в формате даты и времени hello **гггг мм дд чч**.</span><span class="sxs-lookup"><span data-stu-id="b698b-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="b698b-169">![Соединитель 8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="b698b-170">На hello **Настройка разделов и иерархий** выберите оба типа объектов.</span><span class="sxs-lookup"><span data-stu-id="b698b-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="b698b-171">![Соединитель 9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="b698b-172">На hello **Выбор типов объектов** и **Выбор атрибутов**, выберите типы объектов и атрибуты.</span><span class="sxs-lookup"><span data-stu-id="b698b-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="b698b-173">На hello **Настройка привязки** щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b698b-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="b698b-174">Создание профилей выполнения</span><span class="sxs-lookup"><span data-stu-id="b698b-174">Create Run Profiles</span></span>
1. <span data-ttu-id="b698b-175">В hello пользовательского интерфейса диспетчера службы синхронизации, выберите **соединители**, и **Настройка профилей выполнения**.</span><span class="sxs-lookup"><span data-stu-id="b698b-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="b698b-176">Щелкните **New Profile**(Новый профиль).</span><span class="sxs-lookup"><span data-stu-id="b698b-176">Click **New Profile**.</span></span> <span data-ttu-id="b698b-177">Мы начнем с профиля **Full Import**(Полный импорт).</span><span class="sxs-lookup"><span data-stu-id="b698b-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="b698b-178">![Профиль выполнения 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="b698b-179">Выберите тип hello **полный импорт (только для этапа)**.</span><span class="sxs-lookup"><span data-stu-id="b698b-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="b698b-180">![Профиль выполнения 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="b698b-181">Выберите секцию hello **объект = пользователь**.</span><span class="sxs-lookup"><span data-stu-id="b698b-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="b698b-182">![Профиль выполнения 3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="b698b-183">Выберите **Table** и введите **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="b698b-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="b698b-184">Прокрутите вниз toohello разделе типа объекта с несколькими значениями и ввод данных hello как hello следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="b698b-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="b698b-185">Выберите **Готово** toosave hello шаг.</span><span class="sxs-lookup"><span data-stu-id="b698b-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="b698b-186">![Профиль выполнения 4а](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="b698b-187">![Профиль выполнения 4б](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="b698b-188">Выберите **New Step**(Новый шаг).</span><span class="sxs-lookup"><span data-stu-id="b698b-188">Select **New Step**.</span></span> <span data-ttu-id="b698b-189">На этот раз выберите **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="b698b-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="b698b-190">На последней странице hello используйте конфигурации hello как hello следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="b698b-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="b698b-191">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="b698b-191">Click **Finish**.</span></span>  
   <span data-ttu-id="b698b-192">![Профиль выполнения 5а](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="b698b-193">![Профиль выполнения 5б](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="b698b-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="b698b-194">Можно настроить дополнительные профили выполнения, но это необязательно.</span><span class="sxs-lookup"><span data-stu-id="b698b-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="b698b-195">В этом пошаговом руководстве используется только hello полный импорт.</span><span class="sxs-lookup"><span data-stu-id="b698b-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="b698b-196">Нажмите кнопку **ОК** toofinish изменение профилей выполнения.</span><span class="sxs-lookup"><span data-stu-id="b698b-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="b698b-197">Добавить некоторые Импорт теста данные и тестирования hello</span><span class="sxs-lookup"><span data-stu-id="b698b-197">Add some test data and test hello import</span></span>
<span data-ttu-id="b698b-198">Введите тестовые данные в образец базы данных.</span><span class="sxs-lookup"><span data-stu-id="b698b-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="b698b-199">Когда будете готовы, щелкните **Run** (Выполнить) и **Full import** (Полный импорт).</span><span class="sxs-lookup"><span data-stu-id="b698b-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="b698b-200">Здесь мы видим пользователя с двумя телефонными номерами и группу с несколькими участниками.</span><span class="sxs-lookup"><span data-stu-id="b698b-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![Пространство соединителя 1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![Пространство соединителя 2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="b698b-203">Приложении A</span><span class="sxs-lookup"><span data-stu-id="b698b-203">Appendix A</span></span>
<span data-ttu-id="b698b-204">**Сценарий toocreate hello образцы базы данных SQL**</span><span class="sxs-lookup"><span data-stu-id="b698b-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
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
