Приложения .NET могут использовать hello **StackExchange.Redis** кэша клиента, который можно настроить в Visual Studio с помощью пакета NuGet, который упрощает настройку hello кэша клиентских приложений. 

> [!NOTE]
> Дополнительные сведения см. в разделе hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github страницы и hello [документации по клиенту кэша StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

клиентское приложение в Visual Studio с помощью пакета StackExchange.Redis NuGet hello tooconfigure, щелкните правой кнопкой мыши проект hello в **обозревателе решений** и выберите **управление пакетами NuGet**. 

![Управление пакетами NuGet](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Тип **StackExchange.Redis** или **StackExchange.Redis.StrongName** в текстовое поле поиска hello, выберите нужную версию hello hello результатов и нажмите кнопку **установить**.

> [!NOTE]
> Если вы предпочитаете toouse версию со строгими именами hello **StackExchange.Redis** клиентской библиотеки выберите **StackExchange.Redis.StrongName**; в противном случае выберите **StackExchange.Redis**.
> 
> 

![Пакет NuGet StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

Hello NuGet пакет загружает и добавляет hello необходимые ссылки на сборки для вашего клиента приложение tooaccess кэш Azure Redis с клиента кэша StackExchange.Redis hello.

> [!NOTE]
> Если ваш проект toouse StackExchange.Redis были настроены ранее, можно проверить наличие обновлений пакета toohello из hello **диспетчера пакетов NuGet**. Щелкните toocheck для и установить обновленную версии hello пакета StackExchange.Redis NuGet **обновления** в hello hello **диспетчера пакетов NuGet** окна. При наличии toohello обновления пакета StackExchange.Redis NuGet можно обновленной версии toouse hello обновить проект.
> 
> 

Можно также установить hello пакета StackExchange.Redis NuGet, щелкнув **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню и работающей hello следующую команду из hello **консоль диспетчера пакетов** окна.
    
```
Install-Package StackExchange.Redis
```
