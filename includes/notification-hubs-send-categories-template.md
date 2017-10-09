
В этом разделе показано, как toosend новости, как пометить шаблон уведомления из консольного приложения .NET.

При использовании мобильных приложений можно найти toohello [Добавление push-уведомлений для мобильных приложений] учебника и выбрать платформу вверху hello.

Toouse Java или PHP см. слишком[как концентраторы уведомлений из Java и PHP toouse]. Можно отправлять уведомления из любого серверного компонента с помощью [интерфейса REST Центров уведомлений].

Пропустите шаги 1 – 3, при создании консольного приложения hello для отправки уведомлений, завершения [приступить к работе с концентраторами уведомлений].

1. В Visual Studio создайте новое консольное приложение Visual C#:
   
       ![][13]
2. В главном меню Visual Studio hello, щелкните **средства**, **диспетчер пакетов библиотеки**, и **консоль диспетчера пакетов**, затем в окне консоли hello введите следующую команду и нажмите клавишу **Введите**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello [пакет NuGet концентраторов Microsoft.Azure.Notification].
3. Откройте файл hello Program.cs и добавьте следующее hello `using` инструкции:
   
        using Microsoft.Azure.NotificationHubs;
4. В hello `Program` класса, добавьте следующий метод hello или заменить его, если он уже существует:
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    Этот код отправляет уведомление шаблона для каждого из шести тегов hello в массив строк hello. Hello использование тегов гарантирует, что устройства получать уведомления только для зарегистрированных hello категорий.
5. В hello над кодом, замените hello `<hub name>` и `<connection string with full access>` местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultFullSharedAccessSignature* из панели мониторинга hello центра уведомлений .
6. Добавьте следующие строки в hello hello **Main** метод:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Построение консольного приложения hello.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[приступить к работе с концентраторами уведомлений]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[интерфейса REST Центров уведомлений]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx (REST API Центров уведомлений)
[Добавление push-уведомлений для мобильных приложений]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[как концентраторы уведомлений из Java и PHP toouse]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[пакет NuGet концентраторов Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/ (Центры уведомлений Microsoft Azure 1.0.7)
