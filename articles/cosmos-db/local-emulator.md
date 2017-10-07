---
title: "aaaDevelop локально с hello DB эмулятор Azure Cosmos | Документы Microsoft"
description: "Hello эмулятор DB Cosmos Azure можно разрабатывать и тестировать приложение для локально бесплатный, без создания подписки Azure."
services: cosmos-db
documentationcenter: 
keywords: "Эмулятор Azure Cosmos DB"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Использовать hello DB эмулятор Azure Cosmos локальной разработки и тестирования

<table>
<tr>
  <td><strong>Двоичные файлы</strong></td>
  <td>[Скачивание MSI](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Концентратор Docker](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Источник Docker</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
Hello эмулятор DB Cosmos Azure предоставляет локальную среду, эмулирующую hello Azure Cosmos DB службу в целях разработки. Hello эмулятор DB Cosmos Azure можно разрабатывать и тестировать приложение локально, без создания подписки Azure или любой расходов. Если вас устраивают, как приложение работает в hello эмулятор DB Cosmos Azure, можно переключиться toousing учетную запись Azure Cosmos DB в облаке hello.

В этой статье рассматриваются hello следующие задачи: 

> [!div class="checklist"]
> * Установка hello эмулятора
> * ОС Docker для Windows hello эмулятора
> * Выполнение проверки подлинности запросов
> * С помощью hello обозреватель данных, в эмуляторе hello
> * Экспорт сертификатов SSL
> * Вызов из командной строки hello hello эмулятора
> * Сбор файлов трассировки

Корпорация Майкрософт рекомендует Приступая к работе посмотрите следующие видео, где Kirill Gavrylyuk показано, как tooget работу с hello DB эмулятор Azure Cosmos hello. Примечание видео hello называется toohello эмулятор hello DocumentDB эмулятора, что был переименован средству hello hello DB эмулятор Azure Cosmos с момента щелкните hello видео. Все сведения в видео hello актуальны для hello Azure Cosmos DB эмулятора. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Как работает hello эмулятора
Hello эмулятор DB Cosmos Azure предоставляет эмуляцию hello Azure Cosmos DB службы высокого качества. В эмуляторе реализованы те же функции, что и в службе Azure Cosmos DB, включая поддержку создания документов JSON и выполнение запросов к ним, подготовку и масштабирование коллекций, а также выполнение хранимых процедур и триггеров. Можно разрабатывать и тестирования приложений с помощью hello Azure Cosmos DB эмулятор и развернуть tooAzure по всему миру, просто чтобы изменить конечную точку подключения toohello для Azure Cosmos DB отдельную конфигурацию.

Хотя мы создали высококачественных локальной эмуляции фактические службы Azure Cosmos DB hello, реализация hello hello DB эмулятор Azure Cosmos отличается от службы hello. Например hello DB эмулятор Azure Cosmos использует стандартных компонентов операционной системы, таких как hello локальной файловой системе сохраняемости и стек протокола HTTPS для подключения. Это означает, что некоторые функции, которая зависит от инфраструктуры Azure как глобальный репликации, задержка до миллисекунды десяти для операций чтения и записи и уровни согласованности пройтись недоступны через hello Azure Cosmos DB эмулятора.

> [!NOTE]
> В это время hello обозреватель данных, в hello эмулятор поддерживает только создание hello DocumentDB API и коллекций MongoDB. Hello обозреватель данных, в эмуляторе hello в настоящее время не поддерживает hello создания таблиц и диаграмм. 

## <a name="system-requirements"></a>Требования к системе
Hello эмулятор DB Cosmos Azure имеет следующие требования к оборудованию и программному обеспечению hello.

* Требования к программному обеспечению
  * Windows Server 2012 R2, Windows Server 2016 или Windows 10.
*   Минимальные требования к оборудованию
  * ОЗУ 2 ГБ.
  * 10 ГБ свободного дискового пространства.

## <a name="installation"></a>Установка
Можно загрузить и установить эмулятор DB Cosmos Azure hello из hello [центра загрузки Майкрософт](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> tooinstall, настройки и запуска hello эмулятор DB Cosmos Azure, необходимо иметь права администратора на компьютере hello.

## <a name="running-on-docker-for-windows"></a>Выполнение в Docker для Windows

Hello Azure Cosmos DB эмулятор может выполняться на Docker для Windows. Hello эмулятор не поддерживает Docker для Oracle Linux.

После получения [Docker для Windows](https://www.docker.com/docker-windows) установлен, вы можете извлечь образа эмулятора hello из Docker Hub, выполнив следующую команду из избранных оболочка hello (cmd.exe, PowerShell, и т. д.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
hello изображение toostart, запустите следующие команды hello.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

Hello ответа выглядит примерно toohello следующее:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Закрытие интерактивной оболочки hello один раз hello запуска эмулятора будет завершить работу hello эмулятора контейнера.

Конечная точка hello и главный ключ в ответе hello в клиентском приложении и импорта hello SSL-сертификата в узле. hello tooimport SSL-сертификат hello от командную строку администратора:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Запуск эмулятора hello

hello toostart эмулятор DB Cosmos Azure, выберите "Пуск" hello, или нажмите клавишу Windows hello. Начните вводить **DB эмулятор Azure Cosmos**и выберите hello эмулятор из списка приложений hello. 

![Выберите hello или клавишу hello Windows ключ запуска, начните вводить ** Azure Cosmos DB эмулятор ** и выберите hello эмулятор из списка приложений hello](./media/local-emulator/database-local-emulator-start.png)

При запуске эмулятора hello, появится значок в области уведомлений панели задач Windows hello. ![Уведомление локального эмулятора Azure Cosmos DB на панели задач](./media/local-emulator/database-local-emulator-taskbar.png)

Hello Azure Cosmos DB эмулятор по умолчанию выполняется на hello локального компьютера («localhost») прослушивания по порту 8081.

Hello Cosmos DB эмулятор Azure установлен по умолчанию toohello `C:\Program Files\Azure Cosmos DB Emulator` каталога. Можно также запустить и остановить hello эмулятор из командной строки hello. Дополнительные сведения см. в [справочнике программы командной строки](#command-line).

## <a name="start-data-explorer"></a>Запуск обозревателя данных

При запуске эмулятора Azure Cosmos DB hello он автоматически открывается обозреватель данных Azure Cosmos DB hello в браузере. Hello адрес будет отображаться как [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Если закрыть hello обозревателя и хотите toore открыть его позже, можно открыть hello URL-адрес в браузере или запустите его из hello DB эмулятор Azure Cosmos в hello значок на панели задач Windows, как показано ниже.

![Запуск обозревателя данных из локального эмулятора Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Проверка наличия обновлений
Обозреватель данных сообщает о наличии нового обновления, доступного для скачивания. 

> [!NOTE]
> Данные, созданные в одной версии hello Azure Cosmos DB эмулятор не гарантируется toobe доступны при использовании другой версии. Если требуется toopersist данных для долгосрочной hello, рекомендуется хранить их в базе данных Azure Cosmos учетной записи, а не в hello Azure Cosmos DB эмулятора. 

## <a name="authenticating-requests"></a>Выполнение проверки подлинности запросов
Так же, как с помощью DB Cosmos Azure в облаке hello каждого запроса, выполняемого для hello DB эмулятор Azure Cosmos должен пройти проверку подлинности. Hello эмулятор DB Cosmos Azure поддерживает фиксированной учетной записи и ключ хорошо известных проверки подлинности для проверки подлинности главного ключа. Эта учетная запись и ключ, hello единственные учетные данные для использования с hello Azure Cosmos DB эмулятора. К ним относятся:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> Hello главного ключа, поддерживаемые hello эмулятор DB Cosmos Azure предназначен только для использования с эмулятором hello. Учетная запись Azure Cosmos DB производства и ключ нельзя использовать с hello Azure Cosmos DB эмулятора. 

> [!NOTE] 
> После запуска эмулятора hello с hello параметр/KEY, затем использовать ключ создан hello вместо «C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw ==»

Кроме того, точно так же как hello Azure Cosmos DB службы, hello эмулятор DB Cosmos Azure поддерживает только безопасный обмен данными через SSL.

## <a name="running-hello-emulator-on-a-local-network"></a>Запуск эмулятора hello в локальной сети

Можно запустить эмулятор hello в локальной сети. tooenable доступа к сети, укажите параметр /AllowNetworkAccess hello в hello [командной строки](#command-line-syntax), который также необходимо указать/Key = key_string или/keyfile = имя_файла. Можно использовать /GenKeyFile = toogenerate имя_файла файл с заранее случайный ключ.  Затем можно передать этот слишком/KeyFile = file_name или/KEY = contents_of_file.

tooenable доступа к сети для hello первый раз hello пользователь должен завершить работу эмулятора hello и удалите каталог данных hello эмулятор (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-hello-emulator"></a>Разработка с использованием эмулятора hello
После имеют hello Azure Cosmos DB эмулятор на рабочем столе, можно использовать любые поддерживаемые [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) или hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract с hello эмулятора. Hello DB эмулятор Azure Cosmos также включает встроенные обозреватель данных, которая позволяет создавать коллекции hello DocumentDB и представление и MongoDB API и редактировать документы без написания кода.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Если вы используете [Azure Cosmos DB поддержка протоколов для MongoDB](mongodb-introduction.md), используйте hello, следующая строка подключения:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

Можно использовать существующие средства, такие как [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello DB эмулятор Azure Cosmos. Можно также перенести данные между hello эмулятор DB Cosmos Azure и службы Azure Cosmos DB hello, с помощью hello [средство переноса данных DB Cosmos Azure](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> После запуска эмулятора hello с hello параметр/KEY, затем использовать ключ создан hello вместо «C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw ==»

С использованием эмулятора Azure Cosmos DB hello, по умолчанию, можно создать коллекции too25 с одной секцией или секционированные коллекцию 1. Дополнительные сведения об изменении этого значения см. в разделе [значение hello PartitionCount](#set-partitioncount).

## <a name="export-hello-ssl-certificate"></a>Экспорт сертификата SSL hello

Языки .NET и toosecurely хранилище сертификатов Windows hello использования среды выполнения подключения локальный эмулятор Azure Cosmos DB toohello. Другие языки используют собственные методы для управления сертификатами и использования сертификатов. Java поддерживает собственное [хранилище сертификатов](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), а Python применяет [оболочки сокетов](https://docs.python.org/2/library/ssl.html).

В порядке tooobtain toouse сертификат с языками и сред выполнения, которые интегрируются с hello хранилище сертификатов Windows вы должны tooexport его с помощью диспетчера сертификатов Windows hello. Вы можете запустить его, выполнив certlm.msc или следуйте инструкциям в разделе шаг за шагом hello [экспортировать сертификаты hello Azure Cosmos DB эмулятор](./local-emulator-export-ssl-certificates.md). После запуска диспетчера сертификатов hello Привет открыть личные сертификаты, как показано ниже и экспорт hello сертификат с понятным именем hello «DocumentDBEmulatorCertificate» как Base64-кодировке x.509 (CER).

![Сертификат SSL для эмулятора Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

сертификат X.509 Hello можно импортировать в хранилище сертификатов Java hello, следуя инструкциям hello [Добавление toohello сертификат, в хранилище сертификатов ЦС Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store). После импорта hello сертификат в хранилище сертификатов hello приложения Java и MongoDB будут может tooconnect toohello DB эмулятор Azure Cosmos.

При подключении toohello эмулятор из Python и Node.js SDK, проверки SSL отключен.

## <a id="command-line"></a>Справочник по программе командной строки
Из места установки hello можно использовать toostart командной строки hello и остановки эмулятора hello, настройте параметры и выполнить другие операции.

### <a name="command-line-syntax"></a>Синтаксис для командной строки

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

tooview hello список параметров, тип `CosmosDB.Emulator.exe /?` hello командной строки.

<table>
<tr>
  <td><strong>Параметр</strong></td>
  <td><strong>Описание</strong></td>
  <td><strong>Команда</strong></td>
  <td><strong>Аргументы</strong></td>
</tr>
<tr>
  <td>[Нет аргументов]</td>
  <td>Запускается hello Azure Cosmos DB эмулятора с параметрами по умолчанию.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Help]</td>
  <td>Отображает hello список поддерживаемых аргументов командной строки.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>Завершает работу эмулятора DB Cosmos Azure hello.</td>
  <td>CosmosDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>Задает путь hello в toostore файлов данных. Значение по умолчанию — %LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath=&lt;путь_к_данным&gt;</td>
  <td>&lt;datapath&gt;: любой доступный путь</td>
</tr>
<tr>
  <td>Порт</td>
  <td>Указывает toouse номера порта hello hello эмулятора.  Значение по умолчанию — 8081.</td>
  <td>CosmosDB.Emulator.exe /Port=&lt;порт&gt;</td>
  <td>&lt;port&gt;: один номер порта</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Указывает hello toouse номер порта для обеспечения совместимости MongoDB API. Значение по умолчанию — 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort=&lt;порт_mongo&gt;</td>
  <td>&lt;mongoport&gt;: один номер порта</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Указывает toouse hello порты для прямого подключения. По умолчанию это порты 10251, 10252, 10253, 10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: разделенный запятыми список из 4 портов</td>
</tr>
<tr>
  <td>Ключ</td>
  <td>Ключ авторизации для эмулятора hello. Ключ должен быть hello 64-разрядного вектора кодировку base-64.</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;ключ&gt;</td>
  <td>&lt;ключ&gt;: ключ должен иметь кодировку base-64 hello 64-разрядного вектора</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Указывает, что ограничение частоты запросов включено.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Указывает, что ограничение частоты запросов отключено.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>Больше не показывать эмулятор hello пользовательского интерфейса.</td>
  <td>CosmosDB.Emulator.exe /NoUI</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>Скрывает обозреватель документов при запуске.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>Указывает максимальное количество hello секционированных коллекций. В разделе [изменить номер hello коллекций](#set-partitioncount) для получения дополнительной информации.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount=&lt;число_разделов&gt;</td>
  <td>&lt;partitioncount&gt;: максимально допустимое количество односекционных коллекций. Значение по умолчанию — 25. Максимально допустимое значение — 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Указывает количество секций в секционированную коллекцию по умолчанию hello.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; Значение по умолчанию — 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Включает эмулятор toohello доступа по сети. Необходимо также передать/KEY =&lt;key_string&gt; или/keyfile =&lt;имя_файла&gt; tooenable доступа к сети.</td>
  <td>CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;строка_ключа&gt;<br><br>или<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;имя_файла&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>Не изменять правила брандмауэра при использовании /AllowNetworkAccess.</td>
  <td>CosmosDB.Emulator.exe /NoFirewall</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>Создать новый ключ авторизации и сохраните toohello указанного файла. Hello созданный ключ может использоваться с hello/KEY или параметры/keyfile.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;tookey путь к файлу&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Целостность</td>
  <td>Задайте уровень согласованности hello по умолчанию для учетной записи hello.</td>
  <td>CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</td>
  <td>&lt;согласованность&gt;: значение должно быть одним из следующих hello [уровни согласованности](consistency-levels.md): сеанс, Strong, Eventual или BoundedStaleness.  значение по умолчанию Hello — сеанса.</td>
</tr>
<tr>
  <td>?</td>
  <td>Показать справочное сообщение hello.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Различия между hello эмулятор DB Cosmos Azure и Azure Cosmos DB 
Поскольку hello эмулятор DB Cosmos Azure предоставляет эмулированной среду на рабочей станции локальной разработчика, существуют функциональные различия между эмулятором hello и учетную запись Azure Cosmos DB в облаке hello:

* Hello эмулятор DB Cosmos Azure поддерживает только одной предопределенной учетной записи и хорошо известных главного ключа.  Повторное создание ключа невозможна в hello Azure Cosmos DB эмулятора.
* Hello Azure Cosmos DB эмулятора, не является масштабируемой службой и не будет поддерживать большого числа коллекций.
* Hello Azure Cosmos DB эмулятора не применяется для моделирования различных [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md).
* Hello Azure Cosmos DB эмулятор не вполне [регионов репликации](distribute-data-globally.md).
* Hello Azure Cosmos DB эмулятор не поддерживает переопределения квоты hello службы, доступные в службе Azure Cosmos DB hello (например ограничений на размер документа, повышенная секционированную коллекцию хранилища).
* Как копию hello Azure Cosmos DB эмулятор может не быть вверх toodate с самых последних изменений hello со службой Azure Cosmos DB hello, пожалуйста, [планировщик ресурсов Azure Cosmos DB](https://www.documentdb.com/capacityplanner) tooaccurately оценки производства пропускной способности (RUs) требования вашего приложения.

## <a id="set-partitioncount"></a>Номер hello изменения коллекций

По умолчанию можно создать коллекции с одной секцией too25 или коллекцию 1 секционированных hello Azure Cosmos DB эмулятора. Изменив hello **PartitionCount** значение, можно создать копию коллекции с одной секцией too250 или 10 секционированных коллекций или любое сочетание hello двух должен превышать 250 одной секции (где 1 секционированные Коллекция = 25 коллекция одной секции).

При попытке toocreate коллекцию после превышения hello текущее количество разделов, эмулятор hello исключение ServiceUnavailable, с сообщением, hello.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

число доступных toohello коллекций эмулятор DB Cosmos Azure, hello toochange hello следующие:

1. Удалить все локальные данные эмулятора DB Cosmos Azure щелкните правой кнопкой мыши hello **DB эмулятор Azure Cosmos** на hello в панели задач и выбрав значок **сброса данных...** .
2. Удалите все данные эмулятора в этой папке: C:\Users\имя_пользователя\AppData\Local\CosmosDBEmulator.
3. Закройте все открытые экземпляры, щелкнув правой кнопкой мыши hello **DB эмулятор Azure Cosmos** на hello в панели задач и выбрав значок **выхода**. Он может занять до минуты для всех экземпляров tooexit.
4. Установите последнюю версию hello hello [DB эмулятор Azure Cosmos](https://aka.ms/cosmosdb-emulator).
5. Запустите эмулятор hello с hello PartitionCount флаг, задав значение < = 250. Например, `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Устранение неполадок

Используйте следующие советы toohelp устранения неполадок, которые могут возникнуть в эмулятор Azure Cosmos DB hello hello.

- Если вы установили новую версию эмулятора hello и возникли ошибки, убедитесь, что сброс данных. Данные можно восстановить, щелкнув правой кнопкой мыши значок эмулятора DB Cosmos Azure hello hello в панели задач, выберите команду восстановить данные... Если hello ошибок не устраняется, можно удалить и переустановить приложение hello. В разделе [удалить локальный эмулятор hello](#uninstall) инструкции.

- В случае отказа эмулятор Azure Cosmos DB hello, собрать файлы дампа из папки c:\Users\user_name\AppData\Local\CrashDumps их сжатие и присоединить их по электронной почте tooan слишком[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- При возникновении сбоев в CosmosDB.StartupEntryPoint.exe, выполните следующую команду из командной строки администратора hello:`lodctr /R` 

- Если возникнет проблема с подключением, [сбор файлов трассировки](#trace-files), их сжатие и присоединить их по электронной почте tooan слишком[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- При получении **служба недоступна** сообщение, hello эмулятор может содержаться ошибка tooinitialize hello сетевой стек. Проверьте toosee при наличии безопасности клиентских Pulse hello или Juniper сетей установленным клиентом, как их сетевые драйверы фильтра может стать причиной проблемы hello. Удаление фильтра сети сторонних драйверов, обычно устраняет ошибку hello.

### <a id="trace-files"></a>Сбор файлов трассировки

toocollect отладочной трассировки, запустите следующие команды из командной строки с правами администратора hello:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Контрольное значение hello лоток toomake убедиться, что hello программы системного завершил работу, он может занять около минуты. Можно также просто щелкнуть **выхода** в интерфейсе пользователя эмулятор Azure Cosmos DB hello.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Воспроизвести проблему hello. Если обозреватель данных не работают, требуется только toowait tooopen hello браузера для ошибки hello toocatch несколько секунд.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Перейдите в слишком`%ProgramFiles%\Azure Cosmos DB Emulator` и найдите файл docdbemulator_000001.etl hello.
7. Отправить ETL-файла hello, а также шаги по воспроизведению слишком[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) для отладки.

### <a id="uninstall"></a>Удалить локальный эмулятор hello

1. Закройте все открытые экземпляры hello локальный эмулятор, щелкнув правой кнопкой мыши значок эмулятора DB Cosmos Azure hello hello в панели задач, выберите команду выхода. Он может занять до минуты для всех экземпляров tooexit.
2. Введите в поле поиска Windows hello **приложений и возможности** и щелкнет hello **приложений и компонентов (системные параметры)** результат.
3. Hello приложений прокрутите список слишком**DB эмулятор Azure Cosmos**, выберите его, щелкните **удаления**, подтверждение и нажмите кнопку **удаления** еще раз.
4. При удалении приложения hello перейдите tooC:\Users\<пользователя > \AppData\Local\CosmosDBEmulator и удалить папку hello. 

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * Установить локальный эмулятор hello
> * Функция RAND hello эмулятора на Docker для Windows
> * выполнили аутентификацию запросов;
> * Использовать hello обозреватель данных, в эмуляторе hello
> * экспортировали сертификаты SSL;
> * Вызывается из командной строки hello hello эмулятора
> * собрали файлы трассировки.

В этом учебнике вы узнали, как toouse hello локальный эмулятор для свободной локальной разработки. Теперь можно продолжить toohello следующее руководство и узнайте, как tooexport эмулятор SSL-сертификаты. 

> [!div class="nextstepaction"]
> [Экспорт сертификатов DB эмулятор Azure Cosmos hello](local-emulator-export-ssl-certificates.md)
