---
title: "aaaRestore одной таблицы из резервной копии базы данных SQL Azure | Документы Microsoft"
description: "Узнайте, как toorestore один таблицу из резервной копии базы данных SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Как toorestore один таблицу из резервной копии базы данных SQL Azure
Могут возникнуть ситуации, в которых случайно изменены некоторые данные в базе данных SQL, а теперь нужно toorecover hello один изменяемой таблицы. В этой статье описывается, как toorestore одной таблицы в базе данных из одной базы данных SQL hello [автоматического резервного копирования](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Действия по подготовке: переименовать таблицу hello и восстановить копию базы данных hello
1. Определите таблицу hello в нужных tooreplace hello восстановить копию базы данных Azure SQL. Используйте таблицу hello toorename Microsoft SQL Management Studio. Например, переименуйте таблицу hello как &lt;имя таблицы&gt;_old.
   
   > [!NOTE]
   > tooavoid блокируются, убедитесь, что никакие действия, выполняемые для таблицы hello переименовываемый. Если возникают какие-либо проблемы, выполняйте это действие в период обслуживания.
   >

2. Восстановление резервной копии базы данных tooa точки времени, которые должны toorecover toousing hello [восстановитьточки-In_Time](sql-database-recovery-using-backups.md#point-in-time-restore) действия.
   
   > [!NOTE]
   > Имя Hello hello восстановления базы данных будет представлено в формате hello DBName + отметки времени; например **Adventureworks2012_2016-01-01T22-12Z**. Этот шаг не приводит к перезаписи hello имя существующей базы данных на сервере hello. Это средство безопасности, и она предназначена tooallow tooverify hello резервной копии базы данных перед их удалите их из текущей базы данных и присвойте hello восстановить базу данных для использования в рабочей среде.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Копирование таблицы hello из hello восстановления базы данных с помощью средства миграции баз данных SQL hello

1. Загрузите и установите hello [мастер миграции баз данных SQL](https://sqlazuremw.codeplex.com).
2. Откройте мастер миграции баз данных SQL, hello на hello **Выбор процесса** выберите **базы данных в группе анализ/перенос**и нажмите кнопку **Далее**.

   ![Мастер миграции баз данных SQL — выбор процесса](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. В hello **подключения tooServer** диалогового окна поле, примените hello следующие параметры:

   * Имя сервера: **ваш сервер SQL**.
   * Аутентификация: **аутентификация SQL Server**.
   * Имя для входа: **ваше имя для входа**.
   * Пароль: **ваш пароль**.
   * База данных: **главная база данных (список всех баз данных)**.
   
   > [!NOTE]
   > По умолчанию hello мастер сохраняет учетные данные входа. Если этого не нужно делать, установите флажок **Forget Login Information** (Не запоминать учетные данные).
   >
   
     ![Мастер миграции баз данных SQL — выбор источника, шаг 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. В hello **Выбор источника** диалоговое окно, выберите hello восстановить имя базы данных из hello **действия по подготовке** статьи в качестве источника, а затем нажмите кнопку **Далее**.
   
    ![Мастер миграции баз данных SQL — выбор источника, шаг 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. В hello **Выбор объектов** диалоговое окно, выберите hello **выбрать конкретные объекты базы данных** и затем выбрать table(or tables) hello нужных toomigrate toohello целевого сервера.
   ![Мастер миграции баз данных SQL — выбор объектов](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. На hello **Сводка мастера сценариев** щелкните **Да** при появлении запроса о ли вы будете готовы toogenerate сценарий SQL. Также имеется параметр hello toosave hello скрипта TSQL для последующего использования.
   ![Мастер миграции баз данных SQL — сводка мастера сценариев](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. На hello **сводки результатов** щелкните **Далее**.
   ![Мастер миграции баз данных SQL — сводка результатов](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. На hello **соединение с целевым сервером установки** щелкните **подключения tooServer**и введите сведения о hello следующим образом:
   
   * **Имя сервера**: экземпляр целевого сервера.
   * **проверка подлинности:** **проверка подлинности SQL Server**. Введите свои учетные данные.
   * **база данных:** **база данных master (список всех баз данных)**. Этот список будет содержать все hello базы данных на целевом сервере hello.
     
     ![Мастер миграции баз данных SQL — настройка подключения к целевому серверу](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Нажмите кнопку **Connect**выберите целевую базу данных hello, toomove hello таблицы и нажмите кнопку **Далее**. Это должно быть завершено выполнение скрипта ранее созданных hello, и вы увидите, что hello вновь перемещены таблицы копируются toohello целевой базы данных.

## <a name="verification-step"></a>Проверка

- Запросов и тестирования hello вновь скопировать таблицу toomake том, что данные hello без изменений. После подтверждения, ее можно удалить hello переименовать таблицу **действия по подготовке** раздела. (Например, &lt;имя таблицы&gt;_old.)

## <a name="next-steps"></a>Дальнейшие действия
[Общие сведения об автоматическом резервном копировании базы данных SQL](sql-database-automated-backups.md)

