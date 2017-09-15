<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="2c191-101">При внесении изменений в адаптер StorSimple для настройки SharePoint RBS вы должны войти в систему с учетной записью, входящей в группу «Администраторы домена».</span><span class="sxs-lookup"><span data-stu-id="2c191-101">When making changes to the StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs to the Domain Admins group.</span></span> <span data-ttu-id="2c191-102">Кроме того, необходимо получить доступ к странице «Конфигурация» из браузера, работающего на том же узле центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="2c191-102">Additionally, you must access the configuration page from a browser running on the same host as Central Administration.</span></span>
> 
> 

#### <a name="to-configure-rbs"></a><span data-ttu-id="2c191-103">Настройка RBS</span><span class="sxs-lookup"><span data-stu-id="2c191-103">To configure RBS</span></span>
1. <span data-ttu-id="2c191-104">Откройте страницу центра администрирования SharePoint и перейдите к странице **Параметры системы**.</span><span class="sxs-lookup"><span data-stu-id="2c191-104">Open the SharePoint Central Administration page, and browse to **System Settings**.</span></span> 
2. <span data-ttu-id="2c191-105">В разделе **Azure StorSimple** щелкните **Configure StorSimple Adapter** (Настроить адаптер StorSimple).</span><span class="sxs-lookup"><span data-stu-id="2c191-105">In the **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Настройка адаптера StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="2c191-107">На странице **Настройка адаптера StorSimple** :</span><span class="sxs-lookup"><span data-stu-id="2c191-107">On the **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="2c191-108">Убедитесь, что установлен флажок **Включить путь редактирования** .</span><span class="sxs-lookup"><span data-stu-id="2c191-108">Make sure that the **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="2c191-109">В текстовом поле введите UNC-путь хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2c191-109">In the text box, type the Universal Naming Convention (UNC) path of the BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="2c191-110">Том хранилища больших двоичных объектов должен быть размещен на томе iSCSI, настроенном на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2c191-110">The BLOB store volume must be hosted on an iSCSI volume configured on the StorSimple device.</span></span>

   3. <span data-ttu-id="2c191-111">Нажмите кнопку **Включить** под каждой из баз данных содержимого, которые нужно настроить для удаленного хранилища.</span><span class="sxs-lookup"><span data-stu-id="2c191-111">Click the **Enable** button below each of the content databases that you want to configure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="2c191-112">Хранилище больших двоичных объектов должно быть общим и доступным всем интерфейсным веб-серверам (WFE), а учетная запись пользователя, настроенная на ферме серверов SharePoint, должна иметь доступ к общей папке.</span><span class="sxs-lookup"><span data-stu-id="2c191-112">The BLOB store must be shared and reachable by all web front-end (WFE) servers, and the user account that is configured for the SharePoint server farm must have access to the share.</span></span>
      
      ![Включение поставщика RBS](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="2c191-114">При включении или отключении RBS также появится следующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="2c191-114">When you enable or disable RBS, you will also see the following message.</span></span>
      
      ![Настройка включения и выключения адаптера StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="2c191-116">Нажмите кнопку **Обновить** , чтобы применить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="2c191-116">Click the **Update** button to apply the configuration.</span></span> <span data-ttu-id="2c191-117">При нажатии кнопки **Обновить** состояние конфигурации RBS будет обновлено на всех интерфейсных веб-серверах, и для всей фермы будет включено RBS.</span><span class="sxs-lookup"><span data-stu-id="2c191-117">When you click the **Update** button, the RBS configuration status will be updated on all WFE servers, and the entire farm will be RBS-enabled.</span></span> <span data-ttu-id="2c191-118">Появится указанное ниже сообщение.</span><span class="sxs-lookup"><span data-stu-id="2c191-118">The following message appears.</span></span>
      
      ![Сообщение о конфигурации адаптера](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="2c191-120">При настройке RBS для фермы SharePoint с очень большим количеством баз данных (более 200) возможен тайм-аут веб-страницы центра администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2c191-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), the SharePoint Central Administration web page might time out.</span></span> <span data-ttu-id="2c191-121">Если это произошло, обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="2c191-121">If that occurs, refresh the page.</span></span> <span data-ttu-id="2c191-122">Это не влияет на процесс настройки.</span><span class="sxs-lookup"><span data-stu-id="2c191-122">This does not affect the configuration process.</span></span>

4. <span data-ttu-id="2c191-123">Проверьте конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="2c191-123">Verify the configuration:</span></span>
   
   1. <span data-ttu-id="2c191-124">Войдите на веб-сайт центра администрирования SharePoint и перейдите на страницу **Настройка адаптера StorSimple** .</span><span class="sxs-lookup"><span data-stu-id="2c191-124">Log on to the SharePoint Central Administration website, and browse to the **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="2c191-125">Проверьте сведения о конфигурации, чтобы убедиться в том, что они соответствуют введенным параметрам.</span><span class="sxs-lookup"><span data-stu-id="2c191-125">Check the configuration details to make sure that they match the settings that you entered.</span></span> 
5. <span data-ttu-id="2c191-126">Проверьте правильность работы RBS.</span><span class="sxs-lookup"><span data-stu-id="2c191-126">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="2c191-127">Отправьте документ в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2c191-127">Upload a document to SharePoint.</span></span> 
   2. <span data-ttu-id="2c191-128">Перейдите по UNC-пути, который вы настроили.</span><span class="sxs-lookup"><span data-stu-id="2c191-128">Browse to the UNC path that you configured.</span></span> <span data-ttu-id="2c191-129">Убедитесь, что структура каталога RBS создана и содержит отправленный объект.</span><span class="sxs-lookup"><span data-stu-id="2c191-129">Make sure that the RBS directory structure was created and that it contains the uploaded object.</span></span>
6. <span data-ttu-id="2c191-130">(Необязательно) Можно использовать командлет PowerShell `Migrate()` для Microsoft RBS, включенный в SharePoint, чтобы перенести существующее содержимое больших двоичных объектов на устройство StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2c191-130">(Optional) You can use the Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint to migrate existing BLOB content to the StorSimple device.</span></span> <span data-ttu-id="2c191-131">Дополнительные сведения см. в разделе [миграции содержимого в или из RBS в SharePoint 2013] [ 6] или [миграции содержимого в или из RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="2c191-131">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="2c191-132">(Необязательно.) При тестовой установке можно следующим образом убедиться, что большие двоичные объекты перемещены из базы данных содержимого.</span><span class="sxs-lookup"><span data-stu-id="2c191-132">(Optional) On test installations, you can verify that the BLOBs were moved out of the content database as follows:</span></span> 
   
   1. <span data-ttu-id="2c191-133">Запустите SQL Management Studio</span><span class="sxs-lookup"><span data-stu-id="2c191-133">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="2c191-134">Выполните запрос ListBlobsInDB_2010.sql или ListBlobsInDB_2013.sql, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2c191-134">Run the ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
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
      
      <span data-ttu-id="2c191-135">Если RBS настроена правильно, значение NULL должно отображаться в столбце SizeOfContentInDB любого объекта, отправленного и успешно перемещенного с помощью RBS.</span><span class="sxs-lookup"><span data-stu-id="2c191-135">If RBS was configured correctly, a NULL value should appear in the SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="2c191-136">(Необязательно.) После настройки RBS и перемещения содержимого больших двоичных объектов на устройство StorSimple можно переместить базу данных содержимого на устройство.</span><span class="sxs-lookup"><span data-stu-id="2c191-136">(Optional) After you configure RBS and move all BLOB content to the StorSimple device, you can move the content database to the device.</span></span> <span data-ttu-id="2c191-137">Если необходимо переместить базу данных содержимого, рекомендуется настроить хранилище базы данных содержимого на устройстве как первичный том.</span><span class="sxs-lookup"><span data-stu-id="2c191-137">If you choose to move the content database, we recommend that you configure the content database storage on the device as a primary volume.</span></span> <span data-ttu-id="2c191-138">Используйте рекомендации по работе с SQL Server для перемещения базы данных содержимого на устройство StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2c191-138">Then, use established SQL Server best practices to migrate the content database to the StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2c191-139">Перемещение базы данных содержимого на устройство поддерживается только для устройств серии StorSimple 8000 (функция не поддерживается для серий 5000 и 7000).</span><span class="sxs-lookup"><span data-stu-id="2c191-139">Moving the content database to the device is only supported for the StorSimple 8000 series (it is not supported for the 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="2c191-140">Если вы храните большие двоичные объекты и базы данных содержимого в разных томах на устройстве StorSimple, рекомендуется настроить их в том же контейнере томов.</span><span class="sxs-lookup"><span data-stu-id="2c191-140">If you store BLOBs and the content database in separate volumes on the StorSimple device, we recommend that you configure them in the same volume container.</span></span> <span data-ttu-id="2c191-141">Это гарантирует, что они будут подвергаться резервному копированию вместе.</span><span class="sxs-lookup"><span data-stu-id="2c191-141">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="2c191-142">Если RBS не включена, перемещать базу данных содержимого на устройство StorSimple не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="2c191-142">If you have not enabled RBS, we do not recommend moving the content database to the StorSimple device.</span></span> <span data-ttu-id="2c191-143">Эта конфигурация не тестировалась.</span><span class="sxs-lookup"><span data-stu-id="2c191-143">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="2c191-144">Перейдите к следующему шагу: [Настройка сборки мусора](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="2c191-144">Go to the next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
