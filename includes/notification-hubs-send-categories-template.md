
<span data-ttu-id="0aeb9-101">В этом разделе показано, как toosend новости, как пометить шаблон уведомления из консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="0aeb9-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="0aeb9-102">При использовании мобильных приложений можно найти toohello [Добавление push-уведомлений для мобильных приложений] учебника и выбрать платформу вверху hello.</span><span class="sxs-lookup"><span data-stu-id="0aeb9-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="0aeb9-103">Toouse Java или PHP см. слишком[как концентраторы уведомлений из Java и PHP toouse].</span><span class="sxs-lookup"><span data-stu-id="0aeb9-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="0aeb9-104">Можно отправлять уведомления из любого серверного компонента с помощью [интерфейса REST Центров уведомлений].</span><span class="sxs-lookup"><span data-stu-id="0aeb9-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="0aeb9-105">Пропустите шаги 1 – 3, при создании консольного приложения hello для отправки уведомлений, завершения [приступить к работе с концентраторами уведомлений].</span><span class="sxs-lookup"><span data-stu-id="0aeb9-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="0aeb9-106">В Visual Studio создайте новое консольное приложение Visual C#:</span><span class="sxs-lookup"><span data-stu-id="0aeb9-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="0aeb9-107">В главном меню Visual Studio hello, щелкните **средства**, **диспетчер пакетов библиотеки**, и **консоль диспетчера пакетов**, затем в окне консоли hello введите следующую команду и нажмите клавишу **Введите**:</span><span class="sxs-lookup"><span data-stu-id="0aeb9-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="0aeb9-108">При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello [пакет NuGet концентраторов Microsoft.Azure.Notification].</span><span class="sxs-lookup"><span data-stu-id="0aeb9-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="0aeb9-109">Откройте файл hello Program.cs и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="0aeb9-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="0aeb9-110">В hello `Program` класса, добавьте следующий метод hello или заменить его, если он уже существует:</span><span class="sxs-lookup"><span data-stu-id="0aeb9-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
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
   
    <span data-ttu-id="0aeb9-111">Этот код отправляет уведомление шаблона для каждого из шести тегов hello в массив строк hello.</span><span class="sxs-lookup"><span data-stu-id="0aeb9-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="0aeb9-112">Hello использование тегов гарантирует, что устройства получать уведомления только для зарегистрированных hello категорий.</span><span class="sxs-lookup"><span data-stu-id="0aeb9-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="0aeb9-113">В hello над кодом, замените hello `<hub name>` и `<connection string with full access>` местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultFullSharedAccessSignature* из панели мониторинга hello центра уведомлений .</span><span class="sxs-lookup"><span data-stu-id="0aeb9-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="0aeb9-114">Добавьте следующие строки в hello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="0aeb9-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="0aeb9-115">Построение консольного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0aeb9-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[приступить к работе с концентраторами уведомлений]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[интерфейса REST Центров уведомлений]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx (REST API Центров уведомлений)
[Добавление push-уведомлений для мобильных приложений]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[как концентраторы уведомлений из Java и PHP toouse]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[пакет NuGet концентраторов Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/ (Центры уведомлений Microsoft Azure 1.0.7)
