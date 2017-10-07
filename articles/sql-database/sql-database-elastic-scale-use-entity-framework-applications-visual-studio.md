---
title: "aaaUsing эластичной базы данных клиентской библиотеки с Entity Framework | Документы Microsoft"
description: "Использование клиентской библиотеки эластичной базы данных и Entity Framework для создания баз данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>Использование клиентской библиотеки эластичных баз данных с Entity Framework
В этом документе показаны изменения hello в приложении Entity Framework, которые требуется toointegrate с hello [эластичной базы данных средства](sql-database-elastic-scale-introduction.md). Hello основное внимание уделяется составление [управления карты сегментов](sql-database-elastic-scale-shard-map-management.md) и [маршрутизации в зависимости от данных](sql-database-elastic-scale-data-dependent-routing.md) с Entity Framework hello **Code First** подход. Hello [сначала - код новой базы данных](http://msdn.microsoft.com/data/jj193542.aspx) учебник по EF служит в качестве рабочего примера в этом документе. Образец кода Hello, сопровождающие данный документ является частью эластичной базы данных средства набор образцов для hello примеры кода Visual Studio.

## <a name="downloading-and-running-hello-sample-code"></a>Загрузка и запуск образца кода hello
toodownload hello код для этой статьи:

* Требуется Visual Studio 2012 или более поздней версии. 
* Загрузите hello [эластичных БД средства для SQL Azure — пример интеграции Entity Framework](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) с MSDN. Распакуйте папку tooa образец hello по своему усмотрению.
* Запустите Visual Studio. 
* Откройте Visual Studio, выберите "Файл" -> "Открыть проект или решение". 
* В hello **Открытие проекта** диалоговое окно, найдите загруженный образец toohello и выберите **EntityFrameworkCodeFirst.sln** tooopen образец hello. 

Образец hello toorun, необходимые toocreate три пустых баз данных в базе данных SQL Azure.

* База данных диспетчера сопоставления сегментов
* База данных сегмента 1
* База данных сегмента 2

После создания этих баз данных, заполните заполнителями hello в **Program.cs** имя сервера базы данных SQL Azure, hello имена баз данных и баз данных toohello tooconnect учетные данные. Выполните сборку решения hello в Visual Studio. Visual Studio загрузит hello необходимые пакеты NuGet для hello эластичной базы данных клиентской библиотеки, Entity Framework и Transient Fault handling как часть процесса построения hello. Убедитесь, что для вашего решения включена функция восстановления пакетов NuGet. Этот параметр можно включить, щелкнув hello файл решения в обозревателе решений Visual Studio hello. 

## <a name="entity-framework-workflows"></a>Рабочие процессы Entity Framework
Entity Framework разработчики основываются на одном из следующих четырех toobuild приложений рабочих процессов и tooensure сохраняемости для объектов приложения hello: 

* **Code First (новая база данных)**: hello EF разработчик создает модель hello в коде приложения hello и затем EF приводит к возникновению ошибки hello базы данных из него. 
* **Code First (существующей базы данных)**: hello developer позволяет EF создание кода приложения hello hello модели из существующей базы данных.
* **Модели первого**: hello разработчик создает модель hello в конструкторе EF hello и затем EF создает hello базы данных из модели hello.
* **Базы данных первой**: hello разработчик использует EF tooinfer hello модели из существующей базы данных для работы с проектами. 

Все эти подходы полагаться на tootransparently класса DbContext hello управление подключения к базе данных и схемы базы данных для приложения. Обсуждаются более подробно далее в документе hello различные конструкторы базового класса DbContext hello Разрешить разные уровни контроля над создания соединения в базе данных создания начальной загрузки и схемы. Проблемы возникают в первую очередь по hello факт, что управление соединениями hello базы данных, предоставляемые EF пересекается с возможность управления подключения hello hello данных зависимых маршрутизации интерфейсов, предоставляемых клиентской библиотекой hello эластичной базы данных. 

## <a name="elastic-database-tools-assumptions"></a>Допущения в отношении средств эластичной базы данных
Определения терминов см. в статье [Глоссарий по средствам работы с эластичными базами данных](sql-database-elastic-scale-glossary.md).

При использовании клиентской библиотеки эластичной базы данных данные приложения разделяются на сегменты, называемые шардлетами. Подсегменты идентифицируются ключ сегментирования и сопоставленные toospecific баз данных. Приложения могут содержать любое количество баз данных, при необходимости и распределить Подсегменты tooprovide hello Недостаточно емкости или производительности, заданному текущим требованиям бизнеса. сопоставление Hello баз данных toohello значения ключа сегментирования хранится hello эластичной базы данных клиентские API, предоставляемые карта сегментов. Для краткости мы называем эту функцию **Shard Map Management**(Управление сопоставлениями сегментов), или SMM. карта сегментов Hello также служит в качестве hello посредника подключений к базе данных для запросов, которые используются для передачи ключа сегментирования. Мы называем возможность toothis как **маршрутизации в зависимости от данных**. 

диспетчера карты сегментов Hello помогает защитить пользователей от несогласованные представления данных подсегмента, может возникать, когда выполняются операции Подсегмент одновременных операций управления (например, перемещению данных из одного сегмента tooanother). Таким образом, toodo hello карт сегментов, которые управляются hello клиента библиотеки broker hello подключения к базе данных для приложения. Это позволяет hello сегментов карты функциональность tooautomatically kill подключения к базе данных при операции управления сегментов может повлиять на hello подсегмента, hello подключение будет создано для. Этот подход должен toointegrate с некоторыми EF функциональных возможностей, таких как создание новых соединений с существующие один toocheck наличие базы данных. Как правило, наши наблюдения был что стандартные конструкторы DbContext hello работать только надежно подключений закрытых базы данных, которые можно безопасно клонировать EF работ. Принцип разработки Hello эластичной базы данных вместо является tooonly broker открыт соединений. Может показаться, что закрытие подключения через посредника клиентской библиотекой hello перед передачей его по toohello EF DbContext можно решить эту проблему. Тем не менее, закрыв соединения hello и полагаться на toore открытия EF, один foregoes hello проверки и согласованность проверок библиотекой hello. функциональные возможности миграции Hello в EF, однако использует базовой схемы базы данных, в результате которого является прозрачным toohello приложение toomanage hello эти подключения система. В идеальном случае бы как tooretain и объединить все эти возможности из клиентской библиотеке эластичной базы данных hello и EF hello того же приложения. Hello следующем разделе описываются эти свойства и требования к более подробно. 

## <a name="requirements"></a>Требования
При работе с клиентской библиотеке эластичной базы данных hello и API платформы Entity Framework, мы хотим tooretain hello следующие свойства: 

* **Масштабирование**: tooadd или удаление баз данных с уровня данных hello сегментированных приложения hello согласно требованиям к емкости hello приложения hello. Это значит, контроль над hello hello Создание и удаление баз данных и с помощью hello эластичной базы данных сегментов карты диспетчера API-интерфейсы toomanage баз данных и сопоставления подсегментов. 
* **Согласованность**: hello приложение использует сегментирования и использует hello зависимые функции маршрутизации данных hello клиентской библиотеки. повреждение tooavoid или результаты запроса неправильный, подключения через посредника, hello диспетчера карты сегментов. Это также позволяет использовать проверки и поддерживать согласованность данных.
* **Code First**: tooretain удобства hello первого подхода EF элемента кода. Code First классов в приложении hello сопоставления прозрачно toohello базовые структуры базы данных. код приложения Hello взаимодействует с DbSets, маску основные аспекты, участвующих в hello базовый обработку базы данных.
* **Схема.**Entity Framework берет на себя создание начальной схемы базы данных и последующего развития схемы в ходе миграций. Сохраняя эти возможности, адаптации приложения можно легко, как приветствия развития данных. 

Hello приводимых предписывает как toosatisfy эти требования для первого кода приложений, с помощью средств эластичной базы данных. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>Маршрутизация на основе данных с помощью EF DbContext
Подключения к базам данных в платформе Entity Framework обычно управляются через подклассы **DbContext**. Создайте эти подклассы, сделав их производными от **DbContext**. Это поле определяется вашей **DbSets** , которые реализуют hello резервной базы данных коллекции объектов среда CLR для вашего приложения. В контексте hello управляемой данными маршрутизацией можно определить несколько полезных свойств, которые не обязательно будет верным для других сценариев EF кода первого приложения: 

* Hello базы данных уже существует и был зарегистрирован в карте сегментов hello эластичной базы данных. 
* Hello схемы приложения hello уже развернутой toohello базы данных (как описано ниже). 
* База данных маршрутизации подключений toohello зависимости от данных посредника по карте сегментов hello. 

toointegrate **DbContexts** с маршрутизации в зависимости от данных для масштабного развертывания:

1. Создать соединения физической базы данных через клиентские интерфейсы hello эластичной базы данных диспетчера карты сегментов hello, 
2. Перенос hello соединения с hello **DbContext** подкласс
3. Передайте hello подключения в hello **DbContext** базовые классы tooensure вся обработка hello hello EF стороны также происходит. 

Этот подход показан в следующем примере кода Hello. (Этот код также является в hello, сопровождающие проекта Visual Studio)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>Основные положения
* Новый конструктор заменяет конструктор по умолчанию hello в подкласс DbContext hello 
* новый конструктор Hello принимает hello аргументы, которые требуются для управляемой данными маршрутизацией по клиентской библиотеке эластичной базы данных:
  
  * tooaccess карты сегментов Hello hello интерфейсов маршрутизации в зависимости от данных,
  * Подсегмент hello tooidentify ключа сегментирования Hello,
  * Строка подключения с учетными данными hello для hello зависимости от данных маршрутизации соединений toohello сегментов. 
* конструктор базового класса toohello вызов Hello учитывает обход статический метод, который выполняет все действия hello необходимые для маршрутизации в зависимости от данных. 
  
  * Он использует вызов OpenConnectionForKey hello интерфейсов клиента hello эластичной базы данных на tooestablish карты сегментов hello открытое соединение.
  * карта сегментов Hello создает hello открытое соединение toohello сегмент, содержащий hello Подсегмент для заданного ключа сегментирования hello.
  * Это открытое подключение передается в конструктор базового класса назад toohello tooindicate DbContext, что данное подключение относится toobe используемые EF фиксированного EF автоматически создать новое соединение. Это подключение hello способом был помечен клиентом hello эластичной базы данных API, чтобы он может гарантировать согласованность в операции управления сопоставлениями сегментов.

Используйте новый конструктор hello для подкласс DbContext вместо конструктор по умолчанию hello в коде. Пример: 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

новый конструктор Hello открывает hello подключения toohello сегментов hello для сохранения данных Подсегмент hello, определяется значением hello объекта **tenantid1**. Здравствуйте, код в hello **с помощью** блока остается неизменным tooaccess hello **DbSet** для блогов, с помощью EF на hello сегментов для **tenantid1**. Это изменяет семантику для кода hello в hello, с помощью блока, теперь являются всех операций базы данных, областью действия один сегмент toohello где **tenantid1** сохраняется. Например, запрос LINQ через блоги hello **DbSet** будут возвращать только блоги, хранящиеся на текущий сегмент hello, но не те, хранящиеся на другие сегменты hello.  

#### <a name="transient-faults-handling"></a>Обработка временных сбоев
Hello шаблонов и практик Майкрософт team опубликованных hello [hello временных Fault Handling Application Block](https://msdn.microsoft.com/library/dn440719.aspx). Библиотека Hello используется с клиентской библиотеки гибкого масштабирования в сочетании с EF. Тем не менее убедитесь, что все временные исключения возвращает tooa месте, где можно гарантировать, что новый конструктор hello используется после временных сбоев, таким образом, все новые попытки подключения выполнялась с использованием hello конструкторов, которые мы слегка изменить. В противном случае toohello подключение, подключение hello существует, без подтверждения, а не гарантируется, что сегмент поддерживаются как карта сегментов toohello происходят изменения. 

Hello следующем образце кода показано, как политику повтора SQL можно использовать вокруг hello новый **DbContext** подкласс конструкторы: 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** в hello приведенный выше код определяется как **SqlDatabaseTransientErrorDetectionStrategy** с числом повторов, равным 10 и 5 секунд время ожидания между повторными попытками. Этот подход является аналогичные toohello руководство по EF и транзакции, инициированной пользователем (в разделе [ограничения, связанные с повторной попыткой выполнения стратегии (начиная EF6)](http://msdn.microsoft.com/data/dn307226). Оба ситуациях требуется hello области toowhich hello Временное исключение возвращает управляет этой программы приложения hello: tooeither повторно открыть транзакции hello, или (как показано) повторно создать контекст hello из конструктора правильную hello, что использует hello эластичной базы данных Клиентская библиотека.

Hello toocontrol необходимость, где временные исключения занять обратно в области не позволяет использовать hello встроенных hello **использовать SqlAzureExecutionStrategy** , который поставляется вместе с EF. **Использовать SqlAzureExecutionStrategy** будут повторно открыть соединение, но не использовать **OpenConnectionForKey** и поэтому не все проверочные hello, которое выполняется как часть hello **OpenConnectionForKey** вызова. Вместо этого образца кода hello использует встроенные hello **DefaultExecutionStrategy** , также имеет EF. В отличие от слишком**использовать SqlAzureExecutionStrategy**, оно правильно работает в сочетании с hello политику повтора из обработка временных сбоев. политика выполнения Hello задана в hello **ElasticScaleDbConfiguration** класса. Обратите внимание, что мы решили не toouse **DefaultSqlExecutionStrategy** , так как он предлагает toouse **использовать SqlAzureExecutionStrategy** при временных исключений - которого может привести toowrong поведение, как описано. Дополнительные сведения о различных политик hello и EF см. в разделе [устойчивость подключения в EF](http://msdn.microsoft.com/data/dn456835.aspx).     

#### <a name="constructor-rewrites"></a>Переделка конструктора
Hello Вышеприведенные примеры кода показывают по умолчанию hello конструктор загрузочную запись, необходимый для приложения в порядке toouse данных зависимых маршрутизации с hello Entity Framework. в следующей таблице Hello обобщает конструкторы tooother этот подход. 

| Текущий конструктор | Переделанный конструктор для данных | Базовый конструктор | Примечания |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |Hello подключение должно toobe функция карты сегментов hello и маршрутизации ключ hello зависимости от данных. Требуется создание автоматическое подключение с отрицательным tooby EF и вместо этого используйте hello сегментов карты toobroker hello соединения. |
| MyContext(string) |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |Hello подключения — это функция карты сегментов hello и hello зависимости от данных маршрутизации ключа. Строка имени или подключения базы данных не будет работать как только они обойти проверку по карте сегментов hello. |
| MyContext(DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |Создать соединение Hello будет получить заданный ключ сегментирования карты и сегментирования с hello модели, предоставляемой hello. Hello скомпилированных модели будут передаваться в базовый c'tor toohello. |
| MyContext(DbConnection, bool) |ElasticScaleContext(ShardMap, TKey, bool) |DbContext(DbConnection, bool) |Hello подключение должно выводиться из карты сегментов hello и ключ hello toobe. Его нельзя указать в качестве ввода (если входа была использована карта сегментов hello и ключ hello). будет передаваться Hello логическое значение. |
| MyContext(string, DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |Hello подключение должно выводиться из карты сегментов hello и ключ hello toobe. Его нельзя указать в качестве ввода (если эти входные данные использовался карта сегментов hello и ключ hello). Hello скомпилированных модели будут передаваться в. |
| MyContext(ObjectContext, bool) |ElasticScaleContext(ShardMap, TKey, ObjectContext, bool) |DbContext(ObjectContext, bool) |новый конструктор Hello должен tooensure, перенаправлен tooa соединения, управляемого компонентом гибкого масштабирования any connection в hello ObjectContext, переданных в качестве входных данных. Подробный рассказ о ObjectContexts выходит за рамки данного документа hello. |
| MyContext(DbConnection, DbCompiledModel,bool) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel, bool) |DbContext(DbConnection, DbCompiledModel, bool); |Hello подключение должно выводиться из карты сегментов hello и ключ hello toobe. подключение Hello нельзя указать в качестве ввода (если входа была использована карта сегментов hello и ключ hello). Модель и логическое значение, передаются toohello конструктор базового класса. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>Развертывание схемы сегментирования через миграции EF
Управление схемой автоматического — удобный метод, предоставляемые hello Entity Framework. В контексте hello приложений с помощью средств эластичной базы данных мы хотим tooretain этой возможности tooautomatically подготовки hello схемы toonewly создания сегментов при добавлении toohello сегментированных приложений баз данных. Hello основном используются tooincrease емкости на уровне данных hello сегментированных приложений с помощью EF. Полагаться на возможности EF элемента схемы управления уменьшает трудозатраты администрирования hello базы данных с сегментированных приложения, созданного на EF. 

Развертывание схемы с помощью миграций EF лучше всего работает для **неоткрытых подключений**. В отличие от toohello сценарий не управляемой данными маршрутизацией, основанный на Привет открыть соединение, предоставляемое API hello эластичной базы данных клиента. Другое отличие состоит в требовании hello: при желательно tooensure согласованности для всех зависящих от данных маршрутизации tooprotect подключений для обработки параллельных сегментов карты, он не важен с новой базой данных tooa развертывания Исходная схема где имеется еще не был зарегистрирован в карте сегментов hello и еще не был выделен toohold подсегментов. Мы рассчитывать на подключения обычной базой данных для этого сценарии маршрутизации в противоположность toodata зависимости.  

Это порождает tooan подход, где развертывания схемы с помощью EF миграции тесно связана с регистрации hello hello новой базы данных как сегментов в карте сегментов приложения hello. Это зависит от hello следующие предварительные требования: 

* Hello базы данных уже был создан. 
* Hello база данных пуста - в ней нет пользовательской схемы и отсутствуют данные пользователя.
* Hello базы данных еще не доступен через клиент hello эластичной базы данных API-интерфейсы для маршрутизации в зависимости от данных. 

Эти условия можно создать обычную без открытого **SqlConnection** tookick off EF миграции для развертывания схемы. Этот подход показан следующий образец кода Hello. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


В этом примере показан метод hello **RegisterNewShard** hello, регистров сегментов в карте сегментов hello, развертывает hello схемы с использованием EF миграции и сохраняет сопоставление сегментом toohello ключа сегментирования. Он основывается на конструктор hello **DbContext** подкласс (**ElasticScaleContext** в образце hello), который принимает строку подключения SQL в качестве входных данных. Код Hello этот конструктор является очевидно, как следующий пример показывает hello: 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Вероятно, один использован hello версия конструктора hello, унаследованные от базового класса hello. Однако tooensure потребностей кода hello, hello инициализатор по умолчанию для EF используется при подключении. Поэтому hello короткий перенаправление в статический метод hello перед вызовом конструктора базового класса hello со строкой подключения hello. Обратите внимание, что регистрация hello сегментов следует выполнять в другое приложение для домена или процесс tooensure, параметры hello инициализатор для EF не конфликтуют. 

## <a name="limitations"></a>Ограничения
Hello подходов, описанных в этом документе включают несколько ограничений: 

* EF приложений, использующих **LocalDb** сначала необходимо регулярное SQL Server базы данных toomigrate tooa перед использованием клиентской библиотеке эластичной базы данных. Горизонтальное масштабирование приложения через сегментирование с помощью эластичного масштабирования невозможно с **LocalDb**. Обратите внимание, что во время разработки **LocalDb**по-прежнему можно использовать. 
* Любое приложение toohello изменения, подразумевают изменения схемы базы данных должны toogo через миграций EF на всех сегментах. Hello образцы кода для этого документа не демонстрирует способ toodo это. Рассмотрите возможность использования Update-Database с параметром ConnectionString tooiterate по всем сегментам; или извлечения hello T-SQL сценарий hello ожидает обновления базы данных с помощью переноса hello - параметр «скрипт» и применить сегменты tooyour сценария hello T-SQL.  
* Получает запрос, предполагается, что все его обработку базы данных содержатся в одном сегменте, идентифицируемый hello сегментирования ключ, указанный в запросе hello. Однако это предположение не всегда является верным. Например, когда это не возможные toomake ключ сегментирования доступны. tooaddress hello, клиентская библиотека предоставляет hello **MultiShardQuery** класс, который реализует абстракцию подключения для выполнения запросов через несколько сегментов. Изучение toouse hello **MultiShardQuery** в сочетании с EF выходит за рамки данного документа hello

## <a name="conclusion"></a>Заключение
Через hello шаги, описанные в этом документе, EF приложения могут использовать возможности hello эластичной базы данных клиентской библиотеки для данных зависимых маршрутизации командой рефакторинга конструкторы hello **DbContext** подклассов, используемых в hello EF приложение. Необходимые изменения hello этого ограничения toothose мест, где **DbContext** классы уже существуют. Кроме того EF приложения сохраняют toobenefit из схемы автоматического развертывания, объединяя hello действия, которые вызывают hello необходимые EF миграции с регистрацией hello новых сегментов и сопоставления в карте сегментов hello. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
