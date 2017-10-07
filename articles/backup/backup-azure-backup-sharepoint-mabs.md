---
title: "tooback сервера aaaUse резервное копирование фермы SharePoint tooAzure | Документы Microsoft"
description: "Используйте tooback Azure резервное копирование и восстановление данных SharePoint. Эта статья содержит сведения tooconfigure hello фермы SharePoint, чтобы необходимые данные могут храниться в Azure. Защищенные данные SharePoint можно восстановить с диска или из Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Резервное копирование фермы SharePoint tooAzure
Резервное копирование SharePoint фермы tooMicrosoft Azure с помощью сервера архивации Microsoft Azure (MABS) в много hello так же, резервное копирование других источников данных. Резервное копирование Azure обеспечивает гибкость в toocreate hello расписание резервного копирования ежедневно, еженедельно, ежемесячно или ежегодно точки резервного копирования и предоставляет параметры политики хранения для различных точках рабочего процесса резервного копирования. Он также предоставляет hello возможность toostore локальный диск копий для целей быстрое время восстановления (RTO) и toostore копирует tooAzure экономичной, долгосрочного хранения.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Поддерживаемые версии SharePoint и соответствующие сценарии защиты
Azure Backup для DPM поддерживает следующие сценарии hello:

| Рабочая нагрузка | Версия | Развертывание SharePoint | Защита и восстановление |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0 |SharePoint разворачивается как физический сервер или виртуальная машина Hyper-V/VMware  <br> -------------- <br> SQL AlwaysOn | Параметры восстановления фермы SharePoint: ферма, база данных, файл или элемент списка для восстановления из точек восстановления диска.  Восстановление фермы и базы данных из точек восстановления Azure. |

## <a name="before-you-start"></a>Перед началом работы
Существует несколько моментов, которые необходимо tooconfirm перед выполнением резервного копирования tooAzure фермы SharePoint.

### <a name="prerequisites"></a>Предварительные требования
Прежде чем продолжить, убедитесь, что [установлен и подготовленные hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect рабочих нагрузок.

### <a name="protection-agent"></a>Агент защиты
агент защиты Hello должен устанавливаться на сервере hello, на котором выполняется SharePoint, hello серверов, работающих под управлением SQL Server и другие серверы, которые являются частью фермы SharePoint hello. Дополнительные сведения о том, как tooset hello агента защиты, в разделе [установки агента защиты](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Hello одно исключение — установить агент hello только на одном веб-сервере переднего плана (WFE). DPM требуется агент hello на один tooserve сервера WFE только в качестве точки входа hello для защиты.

### <a name="sharepoint-farm"></a>Ферма SharePoint
Для каждых 10 млн элементов в ферме hello должен быть по крайней мере 2 ГБ дискового пространства на томе hello, где находится папка MABS hello. Эта память нужна для создания каталога. MABS toorecover определенных элементов (семейств веб-сайтов, сайты, списки, библиотеки документов, папки, отдельные документы и элементы списка) создания каталогов создает список hello URL-адресов, которые содержатся в каждой базе данных контента. Можно просмотреть список hello URL-адреса в hello hello восстанавливаемый элемент области **восстановления** области консоли администратора MABS задач.

### <a name="sql-server"></a>SQL Server
MABS запускается от имени учетной записи LocalSystem. tooback копирование баз данных SQL Server MABS должен прав системного администратора для этой учетной записи для hello сервера, на котором выполняется SQL Server. Задать NT AUTHORITY\SYSTEM слишком*sysadmin* hello сервера, на котором выполняется SQL Server, прежде чем создать его резервную копию.

Если ферма SharePoint hello баз данных SQL Server, которые настроены с псевдонимами SQL Server, установите клиентские компоненты SQL Server hello на hello интерфейсный веб-сервер, который будет защищать MABS.

### <a name="sharepoint-server"></a>SharePoint Server
Производительность системы зависит от многих факторов, включая размер фермы SharePoint. Как правило, для защиты фермы SharePoint объемом 25 ТБ используется один сервер MABS.

### <a name="whats-not-supported"></a>Что не поддерживается
* Защита фермы SharePoint с помощью MABS не охватывает индексы поиска или базы данных службы приложений. Необходимо будет tooconfigure hello защиты этих баз данных отдельно.
* MABS не поддерживает резервное копирование баз данных SharePoint SQL Server, размещенных в общих хранилищах на масштабируемом файловом сервере.

## <a name="configure-sharepoint-protection"></a>Настройка защиты SharePoint
Прежде чем использовать MABS tooprotect SharePoint, необходимо настроить hello модуля записи VSS SharePoint (службы модуля записи WSS) с помощью **ConfigureSharePoint.exe**.

Можно найти **ConfigureSharePoint.exe** в папке \bin hello [путь установки MABS] на интерфейсном веб-сервере hello. Это средство предоставляет hello агент защиты с hello учетные данные для фермы SharePoint hello. Файл нужно распаковать на одном интерфейсном веб-сервере. Если у вас таких серверов несколько, выберите один из них для настройки группы защиты.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>hello tooconfigure служба модуля записи VSS SharePoint
1. На сервере WFE hello, в командной строке перейти слишком \bin\ [расположение установки MABS]
2. Введите ConfigureSharePoint -EnableSharePointProtection.
3. Введите учетные данные администратора фермы hello. Эта учетная запись должна быть членом hello локальной группы администраторов на сервере WFE hello. Если администратор фермы hello не hello grant локального администратора, следующие разрешения на сервере WFE hello:
   * Предоставление hello WSS_Admin_WPG полный доступ toohello DPM папку группы (% Program Files%\Microsoft Azure Backup\DPM).
   * Предоставьте hello WSS_Admin_WPG группы доступа на чтение toohello DPM реестра (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Вам потребуется toorerun ConfigureSharePoint.exe при каждом изменении в hello учетные данные администратора фермы SharePoint.
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a>Архивация фермы SharePoint с помощью MABS
После настройки MABS и hello фермы SharePoint, как описано ранее SharePoint может быть защищен MABS.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect фермы SharePoint
1. Из hello **защиты** щелкните вкладку hello консоли администратора MABS **New**.
    ![Вкладка создания защиты](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. На hello **Выбор типа группы защиты** страница hello **создания новой группы защиты** мастера, выберите **серверы**, а затем нажмите кнопку **Далее** .

    ![Выберите тип группы защиты](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. На hello **Выбор членов группы** экрана, выберите hello флажок для сервера SharePoint hello tooprotect и щелкните **Далее**.

    ![Выберите членов группы](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > С установленным агентом защиты hello вы увидите hello сервера в мастере hello. Также сервер MABS отображает его структуру. Поскольку вы запустили ConfigureSharePoint.exe, MABS взаимодействует со службой модуля записи VSS SharePoint hello и все соответствующие базы данных SQL Server и распознает hello структура фермы SharePoint, hello связанных баз данных содержимого и все соответствующие элементы.
   >
   >
4. На hello **Выбор метода защиты данных** введите имя hello hello **группы защиты**и выберите предпочитаемом *методы защиты*. Щелкните **Далее**.

    ![Выберите метод защиты данных](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > метод защиты диска Hello помогает toomeet короткое время восстановления целей.
   >
   >
5. На hello **Выбор краткосрочных целей** выберите предпочитаемом **диапазон хранения** и определить, когда требуется toooccur резервных копий.

    ![Выберите краткосрочные цели](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > Так как восстановление чаще всего требуется для данных, которые меньше пяти дней, мы выбранные диапазон хранения равен пяти дней на диске и гарантирует, что эта резервная копия hello происходит в непроизводственной часы, в этом примере.
   >
   >
6. Просмотрите hello пула хранения дискового пространства, выделенного для группы защиты hello, а затем нажмите кнопку **Далее**.
7. Для каждой группы защиты MABS выделяет toostore места на диске и управление репликами. На этом этапе MABS необходимо создать копию hello выбранных данных. Выберите способ и время создания реплика hello и нажмите кнопку **Далее**.

    ![Выберите метод создания реплики](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > убедиться, что сетевой трафик не устаревший toomake выберите время вне рабочих часов.
   >
   >
8. MABS гарантирует целостность данных путем выполнения проверки согласованности в реплике hello. Доступны два параметра. Можно определить проверяет согласованность toorun расписание или DPM запустить проверку согласованности автоматически hello реплики всякий раз, когда он становится несогласованной. Выберите желаемый параметр и нажмите кнопку **Далее**.

    ![Проверка согласованности](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. На hello **укажите оперативной защиты данных** выберите hello фермы SharePoint будет tooprotect и нажмите кнопку **Далее**.

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. На hello **укажите расписание оперативной архивации** выберите предпочтительное расписание и нажмите кнопку **Далее**.

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > MABS обеспечивает максимальную два tooAzure ежедневных резервных копий из hello, а затем доступны последние точки для резервного копирования диска. Резервное копирование Azure можно также управлять hello объем пропускной способности глобальной сети, который может использоваться для архивации в пиковые и непиковые часы с помощью [регулирование сети резервного копирования Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).
    >
    >
11. В зависимости от расписания архивации hello, выбранного на hello **указание политики оперативного хранения** страницы выберите hello политику хранения для резервного копирования точек ежедневно, еженедельно, ежемесячно и ежегодно.

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > MABS использует трехуровневую схему хранения, которая позволяет выбирать разную политику хранения для разных точек резервного копирования.
    >
    >
12. Аналогичные toodisk реплики точки начальную ссылку должен toobe, созданные в Azure. Выберите ваш предпочтительный вариант toocreate tooAzure начальной резервной копии и нажмите кнопку **Далее**.

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Просмотрите выбранные параметры на hello **Сводка** и нажмите кнопку **создать группу**. После создания группы защиты hello, вы увидите сообщение об успешном выполнении.

    ![Сводка](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a>Восстановление элемента SharePoint с диска с помощью MABS
В следующем примере hello, hello *элемент восстановление SharePoint* был случайно удален и требуется восстановить toobe.
![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Откройте hello **консоли администрирования DPM**. Показаны все ферм SharePoint, которые защищены с помощью DPM в hello **защиты** вкладки.

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. toorecover hello toobegin элемента, выберите hello **восстановления** вкладки.

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. Чтобы найти *элемент восстановления SharePoint* , можно использовать поиск на основе подстановки в пределах диапазона точек восстановления.

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Выберите точку восстановления, соответствующих hello из результатов поиска hello, щелкните правой кнопкой мыши элемент hello и выберите **восстановить**.
5. Также можно просматривать различные точки восстановления и выбрать базу данных или элемент toorecover. Выберите **даты > времени восстановления**и выберите правильный hello **базы данных > фермы SharePoint > точка восстановления > элемент**.

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Щелкните правой кнопкой мыши элемент hello, а затем выберите **восстановить** tooopen hello **мастер восстановления**. Щелкните **Далее**.

    ![Просмотр выбранных параметров восстановления](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Выберите тип восстановления требуется tooperform и нажмите кнопку hello **Далее**.

    ![Тип восстановления](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > Здравствуйте, выбор **восстановить toooriginal** в hello производится восстановление исходного узла SharePoint hello элемента toohello.
   >
   >
8. Выберите hello **процесса восстановления** нужных toouse.

   * Выберите **восстановление без использования фермы восстановления** Если ферма SharePoint hello не изменилась и hello таким же, как hello восстановления точка, которая является время восстановления.
   * Выберите **восстановления с использованием фермы восстановления** hello фермы SharePoint изменился с момента создания точки восстановления hello.

     ![процесс восстановления](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Временно обеспечивают промежуточного экземпляра расположение toorecover hello базы данных SQL Server, а также в промежуточной папке MABS и hello сервера, на котором выполняется SharePoint toorecover hello элемента.

    ![Расположение промежуточного хранения 1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    MABS присоединяет hello базы данных содержимого, на котором размещается hello SharePoint элемент toohello временный экземпляр SQL Server. Из базы данных контента hello он восстанавливает элемент hello и помещает его в промежуточное расположение файла в MABS hello. Hello восстановить элемент, на hello, теперь промежуточное расположение toohello toobe экспортировать потребностей промежуточное расположение на ферме SharePoint hello.

    ![Расположение промежуточного хранения 2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Выберите **задание параметров восстановления**и применить параметры безопасности toohello фермы SharePoint или применить настройки безопасности hello hello точки восстановления. Щелкните **Далее**.

    ![Варианты восстановления](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > Можно выбрать использование полосы пропускания сети toothrottle hello. Это сводит к минимуму влияние toohello рабочего сервера во время рабочих часов.
    >
    >
11. Просмотрите сводные данные hello и нажмите кнопку **восстановить** toobegin восстановления файла hello.

    ![Сводка параметров восстановления](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Теперь выберите hello **мониторинг** на вкладке hello **консоли администрирования MABS** tooview hello **состояние** hello восстановления.

    ![Состояние восстановления](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > восстановлен файл Hello. Вы можете обновить файл hello восстановить toocheck сайта SharePoint hello.
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Восстановление базы данных SharePoint из Azure с помощью DPM
1. toorecover базы данных содержимого SharePoint, просмотрите различные точки восстановления (как показано выше) и выберите точку восстановления hello, которая будет toorestore.

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Дважды щелкните hello SharePoint tooshow точки hello доступных SharePoint каталог данных для восстановления.

   > [!NOTE]
   > Так как ферма SharePoint hello защищен для долгосрочного хранения в Azure, можно найти в MABS никаких сведений каталога (метаданные). В результате каждый раз, когда в момент базы данных содержимого SharePoint должен восстановить toobe, понадобятся toocatalog hello веб-фермы SharePoint.
   >
   >
3. Нажмите кнопку **Повторить каталогизацию**.

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    Hello **повторная Каталогизация облака** откроется окно состояния.

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    После завершения создания каталога hello состояние изменяется слишком*успешно*. Нажмите кнопку **Закрыть**

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Щелкните объект SharePoint hello показано hello MABS **восстановления** вкладке Структура базы данных контента tooget hello. Щелкните правой кнопкой мыши элемент hello и нажмите кнопку **восстановить**.

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. На этом этапе выполните hello [шаги восстановления ранее в этой статье](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover базы данных содержимого SharePoint с диска.

## <a name="faqs"></a>Часто задаваемые вопросы
Вопрос. можно ли восстановить исходное расположение элемента toohello SharePoint, если SharePoint настраивается с помощью SQL AlwaysOn (с защитой на диске)?<br>
Ответ Да, hello элемент может быть восстановленные toohello исходного сайта SharePoint.

Вопрос. можно ли восстановить исходное расположение toohello базы данных SharePoint, если SharePoint настраивается с помощью SQL AlwaysOn?<br>
Ответ, так как базы данных SharePoint настраиваются в SQL AlwaysOn, их нельзя изменить, если удаляется группа доступности hello. В результате MABS нельзя восстановить в исходное расположение toohello базы данных. Можно восстановить экземпляр SQL Server tooanother базы данных SQL Server.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о защите SharePoint с помощью MABS см. в [этой серии видеоматериалов](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group).
