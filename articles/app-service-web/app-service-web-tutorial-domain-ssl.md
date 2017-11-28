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
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="e58fe-104">Добавление пользовательского домена и SSL tooan веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="e58fe-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="e58fe-105">Этот учебник показывает, как tooquickly сопоставления Azure веб-приложении tooyour имя пользовательского домена и затем обеспечивать защиту с SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="e58fe-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="e58fe-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e58fe-106">Before you begin</span></span>

<span data-ttu-id="e58fe-107">Перед запуском этого образца установите hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) локально.</span><span class="sxs-lookup"><span data-stu-id="e58fe-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="e58fe-108">Необходимо также странице конфигурации DNS toohello административного доступа для поставщика соответствующего домена.</span><span class="sxs-lookup"><span data-stu-id="e58fe-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="e58fe-109">Например, tooadd `www.contoso.com`, вам нужно записей DNS может tooconfigure toobe для `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e58fe-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="e58fe-110">Наконец вы должны является допустимым. PFX-файла _и_ ее пароль для SSL-сертификата hello требуется tooupload и привязку.</span><span class="sxs-lookup"><span data-stu-id="e58fe-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="e58fe-111">SSL-сертификата должно быть настроенный toosecure hello пользовательских доменов нужное имя.</span><span class="sxs-lookup"><span data-stu-id="e58fe-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="e58fe-112">В приведенном выше примере hello, следует разделить SSL-сертификат `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e58fe-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="e58fe-113">Шаг 1. Создание веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="e58fe-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="e58fe-114">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="e58fe-114">Log in tooAzure</span></span>

<span data-ttu-id="e58fe-115">Приносим теперь будет toouse hello Azure CLI 2.0 в ресурсах hello toocreate окно терминала необходимости toohost нашего приложения Node.js в Azure.</span><span class="sxs-lookup"><span data-stu-id="e58fe-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="e58fe-116">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="e58fe-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="e58fe-117">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e58fe-117">Create a resource group</span></span>   
<span data-ttu-id="e58fe-118">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e58fe-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e58fe-119">Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание ресурсов Azure (веб-приложений, баз данных и учетных записей хранения) и управление ими.</span><span class="sxs-lookup"><span data-stu-id="e58fe-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="e58fe-120">toosee какие возможные значения следует использовать для `---location`, использовать hello `az appservice list-locations` команду Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e58fe-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="e58fe-121">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="e58fe-121">Create an App Service plan</span></span>

<span data-ttu-id="e58fe-122">Создать план служб приложений с hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e58fe-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="e58fe-123">Hello следующий пример создает план службы приложений с именем `myAppServicePlan` с помощью hello **основные** ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="e58fe-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="e58fe-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="e58fe-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="e58fe-125">При создании плана служб приложений hello hello Azure CLI показано toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="e58fe-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="e58fe-126">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e58fe-126">Create a web app</span></span>

<span data-ttu-id="e58fe-127">После создания план служб приложений для создания веб-приложения в рамках hello `myAppServicePlan` план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="e58fe-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="e58fe-128">Предоставляет приложение Hello веб вы являетесь размещения toodeploy места кода, а также предоставляет URL-адрес для вас tooview hello развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="e58fe-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="e58fe-129">Используйте hello [создать az appservice web](/cli/azure/appservice/web#create) команда toocreate hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e58fe-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="e58fe-130">В следующую команду hello, следует заменить собственное имя уникальным приложения, где вы видите hello `<app_name>` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="e58fe-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="e58fe-131">Это уникальное имя будет использоваться как часть hello hello имя домена по умолчанию для веб-приложения hello, поэтому hello имя должно toobe уникальным для всех приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="e58fe-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="e58fe-132">Позже можно сопоставить любые пользовательские DNS запись toohello веб-приложения перед его предоставления tooyour пользователей.</span><span class="sxs-lookup"><span data-stu-id="e58fe-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="e58fe-133">При создании веб-приложения hello hello Azure CLI показано toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="e58fe-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

<span data-ttu-id="e58fe-134">Из выходных данных JSON, hello `defaultHostName` содержит имя домена по умолчанию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e58fe-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="e58fe-135">В браузере перейдите toothis адрес.</span><span class="sxs-lookup"><span data-stu-id="e58fe-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="e58fe-137">Шаг 2. Настройка сопоставления DNS</span><span class="sxs-lookup"><span data-stu-id="e58fe-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="e58fe-138">На этом шаге от доменного имени пользовательского домена tooyour веб-приложения по умолчанию, добавьте сопоставление `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e58fe-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="e58fe-139">Обычно этот шаг выполняется на веб-сайте вашего поставщика домена.</span><span class="sxs-lookup"><span data-stu-id="e58fe-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="e58fe-140">Каждый веб-сайт регистратора доменов несколько отличается, поэтому вам следует обратиться к документации вашего поставщика.</span><span class="sxs-lookup"><span data-stu-id="e58fe-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="e58fe-141">Ниже приведены некоторые общие рекомендации.</span><span class="sxs-lookup"><span data-stu-id="e58fe-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="e58fe-142">Перейдите на страницу управления tootooDNS</span><span class="sxs-lookup"><span data-stu-id="e58fe-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="e58fe-143">Во-первых Войдите на веб-сайте регистратора домена tooyour.</span><span class="sxs-lookup"><span data-stu-id="e58fe-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="e58fe-144">Найдите страницу приветствия для управления записями DNS.</span><span class="sxs-lookup"><span data-stu-id="e58fe-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="e58fe-145">Найдите ссылки или областей с меткой узла hello **доменное имя**, **DNS**, или **управление сервером имен**.</span><span class="sxs-lookup"><span data-stu-id="e58fe-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="e58fe-146">Часто можно найти ссылку hello просматривая данные учетной записи и Отыскав ссылку например **Мои домены**.</span><span class="sxs-lookup"><span data-stu-id="e58fe-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="e58fe-147">Когда вы найдете эту страницу, найдите ссылку, которая позволяет добавлять или изменять записи DNS.</span><span class="sxs-lookup"><span data-stu-id="e58fe-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="e58fe-148">Это может быть ссылка **Файл зоны**, **Записи DNS** или **Расширенная конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="e58fe-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="e58fe-149">Создание записи CNAME</span><span class="sxs-lookup"><span data-stu-id="e58fe-149">Create a CNAME record</span></span>

<span data-ttu-id="e58fe-150">Добавьте запись CNAME, которая сопоставляет имя домена по умолчанию hello поддомен нужное имя tooyour веб-приложения (`<app_name>.azurewebsites.net`, где `<app_name>` — уникальное имя приложения).</span><span class="sxs-lookup"><span data-stu-id="e58fe-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="e58fe-151">Для hello `www.contoso.com` пример, создайте запись CNAME, которая сопоставляет hello `www` hostname слишком`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e58fe-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="e58fe-152">Шаг 3 — Настройка hello настраиваемого домена на веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e58fe-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="e58fe-153">После завершения настройки hello сопоставления имени узла в веб-сайта поставщика доменов, вы готовы tooconfigure hello настраиваемого домена на веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e58fe-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="e58fe-154">Используйте hello [добавьте az appservice web config hostname](/cli/azure/appservice/web/config/hostname#add) команды tooadd этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e58fe-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="e58fe-155">В следующей команде hello, замените `<app_name>` — имя уникальным приложения, а < your_custom_domain > с hello полное доменное имя (например `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="e58fe-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="e58fe-156">Пользовательский домен Hello теперь является полностью сопоставленных tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e58fe-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="e58fe-157">В браузере перейдите toohello пользовательское имя домена.</span><span class="sxs-lookup"><span data-stu-id="e58fe-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="e58fe-158">Например:</span><span class="sxs-lookup"><span data-stu-id="e58fe-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="e58fe-160">Шаг 4. Привязка пользовательского приложения web tooyour сертификат SSL</span><span class="sxs-lookup"><span data-stu-id="e58fe-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="e58fe-161">Теперь у вас есть веб-приложение Azure, с доменным именем hello в адресной строке браузера hello.</span><span class="sxs-lookup"><span data-stu-id="e58fe-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="e58fe-162">Тем не менее если вы перейдете toohello `https://<your_custom_domain>` теперь получить сообщение об ошибке сертификата.</span><span class="sxs-lookup"><span data-stu-id="e58fe-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="e58fe-164">Эта ошибка возникает потому, что веб-приложение еще не имеет привязки сертификата SSL, соответствующей имени личного домена.</span><span class="sxs-lookup"><span data-stu-id="e58fe-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="e58fe-165">Тем не менее, не возникает сообщение об ошибке при переходе слишком`https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e58fe-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="e58fe-166">Это так, как приложения, а также все приложения службы приложений Azure, защищенный с помощью hello SSL-сертификат для hello `*.azurewebsites.net` подстановочный домен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e58fe-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="e58fe-167">Упорядочить tooaccess веб-приложения по пользовательское имя домена, необходимо toobind hello SSL-сертификат для веб-приложения toohello пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="e58fe-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="e58fe-168">что мы и сделаем на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="e58fe-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="e58fe-169">Отправка сертификата SSL hello</span><span class="sxs-lookup"><span data-stu-id="e58fe-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="e58fe-170">Отправьте hello SSL-сертификат для пользовательского домена tooyour веб-приложения с помощью hello [az appservice web config ssl передачи](/cli/azure/appservice/web/config/ssl#upload) команды.</span><span class="sxs-lookup"><span data-stu-id="e58fe-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="e58fe-171">В следующей команде hello, замените `<app_name>` приложения уникальным именем `<path_to_ptx_file>` с tooyour путь hello. PFX-файла и `<password>` с паролем свой сертификат.</span><span class="sxs-lookup"><span data-stu-id="e58fe-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="e58fe-172">При отправке сертификата hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="e58fe-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="e58fe-173">Из выходных данных JSON, hello `thumbprint` показывает отпечаток загруженного сертификата.</span><span class="sxs-lookup"><span data-stu-id="e58fe-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="e58fe-174">Скопируйте его значение для следующего шага hello.</span><span class="sxs-lookup"><span data-stu-id="e58fe-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="e58fe-175">Привязать hello отправлен SSL сертификат toohello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e58fe-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="e58fe-176">Веб-приложение теперь имеет имя пользовательского домена hello и также имеет SSL-сертификат, который защищает этого пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="e58fe-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="e58fe-177">Hello toodo самое левой — toobind hello отправленный сертификат toohello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e58fe-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="e58fe-178">Это делается с помощью hello [привязки ssl конфигурации web appservice az](/cli/azure/appservice/web/config/ssl#bind) команды.</span><span class="sxs-lookup"><span data-stu-id="e58fe-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="e58fe-179">В следующей команде hello, замените `<app_name>` с вашим именем уникальные приложения и `<thumbprint-from-previous-output>` с отпечатком сертификата hello, получаемые из предыдущей команды hello.</span><span class="sxs-lookup"><span data-stu-id="e58fe-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="e58fe-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="e58fe-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="e58fe-181">Когда сертификат hello привязанного tooyour веб-приложения, hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="e58fe-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="e58fe-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="e58fe-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="e58fe-183">В браузере перейдите на конечную точку tooHTTPS пользовательское имя домена.</span><span class="sxs-lookup"><span data-stu-id="e58fe-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="e58fe-184">Например:</span><span class="sxs-lookup"><span data-stu-id="e58fe-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="e58fe-186">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e58fe-186">More resources</span></span>

<span data-ttu-id="e58fe-187">[Приобретение и настройка имени личного домена для службы приложений Azure](custom-dns-web-site-buydomains-web-app.md)
[Приобретение и настройка сертификата SSL для службы приложений Azure](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="e58fe-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
