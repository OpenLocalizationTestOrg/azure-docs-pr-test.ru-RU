---
title: "aaaQuickly развернуть существующий кластер Azure Service Fabric tooan приложения"
description: "Использование Azure Service Fabric кластера toohost существующего приложения Node.js в Visual Studio."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Размещение приложения Node.js в Azure Service Fabric

Это краткое руководство поможет вам развернуть кластер Service Fabric существующего приложения (Node.js в этом примере) tooa работает в Azure.

## <a name="prerequisites"></a>Предварительные требования

Перед началом работы [настройте среду разработки](service-fabric-get-started.md). В том числе установка hello Service Fabric SDK и Visual Studio 2017 г. или 2015 г.

Необходимо также toohave существующее приложение Node.js для развертывания. В этом кратком руководстве используется простой веб-сайт Node.js, который можно загрузить [здесь][download-sample]. Извлечь этот файл tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` папку после создания проекта hello в следующем шаге hello.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure][create-account].

## <a name="create-hello-service"></a>Создать службу hello

Запустите Visual Studio от имени **администратора**.

Создайте проект, нажав клавиши `CTRL`+`SHIFT`+`N`.

В hello **новый проект** диалоговое окно, выберите **облака > приложение Service Fabric**.

Имя приложения hello **MyGuestApp** и нажмите клавишу **ОК**.

>[!IMPORTANT]
>Node.js легко может нарушить работу 260 знаков hello для путей, которые имеет windows. Использовать короткий путь для самого hello проекта, такие как **c:\code\svc1**.
   
![Диалоговое окно "Новый проект" в Visual Studio][new-project]

В следующем диалоговом окне приветствия, можно создать любой тип службы Service Fabric. В рамках этого краткого руководства выберите **Гостевой исполняемый файл**.

Имя службы hello **MyGuestService** и задание параметров hello на правом toohello hello следующие значения:

| Настройка                   | Значение |
| ------------------------- | ------ |
| Папка пакета кода       | _&lt;Папка Hello приложение Node.js&gt;_ |
| Поведение пакета кода     | Скопируйте папку tooproject содержимое |
| Программа                   | node.exe |
| Аргументы                 | server.js |
| Рабочая папка            | CodePackage |

Нажмите кнопку **ОК**.

![Диалоговое окно "Новая служба" в Visual Studio][new-service]

Visual Studio создает проект приложения hello и проект службы субъекта hello и отображает их в обозревателе решений.

проект приложения Hello (**MyGuestApp**) содержит код напрямую. Он только ссылается на набор проектов служб. Также он содержит данные еще трех типов.

* **Профили публикации**  
Средства настройки для различных сред.

* **Сценарии**  
Сценарий PowerShell для развертывания и обновления приложения.

* **Определение приложения**  
Включает в себя манифест приложения hello под *ApplicationPackageRoot*. Файлы параметров связанного приложения находятся в *ApplicationParameters*, который определении приложения hello и позволяют tooconfigure он специально для данной среды.
    
Общие сведения о hello содержимое проекта службы hello. в разделе [Приступая к работе с надежного обмена](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Настройка сети

пример Hello, мы развертываете приложение Node.js использует порт **80** нам нужны tootell Service Fabric, нам нужно, что порт доступ.

Откройте hello **ServiceManifest.xml** файл в проекте hello. Внизу hello hello манифеста — `<Resources> \ <Endpoints>` с записью уже определен. Изменение этой записи tooadd `Port`, `Protocol`, и `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>Развертывание tooAzure

Если нажать клавишу **F5** и запустите проект hello, развернутых toohello локального кластера. Тем не менее давайте развернуть tooAzure вместо него.

Правой кнопкой мыши проект hello и выберите **публикации...**  . Откроется диалоговое окно toopublish tooAzure.

![Диалоговое окно tooazure для служба service fabric публикации][publish]

Выберите hello **PublishProfiles\Cloud.xml** целевой профиль.

Если вы еще не ранее, выберите toodeploy учетная запись Azure для. Если у вас ее нет, [зарегистрируйте ее][create-account].

В разделе **конечной точки подключения**, выберите hello toodeploy кластера Service Fabric для. Если нет, выберите  **&lt;создать новый кластер... &gt;**  которого открывается toohello окна браузера web портал Azure. Дополнительные сведения см. в разделе [создания кластера в портале hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

При создании кластера Service Fabric hello, убедитесь, что hello tooset **пользовательские конечные точки** задание слишком**80**.

![Конфигурация типа узла Service Fabric с настраиваемой конечной точкой][custom-endpoint]

Создание нового кластера Service Fabric занимает некоторое время toocomplete. Если он был создан, перейдите назад toohello диалоговое окно публикации и выберите  **&lt;обновление&gt;**. Hello нового кластера, перечисленные в поле со списком hello; выберите его.

Нажмите клавишу **публикации** и дождитесь toofinish развертывания hello.

Это может занять несколько минут. После его завершения может потребоваться несколько минут для toobe приложения hello полностью доступны.

## <a name="test-hello-website"></a>Веб-сайт для тестирования hello

После публикации службы проверьте ее в веб-браузере. 

Во-первых откройте hello портал Azure и найти службу Service Fabric.

Проверьте колонке Обзор hello hello адреса службы. Используйте hello доменное имя от hello _конечной точки подключения клиента_ свойство. Например, `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Колонка Общие сведения о Service fabric на hello портал Azure][overview]

Перейдите toothis адрес, где можно будет увидеть hello `HELLO WORLD` ответа.

## <a name="delete-hello-cluster"></a>Удалить кластер hello

Не забудьте toodelete все ресурсы hello, созданный для краткого руководства, что и у вас взимается для этих ресурсов.

## <a name="next-steps"></a>Дальнейшие действия
Ознакомьтесь с дополнительными сведениями о [гостевых исполняемых файлах](service-fabric-deploy-existing-app.md).

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F