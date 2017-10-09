

## <a name="generate-hello-certificate-signing-request-file"></a>Создать файл запроса подписи сертификата hello
Hello Apple Push Notification Service (APNS) использует tooauthenticate сертификатов push-уведомлений. Выполните эти инструкции toosend toocreate hello необходимые принудительной сертификата и получать уведомления. Дополнительные сведения об этих возможностях см официальные hello [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) документации.

Создать файл запрос подписи сертификата (CSR) hello, являющийся используемые Apple toogenerate сертификат знаком push.

1. На компьютере Mac запустите hello средство доступа к цепочке ключей. Его можно открыть из hello **программы** папки или hello **других** папку на панель запуска hello.
2. Щелкните **Keychain Access**, разверните **Certificate Assistant** (Помощник по сертификатам), а затем выберите **Request a Certificate from a Certificate Authority...** (Запросить сертификат в центре сертификации...).
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Выберите ваш **адреса электронной почты пользователя** и **общее имя** , убедитесь, что **сохранить toodisk** выбран и нажмите кнопку **Продолжить**. Оставьте hello **адрес электронной почты ЦС** поле пустым, поскольку она не является обязательным.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Введите имя для файла запрос подписи сертификата (CSR) hello в **Сохранить как**, выберите расположение hello в **где**, нажмите кнопку **Сохранить**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      Это экономит hello CSR-файл в расположение hello выбран; расположение по умолчанию Hello имеет hello рабочего стола. Не забывайте hello местоположения, выбранного для этого файла.

Далее будет зарегистрировать приложение с помощью Apple, включить push-уведомления и передать этот экспортированный CSR toocreate сертификат push.

## <a name="register-your-app-for-push-notifications"></a>Регистрация приложения для работы с push-уведомлениями
toobe может toosend принудительной уведомления tooan приложения iOS, необходимо зарегистрировать приложение в Apple, а также зарегистрировать push-уведомления.  

1. Если приложение еще не зарегистрирован, перейдите в папку toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">портал Провизионирования iOS</a> hello Центр разработчиков Apple, войдите в систему с Идентификатором Apple, нажмите кнопку **идентификаторы**, нажмите кнопку **идентификаторы приложений** , а затем щелкните на hello  **+**  входа tooregister новое приложение.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Обновите следующие три поля для нового приложения hello и нажмите кнопку **Продолжить**:
   
   * **Имя**: Введите описательное имя для вашего приложения в hello **имя** в hello **описания идентификатор приложения** раздела.
   * **Идентификатор**: в списке hello **явный идентификатор приложения** введите **идентификатор пакета** в форме hello `<Organization Identifier>.<Product Name>` как упоминалось в hello [распространения приложений Руководство по](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Hello *идентификатор организации* и *название продукта* использовать должен соответствовать hello идентификатор организации и название продукта, которые будут использоваться при создании проекта XCode. В ниже screeshot hello *NotificationHubs* используется как идентификатор организации и *GetStarted* используется как имя продукта hello. Убедившись, что он соответствует hello значения, которые будет использовать в своем проекте XCode позволит вам toouse hello правильный профиль публикации с XCode. 
   * **Push-уведомления**: hello проверка **Push-уведомления** параметр в hello **службы приложений** разделе.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      Это приводит к возникновению ошибки ваш код приложения и просит вас сведения tooconfirm hello. Нажмите кнопку **зарегистрировать** tooconfirm hello новый идентификатор приложения.
     
      После нажатия кнопки **зарегистрировать**, вы увидите hello **завершения регистрации** экрана, как показано ниже. Нажмите кнопку **Done**(Готово).
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. Найдите идентификатор приложения hello, который вы только что созданного и щелкните его строку hello Центр разработчиков, в разделе идентификаторы приложений.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Щелкнув идентификатор приложения hello будут отображаться сведения о приложении hello. Нажмите кнопку hello **изменить** кнопку в нижней части hello.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Прокрутите toohello внизу экрана приветствия и нажмите кнопку hello **Создание сертификата...**  кнопки в разделе "hello" **разработки Push SSL-сертификат**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      При этом отображаются помощника «Добавить iOS сертификат» hello.
   
   > [!NOTE]
   > В этом учебнике используется сертификат разработки. Hello же процесс используется при регистрации сертификат производства. Просто убедитесь, что используется hello же тип сертификата, при отправке уведомлений.
   > 
   > 
3. Нажмите кнопку **выбрать файл**, поиск toohello расположения, где был сохранен hello CSR-файл, созданный в первой задаче hello, а затем нажмите кнопку **формирования**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. После создания сертификата hello hello портала щелкните hello **загрузки** и нажмите кнопку **сделать**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Это загружает сертификат hello и сохраняет его tooyour компьютере в папке загрузок.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > По умолчанию файл с именем сертификата разработки загружен hello **aps_development.cer**.
   > 
   > 
5. Дважды щелкните загруженный принудительной сертификат hello **aps_development.cer**.
   
      При этом устанавливаются hello новый сертификат в цепочке ключей, hello, как показано ниже:
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > Имя Hello в сертификатов может отличаться, но он будет иметь префикс **разработки Apple iOS служб Push-:**.
   > 
   > 
6. Доступ к цепочке ключей, щелкните правой кнопкой мыши hello новый принудительной сертификат, созданный в hello **сертификаты** категории. Нажмите кнопку **Экспорт**, имя файла hello, выберите hello **.p12** форматирования, а затем нажмите кнопку **Сохранить**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Сделать заметку hello имя файла и расположение hello .p12 экспортированного сертификата. Оно будет использоваться tooenable проверки подлинности в APNS.
   
   > [!NOTE]
   > В этом учебнике создается файл Quickstart.p12. Имя файла и расположение могут отличаться.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Создайте подготовительный профиль для приложения hello
1. В hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">портал Провизионирования iOS</a>выберите **профили подготовки**выберите **все**и нажмите кнопку hello  **+**  Кнопка toocreate профиля. Будет запущен hello **добавить профиль Provisiong iOS** мастера
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Выберите **разработки приложений iOS** под **разработки** тип профиля provisiong hello и нажмите кнопку **Продолжить**. 
3. Затем выберите только что созданному hello идентификатор приложения hello **идентификатор приложения** раскрывающегося списка и нажмите кнопку **продолжить**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. В hello **выберите сертификаты** экране обычные разработки сертификат для подписи кода и нажмите кнопку **Продолжить**. Это не hello принудительной сертификат, который вы только что создали.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. Затем выберите hello **устройств** toouse тестирование, а затем щелкните **продолжить**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Наконец, выберите имя для профиля hello в **имя профиля**, нажмите кнопку **формирования**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Когда создается новый профиль подготовки hello щелкните toodownload, его и установить его на компьютере разработки Xcode. Затем нажмите кнопку **Done**(Готово).
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
