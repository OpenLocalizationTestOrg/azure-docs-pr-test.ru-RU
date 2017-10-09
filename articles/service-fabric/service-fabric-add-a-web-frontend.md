---
title: "веб-интерфейса для приложения Azure Service Fabric с помощью ASP.NET Core aaaCreate | Документы Microsoft"
description: "Предоставлять веб-приложения toohello Service Fabric с помощью проекта ASP.NET Core и связи между службами через службу удаленного взаимодействия."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>Создание внешнего интерфейса веб-службы для приложения с помощью ASP.NET Core
По умолчанию службы Azure Service Fabric не предоставляют toohello общедоступный веб-сайт. tooexpose клиентов tooHTTP функциональные возможности приложения, у вас есть toocreate веб-узел проекта tooact в качестве точки входа, а затем взаимодействовать с ней tooyour отдельных служб.

В этом учебнике мы взять с момента остановки в hello [создание первого приложения в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) учебника и добавить в веб-службу ASP.NET Core перед службы с отслеживанием состояния счетчика hello. Выполните соответствующие указания в этом руководстве, если вы этого еще не сделали.

## <a name="set-up-your-environment-for-aspnet-core"></a>Настройте среду для ASP.NET Core

Требуется Visual Studio 2017 г toofollow вместе с учебником. Подойдет любой выпуск. 

 - Установите [Visual Studio 2017](https://www.visualstudio.com/).

приложения ASP.NET Core Service Fabric toodevelop, должно быть hello, следуя рабочей нагрузки:
 - **разработка Azure** (в разделе *Web & Cloud* (Сеть и облако));
 - **ASP.NET и веб-разработка** (в разделе *Web & Cloud* (Сеть и облако));
 - **кроссплатформенная разработка .NET Core** (в разделе *Other Toolsets* (Другие наборы средств)).

>[!Note] 
>Hello .NET основные инструменты для Visual Studio 2015 больше не обновляются, но если вы все еще используете Visual Studio 2015, вам нужно toohave [.NET Core VS 2015 средства предварительного просмотра 2](https://www.microsoft.com/net/download/core) установлен.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>Добавление приложения ASP.NET Core service tooyour
ASP.NET Core — это платформа разработки упрощенных кросс платформенных веб-, можно использовать toocreate современного пользовательского веб-интерфейса и веб-API. 

Давайте добавим существующее приложение tooour проекта веб-API ASP.NET.

1. В обозревателе решений щелкните правой кнопкой мыши **службы** в проект приложения hello и выберите **Добавить > Новая служба Service Fabric**.
   
    ![Добавление нового tooan существующего приложения службы][vs-add-new-service]
2. На hello **создать службу** выберите **ASP.NET Core** и присвойте ему имя.
   
    ![Выбор веб-службы ASP.NET в диалоговое окно создания службы hello][vs-new-service-dialog]

3. Следующая страница Hello предоставляет набор ASP.NET Core шаблоны проектов. Обратите внимание, что они являются hello же варианты, которые появляются при создании проекта ASP.NET Core вне приложения Service Fabric, с помощью небольшого количества tooregister дополнительного кода hello службы среды выполнения Service Fabric hello. В этом руководстве мы будем использовать **веб-API**. Тем не менее, можно применить hello же понятия toobuilding полного веб-приложения.
   
    ![Выбор типа проекта ASP.NET][vs-new-aspnet-project-dialog]
   
    После создания проекта веб-API в вашем приложении будут две службы. Как вы по-прежнему toobuild приложения, можно добавить дополнительные службы в точности hello таким же образом. Каждая из этих служб может быть отдельно обновлена, в том числе до определенной версии.

## <a name="run-hello-application"></a>Запустите приложение hello
Общее представление о том, что мы сделали, давайте tooget развертывания нового приложения hello и предоставляет поведение по умолчанию hello, hello шаблона веб-API ASP.NET Core рассмотреть take.

1. Нажмите клавишу F5 в Visual Studio приложение hello toodebug.
2. После завершения развертывания Visual Studio запускает браузер toohello корень hello службы веб-API ASP.NET. шаблон веб-API ASP.NET Core Hello не предоставляет поведение по умолчанию для корневого hello, должно появиться сообщение об ошибке 404 в браузере hello.
3. Добавить `/api/values` toohello расположение в браузере hello. При этом вызывается hello `Get` метод hello ValuesController в шаблоне hello веб-API. Он возвращает ответ по умолчанию hello, предоставляемого шаблоном hello — массив JSON, который содержит две строки:
   
    ![Значения по умолчанию, возвращаемые шаблоном веб-API ASP.NET Core][browser-aspnet-template-values]
   
    Hello конце учебника hello этой странице будет представлен hello самое последнее значение счетчика из нашей службы с отслеживанием состояния вместо hello строки по умолчанию.

## <a name="connect-hello-services"></a>Подключение служб hello
Service Fabric позволяет пользователям самим определять способ взаимодействия со службами Reliable Services. В одном приложении можно иметь службы, доступные по TCP, другие службы, которые доступны через HTTP REST API, и третьи службы, которые доступны через веб-сокеты. Основные сведения о доступные варианты hello, а также соотношение hello. в разделе [взаимодействия со службами](service-fabric-connect-and-communicate-with-services.md). В этом руководстве мы используем [удаленного взаимодействия службы структуры службы](service-fabric-reliable-services-communication-remoting.md), предоставленный в hello SDK.

В hello подход службы удаленного взаимодействия (основанный на удаленных вызовов процедур или RPC) определить интерфейс tooact как hello открытый контракт для службы hello. Затем использовать этот интерфейс toogenerate класс-посредник для взаимодействия со службой hello.

### <a name="create-hello-remoting-interface"></a>Создать интерфейс hello удаленного взаимодействия
Давайте начнем с создания интерфейса tooact hello как hello контракт между службой с отслеживанием состояния hello и другие службы, в этом вариантов hello веб-проекта ASP.NET Core. Этот интерфейс должен быть одинаков для всех служб, которые его используют toomake вызовы RPC, поэтому мы создадим в отдельном проекте библиотеки классов.

1. В обозревателе решений щелкните решение правой кнопкой мыши и выберите **В браузере добавьте к адресу путь** > **Новый проект**.

2. Выберите hello **Visual C#** запись в hello слева на панели навигации и выберите hello **библиотеки классов** шаблона. Убедитесь, эта версия .NET Framework hello задано слишком**4.5.2**.
   
    ![Создание проекта интерфейса для службы с отслеживанием состояния][vs-add-class-library-project]

3. Установка hello **Microsoft.ServiceFabric.Services.Remoting** пакет NuGet. Поиск **Microsoft.ServiceFabric.Services.Remoting** в hello NuGet пакета диспетчера и установить его для всех проектов в решении hello, использующих службы удаленного взаимодействия, включая:
   - проект библиотеки классов Hello, содержащий интерфейс службы hello
   - проект службы с отслеживанием состояния Hello
   - проект веб-службы ASP.NET Core Hello
   
    ![При добавлении пакета NuGet службы hello][vs-services-nuget-package]

4. В библиотеке классов hello, создать интерфейс с одним методом `GetCountAsync`, и расширения интерфейса hello из `Microsoft.ServiceFabric.Services.Remoting.IService`. Hello интерфейс удаленного доступа должен быть производным от этого интерфейса tooindicate, это интерфейс службы удаленного взаимодействия.
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>Реализуйте интерфейс hello в вашей службы с отслеживанием состояния
Теперь, когда мы определили интерфейс hello, нам нужно tooimplement в hello службы с отслеживанием состояния.

1. В службе с отслеживанием состояния добавьте ссылку toohello проект библиотеки классов, содержащий интерфейс hello.
   
    ![Добавление проекта библиотеки классов toohello ссылку в hello службы с отслеживанием состояния][vs-add-class-library-reference]
2. Найдите hello класс, наследующий от `StatefulService`, такие как `MyStatefulService`и расширить tooimplement hello `ICounter` интерфейса.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. Теперь реализуют hello единственный метод, который определен в hello `ICounter` интерфейса `GetCountAsync`.
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>Предоставлять службы с отслеживанием состояния hello, с помощью прослушиватель службы удаленного взаимодействия
С hello `ICounter` интерфейс реализован, hello последний шаг — tooopen hello службы удаленного взаимодействия коммуникационный канал. Для служб с отслеживанием состояния Service Fabric предоставляет переопределяемый метод `CreateServiceReplicaListeners`. В этом методе можно указать один или несколько прослушивателей связи, на основе типа hello взаимодействия, что требуется tooenable для службы.

> [!NOTE]
> вызывается Hello эквивалентный метод для открытия службы toostateless канала связи `CreateServiceInstanceListeners`.

В этом случае мы заменить существующий hello `CreateServiceReplicaListeners` метод и предоставить экземпляр `ServiceRemotingListener`, который создает конечную точку RPC может быть вызван из клиентов через `ServiceProxy`.  

Hello `CreateServiceRemotingListener` метод расширения в hello `IService` интерфейс позволяет tooeasily создания `ServiceRemotingListener` со всеми параметрами по умолчанию. toouse этот метод расширения, убедитесь в наличии hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` импортированные пространства имен. 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Использовать класс toointeract hello ServiceProxy со службой hello
Наши службы с отслеживанием состояния — это теперь готовы tooreceive трафик от других служб через RPC. Поэтому все, что остается состоит в добавлении toocommunicate кода hello с ним из веб-службы ASP.NET hello.

1. В проекте ASP.NET, добавить библиотека классов toohello ссылку, которая содержит hello `ICounter` интерфейса.

2. Ранее вы добавили hello **Microsoft.ServiceFabric.Services.Remoting** проекта ASP.NET toohello пакета NuGet. Этот пакет содержит hello `ServiceProxy` класс, который можно использовать toomake RPC вызывает toohello службы с отслеживанием состояния. Убедитесь, что при установке этого пакета NuGet в проект веб-службы ASP.NET Core hello.

4. В hello **контроллеров** папки, откройте hello `ValuesController` класса. Обратите внимание, что hello `Get` метод в данный момент просто возвращает массив жестко заданная строка «значение1» и «значение2»--соответствует мы видели ранее в браузере hello. Замените эту реализацию hello, следующий код:
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    Первая строка кода Hello является ключом hello один. toocreate hello ICounter прокси toohello службы с отслеживанием состояния, требуется tooprovide два блока данных: имя идентификатора и hello секции hello службы.
   
    Секционирования службы с отслеживанием состояния tooscale можно использовать, разбив их состояние в разные сегменты на основе ключа, определяющие, как код потребителя или почтовый индекс. В данном тривиальные службы с отслеживанием состояния hello имеет только одну секцию, поэтому hello ключ не имеет значения. Любую клавишу, указываемое приведет toohello одной секции. toolearn Дополнительные сведения о секционировании служб, в разделе [как toopartition надежного служб Service Fabric](service-fabric-concepts-partitioning.md).
   
    Имя службы Hello является URI структуры формы hello: /&lt;имя_приложения&gt;/&lt;service_name&gt;.
   
    С эти два блока данных Service Fabric можно однозначно определить hello компьютере, на который должны отправляться запросы. Hello `ServiceProxy` класс также легко обрабатывает hello случай, когда hello компьютер, на котором размещена раздела с отслеживанием состояния службы hello выходит из строя, и другой компьютер должен быть повышенным уровнем tootake его место. Эта абстракция делает написание hello toodeal кода клиента с другими службами, которые значительно проще.
   
    После получения hello прокси-сервера, достаточно вызвать hello `GetCountAsync` метод и возвращает ее результат.

5. Нажмите клавишу F5, снова toorun hello изменения приложения. Как и прежде, Visual Studio автоматически запускает корневой toohello браузера hello hello веб-проекта. Добавить путь «api или значения» hello, и вы увидите hello возвращается текущее значение счетчика.
   
    ![значение счетчика с отслеживанием состояния Hello, отображенные в браузере hello][browser-aspnet-counter-value]
   
    Обновите браузер hello периодически toosee hello счетчик значение обновления.

## <a name="kestrel-and-weblistener"></a>Kestrel и WebListener

Hello стандартного ASP.NET Core веб-сервера, известный как Kestrel, является [не поддерживается для обработки прямой Интернет-трафик](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel). В результате hello шаблон службы без отслеживания состояния ASP.NET Core для Service Fabric использует [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) по умолчанию. 

toolearn Дополнительные сведения о Kestrel и WebListener в служб Service Fabric см. слишком[ASP.NET Core в Service Fabric надежного обмена](service-fabric-reliable-services-communication-aspnetcore.md).

## <a name="connecting-tooa-reliable-actor-service"></a>Подключение службы Reliable Actor tooa
В этом руководстве описывается добавление веб-интерфейса для обеспечения связи со службой с отслеживанием состояния. Тем не менее вы можете использовать схожий tooactors tootalk модели. При создании проекта Reliable Actor Visual Studio автоматически создает проект интерфейса. Можно использовать этот интерфейс toogenerate прокси-сервер субъекта в проект toocommunicate hello web с hello субъекта. канал связи Hello предоставляется автоматически. Таким образом не требуется что-либо toodo, является эквивалентные tooestablishing `ServiceRemotingListener` как это было сделано для службы с отслеживанием состояния hello в этом учебнике.

## <a name="how-web-services-work-on-your-local-cluster"></a>Как работают веб-службы на локальном кластере
Как правило можно развернуть точно hello же Service Fabric приложения tooa несколькими компьютерами кластера, которые развернуты на локальный кластер и быть высокой уверенности, что он работает должным образом. Это происходит потому локального кластера является просто пяти узла конфигурации, свернут tooa одного компьютера.

Что касается служб tooweb, однако есть одно ключевые особенности организации. При кластера находится за подсистемой балансировки нагрузки, как и в Azure, необходимо убедиться, что веб-служб развертываются на каждом компьютере, так как Подсистема балансировки нагрузки hello просто циклическое трафик между компьютерами hello. Это можно сделать, установка hello `InstanceCount` для hello службы toohello специальное значение «-1».

Напротив, при локальном запуске веб-службы необходимо tooensure работает, только один экземпляр службы hello. В противном случае возникнут конфликтов в нескольких процессах, которые прослушивают hello же путь и порт. В результате число экземпляр службы web hello должно быть задано слишком «1» для локального развертывания.

tooconfigure разные значения для отдельной среды. в статье toolearn [Управление параметрами приложения для нескольких сред](service-fabric-manage-multiple-environment-app-configuration.md).

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы настроили веб-интерфейс для приложения с помощью ASP.NET Core, получите дополнительные сведения о работе ASP.NET Core с Service Fabric в статье о [ASP.NET Core в Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).

Далее, [Дополнительные сведения о взаимодействии со службами](service-fabric-connect-and-communicate-with-services.md) вообще tooget a завершения рисунок из как службы связи работает в Service Fabric.

После полного понимания того, как работает связь со службой, [создать кластер в Azure и развертывание облачных приложений toohello](service-fabric-cluster-creation-via-portal.md).

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
