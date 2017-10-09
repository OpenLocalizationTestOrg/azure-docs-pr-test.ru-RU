<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="f54d8-101">При внесении изменений toohello адаптера StorSimple для SharePoint RBS конфигурации, вы должны войти в систему с учетной записью пользователя, которая принадлежит группе администраторов домена toohello.</span><span class="sxs-lookup"><span data-stu-id="f54d8-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="f54d8-102">Кроме того для доступа к странице конфигурации hello из браузера на hello же разместить в качестве центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="f54d8-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="f54d8-103">tooconfigure RBS</span><span class="sxs-lookup"><span data-stu-id="f54d8-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="f54d8-104">Откройте страницу центра администрирования SharePoint hello и обзор слишком**параметры системы**.</span><span class="sxs-lookup"><span data-stu-id="f54d8-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="f54d8-105">В hello **Azure StorSimple** щелкните **настроить адаптер StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="f54d8-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Настройка адаптера StorSimple hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="f54d8-107">На hello **настроить адаптер StorSimple** страницы:</span><span class="sxs-lookup"><span data-stu-id="f54d8-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="f54d8-108">Убедитесь в том, что hello **Включение редактирования путь** установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="f54d8-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="f54d8-109">В текстовом поле hello введите путь соглашения об универсальных именах (UNC) hello hello хранилища больших двоичных ОБЪЕКТОВ.</span><span class="sxs-lookup"><span data-stu-id="f54d8-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f54d8-110">том хранилища больших двоичных ОБЪЕКТОВ Hello должен размещаться в томе iSCSI, настроенном на устройстве StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="f54d8-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="f54d8-111">Нажмите кнопку hello **включить** расположенную под каждой из баз данных содержимого hello, что требуется tooconfigure для удаленного хранилища.</span><span class="sxs-lookup"><span data-stu-id="f54d8-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f54d8-112">Hello хранилища больших двоичных ОБЪЕКТОВ должен быть общим и доступным, все серверы (WFE) веб-интерфейса и hello учетной записи пользователя, настроенного для фермы серверов SharePoint hello должен иметь доступ toohello папки.</span><span class="sxs-lookup"><span data-stu-id="f54d8-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Включение поставщика RBS hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="f54d8-114">При включении или отключении RBS появится также следующие сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="f54d8-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![Настройка включения и выключения адаптера StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="f54d8-116">Нажмите кнопку hello **обновление** конфигурация hello tooapply кнопок.</span><span class="sxs-lookup"><span data-stu-id="f54d8-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="f54d8-117">При нажатии кнопки hello **обновление** кнопки hello состояние конфигурации RBS будет обновлена на всех интерфейсных веб-серверах и hello Вся ферма получит поддержку RBS.</span><span class="sxs-lookup"><span data-stu-id="f54d8-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="f54d8-118">появляется после сообщения Hello.</span><span class="sxs-lookup"><span data-stu-id="f54d8-118">hello following message appears.</span></span>
      
      ![Сообщение о конфигурации адаптера](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="f54d8-120">Если RBS настраивается для фермы SharePoint с очень большим числом баз данных (более 200), веб-страницы центра администрирования SharePoint hello время ожидания может истечь. В этом случае обновите страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="f54d8-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="f54d8-121">Это не влияет на процесс настройки hello.</span><span class="sxs-lookup"><span data-stu-id="f54d8-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="f54d8-122">Проверка конфигурации hello:</span><span class="sxs-lookup"><span data-stu-id="f54d8-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="f54d8-123">Войдите на веб-сайт центра администрирования SharePoint toohello и обзор toohello **настроить адаптер StorSimple** страницы.</span><span class="sxs-lookup"><span data-stu-id="f54d8-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="f54d8-124">Проверьте соответствие введенных параметров hello toomake сведения о конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="f54d8-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="f54d8-125">Проверьте правильность работы RBS.</span><span class="sxs-lookup"><span data-stu-id="f54d8-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="f54d8-126">Отправьте tooSharePoint документа.</span><span class="sxs-lookup"><span data-stu-id="f54d8-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="f54d8-127">Обзор toohello UNC-путь, который вы настроили.</span><span class="sxs-lookup"><span data-stu-id="f54d8-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="f54d8-128">Убедитесь, что hello структура каталога RBS создана и что он содержит отправлен hello объекта.</span><span class="sxs-lookup"><span data-stu-id="f54d8-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="f54d8-129">(Необязательно) Можно использовать Microsoft RBS hello `Migrate()` командлет PowerShell, входящий в состав SharePoint toomigrate существующего большого двоичного ОБЪЕКТА содержимого toohello устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f54d8-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="f54d8-130">Дополнительные сведения см. в разделе [миграции содержимого в или из RBS в SharePoint 2013] [ 6] или [миграции содержимого в или из RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="f54d8-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="f54d8-131">(Необязательно) При тестовой установке Вы можете убедиться, что hello большие двоичные объекты перемещены из базы данных содержимого hello, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f54d8-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="f54d8-132">Запустите SQL Management Studio</span><span class="sxs-lookup"><span data-stu-id="f54d8-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="f54d8-133">Запустите запрос ListBlobsInDB_2010.sql или ListBlobsInDB_2013.sql hello, следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f54d8-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="f54d8-134">Если RBS настроены правильно, значение NULL должно отображаться в столбце SizeOfContentInDB hello для любого объекта, отправленного и успешно перемещенного в удаленном Хранилище.</span><span class="sxs-lookup"><span data-stu-id="f54d8-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="f54d8-135">(Необязательно) После настройки RBS и перемещения всех больших двоичных ОБЪЕКТОВ содержимого toohello устройства StorSimple можно переместить устройство toohello hello содержимого базы данных.</span><span class="sxs-lookup"><span data-stu-id="f54d8-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="f54d8-136">При выборе базы данных контента toomove hello, рекомендуется настроить хранилище hello базы данных контента на устройстве hello как первичный том.</span><span class="sxs-lookup"><span data-stu-id="f54d8-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="f54d8-137">Затем используйте установленные устройства StorSimple toohello базы данных контента hello toomigrate рекомендации наиболее SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f54d8-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f54d8-138">Перемещение устройства toohello hello содержимого базы данных поддерживается только для серии StorSimple 8000 hello (не поддерживается для ряда hello 5000 или 7000).</span><span class="sxs-lookup"><span data-stu-id="f54d8-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="f54d8-139">Если хранить большие двоичные объекты и базы данных содержимого hello в разных томах на устройстве StorSimple hello, рекомендуется настроить их в hello одном контейнере томов.</span><span class="sxs-lookup"><span data-stu-id="f54d8-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="f54d8-140">Это гарантирует, что они будут подвергаться резервному копированию вместе.</span><span class="sxs-lookup"><span data-stu-id="f54d8-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f54d8-141">Если RBS не включен, не рекомендуется перемещение устройства StorSimple toohello hello базы данных содержимого.</span><span class="sxs-lookup"><span data-stu-id="f54d8-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="f54d8-142">Эта конфигурация не тестировалась.</span><span class="sxs-lookup"><span data-stu-id="f54d8-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="f54d8-143">Далее перейдите toohello: [Настройка сбора мусора](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="f54d8-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
