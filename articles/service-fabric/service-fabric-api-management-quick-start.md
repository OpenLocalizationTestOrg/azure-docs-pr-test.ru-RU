---
title: "aaaAzure Service Fabric с помощью быстрого запуска управления API | Документы Microsoft"
description: "В этом руководстве показано, как tooquickly Приступая к работе с API управления Azure и фабрикой служб."
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
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Краткое руководство по Service Fabric со службой управления API Azure

В этом руководстве рассказывается, как tooset управления API Azure в Service Fabric и настройка служб трафика tooback окончания первого API операции toosend в Service Fabric. toolearn Дополнительные сведения о сценариях управления API Azure в Service Fabric. в разделе hello [Обзор](service-fabric-api-management-overview.md) статьи. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>Развертывание tooAzure управления API и Service Fabric

Hello первым шагом является toodeploy управления API и tooAzure кластера Service Fabric в общей виртуальной сети. Это позволяет toocommunicate API управления непосредственно в Service Fabric, можно выполнить обнаружение службы, разрешения раздела службы и перенаправлял трафик, напрямую tooany серверной службы в Service Fabric.

### <a name="topology"></a>Топология

В этом руководстве развертывает следующие hello tooAzure топологии, в которой API управления и структуры службы находятся в подсетях hello одной виртуальной сети:

 ![Рисунок][sf-apim-topology-overview]

tooget быстро начать работу, диспетчер ресурсов предоставляются шаблоны для каждого из шагов развертывания:

 - Топология сети:
    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]
 - Кластер Service Fabric:
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]
 - Управление API
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>Войдите в tooAzure и выберите свою подписку

В этом руководстве используется [Azure PowerShell][azure-powershell]. При запуске нового сеанса PowerShell, войдите в tooyour учетная запись Azure и выберите подписку, перед выполнением команды Azure.
 
Войдите в tooyour учетная запись Azure.

```powershell
PS > Login-AzureRmAccount
```

Выберите свою подписку.

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>Создание группы ресурсов

Создайте новую группу ресурсов для развертывания. Назначьте ей имя и расположение.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Развертывание hello топологии сети

Hello первый шаг — tooset копирование toowhich топологии сети hello API управления и кластера Service Fabric hello будет развертываться. Hello [network.json] [ network-arm] шаблона диспетчера ресурсов является настроенным toocreate виртуальной сети (VNET) с двумя подсетями и две группы безопасности сети (NSG). 

Hello [network.parameters.json] [ network-parameters-arm] файл параметров содержит hello имена подсетей hello и Nsg, которые будут развернуты для управления API и Service Fabric. В этом руководстве hello значения параметров не обязательно toobe изменен. шаблоны управления API и диспетчер ресурсов структуры службы Hello использовать эти значения, если они изменяются здесь, необходимо изменить их в другие шаблоны диспетчера ресурсов hello соответствующим образом. 

 1. Загрузите следующий файл шаблона и параметров диспетчера ресурсов hello:

    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]

 2. Используйте следующие PowerShell команды toodeploy hello диспетчера ресурсов файлы шаблонов и параметров для настройки сети hello hello.

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Развертывание кластера Service Fabric hello

После hello сетевым ресурсам завершено развертывание, hello следующим шагом является toodeploy toohello кластера Service Fabric виртуальной сети в подсеть hello и NSG предназначенные для кластера Service Fabric hello. В этом учебнике шаблона диспетчера ресурсов структуры службы hello — имена hello предварительно настроенных toouse hello виртуальной сети, подсети и NSG, которая настраивается в предыдущем шаге hello. 

шаблона диспетчера ресурсов кластера Service Fabric Hello является настроенным toocreate безопасного кластера сертификат безопасности. Hello сертификат является используется toosecure связи для узлов для кластера и кластера Service Fabric tooyour доступа пользователя toomanage. API управления использует этот сертификат tooaccess hello служба именования Service Fabric для обнаружения службы.

Этот шаг требует наличия сертификата в Key Vault для обеспечения безопасности кластера. Дополнительные сведения о настройке безопасного кластера с помощью Key Vault см. в статье [Создание кластера Service Fabric в Azure с помощью Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

> [!NOTE]
> Проверка подлинности Azure Active Directory можно добавить в дополнение toohello сертификат, используемый для доступа к кластеру. Azure Active Directory рекомендуется кластера Service Fabric tooyour доступа пользователя способом toomanage hello, но не обязательно toocomplete этого учебника. Сертификат является обязательным для обеспечения безопасности кластера при обмене данными между узлами, а также для аутентификации службы управления API Azure, которая в настоящее время не поддерживает аутентификацию с помощью Azure Active Directory для серверной части Service Fabric.

 1. Загрузите следующий файл шаблона и параметров диспетчера ресурсов hello:
 
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]

 2. Заполните пустые параметры hello в hello `cluster.parameters.json` файл для развертывания, включая hello [сведения о хранилище ключей](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) сертификата кластера.

 3. Используйте следующие PowerShell команды toodeploy hello диспетчера ресурсов шаблонов и параметров файлы toocreate hello кластера Service Fabric hello.

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>Развертывание управления API

Наконец можно разверните toohello API управления виртуальной сети в подсеть hello и NSG, предназначенные для управления API. Необязательно toowait для toofinish развертывания кластера Service Fabric hello перед развертыванием управления API. 

В этом учебнике шаблона диспетчера ресурсов для управления API hello — имена hello предварительно настроенных toouse hello виртуальной сети, подсети и NSG, которая настраивается в предыдущем шаге hello. 

 1. Загрузите следующий файл шаблона и параметров диспетчера ресурсов hello:
 
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

 2. Заполните пустые параметры hello в hello `apim.parameters.json` для развертывания.

 3. Используйте следующие PowerShell команды toodeploy hello диспетчера ресурсов файлы шаблонов и параметров для управления API hello.

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>Настройка управления API

После развертывания кластера Service Fabric и управления API можно настроить серверную часть Service Fabric в службе управления API. Это позволяет toocreate политику серверной службы, которая отправляет трафик кластера Service Fabric tooyour.

### <a name="api-management-security"></a>Безопасность управления API

tooconfigure hello Service Fabric серверной части, необходимо сначала tooconfigure параметры безопасности управления API. параметры безопасности tooconfigure, перейдите tooyour API службы управления в hello портал Azure.

#### <a name="enable-hello-api-management-rest-api"></a>Включить hello API REST управления API

Hello API REST управления API в настоящий момент hello единственным способом tooconfigure серверной службы. Первым шагом Hello — tooenable hello API REST управления API и защитить ее.

 1. В hello службы управления API, выберите **API управления - PREVIEW** под **безопасности**.
 2. Проверьте hello **включить API REST управления** флажок.
 3. Обратите внимание, hello URL-адрес API управления — hello URL-адрес, мы будем использовать более поздней версии tooset копирование серверной hello Service Fabric
 4. Создание **маркер доступа** , выбрав дату окончания действия и ключ, нажмите кнопку hello **формирования** кнопку нижней hello страницы приветствия.
 5. Копировать hello **маркер доступа** и сохранить его — мы будем использовать в hello следующие шаги. Обратите внимание, что это отличается от hello первичного и вторичного ключа.

#### <a name="upload-a-service-fabric-client-certificate"></a>Отправка клиентского сертификата Service Fabric

API управления должны пройти проверку подлинности с кластером Service Fabric для обнаружения службы с помощью сертификат клиента, который имеет доступ tooyour кластера. Для простоты в этом учебнике используется hello один сертификат, указанный при создании кластера Service Fabric hello, который по умолчанию можно использовать tooaccess кластера.

 1. В hello службы управления API, выберите **сертификаты клиента — Предварительный просмотр** под **безопасности**.
 2. Нажмите кнопку hello **+ добавить** кнопки
 2. Выберите hello файл закрытого ключа (PFX-файл) сертификата hello кластера, указанный при создании кластера Service Fabric, присвойте ему имя и укажите пароль закрытого ключа hello.

> [!NOTE]
> В этом учебнике используется hello же сертификат безопасности клиента проверки подлинности и кластера узла на узел. Может использовать сертификат отдельного клиента, при наличии одного настроенного tooaccess кластера Service Fabric.

### <a name="configure-hello-backend"></a>Настройка внутреннего hello

Теперь, когда настройки параметров безопасности для управления API можно настроить внутренний Service Fabric hello. Для серверных системах Service Fabric hello кластера Service Fabric — hello серверной части, а не конкретной службы Service Fabric. Это позволяет toomore tooroute отдельную политику больше одной службы в кластере hello.

Этот шаг требуется hello маркер доступа, который был создан ранее и hello отпечаток сертификата кластера отправленный tooAPI управления на предыдущем шаге hello.

> [!NOTE]
> Если используется отдельный клиентский сертификат на предыдущем шаге hello для управления API, необходимо hello отпечаток сертификата клиента hello отпечаток сертификата сложения toohello кластера на этом шаге.

Отправьте следующие toohello запрос HTTP PUT API управления URL-адрес API записанные ранее при включении hello API REST управления tooconfigure hello Service Fabric серверную службу hello. Вы увидите `HTTP 201 Created` ответ после успешного завершения команды hello. Дополнительные сведения о каждом поле см. в разделе hello API управления [справочной документации по API внутреннего сервера](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).

Команда HTTP и URL-адрес:
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

Заголовки запроса:
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

Тело запроса:
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

Hello **URL-адрес** здесь является полное службы имя службы в кластере, все запросы направлено tooby по умолчанию, если имя службы не указано в политике серверной части. Может использовать имя фиктивное службы, такие как «fabric: / фиктивное/служба», если не требуется делать toohave резервной службы.

Ссылки toohello API управления [справочной документации по API внутреннего сервера](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) Дополнительные сведения о каждом поле.

#### <a name="example"></a>Пример

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Развертывание внутренней службы Service Fabric

Теперь, когда Service Fabric настроен в качестве серверной части tooAPI управления приветствия, можно создавать политики серверной части для собственные интерфейсы API, отправлять трафик tooyour служб Service Fabric. Но сначала необходимо к службе, запущенной в запросах tooaccept Service Fabric.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>Создание службы Service Fabric с конечной точкой HTTP

В этом учебнике мы создадим базовую без сохранения состояния ASP.NET Core надежного службу с помощью шаблона проекта веб-API по умолчанию hello. Так мы получим конечную точку HTTP для службы, которую можно будет использовать через службу управления API Azure:

```
/api/values
```

Ознакомьтесь с разделом о [настройке среды разработки для разработки ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).

После настройки среды разработки запустите Visual Studio от имени администратора и создайте службу ASP.NET Core:

 1. В Visual Studio выберите последовательно «Файл» -> «Создать проект».
 2. Выберите шаблон службы структуры приложение hello в облаке и назовите его **«ApiApplication»**.
 3. Выберите шаблон службы ASP.NET Core hello и имя проекта hello **«WebApiService»**.
 4. Выберите шаблон проекта hello Web API ASP.NET Core 1.1.
 5. После создания проекта Привет открыть `PackageRoot\ServiceManifest.xml` и удалите hello `Port` атрибут из конфигурации ресурса hello конечной точки:
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    Это позволяет toospecify Service Fabric порт динамически из диапазона портов приложения hello, который мы открытые с ее помощью hello сетевой группы безопасности в шаблоне диспетчер ресурсов кластера hello, предоставляя tooit tooflow трафика управления API.
 
 6. Нажмите клавишу F5 в Visual Studio tooverify hello веб-API доступен локально. 

    Откройте обозреватель Service Fabric и детализацию tooa определенного экземпляра hello, ASP.NET Core toosee hello базовый адрес hello служба выполняет прослушивание. Добавить `/api/values` toohello базовый адрес и откройте его в браузере. При этом вызывается метод Get на hello ValuesController в шаблоне веб-API hello hello. Он возвращает ответ по умолчанию hello, предоставляемого шаблоном hello, массив JSON, который содержит две строки:

    ```json
    ["value1", "value2"]`
    ```

    Это конечная точка hello, который будет предоставлять через управление API в Azure.

 7. Наконец разверните кластер tooyour приложения hello в Azure. [С помощью Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), щелкните правой кнопкой мыши проект приложения hello и выберите **публикации**. Укажите конечную точку кластера (например, `mycluster.westus.cloudapp.azure.com:19000`) tooyour приложения hello toodeploy Service Fabric кластер в Azure.

В кластере Service Fabric в Azure должна запуститься служба ASP.NET Core без отслеживания состояния с именем `fabric:/ApiApplication/WebApiService`.

## <a name="create-an-api-operation"></a>Создание операции API

Теперь мы готовы toocreate операции в службе управления API, toocommunicate использование внешних клиентов с hello в кластер Service Fabric hello службы без отслеживания состояния ASP.NET Core.

 1. Войдите в портал Azure toohello и перейдите tooyour развертывания службы управления API.
 2. В колонке службы управления API hello выберите **API-интерфейсов - Предварительный просмотр**
 3. Добавить новый API, щелкнув hello **пустой API** поле и заполнив диалоговое окно «hello»:

     - **URL-адрес веб-службы**: для серверных систем Service Fabric это значение URL-адреса не используется. Здесь вы можете использовать любое значение. В рамках этого руководства используйте `http://servicefabric`.
     - **Имя**: укажите любое имя для API. В рамках этого руководства используйте `Service Fabric App`.
     - **Схема URL-адреса**: выберите HTTP, HTTPS или оба варианта. В рамках этого руководства используйте `both`.
     - **API URL Suffix** (Суффикс URL-адреса API): укажите суффикс для API. В рамках этого руководства используйте `myapp`.
 
 4. После создания hello API щелкните **+ добавить операцию** операции tooadd интерфейса API. Заполните значения hello:
    
     - **URL-адрес**: выберите `GET` и укажите URL-путь для hello API. В рамках этого руководства используйте `/api/values`.
     
       По умолчанию hello URL-пути, здесь указывается hello URL-адрес отправляется toohello серверная служба Service Fabric. Если вы используете hello же URL-пути здесь, в этом случае служба использует `/api/values`, затем hello операция работает без дальнейших изменений. Можно также указать URL-путь здесь, отличный от hello URL-адрес, используемый сервером службы Service Fabric в этом случае будут также toospecify необходимости измените путь в политике операцию позже.
     - **Отображаемое имя**: Введите любое имя для hello API. В рамках этого руководства используйте `Values`.

## <a name="configure-a-backend-policy"></a>Настройка внутренней политики

политика серверной Hello объединяет все данные. Это связано с которой выполняется настройка hello серверной службы toowhich запросы направляются Service Fabric. Можно применить эту операцию API tooany политики. Hello [Внутренняя конфигурация для Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) предоставляет hello следующий запрос маршрутизации элементов управления: 
 - Службы Выбор экземпляра путем указания имени экземпляра службы Service Fabric, либо жестко закодировано (например, `"fabric:/myapp/myservice"`) или создан из запроса hello HTTP (например, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Разрешение раздела путем создания ключа секции с помощью любой схемы секционирования Service Fabric.
 - Выбор реплики для служб с отслеживанием состояния.
 - Разрешение повторите условия, которые позволяют вам toospecify условиям hello повторно разрешить расположение службы и снова отправить запрос.

В этом учебнике создайте политику серверной маршруты напрямую запрашивает toohello ASP.NET Core службы без отслеживания состояния, развернутую ранее.

 1. Выберите и измените hello **входящих политики** для hello `Values` операции, щелкнув значок редактирования hello и затем выбрав **в представлении кода**.
 2. В редакторе кода hello политики, добавьте `set-backend-service` политики в разделе входящих политики, как показано ниже и нажмите кнопку hello **Сохранить** кнопки:
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

Полный набор атрибутов Service Fabric внутренней политики, см. в разделе toohello [документации внутреннего интерфейса API управления](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Добавьте hello API tooa продукта. 

Перед вызовом hello API, его необходимо добавить tooa продукта, где вы можете предоставить доступ toousers. 

 1. В hello службы управления API, выберите **продуктов - PREVIEW**.
 2. По умолчанию служба управления API предоставляет два продукта: фиксированный и без ограничений. Выберите продукт неограниченное hello.
 3. Выберите API-интерфейсы.
 4. Нажмите кнопку hello **+ добавить** кнопки.
 5. Выберите hello `Service Fabric App` API, созданные в предыдущих шагах hello и нажмите кнопку hello **выберите** кнопки.

### <a name="test-it"></a>Тестирование

Теперь можно попробовать передачу запроса tooyour внутренней службой в Service Fabric через API управления непосредственно из hello портал Azure.

 1. В hello службы управления API, выберите **API — Предварительная версия**.
 2. В hello `Service Fabric App` API, созданный на предыдущих шагах hello, выберите hello **тест** вкладки.
 3. Нажмите кнопку hello **отправки** toosend кнопку toohello внутреннего тестирования запроса службы.

## <a name="next-steps"></a>Дальнейшие действия

На этом этапе базовая установка службы управления API и Service Fabric завершена.

Для вашего tooget кластера Service Fabric, которую можно быстро настроить в этом учебнике используется обычный пользователь на основе сертификатов проверки подлинности. Расширенную аутентификацию пользователя для кластера Service Fabric лучше использовать с [аутентификацией Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication). 

Далее, [Создание и настройка расширенных параметров продукта в службе управления API Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare приложения для трафика в реальном мире.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
