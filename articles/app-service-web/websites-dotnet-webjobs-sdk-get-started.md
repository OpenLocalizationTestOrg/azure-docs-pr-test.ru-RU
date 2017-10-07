---
title: "aaaCreate веб-задания .NET в службе приложений Azure | Документы Microsoft"
description: "Создание многоуровневого приложения с помощью ASP.NET MVC и Azure. Hello запускает в веб-приложения в службе приложений Azure и hello запускает в качестве веб-задания. приложение Hello используется Entity Framework, база данных SQL и очереди хранилища Azure и больших двоичных объектов."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Создание веб-задания .NET в службе приложений Azure
В этом учебнике показано, как toowrite кода для простой многоуровневого приложения ASP.NET MVC 5, использующий hello [SDK веб-задания](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Здравствуйте, назначение hello [SDK веб-заданий](websites-webjobs-resources.md) является toosimplify hello код, предназначенный для выполнения стандартных задач, которые могут выполнять веб-задания, например обработки изображений, обработки очередей, объединение RSS, обслуживание файлов и отправки сообщений электронной почты. Hello SDK веб-задания имеет встроенные функции для работы с хранилищем Azure и Service Bus, планирование задач и обработка ошибок и других стандартных сценариев. Кроме того, он имеет разработан toobe расширяемой и [репозитория открытым исходным кодом для расширений](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Пример приложения Hello является доски рекламных объявлений. Пользователи могут загружать изображения для рекламных материалов и фоновой обработки преобразует hello toothumbnails изображения. Страница списка ad Hello показывает эскизы hello, а страница сведений о ad hello hello полноразмерное изображение. Ниже приведен снимок экрана:

![Список рекламы](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

В этом примере приложение работает с [очередями Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) и [большими двоичными объектами Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Hello учебнике показано, как toodeploy hello приложения слишком[службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) и [базы данных SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Предварительные требования
Hello учебнике предполагается, что вы знаете, как toowork с [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) проектов в Visual Studio.

Учебник Hello первоначально был написан для Visual Studio 2013, но может использоваться с более поздними версиями Visual Studio. При использовании Visual Studio 2015 или 2017 г обратить внимание, что перед запуском приложения hello локально, необходимо изменить hello `Data Source` частью строка подключения SQL Server LocalDB hello в файлах Web.config и App.config hello из `Data Source=(localdb)\v11.0` слишком`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>Необходимо иметь учетную запись Azure toocomplete этого учебника:
>
> * Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): вы получаете кредиты можно использовать tootry out платных служб Azure, и даже после того, они используются, можно защитить учетную запись hello и использовать свободного служб Azure, таких как веб-сайтов. Вашей кредитной карты не взимается, пока вы явным образом изменения параметров и попросите toobe взимается плата.
> * Вы можете [активировать ежемесячные деньги на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Каждый месяц ваша подписка Visual Studio предоставляет вам кредиты, которые можно использовать для оплаты служб Azure.
>
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
>
>

## <a id="learn"></a>Содержание обучения
Hello учебнике показано, как hello toodo следующие задачи:

* Включите компьютер для разработки Azure, установив hello Azure SDK (только для Visual Studio 2013 и 2015 пользователей).
* Создайте проект консольного приложения, которая автоматически развертывает как веб-задание Azure при развертывании hello связанного веб-проекта.
* Проверка серверной части пакета SDK веб-задания на компьютере разработки hello.
* Публикация приложения с веб-заданий tooa серверной части веб-приложения в службе приложений.
* Отправка файлов и сохранения их в hello службы больших двоичных объектов.
* Используйте toowork hello веб-заданий Azure SDK с очереди хранилища Azure и больших двоичных объектов.

## <a id="contosoads"></a>Архитектура приложения
Пример приложения Hello использует hello [шаблон ориентированное очереди рабочих](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff нагрузки hello процессор действий по созданию эскизы tooa фоновой обработки.

приложение Hello сохраняет рекламы в базе данных SQL, с помощью Entity Framework Code First таблиц hello toocreate и доступа к данным hello. Для каждого рекламного объявления hello база данных хранит два URL-адреса: один для hello полноразмерное изображение и один для эскиза hello.

![Таблица рекламы](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

При отправке изображение, веб-приложения hello хранит изображения hello в [BLOB-объектов Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), и хранит сведения ad hello в базе данных hello с URL-адресом toohello больших двоичных объектов. AT hello же времени, он записывает сообщение tooan очереди Azure. Фоновый процесс, выполняющийся как веб-задания Azure hello SDK веб-заданий выполняет опрос очереди hello для новых сообщений. При появлении нового сообщения hello веб-задание создает эскиз для этого образа и обновления hello эскиза поле URL-адрес базы данных для данного рекламного объявления. Вот это диаграмма, показывающая, как взаимодействуют компоненты hello приложения hello.

![Архитектура Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
Hello учебника инструкции применяются tooAzure пакета SDK для .NET 2.7.1 или более поздней версии.

## <a id="storage"></a>Создание учетной записи хранения Azure
Учетная запись хранилища Azure предоставляет ресурсы для хранения данных больших двоичных объектов и очереди в облаке hello. Он также используется hello данных журналов toostore SDK веб-заданий для мониторинга "hello".

В реальном приложении обычно создают отдельные учетные записи для данных приложения и данных журналов, а также отдельные учетные записи для тестовых данных и рабочих данных. В этом руководстве будет использоваться одна учетная запись.

1. Откройте hello **обозревателя серверов** окна в Visual Studio.
2. Щелкните правой кнопкой мыши hello **Azure** узла, а затем щелкните **подключения tooMicrosoft подписки Azure...** .
   
   ![Подключение tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Выполните вход с использованием учетных данных Azure.
4. Щелкните правой кнопкой мыши **хранения** в разделе hello узла Azure, а затем нажмите кнопку **создать учетную запись хранилища**.
   
   ![Учетная запись хранения](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. В hello **создать учетную запись хранилища** диалоговое окно, введите имя для учетной записи хранения hello.

    Имя Hello должен быть уникальным (нет других учетной записи хранилища Azure может иметь hello таким же именем). Если ввести имя hello уже используется, вы получите toochange вероятность его.

    Здравствуйте, tooaccess URL-адрес учетной записи хранения будут *{имя}*. core.windows.net.
6. Набор hello **регион или территориальная группа** tooyou ближайший регион toohello раскрывающегося списка.

    Этот параметр указывает, в каком центре обработки данных Azure будет размещаться учетная запись хранения. Теоретически этот выбор не имеет большого значения. Однако для рабочего веб-приложения требуется веб-сервер и вашей toobe учетной записи хранилища в hello задержки toominimize же регионе и данные исходящих расходов. веб-приложения Hello (который вы создадите в более поздней версии) должно быть центра обработки данных, как закрыть как можно toohello браузеры, доступ к веб-приложения hello в порядке toominimize задержки.
7. Набор hello **репликации** раскрывающемся списке слишком**локально избыточной**.

    При включении георепликации для учетной записи хранения hello хранимых содержимое является реплицированной tooa вторичный центр обработки данных tooenable перехода на другой ресурс в случае серьезной аварии в основное расположение hello toothat расположение. Георепликация может потребовать дополнительных затрат. Для тестирования и разработки учетных записей обычно не следует toopay для георепликации. Дополнительные сведения см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).
8. Щелкните **Создать**.

    ![Новая учетная запись хранения](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Загрузить приложение hello
1. Загрузите и распакуйте hello [завершения решения](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Запустите Visual Studio.
3. Из hello **файл** меню щелкните **откройте > проект или решение**, перейдите toowhere загруженный hello решение и затем откройте файл решения hello.
4. Нажмите клавиши CTRL + SHIFT + B toobuild hello решения.

    По умолчанию Visual Studio автоматически восстанавливает содержимое пакета NuGet hello, которое не входит в hello *.zip* файла. Если не восстановить hello пакетов, установите их вручную, будут toohello **управление пакетами NuGet для решения** диалогового окна, нажав кнопку hello **восстановить** кнопки в правом верхнем углу hello.
5. В **обозревателе решений**, убедитесь, что **ContosoAdsWeb** выбран в качестве запускаемого проекта hello.

## <a id="configurestorage"></a>Настройка учетной записи хранения toouse приложения hello
1. Откройте приложение hello *Web.config* файл в проекте ContosoAdsWeb hello.

    Hello файл содержит строку подключения SQL и строку соединения хранения Azure для работы с BLOB-объектов и очередей.

    Строка подключения SQL Hello указывает tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) базы данных.

    Строка подключения хранилища Hello приведен пример с заполнителями для hello хранилища учетной записи имя и ключ доступа. Это будет заменено строку подключения с именем hello и ключ учетной записи.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    Строка подключения хранилища Hello называется AzureWebJobsStorage так, как это имя hello приветствия использует пакет SDK веб-заданий по умолчанию. Здравствуйте, таким же именем используется здесь, чтобы обеспечить tooset только одно подключение строковое значение в среде Azure hello.
2. В **обозревателя серверов**, щелкните правой кнопкой мыши учетную запись хранилища в группе hello **хранения** , а затем щелкните **свойства**.

    ![Щелкните свойства учетной записи хранения](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. В hello **свойства** окно, нажмите кнопку **ключи учетной записи хранения**и нажмите кнопку с многоточием hello.

    ![Ключи учетной записи хранения](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Копировать hello **строка подключения**.

    ![Диалоговое окно "Ключи учетной записи хранения"](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Замените строку соединения хранения hello в hello *Web.config* файл со строкой подключения hello был скопирован в буфер. Убедитесь, что выбраны все внутри кавычек hello, но не включая кавычки hello перед вставкой.
6. Откройте hello *App.config* файл в проекте ContosoAdsWebJob hello.

    Этот файл содержит две строки подключения хранилища: одну для данных приложения, а другую для ведения журнала. Можно использовать отдельные учетные записи хранения для данных приложений и ведения журнала; также можно использовать [несколько учетных записей хранения для данных](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). В этом руководстве будет использоваться одна учетная запись. строки подключения Hello имеют прототипы для hello ключи учетной записи хранения.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    По умолчанию hello SDK веб-заданий ищет строки подключения с именем AzureWebJobsStorage и AzureWebJobsDashboard. Кроме того, вы можете [хранения строки подключения hello, однако требуется и передать его в явном виде toohello `JobHost` объекта](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Замените строку подключения hello скопированный ранее обе строки подключения хранилища.
8. Сохраните изменения.

## <a id="run"></a>Запустите приложение hello локально
1. веб-клиентом toostart hello приложения hello, нажмите клавиши CTRL + F5.

    toohello Домашняя страница откроется в браузере по умолчанию Hello. (hello веб-проекта запускается, поскольку вы внесли hello запускаемого проекта.)

    ![Домашняя страница Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. серверной части веб-задания hello toostart приложения hello, щелкните правой кнопкой мыши проект ContosoAdsWebJob hello в **обозревателе решений**, а затем нажмите кнопку **отладки** > **запустить новый экземпляр** .

    Приложения окно консоли открывается и отображает сообщения для ведения журнала, указывающий, что запущен toorun hello объекта JobHost SDK веб-заданий.

    ![Выполняется отображение этого hello серверной части окна приложения консоли](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. В браузере нажмите кнопку **Create an Ad** (Создать рекламу).
4. Введите некоторые тестовые данные, выберите образ tooupload и нажмите кнопку **создать**.

    ![Страница создания](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    приложение Hello переходит toohello страницы индекса, но он не отображается эскиз для нового ad hello, поскольку еще не произошло, обработку.

    В то же время после короткого ожидания ведения журнала сообщений в окне приложения hello консоли показывает, что сообщения в очереди было получено и обработки.

    ![Окно приложения консоли, отображающее, что сообщение очереди обработано](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. После появления hello, ведение журнала сообщений в окне приложения hello консоли обновите hello индекс страницы toosee hello эскиз.

    ![Страница индексации](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Нажмите кнопку **сведения** для вашей toosee ad hello полноразмерное изображение.

    ![Страница сведений](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Приложение hello работы локального компьютера и использует SQL Server, базы данных, расположенной на компьютере, но он работает с очередями и больших двоичных объектов в облаке hello. В следующем разделе hello вы будете запускать приложение hello в облаке hello, используя это облачная база данных, а также большие двоичные объекты в облаке и очереди.  

## <a id="runincloud"></a>Запустите приложение hello в облаке hello
Вам предстоит выполнить hello следующие приложения hello toorun действия в облаке hello:

* Развертывание приложений tooWeb. Visual Studio автоматически создаст новое веб-приложение в службе приложений и экземпляр базы данных SQL.
* Настройте hello web app toouse учетную запись базы данных и хранения данных Azure SQL.

После создания некоторых рекламы при выполнении в облаке hello вы просмотрите hello SDK веб-задания мониторинга toosee hello широкие возможности, он имеет toooffer наблюдения.

### <a name="deploy-tooweb-apps"></a>Развертывание приложений tooWeb

1. Закройте окно браузера hello и окно приложения hello консоли.
2. Следуйте указаниям hello hello [публикации tooAzure с базой данных SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) раздела.
3. После завершения hello шаги развертывания, продолжите hello оставшихся задач в этой статье.

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>Настроить hello web app toouse учетную запись базы данных и хранения данных Azure SQL
Рекомендации по безопасности является слишком[не размещайте конфиденциальные сведения, такие как строки соединения в файлах, которые хранятся в репозитории исходного кода](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Azure предоставляет toodo способ: можно задать строку подключения и другие значения параметров в среде Azure hello и интерфейсы API настройки ASP.NET автоматически получать эти значения при запуске приложения hello в Azure. Эти значения можно задать в Azure с помощью **обозревателя серверов**, hello портал Azure, Windows PowerShell или hello межплатформенного интерфейса командной строки. Дополнительные сведения см. в статье [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Веб-сайты Microsoft Azure: как работают строки приложений и строки подключения).

В этом разделе используется **обозревателя серверов** tooset значений строки подключения в Azure.

1. В **обозревателе сервера** щелкните правой кнопкой мыши свое веб-приложение в узле **Azure > Служба приложений > {ваша группа ресурсов}**, а затем щелкните **Просмотреть параметры**.

    Hello **веб-приложения Azure** в hello появится окно **конфигурации** вкладки.
2. Изменение имени hello имя toohello строка подключения DefaultConnection hello выбран при настройке базы данных SQL hello в hello [публикации tooAzure с базой данных SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) статьи.

    Azure автоматически создается в этой строке подключения при создании веб-приложения hello со связанной базой данных, поэтому уже имеет значение строки правой подключения hello. Вы меняете только hello имя toowhat правильный код.
3. Добавьте две новые строки подключения с именами AzureWebJobsStorage и AzureWebJobsDashboard. Задайте тип базы данных hello слишком**настраиваемый**и набор hello подключения строковое значение toohello одинаковое значение, что вы использовали для hello *Web.config* и *App.config* файлов. (Убедитесь, включает строку hello все подключение, не только hello ключ доступа и не включать hello кавычки).

    Эти строки подключения используются hello SDK веб-заданий, один для данных приложений и один для ведения журнала. Как показано выше, hello, один для данных приложений также используется hello веб-интерфейса кода.
4. Щелкните **Сохранить**.

    ![Строки подключения на портале Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. В **обозревателя серверов**, щелкните правой кнопкой мыши веб-приложения hello и нажмите кнопку **остановить**.
6. После остановки веб-приложения hello, щелкните правой кнопкой мыши веб-приложение hello и нажмите кнопку **запустить**.

   Hello веб-задание запускается автоматически при публикации, но он останавливается при изменении конфигурации. toorestart, можно перезапустить веб-приложение hello или перезагрузите веб-задания hello в hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Это обычно рекомендуется toorestart hello веб-приложения после изменения конфигурации.
7. Обновите окно браузера hello с URL-адрес приложения hello в адресную строку.

    Откроется домашняя страница приветствия.
8. Создание рекламы, как в случае, когда вы [локально запустить приложение hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   страница индекса Hello показана без эскиза на первый.
9. Обновите страницу приветствия через несколько секунд и hello эскиза отображается.

   Если эскиз hello не отображается, может потребоваться toowait приблизительно минуты для hello toorestart веб-задания. Если после некоторое время, по-прежнему не отображается эскиз hello при обновлении страницы приветствия, hello веб-задания не может иметь автоматически начата. В этом случае переход toohello **службы приложений** колонки в hello [портал Azure](https://portal.azure.com/), найдите веб-приложения и нажмите кнопку **запустить**.

### <a name="view-hello-webjobs-sdk-dashboard"></a>Hello представления панели мониторинга пакета SDK веб-заданий
1. В hello [портал Azure](https://portal.azure.com/)выберите hello **колонку служб приложения**, найдите веб-приложения и выберите **веб-задания**.
3. Выберите hello **журналы** вкладки.

    ![Вкладка "Журналы"](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    На новой вкладке браузера откроется toohello панели мониторинга пакета SDK веб-заданий. панель мониторинга Hello показывает, hello веб-задание работает и отображается список функций в коде, пакет SDK веб-заданий запускается приветствия.
4. Выберите один из hello функции toosee сведения о его выполнения.

    ![Панель мониторинга пакета SDK веб-заданий](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Панель мониторинга пакета SDK веб-заданий](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    Hello **функция воспроизведения** кнопку на этой странице снова вызывает hello SDK веб-заданий для функции hello toocall framework, и она предоставляет функции вероятность toochange hello данные, передаваемые toohello сначала.

> [!NOTE]
> После окончания тестирования, рассмотрите возможность удаления веб-приложения hello, учетной записи хранилища и экземпляр базы данных SQL. веб-приложения Hello предоставляется бесплатно, однако плата начисляется hello SQL учетной записи хранилища и экземпляр базы данных (хотя и минимальная из-за малого размера toohello). Кроме того Если оставить hello веб-приложения под управлением любой пользователь находит URL-адрес, можно создать и просмотра рекламы. 
>
>

### <a name="delete-your-web-app"></a>Удаление веб-приложения
На портале hello go toohello **службы приложений** колонки, найдите и выберите веб-приложения и нажмите кнопку **удалить**. Если необходимо просто tootemporarily запретить другим пользователям доступ к веб-приложения hello, нажмите кнопку **остановить** вместо. В этом случае накладные расходы по-прежнему tooaccrue для hello базы данных SQL и учетную запись хранилища.

### <a name="delete-your-storage-account"></a>Удаление учетной записи хранения
toodelete вашей учетной записи хранения в разделе [удалить учетную запись хранения](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Удаление базы данных
toodelete SQL базы данных см. в разделе hello [API REST для базы данных SQL Azure](https://docs.microsoft.com/rest/api/sql/) документации.

## <a id="create"></a>Создание приложения hello с нуля
В этом разделе вы выполните hello следующие задания:

* Создание решения Visual Studio с веб-проектом.
* Добавьте проект библиотеки классов для данных hello уровень доступа, общим для внешнего интерфейса hello и серверной части.
* Добавьте проект консольного приложения для внутреннего hello с включено развертывание веб-заданий.
* Добавление пакетов NuGet.
* Указание ссылок на проекты.
* Скопируйте файлы кода и конфигурации приложения из приложения загружаются hello, с которой выполнялись в предыдущем разделе hello hello учебника.
* Просмотрите компоненты hello кода hello, поддерживающих Azure BLOB-объектов и очередей и hello SDK веб-заданий.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Создание решения Visual Studio с веб-проектом и проектом библиотеки класса
1. В Visual Studio выберите **Файл** > **Создать** > **Проект**.
2. В hello **новый проект** диалоговое окно, выберите **Visual C#** > **Web** > **веб-приложение ASP.NET (.NET Framework)**.
3. Имя проекта hello ContosoAdsWeb, назовите решение hello ContosoAdsWebJobsSDK (изменить имя решения hello, если вы будете помещать в hello же папке, что hello загрузки решения) и нажмите кнопку **ОК**.

    ![Новый проект](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. В hello **новое веб-приложение ASP.NET** диалоговое окно, выберите шаблон MVC hello и выберите **изменить аутентификацию**.

    ![Изменить проверку подлинности](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. В hello **изменить аутентификацию** диалоговое окно, выберите **без проверки подлинности**, а затем нажмите кнопку **ОК**.

    ![Без аутентификации](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. В hello **новое веб-приложение ASP.NET** диалоговое окно, нажмите кнопку **ОК**.

    Visual Studio создает решение hello и hello веб-проекта.
7. В **обозревателе решений**, щелкните правой кнопкой мыши решение hello (не hello проект), а затем выберите **добавить** > **новый проект**.
8. В hello **Добавление нового проекта** диалоговое окно, выберите **Visual C#** > **Windows классического** > **библиотека классов (.NET Платформа)** шаблона.  
9. Имя проекта hello *ContosoAdsCommon*, а затем нажмите кнопку **ОК**.

    Этот проект будет содержать контекста Entity Framework hello и hello модели данных, для которых hello переднего плана и будет использовать серверной части. Кроме того можно определить классы, связанные с EF hello в веб-проекте hello и ссылку на этот проект из проекта веб-задания hello. Однако проект веб-задания будут иметь tooweb ссылочных сборок, которые ему не требуется.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Добавление проекта приложения консоли, в котором включено развертывание веб-заданий
1. Щелкните правой кнопкой мыши веб-проект hello (не hello решение или проект библиотеки классов hello) и нажмите кнопку **добавить** > **новый проект веб-задания Azure**.

    ![Пункт меню "Новый проект веб-задания Azure"](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. В hello **добавить веб-задание Azure** диалоговое окно, введите в качестве обеих hello ContosoAdsWebJob **имя проекта** и hello **имя веб-задания**. Оставить **режим запуска веб-задания** значение слишком**запуска постоянно**.
3. Нажмите кнопку **ОК**.

   Visual Studio создает консольное приложение, настроенное toodeploy как веб-задания при каждом развертывании hello веб-проекта. toodo, что она выполнена hello следующие задачи после создания проекта hello:

   * Добавлен *публикации settings.json веб-задания* файл в папке свойств проекта веб-задания hello.
   * Добавлен *list.json веб-заданий* файл в hello веб-проекта свойства папки.
   * Установить пакет Microsoft.Web.WebJobs.Publish NuGet hello в проект веб-задания hello.

   Дополнительные сведения об этих изменениях см. в разделе [как toodeploy веб-заданий с помощью Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>Добавление пакетов NuGet
Hello шаблон нового проекта для проекта веб-задания автоматически устанавливает пакет NuGet SDK веб-заданий hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) и его зависимости.

Один является зависимости пакета SDK веб-заданий, которые автоматически устанавливается в проект веб-задания hello hello hello библиотека клиента хранилища Azure (SCL). Однако необходимо tooadd его toowork проект web toohello с BLOB-объектов и очередей.

1. Откройте hello **управление пакетами NuGet** диалоговое окно для решения hello.
2. Выберите в левой области hello **установленных пакетов**.
3. Найти hello *хранилища Azure* пакета, а затем нажмите кнопку **управление**.
4. В hello **выберите проекты** поле, выберите hello **ContosoAdsWeb** флажок и нажмите кнопку **ОК**.

    Все три проекта используйте toowork hello Entity Framework с данными в базе данных SQL.
5. Выберите в левой области hello **Online**.
6. Найти hello *EntityFramework* NuGet пакета и установить на всех трех проектов.

### <a name="set-project-references"></a>Установите ссылки проекта
Проекты веб-задания и веб работать с hello базы данных SQL, поэтому оба проекта ContosoAdsCommon toohello ссылки.

1. В проекте ContosoAdsWeb hello установите проект ContosoAdsCommon toohello ссылки. (Щелкните правой кнопкой мыши проект ContosoAdsWeb hello и нажмите кнопку **добавить** > **ссылка**. 
2. В hello **диспетчер ссылок** выберите **проекты** > **решения** > **ContosoAdsCommon**, а затем нажмите кнопку **ОК**.)
   
    проект веб-задания Hello необходимо ссылки для работы с изображениями и доступ к строки подключения.

4. В проекте ContosoAdsWebJob hello, задать ссылку слишком`System.Drawing` и `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Добавление кода и файлов конфигурации
Этот учебник не содержит как слишком[создавать MVC контроллеры и представления, с помощью формирования шаблонов](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), также как[написать код платформы Entity Framework, который работает с базами данных SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), или [hello основы Асинхронное программирование в ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Таким образом, все, что остается toodo — копирование файлов кода и конфигурации из решения hello загружены в решение новый hello. После этого hello следующих разделах покажите и объясните основные части кода hello.

файлы tooadd tooa проект или папку, щелкните правой кнопкой мыши проект hello или папку и нажмите кнопку **добавить** > **существующий элемент**. Выберите hello файлов требуется и нажмите кнопку **добавить**. Если запрос на подтверждение tooreplace существующие файлы, нажмите кнопку **Да**.

1. В проекте ContosoAdsCommon hello, удалите hello *Class1.cs* и добавьте в его hello месте следующие файлы из проекта hello загрузки файла.

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. В проекте ContosoAdsWeb hello добавьте следующие файлы из проекта загружаются hello hello.

   * *Web.config*
   * *Global.asax.cs*  
   * В hello *контроллеров* папки: *AdController.cs*
   * В hello *представления\общие* папки: *_Layout.cshtml* файла
   * В hello *Views\Home* папки: *Index.cshtml*
   * В hello *Views\Ad* папку (сначала создать папки hello): пять *.cshtml* файлов
3. В проекте ContosoAdsWebJob hello добавьте следующие файлы из проекта загружаются hello hello.

   * *App.config* (изменение hello фильтром типов файлов слишком**все файлы**)
   * *Program.cs*
   * *Functions.cs*

Теперь можно построить, запуска и развертывания приложения hello, как описано ранее в учебнике hello. Перед этим Однако остановите веб-задания, по-прежнему работает в hello первого веб-приложения, развернутые на hello. В противном случае этого веб-задания будет обрабатывать сообщения очереди, созданные локально или по приложения hello в новое веб-приложение, так как все используете hello же учетной записи хранилища.

## <a id="code"></a>Просмотрите код приложения hello
Hello ниже разделы содержат определение кода hello связанных tooworking с hello SDK веб-задания и больших двоичных объектах хранилища Azure и очереди.

> [!NOTE]
> Hello при кода определенного toohello SDK веб-заданий, см. toohello [Program.cs и Functions.cs](#programcs) разделы.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
файл Ad.cs Hello определяет перечисление для категорий ad и класс сущности POCO ad сведения.

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Hello класс ContosoAdsContext указывает, используется класс Ad hello в коллекцию DbSet, что платформа Entity Framework хранит в базе данных SQL.

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

Класс Hello имеет два конструктора. Здравствуйте сначала используется hello веб-проекта и указывает имя строки подключения, которая хранится в файле Web.config hello или среды выполнения Azure hello hello. Второй конструктор Hello позволяет toopass в строку hello фактическое подключения. Необходим проект веб-задания hello поскольку он не содержит файл Web.config. Вы уже видели раньше была сохранена эта строка подключения, куда вы увидите позже как код hello извлекает hello строку подключения, когда он создает экземпляр класса DbContext hello.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon — BlobInformation.cs
Hello `BlobInformation` класс — это toostore используется информация о BLOB-объект образа в очереди сообщений.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Код, который вызывается из hello `Application_Start` метод создает *изображения* контейнер больших двоичных объектов и *изображения* очередь, если они еще не существуют. Это гарантирует, что при каждом запуске с помощью новой учетной записи хранения hello требуемые контейнер больших двоичных объектов и очереди создаются автоматически.

Здравствуйте, учетной записи хранилища toohello кода получает доступ с помощью строки подключения к хранилищу hello из hello *Web.config* файл или среды выполнения Azure.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Затем он возвращает toohello ссылки *изображения* большого двоичного объекта контейнера, создает контейнер hello в том случае, если он еще не существует, и наборы разрешений доступа на новый контейнер hello. По умолчанию новые контейнеры разрешено только клиенты с большими двоичными объектами tooaccess учетные данные учетной записи хранилища. веб-приложения Hello должен hello public toobe больших двоичных объектов, чтобы он может отображать изображения с помощью URL-адреса, большие двоичные объекты toohello точки изображения.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

Аналогичный код получает toohello ссылки *thumbnailrequest* ставить в очередь и создает новую очередь. В этом случае изменений разрешений не требуется.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb — _Layout.cshtml
Hello *_Layout.cshtml* файл задает имя приложения hello в hello верхний и нижний колонтитулы и создает запись меню «Объявления».

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hello *Views\Home\Index.cshtml* файла отображаются категории ссылки на домашнюю страницу приветствия. ссылки Hello передать целое значение hello hello `Category` перечисления в страницу индекса рекламы toohello переменной строки запроса.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
В hello *AdController.cs* файл, hello вызывает конструктор hello `InitializeStorage` метод toocreate клиентская библиотека хранилища Azure объекты, которые предоставляют API для работы с BLOB-объектов и очередей.

Затем код hello получает toohello ссылки *изображения* большого двоичного объекта контейнера, как было показано ранее в *Global.asax.cs*. При этом он устанавливает [политику повторения](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) по умолчанию, подходящую для веб-приложения. политика повтора экспоненциально растущим по умолчанию Hello зависание веб-приложения hello дольше, чем через минуту на нескольких повторных попыток для временных ошибок. политика повтора Hello, указанные здесь ожидает три секунды после каждого повторите для копирования toothree попыток.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Аналогичный код получает toohello ссылки *изображения* очереди.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

Большая часть кода hello контроллера является типичным для работы с моделью данных Entity Framework, с помощью класса DbContext. Исключение — hello HttpPost `Create` метод, который отправляет файл и сохраняет его в хранилище больших двоичных объектов. предоставляет связыватель модели Hello [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello метод объекта.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Если hello пользователь выбрал tooupload файла, кода hello передает файл hello, сохраняет его в большой двоичный объект и обновляет запись в базе данных Ad hello URL-адресом toohello больших двоичных объектов.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Hello код, hello передачи находится в hello `UploadAndSaveBlobAsync` метод. Он создает имя GUID для hello больших двоичных объектов, передачи и сохраняет файл hello и возвращает toohello сохранен эталонный BLOB-объект.

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

После hello HttpPost `Create` метод передает большой двоичный объект и обновления Здравствуйте, базы данных, он создает очередь сообщений tooinform hello серверной части процесс, образ будет готов для преобразования tooa эскиз.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

Здравствуйте, код для hello HttpPost `Edit` метод аналогичен, за исключением того, что если hello пользователь выбирает новый файл образа, необходимо удалить все большие двоичные объекты, которые уже существуют для этой ad.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Ниже приведен код hello, удаляет большие двоичные объекты при удалении ad.

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml и Details.cshtml
Hello *Index.cshtml* файла отображаются эскизы с hello другие данные ad:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

Hello *Details.cshtml* файл отображает hello полноразмерное изображение:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml и Edit.cshtml
Hello *Create.cshtml* и *Edit.cshtml* -файлы указывают кодирования, что включает hello контроллера tooget hello форм `HttpPostedFileBase` объекта.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

`<input>` Элемент предписывает tooprovide браузера hello диалоговое окно выбора файла.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Когда hello запускает веб-задания hello `Main` вызовы методов hello SDK веб-заданий `JobHost.RunAndBlock` выполнения метода toobegin триггеру функций hello текущем потоке.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail
Этот метод вызывается Hello SDK веб-заданий при получении сообщения в очереди. Создает Hello метод эскиз и помещает hello эскиз URL-адрес в базе данных hello.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* Hello `QueueTrigger` атрибут направляет hello SDK веб-заданий toocall этот метод при получении нового сообщения в очереди thumbnailrequest hello.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    Hello `BlobInformation` из очереди сообщения hello автоматически десериализовать в hello `blobInfo` параметра. По завершении метода hello hello очереди сообщение удаляется. При сбое метода hello перед завершением hello очереди сообщение не удаляется; После истечения срока аренды 10 минут, сообщение hello является выпущено toobe взял еще раз и обработки. Если сообщение вызывает исключение, эта последовательность не будет повторяться бесконечно. После 5 неудачных попыток tooprocess сообщение, сообщение hello является перемещенный tooa очередь с именем {имя}-подозрительное. Максимальное число попыток Hello настраивается.
* Здравствуйте, два `Blob` атрибуты предоставляют объекты, привязанные tooblobs: один toohello существующего BLOB-объекта изображения и один tooa новый эскиза большой двоичный объект, создаваемый методом hello.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    Имена больших двоичных объектов будут взяты из свойств объекта hello `BlobInformation` получено в очереди сообщение hello объекта (`BlobName` и `BlobNameWithoutExtension`). tooget hello всеми функциональными возможностями hello клиентской библиотеки хранилища, можно использовать hello `CloudBlockBlob` toowork класса с большими двоичными объектами. Если требуется tooreuse кода, написанного toowork с `Stream` объектов, которые можно использовать hello `Stream` класса.

Дополнительные сведения о том, как toowrite функции, используйте пакет SDK веб-задания атрибутов см. в разделе hello следующие ресурсы:

* [Как toouse Azure очередь хранилища с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Как toouse Azure таблицу хранилища с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Как toouse шины обслуживания Azure с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Если веб-приложение выполняется на нескольких виртуальных машин, несколько веб-задания будут выполняться одновременно, а в некоторых случаях это может привести к hello же данные, обработка несколько раз. Это не проблема, при использовании встроенных очереди hello, BLOB-объекта и триггеры Service Bus. Hello SDK гарантирует, что функций будет обрабатываться только один раз для каждого сообщения или большого двоичного объекта.
> * Сведения о том, как нормальное завершение работы tooimplement. в разделе [нормальное завершение работы](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Здравствуйте, код в hello `ConvertImageToThumbnailJPG` метод (не показано) использует классы в hello `System.Drawing` пространство имен для простоты. Однако hello классы этого пространства имен были разработаны для работы с Windows Forms. Они не поддерживаются в службе Windows или ASP.NET. Дополнительные сведения о параметрах обработки изображений см. в статьях [Back to Basics: Dynamic Image Generation, ASP.NET Controllers, Routing, IHttpHandlers, and runAllManagedModulesForAllRequests](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Основы: создание динамического образа, контроллеры ASP.NET, маршрутизация и runAllManagedModulesForAllRequests) и [Deep Inside Image Resizing and scaling with ASP.NET and IIS with ImageResizing.net author Nathanael](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Особенности изменения размеров и масштабирования изображения с использованием ASP.NET и IIS с автором ImageResizing.net Натанаэлем).
>
>

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике было показано простое многоуровневого приложения, использующего hello SDK веб-заданий для серверной обработки. В этом разделе приведены рекомендации по дальнейшему изучению многоуровневых приложений ASP.NET и веб-заданий.

### <a name="missing-features"></a>Отсутствующие функции
приложение Hello довольно просты учебник Приступая к работе. В реальном приложении следует реализовать [внедрения зависимостей](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) и hello [репозитория и единицу работы шаблоны](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), используйте [интерфейса для ведения журнала](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), используйте [ EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage данные изменений в модели и использовать [устойчивость подключений EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage временный сетевой ошибки.

### <a name="scaling-webjobs"></a>Масштабирование веб-заданий
Веб-задания выполняются в контексте веб-приложения hello и не масштабируемая отдельно. Например если имеется один экземпляр приложения стандартные веб-сайтов, имеется только один экземпляр запущен процесс фоновой и она использует некоторые hello server ресурсов (ЦП, памяти и т. д.), в противном случае будут доступны tooserve веб-содержимого.

Если трафика зависит от времени день или день недели, и hello серверной обработки вы должны toodo может ожидать, может планировать toorun вашего веб-задания по низкой нагрузки. Если hello нагрузки по-прежнему слишком большое для этого решения, можно запустить серверной hello как веб-задания в выделенном отдельные веб-приложения для этой цели. Затем можно масштабировать веб-приложение внутреннего сервера отдельно от веб-приложения внешнего сервера.

Дополнительные сведения см. в разделе [Масштабирование веб-заданий](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Предотвращение завершения работы веб-приложений из-за превышения времени ожидания
toomake убедиться, что веб-заданий всегда работает, и работает на всех экземплярах веб-приложения, у вас есть tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) компонентов.

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>С помощью пакета SDK веб-задания вне веб-заданий hello
Программа, использующая hello SDK веб-заданий не toorun в Azure в веб-задания. Ее можно запустить локально, а также в другой среде, например в рабочей роли облачной службы или службы Windows. Тем не менее можно только обращаться hello мониторинга SDK веб-заданий Azure веб-приложение. у вас есть tooconnect hello web app toohello учетной записи хранения вы используете, задав строку подключения AzureWebJobsDashboard hello на hello мониторинга hello toouse **Настройка** hello классического портала. Затем toohello панели мониторинга можно получить с помощью hello URL-адреса:

https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions

Дополнительные сведения см. в разделе [получение панели мониторинга для локальной разработки с помощью hello SDK веб-заданий](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), но Обратите внимание, что в нем отображаются старые имя строки подключения.

### <a name="more-webjobs-documentation"></a>Дополнительная документация по веб-заданиям
Дополнительные сведения см. в статье [Документация по веб-заданиям Azure](http://go.microsoft.com/fwlink/?LinkId=390226).
