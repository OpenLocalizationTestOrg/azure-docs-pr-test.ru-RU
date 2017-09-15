1. <span data-ttu-id="efa80-101">Откройте диспетчер пакетов SDK для Android, щелкнув значок на панели инструментов Android Studio или выбрав **Сервис** -> **Android** -> **SDK Manager** (Диспетчер пакетов SDK) в меню.</span><span class="sxs-lookup"><span data-stu-id="efa80-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span></span> <span data-ttu-id="efa80-102">Найдите нужную версию пакета SDK для Android, которая используется в проекте. Откройте ее, щелкнув **Show Package Details** (Отображать окно свойств пакета), и выберите **Google APIs** (Интерфейсы API Google), если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="efa80-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="efa80-103">Щелкните вкладку **Пакет инструментов SDK**.</span><span class="sxs-lookup"><span data-stu-id="efa80-103">Click the **SDK Tools** tab.</span></span> <span data-ttu-id="efa80-104">Если сервисы Google Play еще не установлены, щелкните **Google Play Services** (Сервисы Google Play), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="efa80-104">If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="efa80-105">Нажмите кнопку **Применить**, чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="efa80-105">Then click **Apply** to install.</span></span> 
   
    <span data-ttu-id="efa80-106">Запишите путь к пакету SDK. Он вам потребуется в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="efa80-106">Note the SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="efa80-107">Откройте файл **build.gradle** в каталоге приложения.</span><span class="sxs-lookup"><span data-stu-id="efa80-107">Open the **build.gradle** file in the app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="efa80-108">Добавьте следующую строку в *зависимости*:</span><span class="sxs-lookup"><span data-stu-id="efa80-108">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="efa80-109">Щелкните значок **Sync Project with Gradle Files** (Синхронизировать проект с файлами Gradle) на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="efa80-109">Click the **Sync Project with Gradle Files** icon in the tool bar.</span></span>
6. <span data-ttu-id="efa80-110">Откройте файл **AndroidManifest.xml** и добавьте этот тег к тегу *application* .</span><span class="sxs-lookup"><span data-stu-id="efa80-110">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

