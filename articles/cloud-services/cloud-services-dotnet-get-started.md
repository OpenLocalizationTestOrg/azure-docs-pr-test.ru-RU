---
title: "aaaGet работы с облачных служб Azure и ASP.NET | Документы Microsoft"
description: "Узнайте, как toocreate многоуровневые приложения, с помощью ASP.NET MVC и Azure. приложение Hello выполняется в облачной службе, с веб-ролью и рабочей роли. В его работе используются: Entity Framework, база данных SQL, очереди и BLOB-объекты службы хранилища Azure."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Начало работы с облачными службами Azure и ASP.NET

## <a name="overview"></a>Обзор
В этом учебнике показано как toocreate многоуровневое приложение .NET с ASP.NET MVC переднего плана и разверните его tooan [облачной службы Azure](cloud-services-choose-me.md). Здравствуйте, приложение использует [базы данных SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [службы больших двоичных объектов](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)и hello [службы очередей Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). Вы можете [загрузите проект Visual Studio hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) из hello коллекции кода MSDN.

Hello учебнике показано, как toobuild и выполнения hello приложения локально, как toodeploy его tooAzure и hello выполнения в облако и как toobuild ее с нуля. Можно начать с создания с нуля и затем hello теста и после развертывания действия при необходимости.

## <a name="contoso-ads-application"></a>Приложение Contoso Ads
приложение Hello — доски рекламных объявлений. Пользователи создают рекламу, вводя текст и загружая изображения. Их можно просмотреть список рекламы с помощью эскизов, и они могут просматривать полноразмерное изображение hello, при выборе сведения hello toosee ad.

![Список рекламы](./media/cloud-services-dotnet-get-started/list.png)

приложение Hello использует hello [шаблон ориентированное очереди рабочих](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff нагрузки hello процессор действий по созданию эскизы tooa серверной части процесса.

## <a name="alternative-architecture-websites-and-webjobs"></a>Альтернативная архитектура: веб-сайты и веб-задания
В этом учебнике показано, как toorun переднего плана и серверной части в Azure облачной службы. Альтернативным вариантом является toorun hello переднего плана в [веб-сайте Azure](/services/web-sites/) и использовать hello [веб-заданий](http://go.microsoft.com/fwlink/?LinkId=390226) компонентов (в настоящее время в предварительной версии) для внутренней hello. Учебник, использующий веб-заданий, в разделе [Приступая к работе с веб-заданий Azure SDK hello](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md). Сведения о как toochoose hello службы, которые лучше всего соответствуют вашего сценария, см. в разделе [веб-сайтов Azure, облачных служб и виртуальных машин сравнения](../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>Что вы узнаете
* Как tooenable компьютер для разработки Azure, установив hello Azure SDK.
* Как toocreate Visual Studio облачные службы проект с веб-роль ASP.NET MVC и рабочей роли.
* Как tootest hello проекта облачной службы локально, с помощью эмулятора хранилища Azure hello.
* Как toopublish hello облака проекта tooan Azure облачной службы и тестов, с помощью учетной записи хранилища Azure.
* Как tooupload файлов и сохранения их в hello Azure BLOB-объектов.
* Как toouse hello службы очередей Azure для обмена данными между уровнями.

## <a name="prerequisites"></a>Предварительные требования
Hello учебнике предполагается, что вы понимаете [основные понятия о Azure облачные службы](cloud-services-choose-me.md) например *веб-роли* и *рабочей роли* терминология.  Также предполагается, что вы знаете, как toowork с [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) или [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) проектов в Visual Studio. Пример приложения Hello использует MVC, но большинство hello учебник также применяется tooWeb форм.

Вы можете запустить приложение hello локально без подписки Azure, но вам потребуется одно облако toohello toodeploy hello приложения. Если у вас нет учетной записи, можно [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) или [подписаться на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).

Hello учебника инструкции работают с любой из следующих продуктов hello.

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Если у вас нет одного из этих, Visual Studio могут быть установлены автоматически при установке hello Azure SDK.

## <a name="application-architecture"></a>Архитектура приложения
приложение Hello сохраняет рекламы в базе данных SQL, с помощью Entity Framework Code First таблиц hello toocreate и доступа к данным hello. Для каждого рекламного объявления hello базы данных хранилища два URL-адреса, один для hello полноразмерное изображение и один для hello эскиз.

![Таблица рекламы](./media/cloud-services-dotnet-get-started/adtable.png)

Когда пользователь загружает изображение, hello переднего плана под управлением в веб-роли хранит изображения hello в [BLOB-объектов Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), и хранится такая информация ad hello в базе данных hello с URL-адресом toohello больших двоичных объектов. AT hello же времени, он записывает сообщение tooan очереди Azure. Тыловой процесс, выполняющийся в рабочей роли периодически опрашивает очередь hello для новых сообщений. При появлении нового сообщения hello рабочей роли создает эскиз для этого образа и обновлений hello эскиза поле URL-адрес базы данных для данного рекламного объявления. Hello следующей схеме показано, как части приложения hello, hello взаимодействуют.

![Архитектура Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>Загрузите и запустите решение hello завершена
1. Загрузите и распакуйте hello [завершения решения](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Запустите Visual Studio.
3. Из hello **файл** меню щелкните **открыть проект**, перейдите toowhere загруженный hello решение и затем откройте файл решения hello.
4. Нажмите клавиши CTRL + SHIFT + B toobuild hello решения.

    По умолчанию Visual Studio автоматически восстанавливает содержимое пакета NuGet hello, которое не входит в hello *.zip* файла. Если не восстановить hello пакетов, установите их вручную, будут toohello **управление пакетами NuGet для решения** диалоговое окно и щелкнув hello **восстановить** кнопки в правом верхнем углу hello.
5. В **обозревателе решений**, убедитесь, что **ContosoAdsCloudService** выбран в качестве запускаемого проекта hello.
6. Если вы используете Visual Studio 2015 или более поздней версии, измените строку подключения SQL Server hello в приложение hello *Web.config* файла проекта ContosoAdsWeb hello и в hello *ServiceConfiguration.Local.cscfg* файл проекта ContosoAdsCloudService hello. В каждом случае изменить «(localdb) \v11.0» слишком «(localdb) \MSSQLLocalDB».
7. Нажмите клавиши CTRL + F5 toorun hello приложения.

    При локальном выполнении проекта облачной службы Visual Studio автоматически вызывает hello Azure *эмулятор вычислений* и Azure *эмулятор хранилища*. Hello вычислений эмулятор использует компьютера ресурсы toosimulate hello веб-роли и роли рабочих сред. Эмулятор хранилища Hello использует [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate Azure облачного хранилища базы данных.

    Hello первый раз при запуске проекта облачной службы занимает приблизительно минуты для Привет эмуляторы toostart вверх. По завершении запуска эмулятора браузер по умолчанию hello откроется домашняя страница приложения toohello.

    ![Архитектура Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. Нажмите кнопку **Create an Ad** (Создать приложение AD).
9. Введите некоторые тестовые данные и выберите *.jpg* изображения tooupload, а затем нажмите кнопку **создать**.

    ![Страница создания](./media/cloud-services-dotnet-get-started/create.png)

    приложение Hello переходит toohello страницы индекса, но он не отображается эскиз для нового ad hello, поскольку еще не произошло, обработку.
10. Подождите немного, а затем обновить hello индекс страницы toosee hello эскиз.

     ![Страница индексации](./media/cloud-services-dotnet-get-started/list.png)
11. Нажмите кнопку **сведения** для вашей toosee ad hello полноразмерное изображение.

     ![Страница сведений](./media/cloud-services-dotnet-get-started/details.png)

Полностью на локальном компьютере без подключения облака toohello работы приложения hello. Эмулятор хранилища Hello хранит очередь hello и данные большого двоичного объекта в базе данных SQL Server Express LocalDB и приложения hello хранит данные ad hello в другой базе данных LocalDB. Базы данных Active Directory Entity Framework Code First автоматически созданные hello hello веб-приложения hello пытался tooaccess при первом его.

В следующем разделе hello следует настроить ресурсы облако Azure toouse hello решения для очереди, BLOB-объектов и базы данных приложения hello при выполнении в облаке hello. Если нужна toocontinue toorun локально, но использует облачные ресурсы хранилища и базы данных, может сделать это. Это лишь Настройка строки подключения, которые вы увидите как toodo.

## <a name="deploy-hello-application-tooazure"></a>Развертывание tooAzure приложения hello
Вам предстоит выполнить hello следующие приложения hello toorun действия в облаке hello:

* Создайте облачную службу Azure.
* Создайте базу данных SQL Azure.
* Создайте учетную запись хранения Azure.
* Настройка решения toouse hello базы данных Azure SQL при запуске в Azure.
* Настройка решения toouse hello вашей учетной записи хранилища Azure при запуске в Azure.
* Развертывание hello проекта tooyour Azure облачной службы.

### <a name="create-an-azure-cloud-service"></a>Создание облачной службы Azure
Приложение hello hello среды будет запущено в — облачной службы Azure.

1. Откройте в браузере, hello [портал Azure](https://portal.azure.com).
2. Щелкните **Создать > Вычисления > Облачная служба**.

3. В hello DNS поле ввода имени введите префикс URL-адреса для hello облачной службы.

    Этот URL-адрес имеет уникальный toobe.  Вы получите сообщение об ошибке, если префикс hello выбрать уже используется.
4. Укажите группу ресурсов для службы hello. Нажмите кнопку **создать новый** и затем введите имя в hello ресурсов группы поле ввода, такие как CS_contososadsRG.

5. Выберите нужное приложение hello toodeploy область hello.

    В этом поле указывается в каком центре обработки данных будет размещаться облачная служба. В рабочем приложении следует выбрать клиентов tooyour ближайший регион hello. В этом учебнике выберите tooyou ближайший регион hello.
5. Щелкните **Создать**.

    В следующие изображения hello облачная служба создается с hello CSvccontosoads.cloudapp.net URL-адрес.

    ![Новая облачная служба](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Создание базы данных SQL Azure
При запуске приложения hello в облаке hello, он будет использовать базы данных на основе облака.

1. В hello [портал Azure](https://portal.azure.com), нажмите кнопку **Создать > базы данных > база данных SQL**.
2. В hello **имя базы данных** введите *contosoads*.
3. В hello **группы ресурсов**, нажмите кнопку **использовать существующие** и выберите hello группы ресурсов, используемой для hello облачной службы.
4. В hello следующие изображения, щелкните **Server — необходимые настройки** и **Создание нового сервера**.

    ![Туннель toodatabase](./media/cloud-services-dotnet-get-started/newdb.png)

    Кроме того Если ваша подписка уже имеет сервер, можно выберите сервер из раскрывающегося списка hello.
5. В hello **имя сервера** введите *csvccontosodbserver*.

6. Введите **имя для входа в систему** и **пароль администратора**.

    Если вы выбрали **Создать сервер**, не используйте имеющиеся имя и пароль. Вводите новое имя и пароль, что вы определяете теперь toouse позже при доступе к базе данных hello. Если был выбран сервер, который вы создали ранее, можно быть выведен hello пароль toohello административной учетной записи уже создан.
7. Выберите hello же **расположение** , выбранное для hello облачной службы.

    Когда hello облачной службы и базы данных находятся в разных центрах обработки данных (различных регионах), приведет к увеличению задержки и будет выставлен счет за пропускную способность за пределами центра обработки данных hello. Пропускная способность в рамках центра обработки данных предоставляется бесплатно.
8. Проверьте **разрешить службам azure tooaccess сервера**.
9. Нажмите кнопку **выберите** для нового сервера hello.

    ![Новый сервер базы данных SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. Щелкните **Создать**.

### <a name="create-an-azure-storage-account"></a>Создание учетной записи хранения Azure
Учетная запись хранилища Azure предоставляет ресурсы для хранения данных больших двоичных объектов и очереди в облаке hello.

В реальном приложении обычно создают отдельные учетные записи для данных приложения и данных журналов, а также отдельные учетные записи для тестовых данных и рабочих данных. В этом руководстве будет использоваться одна учетная запись.

1. В hello [портал Azure](https://portal.azure.com), нажмите кнопку **Создать > хранения > учетной записи хранения - больших двоичных объектов, файл таблицы, очереди**.
2. В hello **имя** введите префикс URL-адреса.

    Этот текст префикса и hello, отображаемые в окне приветствия будет hello уникальный URL-адрес tooyour учетной записи хранилища. Если префикс Привет вводимых вами уже используется другим пользователем, у вас будет toochoose другой префикс.
3. Набор hello **модель развертывания** слишком*классический*.

4. Набор hello **репликации** раскрывающемся списке слишком**локально избыточное хранилище**.

    При включении георепликации для учетной записи хранения hello хранимых содержимое является реплицированной tooa дополнительный ЦОД tooenable перехода на другой ресурс, случае серьезной аварии в основное расположение hello. Георепликация может потребовать дополнительных затрат. Для тестирования и разработки учетных записей обычно не следует toopay для георепликации. Дополнительные сведения см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).

5. В hello **группы ресурсов**, нажмите кнопку **использовать существующие** и выберите hello группы ресурсов, используемой для hello облачной службы.
6. Набор hello **расположение** раскрывающегося списка toohello же регионе, выбранное для hello облачной службы.

    Когда hello облачной службы и учетной записи хранения находятся в разных центрах обработки данных (различных регионах), приведет к увеличению задержки и будет выставлен счет за пропускную способность за пределами центра обработки данных hello. Пропускная способность в рамках центра обработки данных предоставляется бесплатно.

    Территориальные группы Azure предоставляют механизм toominimize hello расстояние между ресурсами в центре обработки данных, который можно уменьшить задержку. В этом учебнике территориальные группы не используются. Дополнительные сведения см. в разделе [как tooCreate территориальную группу в Azure](http://msdn.microsoft.com/library/jj156209.aspx).
7. Щелкните **Создать**.

    ![Новая учетная запись хранения](./media/cloud-services-dotnet-get-started/newstorage.png)

    В образе hello учетную запись хранения создается с hello URL-адрес `csvccontosoads.core.windows.net`.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Настройка toouse hello решения базы данных Azure SQL, работающей в Azure
Здравствуйте веб-проекта и hello проект рабочей роли каждого имеет собственную строку подключения базы данных, и каждый требуется база данных Azure SQL toohello toopoint, когда работает приложение hello в Azure.

Вы воспользуетесь [преобразование файла Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) hello веб-роли и параметр среды облачной службы для hello рабочей роли.

> [!NOTE]
> В данном разделе и следующем разделе hello хранить учетные данные в файлах проекта. [Не сохраняйте важные данные в общедоступном репозитории исходного кода](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).
>
>

1. В проекте ContosoAdsWeb hello откройте hello *Web.Release.config* файл преобразования для приложения hello *Web.config* файл, удалите блок комментариев hello, содержащий `<connectionStrings>` элемент и вставить Здравствуйте, следующий код на его месте.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Не закрывайте hello файл для редактирования.
2. В hello [портал Azure](https://portal.azure.com), нажмите кнопку **баз данных SQL** hello левой панели щелкните hello базы данных, созданный в этом учебнике и нажмите кнопку **Показать строки подключения**.

    ![Показать строки подключения](./media/cloud-services-dotnet-get-started/showcs.png)

    портал Hello отображает строки соединения, с помощью заполнителя для hello пароля.

    ![Строки подключения](./media/cloud-services-dotnet-get-started/connstrings.png)
3. В hello *Web.Release.config* файл преобразования, удалите `{connectionstring}` и вставьте его месте hello строки подключения ADO.NET из hello портал Azure.
4. В строке подключения hello, вставленного в hello *Web.Release.config* файл преобразования, замените `{your_password_here}` с hello пароль, созданный для hello новой базы данных SQL.
5. Сохраните файл hello.  
6. Выделите и скопируйте строку подключения hello (без кавычек вокруг hello) для использования в hello, выполните действия по настройке hello проект рабочей роли.
7. В **обозревателе решений**в разделе **ролей** hello проекта облачной службы, щелкните правой кнопкой мыши **ContosoAdsWorker** и нажмите кнопку **свойства**.

    ![Свойства роли](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Нажмите кнопку hello **параметры** вкладки.
9. Изменение **конфигурации службы** слишком**облака**.
10. Выберите hello **значение** для hello `ContosoAdsDbConnectionString` задание, а затем вставьте строку подключения hello, скопированный в предыдущем разделе учебника hello hello.

     ![Строка подключения базы данных для рабочей роли](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Сохраните изменения.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Настроить учетную запись хранилища Azure toouse решения hello, работающей в Azure
Строки подключения учетной записи хранилища Azure для проекта веб-роли hello и hello проект рабочей роли хранятся в параметры среды в проект облачной службы hello. Для каждого проекта отсутствует отдельный набор toobe параметры, используемые при запуске приложения hello локально и при выполнении в облаке hello. Обновите параметры среды hello облака для рабочих и веб-проектов роли.

1. В **обозревателе решений**, щелкните правой кнопкой мыши **ContosoAdsWeb** под **ролей** в hello **ContosoAdsCloudService** проекта, а затем нажмите кнопку **Свойства**.

    ![Свойства роли](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Нажмите кнопку hello **параметры** вкладки. В hello **конфигурации службы** раскрывающегося списка выберите **облака**.

    ![Конфигурация облака](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Выберите hello **StorageConnectionString** входа и вы увидите кнопку с многоточием (**...** ), расположенную hello справа от строки hello. Нажмите кнопку hello tooopen кнопку с многоточием hello **Создание строки подключения учетной записи хранилища** диалоговое окно.

    ![Откройте окно создания строки подключения](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. В hello **Создание строки подключения хранилища** диалоговое окно, нажмите кнопку **подписки**, выберите учетную запись хранения hello, которое было создано ранее и нажмите кнопку **ОК**. Если вы еще не вошли, появится запрос на ввод учетных данных учетной записи Azure.

    ![Создайте строку подключения хранилища](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Сохраните изменения.
6. Выполните hello же процедуру, которая используется для hello `StorageConnectionString` hello tooset строка соединения `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` строку подключения.

    Эта строка подключения используется для журнала.
7. Выполните hello же процедуру, которая используется для hello **ContosoAdsWeb** tooset роли обе строки подключения для hello **ContosoAdsWorker** роли. Не забывайте tooset **конфигурации службы** слишком**облака**.

параметры среды роли Hello, настроенного с помощью пользовательского интерфейса Visual Studio hello хранятся в следующие файлы в проекте ContosoAdsCloudService hello hello:

* *ServiceDefinition.csdef* -определяет имена параметров hello.
* *ServiceConfiguration.Cloud.cscfg* -предоставляет значения, по которым будет выполняться приложение hello в облаке hello.
* *ServiceConfiguration.Local.cscfg* -предоставляет значения, по которым приложение hello будет выполняться локально.

Например hello ServiceDefinition.csdef включает hello следующие определения:

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

И hello *ServiceConfiguration.Cloud.cscfg* файл включает hello значениям, введенным для этих параметров в Visual Studio.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

Hello `<Instances>` определяет hello число виртуальных машин, Azure выполняет hello рабочей роли код на. Hello [дальнейшие действия](#next-steps) раздел содержит toomore ссылки на сведения о горизонтальное масштабирование облачной службы

### <a name="deploy-hello-project-tooazure"></a>Развертывание проекта tooAzure hello
1. В **обозреватель решений**, щелкните правой кнопкой мыши hello **ContosoAdsCloudService** облако проекта, а затем выберите **публикации**.

   ![Меню публикации](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. В hello **входа** шага hello **публикации приложения Azure** мастера, нажмите кнопку **Далее**.

    ![Этап входа](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. В hello **параметры** шаг приветствия мастера нажмите кнопку **Далее**.

    ![Этап настроек](./media/cloud-services-dotnet-get-started/pubsettings.png)

    Здравствуйте, параметры по умолчанию в hello **Дополнительно** вкладку допустимы для этого учебника. Сведения о вкладке "Дополнительно" hello, в разделе [мастер публикации приложений Azure](http://msdn.microsoft.com/library/hh535756.aspx).
4. В hello **Сводка** шаг, нажмите кнопку **публикации**.

    ![Сводка действий](./media/cloud-services-dotnet-get-started/pubsummary.png)

   Hello **журнал действий Azure** открывается окно в Visual Studio.
5. Выберите сведения о развертывании hello tooexpand в значок со стрелкой вправо hello.

    Hello развертывания может занять too5 минут или более toocomplete.

    ![Окно журнал действий Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. После завершения состояние развертывания hello, нажмите кнопку hello **веб-приложения URL-адрес** toostart приложения hello.
7. Теперь можно протестировать приложение hello путем создания, просмотра и изменения некоторых рекламные объявления, как при запуске приложения hello локально.

> [!NOTE]
> После завершения тестирования, удаления или остановки hello облачной службы. Даже если вы не используете hello облачной службы, он накапливаемый расходы, так как для него зарезервированные ресурсы виртуальной машины. Если оставить ее работающей, любой кто найдет этот URL-адрес, сможет создать и просмотреть рекламу. В hello [портал Azure](https://portal.azure.com), go toohello **Обзор** для облачной службы, а затем щелкните hello **удалить** кнопку вверху hello страницы приветствия. Если необходимо просто tootemporarily никто другой не доступа к узлу hello, щелкните **остановить** вместо него. В этом случае накладные расходы по-прежнему tooaccrue. Вы можете использовать аналогичную процедуру toodelete hello учетные записи хранилища и базы данных SQL, когда они больше не нужны.
>
>

## <a name="create-hello-application-from-scratch"></a>Создание приложения hello с нуля
Если вы еще не загрузили [приложения hello завершения](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), сделайте это сейчас. Будет скопируйте файлы из проекта загружаются hello в новый проект hello.

Создание приложения hello рекламы Contoso включает hello следующие шаги.

* Создайте новое решение облачной службы в Visual Studio.
* Обновите и добавьте пакеты NuGet.
* Указание ссылок на проекты.
* Настройте строки подключения.
* Добавьте файлы кода.

После создания решения hello вам предстоит рассмотреть hello код, который является уникальным toocloud службы проектов Azure BLOB-объектов и очередей.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Создайте новое решение облачной службы в Visual Studio
1. В Visual Studio выберите **новый проект** из hello **файл** меню.
2. В левой области hello hello **новый проект** диалогового окна разверните **Visual C#** и выберите **облака** шаблонов и выберите hello **облачной службы Azure** шаблона.
3. Имя проекта hello и решения ContosoAdsCloudService и нажмите кнопку **ОК**.

    ![Новый проект](./media/cloud-services-dotnet-get-started/newproject.png)
4. В hello **новая облачная служба Azure** диалогового окна добавьте веб-роли и рабочей роли. Имя веб-роли hello ContosoAdsWeb и имя рабочей роли hello ContosoAdsWorker. (Используйте значок карандаша hello в hello правой панели toochange hello по умолчанию имена ролей hello).

    ![Проект новой облачной службы](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. При появлении hello **новый проект ASP.NET** диалоговое окно приветствия веб-роли, Выбор шаблона MVC hello и нажмите кнопку **изменить аутентификацию**.

    ![Изменить проверку подлинности](./media/cloud-services-dotnet-get-started/chgauth.png)
6. В hello **изменить аутентификацию** диалогового окна выберите **без проверки подлинности**, а затем нажмите кнопку **ОК**.

    ![Без аутентификации](./media/cloud-services-dotnet-get-started/noauth.png)
7. В hello **новый проект ASP.NET** диалоговое окно, нажмите кнопку **ОК**.
8. В **обозревателе решений**, щелкните правой кнопкой мыши hello решение (не hello проектов) и выберите **Add - новый проект**.
9. В hello **Добавление нового проекта** диалогового окна выберите **Windows** под **Visual C#** в hello левой панели, затем щелкните hello **библиотеки классов** шаблон.  
10. Имя проекта hello *ContosoAdsCommon*, а затем нажмите кнопку **ОК**.

    Необходимо tooreference hello hello и контекста модели данных Entity Framework из рабочих и веб-проектов роли. Кроме того можно определить классы, связанные с EF hello в проект веб-роли hello и ссылку на этот проект в проект рабочей роли hello. Но в hello альтернативный подход, проект рабочей роли ссылочные сборки tooweb, которые ему не требуется.

### <a name="update-and-add-nuget-packages"></a>Обновите и добавьте пакеты NuGet
1. Откройте hello **управление пакетами NuGet** диалоговое окно для решения hello.
2. Hello верхней части окна hello, выберите **обновления**.
3. Найдите hello *WindowsAzure.Storage* пакета и, если он находится в списке hello, выберите его и выберите tooupdate hello рабочих и веб-проектов, его и нажмите кнопку **обновление**.

    Клиентская библиотека хранилища Hello обновляется чаще, чем шаблоны проектов Visual Studio, в toobe потребностей только что созданный проект обновлен часто вы найдете этой версии hello.
4. Hello верхней части окна hello, выберите **Обзор**.
5. Найти hello *EntityFramework* NuGet пакета и установить на всех трех проектов.
6. Найти hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet пакет и установите его в проект рабочей роли hello.

### <a name="set-project-references"></a>Установите ссылки проекта
1. В проекте ContosoAdsWeb hello установите проект ContosoAdsCommon toohello ссылки. Щелкните правой кнопкой мыши проект ContosoAdsWeb hello и нажмите кнопку **ссылки** - **Добавление ссылок**. В hello **диспетчер ссылок** установите флажок **решения — проекты** hello левой панели выберите **ContosoAdsCommon**, а затем нажмите кнопку **ОК**.
2. В проекте ContosoAdsWorker hello установите проект ContosAdsCommon toohello ссылки.

    ContosoAdsCommon будет содержать hello Entity Framework данных модели и контекста класса, который будет использоваться в обоих hello внешнего и внутреннего интерфейса.
3. В проекте ContosoAdsWorker hello, задать ссылку слишком`System.Drawing`.

    Эта сборка используется toothumbnails изображения hello tooconvert серверной части.

### <a name="configure-connection-strings"></a>Настройте строки подключения
В этом разделе настройте хранилище Azure и строки подключения SQL для локального тестирования. инструкции по развертыванию Hello ранее в учебнике hello объясняется, как tooset подключение hello строки для при hello приложение выполняется в облаке hello.

1. В проект ContosoAdsWeb hello, hello откройте файл Web.config приложения и вставки hello следующие `connectionStrings` элемента после hello `configSections` элемента.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Если вы используете Visual Studio 2015 или более поздней версии, замените v11.0 на MSSQLLocalDB.
2. Сохраните изменения.
3. В проекте ContosoAdsCloudService hello, щелкните правой кнопкой мыши ContosoAdsWeb под **ролей**и нажмите кнопку **свойства**.

    ![Свойства роли](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. В hello **ContosAdsWeb [роль]** окне свойств щелкните hello **параметры** , а затем щелкните **добавить параметр**.

    Оставить **конфигурации службы** значение слишком**все конфигурации**.
5. Добавьте настройку с именем *StorageConnectionString*. Задать **тип** слишком*ConnectionString*и задайте **значение** слишком*UseDevelopmentStorage = true*.

    ![Новая строка подключения](./media/cloud-services-dotnet-get-started/scall.png)
6. Сохраните изменения.
7. Выполните hello же процедура tooadd строки подключения хранилища в свойствах роли ContosoAdsWorker hello.
8. По-прежнему в hello **ContosoAdsWorker [роль]** окно свойств добавить другую строку подключения:

   * Имя: ContosoAdsDbConnectionString
   * Тип: строка
   * Значение: Вставить hello же строка подключения, используемая для проекта веб-роли hello. (следующий пример hello предназначен для Visual Studio 2013. Не забывайте hello toochange источника данных при копировании в этом примере, и вы используете Visual Studio 2015 или более поздней версии.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Добавьте файлы кода
В этом разделе скопируйте файлы кода из решения загружаются hello в новое решение hello. Hello следующих разделах будет отображать и объясняются основные части этого кода.

файлы tooadd tooa проект или папку, щелкните правой кнопкой мыши проект hello или папку и нажмите кнопку **добавить** - **существующий элемент**. Выберите файлы hello и нажмите кнопку **добавить**. Если запрос на подтверждение tooreplace существующие файлы, нажмите кнопку **Да**.

1. В проекте ContosoAdsCommon hello, удалите hello *Class1.cs* и добавьте в его месте hello *Ad.cs* и *ContosoAdscontext.cs* файлы из hello загружен проекта.
2. В проекте ContosoAdsWeb hello добавьте следующие файлы из проекта загружаются hello hello.

   * *Global.asax.cs*.  
   * В hello *представления\общие* папки:  *\_Layout.cshtml*.
   * В hello *Views\Home* папки: *Index.cshtml*.
   * В hello *контроллеров* папки: *AdController.cs*.
   * В hello *Views\Ad* папку (сначала создать папки hello): пять *.cshtml* файлов.
3. Добавьте в проект ContosoAdsWorker hello, *WorkerRole.cs* из hello загружен проекта.

Теперь можно построить и запустить приложение hello, как описано ранее в учебнике hello и будет использовать приложение hello локальной базы данных и ресурсов эмулятора хранилища.

Hello ниже разделы содержат определение кода hello tooworking, связанные с hello среды Azure, большие двоичные объекты и очереди. Этот учебник не объясняют, как toocreate MVC контроллеры и представления с помощью формирования шаблонов, как toowrite кода Entity Framework, работает с базами данных SQL Server или основы hello асинхронного программирования в ASP.NET 4.5. Сведения об этих темах см. в разделе hello следующие ресурсы:

* [Начало работы с MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Начало работы с EF 6 и MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Введение tooasynchronous программирование в .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
файл Ad.cs Hello определяет перечисление для категорий ad и класс сущности POCO ad сведения.

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Класс ContosoAdsContext Hello указывает, используется класс Ad hello в коллекцию DbSet, что платформа Entity Framework будут храниться в базе данных SQL.

```csharp
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
```

Класс Hello имеет два конструктора. Здравствуйте, сначала из них используется hello веб-проекта и указывает имя строки подключения, которая хранится в файле Web.config hello hello. Второй конструктор Hello позволяет toopass в hello фактическое строка подключения hello проект рабочей роли, поскольку он не содержит файл Web.config. Вы уже видели раньше была сохранена эта строка подключения, куда вы увидите позже как код hello извлекает hello строку подключения, когда он создает экземпляр класса DbContext hello.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Код, который вызывается из hello `Application_Start` метод создает *изображения* контейнер больших двоичных объектов и *изображения* очередь, если они еще не существуют. Это гарантирует, что каждый раз, когда начать работу с новой учетной записи хранения или начать использовать эмулятор хранилища hello на новом компьютере, контейнер hello необходимые больших двоичных объектов и очереди будет создана автоматически.

Здравствуйте, учетной записи хранилища toohello кода получает доступ с помощью строки подключения к хранилищу hello из hello *.cscfg* файла.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

Затем он возвращает toohello ссылки *изображения* большого двоичного объекта контейнера, создает контейнер hello в том случае, если он еще не существует, и наборы разрешений доступа на новый контейнер hello. По умолчанию новые контейнеры только позволяют клиентам с помощью учетной записи хранилища больших двоичных объектов tooaccess учетные данные. Hello веб-сайт должен hello public toobe больших двоичных объектов, чтобы он может отображать изображения с помощью URL-адреса, большие двоичные объекты toohello точки изображения.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

Аналогичный код получает toohello ссылки *изображения* ставить в очередь и создает новую очередь. В этом случае изменения разрешений не требуется.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb — \_Layout.cshtml
Hello *_Layout.cshtml* файл задает имя приложения hello в hello верхний и нижний колонтитулы и создает запись меню «Объявления».

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hello *Views\Home\Index.cshtml* файла отображаются категории ссылки на домашнюю страницу приветствия. ссылки Hello передать целое значение hello hello `Category` перечисления в страницу индекса рекламы toohello переменной строки запроса.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
В hello *AdController.cs* файл, hello вызывает конструктор hello `InitializeStorage` метод toocreate клиентская библиотека хранилища Azure объекты, которые предоставляют API для работы с BLOB-объектов и очередей.

После создания кода hello получает toohello ссылки *изображения* большого двоичного объекта контейнера, как было показано ранее в *Global.asax.cs*. При этом он устанавливает [политику повторения](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) по умолчанию, подходящую для веб-приложения. политика повтора экспоненциально растущим по умолчанию Hello зависание веб-приложения hello дольше, чем через минуту на нескольких повторных попыток для временных ошибок. политика повтора Hello, указанные здесь ожидает три секунды после каждого повторите для копирования toothree попыток.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Аналогичный код получает toohello ссылки *изображения* очереди.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

Большая часть кода hello контроллера является типичным для работы с моделью данных Entity Framework, с помощью класса DbContext. Исключение — hello HttpPost `Create` метод, который отправляет файл и сохраняет его в хранилище больших двоичных объектов. предоставляет связыватель модели Hello [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello метод объекта.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Если hello пользователь выбрал tooupload файла, кода hello передает файл hello, сохраняет его в большой двоичный объект и обновляет запись в базе данных Ad hello URL-адресом toohello больших двоичных объектов.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Hello код, hello передачи находится в hello `UploadAndSaveBlobAsync` метод. Он создает имя GUID для hello больших двоичных объектов, передачи и сохраняет файл hello и возвращает toohello сохранен эталонный BLOB-объект.

```csharp
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
```

После hello HttpPost `Create` метод передает большой двоичный объект и обновления hello базы данных, он создает tooinform очереди сообщений, образ будет готов для преобразования tooa эскиз серверной части процесса.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

Здравствуйте, код для hello HttpPost `Edit` метод аналогичен за исключением того, что если hello пользователь выбирает новый файл образа необходимо удалить все большие двоичные объекты, которые уже существуют.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

Следующий пример Hello показан hello код, который удаляет большие двоичные объекты при удалении ad.

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml и Details.cshtml
Hello *Index.cshtml* файла отображаются эскизы с hello другие данные ad.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Hello *Details.cshtml* файл отображает hello полноразмерное изображение.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml и Edit.cshtml
Hello *Create.cshtml* и *Edit.cshtml* -файлы указывают кодирования, что включает hello контроллера tooget hello форм `HttpPostedFileBase` объекта.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

`<input>` Элемент предписывает tooprovide браузера hello диалоговое окно выбора файла.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - метод OnStart
Hello Azure рабочей роли среда вызывает hello `OnStart` метод в hello `WorkerRole` класс при hello рабочая роль начало работы и вызывает hello `Run` метод при hello `OnStart` метод завершения.

Hello `OnStart` метод возвращает строку подключения базы данных hello из hello *.cscfg* файл и передает его toohello класса Entity Framework DbContext. поставщик SQLClient Hello используется по умолчанию, поэтому не требуется toobe указан поставщик hello.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

После этого метод hello получает учетную запись хранения toohello ссылки и создает hello контейнер больших двоичных объектов и очереди, если они не существуют. Код Hello, — примерно toowhat, вы уже видели в веб-роли hello `Application_Start` метод.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - метод Run
Hello `Run` метод вызывается, когда hello `OnStart` метод завершает свою работу инициализации. метод Hello выполняется бесконечный цикл, который отслеживает наличие новых сообщений очереди и обрабатывает их при поступлении.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

После каждой итерации цикла hello сообщения в очереди, если было обнаружено программа hello бездействует в течение секунды. Это предотвращает расходов чрезмерного ЦП времени и объема хранилища транзакции hello рабочей роли. Hello группа консультантов по Microsoft истории о разработчике, забывший tooinclude, развернуты tooproduction и указывает слева для отпуска. Когда он вернулся его контроля стоимость которой превышает отпуска hello.

Иногда hello содержимое сообщения в очереди приводит к ошибке во время обработки. Это называется *подозрительное сообщение*, и если вы только произошла ошибка и перезапуска цикла hello, ведут бесконечные попробуйте tooprocess это сообщение.  Поэтому блок catch hello включает if Здравствуйте, сколько раз приложение hello предпринял tooprocess инструкцию, которая проверяет toosee текущего сообщения, и если прошло более 5 раз приветственное сообщение удаляется из очереди hello.

`ProcessQueueMessage` вызывается, когда сообщение найдено в очереди.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

Этот код считывает URL-адрес hello базы данных tooget hello изображения, преобразует эскиз tooa рисунка hello, сохраняет эскиз hello в большом двоичном объекте, обновляет базу данных hello URL-адрес эскиза blob hello и удаляет сообщение hello очереди.

> [!NOTE]
> Здравствуйте, код в hello `ConvertImageToThumbnailJPG` метод использует классы в пространстве имен System.Drawing hello для простоты. Однако hello классы этого пространства имен были разработаны для работы с Windows Forms. Они не поддерживаются в службе Windows или ASP.NET. Дополнительные сведения о параметрах обработки изображений см. в статьях [Back to Basics: Dynamic Image Generation, ASP.NET Controllers, Routing, IHttpHandlers, and runAllManagedModulesForAllRequests](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Основы: создание динамического образа, контроллеры ASP.NET, маршрутизация, IHttpHandlers и runAllManagedModulesForAllRequests) и [Deep Inside Image Resizing and scaling with ASP.NET and IIS with ImageResizing.net author Nathanael](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Особенности изменения размеров и масштабирования образов с использованием ASP.NET и IIS с автором ImageResizing.net Натанаэлем).
>
>

## <a name="troubleshooting"></a>Устранение неполадок
В случае, если что-то не сработает, пока вы следуете инструкциям hello в этом учебнике, ниже приведены некоторые распространенные ошибки и каким образом tooresolve их.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
Hello `RoleEnvironment` при запуске приложения в Azure или при запуске локально с помощью эмулятора вычислений Azure hello объекта передается Azure.  Если эта ошибка появляется при запуске локально, убедитесь, что вы указали проекта ContosoAdsCloudService hello hello запускаемым проектом. Это настраивает hello toorun проекта, с помощью эмулятора вычислений Azure hello.

Одно из действий hello использует приложение hello hello Azure RoleEnvironment для — tooget подключения hello строковых значений, хранящихся в hello *.cscfg* файлы, поэтому отсутствует строка подключения имеет другой причиной этого исключения. Убедитесь, что вы создали StorageConnectionString приветствия для облака, как и локальные конфигурации в проекте ContosoAdsWeb hello и создания обеих строках подключения для обеих конфигураций, в проекте ContosoAdsWorker hello. Если сделать **найти все** поиска для StorageConnectionString в hello всего решения, вы должны увидеть его 9 раз в 6-файлы.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Не может переопределять tooport xxx. Новый порт ниже минимально разрешенного значения 8080 для протокола http
Попробуйте изменить номер порта hello hello веб-проекта. Щелкните правой кнопкой мыши проект ContosoAdsWeb hello и нажмите кнопку **свойства**. Нажмите кнопку hello **Web** , а затем измените номер порта hello в hello **URL-адрес проекта** параметр.

Другим способом, hello проблему можно разрешить см. hello в следующем разделе.

### <a name="other-errors-when-running-locally"></a>Другие ошибки при работе локально
По умолчанию новой облачной службы проекты используют hello вычислений Azure emulator express toosimulate hello среды Azure. Это облегченная версия полной вычислений hello и в некоторых условиях hello полный эмулятор будут работать при версию express hello не.  

toochange hello проекта toouse hello полный эмулятор, щелкните правой кнопкой мыши проект ContosoAdsCloudService hello и нажмите кнопку **свойства**. В hello **свойства** щелкните hello **Web** , а затем щелкните hello **использовать полный эмулятор** переключатель.

В приложение hello toorun заказов с hello полный эмулятор имеют tooopen Visual Studio с правами администратора.

## <a name="next-steps"></a>Дальнейшие действия
Hello приложение Contoso рекламы намеренно была сохранена в простой учебник Приступая к работе. Например, он не реализует [внедрения зависимостей](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) или hello [репозитория и единицу работы шаблоны](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), это не [используют интерфейс для ведения журнала](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), он не использовал [ EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) изменений в модели данных toomanage или [устойчивость подключений EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage временной ошибки сети и т. д.

Ниже приведены некоторые примеры приложений облачной службы, демонстрируют дополнительные реальных написания безопасного кода, перечисленными далее от менее сложные toomore сложных.

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Аналогично окну tooContoso рекламы но реализует дополнительные функции и дополнительные реальных написания безопасного кода.
* [Многоуровневое облачное приложение Azure с таблицами, квотами, и большими двоичными объектами](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36). Представляет таблицы, а также большие двоичные объекты и очереди службы хранилища Azure. Исходя из более старой версии hello Azure SDK для .NET, требует toowork некоторые изменения в текущей версии hello.
* [Основы облачных служб в Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Полный образец, демонстрирующий широкий спектр советы и рекомендации, созданных группой шаблонов и методов Майкрософт hello.

Общие сведения о разработке для облака hello см. в разделе [Создание реальных облачных приложений с Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Для tooAzure Видеообзор хранилища лучшие шаблоны и практические рекомендации см. в разделе [хранилища Microsoft Azure — новые, рекомендации и шаблоны](http://channel9.msdn.com/Events/Build/2014/3-628).

Дополнительные сведения см. в разделе hello следующие ресурсы:

* [Облачные службы Azure, часть 1: Введение](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Как toomanage облачных служб](cloud-services-how-to-manage.md)
* [Хранилище Azure](/documentation/services/storage/)
* [Как поставщиком услуг toochoose облака](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
