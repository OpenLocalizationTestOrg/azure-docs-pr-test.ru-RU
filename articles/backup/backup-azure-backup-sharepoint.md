---
title: "aaaDPM/Azure резервной копии сервера защиту фермы SharePoint tooAzure | Документы Microsoft"
description: "В этой статье содержится обзор защиты сервера DPM и Azure Backup tooAzure фермы SharePoint"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 726d59320b8d9f14b38e0f041308019eebcfb77b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Резервное копирование фермы SharePoint tooAzure
Резервное копирование SharePoint фермы tooMicrosoft Azure с помощью System Center Data Protection Manager (DPM) в много hello так же, резервное копирование других источников данных. Резервное копирование Azure обеспечивает гибкость в toocreate hello расписание резервного копирования ежедневно, еженедельно, ежемесячно или ежегодно точки резервного копирования и предоставляет параметры политики хранения для различных точках рабочего процесса резервного копирования. DPM обеспечивает hello возможность toostore локальный диск копий целях быстрое время восстановления (RTO) и toostore копирует tooAzure экономичной, долгосрочного хранения.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Поддерживаемые версии SharePoint и соответствующие сценарии защиты
Azure Backup для DPM поддерживает следующие сценарии hello:

| Рабочая нагрузка | Версия | Развертывание SharePoint | Тип развертывания DPM | DPM – System Center 2012 R2 | Защита и восстановление |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0 |SharePoint разворачивается как физический сервер или виртуальная машина Hyper-V/VMware  <br> -------------- <br> SQL AlwaysOn |Физический сервер или локальная виртуальная машина Hyper-V |Поддержка резервного копирования tooAzure из накопительного пакета обновления 5 |Параметры восстановления фермы SharePoint: ферма, база данных, файл или элемент списка для восстановления из точек восстановления диска.  Восстановление фермы и базы данных из точек восстановления Azure. |

## <a name="before-you-start"></a>Перед началом работы
Существует несколько моментов, которые необходимо tooconfirm перед выполнением резервного копирования tooAzure фермы SharePoint.

### <a name="prerequisites"></a>Предварительные требования
Прежде чем продолжить, убедитесь, что выполнены все hello [предварительные требования для использования службы архивации Microsoft Azure](backup-azure-dpm-introduction.md#prerequisites) tooprotect рабочих нагрузок. Некоторые задачи предварительных требований для включения: создание резервного хранилища, загрузить учетные данные хранилища, установка агента резервного копирования Azure и зарегистрируйте хранилище hello резервного копирования сервера DPM и Azure.

### <a name="dpm-agent"></a>Агент DPM
Hello DPM агент должен устанавливаться на приветствия сервера, на котором выполняется SharePoint, hello серверов, работающих под управлением SQL Server и другие серверы, которые являются частью фермы SharePoint hello. Дополнительные сведения о том, как tooset hello агента защиты, в разделе [установки агента защиты](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Hello одно исключение — установить агент hello только на одном веб-сервере переднего плана (WFE). DPM требуется агент hello на один tooserve сервера WFE только в качестве точки входа hello для защиты.

### <a name="sharepoint-farm"></a>Ферма SharePoint
Для каждых 10 млн элементов в ферме hello должен быть по крайней мере 2 ГБ дискового пространства на томе hello, где находится папка DPM hello. Эта память нужна для создания каталога. Для DPM toorecover конкретных элементов (семейств веб-сайтов, сайты, списки, библиотеки документов, папки, отдельные документы и элементы списка) создания каталогов создает список hello URL-адресов, которые содержатся в каждой базе данных контента. Можно просмотреть список hello URL-адреса в hello hello восстанавливаемый элемент области **восстановления** задач консоли администрирования DPM.

### <a name="sql-server"></a>SQL Server
DPM выполняется как учетная запись LocalSystem. tooback копирование баз данных SQL Server, DPM требуется прав системного администратора для этой учетной записи для hello сервера, на котором выполняется SQL Server. Задать NT AUTHORITY\SYSTEM слишком*sysadmin* hello сервера, на котором выполняется SQL Server, прежде чем создать его резервную копию.

Если ферма SharePoint hello баз данных SQL Server, которые настроены с псевдонимами SQL Server, установите клиентские компоненты SQL Server hello на hello интерфейсный веб-сервер, который будет защищать DPM.

### <a name="sharepoint-server"></a>SharePoint Server
Производительность системы зависит от многих факторов, включая размер фермы SharePoint. Как правило, для защиты фермы SharePoint объемом 25 ТБ используется один сервер DPM.

### <a name="dpm-update-rollup-5"></a>Накопительный пакет обновления DPM 5
toobegin защиты tooAzure фермы SharePoint, необходимо tooinstall накопительного пакета обновления DPM 5 или более поздней версии. Накопительный пакет обновления 5 предоставляет возможность tooprotect hello tooAzure фермы SharePoint, если hello ферма настроена с помощью SQL AlwaysOn.
Дополнительные сведения см. в разделе hello блога, вводит [набор обновлений 5 DPM](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)

### <a name="whats-not-supported"></a>Что не поддерживается
* Защита фермы SharePoint с помощью DPM не охватывает индексы поиска или базы данных службы приложений. Необходимо будет tooconfigure hello защиты этих баз данных отдельно.
* DPM не поддерживает архивацию баз данных SharePoint SQL Server, размещенных в общих хранилищах на масштабируемом файловом сервере.

## <a name="configure-sharepoint-protection"></a>Настройка защиты SharePoint
Перед использованием DPM tooprotect SharePoint, необходимо настроить hello модуля записи VSS SharePoint (службы модуля записи WSS) с помощью **ConfigureSharePoint.exe**.

Можно найти **ConfigureSharePoint.exe** в папке \bin hello [путь установки DPM] на интерфейсном веб-сервере hello. Это средство предоставляет hello агент защиты с hello учетные данные для фермы SharePoint hello. Файл нужно распаковать на одном интерфейсном веб-сервере. Если у вас таких серверов несколько, выберите один из них для настройки группы защиты.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>hello tooconfigure служба модуля записи VSS SharePoint
1. На сервере WFE hello, в командной строке перейти слишком \bin\ [расположение установки DPM]
2. Введите ConfigureSharePoint -EnableSharePointProtection.
3. Введите учетные данные администратора фермы hello. Эта учетная запись должна быть членом hello локальной группы администраторов на сервере WFE hello. Если администратор фермы hello не hello grant локального администратора, следующие разрешения на сервере WFE hello:
   * Предоставление hello WSS_Admin_WPG полный доступ toohello DPM папку группы (% Program Files%\Microsoft Data Protection Manager\DPM).
   * Предоставьте hello WSS_Admin_WPG группы доступа на чтение toohello DPM реестра (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Вам потребуется toorerun ConfigureSharePoint.exe при каждом изменении в hello учетные данные администратора фермы SharePoint.
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a>Архивация фермы SharePoint с помощью DPM
После настройки DPM и hello фермы SharePoint, как описано ранее SharePoint могут быть защищены с помощью DPM.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect фермы SharePoint
1. Из hello **защиты** вкладка hello консоли администратора DPM щелкните **New**.
    ![Вкладка создания защиты](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. На hello **Выбор типа группы защиты** страница hello **создания новой группы защиты** мастера, выберите **серверы**, а затем нажмите кнопку **Далее** .
   
    ![Выберите тип группы защиты](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. На hello **Выбор членов группы** экрана, выберите hello флажок для сервера SharePoint hello tooprotect и щелкните **Далее**.
   
    ![Выберите членов группы](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > С установленным агентом DPM hello вы увидите hello сервера в мастере hello. DPM демонстрирует также его структуру. Поскольку вы запустили ConfigureSharePoint.exe, DPM взаимодействует со службой модуля записи VSS SharePoint hello и все соответствующие базы данных SQL Server и распознает hello структура фермы SharePoint, hello связанных баз данных содержимого и все соответствующие элементы.
   > 
   > 
4. На hello **Выбор метода защиты данных** введите имя hello hello **группы защиты**и выберите предпочитаемом *методы защиты*. Щелкните **Далее**.
   
    ![Выберите метод защиты данных](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > метод защиты диска Hello помогает toomeet короткое время восстановления целей. Azure является tootapes сравнение плана экономичной, долгосрочной защиты. Дополнительные сведения см. в разделе [tooreplace резервного копирования Azure для использования инфраструктуры ленты](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)
   > 
   > 
5. На hello **Выбор краткосрочных целей** выберите предпочитаемом **диапазон хранения** и определить, когда требуется toooccur резервных копий.
   
    ![Выберите краткосрочные цели](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > Так как восстановление чаще всего требуется для данных, которые меньше пяти дней, мы выбранные диапазон хранения равен пяти дней на диске и гарантирует, что эта резервная копия hello происходит в непроизводственной часы, в этом примере.
   > 
   > 
6. Просмотрите hello пула хранения дискового пространства, выделенного для группы защиты hello, а затем нажмите кнопку **Далее**.
7. Для каждой группы защиты DPM выделяет toostore места на диске и управление репликами. На этом этапе DPM необходимо создать копию hello выбранных данных. Выберите способ и время создания реплика hello и нажмите кнопку **Далее**.
   
    ![Выберите метод создания реплики](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > убедиться, что сетевой трафик не устаревший toomake выберите время вне рабочих часов.
   > 
   > 
8. DPM обеспечивает целостность данных путем выполнения проверки согласованности в реплике hello. Доступны два параметра. Можно определить проверяет согласованность toorun расписание или DPM запустить проверку согласованности автоматически hello реплики всякий раз, когда он становится несогласованной. Выберите желаемый параметр и нажмите кнопку **Далее**.
   
    ![Проверка согласованности](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. На hello **укажите оперативной защиты данных** выберите hello фермы SharePoint будет tooprotect и нажмите кнопку **Далее**.
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. На hello **укажите расписание оперативной архивации** выберите предпочтительное расписание и нажмите кнопку **Далее**.
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > DPM обеспечивает более двух tooAzure ежедневных резервных копий в разные моменты времени. Резервное копирование Azure можно также управлять hello объем пропускной способности глобальной сети, который может использоваться для архивации в пиковые и непиковые часы с помощью [регулирование сети резервного копирования Azure](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).
    > 
    > 
11. В зависимости от расписания архивации hello, выбранного на hello **указание политики оперативного хранения** страницы выберите hello политику хранения для резервного копирования точек ежедневно, еженедельно, ежемесячно и ежегодно.
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > DPM использует трехуровневую схему хранения, позволяющую выбирать разную политику хранения для разных точек архивации.
    > 
    > 
12. Аналогичные toodisk реплики точки начальную ссылку должен toobe, созданные в Azure. Выберите ваш предпочтительный вариант toocreate tooAzure начальной резервной копии и нажмите кнопку **Далее**.
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Просмотрите выбранные параметры на hello **Сводка** и нажмите кнопку **создать группу**. После создания группы защиты hello, вы увидите сообщение об успешном выполнении.
    
    ![Сводка](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a>Восстановление элемента SharePoint с диска с помощью DPM
В следующем примере hello, hello *элемент восстановление SharePoint* был случайно удален и требуется восстановить toobe.
![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Откройте hello **консоли администрирования DPM**. Показаны все ферм SharePoint, которые защищены с помощью DPM в hello **защиты** вкладки.
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. toorecover hello toobegin элемента, выберите hello **восстановления** вкладки.
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. Чтобы найти *элемент восстановления SharePoint* , можно использовать поиск на основе подстановки в пределах диапазона точек восстановления.
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Выберите точку восстановления, соответствующих hello из результатов поиска hello, щелкните правой кнопкой мыши элемент hello и выберите **восстановить**.
5. Также можно просматривать различные точки восстановления и выбрать базу данных или элемент toorecover. Выберите **даты > времени восстановления**и выберите правильный hello **базы данных > фермы SharePoint > точка восстановления > элемент**.
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
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
9. Временно обеспечивают промежуточного экземпляра расположение toorecover hello базы данных SQL Server, а также промежуточной общую папку на сервере DPM hello и hello сервера, на котором выполняется SharePoint toorecover hello элемента.
   
    ![Расположение промежуточного хранения 1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    Присоединяет hello содержимого базы данных DPM, на котором размещается hello SharePoint элемент toohello временный экземпляр SQL Server. Из базы данных контента hello сервер DPM hello восстанавливает элемент hello и помещает его в промежуточное расположение файла на сервере DPM hello hello. Hello восстановленные элемента, который находится на hello, теперь промежуточное расположение сервера DPM hello должен toohello toobe экспортировать промежуточное расположение на ферме SharePoint hello.
   
    ![Расположение промежуточного хранения 2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Выберите **задание параметров восстановления**и применить параметры безопасности toohello фермы SharePoint или применить настройки безопасности hello hello точки восстановления. Щелкните **Далее**.
    
    ![Варианты восстановления](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > Можно выбрать использование полосы пропускания сети toothrottle hello. Это сводит к минимуму влияние toohello рабочего сервера во время рабочих часов.
    > 
    > 
11. Просмотрите сводные данные hello и нажмите кнопку **восстановить** toobegin восстановления файла hello.
    
    ![Сводка параметров восстановления](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Теперь выберите hello **мониторинг** на вкладке hello **консоли администрирования DPM** tooview hello **состояние** восстановления hello.
    
    ![Состояние восстановления](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > восстановлен файл Hello. Вы можете обновить файл hello восстановить toocheck сайта SharePoint hello.
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Восстановление базы данных SharePoint из Azure с помощью DPM
1. toorecover базы данных содержимого SharePoint, просмотрите различные точки восстановления (как показано выше) и выберите точку восстановления hello, которая будет toorestore.
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Дважды щелкните hello SharePoint tooshow точки hello доступных SharePoint каталог данных для восстановления.
   
   > [!NOTE]
   > Так как для долгосрочного хранения в Azure защиты фермы SharePoint hello, никаких сведений каталога (метаданные) доступен на сервере DPM hello. В результате каждый раз, когда в момент базы данных содержимого SharePoint должен восстановить toobe, понадобятся toocatalog hello веб-фермы SharePoint.
   > 
   > 
3. Нажмите кнопку **Повторить каталогизацию**.
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    Hello **повторная Каталогизация облака** откроется окно состояния.
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    После завершения создания каталога hello состояние изменяется слишком*успешно*. Нажмите кнопку **Закрыть**
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Щелкните объект SharePoint hello показано hello DPM **восстановления** вкладке Структура базы данных контента tooget hello. Щелкните правой кнопкой мыши элемент hello и нажмите кнопку **восстановить**.
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. На этом этапе выполните hello [шаги восстановления ранее в этой статье](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover базы данных содержимого SharePoint с диска.

## <a name="faqs"></a>Часто задаваемые вопросы
Вопрос (В.). Какие версии DPM поддерживаются в SQL Server 2014 и SQL Server 2012 (SP2)?<br>
Ответ (О.). DPM 2012 R2 с накопительным пакетом обновления 4 поддерживает обе версии.

Вопрос. можно ли восстановить исходное расположение элемента toohello SharePoint, если SharePoint настраивается с помощью SQL AlwaysOn (с защитой на диске)?<br>
Ответ Да, hello элемент может быть восстановленные toohello исходного сайта SharePoint.

Вопрос. можно ли восстановить исходное расположение toohello базы данных SharePoint, если SharePoint настраивается с помощью SQL AlwaysOn?<br>
Ответ, так как базы данных SharePoint настраиваются в SQL AlwaysOn, их нельзя изменить, если удаляется группа доступности hello. В результате DPM нельзя восстановить в исходное расположение toohello базы данных. Можно восстановить экземпляр SQL Server tooanother базы данных SQL Server.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о защите SharePoint с помощью DPM см. в [этих видеоматериалах](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group).
* Ознакомьтесь со статьей [Заметки о выпуске System Center 2012 — Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx).
* Ознакомьтесь со статьей [Заметки о выпуске Data Protection Manager в составе System Center 2012 с пакетом обновления 1 (SP1)](https://technet.microsoft.com/library/jj860394.aspx).

