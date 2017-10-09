
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="84144-101">Обновить файл манифеста tooenable уведомления</span><span class="sxs-lookup"><span data-stu-id="84144-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="84144-102">Скопируйте hello ресурсов обмена сообщениями в приложении ниже в вашей Manifest.xml между hello `<application>` и `</application>` тегов.</span><span class="sxs-lookup"><span data-stu-id="84144-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="84144-103">Добавление значка для уведомлений</span><span class="sxs-lookup"><span data-stu-id="84144-103">Specify an icon for notifications</span></span>
<span data-ttu-id="84144-104">Следующий фрагмент XML в вашей Manifest.xml между hello hello вставить `<application>` и `</application>` тегов.</span><span class="sxs-lookup"><span data-stu-id="84144-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="84144-105">Этот параметр определяет hello значка, отображаемого в системе и уведомления в приложения.</span><span class="sxs-lookup"><span data-stu-id="84144-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="84144-106">Это необязательно для уведомлений в приложении, но обязательно для системных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="84144-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="84144-107">Система Android отклоняет системные уведомления с недопустимыми значками.</span><span class="sxs-lookup"><span data-stu-id="84144-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="84144-108">Убедитесь, что вы используете значок, который существует в одном из hello **drawable** папок (например ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="84144-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="84144-109">**mipmap** не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="84144-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="84144-110">Не следует использовать hello **запуска** значок.</span><span class="sxs-lookup"><span data-stu-id="84144-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="84144-111">Он имеет другое разрешение и обычно в папках hello MIP-карт, которые не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="84144-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="84144-112">В реальных приложениях следует использовать значок, который подходит для уведомлений в соответствии с [рекомендациями по разработке для Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="84144-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="84144-113">убедиться, что toouse toobe правильное разрешение значок, можно взглянуть на [эти примеры](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="84144-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="84144-114">Прокрутите вниз toohello **уведомления** статьи, щелкните значок и выберите `PNGS` drawable набора toodownload hello значков.</span><span class="sxs-lookup"><span data-stu-id="84144-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="84144-115">Вы увидите drawable папки с toouse какие разрешения для каждой версии значок hello.</span><span class="sxs-lookup"><span data-stu-id="84144-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="84144-116">Включить вашего приложения tooreceive GCM push-уведомления</span><span class="sxs-lookup"><span data-stu-id="84144-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="84144-117">Вставьте следующие hello в вашей Manifest.xml между hello `<application>` и `</application>` тегов после замены hello **идентификатор отправителя** получить консоли с помощью Firebase проекта.</span><span class="sxs-lookup"><span data-stu-id="84144-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="84144-118">Hello \n преднамеренного поэтому убедитесь, что завершения проекта hello чисел с ним.</span><span class="sxs-lookup"><span data-stu-id="84144-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="84144-119">Вставить ниже код hello в вашей Manifest.xml между hello `<application>` и `</application>` тегов.</span><span class="sxs-lookup"><span data-stu-id="84144-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="84144-120">Замените имя пакета hello <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="84144-120">Replace hello package name <Your package name>.</span></span>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. <span data-ttu-id="84144-121">Добавить hello последний набор разрешений, которые выделены перед hello `<application>` тег.</span><span class="sxs-lookup"><span data-stu-id="84144-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="84144-122">Замените `<Your package name>` по имени hello сам пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="84144-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

