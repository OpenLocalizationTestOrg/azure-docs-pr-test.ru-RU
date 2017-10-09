---
title: "aaaBack копирование Exchange server tooAzure резервной копии с Azure Backup Server | Документы Microsoft"
description: "Узнайте, как резервное копирование tooback копирование tooAzure сервера Exchange, используя сервер резервного копирования Azure"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a>Резервное копирование Exchange server tooAzure резервной копии с сервера резервного копирования Azure
В этой статье описывается как tooback сервера архивации Microsoft Azure (MABS) tooconfigure копирование tooAzure Microsoft Exchange server.  

## <a name="prerequisites"></a>Предварительные требования
Прежде чем продолжить, убедитесь, что Сервер резервного копирования Azure [установлен и подготовлен](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>Агент защиты MABS
агент защиты MABS tooinstall hello на hello Exchange server, выполните следующие действия.

1. Убедитесь, что hello брандмауэры настроены правильно. В разделе [Настройка исключений брандмауэра для агента hello](https://technet.microsoft.com/library/Hh758204.aspx).
2. Установите агент hello на сервере Exchange hello, щелкнув **управления > агенты > установить** в консоли администрирования MABS. В разделе [установке агента защиты MABS hello](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) подробное описание шагов.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Создайте группу защиты для hello Exchange server
1. В hello MABS консоль, нажмите кнопку **защиты**и нажмите кнопку **New** на ленте tooopen hello средство hello **создания новой группы защиты** мастера.
2. На hello **приветствия** экран приветствия мастера выберите **Далее**.
3. На hello **Выбор типа группы защиты** выберите **серверы** и нажмите кнопку **Далее**.
4. Базы данных выберите hello Exchange server tooprotect и нажмите кнопку **Далее**.

   > [!NOTE]
   > Если необходимо обеспечить защиту Exchange 2013, проверьте hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    В следующем примере hello база данных Exchange 2010 hello выбрана.

    ![Выберите членов группы](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Выбор метода защиты данных hello.

    Имя группы защиты hello и выберите оба hello следующие параметры:

   * «Мне нужна краткосрочная защита с использованием диска»;
   * «Мне нужна оперативная защита».
6. Щелкните **Далее**.
7. Выберите hello **целостности данных toocheck запустить программу Eseutil** Если требуется toocheck hello целостность баз данных Exchange Server hello.

    После выбора этого параметра, проверки согласованности резервного копирования будут выполняться на MABS tooavoid hello ввода-вывода трафика, создаваемого при выполнении hello **eseutil** команду на сервере Exchange hello.

   > [!NOTE]
   > toouse этот параметр, необходимо скопировать hello Ese.dll и Eseutil.exe каталога C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin toohello файлов на сервере MAB hello. В противном случае запускается hello следующая ошибка:  
   > ![ошибка Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. Щелкните **Далее**.
9. Выберите hello базы данных для **резервного копирования**, а затем нажмите кнопку **Далее**.

   > [!NOTE]
   > Если не выбрать «Полное резервное копирование» хотя бы для одной копии базы данных в группе обеспечения доступности баз данных, журналы не будут усечены.
   >
   >
10. Настройка цели hello для **краткосрочное резервное копирование**, а затем нажмите кнопку **Далее**.
11. Просмотрите hello места на диске и нажмите кнопку **Далее**.
12. Выберите время hello в какой hello MAB сервер создаст hello начальной репликации и нажмите кнопку **Далее**.
13. Выберите параметры проверки согласованности hello и нажмите кнопку **Далее**.
14. Выберите базу данных hello требуется tooback копирование tooAzure и нажмите кнопку **Далее**. Например:

    ![Выбор оперативной защиты данных](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. Определение расписания hello для **резервного копирования Azure**, а затем нажмите кнопку **Далее**. Например:

    ![Выбор расписания оперативного резервного копирования](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Обратите внимание, что точки оперативного восстановления создаются на основании точек быстрого полного восстановления. Таким образом, необходимо запланировать hello точку восстановления после hello времени, указанный для hello express точки полного восстановления.
    >
    >
16. Настроить политику хранения hello для **резервного копирования Azure**, а затем нажмите кнопку **Далее**.
17. Выберите параметр оперативной репликации и нажмите кнопку **Далее**.

    При наличии больших баз данных может занять много времени для резервного копирования toobe с начальной hello создания сети hello. tooavoid эту проблему, можно создать автономный архив.  

    ![Выбор политики оперативного хранения](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Подтверждение параметров hello и нажмите кнопку **создать группу**.
19. Нажмите кнопку **Закрыть**

## <a name="recover-hello-exchange-database"></a>Восстановление базы данных Exchange hello
1. Нажмите кнопку toorecover базы данных Exchange, **восстановления** в консоли администрирования MABS hello.
2. Найдите hello базы данных Exchange, которые должны toorecover.
3. Выберите точку восстановления из hello *время восстановления* раскрывающегося списка.
4. Нажмите кнопку **восстановить** toostart hello **мастер восстановления**.

Для точек оперативного восстановления существует пять типов восстановления:

* **Восстановить toooriginal расположение сервера Exchange:** hello данные будут восстановленные toohello исходного сервера Exchange.
* **Восстановление базы данных tooanother на сервере Exchange Server:** hello данные будут tooanother восстановленной базы данных на другой сервер Exchange server.
* **Восстановление базы данных восстановления tooa:** hello данные будут tooan восстановленной базы данных Exchange восстановления (RDB).
* **Копирование tooa сетевой папки:** hello данные будут восстановленные tooa сетевую папку.
* **Скопируйте tootape:** Если у вас есть ленточную библиотеку или изолированный ленточный накопитель, присоединенных и не настроен на MABS hello точки восстановления будут скопированы tooa свободная лента.

    ![Выбор оперативной репликации](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Часто задаваемые вопросы о службе архивации Azure](backup-azure-backup-faq.md)
