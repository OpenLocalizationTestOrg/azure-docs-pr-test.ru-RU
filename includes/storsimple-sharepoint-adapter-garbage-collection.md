<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="83baf-101">В этой процедуре будут выполнены следующие действия.</span><span class="sxs-lookup"><span data-stu-id="83baf-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="83baf-102">[Подготовка исполняемый файл программы обслуживания hello toorun](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="83baf-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="83baf-103">[Подготовка базы данных контента hello и Корзина для немедленного удаления потерянных больших двоичных объектов](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="83baf-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="83baf-104">[Запуск Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="83baf-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="83baf-105">[Восстановить базу данных контента hello и параметров корзины](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="83baf-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="83baf-106">hello toorun tooprepare программы обслуживания</span><span class="sxs-lookup"><span data-stu-id="83baf-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="83baf-107">На hello веб-сервере переднего плана откройте консоль управления SharePoint 2013 hello от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="83baf-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="83baf-108">Перейдите в папку toohello *загрузочный диск*: \Program Files\Microsoft 10.50\Maintainer удаленного хранилища BLOB-данных SQL\.</span><span class="sxs-lookup"><span data-stu-id="83baf-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="83baf-109">Переименуйте **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** слишком**web.config**.</span><span class="sxs-lookup"><span data-stu-id="83baf-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="83baf-110">Используйте `aspnet_regiis -pdf connectionStrings` toodecrypt файл web.config hello.</span><span class="sxs-lookup"><span data-stu-id="83baf-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="83baf-111">В файле web.config расшифрованные hello под hello `connectionStrings` , добавьте строку hello подключения для экземпляра SQL server и hello имя базы данных содержимого.</span><span class="sxs-lookup"><span data-stu-id="83baf-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="83baf-112">См. следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="83baf-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="83baf-113">Используйте `aspnet_regiis –pef connectionStrings` toore-зашифровать файл web.config hello.</span><span class="sxs-lookup"><span data-stu-id="83baf-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="83baf-114">Переименуйте web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span><span class="sxs-lookup"><span data-stu-id="83baf-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="83baf-115">базы данных контента tooprepare hello и tooimmediately корзины удаление потерянных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="83baf-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="83baf-116">Запустите следующие запросы на обновление для базы данных содержимого целевой hello hello hello SQL Server в SQL Management Studio:</span><span class="sxs-lookup"><span data-stu-id="83baf-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="83baf-117">На hello веб-сервере переднего плана, в разделе **центра администрирования**, изменить hello **Web приложения Общие настройки** для hello требуемого hello отключения базы данных контента tootemporarily корзины.</span><span class="sxs-lookup"><span data-stu-id="83baf-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="83baf-118">Это действие также будет пустым hello корзины для любых коллекций связанному сайту.</span><span class="sxs-lookup"><span data-stu-id="83baf-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="83baf-119">toodo, нажмите кнопку **центра администрирования** -> **управление приложениями** -> **веб-приложений (Управление веб-приложениями)**  ->  **SharePoint - 80** -> **Общие параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="83baf-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="83baf-120">Набор hello **очистки состояния Bin** слишком**OFF**.</span><span class="sxs-lookup"><span data-stu-id="83baf-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Общие параметры веб-приложения](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="83baf-122">hello toorun программы обслуживания</span><span class="sxs-lookup"><span data-stu-id="83baf-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="83baf-123">Hello веб-сервере переднего плана в консоль управления SharePoint 2013 hello запустите hello программы обслуживания следующим образом:</span><span class="sxs-lookup"><span data-stu-id="83baf-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="83baf-124">Здравствуйте, только `GarbageCollection` операция поддерживается для StorSimple на данный момент.</span><span class="sxs-lookup"><span data-stu-id="83baf-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="83baf-125">Обратите внимание на то, что параметры hello для Microsoft.Data.SqlRemoteBlobs.Maintainer.exe чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="83baf-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="83baf-126">базы данных контента toorevert hello и параметров корзины</span><span class="sxs-lookup"><span data-stu-id="83baf-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="83baf-127">Запустите следующие запросы на обновление для базы данных содержимого целевой hello hello hello SQL Server в SQL Management Studio:</span><span class="sxs-lookup"><span data-stu-id="83baf-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="83baf-128">На hello веб-сервере переднего плана в **центра администрирования**, изменить hello **Web приложения Общие настройки** для hello требуемого hello toore включения базы данных содержимого корзины.</span><span class="sxs-lookup"><span data-stu-id="83baf-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="83baf-129">toodo, нажмите кнопку **центра администрирования** -> **управление приложениями** -> **веб-приложений (Управление веб-приложениями)**  ->  **SharePoint - 80** -> **Общие параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="83baf-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="83baf-130">Задать hello очистки состояния Bin слишком**ON**.</span><span class="sxs-lookup"><span data-stu-id="83baf-130">Set hello Recycle Bin Status too**ON**.</span></span>

