---
title: "aaaUsing Elasticsearch как магазин трассировки приложения Service Fabric | Документы Microsoft"
description: "Описывает способ использования приложения Service Fabric Elasticsearch и Kibana toostore, индекса и поиск по трассировок приложения (журнал)"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Использование ElasticSearch в качестве хранилища данных трассировки приложения Service Fabric
## <a name="introduction"></a>Введение
В этой статье описывается, как приложения [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) используют **ElasticSearch** и **Kibana** для хранения данных трассировки приложений, индексирования и поиска. [ElasticSearch](https://www.elastic.co/guide/index.html) — это распределенная и масштабируемая система с открытым кодом, предназначенная для поиска и анализа данных в режиме реального времени. Она хорошо подходит для описанной здесь задачи. Ее можно установить на виртуальные машины Windows или Linux, запущенные в Microsoft Azure. ElasticSearch может эффективно обрабатывать *структурированные* трассировки, созданные с помощью таких технологий, как **трассировка событий Windows (ETW)**.

Трассировка событий Windows используется служба среды выполнения toosource диагностических сведений о структуре (трассировки). Он является hello слишком рекомендуется метод toosource приложения Service Fabric для их диагностические сведения. С помощью hello тот же механизм позволяет корреляцию между трассировками предоставленный среды выполнения и предоставляемую приложением и облегчает Устранение неполадок. Service Fabric шаблоны проектов в Visual Studio включают API ведения журнала (в зависимости от hello .NET **EventSource** класса), создает трассировки событий Windows по умолчанию. Общие сведения о трассировке приложений Service Fabric с помощью ETW см. в разделе [Мониторинг и диагностика состояния служб в локальной среде разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Для hello трассировки tooshow вверх в Elasticsearch они должны toobe перенаправляться на узлах кластера Service Fabric hello в режиме реального времени (пока приложение hello) и отправляются в конечную точку tooan Elasticsearch. Есть два основных способа записи данных трассировки.

* **Внутрипроцессная запись данных трассировки.**  
  приложения Hello, или более точно, процесс службы отвечает за отправку hello диагностических данных toohello трассировки хранилища (Elasticsearch).
* **Внепроцессная запись данных трассировки.**  
  Отдельный агент захватывать трассировку из процесса hello службы или процессы и отправки их в хранилище toohello трассировки.

Ниже описаны как tooset копирование Elasticsearch в Azure, рассматриваются преимущества hello и недостатки для обоих параметров захвата и объясняется, как tooconfigure Service Fabric службы tooElasticsearch toosend данных.

## <a name="set-up-elasticsearch-on-azure"></a>Настройка ElasticSearch в Azure
Hello наиболее простым способом tooset hello Elasticsearch службы в Azure выполняется с помощью [ **шаблоны Azure Resource Manager**](../azure-resource-manager/resource-group-overview.md). Полнофункциональный [шаблон быстрого запуска диспетчера ресурсов Azure для ElasticSearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) можно получить из репозитория шаблонов быстрого запуска Azure. В этом шаблоне используются отдельные учетные записи хранения для единиц масштабирования (групп узлов). Он также может подготовить отдельные узлы клиента и сервера с различными конфигурациями и различным количеством подключенных дисков данных.

Здесь мы используем другой шаблон, с именем **ES MultiNode** из hello [хранилища Azure средства диагностики](https://github.com/Azure/azure-diagnostics-tools). Этот шаблон является проще toouse и создает кластер Elasticsearch защищен обычной проверки подлинности HTTP. Прежде чем продолжить, загрузите репозитория hello из GitHub tooyour машины (путем клонирования репозитория hello или загрузка ZIP-файл). Hello ES MultiNode шаблона находится в папке hello с hello таким же именем.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Подготовка toorun машины Elasticsearch сценарии установки
Hello шаблона hello ES MultiNode toouse простым способом — через указанный сценарий Azure PowerShell с именем `CreateElasticSearchCluster`. toouse этот сценарий, необходимо tooinstall модули PowerShell и инструмент, который называется **openssl**. последний Hello необходим для создания SSH-ключ, который можно использовать tooadminister кластера Elasticsearch удаленно.

`CreateElasticSearchCluster`скрипт предназначен для удобства использования с шаблоном hello ES MultiNode с компьютером Windows. Это шаблон hello возможных toouse на компьютере не под управлением Windows, но в этом сценарии выходит за рамки данной статьи hello.

1. Установите [**модули Azure PowerShell**](http://aka.ms/webpi-azps) (если они еще не установлены). При появлении запроса щелкните **Запуск**, а затем — **Установить**. Требуется Azure PowerShell 1.3 или более поздней версии.
2. Hello **openssl** средство включено в распределение hello [ **Git для Windows**](http://www.git-scm.com/downloads). Установите [Git для Windows](http://www.git-scm.com/downloads) , если вы этого еще не сделали. (параметры установки по умолчанию hello корректны.)
3. Предположим, что Git установлен, но не включены в системном пути hello, откройте окно Microsoft Azure PowerShell и выполните hello, следующие команды:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Замените hello `<Git installation folder>` с расположением hello Git на компьютере; по умолчанию hello — **«C:\Program Files\Git»**. Обратите внимание, hello символ точки с запятой в начале hello hello первого пути.
4. Убедитесь, что вы вошли на tooAzure (через [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) командлета) и выбранных hello подписка, которая используется toocreate кластера эластичной поиска. Проверить, правильно ли выбрана подписка, можно с помощью командлетов `Get-AzureRmContext` и `Get-AzureRmSubscription`.
5. Если вы еще не сделали этого, измените hello в папку текущего каталога toohello ES MultiNode.

### <a name="run-hello-createelasticsearchcluster-script"></a>Запустите сценарий CreateElasticSearchCluster hello
Перед запуском сценария Привет открыть hello `azuredeploy-parameters.json` файл и проверьте либо указать значения для параметров сценария hello. предоставляются следующие параметры Hello.

| Имя параметра | Описание |
| --- | --- |
| dnsNameForLoadBalancerIP |Имя Hello, используемые toocreate hello публично видимых DNS-имя кластера эластичной поиска hello (путем добавления toohello указано доменное имя для hello регион Azure). Например если значение этого параметра — «myBigCluster» и hello выбранный регион Azure находится Запад США, hello результирующее имя DNS для кластера hello — myBigCluster.westus.cloudapp.azure.com. <br /><br />Это имя также служит в качестве корневое имя для многих артефактов, связанных с кластером hello эластичной поиска, такие как имена узлов данных. |
| adminUsername |Имя Hello hello учетной записи администратора по управлению кластером эластичной поиска hello (автоматически создаются соответствующие ключи SSH). |
| dataNodeCount |количество узлов в кластере эластичной поиска hello Hello. Текущая версия скрипта hello Hello не различает узлы данных и запросов; все узлы воспроизвести обеих ролей. Узлы too3 значения по умолчанию. |
| dataDiskSize |размер Hello дисков данных (в ГБ), выделяемый для каждого узла данных. Каждый узел получает 4 дисков данных, специально выделенном tooElastic службы поиска. |
| region |Имя Hello регион Azure, где следует разместить hello эластичной поиска кластера. |
| esUserName |Hello имя пользователя hello, настроить кластера tooES toohave доступа (тема tooHTTP обычной проверки подлинности). Hello пароль не является частью файла параметров и должно быть обеспечено при `CreateElasticSearchCluster` запуске сценария. |
| vmSizeDataNodes |Hello Azure размер виртуальной машины для узлов кластера эластичной поиска. TooStandard_D2 значения по умолчанию. |

Теперь все готово toorun hello скрипта. Проблема hello следующую команду:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

где: 

| Имя параметра скрипта | Описание |
| --- | --- |
| `<es-group-name>` |Имя группы ресурсов Azure hello, который будет содержать все ресурсы кластера эластичной поиска Hello. |
| `<azure-region>` |Имя Hello hello регион Azure, которой должен быть создан hello эластичной поиска кластера. |
| `<es-password>` |Hello пароль для пользователя эластичной поиска hello. |

> [!NOTE]
> При появлении исключения NullReferenceException из командлета hello AzureResourceGroup теста, вы забыли toolog на tooAzure (`Add-AzureRmAccount`).
> 
> 

Если появляется сообщение об ошибке из выполнения сценария hello и определить, что hello ошибка вызвана значение параметра неправильный шаблон, исправьте файл параметров hello и снова запустите скрипт hello с именем группы ресурсов, отличной. Кроме того, можно использовать повторно hello одинаковые имена групп ресурсов и иметь hello скрипт очистки hello старого, добавив hello `-RemoveExistingResourceGroup` вызов сценария toohello параметра.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Результат выполнения сценария CreateElasticSearchCluster hello
После запуска hello `CreateElasticSearchCluster` скрипта, будут созданы следующие основные артефакты hello. В этом примере предполагается, что «myBigCluster» используется в качестве значения hello hello `dnsNameForLoadBalancerIP` параметр и этого hello региона, где была создана hello кластера является Запад США.

| Артефакт | Имя, расположение и примечания |
| --- | --- |
| Ключ SSH для удаленного администрирования |файл myBigCluster.key (в каталоге hello, из которого hello CreateElasticSearchCluster была запущена). <br /><br />Данный файл ключа может быть узел администрирования используется tooconnect toohello и (через узел администрирования hello) toodata узлов в кластере hello. |
| Узел администрирования |myBigCluster-admin.westus.cloudapp.azure.com <br /><br />Выделенной виртуальной Машины для удаленного администрирования кластера Elasticsearch--hello только один из них обеспечивает внешних соединений по протоколу SSH. Он выполняется на hello же виртуальной сети, что все узлы кластера Elasticsearch hello, но он не не запускайте все службы Elasticsearch. |
| Узлы данных |myBigCluster1– myBigCluster*N* <br /><br />Узлы данных, на которых работают службы ElasticSearch и Kibana. Вы можете подключиться через SSH tooeach узла, но только через узел администрирования hello. |
| Кластер Elasticsearch |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />Hello основную конечную точку для кластера Elasticsearch hello (Примечание hello /es суффикс). Используется обычная проверка подлинности HTTP (hello учетные данные были hello указанных параметров esUserName/esPassword шаблона hello ES MultiNode). кластер Hello также имеет hello head подключаемый модуль установлен (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) для администрирования базового кластера. |
| Служба Kibana |http://myBigCluster.westus.cloudapp.azure.com <br /><br />Hello Kibana службы, Настройка tooshow данных из hello создания кластера Elasticsearch. Он защищен hello же учетные данные проверки подлинности как hello кластера сам. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>Внутрипроцессная и внепроцессная запись данных трассировки
В введение hello упоминалось два основных способа сбора диагностических данных: в процессе и out of process. Каждый имеет свои преимущества и недостатки.

Преимущества hello **процесс записи трассировки** включают:

1. *Простая настройка и развертывание.*
   
   * Конфигурация Hello сбора диагностических данных — просто частью конфигурации приложения hello. Это легко tooalways оставить его «синхронизировано» с hello остальной части приложения hello.
   * Настройка каждого приложения или службы также является несложной задачей.
   * Захват трассировки out of process обычно требуется отдельное развертывание и конфигурация диагностики агента hello, лишние административную задачу и потенциальный источник ошибок. Технология определенного агента Hello часто позволяет только один экземпляр агента hello на каждую виртуальную машину (узел). Это означает этой конфигурации для hello коллекцию конфигурации диагностики hello является общим для всех приложений и служб, работающих на этом узле.
2. *Гибкость*
   
   * Hello приложение может отправлять данные hello везде, где он должен toogo, при условии, что имеется клиентская библиотека, которая поддерживает hello целевые системы хранения данных. При необходимости можно добавлять новые приемники.
   * Можно реализовать сложные правила сбора, фильтрации и статистической обработки данных.
   * Захват трассировки out of process часто ограничивается hello данных приемников, которые поддерживает агент hello. Некоторые агенты являются расширяемыми.
3. *Доступ к данным приложения toointernal и контекстом*
   
   * Hello диагностики подсистемы, выполняющиеся внутри процесса hello приложения или службы можно легко дополнить hello трассировок с помощью контекстных сведений.
   * В подходе out of process hello hello данных должны отправляться агента tooan через механизм межпроцессного взаимодействия например трассировки событий Windows. Однако при таком механизме могут возникнуть дополнительные ограничения.

Преимущества hello **захват трассировки out of process** включают:

1. *Здравствуйте, приложение hello toomonitor возможности и сбор аварийных дампов*
   
   * Захват в процесс трассировки может быть неудачной, если приложение hello сбоя toostart или аварийно завершает работу. Независимый агент имеет гораздо больше шансов собрать важные сведения для устранения неполадок.<br /><br />
2. *Зрелость, надежность и высокая производительность*
   
   * Поставщик платформы (например, агент диагностики Microsoft Azure), разработанный агент был toorigorous субъекта, тестирования и усиление Битва.
   * В процессе трассировки записи необходимо соблюдать осторожность tooensure действие hello передачи диагностических данных из процесса приложения не мешать основных задач приложения hello или вызвать проблемы синхронизации или производительности. Независимо друг от друга агента является менее подвержены возникновению проблем toothese и специально разработанные toolimit его воздействие на систему hello.

Это возможно toocombine и преимущества обоих подходов. На самом деле бывает hello наилучшим решением для многих приложений.

Здесь мы используем hello **Microsoft.Diagnostic.Listeners библиотеки** и hello в процессе трассировки сбор данных toosend из кластера Service Fabric приложения tooan Elasticsearch.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Используйте hello прослушиватели библиотеки toosend диагностических данных tooElasticsearch
Библиотека Microsoft.Diagnostic.Listeners Hello является частью PartyCluster образец приложения Service Fabric. toouse его:

1. Загрузить [PartyCluster образец hello](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) из GitHub.
2. Копировать из hello PartyCluster directory toohello решения папки образца приложения hello, который должен toosend hello данных tooElasticsearch hello Microsoft.Diagnostics.Listeners и Microsoft.Diagnostics.Listeners.Fabric проекты (всей папки) .
3. Откройте решение целевой hello, щелкните правой кнопкой мыши узел решения hello в hello в обозревателе решений и выберите **Добавление существующего проекта**. Добавьте проект toohello hello Microsoft.Diagnostics.Listeners решение. Повторите эти шаги hello же hello Microsoft.Diagnostics.Listeners.Fabric проекта.
4. Добавьте ссылку на проект из службы проекты toohello двух добавленных проектов. (Microsoft.Diagnostics.EventListeners и Microsoft.Diagnostics.EventListeners.Fabric должен ссылаться каждой службы, который должен tooElasticsearch toosend данных).
   
    ![Проект ссылается на tooMicrosoft.Diagnostics.EventListeners и Microsoft.Diagnostics.EventListeners.Fabric библиотеки][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Общедоступная версия Service Fabric и пакет Microsoft.Diagnostics.Tracing NuGet
Приложения, основанные на общедоступной версии Service Fabric (версия 2.0.135 от 31 марта 2016 года), нацелены на платформу **.NET Framework 4.5.2**. Эта версия предназначена hello самую новую версию hello поддерживается Azure во время hello hello Общедоступной версии .NET Framework. К сожалению эта версия hello framework отсутствуют некоторые EventListener API, требуется библиотека Microsoft.Diagnostics.Listeners hello. Поскольку EventSource (hello компонент, являющийся основой hello ведения журнала интерфейсы API в приложениях структуры) и EventListener тесно связаны, каждый проект, использующий библиотеку Microsoft.Diagnostics.Listeners hello необходимо использовать альтернативной реализации EventSource. Эта реализация обеспечивается hello **пакет Microsoft.Diagnostics.Tracing Nuget**, разработанный корпорацией Майкрософт. пакет Hello полной обратной совместимостью с EventSource включаются в hello framework, поэтому изменять код не должно возникать необходимости отличные от имен, на которую указывает ссылка.

toostart с помощью реализации Microsoft.Diagnostics.Tracing hello класса EventSource hello, выполните следующие действия для каждого проекта службы, который должен tooElasticsearch toosend данных:

1. Правой кнопкой мыши проект службы hello и выберите **управление пакетами Nuget**.
2. Переключение источника пакета toohello nuget.org (если он не установлен) и выполните поиск «**Microsoft.Diagnostics.Tracing**».
3. Установка hello `Microsoft.Diagnostics.Tracing.EventSource` пакет (и его зависимости).
4. Откройте hello **ServiceEventSource.cs** или **ActorEventSource.cs** в проекте службы и замените hello `using System.Diagnostics.Tracing` директив поверх hello файл с hello `using Microsoft.Diagnostics.Tracing` директивы.

Эти действия не будет требоваться один раз hello **.NET Framework 4.6** поддерживается в Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Создание и настройка экземпляра прослушивателя ElasticSearch
Hello последним шагом для отправки tooElasticsearch диагностических данных является toocreate экземпляр `ElasticSearchListener` и настройте его с данными подключения Elasticsearch. прослушиватель Hello автоматически захватывает всех событий, вызванных через EventSource классов, определенных в проекте службы hello. Ему toobe активности во время существования hello службы hello, наиболее hello размещать toocreate, где находится hello код инициализации службы. Код инициализации hello для службы без отслеживания состояния может выглядеть после hello необходимые изменения (указано дополнения в комментарии, начиная с `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Данные подключения Elasticsearch должны быть помещены в отдельный раздел в файле конфигурации службы hello (**PackageRoot\Config\Settings.xml**). Имя Hello hello раздела должно соответствовать toohello значению, переданному в toohello `FabricConfigurationProvider` конструктор, например:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Здравствуйте, значения `serviceUri`, `userName` и `password` параметров соответствуют адрес конечной точки кластера Elasticsearch toohello, Elasticsearch имя пользователя и пароль, соответственно. `indexNamePrefix`— префикс hello Elasticsearch индексов; Библиотека Microsoft.Diagnostics.Listeners Hello ежедневно создает новый индекс для своих данных.

### <a name="verification"></a>Проверка
Вот и все! Теперь при запуске службы hello начинается отправка трассировок toohello Elasticsearch службы, указанной в конфигурации hello. Это можно проверить, открывающей hello Kibana пользовательского интерфейса, связанного с hello целевого экземпляра Elasticsearch. В нашем примере адрес страницы приветствия — http://myBigCluster.westus.cloudapp.azure.com/. Убедитесь, что индексы с префиксом имени hello, выбранные для hello `ElasticSearchListener` экземпляр действительно были создается и заполняется данными.

![Отображение событий приложения PartyCluster в службе Kibana][2]

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о диагностике и мониторинге службы Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
