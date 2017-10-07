---
title: "Как сервер в базе данных Azure для PostgreSQL tooRestore | Документы Microsoft"
description: "В этой статье описывается как toorestore сервера в базе данных Azure для использования PostgreSQL hello портал Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a>Как tooBackup и восстановления сервера в базе данных Azure для использования PostgreSQL hello портал Azure

## <a name="backup-happens-automatically"></a>Архивация выполняется автоматически
При использовании базы данных Azure для PostgreSQL, hello служба базы данных автоматически создает резервную копию службы hello каждые 5 минут. 

Hello резервные копии доступны в течение 7 дней, при использовании базового уровня и на 35 дней при использовании стандартного уровня. Дополнительные сведения см. в разделе [Параметры и производительность базы данных Azure для PostgreSQL: возможности разных уровней служб](concepts-service-tiers.md).

С помощью этой функции автоматического резервного копирования вы можете восстановить сервер hello и все его базы данных на новый сервер tooan ранее в определенный момент.

## <a name="restore-in-hello-azure-portal"></a>Восстановление в hello портал Azure
Базы данных Azure для PostgreSQL позволяет toorestore hello server задней tooa точки на время и в новой копии tooa сервера hello. Этот новый toorecover сервера можно использовать данные. 

Например если таблица была случайно удалены в полдень в настоящее время можно восстановить время toohello только до полудня и получить hello отсутствует таблицы и данные из этой новой копии сервера hello.

Hello следующее моментов hello образец server tooa времени:
1. Вход в hello [портал Azure](https://portal.azure.com/)
2. Найдите сервер базы данных Azure для PostgreSQL. В hello портал Azure, щелкните **все ресурсы** из hello левого меню и введите имя hello, таких как **mypgserver 20170401**, toosearch для существующего сервера. Щелкните имя сервера hello, перечисленные в результатах поиска hello. Hello **Обзор** страница сервера открывает и предоставляет параметры для дальнейшей настройки.

   ![Портал Azure — поиск toolocate сервера](media/postgresql-howto-restore-server-portal/1-locate.png)

3. Щелкните hello верхней части колонки Обзор сервера hello, **восстановить** на панели инструментов hello. Открывает колонку восстановления Hello.

   ![База данных Azure для PostgreSQL: колонка "Восстановление" в колонке "Обзор"](./media/postgresql-howto-restore-server-portal/2_server.png)

4. Заполните форму восстановления hello hello необходимые сведения:

   ![База данных Azure для PostgreSQL: информация для восстановления ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **Точка восстановления**: выберите в момент, выполняемой до hello сервер был изменен
  - **Целевой сервер**: Введите имя нового сервера требуется toorestore для
  - **Расположение**: не удается выбрать область hello, по умолчанию его значение совпадает hello исходного сервера
  - **Ценовая категория**: это значение нельзя изменить при восстановлении сервера. Это то же, что hello исходного сервера. 

5. Нажмите кнопку **ОК** toorestore hello server toorestore tooa моменту времени. 

6. После завершения выполнения hello восстановления, найдите hello новый сервер, который создается приветствия tooverify восстановления данных должным образом.

## <a name="next-steps"></a>Дальнейшие действия
- [Библиотеки подключений для базы данных Azure для PostgreSQL](concepts-connection-libraries.md)
