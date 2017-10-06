---
title: "aaaHow tooRestore сервера в базе данных Azure для MySQL | Документы Microsoft"
description: "В этой статье описывается как toorestore сервера в базе данных Azure для использования MySQL hello портал Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>Здравствуйте как tooBackup и восстановления сервера в базе данных Azure для MySQL с помощью портала Azure

## <a name="backup-happens-automatically"></a>Архивация выполняется автоматически
При использовании базы данных Azure для MySQL, hello служба базы данных автоматически создает резервную копию службы hello каждые 5 минут. 

Hello резервные копии доступны в течение 7 дней, при использовании базового уровня и на 35 дней при использовании стандартного уровня. Дополнительные сведения см. в разделе [Параметры и производительность базы данных Azure для MySQL: возможности разных уровней служб](concepts-service-tiers.md).

С помощью этой функции автоматического резервного копирования вы можете восстановить сервер hello и все его базы данных на новый сервер tooan ранее в определенный момент.

## <a name="restore-in-hello-azure-portal"></a>Восстановление в hello портал Azure
Базы данных Azure для MySQL позволяет toorestore hello server задней tooa точки на время и в новой копии tooa сервера hello. Этот новый toorecover сервера можно использовать данные. 

Например если таблица была случайно удалены в полдень в настоящее время можно восстановить время toohello только до полудня и получить hello отсутствует таблицы и данные из этой новой копии сервера hello.

Hello следующее моментов hello образец server tooa времени:

1. Вход в hello [портал Azure](https://portal.azure.com/)

2. Найдите сервер базы данных Azure для MySQL. Выберите в левой области hello **все ресурсы**, затем выберите сервер из списка hello.

3.  Щелкните hello верхней части колонки Обзор сервера hello, **восстановить** на панели инструментов hello. Открывает колонку восстановления Hello.
![Нажатие кнопки "Восстановить"](./media/howto-restore-server-portal/click-restore-button.png)

4. Заполните форму восстановления hello hello необходимые сведения:

- **(UTC) точку восстановления**: с помощью выбора даты hello и выбор времени выберите в момент toorestore для. Hello указано в формате UTC, поэтому вы скорее всего, потребуется tooconvert hello местное время в формате UTC.
- **Восстановление сервера toonew**: укажите имя toorestore hello существующий сервер в новый сервер.
- **Расположение**: Выбор региона hello автоматически заполняет регион сервера hello источника и не может быть изменено.
- **Ценовая категория**: hello ценовой уровень выбора автоматически заполняет hello одинаковые цены уровня hello и исходный сервер и здесь нельзя изменить. 
![Восстановление до точки во времени](./media/howto-restore-server-portal/pitr-restore.png)

5. Нажмите кнопку **ОК** toorestore hello server toorestore tooa моменту времени. 

6. После завершения восстановления hello, найдите hello новый сервер, который был создан приветствия tooverify базы данных были восстановлены должным образом.

## <a name="next-steps"></a>Дальнейшие действия
- [Библиотеки подключений для базы данных Azure для MySQL](concepts-connection-libraries.md)