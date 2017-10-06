---
title: "aaaRestore приложения в Azure"
description: "Узнайте, как toorestore приложения из резервной копии."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a>Восстановление приложения в Azure
В этой статье показано, как toorestore приложения в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) , вы уже создали резервные копии (см. [резервное копирование приложения в Azure](web-sites-backup.md)). Восстановите приложение с предыдущего состояния tooa по требованию привязанных баз данных или создайте новое приложение на основе одного из резервной копии исходного приложения. Служба приложений Azure поддерживает следующие базы данных для резервного копирования и восстановления hello:
- [База данных SQL](https://azure.microsoft.com/en-us/services/sql-database/)
- [база данных Azure для MySQL (предварительная версия)](https://azure.microsoft.com/en-us/services/mysql);
- [база данных Azure для PostgreSQL (предварительная версия)](https://azure.microsoft.com/en-us/services/postgres);
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview);
- [MySQL в приложении](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app).

Восстановление из резервных копий является доступной tooapps в **Стандартная** и **Premium** уровня. Дополнительные сведения об увеличении масштаба приложения см. в статье [Увеличение масштаба приложения в Azure](web-sites-scale.md). **Premium** уровня позволяет большего количества ежедневных резервных копий toobe, выполнить чем **Стандартная** уровня.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Восстановление приложения из существующей резервной копии
1. На hello **параметры** колонке приложения в hello портала Azure щелкните **резервные копии** toodisplay hello **резервные копии** колонку. Затем щелкните **Восстановить**.
   
    ![Выбор команды "Восстановить сейчас"][ChooseRestoreNow]
2. В hello **восстановить** колонки, первый источник резервного копирования выберите hello.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    Hello **приложение резервного копирования** на экране отображается все существующие резервные копии текущее приложение hello Здравствуйте, и вы можете легко выбрать один.
    Hello **хранения** параметр позволяет выбрать любой резервной копии ZIP-файл из существующей учетной записи хранилища Azure и контейнер в вашей подписке.
    Если вы пытаетесь toorestore резервной копии другое приложение, используйте hello **хранения** параметр.
3. Укажите назначение hello для восстановления приложения hello в **назначения для восстановления**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Если вы выберете **Перезаписать**, то все существующие данные в текущем приложении будут удалены и перезаписаны. Прежде чем нажимать кнопку **ОК**, убедитесь, что это именно вы хотите toodo.
   > 
   > 
   
    Можно выбрать **существующего приложения** toorestore приложение резервного копирования tooanother приложения hello в hello одной группе ресурс. Прежде чем использовать этот параметр, необходимо другое приложение, уже созданных в группе ресурсов с зеркальным отображением базы данных конфигурации toohello один определенный в резервную копию приложения hello. Можно также создать **New** toorestore приложения содержимого.

4. Нажмите кнопку **ОК**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Скачивание и удаление резервной копии в учетной записи хранения
1. Из основной hello **Обзор** колонке hello Azure portal, **учетные записи хранения**. Откроется список существующих учетных записей хранения.
2. Выберите учетную запись хранения hello, содержащий резервную копию hello требуется берется колонке toodownload или delete.hello для учетной записи хранения hello.
3. В колонке учетной записи хранилища hello выберите hello контейнера
   
    ![Просмотр контейнеров][ViewContainers]
4. Выберите файл резервной копии, которые вы желаете toodownload или удалить.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Нажмите кнопку **загрузки** или **удалить** в зависимости от того, что вы хотите toodo.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Мониторинг операции восстановления
toosee сведения об успешности hello операции восстановления приложения hello, перейдите toohello **журнал действий** колонки в hello портал Azure.  
 

Прокрутите вниз toofind hello требуемого восстановления операции и нажмите кнопку tooselect его.

Hello сведения колонке отображает hello доступные данные, относящиеся toohello операции восстановления.

## <a name="next-steps"></a>Дальнейшие действия
Выполнять резервное копирование и восстановление приложения служб приложений с помощью REST API (см. [tooback REST, используйте копирование и восстановление приложения служб приложений](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
