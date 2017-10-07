---
title: "aaaMigrate базы данных MySQL с помощью дампа и восстановления в базе данных Azure для MySQL | Документы Microsoft"
description: "В этой статье объясняется два распространенных способов tooback копирование и восстановление баз данных в базе данных Azure для MySQL, с помощью средств, таких как mysqldump MySQL Workbench и PHPMyAdmin."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: d05d483ff53483df8e005eae2d9a4f8190e8f663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-tooazure-database-for-mysql-using-dump-and-restore"></a>Перенести вашей tooAzure базы данных MySQL базы данных MySQL с помощью дампа и восстановления
В этой статье описывается два распространенных способов tooback копирование и восстановление баз данных в базе данных Azure для MySQL
- Дампа и восстановление из hello командной строки (с помощью mysqldump) 
- дамп и восстановление с помощью PHPMyAdmin. 

## <a name="before-you-begin"></a>Перед началом работы
toostep через этот как tooguide необходимые toohave.
- [создать сервер базы данных Azure для MySQL с помощью портала Azure](quickstart-create-mysql-server-database-using-azure-portal.md);
- установить на компьютере служебную программу командной строки [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html);
- MySQL Workbench [загрузить Workbench MySQL](https://dev.mysql.com/downloads/workbench/), Toad, Navicat или других toodo сторонних MySQL средство дампа и восстановить команды.

## <a name="use-common-tools"></a>Использование распространенных инструментов
Использование стандартных средств и средств, таких как MySQL Workbench, mysqldump, Toad или Navicat tooremotely подключения и восстановление данных в базе данных Azure для MySQL. Используйте такие средства на клиентском компьютере с Интернет toohello tooconnect подключения базы данных Azure для MySQL. Для обеспечения безопасности используйте подключение с SSL-шифрованием, а также см. статью [SSL-соединения в базе данных Azure для MySQL](concepts-ssl-connection-security.md). Местоположение специальные облака tooany файлов дампа toomove hello не обязательно при переносе tooAzure базы данных для MySQL. 

## <a name="common-uses-for-dump-and-restore"></a>Распространенные варианты использования дампа и восстановления
Вы можете использовать MySQL таких служебных программ mysqldump mysqlpump toodump и загрузка баз данных и в базе данных MySQL в несколько типичных сценариев. В других сценариях могут использовать hello [импорта и экспорта](concepts-migrate-import-export.md) вместо этого подхода.

- Использовать базу данных выводит при переносе hello всей базы данных. Эта рекомендация содержит при перемещении большой объем данных MySQL, или в том случае, когда требуется toominimize перерывов для динамической сайтов или приложений. 
-  Убедитесь, что все таблицы в базе данных hello следует использовать механизм хранения InnoDB hello при загрузке данных в базе данных Azure для MySQL. База данных Azure для MySQL поддерживает только подсистему хранилища InnoDB и не поддерживает другие подсистемы хранилища. Если таблицы должны быть настроены другие механизмы хранения, преобразуйте их в формат engine InnoDB hello перед tooAzure миграции базы данных для MySQL.
   Например при наличии WordPress или веб-приложения с использованием таблиц MyISAM hello, сначала преобразуйте эти таблицы путем переноса в формат InnoDB перед восстановлением базы данных tooAzure для MySQL. Используйте предложение hello `ENGINE=InnoDB` tooset hello ядро, используемое при создании новой таблицы, а затем перенесите данные hello в таблицу совместимые hello перед восстановлением hello. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```
- tooavoid любой совместимостью, убедитесь, hello при записи в дамп баз данных в системах источника и назначения hello используется одинаковая версия MySQL. Например если существующий сервер MySQL версии 5.7, необходимо перенести tooAzure базы данных MySQL настроена toorun версии 5.7. Hello `mysql_upgrade` команда не работает в базе данных Azure для MySQL server и не поддерживается. Если вам требуется tooupgrade версиях MySQL, сначала дамп или экспортировать нижней версию базы данных в более новой версии MySQL в собственной среде. Затем перед выполнением перемещения в базу данных Azure для MySQL запустите `mysql_upgrade`.

## <a name="performance-considerations"></a>Рекомендации по производительности
производительность toooptimize уведомление взять эти соображения при выполнении дампа больших баз данных:
-   Используйте hello `exclude-triggers` параметр в mysqldump при выполнении дампа баз данных. Исключите триггеры из дампа файлы tooavoid hello триггер команды обработки во время восстановления данных hello. 
-   Избегайте hello `single-transaction` параметр в mysqldump при выполнении дампа очень больших баз данных. Формирование дампа много таблиц в одной транзакции приводит дополнительного объема хранения и toobe ресурсы памяти использоваться во время восстановления и может привести к задержкам производительности или ограничения ресурсов.
-   Используйте несколько значений операции вставки при загрузке с SQL toominimize инструкции нагрузка при выполнении дампа баз данных. При использовании файлов дампа, созданных служебной программой mysqldump, операции вставки нескольких значений включены по умолчанию. 
-  Используйте hello `order-by-primary` параметр в mysqldump при выполнении дампа баз данных, чтобы данные hello в скрипт в порядке первичного ключа.
-   Используйте hello `disable-keys` параметр в mysqldump при выполнении дампа toodisable ограничения внешнего ключа перед загрузкой данных. Отключение проверок внешнего ключа обеспечивает значительный прирост производительности. Включить ограничения hello и проверка данных hello после hello нагрузки tooensure ссылочной целостности.
-   Используйте секционированные таблицы, когда это необходимо.
-   Загружайте данные в параллельном режиме. Избегайте слишком много параллелизма, которые бы привести к toohit ограничение ресурсов и отслеживать ресурсы с использованием hello метрик, доступных в hello портал Azure. 
-   Используйте hello `defer-table-indexes` параметр в mysqlpump при выполнении дампа баз данных, чтобы создание индексов происходит после загрузки данных таблицы.

## <a name="create-a-backup-file-from-hello-command-line-using-mysqldump"></a>Создать файл резервной копии из hello командной строки с помощью mysqldump
tooback копии существующей базы данных MySQL на сервере локальных hello, или на виртуальной машине, запустите hello следующую команду: 
```bash
$ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
```

Параметры tooprovide Hello являются:
- [uname] — имя пользователя базы данных; 
- [проход] hello пароль для базы данных (Обратите внимание, нет пробела между -p и hello пароль) 
- Имя базы данных [имяБазыДанных] hello 
- Имя файла hello [backupfile.sql] для резервного копирования базы данных 
- [--необ] hello mysqldump параметр 

Например, tooback копии базы данных с именем «testdb» на сервере MySQL с hello имени пользователя «testuser» и не testdb_backup.sql файл tooa пароль, используйте hello следующую команду. Hello команда создает резервную копию hello `testdb` базы данных в файл с именем `testdb_backup.sql`, который содержит все инструкции SQL hello необходимости toore-Создание hello базы данных. 

```bash
$ mysqldump -u root -p testdb > testdb_backup.sql
```
tooselect определенных таблиц в вашей базе данных tooback вверх, имена таблиц hello список разделенных пробелами. Например tooback копирование только таблицы table1 и table2 из hello «testdb», выполните в этом примере. 
```bash
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

tooback более чем одной базы данных за один раз, используйте hello--переключения базы данных и имена баз данных hello список разделенных пробелами. 
```bash
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```
tooback копирование всех баз данных hello в hello server за один раз, следует использовать hello--параметр базы данных все.
```
$ mysqldump -u root -p --all-databases > alldb_backup.sql 
```

## <a name="create-a-database-on-hello-target-azure-database-for-mysql-server"></a>Создание базы данных на целевом сервере hello базы данных Azure для сервера MySQL
Создайте пустую базу данных на целевом сервере hello базы данных Azure для MySQL server, где требуется сохранить данные hello toomigrate. С помощью средства, например MySQL Workbench, Toad или Navicat hello toocreate базы данных. Hello базы данных могут иметь одинаковые имена, что hello базу данных, является автономной hello дамп данных hello, или можно создать базу данных с другим именем.

tooget подключение, найдите сведения о соединении hello на странице свойств hello в базе данных Azure для MySQL.
![Найти сведения о соединении hello в hello портал Azure](./media/concepts-migrate-dump-restore/1_server-properties-name-login.png)

Добавьте сведения о соединении hello в вашей рабочей среды MySQL.
![Строка подключения MySQL Workbench](./media/concepts-migrate-dump-restore/2_setup-new-connection.png)


## <a name="restore-your-mysql-database-using-command-line-or-mysql-workbench"></a>Восстановление базы данных MySQL с помощью командной строки или MySQL Workbench
После создания hello целевой базы данных, можно использовать команду mysql hello или MySQL Workbench toorestore hello данных в определенных hello вновь созданные базы данных из файла дампа hello.
```bash
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```
В этом примере восстановите данные hello в hello вновь созданные базы данных на целевом сервере hello базы данных Azure для сервера MySQL.
```bash
$ mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p testdb < testdb_backup.sql
```

## <a name="export-using-phpmyadmin"></a>Экспорт с помощью PHPMyAdmin
tooexport, можно использовать общие средства phpMyAdmin hello, который может уже установлено локально в вашей среде. tooexport базу данных MySQL с помощью PHPMyAdmin:
- Откройте phpMyAdmin.
- Выберите свою базу данных. Щелкните имя базы данных hello в списке hello слева hello. 
- Нажмите кнопку hello **Экспорт** ссылку. Новая страница откроется дампа hello tooview базы данных.
- В hello экспортируемой области, щелкните hello **выделить все** связать toochoose hello таблицы в базе данных. 
- В hello области параметров SQL выберите соответствующие параметры hello. 
- Щелкните hello **Сохранить как файл** параметр и соответствующего сжатия hello и нажмите кнопку hello **Go** кнопки. Должно появиться диалоговое окно запроса вы toosave hello файл локально.

## <a name="import-using-phpmyadmin"></a>Импорт с помощью PHPMyAdmin
Импорт базы данных — примерно tooexporting. Здравствуйте, следующие действия:
- Откройте phpMyAdmin. 
- На странице установки phpMyAdmin hello, нажмите кнопку **добавить** tooadd базы данных Azure для сервера MySQL. Укажите сведения о подключении hello и сведения об имени входа.
- Создание соответствующим именем базы данных и выберите его в hello левой части экрана приветствия. toorewrite hello существующей базы данных, щелкните имя базы данных hello, установите все флажки hello рядом с именами таблиц hello и выберите **Drop** toodelete hello существующих таблиц. 
- Нажмите кнопку hello **SQL** ссылки tooshow hello страницу, где можно ввести в командах SQL, или отправить файл SQL. 
- Используйте hello **Обзор** файл базы данных кнопку toofind hello. 
- Нажмите кнопку hello **Go** кнопку tooexport hello архивации, выполнения команд SQL hello и повторного создания базы данных.

## <a name="next-steps"></a>Дальнейшие действия
[Подключение приложений tooAzure базы данных MySQL](./howto-connection-string.md)
