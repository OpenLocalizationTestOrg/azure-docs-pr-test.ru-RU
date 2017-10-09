---
title: "aaaDesign первый Azure базы данных для базы данных MySQL - портал Azure | Документы Microsoft"
description: "В этом учебнике описано как toocreate и управления базой данных Azure для MySQL server и базы данных с помощью портала Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Проектирование первой базы данных Azure для MySQL
База данных Azure для MySQL является управляемой службы, которая позволяет toorun, управлять и масштабировать высокодоступных баз данных MySQL в облаке hello. С помощью hello портал Azure, можно легко управлять сервером и разработке базы данных.

В этом учебнике используется hello Azure портала toolearn как для:

> [!div class="checklist"]
> * создание базы данных Azure для MySQL;
> * Настройте брандмауэр сервера hello
> * Используйте средство командной строки mysql toocreate базы данных
> * Загрузка примера данных
> * Запрос данных
> * Обновление данных
> * восстановление данных.

## <a name="sign-in-toohello-azure-portal"></a>Войдите в toohello портал Azure
Откройте избранных веб-браузере и войдите hello [портал Microsoft Azure](https://portal.azure.com/). Введите ваш toosign учетные данные на портале toohello. представление по умолчанию Hello, панели мониторинга службы.

## <a name="create-an-azure-database-for-mysql-server"></a>Создание сервера базы данных Azure для MySQL
Сервер базы данных Azure для MySQL создается с определенным набором [вычислительных ресурсов и ресурсов хранения](./concepts-compute-unit-and-storage.md). сервер Hello создается в пределах [группы ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

1. Перейдите в слишком**баз данных** > **базы данных Azure для MySQL**. Если не удается найти сервер MySQL в группе **баз данных** категории, нажмите кнопку **все** tooshow все доступные службы баз данных. Можно также ввести **базы данных Azure для MySQL** в tooquickly поле поиска hello найдите службу hello.
![Навигатор tooMySQL 2-1](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. Щелкните элемент **База данных Azure для MySQL**, а затем нажмите кнопку **Создать**.

В нашем примере заполните hello базы данных Azure для MySQL формы с hello следующую информацию:

| **Параметр** | **Рекомендуемое значение** | **Описание поля** |
|---|---|---|
| *Server name* (Имя сервера) | myserver4demo  | Имя сервера содержит toobe глобально уникальным. |
| *Подписка* | mysubscription | Выберите подписку из раскрывающегося списка hello. |
| *Группа ресурсов* | myresourcegroup | Создайте новую группу ресурсов или выберите существующую. |
| *Имя для входа администратора сервера* | myadmin | Укажите имя учетной записи администратора. |
| *Пароль* |  | Укажите надежный пароль для учетной записи администратора. |
| *Подтверждение пароля.* |  | Подтвердите пароль учетной записи администратора hello. |
| *Расположение* |  | Выберите доступный регион. |
| *Версия* | 5.7 | Выберите последнюю версию hello. |
| *Настройка производительности* | "Базовый", 50 единиц вычислений, 50 ГБ  | Укажите значения для параметров **Ценовая категория**, **Единицы вычислений**, **Хранилище (ГБ)** и нажмите кнопку **ОК**. |
| *TooDashboard ПИН-кода* | Проверка | Рекомендуется toocheck этот флажок, поэтому может оказаться hello server легко позже на |
Затем щелкните **Создать**. В одну-две минуты в облаке hello выполняется новой базы данных Azure для сервера MySQL. Можно щелкнуть **уведомления** кнопку на панели инструментов toomonitor hello hello-процесс развертывания.

## <a name="configure-firewall"></a>Настройка брандмауэра
Базы данных Azure для MySQL защищены брандмауэром. По умолчанию все соединения toohello сервера hello базы данных и внутри сервера hello, отклоняются. Прежде чем подключаться tooAzure базы данных MySQL для hello первый раз, настройте IP-адрес общедоступной сети hello брандмауэра tooadd hello на компьютере клиента (или диапазон IP-адресов).

1. Щелкните созданный сервер и выберите **Безопасность подключения**.
   ![3.1. Безопасность подключения](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. Здесь вы можете **добавить свой IP-адрес** или настроить правила брандмауэра. Помните, tooclick **Сохранить** после создания правила hello.
Теперь можно подключиться toohello сервера с помощью средства командной строки mysql или средство графического интерфейса пользователя MySQL рабочей среды.

> [!TIP]
> Сервер базы данных Azure для MySQL обменивается данными через порт 3306. Если вы пытаетесь tooconnect из корпоративной сети, исходящий трафик через порт 3306 может оказаться невозможным брандмауэром вашей сети. В этом случае tooAzure MySQL server не удается подключиться, если ИТ-отдел открывает порт 3306.

## <a name="get-connection-information"></a>Получение сведений о подключении
Полное hello Get **имя сервера** и **имя входа администратора сервера** для базы данных Azure для сервера MySQL из hello портал Azure. Можно использовать hello полное имя tooconnect tooyour сервер с помощью средства командной строки mysql. 

1. В [портал Azure](https://portal.azure.com/), нажмите кнопку **все ресурсы** из левого меню hello, имя типа hello и поиск для базы данных Azure для сервера MySQL. Выберите данные hello tooview имени сервера hello.

2. В разделе hello параметров щелкните **свойства**. Запишите значения параметров **Имя сервера** и **Имя для входа администратора сервера**. Можно щелкнуть hello скопировать кнопку Далее tooeach поле toocopy toohello буфер обмена.
   ![4.2. Свойства сервера](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

В этом примере — имя сервера hello *myserver4demo.mysql.database.azure.com*, и имя входа администратора сервера hello является  *myadmin@myserver4demo* .

## <a name="connect-toohello-server-using-mysql"></a>Подключиться с помощью mysql server toohello
Используйте [средство командной строки mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish tooyour подключения базы данных Azure для сервера MySQL. Средство командной строки mysql hello можно запустить hello оболочки облако Azure в обозревателе hello с компьютера с помощью средства mysql установлены локально. hello toolaunch оболочки облако Azure, щелкните hello `Try It` на блок кода в этой статье, или посетите портал Azure hello и нажмите кнопку hello `>_` значок в верхней правой панели инструментов hello. 

Введите команду tooconnect hello:
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>Создание пустой базы данных
Когда вы будете toohello подключенного сервера, создайте toowork пустую базу данных с.
```sql
CREATE DATABASE mysampledb;
```

В строке приветствия выполните hello, следующая команда tooswitch подключение к только что созданный toothis базе данных:
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Создание таблиц в базе данных hello
Теперь, когда вы знаете, как tooconnect toohello базы данных Azure для базы данных MySQL, мы можем открыть как toocomplete некоторых базовых задач.

Сначала можно создать таблицу и заполнить ее некоторыми данными. Давайте создадим таблицу, в которой хранятся данные инвентаризации.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Загрузка данных в таблицы hello
Теперь, когда таблица создана, мы можем вставить в нее данные. Привет открыть окно командной строки запустите следующий запрос tooinsert hello некоторых строк данных.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Теперь у вас две строки образца данных в таблицу hello, созданную ранее.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Запрашивать и обновлять данные hello в таблицах hello
Выполните следующую информацию tooretrieve запроса из таблицы базы данных hello hello.
```sql
SELECT * FROM inventory;
```

Можно также обновить данные hello в таблицах hello.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

Строка Hello обновляется соответствующим образом при извлечении данных.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Восстановление предыдущей точки tooa базы данных времени
Представьте, что случайно удалили таблицу важные базы данных, невозможно было легко восстановить данные hello. Базы данных Azure для MySQL позволяет toorestore hello server tooa точки времени, создав копию hello баз данных на новый сервер. Можно использовать этот новый сервер toorecover удаленные данные. Здравствуйте, следующая точка tooa сервера образец hello действия восстановления перед hello таблица была добавлена.

1. Найдите базу данных Azure для MySQL hello портал Azure. На hello **Обзор** щелкните **восстановить** на панели инструментов hello. Откроется страница приветствия восстановления.

   ![10.1. Восстановление базы данных](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Заполните hello **восстановить** формы с hello необходимые сведения.
   
   ![10.2. Форма восстановления](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **Точка восстановления**: выберите в момент, которые должны toorestore, в течение периода времени hello в списке. Убедитесь, что tooconvert tooUTC ваш локальный часовой пояс.
   - **Восстановление сервера toonew**: Введите имя нового сервера требуется toorestore для.
   - **Расположение**: hello региона совпадает с исходного сервера hello и не может быть изменено.
   - **Ценовая категория**: hello ценовой категории — hello таким же, как hello исходный сервер и не может быть изменено.
   
3. Нажмите кнопку **ОК** toorestore hello server слишком[моментов времени tooa](./howto-restore-server-portal.md) перед hello таблица была удалена. Восстановление сервера создает новую копию hello server, на момент времени, заданного hello. 

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике используется hello Azure портала toolearned как для:

> [!div class="checklist"]
> * создание базы данных Azure для MySQL;
> * Настройте брандмауэр сервера hello
> * Используйте средство командной строки mysql toocreate базы данных
> * Загрузка примера данных
> * Запрос данных
> * Обновление данных
> * восстановление данных.

> [!div class="nextstepaction"]
> [Как tooAzure tooconnect приложений базы данных MySQL](./howto-connection-string.md)
