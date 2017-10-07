---
title: "aaaBack копию приложения в Azure"
description: "Узнайте, как резервные копии toocreate приложений в службе приложений Azure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a>Архивация приложения в Azure
Здравствуйте, резервное копирование и восстановление из состава [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) позволяет легко создавать резервные копии приложения, вручную или по расписанию. Можно восстановить снимок tooa приложения hello предыдущее состояние, восстановление приложения tooanother или перезаписи существующего приложения hello. 

Сведения о восстановлении приложения из резервной копии см. в статье [Восстановление приложения в службе приложений Azure](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>Что входит в резервную копию
Службы приложений можно создавать резервные копии следующих hello сведения учетной записи хранилища Azure tooan и контейнера, что вы настроили toouse вашего приложения. 

* конфигурация приложения;
* содержимое файла;
* Приложение tooyour подключенной базы данных

функция резервного копирования поддерживает Hello следующие решения базы данных. 
   - [База данных SQL](https://azure.microsoft.com/en-us/services/sql-database/)
   - [база данных Azure для MySQL (предварительная версия)](https://azure.microsoft.com/en-us/services/mysql);
   - [база данных Azure для PostgreSQL (предварительная версия)](https://azure.microsoft.com/en-us/services/postgres);
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview);
   - [MySQL в приложении](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app).
 

> [!NOTE]
>  Каждая резервная копия является полной автономной копией приложения, а не добавочным обновлением.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Требования и ограничения
* Здравствуйте, создайте резервную копию, и функция восстановления требует hello toobe плана служб приложений в hello **Стандартная** уровня или **Premium** уровня. Дополнительные сведения о масштабировании вашей toouse план службы приложений более высокого уровня см. в разделе [масштабировать приложение в Azure](web-sites-scale.md).  
  Уровень **Премиум** позволяет создавать большее количество ежедневных резервных копий по сравнению с уровнем **Стандартный**.
* Требуется имя учетной записи хранилища Azure и контейнер в hello той же подписке, что требуется toobackup приложение hello. Дополнительные сведения об учетных записях хранения Azure см. в разделе hello [ссылки](#moreaboutstorage) конце hello в этой статье.
* Резервные копии могут быть too10 Гбайт, приложение и база данных содержимого. Если размер резервной копии hello превышает это ограничение, возникает сообщение об ошибке.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>Создание резервной копии вручную
1. В hello [портала Azure](https://portal.azure.com), перейдите в колонку tooyour приложения, выберите **резервные копии**. Hello **резервные копии** отображается колонку.
   
    ![Страница резервных копий][ChooseBackupsPage]
   
   > [!NOTE]
   > Если вы видите сообщение hello, показанное ниже, выберите его tooupgrade плана служб приложений перед продолжением с резервными копиями.
   > Дополнительные сведения см. в разделе [Масштабирование веб-приложения в службе приложений Azure](web-sites-scale.md).  
   > ![Выбор учетной записи хранения](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. В hello **резервного копирования** колонка, щелкните **Настройка**
![нажмите кнопку настроить.](./media/web-sites-backup/ClickConfigure1.png)
3. В hello **конфигурация резервного копирования** колонка, щелкните **хранилища: не настроен** tooconfigure учетной записи хранилища.
   
    ![Выбор учетной записи хранения][ChooseStorageAccount]
4. Выберите расположение резервной копии, щелкнув **Учетная запись хранения** > **Контейнер**. Учетная запись хранения Hello должны принадлежать toohello той же подписке, необходимо tooback приложение hello. При желании можно создать новую учетную запись хранения или новый контейнер в соответствующих колонках hello. Закончив, щелкните **Выбрать**.
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. В hello **конфигурация резервного копирования** колонки, по-прежнему остается открытым, можно настроить **Backup Database**, выберите hello базы данных, вы должны tooinclude в резервных копиях hello (база данных SQL или MySQL), а затем нажмите кнопку **ОК**.  
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Для tooappear базы данных, в этом списке, его строка подключения должен существовать в hello **строки подключения** раздел hello **параметры приложения** колонку для вашего приложения.
   > 
   > 
6. В hello **конфигурация резервного копирования** колонка, щелкните **Сохранить**.    
7. В hello **резервные копии** колонка, щелкните **резервного копирования**.
   
    ![Кнопка создания резервной копии][BackUpNow]
   
    Появится сообщение о ходе выполнения во время процесса резервного копирования hello.

После завершения настройки учетной записи хранилища hello и контейнер может инициировать архивации вручную в любое время.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Настройка автоматического резервного копирования
1. В hello **конфигурации резервного копирования** задать колонке **запланированное резервное копирование** слишком**на**. 
   
    ![Выбор учетной записи хранения](./media/web-sites-backup/05ScheduleBackup1.png)
2. Задать расписание резервного копирования, параметры будут отображаться, **запланированного резервного копирования** слишком**на**, можно настроить желаемым образом hello расписание резервного копирования и нажмите кнопку **ОК**.
   
    ![Включение автоматически создаваемых резервных копий][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Настройка частичной архивации
Иногда необходимо исключить toobackup все данные в приложении. Вот несколько таких случаев.

* У вас [настроена еженедельная архивация](web-sites-backup.md#configure-automated-backups) приложения со статическим содержимым, которое никогда не меняется. Это могут быть старые записи блога или изображения.
* Приложение имеет более 10 ГБ содержимого (то есть hello max сумму, которую можно создать резервные копии за раз).
* Файлы журнала toobackup hello не следует.

Частичные резервные копии позволяет выбрать только набор файлов, вы хотите toobackup.

### <a name="exclude-files-from-your-backup"></a>Исключение файлов из резервной копии
Предположим, что у вас есть приложение, которое содержит файлы журналов и статические изображения, которые были резервного копирования один раз и не будут toochange. В таких случаях вы можете исключить эти папки и файлы из будущих резервных копий. tooexclude файлов и папок из резервных копий, создавать `_backup.filter` файла в hello `D:\home\site\wwwroot` папку приложения. Укажите список файлов и папок необходимо tooexclude в этом файле hello. 

Файлы — toouse Kudu tooaccess легко. Нажмите кнопку **Дополнительные инструменты -> Go** для вашей веб приложения tooaccess Kudu.

![Использование Kudu с помощью портала][kudu-portal]

Определите hello папок, tooexclude из резервных копий.  Например вы хотите toofilter файлы и папки выделенный hello.

![Папка с изображениями][ImagesFolder]

Создайте файл с именем `_backup.filter` в файл hello поместить hello выше списка, но удалить `D:\home`. В одной строке указывайте один каталог или файл. Поэтому содержимое hello hello файла должно быть:
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Отправка `_backup.filter` файл toohello `D:\home\site\wwwroot\` каталога сайта с помощью [ftp](web-sites-deploy.md#ftp) или любой другой метод. Если вы хотите, можно создать файл hello непосредственно с помощью Kudu `DebugConsole` и вставка содержимого hello существует.

Выполнение архивации hello таким же образом, это обычно делается, [вручную](#create-a-manual-backup) или [автоматически](#configure-automated-backups). Теперь, все файлы и папки, указанные в `_backup.filter` исключается из hello следующие операции резервного копирования в план или запуск вручную. 

> [!NOTE]
> Восстановление частичные резервные копии вашего сайта hello так же, как [восстановить регулярного резервного копирования](web-sites-restore.md). процесс восстановления Hello hello правильно.
> 
> При восстановлении полной резервной копии все содержимое на сайте hello заменяется на hello резервного копирования. Если файл находится на сайте hello, но не в резервной копии hello, она удаляется. Но если частичная резервная копия будет восстановлена, любое содержимое, которое находится в одном из каталогов hello черный или любой черного списка файл оставляется.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Как хранятся резервные копии
После внесения одной или нескольких копий приложения hello резервные копии являются видимыми в hello **контейнеры** колонке вашей учетной записи хранилища и приложения. В учетной записи хранения hello, каждой резервной копии состоит из`.zip` файл, содержащий данные резервного копирования hello и `.xml` файл, содержащий манифест hello `.zip` содержимое файлов. Можно распаковать и обзор эти файлы, если требуется tooaccess резервных копий без фактического выполнения восстановления в приложение.

Hello резервной копии базы данных для приложения hello хранится в корневой hello the.zip файла. Для базы данных SQL это файл BACPAC (без расширения), и его можно импортировать. toocreate на hello экспорта BACPAC основе базы данных SQL см. в разделе [импорта файла BACPAC tooCreate новой пользовательской базы данных](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> Изменение любого файла hello в вашей **websitebackups** контейнер может привести к hello резервного копирования toobecome недопустимые и поэтому невосстановимой.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>Дальнейшие действия
Сведения о восстановлении приложения из резервной копии см. в статье [Восстановление приложения в службе приложений Azure](web-sites-restore.md). Можно также резервное копирование и восстановление приложения служб приложений с помощью REST API (см. [использования REST toobackup и восстановление приложения служб приложений](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

