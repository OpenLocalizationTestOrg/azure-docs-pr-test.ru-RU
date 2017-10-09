---
title: "службы Service Fabric aaaPartitioning | Документы Microsoft"
description: "Описывает способ служб с отслеживанием состояния toopartition Service Fabric. Секций обеспечивает хранение данных на локальных компьютерах hello, данных и вычислений может масштабироваться друг с другом."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>Секционирование служб Reliable Services в Service Fabric
Эта статья содержит введение toohello основные понятия секционирования надежные службы Azure Service Fabric. Hello исходного кода, использованной в статье hello доступна также на [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="partitioning"></a>Секционирование
Секционирование не является уникальным tooService структуры. По сути, это основной способ создания масштабируемых служб. В более широком смысле мы подумать о секционировании как понятие деления состояние (данные) и вычислений в небольших доступны единицы tooimprove масштабируемость и производительность. Распространенный пример секционирования — это [секционирование данных][wikipartition], которое еще называют сегментированием.

### <a name="partition-service-fabric-stateless-services"></a>Секционирование служб без отслеживания состояния в Service Fabric
В случае со службами без отслеживания состояния секцию можно описать как логическую единицу, содержащую один или несколько экземпляров службы. На рис. 1 показана служба без отслеживания состояния с пятью экземплярами, распределенными в кластере и объединенными в одну секцию.

![Служба без отслеживания состояния](./media/service-fabric-concepts-partitioning/statelessinstances.png)

Есть два типа решений служб без отслеживания состояния. Hello первого одно — это служба, которая сохраняет состояние извне, например в базе данных Azure SQL (например, веб-сайт, сохраняет данные и сведения о сеансе hello). Hello второй раз — только для вычисления служб (например, создание эскизов калькулятора или изображение), управление которыми невозможно любое постоянное состояние.

Секционирование служб без отслеживания состояния выполняется очень редко. запрашивает Hello только время tooconsider несколько секций для экземпляров службы без отслеживания состояния — при необходимости toomeet специального маршрута.

Примером может быть случай, когда пользователи с идентификаторами из определенного диапазона должны обслуживаться только определенным экземпляром службы. Если выполнено секционирование службы без отслеживания состояния еще один пример — у вас действительно секционированной базы данных (например сегментированной базы данных SQL), если необходимо toocontrol экземпляра данной службы следует записать toohello сегментов базы данных — или выполнять другую работу подготовки в Hello службы без отслеживания состояния, которая требует hello же сведения о секционировании, так как используется в серверном hello. Подобные сценарии также можно решить другими способами, не требующими секционирования службы.

Остаток Hello в данном пошаговом руководстве основное внимание уделяется служб с отслеживанием состояния.

### <a name="partition-service-fabric-stateful-services"></a>Секционирование служб с отслеживанием состояния в Service Fabric
Service Fabric позволяет легко toodevelop масштабируемых служб с отслеживанием состояния, предлагая первого класса способом toopartition состояние (данных). По существу, можно считать о разделе службы с отслеживанием состояния единица масштабирования, которую высокую степень доступности посредством [реплик](service-fabric-availability-services.md) , распространяются и равномерно распределяется по hello узлов в кластере.

Секционирование в контексте служб с отслеживанием состояния Service Fabric hello ссылается toohello процесс определения того, что раздел конкретной службы отвечает за часть полного состояния службы hello hello. (Как уже говорилось ранее, секция представляет собой набор [реплик](service-fabric-availability-services.md).) Преимущество Service Fabric — что он помещает hello секций на разных узлах. Это позволяет им ограничение ресурсов toogrow tooa узла. По мере роста данных hello увеличиваться секций и Service Fabric балансировку секций между узлами. Это гарантирует, что hello продолжение эффективного использования ресурсов оборудования.

toogive вы пример, предположим, вы начинаются с 5 узлами кластера и службы, настроенные toohave 10 секций и как целевой объект три реплики. В этом случае Service Fabric бы балансировки и распределить hello реплик по hello кластера — и вы появятся два основных [реплик](service-fabric-availability-services.md) на каждом узле.
Если требуется tooscale out too10 hello кластеру, Service Fabric бы балансирования hello первичный [реплик](service-fabric-availability-services.md) на всех узлах 10. Аналогичным образом Если увеличили задней too5 узлов Service Fabric бы балансирования все реплики hello по узлам hello 5.  

Рис. 2 показана hello распределение 10 секций до и после масштабирования hello кластера.

![Служба с отслеживанием состояния](./media/service-fabric-concepts-partitioning/partitions.png)

В результате масштабирования hello достигается запросы клиентов распределяются на нескольких компьютерах, поэтому повысить общую производительность приложения hello и конфликты доступа toochunks данных сокращается.

## <a name="plan-for-partitioning"></a>Планирование секционирования
Перед реализацией службы, рекомендуется всегда hello, требуется tooscale out стратегию секционирования. Можно различными способами, но все они сосредоточиться на какие hello приложению tooachieve. Для контекста hello в этой статье давайте рассмотрим некоторые hello более важные аспекты.

Рекомендуется toothink о структуре hello hello состояния, которые toobe секционирование, в качестве первого шага hello.

Давайте рассмотрим простой пример. Если toobuild службы для countywide опроса, можно создать новый раздел для каждого города в округе hello. Затем можно хранить в городе hello в секции hello, соответствующий Город toothat hello голосов для каждого человека. Рис. 3 показана набор пользователей, а также hello Город, в которой они находятся.

![Простой раздел](./media/service-fabric-concepts-partitioning/cities.png)

Как заполнение hello городов сильно варьируется, может оказаться некоторые разделы, которые содержат большой объем данных (например, Seattle) и другие разделы с состоянием очень мало (например Кирклэнд). Так что такое последствия hello секций с неравномерной объемов состояние?

Если вы думаете о примере hello еще раз, можно легко увидеть, получение hello секции, в которой размещается hello голосов для Сиэтла больше трафика, чем Кирклэнд hello один. По умолчанию Service Fabric гарантирует, что имеется о hello одинаковое число первичных и вторичных реплик на каждом узле. Поэтому у вас могут получиться узлы, реплики на которых обслуживают разный объем трафика. Предпочтительно потребовалось бы tooavoid горячие и холодные перегруженные участки, как в данном в кластере.

Чтобы tooavoid это, необходимо сделать две вещи, с секционирования точки зрения:

* Попробуйте toopartition hello состояния, чтобы равномерно распределяется все секции.
* Загрузка отчета из каждой из реплик hello hello службы. (Чтобы узнать, как это сделать, прочитайте эту статью о [метриках и загрузке](service-fabric-cluster-resource-manager-metrics.md).) Service Fabric предоставляет hello возможность tooreport нагрузки на службы, такие как объем памяти или число записей. На основании hello показатели, Service Fabric обнаруживает, что некоторые разделы обслуживающей более высокие нагрузки, чем другие и балансировку кластера hello скользящего реплик toomore подходящий узлами, чтобы в целом ни один узел не перегружен.

В некоторых случаях невозможно заранее определить, какой объем данных будет в той или иной секции. Поэтому общая рекомендация toodo оба--во-первых, принимая стратегии секционирования, распространяет hello данных равномерно по hello секции во-вторых, путем загрузки отчетов.  Первый метод Hello предотвращает ситуациях, описанных в hello голосования примере хотя hello второй помогает сглаживают временные разницы в доступа или нагрузки со временем.

Другим аспектом планирования раздела является toochoose hello неверное количество секций toobegin с.
В Service Fabric нет никаких ограничений относительно использования большего количества секций, чем требуется для тех или иных целей.
Фактически при условии, что hello максимального количества секций — это допустимый подход.

Большее количество секций, чем выбрано изначально, может понадобиться в редких случаях. Число секций hello нельзя изменить после проведения hello, потребовалось бы tooapply некоторые подходы дополнительные секции, например для создания нового экземпляра службы из hello же тип службы. Необходимо также tooimplement некоторые клиентские логику, которая направляет hello запрашивает экземпляр toohello правильную службу, на основе набора знаний стороны клиента, необходимо обеспечить код клиента.

Другой аспект для секционирования планирования — hello доступный компьютер ресурсы. По мере toobe доступ и хранится состояние hello будут привязанного toofollow:

* пропускная способность сети;
* память системы;
* место на диске.

Что произойдет, если возникнут ограничения ресурсов в кластере выполнение? Hello ответ заключается в том, что можно просто масштабировать hello tooaccommodate hello новые требования к кластеру.

[руководство по планированию емкости Hello](service-fabric-capacity-planning.md) предлагает руководство toodetermine сколько узлов кластера требуется.

## <a name="get-started-with-partitioning"></a>Начало секционирования
В этом разделе описывает, как tooget работу с секционирования службы.

В Service Fabric можно выбрать одну из трех возможных схем секционирования.

* Секционирование по диапазонам значений (также известное как UniformInt64Partition).
* Секционирование по именам. Как правило, данные приложений, которые используют эту модель, можно поместить в контейнер в рамках ограниченного набора данных. Вот некоторые наиболее распространенные примеры полей данных, которые используются в качестве ключей для секционирования по именам: регионы, почтовые индексы, группы клиентов и др.
* Одноэлементное секционирование. Одноэлементный секции обычно используются при hello служба не требует какой-либо дополнительных маршрутизации. Например, службы без отслеживания состояния используют эту схему секционирования по умолчанию.

Схемы секционирования по именам и одноэлементного секционирования являются особыми формами секционирования по диапазонам. По умолчанию hello шаблонов Visual Studio для использования Service Fabric циклы секционирования, как он hello наиболее распространенным и полезным один. Hello оставшейся части этой статьи посвящена hello срез схему секционирования.

### <a name="ranged-partitioning-scheme"></a>Схема секционирования по диапазонам
Это используется toospecify целое диапазона (определяемая нижний ключ и верхний ключ) и количество секций (n). Он создает n секций, каждый из которых отвечает для стадии hello неперекрывающиеся секции диапазона ключей в целом. Например, схема секционирования по диапазонам, в которой нижний ключ равен 0, верхний ключ равен 99, а количество секций равно 4, создаст четыре секции, как показано ниже.

![Секционирование по диапазону](./media/service-fabric-concepts-partitioning/range-partitioning.png)

Наиболее распространенный подход заключается toocreate хэша, основанная на уникальный ключ в наборе данных hello. Вот некоторые наиболее распространенные примеры ключей: код идентификации транспортного средства (VIN), идентификатор сотрудника, уникальная строка и пр. Используя этот уникальный ключ, будет затем создать хэш-код, диапазона ключей hello остатка от деления, toouse как ключ. Можно указать hello верхней и нижней границ допустимого диапазона ключей hello.

### <a name="select-a-hash-algorithm"></a>Выбор хэш-алгоритма
Важной частью хэширования является выбор хэш-алгоритма. Следует учитывать, является ли цель hello toogroup аналогичные ключи рядом друг с другом (конфиденциальные хэширования местоположению)--или если действия должен быть предоставлен широко во всех разделах (распространения хэширования), который чаще.

Это легко toocompute, он имеет несколько конфликтов и равномерно распределяет hello ключи приведены характеристики Hello распространения хорошей хэш-алгоритма. Хорошим примером алгоритма хэширования эффективный — hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) хэш-алгоритм.

Hello является ценным ресурсом для варианты алгоритм хэширования общие кода [страницы Википедии на хэш-функции](http://en.wikipedia.org/wiki/Hash_function).

## <a name="build-a-stateful-service-with-multiple-partitions"></a>Создание службы с отслеживанием состояния с несколькими секциями
Далее вы создадите свою первую службу Reliable Services с отслеживанием состояния с несколькими разделами. В этом примере будет создать все фамилии, начинающиеся с буквы в hello hello очень простое приложение место toostore одной секции.

Прежде чем писать программный код необходим toothink о секциях hello и ключи разделов. Добавить 26 разделы (по одному для каждой буквы в алфавите hello), но что о hello низким и высоким ключей?
Как буквально, мы хотим toohave один раздел на букву, мы используем 0 как нижний ключ hello и 25 как hello верхний ключ, как каждая буква представляет свой собственный ключ.

> [!NOTE]
> Это упрощенное сценарий, как на самом деле бы неравномерное распределение hello. Последний имена, начинающиеся с буквы hello «S» или «M» чаще, чем hello из них, начиная с «X» или «Y».
> 
> 

1. Выберите **Visual Studio** > **Файл** > **Создать** > **Проект**.
2. В hello **новый проект** диалогового окна выберите приложение hello Service Fabric.
3. Вызов hello проекта «AlphabetPartitions».
4. В hello **создать службу** диалогового окна выберите **с отслеживанием состояния** службы и назовите его «Alphabet.Processing», как показано в приведенном ниже рисунке hello.
       ![Диалоговое окно "Новая служба" в Visual Studio][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Задайте hello количество секций. Привет открыть файл Applicationmanifest.xml находится в hello ApplicationPackageRoot папки AlphabetPartitions hello проекте и обновите параметр hello too26 Processing_PartitionCount, как показано ниже.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    Необходимо также tooupdate hello LowKey и HighKey свойств элемента StatefulService hello в hello ApplicationManifest.xml, как показано ниже.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Для toobe hello службы доступны открывая конечную точку на порте, добавив hello. элемент конечной точки ServiceManifest.xml (находится в папке PackageRoot hello) для hello Alphabet.Processing службы, как показано ниже:
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    Теперь служба hello является настроенным toolisten tooan внутренней конечной точки с 26 секций.
7. Далее необходимо toooverride hello `CreateServiceReplicaListeners()` метод класса обработки hello.
   
   > [!NOTE]
   > В этом примере предполагается, что вы используете простой прослушиватель HttpCommunicationListener. Дополнительные сведения о связи надежной службы см. в разделе [модель взаимодействия hello надежной службы](service-fabric-reliable-services-communication.md).
   > 
   > 
8. Рекомендуемый шаблон для hello URL-адрес, который прослушивает реплики — hello, следующий формат: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.
    Поэтому вы хотите tooconfigure ваш прослушиватель toolisten связи на hello нужных конечных точек и с этим шаблоном.
   
    Несколько реплик эта служба может размещаться на hello одном компьютере, поэтому этот адрес должен toobe уникальный toohello реплики. Именно поэтому идентификатор секции + идентификатор реплики находятся в URL-адрес hello. HttpListener может прослушивать несколько адресов на приветствия же порт, при условии, что префикс URL-адреса hello является уникальным.
   
    Здравствуйте, есть ли дополнительные GUID для сложных случаях, где также прослушивания вторичные реплики для запросов только для чтения. Это случай hello, нужно убедиться, что новый уникальный адрес используется во время перехода с основной toosecondary tooforce клиентов toore resolve hello адрес toomake. «+» используется как адрес hello, чтобы hello реплика прослушивает все доступные узлы в (IP, FQDM, localhost, т. д.) hello кода ниже показан пример.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    Также стоит отметить, что hello опубликованные URL-адрес имеет некоторые отличия от hello прослушивания префикс URL-адреса.
    Hello прослушивания задан URL-адрес tooHttpListener. Здравствуйте, hello URL-адрес, опубликованный toohello служба именования Service Fabric, которая используется для обнаружения службы является URL-адрес публикации. Клиенты будут запрашивать этот адрес с помощью службы обнаружения. адрес Hello, клиенты получают потребностей toohave hello фактических IP-адрес или полное доменное имя узла hello в tooconnect порядке. Поэтому необходимо tooreplace '+' с hello узла в IP-адрес или полное доменное имя как показано выше.
9. Последний шаг Hello — hello tooadd обработки логики toohello службы, как показано ниже.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`операции чтения hello значения секции hello toocall параметр, используемый строку hello запросов и вызовов `AddUserAsync` надежного словарь lastname hello toohello tooadd `dictionary`.
10. Давайте добавим toosee проекта службы без отслеживания состояния toohello как можно вызвать заданной секции.
    
    Эта служба служит в качестве простого веб-интерфейса, который принимает lastname hello как параметр строки запроса, определяет ключ раздела hello и отправляет его службе Alphabet.Processing toohello для обработки.
11. В hello **создать службу** диалогового окна выберите **Stateless** службы и назовите его «Alphabet.Web», как показано ниже.
    
    ![Снимок экрана, на котором изображена служба без отслеживания состояния](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. Обновите сведения о конечной точке hello в hello ServiceManifest.xml tooopen службы Alphabet.WebApi hello порт, как показано ниже.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. Необходимо tooreturn коллекцию ServiceInstanceListeners в классе hello Web. Опять же вы можете tooimplement простой HttpCommunicationListener.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. Теперь вам требуется логика обработки tooimplement hello. Здравствуйте, вызовы HttpCommunicationListener `ProcessInputRequest` при поступлении запроса. Поэтому добавим и добавьте приведенный ниже код hello.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    Давайте разберемся в процессе, шаг за шагом. Код Hello считывает hello первую букву из параметра строки запроса hello `lastname` в тип char. Затем определяет hello ключ раздела для эту букву путем вычитания hello шестнадцатеричное значение `A` из hello шестнадцатеричное значение hello фамилий первая буква.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    Напоминаем, что в этом примере мы используем 26 секций с одним ключом на секцию.
    Затем мы получим hello служебного раздела `partition` для этого ключа с помощью hello `ResolveAsync` метод hello `servicePartitionResolver` объекта. `servicePartitionResolver` определяется так:
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    Hello `ResolveAsync` URI службы hello метод принимает ключ раздела hello и токен отмены в качестве параметров. Здравствуйте URI службы для службы обработки hello `fabric:/AlphabetPartitions/Processing`. Далее мы получаем конечной точки hello hello секции.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    Наконец мы построения URL-адрес конечной точки hello плюс строка запроса hello и вызовите hello службы обработки.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    После завершения обработки hello мы вывода hello обратно.
15. Последний шаг Hello — служба tootest hello. Visual Studio использует параметры приложения для локального и облачного развертываний. службы hello tootest с 26 секций на локальном компьютере, необходимо tooupdate hello `Local.xml` файл в папке ApplicationParameters hello hello AlphabetPartitions проекта, как показано ниже:
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. После завершения развертывания можно проверить службу hello и всех своих секций в обозреватель Service Fabric hello.
    
    ![Снимок экрана, на котором изображен обозреватель Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. В браузере можно проверить секционирование логику, введя hello `http://localhost:8081/?lastname=somename`. Вы увидите, что каждой фамилии, который начинается с такой же буквой, хранящихся в hello hello одной секции.
    
    ![Снимок экрана, на котором изображен браузер](./media/service-fabric-concepts-partitioning/samplerunning.png)

Hello весь исходный код образца hello доступен на [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="next-steps"></a>Дальнейшие действия
Сведения о Service Fabric см. ниже hello:

* [Доступность служб структуры служб](service-fabric-availability-services.md)
* [Масштабируемость служб структуры служб](service-fabric-concepts-scalability.md)
* [Планирование емкости для приложений Service Fabric](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png