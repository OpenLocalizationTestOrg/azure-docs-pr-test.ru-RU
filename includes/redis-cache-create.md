toocreate кэш, сначала войти в toohello [портал Azure](https://portal.azure.com)и нажмите кнопку **New** > **баз данных** > **кэша Redis**.

> [!NOTE]
> Если у вас нет учетной записи Azure, ее можно [бесплатно создать](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) всего за несколько минут.
> 
> 

![Новый кэш](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> Кроме того, toocreating кэши в hello портал Azure, их с помощью диспетчера ресурсов также можно создать шаблоны, PowerShell или Azure CLI.
> 
> * toocreate в кэш, используя шаблоны диспетчера ресурсов. в разделе [создание кэша Redis с помощью шаблона](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * toocreate кэша с использованием Azure PowerShell, в разделе [управления кэша Redis для Azure с помощью Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * toocreate кэша, с помощью Azure CLI см. в разделе [как toocreate и управлять ими с помощью интерфейса командной строки Azure (Azure CLI) hello кэш Azure Redis](../articles/redis-cache/cache-manage-cli.md).
> 
> 

В hello **новый кэш Redis** колонки, укажите нужную конфигурацию кэша hello hello.

![Создание кэша](media/redis-cache-create/redis-cache-cache-create.png) 

* В **DNS-имя**, введите toouse кэша уникальное имя для конечной точки кэша hello. Имя кэша Hello должно быть строкой длиной от 1 до 63 символов и содержать только цифры, буквы и hello `-` символов. Hello имя кэша не может начинаться или заканчиваться hello `-` символьных и последовательных `-` символы не допускаются.
* Для **подписки**, выберите hello подписки Azure, чтобы получить toouse кэша hello. Если у вас есть только одна подписка, она будет автоматически выбран и hello **подписки** раскрывающийся список не будет отображаться.
* В поле **Группа ресурсов**выберите или создайте группу ресурсов для кэша. Дополнительные сведения см. в разделе [использование ресурса группы toomanage ресурсам Azure](../articles/azure-resource-manager/resource-group-overview.md). 
* Используйте **расположение** toospecify hello географическое расположение, в котором размещен ваш кэш. Для наилучшей производительности hello, корпорация Майкрософт настоятельно рекомендует создавать кэш hello в hello же регионе, что клиентское приложение hello кэша.
* Используйте **Ценовая категория** tooselect hello требуемого размера кэша и компоненты.
* **Redis кластера** позволяет toocreate кэши больше, чем 53 ГБ и tooshard данные по нескольким узлам Redis. Дополнительные сведения см. в разделе [как tooconfigure кластеризации для кэша Redis Azure Premium](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Redis сохраняемости** предлагает возможность toopersist hello вашего кэша tooan учетной записи хранилища Azure. Инструкции по настройке сохраняемости см. в разделе [как tooconfigure сохраняемости для кэша Redis Azure Premium](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Виртуальная сеть** предоставляет усиленной безопасности и изоляции путем ограничения доступа tooyour кэша tooonly эти клиенты в пределах указанного hello виртуальной сети Azure. Можно использовать все возможности hello виртуальной сети, такие как подсети, политики управления доступом и другие функции toofurther ограничить доступ tooRedis. Дополнительные сведения см. в разделе [как поддерживают tooconfigure виртуальной сети для кэша Redis Azure Premium](../articles/redis-cache/cache-how-to-premium-vnet.md).
* Для новых кэшей без SSL порт по умолчанию отключен. порт не SSL hello tooenable, проверка **разблокировать порт (не SSL-шифрование) 6379**.

После настройки параметров нового кэша hello щелкните **создать**. Он может занять несколько минут для создания toobe кэша hello. состояние toocheck hello, можно наблюдать за ходом hello на начальной панели hello. После создания кэша hello новый кэш находится **под управлением** состояния и готов для использования с [параметры по умолчанию](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Кэш создан](media/redis-cache-create/redis-cache-cache-created.png)

