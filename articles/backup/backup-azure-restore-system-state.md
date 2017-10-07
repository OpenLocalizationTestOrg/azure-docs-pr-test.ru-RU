---
title: "Резервного копирования Azure: Tooa восстановления состояния системы Windows Server | Документы Microsoft"
description: "Это пошаговое руководство по восстановлению состояния системы Windows Server из резервной копии в Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>TooWindows восстановления состояния системы сервера

В этой статье объясняется, как хранилище резервных копий состояния системы Windows Server toorestore из служб восстановления Azure. toorestore состояния системы, необходимо иметь резервную копию состояния системы (созданные с помощью инструкции hello в [создайте резервную копию состояния системы](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) и убедитесь, что вы установили hello [последнюю версию hello восстановления Microsoft Azure Агент служб (режим MARS)](http://aka.ms/azurebackup_agent). Восстановление данных состояния системы Windows Server из хранилища службы восстановления Azure состоит из двух этапов:

1. Восстановление состояния системы в виде файлов из службы Azure Backup. При восстановлении состояния системы в виде файлов из службы Azure Backup вы можете:
  * Восстановить состояние системы toohello же сервере, где было выполнено резервное копирование журнала hello, или
  * Восстановление состояния системы файл tooan альтернативного сервера.

2. Примените tooa файлы hello восстановить состояние системы Windows Server.


## <a name="recover-system-state-files-toohello-same-server"></a>Восстановить состояние системы файлы toohello того же сервера.
Hello следующие шаги поясняют, как tooroll обратно к конфигурации Windows Server tooa предыдущее состояние. Последовательное задней tooa конфигурации известны, устойчивое состояние сервера может быть особо важных. Здравствуйте, следующие шаги восстановления hello server состояние системы из хранилища служб восстановления. 

1. Откройте hello **архивации Microsoft Azure** оснастки. Если вы не знаете, где установлена оснастка hello, поиск hello компьютере или сервере **архивации Microsoft Azure**.

    Настольные приложения Hello должны отображаться в результатах поиска hello.

2. Нажмите кнопку **восстановить данные** toostart приветствия мастера.

    ![Восстановить данные](./media/backup-azure-restore-windows-server/recover.png)

3. На hello **Приступая к работе** области, toohello данных hello toorestore того же сервера или компьютера, выберите **этим сервером (`<server name>`)** и нажмите кнопку **Далее**.

    ![Выберите этот сервер toohello параметр toorestore hello данных того же компьютера](./media/backup-azure-restore-system-state/samemachine.png)

4. На hello **выберите режим восстановления** области, выберите **состояния системы** и нажмите кнопку **Далее**.

    ![Обзор файлов](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. В календаре hello в **выберите том и дату** точки выберите восстановления. 

    Можно восстановить данные на любой момент времени. Даты в **полужирным** указать hello доступность по крайней мере одна точка восстановления. После выбора даты, если доступны несколько точек восстановления, выберите hello конкретную точку восстановления из hello **время** раскрывающееся меню.

    ![Том и дата](./media/backup-azure-restore-system-state/select-date.png)

6. После выбора toorestore точки восстановления hello щелкните **Далее**.

    Резервное копирование Azure подключает точку локального восстановления hello и использует его в качестве тома для восстановления.

7. На следующей панели hello, укажите место назначения hello для hello восстановленные файлы состояния системы и нажмите кнопку **Обзор** требуется tooopen проводника поиска hello файлы и папки. Здравствуйте, параметр, **создавать копии, чтобы иметь обе версии**, создает копии отдельных файлов в существующий файл архив состояния системы вместо создания копии hello hello весь архив состояния системы.

    ![Варианты восстановления](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Убедитесь, что сведения hello восстановления на hello **Подтверждение** панели и нажмите **восстановить**.

   ![Выберите действие восстановления hello tooacknowledge восстановления](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Копировать hello *WindowsImageBackup* каталог в hello назначения tooa некритические тома восстановления сервера hello. Как правило hello тома операционной системы Windows — критический том hello.

10. После успешного восстановления hello, выполните действия hello в разделе "hello" [применить восстановить toohello файлы состояния системы Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello процесс восстановления состояния системы.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Восстановить состояние системы файлы tooan альтернативный сервер

Если сервер Windows, поврежден или недоступен, и требуется, чтобы toorestore его tooa устойчивое состояние путем восстановления Здравствуйте состояния системы Windows Server, можно восстановить состояние системы hello поврежденный сервера с другого сервера. Используйте следующие шаги toohello восстановления состояния системы на отдельном сервере hello.  

включает Hello терминология, используемая в этом пошаговом руководстве:

- *Исходный компьютер* — была сделана hello исходной машины, из какой резервный hello и который в данный момент недоступен.
- *Целевой компьютер* — восстанавливаются данные hello toowhich машины hello.
- *Образец хранилища* — hello toowhich хранилище служб восстановления hello *исходной машины* и *целевой компьютер* зарегистрированы. <br/>

> [!NOTE]
> Резервные копии, созданные с одного компьютера не может быть восстановленной tooa компьютере, работающем под управлением более ранней версии операционной системы hello. Например резервные копии, созданные из Windows Server 2016 машины не может быть восстановлена tooWindows Server 2012 R2. Тем не менее возможна hello обратное. Можно использовать резервные копии из Windows Server 2012 R2 toorestore Windows Server 2016.
>

1. Откройте hello **архивации Microsoft Azure** оснастки на hello *целевой компьютер*.
2. Убедитесь, что hello *целевой компьютер* и hello *исходной машины* , зарегистрированных toohello же восстановления службы в хранилище.
3. Нажмите кнопку **восстановить данные** рабочего процесса tooinitiate hello.

    ![Восстановить данные](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Выберите **Другой сервер**

    ![Другой сервер](./media/backup-azure-restore-system-state/anotherserver.png)

5. Укажите файл hello хранилище учетных данных, который соответствует toohello *хранилище образец*. Если файл учетных данных хранилища hello является недопустимым (или истекшим сроком действия), загрузите новый файл учетных данных хранилища из hello *хранилище образец* в hello портал Azure. После задания предоставляется файл учетных данных хранилища hello, отображается hello хранилище служб восстановления, связанных с hello файл учетных данных хранилища.

6. На панели выберите резервный сервер hello выберите hello *исходной машины* из списка отображаемых машины hello.

    ![Список компьютеров](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. В области hello выберите режим восстановления, выберите **состояния системы** и нажмите кнопку **Далее**. 

    ![Поиск](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. На hello календаря в hello **выберите том и дату** точки выберите восстановления. Можно восстановить данные на любой момент времени. Даты в **полужирным** указать hello доступность по крайней мере одна точка восстановления. После выбора даты, если доступны несколько точек восстановления, выберите hello конкретную точку восстановления из hello **время** раскрывающееся меню. 

    ![Поиск элементов](./media/backup-azure-restore-system-state/select-date.png)

9. После выбора toorestore точки восстановления hello щелкните **Далее**.

10. На hello **выберите режим восстановления состояния системы** области, укажите hello место назначения toobe восстановить файлы состояния системы, а затем нажмите кнопку **Далее**.

    ![Шифрование](./media/backup-azure-restore-system-state/recover-as-files.png)

    Здравствуйте, параметр, **создавать копии, чтобы иметь обе версии**, создает копии отдельных файлов в существующий файл архив состояния системы вместо создания копии hello hello весь архив состояния системы.

11. Убедитесь, что сведения hello восстановления на панели hello подтверждения и нажмите кнопку **восстановить**. 

    ![Нажмите кнопку hello hello восстановить кнопки tooconfirm процесс восстановления](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Копировать hello *WindowsImageBackup* каталога tooa некритические тома hello сервере (например D:\). Обычно hello тома операционной системы Windows — критический том hello.

13. процесс восстановления toocomplete hello, используйте следующие hello статьи слишком[применять hello восстановить файлы состояния системы в Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Применение восстановленного состояния системы в Windows Server

После восстановления состояния системы как файлы, используя агент служб восстановления Azure используйте hello архивации данных Windows Server программа tooapply hello восстановить tooWindows состояние системы сервера. Hello программа архивации данных Windows Server уже доступна на сервере hello. Hello следующие шаги поясняют, как tooapply hello восстановить состояние системы.

1. Используйте hello следующими командами tooreboot к серверу в *режиме восстановления служб каталогов*. В командной строке с повышенными привилегиями:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. После перезагрузки hello откройте оснастку hello архивации данных Windows Server. Если вы не знаете, где установлена оснастка hello, поиск hello компьютере или сервере **архивации данных Windows Server**.

    Настольные приложения Hello появится в результатах поиска hello.

3. В оснастке hello, выберите **локальная Архивация**.

    ![Выберите toorestore локальная архивация оттуда.](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. На консоли локальной резервной копии hello в hello **панель действий**, нажмите кнопку **восстановить** tooopen приветствия мастера восстановления.

5. Выберите параметр hello **резервной копии, хранящейся в другом месте**и нажмите кнопку **Далее**.

   ![Выберите другой сервер tooa toorecover](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. При указании типа расположения hello выберите **удаленная общая папка** восстановленные tooanother сервера в случае резервного копирования состояния системы. Если состояние системы было восстановлено локально, выберите **Локальные диски**. 

    ![Выберите ли toorecovery с локального сервера или другой](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Введите путь toohello hello *WindowsImageBackup* каталога, или выберите hello локальный диск, содержащий этот каталог (например, D:\WindowsImageBackup), восстановление в процессе восстановления файлов hello состояния системы, с помощью службы восстановления Azure Службы агента и нажмите кнопку **Далее**.

    ![путь toohello общего файла](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Версия состояния системы выберите hello требуется toorestore и нажмите кнопку **Далее**.

9. В области выберите тип восстановления hello выберите **состояния системы** и нажмите кнопку **Далее**.

10. Расположение hello hello восстановления состояния системы, выберите **исходное расположение**и нажмите кнопку **Далее**.

11. Просмотрите сведения о подтверждении hello, проверьте параметры перезагрузки hello и нажмите кнопку **восстановить** tooapplly hello восстановленных файлов состояния системы.

    ![hello запуска восстановления состояния системы файлов](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Специальные рекомендации для восстановления состояния системы на сервере Active Directory

Резервная копия состояния системы включает данные Active Directory. Используйте следующие шаги toorestore доменные службы Active Directory (AD DS) из текущего состояния tooa предыдущего состояния hello.

1. Перезапустите контроллер домена hello в режиме восстановления служб каталогов (DSRM).
2. Выполните действия hello [здесь](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover командлеты toouse архивации данных Windows Server AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Устранение неполадок при сбое восстановления состояния системы

Если hello предыдущий процесс применения состояния системы не завершается успешно, используйте toorecover hello среды восстановления Windows (Win RE) Windows Server. Hello следующие шаги поясняют, как с помощью Win RE toorecover. Используйте этот вариант, только если Windows Server не загружается нормально после восстановления состояния системы. Привет, следуйте процедуре стирает данные систем, соблюдайте осторожность. 

1. Загрузка сервера Windows hello среды восстановления Windows (Win RE).

2. Выберите Устранение неполадок из трех доступных вариантов hello.

    ![Открытие меню](./media/backup-azure-restore-system-state/winre-1.png)

3. Из hello **Дополнительные параметры** выберите **командной строки** и укажите имя пользователя администратора сервера hello и пароль.

   ![Открытие меню](./media/backup-azure-restore-system-state/winre-2.png)

4. Укажите имя пользователя администратора сервера hello и пароль.

    ![Открытие меню](./media/backup-azure-restore-system-state/winre-3.png)

5. При открытии hello командной строки с правами администратора, запустите следующие версии резервного копирования состояния системы hello tooget команды.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Получение версий резервного копирования состояния системы](./media/backup-azure-restore-system-state/winre-4.png)

6. Запустите следующие команды tooget hello все тома в резервной копии hello.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Получение версий резервного копирования состояния системы](./media/backup-azure-restore-system-state/winre-5.png)

7. Hello следующая команда восстанавливает все тома, которые являются частью hello резервной копии состояния системы. Обратите внимание, что этот шаг восстанавливает только hello критические тома, которые являются частью hello состояния системы. Все несистемные данные удаляются.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Получение версий резервного копирования состояния системы](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Дальнейшие действия
* Теперь после восстановления файлов и папок можно [управлять резервными копиями](backup-azure-manage-windows-server.md).
