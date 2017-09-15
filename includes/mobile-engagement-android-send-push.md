
### <a name="update-manifest-file-to-enable-notifications"></a><span data-ttu-id="b7419-101">Обновление файла манифеста для включения уведомлений</span><span class="sxs-lookup"><span data-stu-id="b7419-101">Update manifest file to enable notifications</span></span>
<span data-ttu-id="b7419-102">Скопируйте ресурсы обмена сообщениями внутри приложения в файл Manifest.xml между тегами `<application>` и `</application>`.</span><span class="sxs-lookup"><span data-stu-id="b7419-102">Copy the in-app messaging resources below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="b7419-103">Добавление значка для уведомлений</span><span class="sxs-lookup"><span data-stu-id="b7419-103">Specify an icon for notifications</span></span>
<span data-ttu-id="b7419-104">Вставьте следующий фрагмент XML-кода в файл Manifest.xml между тегами `<application>` и `</application>`.</span><span class="sxs-lookup"><span data-stu-id="b7419-104">Paste the following XML snippet in your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="b7419-105">Так вы определите значок, используемый в системных уведомлениях и уведомлениях в приложении.</span><span class="sxs-lookup"><span data-stu-id="b7419-105">This defines the icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="b7419-106">Это необязательно для уведомлений в приложении, но обязательно для системных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b7419-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="b7419-107">Система Android отклоняет системные уведомления с недопустимыми значками.</span><span class="sxs-lookup"><span data-stu-id="b7419-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="b7419-108">Убедитесь, что вы используете значок, который находится в одной из **папок с рисунками**, например ``engagement_close.png``.</span><span class="sxs-lookup"><span data-stu-id="b7419-108">Make sure you are using an icon that exists in one of the **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="b7419-109">**mipmap** не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b7419-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="b7419-110">Не следует использовать значок **запуска** .</span><span class="sxs-lookup"><span data-stu-id="b7419-110">You should not use the **launcher** icon.</span></span> <span data-ttu-id="b7419-111">Он имеет другое разрешение и, как правило, находится в неподдерживаемых папках MIP-карт.</span><span class="sxs-lookup"><span data-stu-id="b7419-111">It has a different resolution and is usually in the mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="b7419-112">В реальных приложениях следует использовать значок, который подходит для уведомлений в соответствии с [рекомендациями по разработке для Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="b7419-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="b7419-113">Чтобы правильно выбрать разрешение значка, ознакомьтесь с [этими примерами](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="b7419-113">To be sure to use correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="b7419-114">Прокрутите страницу вниз до раздела **Notification** (Уведомления), щелкните значок и выберите команду `PNGS`, чтобы скачать набор рисунков.</span><span class="sxs-lookup"><span data-stu-id="b7419-114">Scroll down to the **Notification** section, click an icon, and then click `PNGS` to download the icon drawable set.</span></span> <span data-ttu-id="b7419-115">Вы увидите, какие папки рисунков и с каким разрешением следует использовать для каждой версии значка.</span><span class="sxs-lookup"><span data-stu-id="b7419-115">You can see what drawable folders with which resolution to use for each version of the icon.</span></span>
> 
> 

### <a name="enable-your-app-to-receive-gcm-push-notifications"></a><span data-ttu-id="b7419-116">Настройка приложения для приема push-уведомлений GCM</span><span class="sxs-lookup"><span data-stu-id="b7419-116">Enable your app to receive GCM push notifications</span></span>
1. <span data-ttu-id="b7419-117">После замены **идентификатора отправителя**, полученного из консоли проекта Firebase, вставьте следующий код в файл Manifest.xml между тегами `<application>` и `</application>`.</span><span class="sxs-lookup"><span data-stu-id="b7419-117">Paste the following into your Manifest.xml between the `<application>` and `</application>` tags after replacing the **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="b7419-118">Перенос строки (\n) указан преднамеренно, поэтому добавьте его в конец номера проекта.</span><span class="sxs-lookup"><span data-stu-id="b7419-118">The \n is intentional so make sure that you end the project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="b7419-119">Вставьте приведенный ниже код в Manifest.xml между тегами `<application>` и `</application>`.</span><span class="sxs-lookup"><span data-stu-id="b7419-119">Paste the code below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span> <span data-ttu-id="b7419-120">Замените имя пакета <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="b7419-120">Replace the package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="b7419-121">Добавьте последний выделенный набор разрешений перед тегом `<application>` .</span><span class="sxs-lookup"><span data-stu-id="b7419-121">Add the last set of permissions that are highlighted before the `<application>` tag.</span></span> <span data-ttu-id="b7419-122">Замените `<Your package name>` фактическим именем пакета вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b7419-122">Replace `<Your package name>` by the actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

