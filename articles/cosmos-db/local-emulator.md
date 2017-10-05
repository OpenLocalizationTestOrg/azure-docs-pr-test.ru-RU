---
title: "Разработка с помощью эмулятора Cosmos DB в локальной среде | Документация Майкрософт"
description: "С помощью эмулятора Azure Cosmos DB вы можете бесплатно разрабатывать и тестировать приложения локально. Для этого вам не нужно создавать подписку Azure."
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
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Использование эмулятора Azure Cosmos DB для разработки и тестирования в локальной среде

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
  
Эмулятор Azure Cosmos DB предоставляет локальную среду для разработки, которая эмулирует службу Azure Cosmos DB. С помощью эмулятора Azure Cosmos DB вы можете локально разрабатывать и тестировать приложения, не создавая подписку Azure и не тратя средства. Если приложение в эмуляторе Azure Cosmos DB работает правильно, вы можете использовать учетную запись Azure Cosmos DB в облаке.

В этой статье рассматриваются следующие задачи: 

> [!div class="checklist"]
> * Установка эмулятора
> * Запуск эмулятора в Docker для Windows
> * Выполнение проверки подлинности запросов
> * Использование обозревателя данных в эмуляторе
> * Экспорт сертификатов SSL
> * Вызов эмулятора из командной строки
> * Сбор файлов трассировки

Рекомендуем просмотреть следующий видеоролик, в котором Кирилл Гаврилюк покажет, как начать работу с эмулятором Azure Cosmos DB. Обратите внимание, что в видео эмулятор называется эмулятором DocumentDB, но с момента съемки видео сам инструмент переименован в эмулятор Azure Cosmos DB с момента записи видео. Все данные в видео актуальны для эмулятора Azure Cosmos DB. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a>Принцип работы эмулятора
Эмулятор Azure Cosmos DB обеспечивает высокоточную эмуляцию службы Azure Cosmos DB. В эмуляторе реализованы те же функции, что и в службе Azure Cosmos DB, включая поддержку создания документов JSON и выполнение запросов к ним, подготовку и масштабирование коллекций, а также выполнение хранимых процедур и триггеров. С помощью эмулятора Azure Cosmos DB можно разрабатывать и тестировать приложения. Чтобы развернуть эти приложения в глобальной среде Azure, нужно изменить всего один параметр конфигурации для конечной точки подключения к Azure Cosmos DB.

Хотя мы и создали высокоточную локальную эмуляцию настоящей службы Azure Cosmos DB, реализация эмулятора Azure Cosmos DB несколько отличается. Например, эмулятор Azure Cosmos DB использует стандартные компоненты ОС: локальную файловую систему для сохранения данных и стек протокола HTTPS для подключений. Это означает, что некоторые возможности инфраструктуры Azure будут не доступны в эмуляторе Azure Cosmos DB, включая глобальную репликацию, задержку менее 10 миллисекунд для операций чтения и записи или настраиваемые уровни согласованности.

> [!NOTE]
> Сейчас обозреватель данных в эмуляторе поддерживает создание коллекций API DocumentDB и MongoDB. Сейчас обозреватель данных в эмуляторе не поддерживает создание таблиц и графов. 

## <a name="system-requirements"></a>Требования к системе
Эмулятор Azure Cosmos DB имеет следующие требования к оборудованию и программному обеспечению.

* Требования к программному обеспечению
  * Windows Server 2012 R2, Windows Server 2016 или Windows 10.
*   Минимальные требования к оборудованию
  * ОЗУ 2 ГБ.
  * 10 ГБ свободного дискового пространства.

## <a name="installation"></a>Установка
Эмулятор Azure Cosmos DB можно скачать и установить из [центра загрузки Майкрософт](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> Чтобы установить, настроить и запустить эмулятор Azure Cosmos DB, нужны права администратора на локальном компьютере.

## <a name="running-on-docker-for-windows"></a>Выполнение в Docker для Windows

Эмулятор Azure Cosmos DB может выполняться в Docker для Windows. Этот эмулятор не работает в Docker для Oracle Linux.

Если установлен [Docker для Windows](https://www.docker.com/docker-windows), вы можете извлечь образ эмулятора из Docker Hub, выполнив следующую команду из любой оболочки по своему усмотрению (cmd.exe, PowerShell и т. д.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
Чтобы запустить образ, выполните следующие команды:

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

Ответ выглядит примерно так:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Если закрыть интерактивную оболочку после запуска эмулятора, его контейнер завершит работу.

Воспользуйтесь конечной точкой и главным ключом из ответа в клиенте и импортируйте SSL-сертификат в узел. Чтобы импортировать SSL-сертификат, выполните следующие действия из командной строки с правами администратора.

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a>Запуск эмулятора

Чтобы запустить эмулятор Azure Cosmos DB, нажмите кнопку "Пуск" или клавишу Windows. Начните вводить текст **Эмулятор Azure Cosmos DB** и выберите эмулятор в списке приложений. 

![Нажмите кнопку "Пуск" или клавишу Windows, начните вводить **Эмулятор Azure Cosmos DB**, а затем выберите эмулятор в списке приложений](./media/local-emulator/database-local-emulator-start.png)

При запуске эмулятора в области уведомлений панели задач Windows появится соответствующий значок. ![Уведомление локального эмулятора Azure Cosmos DB на панели задач](./media/local-emulator/database-local-emulator-taskbar.png)

Эмулятор Azure Cosmos DB по умолчанию выполняется на локальном компьютере (localhost) и прослушивает порт 8081.

Эмулятор Azure Cosmos DB по умолчанию устанавливается в каталог `C:\Program Files\Azure Cosmos DB Emulator`. Можно также запустить и остановить эмулятор из командной строки. Дополнительные сведения см. в [справочнике программы командной строки](#command-line).

## <a name="start-data-explorer"></a>Запуск обозревателя данных

При запуске эмулятор Azure Cosmos DB автоматически откроет в браузере страницу обозревателя данных Azure Cosmos DB. В адресной строке вы увидите адрес [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Чтобы позднее открыть страницу обозревателя данных, вы можете ввести в браузере этот URL-адрес или запустить обозреватель из эмулятора Azure Cosmos DB, используя значок в области уведомлений Windows, как показано ниже.

![Запуск обозревателя данных из локального эмулятора Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Проверка наличия обновлений
Обозреватель данных сообщает о наличии нового обновления, доступного для скачивания. 

> [!NOTE]
> Данные, созданные в одной версии эмулятора Azure Cosmos DB, могут оказаться недоступными при использовании другой версии. Если нужно сохранить данные на длительный срок, мы рекомендуем хранить их в учетной записи хранения Azure Cosmos DB, а не эмуляторе Azure Cosmos DB. 

## <a name="authenticating-requests"></a>Выполнение проверки подлинности запросов
Как и в настоящей облачной службе Azure, в эмуляторе Azure Cosmos DB для каждого полученного запроса должна выполняться аутентификация. Эмулятор Azure Cosmos DB поддерживает аутентификацию с помощью главного ключа, используя одну предопределенную учетную запись и известный ключ аутентификации. В качестве учетных данных для эмулятора Azure Cosmos DB можно использовать только эту учетную запись и только этот ключ. К ним относятся:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> Главный ключ, поддерживаемый эмулятором Azure Cosmos DB, предназначен для использования только с этим эмулятором. Нельзя использовать рабочую учетную запись Azure Cosmos DB и ключ с эмулятором Azure Cosmos DB. 

> [!NOTE] 
> Если вы запустили эмулятор с параметром /Key, то используйте созданный ключ вместо "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="

Кроме того, как и настоящая служба Azure Cosmos DB, эмулятор Azure Cosmos DB поддерживает только безопасное подключение по протоколу SSL.

## <a name="running-the-emulator-on-a-local-network"></a>Запуск эмулятора в локальной сети

Вы можете запустить эмулятор в локальной сети. Чтобы разрешить доступ к сети, укажите параметр /AllowNetworkAccess в [командной строке](#command-line-syntax), а также один из обязательных дополнительных параметров /Key=key_string или /KeyFile=file_name. Можно также применить параметр GenKeyFile=file_name, чтобы заранее создать случайный ключ.  Затем передайте этот ключ в параметре /KeyFile=file_name или /Key=contents_of_file.

Чтобы в первый раз получить доступ к сети, пользователь должен завершить работу эмулятора и удалить каталог данных эмулятора (C:\Users\имя_пользователя\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-the-emulator"></a>Разработка с помощью эмулятора
Когда эмулятор Azure Cosmos DB будет запущен на рабочем столе, вы сможете работать с ним с помощью любых поддерживаемых [пакетов SDK для Azure Cosmos DB](documentdb-sdk-dotnet.md) или [REST API Azure Cosmos DB](/rest/api/documentdb/). Эмулятор Azure Cosmos DB также содержит встроенный обозреватель данных, позволяющий создавать коллекции для API DocumentDB и MongoDB, а также просматривать и редактировать документы без написания кода.   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Если вы используете [поддержку протокола Azure Cosmos DB для MongoDB](mongodb-introduction.md), используйте следующую строку подключения:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

Для подключения к эмулятору Azure Cosmos DB вы можете использовать имеющиеся инструменты, такие как [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio). Можно также переносить данные между эмулятором Azure Cosmos DB и службой Azure Cosmos DB с помощью [средства миграции данных Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Если вы запустили эмулятор с параметром /Key, то используйте созданный ключ вместо "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="

По умолчанию с помощью эмулятора Azure Cosmos DB можно создать до 25 односекционных коллекций или одну секционированную коллекцию. Дополнительные сведения об изменении этого значения см. в разделе [Изменение количества коллекций](#set-partitioncount).

## <a name="export-the-ssl-certificate"></a>Экспорт SSL-сертификата

Языки и среда выполнения .NET используют хранилище сертификатов Windows для безопасного подключения к локальному эмулятору Azure Cosmos DB. Другие языки используют собственные методы для управления сертификатами и использования сертификатов. Java поддерживает собственное [хранилище сертификатов](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), а Python применяет [оболочки сокетов](https://docs.python.org/2/library/ssl.html).

Чтобы использовать сертификат с языками и средами выполнения, которые не интегрируются с хранилищем сертификатов Windows, необходимо экспортировать сертификат с помощью диспетчера сертификатов Windows. Чтобы открыть его, запустите файл certlm.msc или выполните пошаговые инструкции по [экспорту сертификатов в эмуляторе Azure Cosmos DB](./local-emulator-export-ssl-certificates.md). Когда откроется диспетчер сертификатов, откройте в нем "Личные сертификаты", как показано ниже, и экспортируйте сертификат с понятным именем DocumentDBEmulatorCertificate в формате X.509 с кодировкой BASE-64 (CER-файл).

![Сертификат SSL для эмулятора Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

Чтобы импортировать сертификат X.509 в хранилище сертификатов Java, выполните инструкции из статьи [Добавление сертификата в хранилище сертификатов ЦС Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store). После импорта сертификата в хранилище сертификатов приложения Java и MongoDB смогут подключаться к эмулятору DB Azure Cosmos.

При подключении к эмулятору с помощью пакетов SDK для Python и Node.js проверка SSL отключена.

## <a id="command-line"></a>Справочник по программе командной строки
С помощью командной строки из папки установки можно запускать и останавливать эмулятор, настраивать параметры и выполнять другие операции.

### <a name="command-line-syntax"></a>Синтаксис для командной строки

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

Чтобы просмотреть список параметров, в командной строке введите `CosmosDB.Emulator.exe /?` .

<table>
<tr>
  <td><strong>Параметр</strong></td>
  <td><strong>Описание</strong></td>
  <td><strong>Команда</strong></td>
  <td><strong>Аргументы</strong></td>
</tr>
<tr>
  <td>[Нет аргументов]</td>
  <td>Запускает эмулятор Azure Cosmos DB с параметрами по умолчанию.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Help]</td>
  <td>Отображает список поддерживаемых аргументов командной строки.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>Завершает работу эмулятора Azure Cosmos DB.</td>
  <td>CosmosDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>Указывает путь для сохранения файлов данных. Значение по умолчанию — %LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath=&lt;путь_к_данным&gt;</td>
  <td>&lt;datapath&gt;: любой доступный путь</td>
</tr>
<tr>
  <td>Порт</td>
  <td>Указывает номер порта, который должен использоваться эмулятором.  Значение по умолчанию — 8081.</td>
  <td>CosmosDB.Emulator.exe /Port=&lt;порт&gt;</td>
  <td>&lt;port&gt;: один номер порта</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Указывает номер порта для использования с интерфейсом совместимости с MongoDB. Значение по умолчанию — 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort=&lt;порт_mongo&gt;</td>
  <td>&lt;mongoport&gt;: один номер порта</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Указывает порты, которые нужно использовать для прямого подключения. По умолчанию это порты 10251, 10252, 10253, 10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: разделенный запятыми список из 4 портов</td>
</tr>
<tr>
  <td>Ключ</td>
  <td>Ключ проверки подлинности для эмулятора. Ключ должен иметь формат 64-разрядного вектора в кодировке Base-64.</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;ключ&gt;</td>
  <td>&lt;key&gt;: ключ в формате 64-разрядного вектора в кодировке base-64</td>
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
  <td>Скрывает пользовательский интерфейс эмулятора.</td>
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
  <td>Указывает максимальное количество секционированных коллекций. Дополнительные сведения см. в разделе [Изменение количества коллекций](#set-partitioncount).</td>
  <td>CosmosDB.Emulator.exe /PartitionCount=&lt;число_разделов&gt;</td>
  <td>&lt;partitioncount&gt;: максимально допустимое количество односекционных коллекций. Значение по умолчанию — 25. Максимально допустимое значение — 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Указывает количество секций по умолчанию для секционированной коллекции.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; Значение по умолчанию — 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Разрешает доступ к эмулятору по сети. Для включения сетевого доступа нужно также передать один из параметров: /Key=&lt;строка_ключа&gt; или /KeyFile=&lt;имя_файла&gt;.</td>
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
  <td>Создает новый ключ авторизации и сохраняет его в указанном файле. Созданный ключ можно использовать с параметрами/Key или/KeyFile.</td>
  <td>CosmosDB.Emulator.exe  /GenKeyFile=&lt;путь к файлу ключа&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Целостность</td>
  <td>Определяет уровень согласованности по умолчанию для учетной записи.</td>
  <td>CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</td>
  <td>&lt;consistency&gt;: допускается любое значение из следующих [уровней согласованности](consistency-levels.md): Session (на уровне сеансов), Strong (сильная), Eventual (итоговая) или BoundedStaleness (с ограниченным устареванием).  По умолчанию используется значение Session.</td>
</tr>
<tr>
  <td>?</td>
  <td>Показывает справочные сообщения.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Различия между эмулятором Azure Cosmos DB и службой Azure Cosmos DB 
Эмулятор Azure Cosmos DB обеспечивает эмулированную среду, выполняемую на локальном компьютере разработчика. Поэтому возможности эмулятора и облачной учетной записи Azure Cosmos DB несколько отличаются.

* Эмулятор Azure Cosmos DB поддерживает только одну предопределенную учетную запись и известный главный ключ.  Повторное создание ключей в эмуляторе Azure Cosmos DB не поддерживается.
* Эмулятор Azure Cosmos DB не поддерживает масштабирование и не может работать с большим числом коллекций.
* Эмулятор Azure Cosmos DB не поддерживает [уровни согласованности Azure Cosmos DB](consistency-levels.md).
* Эмулятор Azure Cosmos DB не поддерживает [репликацию между несколькими регионами](distribute-data-globally.md).
* Эмулятор Azure Cosmos DB не поддерживает переопределение квот для службы, которое возможно в службе Azure Cosmos DB (например, ограничения на размер документа, увеличение хранилища для секционированных коллекций).
* Локальная версия эмулятора Azure Cosmos DB может не всегда отражать свежие изменения в службе Azure Cosmos DB. Поэтому, чтобы точно оценить необходимую пропускную способность для приложения, используйте [планировщик ресурсов Azure Cosmos DB](https://www.documentdb.com/capacityplanner).

## <a id="set-partitioncount"></a>Изменение количества коллекций

По умолчанию с помощью эмулятора Azure Cosmos DB можно создать до 25 односекционных коллекций или одну секционированную коллекцию. Изменив значение **PartitionCount**, можно создать до 250 односекционных или 10 секционированных коллекций. А также можно комбинировать оба типа коллекций, при этом количество отдельных секций не должно превышать 250 (из расчета, что 1 секционированная коллекция = 25 односекционных коллекций).

При попытке создать коллекцию сверх этих ограничений на количество секций эмулятор порождает исключение ServiceUnavailable со следующим сообщением:

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

Чтобы изменить число доступных для эмулятора Azure Cosmos DB коллекций, сделайте следующее.

1. Удалите все локальные данные эмулятора Azure Cosmos DB, щелкнув правой кнопкой мыши значок **эмулятора Azure Cosmos DB** в области уведомлений и выбрав **Сброс данных**.
2. Удалите все данные эмулятора в этой папке: C:\Users\имя_пользователя\AppData\Local\CosmosDBEmulator.
3. Выйдите из всех открытых экземпляров, щелкнув правой кнопкой мыши значок **эмулятора Azure Cosmos DB** в области уведомлений и выбрав **Выход**. Выход из всех экземпляров может занять около минуты.
4. Установите последнюю версию [эмулятора Azure Cosmos DB](https://aka.ms/cosmosdb-emulator).
5. Запустите эмулятор с флагом PartitionCount, задав значение <= 250. Например, `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Устранение неполадок

Ниже перечислены способы устранения неполадок с эмулятором Azure Cosmos DB.

- Если установлена новая версия эмулятора и возникли ошибки, убедитесь, что вы сбросили данные. Вы можете сбросить данные, щелкнув правой кнопкой мыши значок эмулятора Azure Cosmos DB в области уведомлений и выбрав "Сбросить данные". Если ошибки не устранены, можно удалить и переустановить приложение. Инструкции см. в разделе [Удаление локального эмулятора](#uninstall).

- В случае аварийного завершения эмулятора Azure Cosmos DB соберите файлы дампа из папки c:\Users\user_name\AppData\Local\CrashDumps, сожмите их, вложите в электронное сообщение и отправьте по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- При возникновении сбоев в CosmosDB.StartupEntryPoint.exe выполните следующую команду из командной строки администратора: `lodctr /R` 

- Если возникли проблемы с подключением, [соберите файлы трассировки](#trace-files), сожмите их, вложите в электронное сообщение и отправьте по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- При получении сообщения **Служба недоступна** эмулятор может не инициализировать сетевой стек. Проверьте, установлен ли защищенный клиент Pulse или сетевой клиент Juniper, так как драйверы их сетевого фильтра могут вызвать проблему. Удаление драйверов сетевого фильтра сторонних производителей обычно устраняет проблему.

### <a id="trace-files"></a>Сбор файлов трассировки

Для сбора отладочных трассировок выполните следующие команды в командной строке с правами администратора.

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Проверьте область уведомлений, чтобы убедиться, что работа программы завершена, так как на это может потребоваться до минуты. Кроме того, можно просто щелкнуть **Выйти** в пользовательском интерфейсе эмулятора Azure Cosmos DB.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Воспроизведите проблему. Если обозреватель данных не работает, необходимо подождать несколько секунд, чтобы открылся браузер и ошибка возникла снова.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Перейдите к `%ProgramFiles%\Azure Cosmos DB Emulator` и найдите файл docdbemulator_000001.etl.
7. Отправьте ETL-файл и описание действий, которые привели к ошибке, на электронный адрес [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) для отладки.

### <a id="uninstall"></a>Удаление локального эмулятора

1. Выйдите из всех открытых экземпляров локального эмулятора, щелкнув правой кнопкой мыши значок эмулятора Azure Cosmos DB в области уведомлений и выбрав "Выход". Выход из всех экземпляров может занять около минуты.
2. Введите в поле поиска Windows **Приложения и возможности** и выберите команду **Apps & features (System settings)** (Приложения и возможности (системные параметры)).
3. В списке приложений перейдите к **эмулятору Azure Cosmos DB**, выберите его, щелкните **Удалить**, подтвердите и щелкните **Удалить** еще раз.
4. Удалив приложение, перейдите к папке C:\Users\<пользователя>\AppData\Local\CosmosDBEmulator и удалите ее. 

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы выполнили следующее:

> [!div class="checklist"]
> * установили локальный эмулятор;
> * запустили эмулятор в Docker для Windows;
> * выполнили аутентификацию запросов;
> * использовали обозреватель данных в эмуляторе;
> * экспортировали сертификаты SSL;
> * вызвали эмулятор из командной строки;
> * собрали файлы трассировки.

Из этого руководства вы также узнали, как использовать локальный эмулятор для бесплатной разработки в локальной среде. Теперь вы можете перейти к следующему руководству, из которого вы узнаете, как экспортировать сертификаты SSL эмулятора. 

> [!div class="nextstepaction"]
> [Экспорт сертификатов эмулятора Azure Cosmos DB для использования с Java, Python и Node.js](local-emulator-export-ssl-certificates.md)
