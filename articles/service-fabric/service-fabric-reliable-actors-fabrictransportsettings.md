---
title: "Параметры FabricTransport aaaChange в Azure микрослужбами | Документы Microsoft"
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
ms.openlocfilehash: e312b475407eb95a435b93d80c0f2e9618b9ea1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="18bfc-103">Настройка параметров FabricTransport для Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="18bfc-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="18bfc-104">Ниже приведены параметры hello, которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="18bfc-104">Here are hello settings that you can configure:</span></span>
- <span data-ttu-id="18bfc-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="18bfc-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="18bfc-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings).</span><span class="sxs-lookup"><span data-stu-id="18bfc-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="18bfc-107">Конфигурация по умолчанию hello FabricTransport можно изменить следующими способами.</span><span class="sxs-lookup"><span data-stu-id="18bfc-107">You can modify hello default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="18bfc-108">Атрибут сборки</span><span class="sxs-lookup"><span data-stu-id="18bfc-108">Assembly attribute</span></span>

<span data-ttu-id="18bfc-109">Hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) toobe применения hello субъекта клиента и субъект службы сборок необходимо, чтобы атрибут.</span><span class="sxs-lookup"><span data-stu-id="18bfc-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs toobe applied on hello actor client and actor service assemblies.</span></span>

<span data-ttu-id="18bfc-110">Hello в следующем примере показано, как toochange hello FabricTransport OperationTimeout параметров по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="18bfc-110">hello following example shows how toochange hello default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="18bfc-111">Во втором примере показано, как изменить значения по умолчанию параметров MaxMessageSize и OperationTimeoutInSeconds в конфигурации FabricTransport.</span><span class="sxs-lookup"><span data-stu-id="18bfc-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="18bfc-112">Пакет конфигурации</span><span class="sxs-lookup"><span data-stu-id="18bfc-112">Config package</span></span>

<span data-ttu-id="18bfc-113">Можно использовать [пакет конфигурации](service-fabric-application-model.md) toomodify конфигурация по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="18bfc-113">You can use a [config package](service-fabric-application-model.md) toomodify hello default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-hello-actor-service"></a><span data-ttu-id="18bfc-114">Настройка параметров FabricTransport для службы субъекта hello</span><span class="sxs-lookup"><span data-stu-id="18bfc-114">Configure FabricTransport settings for hello actor service</span></span>

<span data-ttu-id="18bfc-115">Добавьте раздел TransportSettings в файле settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="18bfc-115">Add a TransportSettings section in hello settings.xml file.</span></span>

<span data-ttu-id="18bfc-116">По умолчанию код субъекта для параметра SectionName выглядит следующим образом: &lt;имя_субъекта&gt;TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="18bfc-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="18bfc-117">Если соответствующее значение не найдено, выполняется поиск значения TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="18bfc-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

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

### <a name="configure-fabrictransport-settings-for-hello-actor-client-assembly"></a><span data-ttu-id="18bfc-118">Настройка параметров FabricTransport для клиентской сборки hello субъекта</span><span class="sxs-lookup"><span data-stu-id="18bfc-118">Configure FabricTransport settings for hello actor client assembly</span></span>

<span data-ttu-id="18bfc-119">Hello клиента не выполняется как часть службы, можно создать «&lt;клиента имя EXE-файла&gt;. settings.xml» файл hello таким же расположении, что и файл .exe hello клиента.</span><span class="sxs-lookup"><span data-stu-id="18bfc-119">If hello client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in hello same location as hello client .exe file.</span></span> <span data-ttu-id="18bfc-120">Затем добавьте раздел TransportSettings в этом файле.</span><span class="sxs-lookup"><span data-stu-id="18bfc-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="18bfc-121">Для параметра SectionName задайте значение TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="18bfc-121">SectionName should be "TransportSettings".</span></span>

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

  * <span data-ttu-id="18bfc-122">Настройка параметров FabricTransport для защиты клиента и службы субъекта с помощью дополнительного сертификата.</span><span class="sxs-lookup"><span data-stu-id="18bfc-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="18bfc-123">Добавить данные дополнительного сертификата можно, добавив параметр CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="18bfc-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="18bfc-124">Ниже приведен пример hello для hello TransportSettings прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="18bfc-124">Below is hello example for hello Listener TransportSettings.</span></span>

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
     <span data-ttu-id="18bfc-125">Ниже приведен пример hello для hello TransportSettings клиента.</span><span class="sxs-lookup"><span data-stu-id="18bfc-125">Below is hello example for hello Client TransportSettings.</span></span>

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
    * <span data-ttu-id="18bfc-126">Настройка параметров FabricTransport для защиты службы или клиента субъекта с помощью имени субъекта.</span><span class="sxs-lookup"><span data-stu-id="18bfc-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="18bfc-127">FindType tooprovide потребностей пользователя как FindBySubjectName, добавьте значения CertificateIssuerThumbprints и CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="18bfc-127">User needs tooprovide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="18bfc-128">Ниже приведен пример hello для hello TransportSettings прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="18bfc-128">Below is hello example for hello Listener TransportSettings.</span></span>

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
  <span data-ttu-id="18bfc-129">Ниже приведен пример hello для hello TransportSettings клиента.</span><span class="sxs-lookup"><span data-stu-id="18bfc-129">Below is hello example for hello Client TransportSettings.</span></span>

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
