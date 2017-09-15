
<span data-ttu-id="afe5f-101">В этом разделе показано, как отправлять экстренные новости в виде шаблонных уведомлений с тегами из консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="afe5f-101">This section shows how to send breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="afe5f-102">Если вы используете мобильные приложения, см. руководство по [добавлению push-уведомлений в мобильные приложения] (выберите платформу в верхней части страницы).</span><span class="sxs-lookup"><span data-stu-id="afe5f-102">If you are using Mobile Apps please refer to the [Add push notifications for Mobile Apps] tutorial and select your platform at the top.</span></span>

<span data-ttu-id="afe5f-103">Если вы хотите использовать Java или PHP, см. руководство по [использованию Центров уведомлений из Java и PHP].</span><span class="sxs-lookup"><span data-stu-id="afe5f-103">If you want to use Java or PHP refer to [How to use Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="afe5f-104">Можно отправлять уведомления из любого серверного компонента с помощью [интерфейса REST Центров уведомлений].</span><span class="sxs-lookup"><span data-stu-id="afe5f-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="afe5f-105">Пропустите шаги 1–3, если консольное приложение для отправки уведомлений создано после завершения работы с руководством по [началу работы с Центрами уведомлений].</span><span class="sxs-lookup"><span data-stu-id="afe5f-105">Skip steps 1-3 if you created the console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="afe5f-106">В Visual Studio создайте новое консольное приложение Visual C#:</span><span class="sxs-lookup"><span data-stu-id="afe5f-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="afe5f-107">В главном меню Visual Studio выберите пункт **Сервис**, **Диспетчер пакетов библиотеки** и **Консоль диспетчера пакетов**, а затем в окне консоли введите следующую команду и нажмите клавишу **ВВОД**:</span><span class="sxs-lookup"><span data-stu-id="afe5f-107">In the Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in the console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="afe5f-108">После этого будет добавлена ссылка на пакет SDK для Центров уведомлений Azure с помощью [пакета NuGet Microsoft.Azure.Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="afe5f-108">This adds a reference to the Azure Notification Hubs SDK using the [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="afe5f-109">Откройте файл Program.cs и добавьте следующий оператор `using` :</span><span class="sxs-lookup"><span data-stu-id="afe5f-109">Open the file Program.cs and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="afe5f-110">В класс `Program` добавьте следующий метод или замените его, если он уже существует:</span><span class="sxs-lookup"><span data-stu-id="afe5f-110">In the `Program` class, add the following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending the notification as a template notification. All template registrations that contain
            // "messageParam" and the proper tags will receive the notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="afe5f-111">Этот код отправляет шаблонное уведомление по каждому из шести тегов в массиве строк.</span><span class="sxs-lookup"><span data-stu-id="afe5f-111">This code sends a template notification for each of the six tags in the string array.</span></span> <span data-ttu-id="afe5f-112">Использование тегов гарантирует, что устройства будут получать уведомления только зарегистрированных категорий.</span><span class="sxs-lookup"><span data-stu-id="afe5f-112">The use of tags makes sure that devices receive notifications only for the registered categories.</span></span>
5. <span data-ttu-id="afe5f-113">В приведенном выше коде замените заполнители `<hub name>` и `<connection string with full access>` именем центра уведомлений и строкой подключения для *DefaultFullSharedAccessSignature*, полученными ранее на панели мониторинга центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="afe5f-113">In the above code, replace the `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and the connection  string for *DefaultFullSharedAccessSignature* from the dashboard of your notification hub.</span></span>
6. <span data-ttu-id="afe5f-114">Добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="afe5f-114">Add the following lines in the **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="afe5f-115">Выполните сборку консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="afe5f-115">Build the console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
<span data-ttu-id="afe5f-116">[началу работы с Центрами уведомлений]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="afe5f-116">[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="afe5f-117">[интерфейса REST Центров уведомлений]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx (REST API Центров уведомлений)</span><span class="sxs-lookup"><span data-stu-id="afe5f-117">[Notification Hubs REST interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span></span>
<span data-ttu-id="afe5f-118">[добавлению push-уведомлений в мобильные приложения]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="afe5f-118">[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="afe5f-119">[использованию Центров уведомлений из Java и PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span><span class="sxs-lookup"><span data-stu-id="afe5f-119">[How to use Notification Hubs from Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span></span>
<span data-ttu-id="afe5f-120">[пакета NuGet Microsoft.Azure.Notification Hubs]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/ (Центры уведомлений Microsoft Azure 1.0.7)</span><span class="sxs-lookup"><span data-stu-id="afe5f-120">[Microsoft.Azure.Notification Hubs NuGet package]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span></span>
