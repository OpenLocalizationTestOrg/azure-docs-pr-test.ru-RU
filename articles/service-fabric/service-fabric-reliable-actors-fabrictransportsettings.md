---
title: "Изменение параметров FabricTransport в микрослужбах Azure | Документация Майкрософт"
description: "Узнайте, как настроить параметры связи субъекта Azure Service Fabric."
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 75bdd4644f4ccc583271b9169c50a375e2cd6629
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="94f56-103">Настройка параметров FabricTransport для Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="94f56-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="94f56-104">Ниже приведены параметры, которые можно настраивать.</span><span class="sxs-lookup"><span data-stu-id="94f56-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="94f56-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="94f56-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="94f56-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings).</span><span class="sxs-lookup"><span data-stu-id="94f56-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="94f56-107">Конфигурацию FabricTransport по умолчанию можно изменить одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="94f56-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="94f56-108">Атрибут сборки</span><span class="sxs-lookup"><span data-stu-id="94f56-108">Assembly attribute</span></span>

<span data-ttu-id="94f56-109">Атрибут [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) необходимо применить в клиенте субъекта и в сборках службы субъектов.</span><span class="sxs-lookup"><span data-stu-id="94f56-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="94f56-110">В следующем примере показано, как изменить значение по умолчанию параметра OperationTimeout в конфигурации FabricTransport.</span><span class="sxs-lookup"><span data-stu-id="94f56-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="94f56-111">Во втором примере показано, как изменить значения по умолчанию параметров MaxMessageSize и OperationTimeoutInSeconds в конфигурации FabricTransport.</span><span class="sxs-lookup"><span data-stu-id="94f56-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="94f56-112">Пакет конфигурации</span><span class="sxs-lookup"><span data-stu-id="94f56-112">Config package</span></span>

<span data-ttu-id="94f56-113">Для изменения конфигурации по умолчанию можно использовать [пакет конфигурации](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="94f56-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="94f56-114">Настройка параметров FabricTransport для службы субъектов</span><span class="sxs-lookup"><span data-stu-id="94f56-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="94f56-115">Добавьте раздел TransportSettings в файл settings.xml.</span><span class="sxs-lookup"><span data-stu-id="94f56-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="94f56-116">По умолчанию код субъекта для параметра SectionName выглядит следующим образом: &lt;имя_субъекта&gt;TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="94f56-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="94f56-117">Если соответствующее значение не найдено, выполняется поиск значения TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="94f56-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="94f56-118">Настройка параметров FabricTransport для сборки службы субъектов</span><span class="sxs-lookup"><span data-stu-id="94f56-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="94f56-119">Если клиент не выполняется как часть службы, можно создать файл &lt;имя_EXE-файла_клиента&gt;.settings.xml в том же каталоге, в котором находится EXE-файл клиента.</span><span class="sxs-lookup"><span data-stu-id="94f56-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="94f56-120">Затем добавьте раздел TransportSettings в этом файле.</span><span class="sxs-lookup"><span data-stu-id="94f56-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="94f56-121">Для параметра SectionName задайте значение TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="94f56-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="94f56-122">Настройка параметров FabricTransport для защиты клиента и службы субъекта с помощью дополнительного сертификата.</span><span class="sxs-lookup"><span data-stu-id="94f56-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="94f56-123">Добавить данные дополнительного сертификата можно, добавив параметр CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="94f56-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="94f56-124">Ниже приведен пример TransportSettings для прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="94f56-124">Below is the example for the Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="94f56-125">Ниже приведен пример TransportSettings для клиента.</span><span class="sxs-lookup"><span data-stu-id="94f56-125">Below is the example for the Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="94f56-126">Настройка параметров FabricTransport для защиты службы или клиента субъекта с помощью имени субъекта.</span><span class="sxs-lookup"><span data-stu-id="94f56-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="94f56-127">Пользователь должен предоставить findType в качестве FindBySubjectName. Добавьте значения CertificateIssuerThumbprints и CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="94f56-127">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="94f56-128">Ниже приведен пример TransportSettings для прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="94f56-128">Below is the example for the Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="94f56-129">Ниже приведен пример TransportSettings для клиента.</span><span class="sxs-lookup"><span data-stu-id="94f56-129">Below is the example for the Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
