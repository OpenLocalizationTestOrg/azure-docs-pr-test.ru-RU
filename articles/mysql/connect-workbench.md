---
title: "Подключение tooAzure базы данных MySQL из рабочей среды MySQL | Документы Microsoft"
description: "Это краткое руководство предоставляет toouse действия hello MySQL Workbench tooconnect и запроса данных из базы данных Azure для MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="e09a4-103">База данных Azure для MySQL: используйте MySQL Workbench tooconnect и запроса данных</span><span class="sxs-lookup"><span data-stu-id="e09a4-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="e09a4-104">Это краткое руководство демонстрирует, как tooan tooconnect базы данных Azure для использования MySQL hello приложения MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="e09a4-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e09a4-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e09a4-105">Prerequisites</span></span>
<span data-ttu-id="e09a4-106">Это краткое руководство использует ресурсы hello, созданные в любой из этих руководствах по в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="e09a4-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="e09a4-107">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Создание сервера базы данных Azure для MySQL с помощью портала Azure)</span><span class="sxs-lookup"><span data-stu-id="e09a4-107">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="e09a4-108">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Создание сервера базы данных Azure для MySQL с помощью Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="e09a4-108">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-mysql-workbench"></a><span data-ttu-id="e09a4-109">Установка MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="e09a4-109">Install MySQL Workbench</span></span>
<span data-ttu-id="e09a4-110">Загрузите и установите на компьютер из рабочей среды MySQL [веб-сайта MySQL hello](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="e09a4-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="e09a4-111">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="e09a4-111">Get connection information</span></span>
<span data-ttu-id="e09a4-112">Получите toohello tooconnect базы данных Azure для hello подключения сведения, необходимые для MySQL.</span><span class="sxs-lookup"><span data-stu-id="e09a4-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="e09a4-113">Необходимо hello server полное имя и учетные данные входа.</span><span class="sxs-lookup"><span data-stu-id="e09a4-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e09a4-114">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e09a4-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="e09a4-115">Hello левого меню на портале Azure, щелкните **все ресурсы** и выполните поиск сервера hello, вы создали, таких как **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="e09a4-116">Щелкните имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="e09a4-116">Click hello server name.</span></span>

4. <span data-ttu-id="e09a4-117">Выберите hello server **свойства** страницы.</span><span class="sxs-lookup"><span data-stu-id="e09a4-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="e09a4-118">Запишите hello **имя сервера** и **имя входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="e09a4-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Имя сервера базы данных Azure для MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="e09a4-120">Если вы забыли учетные данные входа сервера, перейдите toohello **Обзор** страница hello tooview: имя пользователя администратора сервера и, при необходимости переустановить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="e09a4-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="e09a4-121">Подключиться с помощью MySQL Workbench server toohello</span><span class="sxs-lookup"><span data-stu-id="e09a4-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="e09a4-122">с помощью средства hello графического интерфейса пользователя MySQL Workbench MySQL server tooAzure tooconnect:</span><span class="sxs-lookup"><span data-stu-id="e09a4-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="e09a4-123">Запустите hello MySQL Workbench приложения на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e09a4-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="e09a4-124">В **установки нового подключения** диалогового окна введите следующую информацию на hello hello **параметры** вкладки:</span><span class="sxs-lookup"><span data-stu-id="e09a4-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![Настройка нового подключения](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="e09a4-126">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="e09a4-126">**Setting**</span></span> | <span data-ttu-id="e09a4-127">**Рекомендуемое значение**</span><span class="sxs-lookup"><span data-stu-id="e09a4-127">**Suggested value**</span></span> | <span data-ttu-id="e09a4-128">**Описание поля**</span><span class="sxs-lookup"><span data-stu-id="e09a4-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="e09a4-129">Имя подключения</span><span class="sxs-lookup"><span data-stu-id="e09a4-129">Connection Name</span></span> | <span data-ttu-id="e09a4-130">Пример подключения</span><span class="sxs-lookup"><span data-stu-id="e09a4-130">Demo Connection</span></span> | <span data-ttu-id="e09a4-131">Укажите метку для этого подключения.</span><span class="sxs-lookup"><span data-stu-id="e09a4-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="e09a4-132">Способ подключения</span><span class="sxs-lookup"><span data-stu-id="e09a4-132">Connection Method</span></span> | <span data-ttu-id="e09a4-133">Стандартный способ (по протоколу TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="e09a4-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="e09a4-134">Стандартный способ (по протоколу TCP/IP) соответствует требованиям.</span><span class="sxs-lookup"><span data-stu-id="e09a4-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="e09a4-135">имя узла;</span><span class="sxs-lookup"><span data-stu-id="e09a4-135">Hostname</span></span> | <span data-ttu-id="e09a4-136">*имя сервера*</span><span class="sxs-lookup"><span data-stu-id="e09a4-136">*server name*</span></span> | <span data-ttu-id="e09a4-137">Укажите значение имени сервера hello, который использовался при создании hello базы данных Azure для MySQL ранее.</span><span class="sxs-lookup"><span data-stu-id="e09a4-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="e09a4-138">В нашем примере используется такое имя сервера: myserver4demo.mysql.database.azure.com. Используйте hello полное доменное имя (\*. mysql.database.azure.com) как показано в примере hello.</span><span class="sxs-lookup"><span data-stu-id="e09a4-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="e09a4-139">Выполните действия hello hello предыдущего раздела tooget hello сведения о соединении, если вы не помните имя вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="e09a4-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="e09a4-140">Порт</span><span class="sxs-lookup"><span data-stu-id="e09a4-140">Port</span></span> | <span data-ttu-id="e09a4-141">3306</span><span class="sxs-lookup"><span data-stu-id="e09a4-141">3306</span></span> | <span data-ttu-id="e09a4-142">Всегда используйте порт 3306 при подключении tooAzure базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="e09a4-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="e09a4-143">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="e09a4-143">Username</span></span> |  <span data-ttu-id="e09a4-144">*имя для входа администратора сервера*</span><span class="sxs-lookup"><span data-stu-id="e09a4-144">*server admin login name*</span></span> | <span data-ttu-id="e09a4-145">Введите в hello входа имя входа администратора сервера указаны при создании hello базы данных Azure для MySQL ранее.</span><span class="sxs-lookup"><span data-stu-id="e09a4-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="e09a4-146">Пример нашего имени пользователя — myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="e09a4-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="e09a4-147">Выполните действия hello hello предыдущего раздела tooget hello сведения о соединении, если вы не помните hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="e09a4-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="e09a4-148">Формат Hello  *username@servername* .</span><span class="sxs-lookup"><span data-stu-id="e09a4-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="e09a4-149">Пароль</span><span class="sxs-lookup"><span data-stu-id="e09a4-149">Password</span></span> | <span data-ttu-id="e09a4-150">Ваш пароль.</span><span class="sxs-lookup"><span data-stu-id="e09a4-150">your password</span></span> | <span data-ttu-id="e09a4-151">Нажмите кнопку **хранилища в хранилище...**  кнопку toosave hello пароль.</span><span class="sxs-lookup"><span data-stu-id="e09a4-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="e09a4-152">Нажмите кнопку **проверить подключение** tootest, если все параметры настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="e09a4-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="e09a4-153">Нажмите кнопку **ОК** toosave hello соединения.</span><span class="sxs-lookup"><span data-stu-id="e09a4-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="e09a4-154">В списке hello **подключений MySQL**выберите сервер tooyour соответствующие плитки hello и ожидания для установления toobe подключения hello.</span><span class="sxs-lookup"><span data-stu-id="e09a4-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="e09a4-155">Откроется новая вкладка SQL с пустым окном редактора, в котором можно вводить запросы.</span><span class="sxs-lookup"><span data-stu-id="e09a4-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e09a4-156">По умолчанию защита SSL-подключения является обязательной и применяется к базе данных Azure для сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="e09a4-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="e09a4-157">Обычно для сервера tooyour tooconnect MySQL Workbench требуется дополнительная настройка с использованием сертификата SSL.</span><span class="sxs-lookup"><span data-stu-id="e09a4-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="e09a4-158">Дополнительные сведения о протоколе SSL см. в разделе [Настройка SSL-подключения в toosecurely вашего приложения подключения tooAzure базы данных MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="e09a4-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="e09a4-159">При необходимости toodisable SSL посетите портал Azure hello и нажмите hello страница безопасности подключения toodisable hello переключателя подключения применять SSL кнопку.</span><span class="sxs-lookup"><span data-stu-id="e09a4-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="e09a4-160">Создание таблицы, добавление, считывание, обновление и удаление данных</span><span class="sxs-lookup"><span data-stu-id="e09a4-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="e09a4-161">Скопируйте и вставьте код SQL в образце hello в пустой tooillustrate вкладку SQL образцами данных.</span><span class="sxs-lookup"><span data-stu-id="e09a4-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="e09a4-162">Этот код создает пустую базу данных с именем quickstartdb, а затем создает пример таблицы с именем inventory.</span><span class="sxs-lookup"><span data-stu-id="e09a4-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="e09a4-163">Вставляет несколько строк, затем считывает строки hello.</span><span class="sxs-lookup"><span data-stu-id="e09a4-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="e09a4-164">Он изменяет hello данных с помощью инструкции update и операций чтения hello строк еще раз.</span><span class="sxs-lookup"><span data-stu-id="e09a4-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="e09a4-165">Наконец он удаляет строку и еще раз считывает строки hello.</span><span class="sxs-lookup"><span data-stu-id="e09a4-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="e09a4-166">Снимок экрана приветствия показан пример hello кода SQL в SQL Workbench и hello выходных данных после его запуска.</span><span class="sxs-lookup"><span data-stu-id="e09a4-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![Вкладка SQL Workbench MySQL toorun пример кода SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="e09a4-168">Образец hello toorun кода SQL, щелкните счет молнии панели инструментов hello hello hello **файл SQL** вкладки.</span><span class="sxs-lookup"><span data-stu-id="e09a4-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="e09a4-169">Обратите внимание, hello три результаты с вкладками в hello **сетки** раздел в середине hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e09a4-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="e09a4-170">Обратите внимание hello **вывода** списке hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e09a4-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="e09a4-171">отображается состояние Hello каждой команды.</span><span class="sxs-lookup"><span data-stu-id="e09a4-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="e09a4-172">Теперь для MySQL с помощью MySQL Workbench подключились tooAzure базы данных и запросов данных с помощью языка SQL hello.</span><span class="sxs-lookup"><span data-stu-id="e09a4-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e09a4-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e09a4-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e09a4-174">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="e09a4-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
