---
title: "aaaManage Azure резервных хранилищ и серверов Azure с помощью hello классической модели развертывания | Документы Microsoft"
description: "Используйте этот учебник toolearn как хранилищ toomanage резервного копирования Azure и серверы."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Управление хранилищами резервного копирования Azure и серверами с помощью hello классической модели развертывания
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](backup-azure-manage-windows-server.md)
> * [Классический](backup-azure-manage-windows-server-classic.md)
>
>

В этой статье вы найдете Обзор задачи управления резервным копированием hello, доступные через hello классический портал Azure и агент службы архивации Microsoft Azure hello.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

> [!IMPORTANT]
> Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии. Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md). Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.<br/> После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ. **К 1 ноября 2017 года**:
>- Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.
>- Вы не будет возможности tooaccess данные резервной копии hello классического портала. Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.
>

## <a name="management-portal-tasks"></a>Задачи на портале управления
1. Войдите в toohello [портала управления](https://manage.windowsazure.com).
2. Нажмите кнопку **службы восстановления**, затем щелкните имя hello страницы быстрый запуск резервного хранилища tooview hello.

    ![Службы восстановления](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

Выбрав параметры hello hello верхней части страницы быстрого запуска hello, вы увидите hello доступных задач управления.

![Управление вкладками](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>Панель мониторинга
Выберите **мониторинга** toosee hello Общие сведения об использовании для сервера hello. Hello **Общие сведения об использовании** включает в себя:

* toocloud зарегистрировано Hello количество серверов Windows
* число Hello Azure виртуальные машины, защищенные в облаке
* Hello общее занятого хранилища в Azure
* состояние последних заданий Hello

Внизу hello hello панели мониторинга можно выполнять следующие задачи hello:

* **Управление сертификатами** — Если сертификат был сервером используется tooregister hello, а затем использовать этот сертификат tooupdate hello. При использовании учетных данных хранилища не используйте пункт **Управление сертификатом**.
* **Удалить** -удалений hello текущего резервного хранилища. Если резервное хранилище больше не используется, ее можно удалить toofree места хранения. **Удалить** доступна только после удаления из хранилища hello все зарегистрированные серверы.

![Задачи панели мониторинга архивации](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>Зарегистрированные элементы
Выберите **зарегистрированные элементы** зарегистрировать имена hello tooview hello серверов, которые являются toothis хранилища.

![Зарегистрированные элементы](./media/backup-azure-manage-windows-server-classic/registered-items.png)

Hello **тип** фильтра по умолчанию tooAzure виртуальной машины. Выберите имена hello tooview hello серверов, которые являются хранилище зарегистрированного toothis **Windows server** из hello раскрывающемся меню.

Здесь можно выполнять следующие задачи hello.

* **Разрешить повторную регистрацию** — при выборе этого параметра для сервера, можно использовать hello **мастер регистрации** hello локальной службы архивации Microsoft Azure агента tooregister hello Server с резервным хранилищем hello еще раз . Может потребоваться toore регистрацию из-за ошибки tooan в hello сертификата или если сервер имеет toobe перестроен.
* **Удалить** -удаляет сервер из резервного хранилища hello. Немедленное удаление всех hello хранимых данных, связанных с сервером hello.

    ![Задачи зарегистрированных элементов](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>Защищенные элементы
Выберите **защищенные элементы** tooview hello элементы, которые были скопированы с серверов hello.

![Защищенные элементы](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>Настройка
Из hello **Настройка** вкладку, можно выбрать параметр избыточности хранилища соответствующие hello. Hello время tooselect hello хранилища избыточности лучше сразу же после создания хранилища, а также перед любой машин, зарегистрированных tooit.

> [!WARNING]
> После элемента хранилища зарегистрированных toohello, параметр избыточности хранилища hello заблокирован и не может быть изменено.
>
>

![Настройка](./media/backup-azure-manage-windows-server-classic/configure.png)

Дополнительные сведения см. в статье об [избыточности хранилища](../storage/common/storage-redundancy.md).

## <a name="microsoft-azure-backup-agent-tasks"></a>Задачи агента службы архивации Microsoft Azure
### <a name="console"></a>Консоль
Откройте hello **агента службы архивации Microsoft Azure** (его можно найти путем поиска свой компьютер и *архивации Microsoft Azure*).

![Агент службы архивации](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

Из hello **действия** найти по адресу hello правой части консоли hello резервного копирования можно выполнять следующие задачи по управлению hello:

* Регистрация сервера
* Создание расписания архивации
* Выполнить архивацию сейчас
* Изменить свойства

![Действия в консоли агента](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> слишком**восстановить данные**, в разделе [восстановить файлы tooa Windows server или клиентским компьютером Windows](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a>Изменение существующего архива
1. В агенте службы архивации Microsoft Azure hello щелкните **планирования резервного копирования**.

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. В hello **мастер планирования резервного копирования** оставить hello **toobackup элементы или время изменения производятся** флажок и нажмите кнопку **Далее**.

    ![Изменение расписания резервного копирования](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Если вы tooadd или изменить элементы на hello **tooBackup выбрать элементы** откройте **добавить элементы**.

    Можно также задать **параметры исключения** на этой странице приветствия мастера. Если требуется tooexclude файлы или типы файлов hello процедура добавления [параметры исключения](#exclusion-settings).
4. Выберите hello файлы и папки tooback вверх и щелкните **хорошо**.

    ![Добавить элементы](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Укажите hello **расписание резервного копирования** и нажмите кнопку **Далее**.

    Вы можете запланировать ежедневное (не более трех раз в день) или еженедельное резервное копирование.

    ![Выбор расписания резервного копирования](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Задание расписания резервного копирования hello подробно рассматривается в этом [статьи](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. Выберите hello **политики хранения** hello резервной копии и нажмите кнопку **Далее**.

    ![Определение политики хранения](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. На hello **Подтверждение** экрана Просмотр сведений об hello и нажмите кнопку **Готово**.
8. После завершения работы приветствия мастера создания hello **расписание резервного копирования**, нажмите кнопку **закрыть**.

    После изменения защиты, можно проверить, правильно инициируют резервных копий с переходом toohello **заданий** вкладку и подтверждения того, что изменения отражаются в hello задания резервного копирования.

### <a name="enable-network-throttling"></a>Включение регулирования сети
агент Azure Backup Hello предоставляет вкладку регулирование, позволяющий toocontrol использование пропускной способности сети при передаче данных. Этот элемент управления может пригодиться, если вам требуется tooback копирование данных в рабочее время, но не требуется toointerfere hello процесс резервного копирования с другими Интернет-трафика. Регулирование данных передачи применяется tooback копирование и восстановление действий.  

Регулирование tooenable:

1. В hello **агента резервного копирования**, нажмите кнопку **изменить свойства**.
2. Выберите hello **включить регулирования для операций резервного копирования использование пропускной способности Интернета** флажок.

    ![Регулирование сети](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. После включения регулирования, укажите допустимый пропускной способности, для передачи во время резервного копирования данных hello **рабочие часы** и **нерабочие часы**.

    значения Hello пропускной способности начинаются с 512 килобайт в секунду (Кбит/с) и можно перейти вверх too1023 мегабайт в секунду (Мбит/с). Можно также назначить hello начала и окончания для **рабочие часы**, и какие дни недели hello считаются рабочих дней. время Hello за пределами указанных рабочих часов hello — считаются toobe нерабочего времени.
4. Нажмите кнопку **ОК**.

## <a name="exclusion-settings"></a>параметры исключений
1. Откройте hello **агента службы архивации Microsoft Azure** (его можно найти путем поиска свой компьютер и *архивации Microsoft Azure*).

    ![Открытие агента службы архивации](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. В агенте службы архивации Microsoft Azure hello щелкните **планирования резервного копирования**.

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. В мастер планирования резервного копирования hello оставьте hello **toobackup элементы или время изменения производятся** флажок и нажмите кнопку **Далее**.

    ![Изменение расписания](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. Щелкните **Параметры исключений**.

    ![Выберите элементы tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. Щелкните **Добавить исключение**.

    ![Добавление исключений](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Выберите расположение hello и затем нажмите кнопку **ОК**.

    ![Выбор расположения для исключения](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Добавлять расширение файла hello в hello **тип файла** поля.

    ![Исключение по типу файлов](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    Добавление расширения .mp3

    ![Пример типа файлов](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd другое расширение, нажмите кнопку **Добавление исключаемых** и введите другое расширение имени файла (Добавление расширения .jpeg).

    ![Другой пример типа файла](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. После добавления всех расширений hello, нажмите кнопку **ОК**.
9. Продолжайте hello мастер планирования резервного копирования, нажав кнопку **Далее** до hello **страница подтверждения**, нажмите кнопку **Готово**.

    ![Подтверждение исключения](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Восстановление Windows Server или клиента Windows из Azure](backup-azure-restore-windows-server.md)
* toolearn Дополнительные сведения об архивации Azure в разделе [Обзор резервного копирования Azure](backup-introduction-to-azure-backup.md)
* Посетите hello [форуме резервного копирования Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
