
1. <span data-ttu-id="19f83-101">На [портале Azure](https://portal.azure.com/) щелкните **Просмотреть все** > **Службы приложений**, а затем выберите серверную часть своего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="19f83-101">In the [Azure portal](https://portal.azure.com/), click **Browse All** > **App Services**, and then click your Mobile Apps back end.</span></span> <span data-ttu-id="19f83-102">В разделе **Параметры** щелкните **App Service Push** (Push-уведомления службы приложений) и выберите имя центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="19f83-102">Under **Settings**, click **App Service Push**, and then click your notification hub name.</span></span>
2. <span data-ttu-id="19f83-103">Выберите **Google (GCM)**, введите значение **ключа сервера**, полученное от Firebase в ходе предыдущей процедуры, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="19f83-103">Go to **Google (GCM)**, enter the **Server Key** value that you obtained from Firebase in the previous procedure, and then click **Save**.</span></span>

    ![Задание ключа GCM API на портале](./media/app-service-mobile-android-configure-push/mobile-push-api-key.png)

<span data-ttu-id="19f83-105">Теперь серверная часть вашего мобильного приложения настроена для использования Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="19f83-105">The Mobile Apps back end is now configured to use Firebase Cloud Messaging.</span></span> <span data-ttu-id="19f83-106">Это позволяет отправлять push-уведомления приложению Android через центр уведомлений.</span><span class="sxs-lookup"><span data-stu-id="19f83-106">This enables you to send push notifications to your app running on an Android device, by using the notification hub.</span></span>

<!-- URLs. -->


<!-- images -->
