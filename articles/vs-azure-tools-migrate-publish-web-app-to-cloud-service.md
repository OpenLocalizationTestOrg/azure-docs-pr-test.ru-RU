---
title: "aaaHow tooMigrate и опубликовать tooan веб-приложения Azure облачной службы из Visual Studio | Документы Microsoft"
description: "Узнайте, как toomigrate и публикация вашего tooan приложения web облачной службы Azure с помощью Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Как: миграция и публикация веб-приложения tooan облачной службы Azure из Visual Studio
преимущества tootake Здравствуйте размещения служб и масштабируемости Azure, могут требуется toomigrate и публикация веб-приложения tooan Azure облачной службы. Веб-приложение можно запустить в Azure с минимальными изменениями tooyour существующего приложения.

> [!NOTE]
> Этот раздел посвящен развертывание служб toocloud, не tooweb сайтов. Сведения о развертывании tooweb сайтов см. в разделе [развертывание веб-приложения в службе приложений Azure](app-service-web/web-sites-deploy.md).
>
>

Список шаблонов, поддерживаемых для Visual C# и Visual Basic, см в разделе hello **поддерживаемые шаблоны проектов** далее в этом разделе.

Для начала необходимо предоставить Azure доступ к веб-приложению из Visual Studio. Hello, Следующая иллюстрация показывает toopublish ключевых шагов hello существующего веб-приложения путем добавления проекта Azure toouse для развертывания. Этот процесс добавляет в проект Azure с hello требуется веб-роли tooyour решения. В зависимости от типа hello веб-проекта, который имеет hello свойства проекта для сборок также обновляются при hello пакету служб требуются дополнительные сборки для развертывания.

![Публикация tooMicrosoft приложения Web Azure](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Hello **преобразовать**, **преобразовать проект облачной службы tooAzure** команда отображается только для hello веб-проекта в решении. Например команда hello недоступна для проекта Silverlight в решении.
> При создании пакета служб или публикации tooAzure вашего приложения, могут возникнуть предупреждения и ошибки. Эти предупреждения и ошибки могут помочь устранить проблемы перед развертыванием tooAzure. Например, может отобразиться предупреждение об отсутствии сборки. Дополнительные сведения о том, как tootreat все предупреждения как ошибки, отображается [настроить проект облачной службы Azure с помощью Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Если сборка приложения, запустить его локально с помощью эмулятора вычислений hello или опубликовать его tooAzure, может появиться следующая ошибка в hello hello **список ошибок** окна: **hello указанный путь, имя файла или оба имеют слишком большую длину** . Эта ошибка возникает, поскольку hello hello полное Azure имя проекта является слишком длинное. Длина Hello hello имя проекта, включая полный путь hello, не должна превышать 146 символов. Например, это имя hello полного проекта, включая путь к файлу проекта Azure, созданного для приложения Silverlight: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Может потребоваться toomove вашего решения tooa другой каталог, имеющий более короткий путь tooreduce hello период hello полное имя проекта.
>
>

toomigrate и публиковать tooAzure приложения web из Visual Studio, выполните следующие действия.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Включить веб-приложения для развертывания tooAzure
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>веб-приложения для развертывания tooAzure tooenable
1. tooenable веб-приложения для развертывания tooAzure, Привет открыть контекстное меню для веб-проекта в решении и выберите команду Добавить проект развертывания Azure.

    происходят следующие действия Hello:

   * Проект Azure вызывается `<name of hello web project>.Azure` добавляется toohello решение для приложения.
   * Веб-роль для hello веб-проекта добавляется toothis проекта Azure.
   * Hello **Копировать локально** свойству tootrue для сборок, которые необходимы для MVC 2, MVC 3, MVC 4 и бизнес-приложений Silverlight. Это добавляет эти сборки toohello пакет службы, используемый для развертывания.

   > [!IMPORTANT]
   > Если у вас есть другие сборки или файлы, необходимые для этого веб-приложения, необходимо вручную задать свойства hello для этих файлов. Сведения о том, как tooset этих свойств отображается hello раздел **включаемых файлов в пакет службы hello** далее в этой статье.
   >
   > [!NOTE]
   > Если веб-роль для конкретного веб-проекта уже существует в проекте Azure в решении hello **преобразовать**, **преобразовать проект облачной службы tooAzure** hello контекстном меню этого веб-проекта не отображается .
   >
   >

   Если имеется несколько веб-проектов веб-приложения и требуется toocreate веб-ролей для каждого веб-проекта, необходимо выполнить действия hello в этой процедуре для каждого веб-проекта. В результате для каждой веб-роли будут созданы отдельные проекты Azure, а каждый веб-проект можно будет опубликовать отдельно. Кроме того можно вручную добавить другой проект веб-роли tooan существующие Azure в веб-приложения. toodo, Привет открыть контекстное меню для hello **ролей** выберите папку в проекте Azure **добавить**, затем **проект веб-роли в решении**, выберите hello tooadd проект как веб- роли, а затем выберите hello **ОК** кнопки.

## <a name="use-an-azure-sql-database-for-your-application"></a>Использование базы данных SQL Azure для приложения
Если строка подключения для веб-приложения, использующего базу данных SQL Server, на локальном компьютере hello, необходимо изменить этот toouse строку соединения экземпляра базы данных SQL, размещенной в Azure вместо.

> [!IMPORTANT]
> Подписку необходимо включить toouse базы данных SQL. Если для доступа к подписке hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), чтобы выяснить, какие услуги обеспечивает подписка. Hello применяются следующие инструкции выпущена toohello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885). Если вы используете hello [портал Azure](http://portal.microsoft.com), пропустить toohello следующей процедуре.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse экземпляр базы данных SQL в веб-роли для строки подключения
1. toocreate экземпляра базы данных SQL в hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), следуйте указаниям hello hello следующей статьей: [Создание базы данных SQL Server](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > При настройке правил брандмауэра hello для экземпляра базы данных SQL, необходимо выбрать hello **разрешить другим службам Azure tooaccess серверу** флажок.
   >
   >
2. toocreate экземпляра базы данных SQL toouse для строки подключения, выполните действия hello в следующем подразделе hello hello следующей статьей: [создать базу данных SQL](http://go.microsoft.com/fwlink/?LinkId=225110).
3. toouse строку подключения ADO.NET hello toocopy для строки подключения, выполните следующие шаги в hello hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Выберите hello **базы данных** кнопку и откройте hello узел для hello подписки используется toocreate экземпляра базы данных SQL.
   2. toodisplay hello доступных экземпляров баз данных SQL, выберите hello **баз данных SQL** узла.
   3. свойства hello toodisplay hello базы данных, выберите базу данных hello. Hello **свойства** отображается представление.

      > [!NOTE]
      > Если hello **свойства** не отображается, может потребоваться tooopen его с помощью hello разделитель.
      >
      >
   4. строки подключения toodisplay hello, выберите tooView далее кнопку с многоточием (...) hello.

      Hello **строки подключения** откроется диалоговое окно.
   5. hello toocopy строки подключения ADO.NET, выделите текст hello и нажмите сочетание клавиш Ctrl + C hello.
   6. диалоговое окно приветствия tooclose выберите hello **закрыть** кнопки.
4. подключение hello tooreplace строка в toouse файл web.config hello этого экземпляра базы данных SQL, откройте файл web.config hello, выделите hello существующую строку подключения и нажмите сочетание клавиш Ctrl + V hello. Hello строку подключения ADO.NET для hello экземпляра базы данных SQL заменяет существующую строку соединения hello.
5. Также необходимо добавить параметр hello `MultipleActiveResultSets=True` toohello строку подключения. Hello строка подключения должна иметь hello следующий формат:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (Необязательно) Альтернативный метод toochanging hello строка подключения непосредственно в файле web.config hello является tooadd раздел в один из файлов преобразования web.config hello в зависимости от конфигурации построения hello использовать toocreate ваш пакет служб. Откройте файл Web.Debug.Config hello или файл Web.Release.Config hello. Добавьте следующий раздел в этот файл hello:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Сохранение измененного файла hello и повторно опубликуйте приложение.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>Здравствуйте, toouse экземпляра базы данных SQL с помощью классического портала Azure
1. В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), выберите узел базы данных SQL hello.

   * Если появится экземпляр базы данных SQL, которые должны toouse hello, выберите tooopen его.
   * Если вы еще не создали все экземпляры, выберите соответствующую ссылку hello и затем создайте экземпляр.
2. После открытия или создания экземпляра базы данных, выберите hello **строки подключения** ссылку.
3. Hello нижней части страницы приветствия выберите параметры брандмауэра tooconfigure ссылку hello и примите значения по умолчанию hello или настроить необходимые значения hello.
4. Скопируйте строку подключения ADO.NET hello, вставьте его в файл web.config поверх hello старой строки подключения для hello локальной базы данных, а также являться убедиться, что tooadd `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Публикация tooAzure веб-приложения
### <a name="toopublish-a-web-application-tooazure"></a>toopublish tooAzure приложения Web
1. приложение hello tootest в hello локальной среде разработки с помощью эмулятора вычислений Azure hello, Привет открыть контекстное меню для hello Azure project для hello веб-роли и выберите **Назначить запускаемым проектом**. Затем выберите **Отладка**, **Начать отладку** (клавиша **F5**).

    Hello **hello запуск среды отладки Azure** откроется диалоговое окно и запуске приложения hello в браузере hello. Подробные сведения о как toostart каждый тип веб-приложения в hello эмулятор вычислений см. в разделе таблица hello в этом разделе.
2. tooset hello служб tooAzure toopublish вашего приложения, необходимо иметь учетную запись Майкрософт и подписка на Azure. Используйте hello шагов в следующий раздел tooset вашей службы hello: [toopublish подготовки или развертывании приложения Azure из Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. tooAzure приложения web toopublish hello, откройте контекстное меню hello hello веб-проекта и выберите **публикации tooAzure**.

    Hello **публикации приложения Azure** откроется диалоговое окно и Visual Studio запускает процесс развертывания hello. Дополнительные сведения о как toopublish hello приложения в разделе hello **публикации приложения Azure из Visual Studio** в [публикация облачной службы с помощью средства Azure hello](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > Также можно опубликовать веб-приложение hello из hello проекта Azure. toodo это, откройте контекстное меню проекта Azure hello hello и выберите **публикации**.
   >
   >
4. toosee hello ход выполнения развертывания hello, можно просмотреть hello **журнал действий Azure** окна. Этот журнал отображается автоматически при запуске процесса развертывания hello. Можно развернуть элемент строку hello в журнал действий hello tooshow подробные сведения, как показано в следующих рисунке hello:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. Процесс развертывания (необязательно) toocancel hello, откройте hello контекстное меню для элемента строки hello в журнал действий hello и выберите **"Отмена" и удалите**. Это останавливает процесс развертывания hello и удаляет среду развертывания hello из Azure.

   > [!NOTE]
   > tooremove был этой среды развертывания после его развертывания необходимо использовать hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (Необязательно) После запуска экземпляров ролей Visual Studio автоматически отображает среду развертывания hello в hello **вычислений Azure** узел в **Cloud Explorer** или **обозревателя серверов**. Здесь можно просмотреть состояние hello hello отдельных экземпляров ролей.

    Hello следующей иллюстрации показаны hello экземпляры роли в **обозревателя серверов** пока они находятся в состоянии Initializing hello:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess приложения после развертывания, выберите hello стрелку Далее tooyour развертыванием, когда состояние **завершено** отображается в hello **журнал действий Azure**. Это позволит отобразить hello URL-адрес для веб-приложения в Azure. См. в следующей таблице описаны hello как toostart определенный тип веб-приложения из Azure hello.

    Привет, в следующей таблице приведены сведения hello об toostart определенного веб-приложений с Azure или toorun или отладки веб-приложения, локально с помощью hello эмулятор вычислений Azure.

   | Тип веб-приложения | Привет, запуск и отладка локально с помощью эмулятора вычислений | Выполнение в Azure |
   | --- | --- | --- |
   | Веб-приложение ASP.NET |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Щелкните гиперссылку URL-адрес hello, отображаемую на hello **развертывания** вкладке hello **журнал действий Azure** tooload hello начальной страницы в браузере hello. |
   | Веб-приложение ASP.NET MVC 2 |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Щелкните гиперссылку URL-адрес hello, отображаемую на hello **развертывания** вкладке hello **журнал действий Azure** tooload hello начальной страницы в браузере hello. |
   | Веб-приложение ASP.NET MVC 3 |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Щелкните гиперссылку URL-адрес hello, отображаемую на hello **развертывания** вкладке hello **журнал действий Azure** tooload hello начальной страницы в браузере hello. |
   | Веб-приложение ASP.NET MVC 4 |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Щелкните гиперссылку URL-адрес hello, отображаемую на hello **развертывания** вкладке hello **журнал действий Azure** tooload hello начальной страницы в браузере hello. |
   | Пустое веб-приложение ASP.NET |Необходимо добавить ASPX-страницы в приложении, которое устанавливается в качестве начальной страницы приветствия для веб-проекта. Hello меню, выберите **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Если в приложении ASPX-страницы по умолчанию, выберите гиперссылку URL-адрес hello, отображаемую на hello **развертывания** вкладке hello **журнал действий Azure** и загрузки этой страницы в браузере hello. При наличии другой ASPX-страницы требуется toonavigate toothis страницы с помощью hello следующая формата URL-адрес:`<url for deployment>/<name of page>.aspx` |
   | Приложение Silverlight |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Для приложения с помощью hello следующая формата URL-адрес необходимо toonavigate toohello определенную страницу.`<url for deployment>/<name of page>.aspx` |
   | Бизнес-приложение Silverlight |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Для приложения с помощью hello следующая формата URL-адрес необходимо toonavigate toohello определенную страницу.`<url for deployment>/<name of page>.aspx` |
   | Приложение навигации Silverlight |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Для приложения с помощью hello следующая формата URL-адрес необходимо toonavigate toohello определенную страницу.`<url for deployment>/<name of page>.aspx` |
   | Приложение службы WCF |Hello SVC-файла необходимо задать как hello начальной страницы для проекта службы WCF. Hello меню, выберите **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Toonavigate toohello svc-файла, необходимые для приложения с помощью hello следующая формата URL-адрес.`<url for deployment>/<name of service file>.svc` |
   | Приложение службы рабочего процесса WCF |Hello SVC-файла необходимо задать как hello начальной страницы для проекта службы WCF. Hello меню, выберите **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Toonavigate toohello svc-файла, необходимые для приложения с помощью hello следующая формата URL-адрес.`<url for deployment>/<name of service file>.svc` |
   | Динамические сущности ASP.NET |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Необходимо обновить строку подключения hello (см. следующий раздел). Необходимо также toonavigate toohello определенную страницу для приложения с помощью hello следующая формата URL-адрес:`<url for deployment>/<name of page>.aspx` |
   | TooSQL Linq динамических данных ASP.NET |Hello меню, выберите пункты **отладки**, **начать отладку** (Клавиатура: выберите hello **F5** ключа.). |Выполните шаги этой процедуры hello: использование базы данных SQL Azure для приложения (см. раздел ранее в этом разделе). Необходимо также toonavigate toohello определенную страницу для приложения с помощью hello следующая формата URL-адрес:`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Обновление строки подключения для динамических сущностей ASP.NET
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate строку подключения для динамических сущностей ASP.NET
1. toocreate базы данных SQL Azure, который может использоваться для веб-приложение динамических сущностей ASP.NET, выполните действия hello в процедуре hello **использование базы данных SQL Azure для приложения** ранее в этом разделе.
2. Добавить hello таблицы и поля, необходимые для этой базы данных из hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Строка подключения Hello для этого типа приложения имеет следующий формат в файле web.config hello hello:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Обновление hello *connectionString* значение с hello строку подключения ADO.NET для базы данных SQL Azure следующим образом:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. файл web.config hello toosave hello изменения, внесенные toohello строку подключения, в строке меню hello выберите **файл**, **сохранить файл web.config**.

## <a name="supported-project-templates"></a>Поддерживаемые шаблоны проектов
toopublish tooAzure приложения web hello приложение должно использовать один из шаблонов проекта hello для C# или Visual Basic, перечисленных в следующей таблице hello.

| Группа шаблонов проекта | Шаблон проекта |
| --- | --- |
| Web |Веб-приложение ASP.NET |
| Web |Веб-приложение ASP.NET MVC 2 |
| Web |Веб-приложение ASP.NET MVC 3 |
| Web |Веб-приложение ASP.NET MVC 4 |
| Web |Пустое веб-приложение ASP.NET |
| Web |Пустое веб-приложение ASP.NET MVC 2 |
| Web |Веб-приложение динамических сущностей данных ASP.NET |
| Web |TooSQL динамических данных Linq ASP.NET веб-приложения |
| Silverlight |Приложение Silverlight |
| Silverlight |Бизнес-приложение Silverlight |
| Silverlight |Приложение навигации Silverlight |
| WCF |Приложение службы WCF |
| WCF |Приложение службы рабочего процесса WCF |
| Рабочий процесс |Приложение службы рабочего процесса WCF |

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о публикации см. в разделе [tooPublish подготовки или развертывании приложения Azure из Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Ознакомьтесь также со статьей [Настройка именованных учетных данных для проверки подлинности](vs-azure-tools-setting-up-named-authentication-credentials.md).
