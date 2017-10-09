---
title: "aaaConnect tooSQL базы данных с помощью C и C++ | Документы Microsoft"
description: "Используйте образец hello в программный код этого краткого toobuild современных приложений с помощью C++ и поддерживаемый мощные реляционной базы данных в облаке hello с базой данных SQL Azure."
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>Подключение tooSQL базы данных с помощью C и C++
Это сообщение предназначено для C и C++ разработчики, tooconnect tooAzure баз данных SQL Server. Он является разбит на разделы, можно легко toohello раздел, который лучше всего захватывает интерес. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Необходимые условия для учебника hello C/C++
Убедитесь, что у вас есть hello следующих элементов:

* Активная учетная запись Azure. Если у вас нет такой учетной записи, вы можете зарегистрироваться для использования [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/) Необходимо установить toobuild компонентов языка C++ hello и запуска этого примера.
* [Инструменты разработки Visual Studio для Linux](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e). Если вы разрабатываете в Linux, необходимо также установить расширения Visual Studio Linux hello. 

## <a id="AzureSQL"></a>База данных SQL Azure и SQL Server на виртуальных машинах
Azure SQL в Microsoft SQL Server и представляет спроектированный tooprovide высокого уровня доступности, высокопроизводительных и масштабируемых службы. Существует много преимуществ toousing SQL Azure через собственный базу данных под управлением на локальном компьютере. SQL Azure не имеют tooinstall, настройки, поддержки или управлять базы данных, но только содержимое hello и hello структуры базы данных. В нее встроены такие возможности, как отказоустойчивость и избыточность, которые так важны при работе с базами данных. 

В данный момент Azure предлагает два варианта для обработки рабочих нагрузок сервера SQL: база данных SQL Azure (база данных как услуга) и сервер SQL на виртуальных машинах. Мы не может получить подробные сведения о hello различия между этими двумя за исключением того, что база данных Azure SQL является лучшим решением для новых облачных приложений tootake преимуществами hello сокращает затраты и предоставляют оптимизации производительности, который облачные службы. Если вы собираетесь миграция или расширение локальных toohello облачных приложений, SQL server на виртуальной машине Azure может удачным для вас. простой tookeep действия для данной статьи, давайте создадим базы данных Azure SQL. 

## <a id="ODBC"></a>Технологии доступа к данным: ODBC и OLE DB
Ничем не отличается tooAzure подключении баз данных SQL Server и в настоящее время существует два способа tooconnect toodatabases: (Open Database connectivity) ODBC и OLE DB (связывание и внедрение объектов базы данных). В последние годы корпорация Майкрософт поддерживает [ODBC для доступа к собственным реляционным данным](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/). Технология ODBC относительно проста и работает гораздо быстрее, чем OLE DB. Hello единственная оговорка здесь заключается в ODBC для использования старого стиля C API. 

## <a id="Create"></a>Шаг 1. Создание базы данных SQL Azure
В разделе hello [Приступая к работе страницы](sql-database-get-started-portal.md) toolearn как toocreate образца базы данных.  Кроме того, можно использовать эту [коротким двухминутное видео](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) toocreate базы данных Azure SQL с помощью hello портал Azure.

## <a id="ConnectionString"></a>Шаг 2. Получение строки подключения
После подготовки базы данных Azure SQL требуется toocarry out hello следующие сведения о соединении toodetermine действия и добавить ваш IP-адрес клиента для доступа в брандмауэре. 

В [портал Azure](https://portal.azure.com/), передавались с использованием hello строки подключения ODBC базы данных Azure SQL tooyour **Показать строки подключения базы данных** перечисляется в составе приветствия разделе общих сведений для базы данных: 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Скопируйте содержимое hello hello **ODBC (включает в себя Node.js) [проверки подлинности SQL]** строки. Мы используем эту строку tooconnect более поздней версии из наших интерпретатор командной строки C++ ODBC. Эта строка содержит такие сведения, как драйвер hello, server и других параметров подключения базы данных. 

## <a id="Firewall"></a>Шаг 3: Добавление брандмауэра toohello IP
Перейдите в раздел toohello брандмауэра для сервера базы данных и добавьте ваш [брандмауэр toohello IP клиента, выполнив следующие действия](sql-database-configure-firewall-settings.md) toomake убедиться, что мы можно для успешного подключения: 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

На этом этапе вы настроили базы данных SQL Azure и готов tooconnect из кода C++. 

## <a id="Windows"></a>Шаг 4. Подключение из приложения Windows C/C++
Можно с легкостью подключать tooyour [базу данных SQL Azure с использованием ODBC в Windows, использование этого образца](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) , которое создает с помощью Visual Studio. Образец Hello реализует интерпретатор командной строки ODBC, которое может быть tooour tooconnect используется база данных SQL Azure. В этом примере принимает или файл базы данных исходного имени файла (DSN) аргумент командной строки или строку hello verbose соединения, которую мы ранее скопированные из hello портал Azure. Открыть страницу свойств hello для этого проекта и вставьте строку подключения hello в качестве аргумента команды, как показано ниже: 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

Убедитесь, что вы сведениями hello правой проверки подлинности для базы данных как часть этой строки подключения базы данных. 

Запустите приложение toobuild hello его. Вы увидите hello следующие окна проверки успешного подключения. Можно даже запустить некоторые основные команды SQL, таких как **создать таблицу** toovalidate подключение к базе данных:

![Команды SQL](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

Кроме того можно создать файл источника данных, с помощью мастера hello, который запускается, когда нет аргументов командной. Рекомендуется попробовать и этот вариант. Этот файл DSN можно использовать для автоматизации и защиты параметров проверки подлинности: 

![Создание файла DSN](./media/sql-database-develop-cplusplus-simple/datasource.png)

Поздравляем! TooAzure SQL успешно теперь подключен с использованием C++ и ODBC в Windows. Можно продолжить чтение toodo hello одинаково для платформы Linux также. 

## <a id="Linux"></a>Шаг 5. Подключение из приложения Linux C/C++
В случае, если вы еще не слышали hello новости, но Visual Studio теперь можно toodevelop также приложения C++ для ОС Linux. Вы можете прочесть об этой новый сценарий в hello [Visual C++ для разработки Linux](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) блога. toobuild для Linux необходимо удаленный компьютер, где запущен в дистрибутив Linux. Если у вас нет такого компьютера, его можно быстро настроить при помощи [виртуальных машин Linux Azure](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Для выполнения инструкций этого руководства предположим, что у вас настроен дистрибутив Linux Ubuntu 16.04. Здесь шаги Hello также необходимо применить tooUbuntu 15.10, Red Hat 6 и Red Hat 7. 

Hello следующие шаги установки hello библиотеки, необходимые для SQL и ODBC для вашего дистрибутив:

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Запустите Visual Studio. В разделе Сервис -> Параметры -> кроссплатформенный -> Диспетчер соединений, добавьте поле подключения tooyour Linux: 

!["Средства" -> "Параметры"](./media/sql-database-develop-cplusplus-simple/tools.png)

После того как установлено подключение по протоколу SSH, создайте шаблон пустого проекта (Linux): 

![Шаблон нового проекта](./media/sql-database-develop-cplusplus-simple/template.png)

Затем можно добавить [новый исходный файл C и заменить его этим содержимым](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c). Используя hello ODBC API-интерфейсы SQLAllocHandle, SQLSetConnectAttr и SQLDriverConnect, необходимо будет tooinitialize и установить tooyour подключения базы данных. Как и с образцом Windows ODBC hello, необходимо вызов SQLDriverConnect tooreplace hello с подробными сведениями hello из вашего параметры строки подключения базы данных, ранее скопировано из hello портал Azure. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

Здравствуйте последнего самое toodo до компиляции tooadd **odbc** как зависимость библиотеки: 

![Добавление ODBC в качестве входной библиотеки](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch приложения, подключить hello консоли Linux из hello **отладки** меню: 

![Консоль Linux](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

Если подключение выполнено успешно, вы увидите hello имя текущей базы данных в hello консоли Linux: 

![Выходные данные в окне консоли Linux](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

Поздравляем! Учебник hello успешно завершена и теперь могут подключаться tooyour базу данных SQL Azure из C++ на платформах Windows и Linux.

## <a id="GetSolution"></a>Получить комплексное решение учебника hello C/C++
Можно найти hello GetStarted решение, которое содержит все образцы hello в этой статье в github:

* [Образец Windows на C++ ODBC](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), загрузите tooAzure tooconnect пример ODBC C++ Windows hello SQL
* [Пример ODBC C++ для ОС Linux](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), загрузите tooAzure tooconnect Linux C++ ODBC образец hello SQL

## <a name="next-steps"></a>Дальнейшие действия
* Просмотрите hello [Общие сведения о разработке базы данных SQL](sql-database-develop-overview.md)
* Дополнительные сведения о hello [Справочник по API-интерфейса ODBC](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Шаблоны разработки для мультитенантных приложений SaaS с использованием базы данных Azure SQL](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Просмотр всех hello [возможностей базы данных SQL](https://azure.microsoft.com/services/sql-database/)

