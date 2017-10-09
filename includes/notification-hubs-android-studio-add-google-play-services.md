1. <span data-ttu-id="fd60d-101">Откройте hello диспетчер Android SDK, щелкнув значок hello на hello инструментов Android Studio или щелкнув **средства** -> **Android** -> **SDK Manager**в меню "hello".</span><span class="sxs-lookup"><span data-stu-id="fd60d-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="fd60d-102">Найдите целевую версию hello hello Android SDK, который используется в проекте, откройте его, нажав кнопку **Показать сведения о пакете**и выберите **Google API-интерфейсы**, если он еще не установлен.</span><span class="sxs-lookup"><span data-stu-id="fd60d-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="fd60d-103">Нажмите кнопку hello **средств SDK** вкладки. Если сервисы Google Play еще не установлены, щелкните **Google Play Services** (Сервисы Google Play), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fd60d-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="fd60d-104">Нажмите кнопку **применить** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="fd60d-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="fd60d-105">Запомните путь пакета SDK для hello, для использования в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="fd60d-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="fd60d-106">Откройте hello **build.gradle** файл в каталоге приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fd60d-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="fd60d-107">Добавьте следующую строку в *зависимости*:</span><span class="sxs-lookup"><span data-stu-id="fd60d-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="fd60d-108">Нажмите кнопку hello **проекта синхронизации с файлами Gradle** значок на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="fd60d-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="fd60d-109">Откройте **AndroidManifest.xml** и добавьте этот тег toohello *приложения* тег.</span><span class="sxs-lookup"><span data-stu-id="fd60d-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

