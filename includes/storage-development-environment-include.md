## <a name="set-up-your-development-environment"></a>Настройка среды разработки
Настройте среды разработки в Visual Studio, вы будете готовы tootry hello код примеров в этом руководстве.

### <a name="create-a-windows-console-application-project"></a>Создание нового проекта консольного приложения Windows
В Visual Studio создайте новое консольное приложение Windows. следующие шаги Hello Показать чем toocreate консольное приложение в Visual Studio 2017 г., однако hello действия схожи в других версиях Visual Studio.

1. Выберите **Файл** > **Создать** > **Проект**.
2. Выберите **Установлено** > **Шаблоны** > **Visual C#** > **Классический рабочий стол Windows**.
3. Выберите **Консольное приложение (.NET Framework)**.
4. Введите имя для вашего приложения в hello **имя:** поля
5. Нажмите кнопку **ОК**.

![Диалоговое окно создания проекта в Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Все примеры кода в этом учебнике можно добавить toohello `Main()` метода приложения командной `Program.cs` файла.

Hello клиентская библиотека хранилища Azure можно использовать в любом приложении .NET, включая Azure облачной службы или веб-приложение и приложений для настольных компьютеров и мобильных устройств. Для упрощения в этом руководстве мы будем использовать консольное приложение.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>Использовать hello необходимые пакеты NuGet tooinstall
Существует два пакета, необходимо использовать tooreference в ваш проект toocomplete этого учебника:

* [Клиентская библиотека хранилища Microsoft Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): данный пакет обеспечивает программный доступ toodata ресурсы в вашей учетной записи хранилища.
* [Библиотека Microsoft Azure Configuration Manager для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) — этот пакет предоставляет класс для анализа строки подключения в файле конфигурации независимо от среды выполнения приложения.

Можно использовать оба пакета NuGet tooobtain. Выполните следующие действия.

1. Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Управление пакетами NuGet**.
2. Найдите в Интернете «WindowsAzure.Storage» и нажмите кнопку **установить** tooinstall hello клиентской библиотеки хранилища и его зависимости.
3. Найдите в Интернете «WindowsAzure.ConfigurationManager» и нажмите кнопку **установить** tooinstall hello Azure Configuration Manager.

> [!NOTE]
> Клиентская библиотека хранилища пакета Hello также включается в hello [Azure SDK для .NET](https://azure.microsoft.com/downloads/). Тем не менее рекомендуется также установить hello клиентской библиотеки хранилища с помощью NuGet tooensure всегда имеют последнюю версию клиентской библиотеки hello hello.
> 
> зависимости ODataLib Hello hello клиентская библиотека хранилища для .NET можно устранить, пакеты ODataLib hello, доступные в NuGet, а не из службы данных WCF. можно непосредственно загрузить библиотеки ODataLib Hello или ссылается проект кода через NuGet. Hello пакеты ODataLib используемые hello клиентской библиотеки хранилища следующие [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), и [пространственный](http://nuget.org/packages/System.Spatial/). Хотя эти библиотеки используются классами хранилища таблиц Azure hello, они могут необходимые зависимости для программирования с hello клиентской библиотеки хранилища.
> 
> 

### <a name="determine-your-target-environment"></a>Определение целевой среды
У вас есть два варианта среды выполнения hello примеры в этом руководстве:

* Для учетной записи хранилища Azure в облаке hello можно запустить код. 
* Код может выполняться hello эмулятор хранилища Azure. Эмулятор хранилища Hello — локальную среду, эмулирующую учетную запись хранилища Azure в облаке hello. Эмулятор Hello свободного вариант для тестирования и отладки кода, пока приложение находится в стадии разработки. Эмулятор Hello использует хорошо известная учетная запись и ключ. Дополнительные сведения см. в разделе [hello использование эмулятора хранилища Azure для разработки и тестирования](../articles/storage/common/storage-use-emulator.md)

Если вы используете учетную запись хранения в облаке hello, скопируйте hello первичный ключ доступа для учетной записи хранения из hello портал Azure. Дополнительные сведения см. в разделе [Просмотр и копирование ключей доступа к хранилищу](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).

> [!NOTE]
> Можно выбрать целевую tooavoid эмулятора хранения hello, любой расходов, связанных со службой хранилища Azure. Тем не менее если вы решите tootarget учетную запись хранилища Azure в облаке hello, затрат на выполнение этого учебника будет незначительно.
> 
> 

### <a name="configure-your-storage-connection-string"></a>Настройка строки подключения хранилища
Hello клиентская библиотека хранилища Azure для .NET поддерживает использование хранилища конечные точки tooconfigure соединения строки и учетные данные для доступа к службам хранилища. Лучшим способом toomaintain Hello строки подключения хранилища находится в файле конфигурации. 

Дополнительные сведения о строках соединения см. в разделе [настроить строку подключения tooAzure хранения](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> Ключ учетной записи хранилища — примерно toohello пароль учетной записи root для вашей учетной записи. Всегда быть тщательно tooprotect ключ учетной записи хранилища. Избегайте распространением их tooother пользователей, жестко запрограммированные ее или сохранить в текстовый файл, доступный tooothers. Повторное создание ключа с помощью hello портал Azure, если вы считаете, что он был скомпрометирован.
> 
> 

tooconfigure в строку подключения, откройте hello `app.config` файл из обозревателя решений в Visual Studio. Добавить содержимое hello hello `<appSettings>` элемент, показанный ниже. Замените `account-name` с именем hello вашей учетной записи хранилища и `account-key` с помощью ключа доступа учетной записи:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

Например, параметр конфигурации может быть приблизительно таким:

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

Эмулятор хранилища tootarget hello, можно использовать ярлык, который сопоставляет toohello хорошо известная учетная запись имени и ключа. В этом случае параметр строки подключения будет таким:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

