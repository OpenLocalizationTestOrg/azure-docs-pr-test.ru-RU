---
title: "aaaCreate и управления базой данных Azure для MySQL правила брандмауэра, с помощью hello портал Azure | Документы Microsoft"
description: "Создание и управление для MySQL правила брандмауэра, с помощью портала Azure hello базы данных Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Создание и управление для MySQL правила брандмауэра, с помощью портала Azure hello базы данных Azure
Правила брандмауэра уровня сервера включите tooaccess администраторы базы данных Azure для сервера MySQL из указанный IP-адрес или диапазон IP-адресов. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Создание правила брандмауэра уровня сервера в hello портал Azure

1. В колонке сервера MySQL hello в разделе Параметры щелкните **безопасности подключения** tooopen hello безопасности подключения колонке hello базы данных Azure для MySQL.

   ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Нажмите кнопку **добавить Мой IP** на toocreate инструментов hello правило с hello IP-адрес компьютера, с точки зрения hello системы Azure.

   ![Портал Azure: нажатие кнопки "Добавить Мой IP-адрес"](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Проверьте свой IP-адрес перед сохранением конфигурации hello. В некоторых ситуациях hello IP-адрес, наблюдается порталом Azure отличается от hello IP-адрес используется при доступе к hello Интернета и серверы Azure. Таким образом может потребоваться toochange hello начальный IP- и конечный IP-toomake правило функции hello должным образом.

   Используйте поисковую систему или другие интерактивное средство toocheck IP-адреса (например, выполните поиск «what is my IP-адрес»).

   ![Поиск текста what is my IP в Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Добавьте дополнительные адресные пространства. В правилах hello для hello базы данных Azure для MySQL брандмауэра можно указать один IP-адрес или диапазон адресов. Если вы хотите toolimit hello правило tooone один IP-адрес, тип hello же адрес в поле hello начальный IP- и конечный IP. Открытие брандмауэра hello позволяет Администраторы и пользователи tooaccess любой базы данных на hello toowhich MySQL server, они имеют допустимые учетные данные.

   ![Портал Azure: правила брандмауэра ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Нажмите кнопку **Сохранить** на hello инструментов toosave этого правила брандмауэра уровня сервера. Дождитесь подтверждения hello, правила брандмауэра toohello hello обновления успешно.

   ![Портал Azure: нажатие кнопки "Сохранить"](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Управлять существующими правилами брандмауэра уровня сервера через портал Azure hello
Повторите шаги toomanage hello hello-правила брандмауэра.
* tooadd hello данного компьютера, нажмите кнопку **+ добавить Мой IP-адрес**.
* tooadd дополнительные IP-адреса, введите в hello **имя ПРАВИЛА**, **НАЧАЛЬНЫЙ IP-**, и **конечным IP**.
* toomodify существующее правило, щелкните любое из полей правила hello hello и изменения.
* правило toodelete существующего, нажмите кнопку с многоточием hello [...] и нажмите кнопку **удалить**.
* Нажмите кнопку **Сохранить** toosave hello изменения.

## <a name="next-steps"></a>Дальнейшие действия
- Справку в подключении tooan базы данных Azure для MySQL server в разделе [библиотеки подключений к базе данных Azure для MySQL](./concepts-connection-libraries.md)
