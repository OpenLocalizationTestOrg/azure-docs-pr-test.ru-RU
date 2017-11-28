---
title: "Что такое модель и пакет облачной службы | Документация Майкрософт"
description: "Описание модели (CSDEF-файл, CSCFG-файл) и пакета облачной службы (CSPKG-файл) в Azure"
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
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="9ca5f-103">Что такое модель облачных служб и как создать ее пакет?</span><span class="sxs-lookup"><span data-stu-id="9ca5f-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="9ca5f-104">Облачная служба создается из трех компонентов: определения службы *(CSDEF-файл)*, конфигурации службы *(CSCFG-файл)* и пакета службы *(CSPKG-файл)*.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="9ca5f-105">Файлы **ServiceDefinition.csdef** и **ServiceConfig.cscfg** являются XML-файлами, которые описывают структуру облачной службы и ее конфигурацию. В совокупности это называется моделью.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="9ca5f-106">**ServicePackage.cspkg** — это ZIP-файл, который создается на основе файла **ServiceDefinition.csdef** и который, помимо прочего, содержит все необходимые зависимости в двоичном формате.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="9ca5f-107">Azure создает облачную службу из двух файлов: **ServicePackage.cspkg** и **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="9ca5f-108">После запуска облачной службы в Azure вы можете перенастроить ее с помощью файла **ServiceConfig.cscfg** , но вы не сможете изменить определение.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="9ca5f-109">Что еще вы хотите узнать?</span><span class="sxs-lookup"><span data-stu-id="9ca5f-109">What would you like to know more about?</span></span>
* <span data-ttu-id="9ca5f-110">Я хочу узнать больше о файлах [ServiceDefinition.csdef](#csdef) и [ServiceConfig.cscfg](#cscfg).</span><span class="sxs-lookup"><span data-stu-id="9ca5f-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="9ca5f-111">Я уже знаю об этих файлах, покажите мне [примеры](#next-steps) того, что я могу настроить.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="9ca5f-112">Я хочу создать файл [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="9ca5f-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="9ca5f-113">Я использую Visual Studio и хочу выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="9ca5f-114">[Создать облачную службу.][vs_create]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="9ca5f-115">[Изменить конфигурацию существующей облачной службы.][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="9ca5f-116">[Развернуть проект облачной службы.][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="9ca5f-117">[Настроить удаленный рабочий стол для экземпляра облачной службы.][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="9ca5f-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="9ca5f-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="9ca5f-119">Файл **ServiceDefinition.csdef** задает параметры, используемые Azure для настройки облачной службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="9ca5f-120">[Схема определения службы Azure (CSDEF-файл)](https://msdn.microsoft.com/library/azure/ee758711.aspx) предоставляет допустимый формат для файла определения службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="9ca5f-121">В следующем примере показаны параметры, которые могут быть определены для веб-ролей и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="9ca5f-122">Чтобы лучше понять используемую здесь схему XML, изучите статью [Схема определения службы](https://msdn.microsoft.com/library/azure/ee758711.aspx). В ней приводится краткое описание некоторых элементов.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="9ca5f-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-123">**Sites**</span></span>  
<span data-ttu-id="9ca5f-124">Содержит определения для веб-сайтов или веб-приложений, размещаемых в IIS7.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="9ca5f-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-125">**InputEndpoints**</span></span>  
<span data-ttu-id="9ca5f-126">Содержит определения для конечных точек, используемых для связи с облачной службой.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="9ca5f-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="9ca5f-128">Содержит определения для конечных точек, используемых экземплярами роли для взаимодействия друг с другом.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="9ca5f-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="9ca5f-130">Содержит определения параметров для функций конкретной роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="9ca5f-131">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-131">**Certificates**</span></span>  
<span data-ttu-id="9ca5f-132">Содержит определения для сертификатов, которые необходимы для роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="9ca5f-133">В предыдущем примере кода показан сертификат, используемый для настройки Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="9ca5f-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-134">**LocalResources**</span></span>  
<span data-ttu-id="9ca5f-135">Содержит определения для локальных ресурсов хранилища.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="9ca5f-136">Локальный ресурс хранилища — это зарезервированный каталог в файловой системе виртуальной машины, в которой выполняется экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="9ca5f-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-137">**Imports**</span></span>  
<span data-ttu-id="9ca5f-138">Содержит определения для импортированных модулей.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="9ca5f-139">В предыдущем примере кода показаны модули для удаленного рабочего стола и Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="9ca5f-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-140">**Startup**</span></span>  
<span data-ttu-id="9ca5f-141">Содержит задачи, которые выполняются при запуске роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="9ca5f-142">Задачи определены в CMD-файле или исполняемом файле.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="9ca5f-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="9ca5f-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="9ca5f-144">Настройка параметров для облачной службы определяется значениями в файле **ServiceConfiguration.cscfg** .</span><span class="sxs-lookup"><span data-stu-id="9ca5f-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="9ca5f-145">Вы указываете количество экземпляров, которые необходимо развернуть для каждой роли в этом файле.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="9ca5f-146">Значения для параметров конфигурации, которые определены в файле определения службы, добавляются в файл конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="9ca5f-147">Отпечатки всех сертификатов управления, связанных с облачной службы, также добавляются в файл.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="9ca5f-148">[Схема конфигурации службы Azure (CSCFG-файл)](https://msdn.microsoft.com/library/azure/ee758710.aspx) предоставляет допустимый формат файла конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="9ca5f-149">Файл конфигурации службы не упакован с приложением; он передается в Azure как отдельный файл и используется для конфигурации облачной службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="9ca5f-150">Вы можете отправить новый файл конфигурации службы без повторного развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="9ca5f-151">Значения конфигурации для облачной службы можно изменить во время работы облачной службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="9ca5f-152">В следующем примере показаны параметры конфигурации, которые можно определить для рабочих ролей и веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="9ca5f-153">Чтобы лучше понять используемую здесь схему XML, см. статью [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) (Схема конфигурации службы). В этой статье приводится краткое описание некоторых элементов.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="9ca5f-154">**Экземпляры**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-154">**Instances**</span></span>  
<span data-ttu-id="9ca5f-155">Задает количество запущенных экземпляров для роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="9ca5f-156">Чтобы предотвратить возможную недоступность облачной службы во время обновлений, рекомендуется развернуть несколько экземпляров веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="9ca5f-157">Развертывая более одного экземпляра, вы выполните рекомендации [Соглашения об уровне обслуживания Azure Compute](http://azure.microsoft.com/support/legal/sla/), что гарантирует 99,95 % внешней доступности для ролей с выходом в Интернет, если для службы развернуто два (или более) экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="9ca5f-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="9ca5f-159">Настраивает параметры для запущенных экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="9ca5f-160">Имена элементов `<Setting>` должны соответствовать определениям параметров в файле определения службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="9ca5f-161">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-161">**Certificates**</span></span>  
<span data-ttu-id="9ca5f-162">Настраивает сертификаты, используемые службой.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="9ca5f-163">В предыдущем примере кода показано, как определить сертификат для модуля RemoteAccess.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="9ca5f-164">Значение атрибута *thumbprint* должно быть присвоено отпечатку сертификата, который будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="9ca5f-165">Отпечаток сертификата можно добавить в файл конфигурации с помощью текстового редактора.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="9ca5f-166">Или можно добавить соответствующее значение на вкладку **Сертификаты** страницы **Свойства** роли в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="9ca5f-167">Определение портов для экземпляров ролей</span><span class="sxs-lookup"><span data-stu-id="9ca5f-167">Defining ports for role instances</span></span>
<span data-ttu-id="9ca5f-168">Azure разрешает только одну точку входа для веб-роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="9ca5f-169">Это означает, что весь трафик идет через один IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="9ca5f-170">Можно сделать так, чтобы веб-сайты совместно использовали порт. Для этого нужно настроить заголовок узла так, чтобы он направлял запрос в нужное расположение.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="9ca5f-171">Можно также настроить приложения для прослушивания известных портов по IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="9ca5f-172">Следующий пример показывает конфигурацию для веб-роли с веб-сайтом и веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="9ca5f-173">Веб-сайт настроен как расположение входа по умолчанию с использованием порта 80. Веб-приложения настроены на получение запросов из альтернативного заголовка узла с именем mail.mysite.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="9ca5f-174">Изменение конфигурации роли</span><span class="sxs-lookup"><span data-stu-id="9ca5f-174">Changing the configuration of a role</span></span>
<span data-ttu-id="9ca5f-175">Вы можете обновить конфигурацию облачной службы, запущенной в Azure, не переводя службу в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="9ca5f-176">Чтобы изменить сведения о конфигурации, можно отправить новый файл конфигурации. Также можно изменить файл конфигурации локально и применить его к работающей службе.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="9ca5f-177">В конфигурацию службы можно внести следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="9ca5f-178">**Изменение значений параметров конфигурации.**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="9ca5f-179">После изменения параметра конфигурации экземпляр роли может применить изменение во время работы экземпляра в сети. Или же он может предусмотрительно перезапустить экземпляр и применить изменение, пока экземпляр запущен в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="9ca5f-180">**Изменение топологии службы экземпляров роли.**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="9ca5f-181">Изменения топологии не влияют на выполняемые экземпляры, кроме случаев, когда экземпляр удаляется.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="9ca5f-182">Все остальные экземпляры обычно не нуждаются в перезапуске. Тем не менее можно выбрать перезапуск экземпляров роли в ответ на изменение топологии.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="9ca5f-183">**Изменение отпечатка сертификата.**</span><span class="sxs-lookup"><span data-stu-id="9ca5f-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="9ca5f-184">Вы можете обновлять сертификат, только когда экземпляр роли запущен в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="9ca5f-185">Если сертификат добавлен, удален или изменен, когда экземпляр роли подключен к сети, Azure предусмотрительно переводит экземпляр в автономный режим для обновления сертификата. После применения изменения экземпляр снова подключается к сети.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="9ca5f-186">Обработка изменений конфигурации с помощью событий среды выполнения службы</span><span class="sxs-lookup"><span data-stu-id="9ca5f-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="9ca5f-187">[Библиотека среды выполнения Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) содержит пространство имен [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx), которое предоставляет классы для взаимодействия со средой Azure из роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="9ca5f-188">Класс [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) определяет следующие события, которые вызываются до и после изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="9ca5f-189">Событие **[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="9ca5f-190">Это событие происходит до применения изменения конфигурации к указанному экземпляру роли, предоставляя экземпляру роли возможность освободить экземпляры роли при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="9ca5f-191">Событие **[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="9ca5f-192">Это событие происходит после применения изменения конфигурации к указанному экземпляру роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="9ca5f-193">Поскольку изменения сертификата всегда переводят экземпляры роли в автономный режим, они не вызывают событий RoleEnvironment.Changing и RoleEnvironment.Changed.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="9ca5f-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="9ca5f-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="9ca5f-195">Чтобы развернуть приложение как облачную службу в Azure, необходимо вначале упаковать приложение в соответствующий формат.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="9ca5f-196">Можно использовать программу командной строки **CSPack** (устанавливается вместе с [Azure SDK](https://azure.microsoft.com/downloads/)) для создания файла пакета в качестве альтернативы Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="9ca5f-197">**CSPack** использует содержимое файла определения службы и файла конфигурации службы для определения содержимого пакета.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="9ca5f-198">**CSPack** создает файл пакета приложения (CSPKG-файл), который можно отправить в Azure с помощью [портала Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="9ca5f-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="9ca5f-199">По умолчанию пакет называется `[ServiceDefinitionFileName].cspkg`, но вы можете указать другое имя, используя параметр `/out` в программе командной строки **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="9ca5f-200">Расположение **CSPack** приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="9ca5f-201">Чтобы найти файл CSPack.exe (в Windows), запустите ярлык **Командная строка Microsoft Azure** , который устанавливается вместе с пакетом SDK.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="9ca5f-202">Запустите программу CSPack.exe отдельно, чтобы просмотреть документацию обо всех возможных параметрах и командах.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="9ca5f-203">Запустите облачную службу локально в **эмуляторе вычислений Microsoft Azure**, использовав параметр **/copyonly**.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="9ca5f-204">При указании этого параметра двоичные файлы приложения копируются в структуру каталогов, из которой они могут выполняться в эмуляторе вычислений.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="9ca5f-205">Пример команды для упаковки облачной службы</span><span class="sxs-lookup"><span data-stu-id="9ca5f-205">Example command to package a cloud service</span></span>
<span data-ttu-id="9ca5f-206">В следующем примере создается пакет приложения, содержащий информацию для веб-роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="9ca5f-207">Команда задает используемый файл определения службы, а также каталог, в котором находятся двоичные файлы, и имя файла пакета.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="9ca5f-208">Если приложение содержит веб-роль и рабочую роль, используется следующая команда.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="9ca5f-209">Здесь переменные определены следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="9ca5f-210">Переменная</span><span class="sxs-lookup"><span data-stu-id="9ca5f-210">Variable</span></span> | <span data-ttu-id="9ca5f-211">Значение</span><span class="sxs-lookup"><span data-stu-id="9ca5f-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9ca5f-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-212">\[DirectoryName\]</span></span> |<span data-ttu-id="9ca5f-213">Подкаталог в корневом каталоге проекта, который содержит CSDEF-файл проекта Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="9ca5f-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="9ca5f-215">Имя файла определения службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-215">The name of the service definition file.</span></span> <span data-ttu-id="9ca5f-216">По умолчанию этот файл называется ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="9ca5f-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-217">\[OutputFileName\]</span></span> |<span data-ttu-id="9ca5f-218">Имя создаваемого файла пакета.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-218">The name for the generated package file.</span></span> <span data-ttu-id="9ca5f-219">Как правило, ему присваивается имя приложения.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="9ca5f-220">Если имя файла не указано, создаваемому пакету приложения с расширением CSPKG присваивается \[имя приложения\].</span><span class="sxs-lookup"><span data-stu-id="9ca5f-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="9ca5f-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-221">\[RoleName\]</span></span> |<span data-ttu-id="9ca5f-222">Имя роли, определенное в файле определения службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="9ca5f-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="9ca5f-224">Расположение двоичных файлов для роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="9ca5f-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-225">\[VirtualPath\]</span></span> |<span data-ttu-id="9ca5f-226">Физические каталоги для каждого виртуального пути, определенного в разделе «Сайты» определения службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="9ca5f-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="9ca5f-228">Физические каталоги содержимого для каждого виртуального пути, заданного в узле «Сайт» определения службы.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="9ca5f-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="9ca5f-230">Имя двоичного файла для роли.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9ca5f-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ca5f-231">Next steps</span></span>
<span data-ttu-id="9ca5f-232">Я создаю пакет облачной службы и я хочу выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="9ca5f-233">[Настроить удаленный рабочий стол для экземпляра облачной службы.][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="9ca5f-234">[Развернуть проект облачной службы.][deploy]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="9ca5f-235">Я использую Visual Studio и хочу выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9ca5f-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="9ca5f-236">[Создать новую облачную службу.][vs_create]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="9ca5f-237">[Изменить конфигурацию существующей облачной службы.][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="9ca5f-238">[Развернуть проект облачной службы.][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="9ca5f-239">[Настроить удаленный рабочий стол для экземпляра облачной службы.][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="9ca5f-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
