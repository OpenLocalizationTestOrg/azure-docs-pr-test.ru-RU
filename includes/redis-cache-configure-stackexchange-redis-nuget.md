<span data-ttu-id="570c2-101">Приложения .NET могут использовать hello **StackExchange.Redis** кэша клиента, который можно настроить в Visual Studio с помощью пакета NuGet, который упрощает настройку hello кэша клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="570c2-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="570c2-102">Дополнительные сведения см. в разделе hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github страницы и hello [документации по клиенту кэша StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="570c2-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="570c2-103">клиентское приложение в Visual Studio с помощью пакета StackExchange.Redis NuGet hello tooconfigure, щелкните правой кнопкой мыши проект hello в **обозревателе решений** и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="570c2-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Управление пакетами NuGet](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="570c2-105">Тип **StackExchange.Redis** или **StackExchange.Redis.StrongName** в текстовое поле поиска hello, выберите нужную версию hello hello результатов и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="570c2-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="570c2-106">Если вы предпочитаете toouse версию со строгими именами hello **StackExchange.Redis** клиентской библиотеки выберите **StackExchange.Redis.StrongName**; в противном случае выберите **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="570c2-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![Пакет NuGet StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="570c2-108">Hello NuGet пакет загружает и добавляет hello необходимые ссылки на сборки для вашего клиента приложение tooaccess кэш Azure Redis с клиента кэша StackExchange.Redis hello.</span><span class="sxs-lookup"><span data-stu-id="570c2-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="570c2-109">Если ваш проект toouse StackExchange.Redis были настроены ранее, можно проверить наличие обновлений пакета toohello из hello **диспетчера пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="570c2-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="570c2-110">Щелкните toocheck для и установить обновленную версии hello пакета StackExchange.Redis NuGet **обновления** в hello hello **диспетчера пакетов NuGet** окна.</span><span class="sxs-lookup"><span data-stu-id="570c2-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="570c2-111">При наличии toohello обновления пакета StackExchange.Redis NuGet можно обновленной версии toouse hello обновить проект.</span><span class="sxs-lookup"><span data-stu-id="570c2-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="570c2-112">Можно также установить hello пакета StackExchange.Redis NuGet, щелкнув **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню и работающей hello следующую команду из hello **консоль диспетчера пакетов** окна.</span><span class="sxs-lookup"><span data-stu-id="570c2-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
