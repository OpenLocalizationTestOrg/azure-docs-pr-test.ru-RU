#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Настройка проекта iOS hello в Xamarin Studio
1. В Xamarin.Studio, откройте **Info.plist**и обновление hello **идентификатор пакета** с hello объединить идентификатор, созданный ранее с свой новый идентификатор приложения.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Прокрутите список вниз слишком**фоновые режимы**. Выберите hello **Включение фоновых режимов** поле и hello **удаленного уведомления** поле.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Дважды щелкните проект в tooopen панель решения hello **параметры проекта**.
4. В разделе **построения**, выберите **подписывание пакета iOS**и выберите hello соответствующих идентификаторов и подготовительный профиль можно просто настроить для этого проекта.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   Это гарантирует, что этот проект hello использует hello новый профиль для подписи кода. Hello подготовки документации официальный устройств Xamarin, в разделе [Xamarin подготовки устройств].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Настроить проект iOS hello в Visual Studio
1. В Visual Studio, щелкните правой кнопкой мыши проект hello и нажмите кнопку **свойства**.
2. На страницах свойств hello выберите hello **приложение iOS** вкладка и обновление hello **идентификатор** с Идентификатором hello, которое было создано ранее.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. В hello **подписывание пакета iOS** вкладке, выберите hello соответствующих идентификаторов и подготовки вы просто набор профилей вверх для этого проекта.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    Это гарантирует, что этот проект hello использует hello новый профиль для подписи кода. Hello подготовки документации официальный устройств Xamarin, в разделе [Xamarin подготовки устройств].
4. Дважды щелкните Info.plist tooopen и затем включите **RemoteNotifications** под **фоновые режимы**.

[Xamarin подготовки устройств]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/ (Подготовка устройства)
