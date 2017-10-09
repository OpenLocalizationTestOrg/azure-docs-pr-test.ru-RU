1. Откройте hello диспетчер Android SDK, щелкнув значок hello на hello инструментов Android Studio или щелкнув **средства** -> **Android** -> **SDK Manager**в меню "hello". Найдите целевую версию hello hello Android SDK, который используется в проекте, откройте его, нажав кнопку **Показать сведения о пакете**и выберите **Google API-интерфейсы**, если он еще не установлен.
2. Нажмите кнопку hello **средств SDK** вкладки. Если сервисы Google Play еще не установлены, щелкните **Google Play Services** (Сервисы Google Play), как показано ниже. Нажмите кнопку **применить** tooinstall. 
   
    Запомните путь пакета SDK для hello, для использования в дальнейшем. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Откройте hello **build.gradle** файл в каталоге приложения hello.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. Добавьте следующую строку в *зависимости*: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Нажмите кнопку hello **проекта синхронизации с файлами Gradle** значок на панели инструментов hello.
6. Откройте **AndroidManifest.xml** и добавьте этот тег toohello *приложения* тег.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

