

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="f8309-101">Создать файл запроса подписи сертификата hello</span><span class="sxs-lookup"><span data-stu-id="f8309-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="f8309-102">Hello Apple Push Notification Service (APNS) использует tooauthenticate сертификатов push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f8309-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="f8309-103">Выполните эти инструкции toosend toocreate hello необходимые принудительной сертификата и получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="f8309-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="f8309-104">Дополнительные сведения об этих возможностях см официальные hello [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) документации.</span><span class="sxs-lookup"><span data-stu-id="f8309-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="f8309-105">Создать файл запрос подписи сертификата (CSR) hello, являющийся используемые Apple toogenerate сертификат знаком push.</span><span class="sxs-lookup"><span data-stu-id="f8309-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="f8309-106">На компьютере Mac запустите hello средство доступа к цепочке ключей.</span><span class="sxs-lookup"><span data-stu-id="f8309-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="f8309-107">Его можно открыть из hello **программы** папки или hello **других** папку на панель запуска hello.</span><span class="sxs-lookup"><span data-stu-id="f8309-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="f8309-108">Щелкните **Keychain Access**, разверните **Certificate Assistant** (Помощник по сертификатам), а затем выберите **Request a Certificate from a Certificate Authority...** (Запросить сертификат в центре сертификации...).</span><span class="sxs-lookup"><span data-stu-id="f8309-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="f8309-109">Выберите ваш **адреса электронной почты пользователя** и **общее имя** , убедитесь, что **сохранить toodisk** выбран и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="f8309-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="f8309-110">Оставьте hello **адрес электронной почты ЦС** поле пустым, поскольку она не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="f8309-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="f8309-111">Введите имя для файла запрос подписи сертификата (CSR) hello в **Сохранить как**, выберите расположение hello в **где**, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f8309-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="f8309-112">Это экономит hello CSR-файл в расположение hello выбран; расположение по умолчанию Hello имеет hello рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="f8309-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="f8309-113">Не забывайте hello местоположения, выбранного для этого файла.</span><span class="sxs-lookup"><span data-stu-id="f8309-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="f8309-114">Далее будет зарегистрировать приложение с помощью Apple, включить push-уведомления и передать этот экспортированный CSR toocreate сертификат push.</span><span class="sxs-lookup"><span data-stu-id="f8309-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="f8309-115">Регистрация приложения для работы с push-уведомлениями</span><span class="sxs-lookup"><span data-stu-id="f8309-115">Register your app for push notifications</span></span>
<span data-ttu-id="f8309-116">toobe может toosend принудительной уведомления tooan приложения iOS, необходимо зарегистрировать приложение в Apple, а также зарегистрировать push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="f8309-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="f8309-117">Если приложение еще не зарегистрирован, перейдите в папку toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">портал Провизионирования iOS</a> hello Центр разработчиков Apple, войдите в систему с Идентификатором Apple, нажмите кнопку **идентификаторы**, нажмите кнопку **идентификаторы приложений** , а затем щелкните на hello  **+**  входа tooregister новое приложение.</span><span class="sxs-lookup"><span data-stu-id="f8309-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="f8309-118">Обновите следующие три поля для нового приложения hello и нажмите кнопку **Продолжить**:</span><span class="sxs-lookup"><span data-stu-id="f8309-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="f8309-119">**Имя**: Введите описательное имя для вашего приложения в hello **имя** в hello **описания идентификатор приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="f8309-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="f8309-120">**Идентификатор**: в списке hello **явный идентификатор приложения** введите **идентификатор пакета** в форме hello `<Organization Identifier>.<Product Name>` как упоминалось в hello [распространения приложений Руководство по](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="f8309-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="f8309-121">Hello *идентификатор организации* и *название продукта* использовать должен соответствовать hello идентификатор организации и название продукта, которые будут использоваться при создании проекта XCode.</span><span class="sxs-lookup"><span data-stu-id="f8309-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="f8309-122">В ниже screeshot hello *NotificationHubs* используется как идентификатор организации и *GetStarted* используется как имя продукта hello.</span><span class="sxs-lookup"><span data-stu-id="f8309-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="f8309-123">Убедившись, что он соответствует hello значения, которые будет использовать в своем проекте XCode позволит вам toouse hello правильный профиль публикации с XCode.</span><span class="sxs-lookup"><span data-stu-id="f8309-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="f8309-124">**Push-уведомления**: hello проверка **Push-уведомления** параметр в hello **службы приложений** разделе.</span><span class="sxs-lookup"><span data-stu-id="f8309-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="f8309-125">Это приводит к возникновению ошибки ваш код приложения и просит вас сведения tooconfirm hello.</span><span class="sxs-lookup"><span data-stu-id="f8309-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="f8309-126">Нажмите кнопку **зарегистрировать** tooconfirm hello новый идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="f8309-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="f8309-127">После нажатия кнопки **зарегистрировать**, вы увидите hello **завершения регистрации** экрана, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f8309-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="f8309-128">Нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="f8309-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="f8309-129">Найдите идентификатор приложения hello, который вы только что созданного и щелкните его строку hello Центр разработчиков, в разделе идентификаторы приложений.</span><span class="sxs-lookup"><span data-stu-id="f8309-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="f8309-130">Щелкнув идентификатор приложения hello будут отображаться сведения о приложении hello.</span><span class="sxs-lookup"><span data-stu-id="f8309-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="f8309-131">Нажмите кнопку hello **изменить** кнопку в нижней части hello.</span><span class="sxs-lookup"><span data-stu-id="f8309-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="f8309-132">Прокрутите toohello внизу экрана приветствия и нажмите кнопку hello **Создание сертификата...**  кнопки в разделе "hello" **разработки Push SSL-сертификат**.</span><span class="sxs-lookup"><span data-stu-id="f8309-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="f8309-133">При этом отображаются помощника «Добавить iOS сертификат» hello.</span><span class="sxs-lookup"><span data-stu-id="f8309-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f8309-134">В этом учебнике используется сертификат разработки.</span><span class="sxs-lookup"><span data-stu-id="f8309-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="f8309-135">Hello же процесс используется при регистрации сертификат производства.</span><span class="sxs-lookup"><span data-stu-id="f8309-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="f8309-136">Просто убедитесь, что используется hello же тип сертификата, при отправке уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f8309-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="f8309-137">Нажмите кнопку **выбрать файл**, поиск toohello расположения, где был сохранен hello CSR-файл, созданный в первой задаче hello, а затем нажмите кнопку **формирования**.</span><span class="sxs-lookup"><span data-stu-id="f8309-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="f8309-138">После создания сертификата hello hello портала щелкните hello **загрузки** и нажмите кнопку **сделать**.</span><span class="sxs-lookup"><span data-stu-id="f8309-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="f8309-139">Это загружает сертификат hello и сохраняет его tooyour компьютере в папке загрузок.</span><span class="sxs-lookup"><span data-stu-id="f8309-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="f8309-140">По умолчанию файл с именем сертификата разработки загружен hello **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="f8309-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="f8309-141">Дважды щелкните загруженный принудительной сертификат hello **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="f8309-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="f8309-142">При этом устанавливаются hello новый сертификат в цепочке ключей, hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="f8309-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="f8309-143">Имя Hello в сертификатов может отличаться, но он будет иметь префикс **разработки Apple iOS служб Push-:**.</span><span class="sxs-lookup"><span data-stu-id="f8309-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="f8309-144">Доступ к цепочке ключей, щелкните правой кнопкой мыши hello новый принудительной сертификат, созданный в hello **сертификаты** категории.</span><span class="sxs-lookup"><span data-stu-id="f8309-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="f8309-145">Нажмите кнопку **Экспорт**, имя файла hello, выберите hello **.p12** форматирования, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f8309-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="f8309-146">Сделать заметку hello имя файла и расположение hello .p12 экспортированного сертификата.</span><span class="sxs-lookup"><span data-stu-id="f8309-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="f8309-147">Оно будет использоваться tooenable проверки подлинности в APNS.</span><span class="sxs-lookup"><span data-stu-id="f8309-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f8309-148">В этом учебнике создается файл Quickstart.p12.</span><span class="sxs-lookup"><span data-stu-id="f8309-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="f8309-149">Имя файла и расположение могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="f8309-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="f8309-150">Создайте подготовительный профиль для приложения hello</span><span class="sxs-lookup"><span data-stu-id="f8309-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="f8309-151">В hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">портал Провизионирования iOS</a>выберите **профили подготовки**выберите **все**и нажмите кнопку hello  **+**  Кнопка toocreate профиля.</span><span class="sxs-lookup"><span data-stu-id="f8309-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="f8309-152">Будет запущен hello **добавить профиль Provisiong iOS** мастера</span><span class="sxs-lookup"><span data-stu-id="f8309-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="f8309-153">Выберите **разработки приложений iOS** под **разработки** тип профиля provisiong hello и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="f8309-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="f8309-154">Затем выберите только что созданному hello идентификатор приложения hello **идентификатор приложения** раскрывающегося списка и нажмите кнопку **продолжить**</span><span class="sxs-lookup"><span data-stu-id="f8309-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="f8309-155">В hello **выберите сертификаты** экране обычные разработки сертификат для подписи кода и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="f8309-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="f8309-156">Это не hello принудительной сертификат, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="f8309-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="f8309-157">Затем выберите hello **устройств** toouse тестирование, а затем щелкните **продолжить**</span><span class="sxs-lookup"><span data-stu-id="f8309-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="f8309-158">Наконец, выберите имя для профиля hello в **имя профиля**, нажмите кнопку **формирования**.</span><span class="sxs-lookup"><span data-stu-id="f8309-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="f8309-159">Когда создается новый профиль подготовки hello щелкните toodownload, его и установить его на компьютере разработки Xcode.</span><span class="sxs-lookup"><span data-stu-id="f8309-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="f8309-160">Затем нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="f8309-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
