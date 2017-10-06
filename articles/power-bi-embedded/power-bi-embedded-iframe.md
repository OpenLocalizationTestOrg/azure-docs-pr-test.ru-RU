---
title: "Power BI Embedded с ОСТАЛЬНОЙ toouse aaaHow | Документы Microsoft"
description: "Узнайте, как toouse Power BI Embedded с REST "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a>Как toouse Power BI Embedded с REST

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded: что это такое и как это использовать

Общие сведения о Power BI Embedded описан в официальное hello [Power BI Embedded сайта](https://azure.microsoft.com/services/power-bi-embedded/), но давайте рассмотрим это быстрый, прежде чем мы перейдем hello сведения об использовании REST.

На самом деле все довольно просто. Вы можете toouse hello динамических данных визуализации [Power BI](https://powerbi.microsoft.com) в приложении.

Большинство пользовательских приложений требуется toodeliver hello данных для своих клиентов, не обязательно пользователей в их собственных организации. Например если какой-либо службой для компании A и B компании программным обеспечением, пользователи в организации A должны видеть только данные для своих собственных компании A. То есть hello многопользовательский режим необходим для доставки hello.

пользовательское приложение Hello может также предложения свои собственные методы проверки подлинности, например форм проверки подлинности, обычная проверка подлинности и т.д... Затем hello внедрения решения необходимо работать совместно с этого существующие методы проверки подлинности безопасно. Это также может потребоваться для пользователей toobe может toouse hello этих приложений независимых поставщиков программного обеспечения, без дополнительных покупки или лицензирования подписки Power BI.

 Служба **Power BI Embedded** разработана именно для такого рода сценариев. Таким образом теперь, когда у нас есть, краткие сведения за пределы hello способом, давайте получить некоторые сведения о

Можно использовать hello .NET \(C#) или Node.js SDK tooeasily построить приложение с Power BI Embedded. Но в этой статье мы рассмотрим, как создать поток HTTP \(включая AuthN) Power BI без использования пакетов SDK. Основные сведения об этой процедуре, можно построить приложение **с любым языком программирования**, и можно понять, глубоко hello суть Power BI Embedded.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Создание коллекции рабочих областей Power BI и получение ключа доступа \(подготовка)

Power BI Embedded является одним из hello служб Azure. Для использования сборов взимается только hello ISV, который использует портал Azure \(за каждый час сеанс пользователя), и пользователь hello, представления отчетов hello не сняты или даже требуется подписка Azure.
Перед началом нашей разработкой приложения, необходимо создать hello **коллекции рабочей области Power BI** с помощью портала Azure.

Каждой рабочей области Power BI Embedded является hello рабочей области для каждого клиента (клиента), и в каждой коллекции в рабочей области можно добавить несколько рабочих областей. Здравствуйте, ключ доступа используется в каждой коллекции в рабочей области. В силу коллекции hello рабочей области является границей безопасности hello для Power BI Embedded.

![](media/power-bi-embedded-iframe/create-workspace.png)

После завершения создания коллекции hello рабочей области, скопируйте ключ доступа hello с портала Azure.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> Мы также подготовить коллекцию hello рабочей области и получить ключ доступа через REST API. toolearn более, в разделе [API-интерфейсы поставщика ресурса Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Создание PBIX-файла с помощью Power BI Desktop

Далее необходимо создать подключение к данным hello и внедренных toobe отчеты.
Эта задача не выполняется программно или с помощью кода. Мы просто воспользуемся Power BI Desktop.
В этой статье мы не будем останавливаться hello сведений о том, как toouse Power BI Desktop. Дополнительные сведения по этому вопросу см. в руководстве [Начало работы с Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). В нашем примере мы просто используем hello [анализ розничной торговли](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Создание рабочей области Power BI

Теперь, когда подготовка hello действия выполняются, давайте приступить к созданию рабочей области клиента в коллекции рабочей hello через интерфейсы API REST. Hello следующие HTTP POST запроса (REST) является создание новой рабочей области hello в существующей коллекции рабочей области. Это hello [POST рабочую область API](https://msdn.microsoft.com/library/azure/mt711503.aspx). В нашем примере является имя коллекции hello рабочей **mypbiapp**. Мы просто установите ключ доступа hello, который мы ранее скопировано, как **AppKey**. Это очень простая аутентификация!

**HTTP-запрос**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**HTTP-ответ**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

Возвращаемый Hello **ИД рабочей области** используется для hello, следуя последующие вызовы API. Это значение должно сохраниться в нашем приложении.

## <a name="import-pbix-file-into-hello-workspace"></a>Импортировать pbix-файла в рабочей области hello

Каждый отчет в рабочей области соответствует tooa один файл Power BI Desktop с набором данных \(включая параметры источника данных). Мы можем импортировать нашей .pbix файл toohello рабочей области, как показано в следующем примере кода hello. Как видите, могут загружаться hello двоичное pbix-файла с помощью составного сообщения MIME в http.

фрагмент uri Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** hello ИД рабочей области, а параметр запроса **datasetDisplayName** — toocreate имя набора данных hello. Hello создан набор данных содержит все данные, связанные hello артефактов в pbix-файл как импортированные данные источника данных toohello указатель, и т. д.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

Выполнение этой задачи импорта может занять некоторое время. По завершении наше приложение может потребовать от состояния задачи hello, с помощью идентификатора импорта. В нашем примере — идентификатор hello импорта **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

запрашивает состояние с помощью этого идентификатора импорта Hello следующие:

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Если задачу hello еще не завершен, hello HTTP-ответа можно следующим образом:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

Если задачу hello завершена, hello HTTP-ответа может быть несколько следующим образом:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>Подключение к источнику данных \(и мультитенантность данных)

Почти все артефакты hello в pbix-файла импортируются в нашей рабочей области, hello учетные данные для источников данных, но не являются. Таким образом, при использовании **режим DirectQuery**, hello внедренный отчет, не может отображаться неправильно. Однако при использовании **режим импорта**, можно просмотреть отчет hello, используя существующие импортированные данные hello. В этом случае нам необходимо задать учетные данные hello, используя следующие шаги через вызовы REST hello.

Во-первых мы должны получить источника данных шлюза hello. Мы знаем, что набор данных hello **идентификатор** hello ранее возвращается идентификатор.

**HTTP-запрос**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**HTTP-ответ**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

С помощью hello возвращается идентификатор шлюза и идентификатор источника данных \(см. предыдущие hello **gatewayId** и **идентификатор** в hello вернул результат), hello учетные данные для этого источника данных можно изменить следующим образом:

**HTTP-запрос**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**HTTP-ответ**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

В рабочей среде можно также задать hello отдельную строку подключения для каждой рабочей области, с помощью API-интерфейса REST. \(т. е., можно разделить hello базы данных для каждого из клиентов.)

следующие Hello изменяется hello строка подключения источника данных через интерфейс REST.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

Или можно использовать безопасность на уровне строк в Power BI Embedded, и мы можно разделить данные hello для каждого пользователя в одном отчете. В результате мы можем подготовить отчет для каждого клиента, используя один PBIX-файл \(который описывает пользовательский интерфейс и т. д.) и разные источники данных.

> [!NOTE]
> Если вы используете **режим импорта** вместо **режим DirectQuery**, нет ни одной модели toorefresh способом через API-Интерфейс. Локальные источники данных через шлюз Power BI пока поддерживаются в Power BI Embedded. Тем не менее, будет действительно необходимо следить за hello tookeep [блоге по Power BI](https://powerbi.microsoft.com/blog/) новые возможности и предстоящие в будущих выпусках.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Аутентификация и размещение (внедрение) отчетов на веб-странице

В Здравствуйте предыдущих API REST, можно использовать клавиши доступа hello **AppKey** себя в качестве заголовка авторизации hello. Поскольку эти вызовы могут обрабатываться на стороне сервера hello серверной части, безопасно.

Но когда мы внедрить отчет hello в наш веб-страницы, подобные сведения безопасности будет обрабатываться с помощью JavaScript \(переднего плана). Затем значение заголовка авторизации hello должен быть защищен. Если наш ключ доступа будет обнаружен пользователем-злоумышленником или вредоносным кодом, то злоумышленник сможет вызывать любые операции с помощью этого ключа.

Когда мы внедрение отчета hello наш веб-страницу, необходимо использовать вычисляемый токен hello вместо ключ доступа **AppKey**. Нашего приложения необходимо создать hello OAuth Json Web Token \(JWT) который состоит из утверждений hello и hello вычисленная цифровая подпись. Как показано ниже, OAuth JWT — это маркер закодированной строки с разделителями-точками.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

Во-первых мы необходимо подготовить hello входное значение, которое входит в более поздней версии. Это значение является строку в кодировке URL-адреса (rfc4648) base64 hello hello, следуя json, и они разделяются точкой hello \(.) символов. Позже вы узнаете, как tooget hello идентификатор отчета.

> [!NOTE]
> Если мы хотим toouse безопасности уровня строк (RLS) с Power BI Embedded, мы также необходимо указать **username** и **роли** в утверждениях hello.

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

Далее необходимо создать строку в кодировке base64 hello объекта HMAC \(hello подписи) с помощью алгоритма SHA256. Входное значение со знаком — предыдущую строку hello.

И, наконец, мы необходимо объединить hello входного значения и строки подписи с помощью период \(.) символов. Строка Hello завершено — маркер приложения hello для внедрения отчета hello. Даже если токен приложения hello обнаружен злонамеренным пользователем, они не удается получить hello исходного ключа доступа. Срок действия этого маркера приложения быстро закончится.

Ниже приведен пример PHP для описанных шагов.

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a>Наконец внедрение отчета hello в веб-страницу приветствия

Для внедрения отчета, мы получаем hello внедрить URL-адрес и отчетов **идентификатор** с помощью следующих API-интерфейса REST hello.

**HTTP-запрос**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**HTTP-ответ**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

В наших веб-приложения с помощью предыдущего маркера приложения hello, можно внедрять hello отчета.
Если мы рассмотрим следующий пример кода hello hello бывшая части hello такой же, как в предыдущем примере hello. В последней части hello, в этом примере показано hello **embedUrl** \(см. предыдущий результат hello) в hello iframe и учитываются в hello iframe токен приложения hello.

> [!NOTE]
> Вам потребуется tooone toochange hello отчета идентификатор значение свой собственный. Кроме того из-за ошибки tooa в нашей системе управления содержимым, тег iframe hello в образце кода hello считывается буквально. Удалите из тега hello текста hello сокращаться, если скопируйте и вставьте этот образец кода.

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

А вот и наш результат:

![](media/power-bi-embedded-iframe/view-report.png)

В настоящее время Power BI Embedded отображаются только hello отчета в hello iframe. Но Обратите внимание на hello [блоге по Power BI](https://powerbi.microsoft.com/blog/). Использовать нового клиентского API, которые будут сообщите нам отправлять сведения в hello iframe, а также получить сведения будущих улучшений. Восхитительные функции!

## <a name="see-also"></a>Дополнительные материалы
* [Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md)

У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)

