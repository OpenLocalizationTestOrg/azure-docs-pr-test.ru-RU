---
title: "aaaSet копирование PostgreSQL на виртуальной Машине Linux | Документы Microsoft"
description: "Узнайте, как tooinstall и настраивать PostgreSQL на виртуальной машине Linux в Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="58c5b-103">Установка и настройка PostgreSQL в Azure</span><span class="sxs-lookup"><span data-stu-id="58c5b-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="58c5b-104">PostgreSQL — это аналогичный tooOracle расширенные базы данных с открытым исходным кодом и DB2.</span><span class="sxs-lookup"><span data-stu-id="58c5b-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="58c5b-105">Она предлагает возможности корпоративного уровня, обеспечивая полное соответствие принципам ACID, надежную обработку транзакций и управление параллелизмом в разных версиях.</span><span class="sxs-lookup"><span data-stu-id="58c5b-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="58c5b-106">Она также поддерживает такие стандарты, как ANSI SQL и SQL/MED (включая оболочки для внешних данных Oracle, MySQL, MongoDB и др.).</span><span class="sxs-lookup"><span data-stu-id="58c5b-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="58c5b-107">Высокая расширяемость обеспечивается поддержкой более 12 процедурных языков, индексов GIN и GIST, пространственных данных, различных функций NoSQL для JSON и приложений на основе пары "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="58c5b-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="58c5b-108">В этой статье вы узнаете, как tooinstall и настраивать PostgreSQL на виртуальной машине Azure под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="58c5b-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="58c5b-109">Установка PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="58c5b-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="58c5b-110">Необходимо иметь уже виртуальной машине Azure под управлением Linux в порядке toocomplete этого учебника.</span><span class="sxs-lookup"><span data-stu-id="58c5b-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="58c5b-111">toocreate и настройка виртуальной Машины Linux, прежде чем продолжить, в разделе [виртуальной Машине Linux Azure учебника](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58c5b-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="58c5b-112">В этом случае использование порта 1999 г., PostgreSQL порт hello.</span><span class="sxs-lookup"><span data-stu-id="58c5b-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="58c5b-113">Подключите toohello виртуальных Машин Linux, созданных посредством PuTTY.</span><span class="sxs-lookup"><span data-stu-id="58c5b-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="58c5b-114">Если это первый раз используете ВМ Linux Azure hello. в разделе [как tooUse SSH с Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) как PuTTY toouse toolearn tooconnect tooa виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="58c5b-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="58c5b-115">Выполнения hello следующая команда корневой toohello tooswitch (для администратора):</span><span class="sxs-lookup"><span data-stu-id="58c5b-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="58c5b-116">Для некоторых дистрибутивов требуется перед установкой PostgreSQL установить другие программы.</span><span class="sxs-lookup"><span data-stu-id="58c5b-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="58c5b-117">Проверьте Ваш дистрибутив в этом списке и выполните соответствующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="58c5b-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="58c5b-118">Linux на базе Red Hat:</span><span class="sxs-lookup"><span data-stu-id="58c5b-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="58c5b-119">Linux на базе Debian:</span><span class="sxs-lookup"><span data-stu-id="58c5b-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="58c5b-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="58c5b-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="58c5b-121">Загрузите PostgreSQL в корневой каталог hello и затем распакуйте hello пакета:</span><span class="sxs-lookup"><span data-stu-id="58c5b-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="58c5b-122">Hello выше приведен пример.</span><span class="sxs-lookup"><span data-stu-id="58c5b-122">hello above is an example.</span></span> <span data-ttu-id="58c5b-123">Можно найти hello более подробное загрузить адрес в hello [индекс/pub/источника/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="58c5b-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="58c5b-124">toostart сборки hello, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="58c5b-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="58c5b-125">Toobuild все, что может быть собран, включая документацию hello (страницы HTML и man) и дополнительных модулей (contrib), выполните следующую команду, вместо hello:</span><span class="sxs-lookup"><span data-stu-id="58c5b-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="58c5b-126">Должно появиться следующие сообщения о подтверждении hello.</span><span class="sxs-lookup"><span data-stu-id="58c5b-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="58c5b-127">Настройка PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="58c5b-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="58c5b-128">(Необязательно) Создание типа hello tooshorten символьную ссылку PostgreSQL ссылки toonot входят: номер версии hello:</span><span class="sxs-lookup"><span data-stu-id="58c5b-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="58c5b-129">Создайте каталог для hello базы данных:</span><span class="sxs-lookup"><span data-stu-id="58c5b-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="58c5b-130">Создайте непривилегированного пользователя и измените его профиль.</span><span class="sxs-lookup"><span data-stu-id="58c5b-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="58c5b-131">Toothis нового пользователя, нажмите кнопку (вызывается *postgres* в нашем примере):</span><span class="sxs-lookup"><span data-stu-id="58c5b-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="58c5b-132">По соображениям безопасности PostgreSQL использует tooinitialize непривилегированного пользователя, запуск или завершение работы базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="58c5b-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="58c5b-133">Изменить hello *bash_profile* файл, введя приведенную ниже команду hello.</span><span class="sxs-lookup"><span data-stu-id="58c5b-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="58c5b-134">Эти строки будут добавлены toohello конец hello *bash_profile* файла:</span><span class="sxs-lookup"><span data-stu-id="58c5b-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. <span data-ttu-id="58c5b-135">Выполнение hello *bash_profile* файла:</span><span class="sxs-lookup"><span data-stu-id="58c5b-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="58c5b-136">Проверка установки с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="58c5b-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="58c5b-137">При успешном выполнении установки вы увидите hello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="58c5b-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="58c5b-138">Можно также проверить hello PostgreSQL версии:</span><span class="sxs-lookup"><span data-stu-id="58c5b-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="58c5b-139">Инициализация hello базы данных:</span><span class="sxs-lookup"><span data-stu-id="58c5b-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="58c5b-140">Должно появиться hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="58c5b-140">You should receive hello following output:</span></span>

![изображение](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="58c5b-142">Настройка PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="58c5b-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="58c5b-143">Выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="58c5b-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="58c5b-144">Изменение двух переменных в файле /etc/init.d/postgresql hello.</span><span class="sxs-lookup"><span data-stu-id="58c5b-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="58c5b-145">префикс Hello задается путь установки toohello PostgreSQL: **pgsql/opt/**.</span><span class="sxs-lookup"><span data-stu-id="58c5b-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="58c5b-146">PGDATA задается путь хранения данных toohello PostgreSQL: **pgsql_data/opt/**.</span><span class="sxs-lookup"><span data-stu-id="58c5b-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![изображение](./media/postgresql-install/no2.png)

<span data-ttu-id="58c5b-148">Измените файл toomake hello его исполняемый файл:</span><span class="sxs-lookup"><span data-stu-id="58c5b-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="58c5b-149">Запустите PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="58c5b-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="58c5b-150">Проверьте, является ли конечная точка hello PostgreSQL на:</span><span class="sxs-lookup"><span data-stu-id="58c5b-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="58c5b-151">Вы увидите hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="58c5b-151">You should see hello following output:</span></span>

![изображение](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="58c5b-153">Подключение базы данных Postgres toohello</span><span class="sxs-lookup"><span data-stu-id="58c5b-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="58c5b-154">Смена пользователя postgres toohello еще раз:</span><span class="sxs-lookup"><span data-stu-id="58c5b-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="58c5b-155">Создайте базу данных Postgres:</span><span class="sxs-lookup"><span data-stu-id="58c5b-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="58c5b-156">Подключение событий базы данных, которая только что созданный toohello:</span><span class="sxs-lookup"><span data-stu-id="58c5b-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="58c5b-157">Создание и удаление таблицы Postgres</span><span class="sxs-lookup"><span data-stu-id="58c5b-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="58c5b-158">Теперь, когда вы подключились toohello базы данных, можно создать в нем таблицы.</span><span class="sxs-lookup"><span data-stu-id="58c5b-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="58c5b-159">Например можно создайте новую таблицу Postgres примере с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="58c5b-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="58c5b-160">Теперь вы настроили четыре столбца таблицы с hello следующие имена столбцов и ограничений:</span><span class="sxs-lookup"><span data-stu-id="58c5b-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="58c5b-161">Привет, столбца «name» была ограничена по toobe команда VARCHAR hello менее 20 символов.</span><span class="sxs-lookup"><span data-stu-id="58c5b-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="58c5b-162">столбец «food» Hello указывает hello блюда, на котором каждый пользователь.</span><span class="sxs-lookup"><span data-stu-id="58c5b-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="58c5b-163">VARCHAR ограничивает toobe этот текст в 30 символов.</span><span class="sxs-lookup"><span data-stu-id="58c5b-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="58c5b-164">Hello «подтвердить» столбец записи ли hello лицо RSVP'd toohello обед.</span><span class="sxs-lookup"><span data-stu-id="58c5b-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="58c5b-165">Hello допустимые значения: «Y» и «N».</span><span class="sxs-lookup"><span data-stu-id="58c5b-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="58c5b-166">Hello «date» отображается при регистрации события hello.</span><span class="sxs-lookup"><span data-stu-id="58c5b-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="58c5b-167">В Postgres даты должны записываться в формате гггг-мм-дд.</span><span class="sxs-lookup"><span data-stu-id="58c5b-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="58c5b-168">Если таблица была создана успешно, вы увидите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="58c5b-168">You should see hello following if your table has been successfully created:</span></span>

![изображение](./media/postgresql-install/no4.png)

<span data-ttu-id="58c5b-170">Можно также проверить hello структура таблицы с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="58c5b-170">You can also check hello table structure by using hello following command:</span></span>

![изображение](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="58c5b-172">Добавить таблицу данных tooa</span><span class="sxs-lookup"><span data-stu-id="58c5b-172">Add data tooa table</span></span>
<span data-ttu-id="58c5b-173">Прежде всего, вставьте в строку следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="58c5b-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="58c5b-174">Вы должны увидеть такой результат:</span><span class="sxs-lookup"><span data-stu-id="58c5b-174">You should see this output:</span></span>

![изображение](./media/postgresql-install/no6.png)

<span data-ttu-id="58c5b-176">Можно добавить несколько дополнительных toohello таблицу people также.</span><span class="sxs-lookup"><span data-stu-id="58c5b-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="58c5b-177">Здесь мы привели несколько примеров, однако вы можете создать собственные:</span><span class="sxs-lookup"><span data-stu-id="58c5b-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="58c5b-178">Просмотр таблиц</span><span class="sxs-lookup"><span data-stu-id="58c5b-178">Show tables</span></span>
<span data-ttu-id="58c5b-179">Используйте hello, следующая команда tooshow таблицы:</span><span class="sxs-lookup"><span data-stu-id="58c5b-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="58c5b-180">Hello отобразится следующее.</span><span class="sxs-lookup"><span data-stu-id="58c5b-180">hello output is:</span></span>

![изображение](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="58c5b-182">Удаление данных из таблицы</span><span class="sxs-lookup"><span data-stu-id="58c5b-182">Delete data in a table</span></span>
<span data-ttu-id="58c5b-183">Используйте hello следующая команда toodelete данных в таблице:</span><span class="sxs-lookup"><span data-stu-id="58c5b-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="58c5b-184">Это удаляет всю информацию hello в hello строки «John».</span><span class="sxs-lookup"><span data-stu-id="58c5b-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="58c5b-185">Hello отобразится следующее.</span><span class="sxs-lookup"><span data-stu-id="58c5b-185">hello output is:</span></span>

![изображение](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="58c5b-187">Обновление данных в таблице</span><span class="sxs-lookup"><span data-stu-id="58c5b-187">Update data in a table</span></span>
<span data-ttu-id="58c5b-188">Используйте hello следующая команда tooupdate данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="58c5b-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="58c5b-189">Sandy подтвердила, что она принимает участие, поэтому изменим ее RSVP из «N» слишком «Y»:</span><span class="sxs-lookup"><span data-stu-id="58c5b-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="58c5b-190">Получение дополнительных сведений о PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="58c5b-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="58c5b-191">После выполнения установки hello PostgreSQL на виртуальной Машине Linux Azure вам нравится, ее использования в Azure.</span><span class="sxs-lookup"><span data-stu-id="58c5b-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="58c5b-192">toolearn Дополнительные сведения о PostgreSQL, посетите hello [PostgreSQL веб-сайт](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="58c5b-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

