---
title: "Пользовательский домен aaaAdd и SSL tooan Azure веб-приложения | Документы Microsoft"
description: "Узнайте, как tooprepare Azure веб-приложения toogo производства, добавив символике вашей организации. Сопоставьте hello имя личного домена (именного домена) tooyour веб-приложения и защитить ее с SSL-сертификат."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>Добавление пользовательского домена и SSL tooan веб-приложение Azure

Этот учебник показывает, как tooquickly сопоставления Azure веб-приложении tooyour имя пользовательского домена и затем обеспечивать защиту с SSL-сертификат. 

## <a name="before-you-begin"></a>Перед началом работы

Перед запуском этого образца установите hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) локально.

Необходимо также странице конфигурации DNS toohello административного доступа для поставщика соответствующего домена. Например, tooadd `www.contoso.com`, вам нужно записей DNS может tooconfigure toobe для `contoso.com`.

Наконец вы должны является допустимым. PFX-файла _и_ ее пароль для SSL-сертификата hello требуется tooupload и привязку. SSL-сертификата должно быть настроенный toosecure hello пользовательских доменов нужное имя. В приведенном выше примере hello, следует разделить SSL-сертификат `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Шаг 1. Создание веб-приложения Azure

### <a name="log-in-tooazure"></a>Войдите в tooAzure

Приносим теперь будет toouse hello Azure CLI 2.0 в ресурсах hello toocreate окно терминала необходимости toohost нашего приложения Node.js в Azure.  Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Создание группы ресурсов   
Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create). Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание ресурсов Azure (веб-приложений, баз данных и учетных записей хранения) и управление ими. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee какие возможные значения следует использовать для `---location`, использовать hello `az appservice list-locations` команду Azure CLI.

## <a name="create-an-app-service-plan"></a>Создание плана службы приложений

Создать план служб приложений с hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команды. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello следующий пример создает план службы приложений с именем `myAppServicePlan` с помощью hello **основные** ценовой категории.

az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1

При создании плана служб приложений hello hello Azure CLI показано toohello аналогичные сведения, следующий пример. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>Создание веб-приложения

После создания план служб приложений для создания веб-приложения в рамках hello `myAppServicePlan` план служб приложений. Предоставляет приложение Hello веб вы являетесь размещения toodeploy места кода, а также предоставляет URL-адрес для вас tooview hello развернутого приложения. Используйте hello [создать az appservice web](/cli/azure/appservice/web#create) команда toocreate hello веб-приложения. 

В следующую команду hello, следует заменить собственное имя уникальным приложения, где вы видите hello `<app_name>` заполнителя. Это уникальное имя будет использоваться как часть hello hello имя домена по умолчанию для веб-приложения hello, поэтому hello имя должно toobe уникальным для всех приложений в Azure. Позже можно сопоставить любые пользовательские DNS запись toohello веб-приложения перед его предоставления tooyour пользователей. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

При создании веб-приложения hello hello Azure CLI показано toohello аналогичные сведения, следующий пример. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

Из выходных данных JSON, hello `defaultHostName` содержит имя домена по умолчанию веб-приложения. В браузере перейдите toothis адрес.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Шаг 2. Настройка сопоставления DNS

На этом шаге от доменного имени пользовательского домена tooyour веб-приложения по умолчанию, добавьте сопоставление `<app_name>.azurewebsites.net`. Обычно этот шаг выполняется на веб-сайте вашего поставщика домена. Каждый веб-сайт регистратора доменов несколько отличается, поэтому вам следует обратиться к документации вашего поставщика. Ниже приведены некоторые общие рекомендации. 

### <a name="navigate-tootoodns-management-page"></a>Перейдите на страницу управления tootooDNS

Во-первых Войдите на веб-сайте регистратора домена tooyour.  

Найдите страницу приветствия для управления записями DNS. Найдите ссылки или областей с меткой узла hello **доменное имя**, **DNS**, или **управление сервером имен**. Часто можно найти ссылку hello просматривая данные учетной записи и Отыскав ссылку например **Мои домены**.

Когда вы найдете эту страницу, найдите ссылку, которая позволяет добавлять или изменять записи DNS. Это может быть ссылка **Файл зоны**, **Записи DNS** или **Расширенная конфигурация**.

### <a name="create-a-cname-record"></a>Создание записи CNAME

Добавьте запись CNAME, которая сопоставляет имя домена по умолчанию hello поддомен нужное имя tooyour веб-приложения (`<app_name>.azurewebsites.net`, где `<app_name>` — уникальное имя приложения).

Для hello `www.contoso.com` пример, создайте запись CNAME, которая сопоставляет hello `www` hostname слишком`<app_name>.azurewebsites.net`.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>Шаг 3 — Настройка hello настраиваемого домена на веб-приложения

После завершения настройки hello сопоставления имени узла в веб-сайта поставщика доменов, вы готовы tooconfigure hello настраиваемого домена на веб-приложения. Используйте hello [добавьте az appservice web config hostname](/cli/azure/appservice/web/config/hostname#add) команды tooadd этой конфигурации. 

В следующей команде hello, замените `<app_name>` — имя уникальным приложения, а < your_custom_domain > с hello полное доменное имя (например `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

Пользовательский домен Hello теперь является полностью сопоставленных tooyour веб-приложения. В браузере перейдите toohello пользовательское имя домена. Например:

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>Шаг 4. Привязка пользовательского приложения web tooyour сертификат SSL

Теперь у вас есть веб-приложение Azure, с доменным именем hello в адресной строке браузера hello. Тем не менее если вы перейдете toohello `https://<your_custom_domain>` теперь получить сообщение об ошибке сертификата. 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Эта ошибка возникает потому, что веб-приложение еще не имеет привязки сертификата SSL, соответствующей имени личного домена. Тем не менее, не возникает сообщение об ошибке при переходе слишком`https://<app_name>.azurewebsites.net`. Это так, как приложения, а также все приложения службы приложений Azure, защищенный с помощью hello SSL-сертификат для hello `*.azurewebsites.net` подстановочный домен по умолчанию. 

Упорядочить tooaccess веб-приложения по пользовательское имя домена, необходимо toobind hello SSL-сертификат для веб-приложения toohello пользовательского домена. что мы и сделаем на этом шаге. 

### <a name="upload-hello-ssl-certificate"></a>Отправка сертификата SSL hello

Отправьте hello SSL-сертификат для пользовательского домена tooyour веб-приложения с помощью hello [az appservice web config ssl передачи](/cli/azure/appservice/web/config/ssl#upload) команды.

В следующей команде hello, замените `<app_name>` приложения уникальным именем `<path_to_ptx_file>` с tooyour путь hello. PFX-файла и `<password>` с паролем свой сертификат. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

При отправке сертификата hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

Из выходных данных JSON, hello `thumbprint` показывает отпечаток загруженного сертификата. Скопируйте его значение для следующего шага hello.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>Привязать hello отправлен SSL сертификат toohello веб-приложения

Веб-приложение теперь имеет имя пользовательского домена hello и также имеет SSL-сертификат, который защищает этого пользовательского домена. Hello toodo самое левой — toobind hello отправленный сертификат toohello веб-приложения. Это делается с помощью hello [привязки ssl конфигурации web appservice az](/cli/azure/appservice/web/config/ssl#bind) команды.

В следующей команде hello, замените `<app_name>` с вашим именем уникальные приложения и `<thumbprint-from-previous-output>` с отпечатком сертификата hello, получаемые из предыдущей команды hello. 

az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI

Когда сертификат hello привязанного tooyour веб-приложения, hello Azure CLI показано toohello аналогичные сведения, следующий пример:

{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }

В браузере перейдите на конечную точку tooHTTPS пользовательское имя домена. Например:

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Дополнительные ресурсы

[Приобретение и настройка имени личного домена для службы приложений Azure](custom-dns-web-site-buydomains-web-app.md)
[Приобретение и настройка сертификата SSL для службы приложений Azure](web-sites-purchase-ssl-web-site.md)
