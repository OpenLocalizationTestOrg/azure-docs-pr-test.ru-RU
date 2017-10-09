
### <a name="update-manifest-file-tooenable-notifications"></a>Обновить файл манифеста tooenable уведомления
Скопируйте hello ресурсов обмена сообщениями в приложении ниже в вашей Manifest.xml между hello `<application>` и `</application>` тегов.

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

### <a name="specify-an-icon-for-notifications"></a>Добавление значка для уведомлений
Следующий фрагмент XML в вашей Manifest.xml между hello hello вставить `<application>` и `</application>` тегов.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Этот параметр определяет hello значка, отображаемого в системе и уведомления в приложения. Это необязательно для уведомлений в приложении, но обязательно для системных уведомлений. Система Android отклоняет системные уведомления с недопустимыми значками.

Убедитесь, что вы используете значок, который существует в одном из hello **drawable** папок (например ``engagement_close.png``). **mipmap** не поддерживается.

> [!NOTE]
> Не следует использовать hello **запуска** значок. Он имеет другое разрешение и обычно в папках hello MIP-карт, которые не поддерживаются.
> 
> 

В реальных приложениях следует использовать значок, который подходит для уведомлений в соответствии с [рекомендациями по разработке для Android](http://developer.android.com/design/patterns/notifications.html).

> [!TIP]
> убедиться, что toouse toobe правильное разрешение значок, можно взглянуть на [эти примеры](https://www.google.com/design/icons).
> Прокрутите вниз toohello **уведомления** статьи, щелкните значок и выберите `PNGS` drawable набора toodownload hello значков. Вы увидите drawable папки с toouse какие разрешения для каждой версии значок hello.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Включить вашего приложения tooreceive GCM push-уведомления
1. Вставьте следующие hello в вашей Manifest.xml между hello `<application>` и `</application>` тегов после замены hello **идентификатор отправителя** получить консоли с помощью Firebase проекта. Hello \n преднамеренного поэтому убедитесь, что завершения проекта hello чисел с ним.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Вставить ниже код hello в вашей Manifest.xml между hello `<application>` и `</application>` тегов. Замените имя пакета hello <Your package name>.
   
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
3. Добавить hello последний набор разрешений, которые выделены перед hello `<application>` тег. Замените `<Your package name>` по имени hello сам пакет приложения.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

