
1. <span data-ttu-id="69643-101">В hello представление решения (или **обозреватель решений** в Visual Studio), щелкните правой кнопкой мыши hello **компоненты** папку, нажмите кнопку **получить более компонентов...** , поиск hello **клиент обмена сообщениями Google облака** компонента и добавьте его в проект toohello.</span><span class="sxs-lookup"><span data-stu-id="69643-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="69643-102">Откройте файл проекта ToDoActivity.cs hello и добавьте следующее hello с помощью класса toohello инструкции:</span><span class="sxs-lookup"><span data-stu-id="69643-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="69643-103">В hello **ToDoActivity** добавьте hello, следуя новый код:</span><span class="sxs-lookup"><span data-stu-id="69643-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="69643-104">Это позволяет tooaccess hello мобильного клиента экземпляра процесса службы обработчика принудительной hello.</span><span class="sxs-lookup"><span data-stu-id="69643-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="69643-105">Добавьте следующий код toohello hello **OnCreate** метод после hello **MobileServiceClient** создается:</span><span class="sxs-lookup"><span data-stu-id="69643-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="69643-106">Ваш класс **ToDoActivity** теперь готов для добавления push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="69643-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

