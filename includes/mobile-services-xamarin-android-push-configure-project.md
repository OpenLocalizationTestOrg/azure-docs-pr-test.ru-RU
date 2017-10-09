
1. В hello представление решения (или **обозреватель решений** в Visual Studio), щелкните правой кнопкой мыши hello **компоненты** папку, нажмите кнопку **получить более компонентов...** , поиск hello **клиент обмена сообщениями Google облака** компонента и добавьте его в проект toohello.
2. Откройте файл проекта ToDoActivity.cs hello и добавьте следующее hello с помощью класса toohello инструкции:
   
        using Gcm.Client;
3. В hello **ToDoActivity** добавьте hello, следуя новый код: 
   
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
   
    Это позволяет tooaccess hello мобильного клиента экземпляра процесса службы обработчика принудительной hello.
4. Добавьте следующий код toohello hello **OnCreate** метод после hello **MobileServiceClient** создается:
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

Ваш класс **ToDoActivity** теперь готов для добавления push-уведомлений.

