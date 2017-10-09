---
title: "aaaWhat — это модель облачной службы и пакета | Документы Microsoft"
description: "Описывает модель облачной службы hello (.csdef, .cscfg) и пакет (cspkg-файл) в Azure"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="f2701-103">Что такое hello модели облачной службы и как его упаковки?</span><span class="sxs-lookup"><span data-stu-id="f2701-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="f2701-104">Облачная служба создается из трех компонентов, определение службы hello *(.csdef)*, hello файла конфигурации службы *(.cscfg)*и пакет службы *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="f2701-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="f2701-105">Оба hello **ServiceDefinition.csdef** и **ServiceConfig.cscfg** файлы основаны на XML и описывают структуру hello hello облачной службы и как оно настроено; под общим названием hello модели.</span><span class="sxs-lookup"><span data-stu-id="f2701-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="f2701-106">Hello **ServicePackage.cspkg** является ZIP-файл, созданный из hello **ServiceDefinition.csdef** и помимо прочего, содержит все необходимые hello двоичном формате зависимости.</span><span class="sxs-lookup"><span data-stu-id="f2701-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="f2701-107">Azure создает облачную службу из обоих hello **ServicePackage.cspkg** и hello **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="f2701-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="f2701-108">После запуска hello облачной службы в Azure можно перенастроить ее через hello **ServiceConfig.cscfg** файла, но его невозможно изменить определение hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="f2701-109">Как Дополнительные сведения о tooknow?</span><span class="sxs-lookup"><span data-stu-id="f2701-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="f2701-110">Требуется больше о hello tooknow [ServiceDefinition.csdef](#csdef) и [ServiceConfig.cscfg](#cscfg) файлов.</span><span class="sxs-lookup"><span data-stu-id="f2701-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="f2701-111">Я уже знаю об этих файлах, покажите мне [примеры](#next-steps) того, что я могу настроить.</span><span class="sxs-lookup"><span data-stu-id="f2701-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="f2701-112">Я хочу toocreate hello [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="f2701-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="f2701-113">Я использую Visual Studio и хочу выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f2701-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="f2701-114">[Создать облачную службу.][vs_create]</span><span class="sxs-lookup"><span data-stu-id="f2701-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="f2701-115">[Изменить конфигурацию существующей облачной службы.][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="f2701-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="f2701-116">[Развернуть проект облачной службы.][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="f2701-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="f2701-117">[Настроить удаленный рабочий стол для экземпляра облачной службы.][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="f2701-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="f2701-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="f2701-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="f2701-119">Hello **ServiceDefinition.csdef** файл задает hello параметры, используемые Azure tooconfigure облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="f2701-120">Hello [схема определения службы Azure (.csdef файла)](https://msdn.microsoft.com/library/azure/ee758711.aspx) предоставляет hello допустимый формат файла определения службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="f2701-121">Hello ниже приведен пример hello параметры, которые могут быть определены для hello Web и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="f2701-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="f2701-122">Можно ссылаться toohello [схема определения службы](https://msdn.microsoft.com/library/azure/ee758711.aspx) для лучшего понимания hello XML-схемы, используемые здесь, однако здесь приводится краткое описание некоторых hello элементов:</span><span class="sxs-lookup"><span data-stu-id="f2701-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="f2701-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="f2701-123">**Sites**</span></span>  
<span data-ttu-id="f2701-124">Содержит определения hello для веб-сайтов или веб-приложений, размещаемых в IIS7.</span><span class="sxs-lookup"><span data-stu-id="f2701-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="f2701-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="f2701-125">**InputEndpoints**</span></span>  
<span data-ttu-id="f2701-126">Содержит определения hello для конечных точек, которые используются toocontact hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="f2701-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="f2701-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="f2701-128">Содержит определения hello для конечных точек, используемых toocommunicate экземпляры роли друг с другом.</span><span class="sxs-lookup"><span data-stu-id="f2701-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="f2701-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="f2701-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="f2701-130">Содержит определения параметров hello для функций определенной роли.</span><span class="sxs-lookup"><span data-stu-id="f2701-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="f2701-131">**Сертификаты**</span><span class="sxs-lookup"><span data-stu-id="f2701-131">**Certificates**</span></span>  
<span data-ttu-id="f2701-132">Содержит определения hello для сертификатов, которые необходимы для роли.</span><span class="sxs-lookup"><span data-stu-id="f2701-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="f2701-133">Предыдущий пример кода Hello показан сертификат, используемый для настройки hello Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="f2701-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="f2701-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="f2701-134">**LocalResources**</span></span>  
<span data-ttu-id="f2701-135">Содержит определения hello для локальных ресурсов хранения.</span><span class="sxs-lookup"><span data-stu-id="f2701-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="f2701-136">Ресурс локального хранилища представляет собой зарезервированный каталог в файловой системе hello hello виртуальной машины, в которой выполняется экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="f2701-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="f2701-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="f2701-137">**Imports**</span></span>  
<span data-ttu-id="f2701-138">Содержит определения hello для импортированных модулей.</span><span class="sxs-lookup"><span data-stu-id="f2701-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="f2701-139">Предыдущий пример кода Hello содержит модули, hello для удаленного рабочего стола и Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="f2701-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="f2701-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="f2701-140">**Startup**</span></span>  
<span data-ttu-id="f2701-141">Содержит задачи, которые выполняются при запуске роли hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="f2701-142">Hello задачи определяются в файле CMD или исполняемого файла.</span><span class="sxs-lookup"><span data-stu-id="f2701-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="f2701-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="f2701-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="f2701-144">Настройка Hello hello параметров для облачной службы определяется значениями hello в hello **ServiceConfiguration.cscfg** файла.</span><span class="sxs-lookup"><span data-stu-id="f2701-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="f2701-145">Указать hello число экземпляров, что требуется toodeploy для каждой роли в этом файле.</span><span class="sxs-lookup"><span data-stu-id="f2701-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="f2701-146">Hello значения для параметров конфигурации hello, которые определены в файле определения службы hello добавляются toohello файла конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="f2701-147">Hello отпечатки всех сертификатов управления, связанные с hello облачной службы также добавляются в файл toohello.</span><span class="sxs-lookup"><span data-stu-id="f2701-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="f2701-148">Hello [схема конфигурации службы Azure (csfg файла)](https://msdn.microsoft.com/library/azure/ee758710.aspx) предоставляет hello допустимый формат файла конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="f2701-149">Hello службы файл конфигурации не упаковывается с приложением hello, но загруженного tooAzure как отдельный файл и — используется tooconfigure hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="f2701-150">Вы можете отправить новый файл конфигурации службы без повторного развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="f2701-151">значения параметров конфигурации Hello hello облачной службы можно изменить во время выполнения hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="f2701-152">Hello ниже приведен пример hello параметры конфигурации, которые могут быть определены для hello Web и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="f2701-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="f2701-153">Можно ссылаться toohello [схема конфигурации службы](https://msdn.microsoft.com/library/azure/ee758710.aspx) для улучшения понимания hello схемы XML, используемый здесь, однако здесь приводится краткое описание hello элементов:</span><span class="sxs-lookup"><span data-stu-id="f2701-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="f2701-154">**Экземпляры**</span><span class="sxs-lookup"><span data-stu-id="f2701-154">**Instances**</span></span>  
<span data-ttu-id="f2701-155">Задает количество запущенных экземпляров роли hello hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="f2701-156">tooprevent вашей облачной службы из потенциально становится недоступным во время обновления, рекомендуется развернуть более одного экземпляра вашего веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="f2701-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="f2701-157">Развертывая более одного экземпляра, вы придерживаетесь toohello рекомендации в hello [Azure вычислений службы соглашения об уровне](http://azure.microsoft.com/support/legal/sla/), это гарантирует 99,95% внешней доступности для ролей с выходом в Интернет, когда два или несколько ролей экземпляры будут развернуты для службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="f2701-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="f2701-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="f2701-159">Настраивает параметры hello hello запущенных экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="f2701-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="f2701-160">Имя Hello hello `<Setting>` элементов должен соответствовать hello определения параметров в файле определения службы hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="f2701-161">**Сертификаты**</span><span class="sxs-lookup"><span data-stu-id="f2701-161">**Certificates**</span></span>  
<span data-ttu-id="f2701-162">Настраивает hello сертификаты, используемые службой hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="f2701-163">Hello предыдущий пример кода показывает, как toodefine hello сертификат для модуля RemoteAccess hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="f2701-164">Здравствуйте, значение hello *отпечаток* атрибут должен быть задан toohello отпечаток сертификата toouse hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="f2701-165">Hello отпечаток сертификата hello можно добавить файл конфигурации toohello, используя текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="f2701-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="f2701-166">Или может быть добавлено значение hello hello **сертификаты** вкладка hello **свойства** страницы приветствия роли в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2701-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="f2701-167">Определение портов для экземпляров ролей</span><span class="sxs-lookup"><span data-stu-id="f2701-167">Defining ports for role instances</span></span>
<span data-ttu-id="f2701-168">Azure позволяет только одна запись tooa точка веб-роли.</span><span class="sxs-lookup"><span data-stu-id="f2701-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="f2701-169">Это означает, что весь трафик идет через один IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f2701-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="f2701-170">Ваш веб-сайтов tooshare порт можно настроить путем настройки hello узла заголовок toodirect hello запроса toohello правильное расположение.</span><span class="sxs-lookup"><span data-stu-id="f2701-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="f2701-171">Можно также настроить порты toowell известного toolisten вашего приложения hello IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f2701-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="f2701-172">Hello ниже приведен пример hello конфигурации для веб-роли с веб-сайта и веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f2701-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="f2701-173">Hello веб-сайт настроен как расположение входа по умолчанию hello на порт 80, а hello веб-приложения, настроенные tooreceive запросов из альтернативного заголовка узла, называется «mail.mysite.cloudapp.net».</span><span class="sxs-lookup"><span data-stu-id="f2701-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="f2701-174">Изменение конфигурации роли hello</span><span class="sxs-lookup"><span data-stu-id="f2701-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="f2701-175">Можно обновить конфигурацию hello облачной службы, запущенной в Azure, не отключая службы hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="f2701-176">toochange сведения о конфигурации, можно либо отправить новый файл конфигурации, или изменить файл конфигурации hello в поместите и применить его tooyour, на котором выполняется служба.</span><span class="sxs-lookup"><span data-stu-id="f2701-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="f2701-177">Hello внесены следующие изменения могут быть toohello конфигурации службы:</span><span class="sxs-lookup"><span data-stu-id="f2701-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="f2701-178">**Изменение hello значений параметров конфигурации**</span><span class="sxs-lookup"><span data-stu-id="f2701-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="f2701-179">При конфигурации изменения, параметров экземпляра роли можно изменить hello tooapply, когда экземпляр hello находится в сети, или экземпляр hello toorecycle надлежащим образом и применить изменение hello в том случае, когда экземпляр hello отключен от сети.</span><span class="sxs-lookup"><span data-stu-id="f2701-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="f2701-180">**Изменение топологии службы hello экземпляров ролей**</span><span class="sxs-lookup"><span data-stu-id="f2701-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="f2701-181">Изменения топологии не влияют на выполняемые экземпляры, кроме случаев, когда экземпляр удаляется.</span><span class="sxs-lookup"><span data-stu-id="f2701-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="f2701-182">Все остальные экземпляры обычно не обязательно toobe перезапуску; Тем не менее вы можете toorecycle экземпляров роли в изменение топологии tooa ответа.</span><span class="sxs-lookup"><span data-stu-id="f2701-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="f2701-183">**Изменение отпечатка сертификата hello**</span><span class="sxs-lookup"><span data-stu-id="f2701-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="f2701-184">Вы можете обновлять сертификат, только когда экземпляр роли запущен в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="f2701-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="f2701-185">Если сертификат добавлен, удален или изменен, когда экземпляр роли находится в оперативном режиме, Azure надлежащим образом принимает сертификат hello tooupdate автономного экземпляра hello и подключить его обратно после завершения изменений hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="f2701-186">Обработка изменений конфигурации с помощью событий среды выполнения службы</span><span class="sxs-lookup"><span data-stu-id="f2701-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="f2701-187">Hello [библиотека времени выполнения Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) включает hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) пространства имен, которое предоставляет классы для взаимодействия с hello средой Azure из роли.</span><span class="sxs-lookup"><span data-stu-id="f2701-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="f2701-188">Hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) класс определяет hello следующие события, которые вызываются до и после изменения конфигурации:</span><span class="sxs-lookup"><span data-stu-id="f2701-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="f2701-189">Событие **[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="f2701-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="f2701-190">Это происходит до примененных tooa указанного экземпляра роли, предоставляя возможность tootake работу экземпляров роли hello при необходимости изменения конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="f2701-191">Событие **[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="f2701-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="f2701-192">Происходит после изменения конфигурации hello примененных tooa указанного экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="f2701-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="f2701-193">Поскольку изменения сертификата всегда отключите hello экземпляров роли, они не вызывают событий RoleEnvironment.Changing и RoleEnvironment.Changed hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="f2701-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="f2701-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="f2701-195">toodeploy приложения как облачной службы в Azure необходимо первого пакета приложения hello в соответствующем формате hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="f2701-196">Можно использовать hello **CSPack** средство командной строки (установлен с hello [пакета Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello пакета файл в качестве альтернативного tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2701-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="f2701-197">**CSPack** использует hello содержимое hello службы определение файловые службы и службы содержимое файла конфигурации toodefine hello hello пакета.</span><span class="sxs-lookup"><span data-stu-id="f2701-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="f2701-198">**CSPack** создает файл пакета приложения (cspkg-файл), вы можете отправить tooAzure с помощью hello [портал Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="f2701-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="f2701-199">По умолчанию с именем пакета hello `[ServiceDefinitionFileName].cspkg`, но можно указать другое имя с помощью hello `/out` параметр **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="f2701-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="f2701-200">Расположение **CSPack** приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="f2701-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="f2701-201">Доступна CSPack.exe (в windows), запустив hello **командной строки пакета Microsoft Azure** ярлык, который устанавливается вместе с hello SDK.</span><span class="sxs-lookup"><span data-stu-id="f2701-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="f2701-202">Запустите программу CSPack.exe hello сам по себе toosee документации о всех возможных параметрах hello и команд.</span><span class="sxs-lookup"><span data-stu-id="f2701-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="f2701-203">Запустить облачную службу локально в hello **эмулятор вычислений Microsoft Azure**, использовать hello **/copyonly** параметр.</span><span class="sxs-lookup"><span data-stu-id="f2701-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="f2701-204">Этот параметр копирует hello двоичные файлы для hello приложения tooa каталог макета, из которого они могут выполняться в эмуляторе вычислений hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="f2701-205">Пример команды toopackage облачной службы</span><span class="sxs-lookup"><span data-stu-id="f2701-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="f2701-206">Hello следующий пример создает пакет приложения, содержащий hello сведения для веб-роли.</span><span class="sxs-lookup"><span data-stu-id="f2701-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="f2701-207">Команда Hello указывает toouse файла определения службы hello, hello каталог, где двоичные файлы могут быть найдены и hello имя файла пакета hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="f2701-208">Если приложение hello содержит веб-роли и рабочей роли, hello следующая команда используется:</span><span class="sxs-lookup"><span data-stu-id="f2701-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="f2701-209">Где hello переменные определены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f2701-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="f2701-210">Переменная</span><span class="sxs-lookup"><span data-stu-id="f2701-210">Variable</span></span> | <span data-ttu-id="f2701-211">Значение</span><span class="sxs-lookup"><span data-stu-id="f2701-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f2701-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="f2701-212">\[DirectoryName\]</span></span> |<span data-ttu-id="f2701-213">Hello вложенную Привет корневого каталога проекта, содержащий файл csdef hello hello проекта Azure.</span><span class="sxs-lookup"><span data-stu-id="f2701-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="f2701-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="f2701-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="f2701-215">Имя файла определения службы hello Hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-215">hello name of hello service definition file.</span></span> <span data-ttu-id="f2701-216">По умолчанию этот файл называется ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="f2701-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="f2701-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="f2701-217">\[OutputFileName\]</span></span> |<span data-ttu-id="f2701-218">Имя Hello hello создан файл пакета.</span><span class="sxs-lookup"><span data-stu-id="f2701-218">hello name for hello generated package file.</span></span> <span data-ttu-id="f2701-219">Как правило этот параметр задается имя toohello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="f2701-220">Если имя файла не указано, пакет приложения hello создается как \[ApplicationName\]cspkg-файл.</span><span class="sxs-lookup"><span data-stu-id="f2701-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="f2701-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="f2701-221">\[RoleName\]</span></span> |<span data-ttu-id="f2701-222">Имя роли hello, заданное в файле определения службы hello Hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="f2701-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="f2701-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="f2701-224">расположение Hello hello двоичные файлы для роли hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="f2701-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="f2701-225">\[VirtualPath\]</span></span> |<span data-ttu-id="f2701-226">Hello физические каталоги для каждого виртуального пути, заданные в разделе сайтов hello hello определения службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="f2701-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="f2701-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="f2701-228">физические каталоги Hello hello содержимого для каждого виртуального пути, определенные в узел hello hello определения службы.</span><span class="sxs-lookup"><span data-stu-id="f2701-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="f2701-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="f2701-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="f2701-230">Имя Hello hello двоичного файла для роли hello.</span><span class="sxs-lookup"><span data-stu-id="f2701-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f2701-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f2701-231">Next steps</span></span>
<span data-ttu-id="f2701-232">Я создаю пакет облачной службы и я хочу выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f2701-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="f2701-233">[Настроить удаленный рабочий стол для экземпляра облачной службы.][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="f2701-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="f2701-234">[Развернуть проект облачной службы.][deploy]</span><span class="sxs-lookup"><span data-stu-id="f2701-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="f2701-235">Я использую Visual Studio и хочу выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f2701-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="f2701-236">[Создать новую облачную службу.][vs_create]</span><span class="sxs-lookup"><span data-stu-id="f2701-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="f2701-237">[Изменить конфигурацию существующей облачной службы.][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="f2701-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="f2701-238">[Развернуть проект облачной службы.][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="f2701-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="f2701-239">[Настроить удаленный рабочий стол для экземпляра облачной службы.][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="f2701-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
