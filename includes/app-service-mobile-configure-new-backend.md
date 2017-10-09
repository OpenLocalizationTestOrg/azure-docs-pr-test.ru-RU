
1. Нажмите кнопку hello **службы приложений** кнопку выберите вашей серверной части мобильных приложений, выберите **краткое руководство**и затем выберите клиентскую платформу (iOS, Android, Xamarin, Cordova).

    ![Портал Azure с выделенным пунктом "Mobile Apps Quickstart" (Быстрый запуск мобильных приложений)][quickstart]

2. Если подключение к базе данных не настроена, создайте, выполнив hello ниже:

    ![Портал Azure с toodatabase подключения мобильных приложений][connect]

    а. Создайте сервер и базу данных SQL.

    ![Создание базы данных и сервера для мобильных приложений на портале Azure][server]

    b. Подождите, пока подключение к данным hello успешно создан.

    ![Уведомление портала Azure об успешном создании подключения к данным][notification]

    c. Подключение к данным должно быть успешными.

    ![Уведомление на портале Azure: "Уже имеется подключение к данным"][already-connection]

3. В разделе **2. Создание API таблицы** выберите **язык серверной части** — Node.js. 
 
4. Примите hello подтверждения, а затем выберите **таблицы TodoItem создания**.  
    В базе данных будет создана таблица с элементами списка дел. 

    >[!IMPORTANT]
    > Переключение существующей серверной части tooNode.js перезаписывает все содержимое. серверной части .NET см. Вместо этого toocreate [работать с сервером hello серверной части .NET SDK для мобильных приложений][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
