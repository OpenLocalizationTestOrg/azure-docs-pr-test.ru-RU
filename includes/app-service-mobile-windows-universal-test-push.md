
1. <span data-ttu-id="5693b-101">Щелкните правой кнопкой мыши проект Магазина Windows, выберите пункт **Назначить запускаемым проектом**и нажмите клавишу F5, чтобы запустить приложение Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="5693b-101">Right-click the Windows Store project, click **Set as StartUp Project**, then press the F5 key to run the Windows Store app.</span></span>
   
    <span data-ttu-id="5693b-102">После запуска приложения выполняется регистрация устройства для получения push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="5693b-102">After the app starts, the device is registered for push notifications.</span></span>
2. <span data-ttu-id="5693b-103">Остановите приложение Магазина Windows и повторите предыдущий шаг для приложения Магазина Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="5693b-103">Stop the Windows Store app and repeat the previous step for the Windows Phone Store app.</span></span>
   
    <span data-ttu-id="5693b-104">Теперь оба устройства зарегистрированы для получения push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="5693b-104">At this point, both devices are registered to receive push notifications.</span></span>
3. <span data-ttu-id="5693b-105">Запустите приложение Магазина Windows и введите текст в поле **Insert a TodoItem** (Вставить TodoItem), после чего нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5693b-105">Run the Windows Store app again, and type text in **Insert a TodoItem**, and then click **Save**.</span></span>
   
       Note that after the insert completes, both the Windows Store and the Windows Phone apps receive a push notification from WNS. The notification is displayed on Windows Phone even when the app isn't running.
   
       ![](./media/app-service-mobile-windows-universal-test-push/mobile-quickstart-push5-wp8.png)

