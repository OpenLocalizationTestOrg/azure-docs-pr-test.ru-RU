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
# <a name="install-and-configure-postgresql-on-azure"></a>Установка и настройка PostgreSQL в Azure
PostgreSQL — это аналогичный tooOracle расширенные базы данных с открытым исходным кодом и DB2. Она предлагает возможности корпоративного уровня, обеспечивая полное соответствие принципам ACID, надежную обработку транзакций и управление параллелизмом в разных версиях. Она также поддерживает такие стандарты, как ANSI SQL и SQL/MED (включая оболочки для внешних данных Oracle, MySQL, MongoDB и др.). Высокая расширяемость обеспечивается поддержкой более 12 процедурных языков, индексов GIN и GIST, пространственных данных, различных функций NoSQL для JSON и приложений на основе пары "ключ — значение".

В этой статье вы узнаете, как tooinstall и настраивать PostgreSQL на виртуальной машине Azure под управлением Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>Установка PostgreSQL
> [!NOTE]
> Необходимо иметь уже виртуальной машине Azure под управлением Linux в порядке toocomplete этого учебника. toocreate и настройка виртуальной Машины Linux, прежде чем продолжить, в разделе [виртуальной Машине Linux Azure учебника](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

В этом случае использование порта 1999 г., PostgreSQL порт hello.  

Подключите toohello виртуальных Машин Linux, созданных посредством PuTTY. Если это первый раз используете ВМ Linux Azure hello. в разделе [как tooUse SSH с Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) как PuTTY toouse toolearn tooconnect tooa виртуальной Машины с Linux.

1. Выполнения hello следующая команда корневой toohello tooswitch (для администратора):
   
        # sudo su -
2. Для некоторых дистрибутивов требуется перед установкой PostgreSQL установить другие программы. Проверьте Ваш дистрибутив в этом списке и выполните соответствующую команду hello:
   
   * Linux на базе Red Hat:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Linux на базе Debian:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Загрузите PostgreSQL в корневой каталог hello и затем распакуйте hello пакета:
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Hello выше приведен пример. Можно найти hello более подробное загрузить адрес в hello [индекс/pub/источника/](https://ftp.postgresql.org/pub/source/).
4. toostart сборки hello, выполните следующие команды:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Toobuild все, что может быть собран, включая документацию hello (страницы HTML и man) и дополнительных модулей (contrib), выполните следующую команду, вместо hello:
   
        # gmake install-world
   
    Должно появиться следующие сообщения о подтверждении hello.
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>Настройка PostgreSQL
1. (Необязательно) Создание типа hello tooshorten символьную ссылку PostgreSQL ссылки toonot входят: номер версии hello:
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Создайте каталог для hello базы данных:
   
        # mkdir -p /opt/pgsql_data
3. Создайте непривилегированного пользователя и измените его профиль. Toothis нового пользователя, нажмите кнопку (вызывается *postgres* в нашем примере):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > По соображениям безопасности PostgreSQL использует tooinitialize непривилегированного пользователя, запуск или завершение работы базы данных hello.
   > 
   > 
4. Изменить hello *bash_profile* файл, введя приведенную ниже команду hello. Эти строки будут добавлены toohello конец hello *bash_profile* файла:
   
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
5. Выполнение hello *bash_profile* файла:
   
        $ source .bash_profile
6. Проверка установки с помощью hello следующую команду:
   
        $ which psql
   
    При успешном выполнении установки вы увидите hello следующий ответ:
   
        /opt/pgsql/bin/psql
7. Можно также проверить hello PostgreSQL версии:
   
        $ psql -V
8. Инициализация hello базы данных:
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Должно появиться hello следующие выходные данные:

![изображение](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>Настройка PostgreSQL
<!--    [postgres@ test ~]$ exit -->

Выполните следующие команды hello.

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Изменение двух переменных в файле /etc/init.d/postgresql hello. префикс Hello задается путь установки toohello PostgreSQL: **pgsql/opt/**. PGDATA задается путь хранения данных toohello PostgreSQL: **pgsql_data/opt/**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![изображение](./media/postgresql-install/no2.png)

Измените файл toomake hello его исполняемый файл:

    # chmod +x /etc/init.d/postgresql

Запустите PostgreSQL:

    # /etc/init.d/postgresql start

Проверьте, является ли конечная точка hello PostgreSQL на:

    # netstat -tunlp|grep 1999

Вы увидите hello следующие выходные данные:

![изображение](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Подключение базы данных Postgres toohello
Смена пользователя postgres toohello еще раз:

    # su - postgres

Создайте базу данных Postgres:

    $ createdb events

Подключение событий базы данных, которая только что созданный toohello:

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Создание и удаление таблицы Postgres
Теперь, когда вы подключились toohello базы данных, можно создать в нем таблицы.

Например можно создайте новую таблицу Postgres примере с помощью hello следующую команду:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

Теперь вы настроили четыре столбца таблицы с hello следующие имена столбцов и ограничений:

1. Привет, столбца «name» была ограничена по toobe команда VARCHAR hello менее 20 символов.
2. столбец «food» Hello указывает hello блюда, на котором каждый пользователь. VARCHAR ограничивает toobe этот текст в 30 символов.
3. Hello «подтвердить» столбец записи ли hello лицо RSVP'd toohello обед. Hello допустимые значения: «Y» и «N».
4. Hello «date» отображается при регистрации события hello. В Postgres даты должны записываться в формате гггг-мм-дд.

Если таблица была создана успешно, вы увидите hello следующее:

![изображение](./media/postgresql-install/no4.png)

Можно также проверить hello структура таблицы с помощью hello следующую команду:

![изображение](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Добавить таблицу данных tooa
Прежде всего, вставьте в строку следующие сведения:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

Вы должны увидеть такой результат:

![изображение](./media/postgresql-install/no6.png)

Можно добавить несколько дополнительных toohello таблицу people также. Здесь мы привели несколько примеров, однако вы можете создать собственные:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Просмотр таблиц
Используйте hello, следующая команда tooshow таблицы:

    select * from potluck;

Hello отобразится следующее.

![изображение](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Удаление данных из таблицы
Используйте hello следующая команда toodelete данных в таблице:

    delete from potluck where name=’John’;

Это удаляет всю информацию hello в hello строки «John». Hello отобразится следующее.

![изображение](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Обновление данных в таблице
Используйте hello следующая команда tooupdate данных в таблице. Sandy подтвердила, что она принимает участие, поэтому изменим ее RSVP из «N» слишком «Y»:

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>Получение дополнительных сведений о PostgreSQL
После выполнения установки hello PostgreSQL на виртуальной Машине Linux Azure вам нравится, ее использования в Azure. toolearn Дополнительные сведения о PostgreSQL, посетите hello [PostgreSQL веб-сайт](http://www.postgresql.org/).

