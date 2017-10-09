---
title: "aaaCreate и управления базой данных Azure для правила брандмауэра PostgreSQL, с помощью hello портал Azure | Документы Microsoft"
description: "Создание и управление для правила брандмауэра PostgreSQL, с помощью портала Azure hello базы данных Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Создание и управление для правила брандмауэра PostgreSQL, с помощью портала Azure hello базы данных Azure
Правила брандмауэра уровня сервера включите tooaccess администраторы базы данных Azure для сервера PostgreSQL указанный IP-адрес или диапазон IP-адресов. 

## <a name="prerequisites"></a>Предварительные требования
toostep через этот как tooguide необходимо:
- [сервер базы данных Azure для PostgreSQL](quickstart-create-server-database-portal.md);

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Создание правила брандмауэра уровня сервера в hello портал Azure
1. В колонке сервера PostgreSQL hello в разделе Параметры щелкните **безопасности подключения** tooopen hello безопасности подключения колонке базы данных Azure для PostgreSQL hello.

  ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Нажмите кнопку **добавить Мой IP** на панели инструментов hello. Это правило автоматически создаст hello IP-адрес компьютера, воспринимаемое, hello системы Azure.

  ![Портал Azure: нажатие кнопки "Добавить Мой IP-адрес"](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Проверьте свой IP-адрес перед сохранением конфигурации hello. В некоторых ситуациях hello IP-адрес, наблюдается порталом Azure отличается от hello IP-адрес используется при доступе к hello Интернета и серверы Azure. Таким образом может потребоваться toochange hello начальный IP- и конечный IP-toomake правило функции hello должным образом.
Используйте поисковую систему или другие toocheck интерактивное средство собственный IP-адрес (например, поиск Bing «what is my IP»).

  ![Поиск текста "what is my IP" в Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Добавьте дополнительные адресные пространства. В правилах hello для hello базы данных Azure для брандмауэра PostgreSQL можно указать один IP-адрес или диапазон адресов. Если вы хотите toolimit hello правило tooone один IP-адрес, тип hello же адрес в поле hello начальный IP- и конечный IP. Открытие брандмауэра hello включает Администраторы и пользователи базу tooany toologin на hello toowhich сервера PostgreSQL, они имеют допустимые учетные данные.

  ![Портал Azure: правила брандмауэра ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Нажмите кнопку **Сохранить** на hello инструментов toosave этого правила брандмауэра уровня сервера. Дождитесь подтверждения hello, правила брандмауэра toohello hello обновления успешно.

  ![Портал Azure: нажатие кнопки "Сохранить"](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Управлять существующими правилами брандмауэра уровня сервера через портал Azure hello
Повторите шаги toomanage hello hello-правила брандмауэра.
* tooadd hello данного компьютера, нажмите кнопку hello слишком + **добавить Мой IP**. Нажмите кнопку **Сохранить** toosave hello изменения.
* tooadd дополнительные IP-адреса, введите в hello имя правила, начальный IP-адрес и конечный IP-адрес. Нажмите кнопку **Сохранить** toosave hello изменения.
* toomodify существующее правило, щелкните любое из полей правила hello hello и изменения. Нажмите кнопку **Сохранить** toosave hello изменения.
* toodelete существующее правило, нажмите кнопку с многоточием hello [...] и щелкните Delete Удаление hello правило. Нажмите кнопку **Сохранить** toosave hello изменения.

## <a name="next-steps"></a>Дальнейшие действия
- Аналогичным образом, можно создать скрипт слишком[Создание и управление базы данных Azure для правила брандмауэра PostgreSQL, с помощью Azure CLI](howto-manage-firewall-using-cli.md)
- Справку в подключении tooan базы данных Azure для сервера PostgreSQL см [библиотеки подключений к базе данных Azure для PostgreSQL](concepts-connection-libraries.md)
