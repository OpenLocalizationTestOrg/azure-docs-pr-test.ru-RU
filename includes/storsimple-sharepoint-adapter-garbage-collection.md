<!--author=SharS last changed: 9/17/15-->

В этой процедуре будут выполнены следующие действия.

1. [Подготовка исполняемый файл программы обслуживания hello toorun](#to-prepare-to-run-the-maintainer) .
2. [Подготовка базы данных контента hello и Корзина для немедленного удаления потерянных больших двоичных объектов](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [Запуск Maintainer.exe](#to-run-the-maintainer).
4. [Восстановить базу данных контента hello и параметров корзины](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>hello toorun tooprepare программы обслуживания
1. На hello веб-сервере переднего плана откройте консоль управления SharePoint 2013 hello от имени администратора.
2. Перейдите в папку toohello *загрузочный диск*: \Program Files\Microsoft 10.50\Maintainer удаленного хранилища BLOB-данных SQL\.
3. Переименуйте **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** слишком**web.config**.
4. Используйте `aspnet_regiis -pdf connectionStrings` toodecrypt файл web.config hello.
5. В файле web.config расшифрованные hello под hello `connectionStrings` , добавьте строку hello подключения для экземпляра SQL server и hello имя базы данных содержимого. См. следующий пример hello.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Используйте `aspnet_regiis –pef connectionStrings` toore-зашифровать файл web.config hello. 
7. Переименуйте web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>базы данных контента tooprepare hello и tooimmediately корзины удаление потерянных больших двоичных объектов
1. Запустите следующие запросы на обновление для базы данных содержимого целевой hello hello hello SQL Server в SQL Management Studio: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. На hello веб-сервере переднего плана, в разделе **центра администрирования**, изменить hello **Web приложения Общие настройки** для hello требуемого hello отключения базы данных контента tootemporarily корзины. Это действие также будет пустым hello корзины для любых коллекций связанному сайту. toodo, нажмите кнопку **центра администрирования** -> **управление приложениями** -> **веб-приложений (Управление веб-приложениями)**  ->  **SharePoint - 80** -> **Общие параметры приложения**. Набор hello **очистки состояния Bin** слишком**OFF**.
   
    ![Общие параметры веб-приложения](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>hello toorun программы обслуживания
* Hello веб-сервере переднего плана в консоль управления SharePoint 2013 hello запустите hello программы обслуживания следующим образом:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Здравствуйте, только `GarbageCollection` операция поддерживается для StorSimple на данный момент. Обратите внимание на то, что параметры hello для Microsoft.Data.SqlRemoteBlobs.Maintainer.exe чувствительны к регистру. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>базы данных контента toorevert hello и параметров корзины
1. Запустите следующие запросы на обновление для базы данных содержимого целевой hello hello hello SQL Server в SQL Management Studio:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. На hello веб-сервере переднего плана в **центра администрирования**, изменить hello **Web приложения Общие настройки** для hello требуемого hello toore включения базы данных содержимого корзины. toodo, нажмите кнопку **центра администрирования** -> **управление приложениями** -> **веб-приложений (Управление веб-приложениями)**  ->  **SharePoint - 80** -> **Общие параметры приложения**. Задать hello очистки состояния Bin слишком**ON**.

