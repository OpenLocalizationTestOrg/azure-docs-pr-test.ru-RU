---
title: "aaaAzure безопасности контейнера Service Fabric | Документы Microsoft"
description: "Узнайте, теперь toosecure контейнер служб."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a><span data-ttu-id="19a32-103">Безопасность контейнера</span><span class="sxs-lookup"><span data-stu-id="19a32-103">Container security</span></span>

<span data-ttu-id="19a32-104">Service Fabric предоставляет механизм для служб внутри tooaccess контейнера сертификата, установленного на hello узлов в кластере Windows или Linux (версии 5.7 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="19a32-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="19a32-105">Кроме того, Service Fabric поддерживает групповые управляемые учетные записи службы (gMSA) для контейнеров Windows.</span><span class="sxs-lookup"><span data-stu-id="19a32-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="19a32-106">Управление сертификатами для контейнеров</span><span class="sxs-lookup"><span data-stu-id="19a32-106">Certificate management for containers</span></span>

<span data-ttu-id="19a32-107">Службы контейнеров можно защитить с помощью сертификата.</span><span class="sxs-lookup"><span data-stu-id="19a32-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="19a32-108">Hello сертификат должен быть установлен на hello узлы кластера hello.</span><span class="sxs-lookup"><span data-stu-id="19a32-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="19a32-109">Hello сертификат сведения предоставляются в манифесте приложения hello под hello `ContainerHostPolicies` тегу в виде hello в следующем фрагменте кода показан:</span><span class="sxs-lookup"><span data-stu-id="19a32-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="19a32-110">При запуске приложения hello, среда выполнения hello считывает сертификаты hello и приводит к возникновению ошибки PFX-файла и пароль для каждого сертификата.</span><span class="sxs-lookup"><span data-stu-id="19a32-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="19a32-111">Этот PFX-файл и пароль, доступны в контейнере hello hello следующие переменные среды с помощью:</span><span class="sxs-lookup"><span data-stu-id="19a32-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="19a32-112">**Certificate_[CodePackageName]_[CertName]_PFX**;</span><span class="sxs-lookup"><span data-stu-id="19a32-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="19a32-113">**Certificate_[CodePackageName]_[CertName]_Password**.</span><span class="sxs-lookup"><span data-stu-id="19a32-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="19a32-114">для импорта PFX-файла hello в контейнер hello отвечает Hello контейнера службы или процесса.</span><span class="sxs-lookup"><span data-stu-id="19a32-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="19a32-115">сертификат tooimport hello, можно использовать `setupentrypoint.sh` выполнения пользовательского кода в рамках процесса контейнера hello или сценариев.</span><span class="sxs-lookup"><span data-stu-id="19a32-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="19a32-116">Образец кода на языке C# для импорта PFX-файла hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="19a32-116">Sample code in C# for importing hello PFX file follows:</span></span>

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
<span data-ttu-id="19a32-117">Этот сертификат PFX-ФАЙЛ можно использовать для проверки подлинности приложения hello или службы или безопасного commmunication с другими службами.</span><span class="sxs-lookup"><span data-stu-id="19a32-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="19a32-118">Настройка gMSA для контейнеров Windows</span><span class="sxs-lookup"><span data-stu-id="19a32-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="19a32-119">tooset копирование групповой управляемой учетной записи (группа управляемые учетные записи служб), спецификация файла учетных данных (`credspec`) помещается на всех узлах в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="19a32-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="19a32-120">Hello файл можно скопировать на всех узлах, используя расширение виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="19a32-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="19a32-121">Hello `credspec` файл должен содержать сведения об учетной записи gMSA hello.</span><span class="sxs-lookup"><span data-stu-id="19a32-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="19a32-122">Дополнительные сведения о hello `credspec` файла см. в разделе [учетные записи служб](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="19a32-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="19a32-123">Спецификация учетных данных Hello и hello `Hostname` тег указаны в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="19a32-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="19a32-124">Hello `Hostname` тега должно соответствовать имя учетной записи gMSA hello, hello выполняется контейнера.</span><span class="sxs-lookup"><span data-stu-id="19a32-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="19a32-125">Hello `Hostname` тег позволяет tooauthenticate hello контейнера сам tooother службы в домене hello, с помощью проверки подлинности Kerberos.</span><span class="sxs-lookup"><span data-stu-id="19a32-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="19a32-126">Пример для указания hello `Hostname` и hello `credspec` в hello отображается манифест приложения hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="19a32-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="19a32-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19a32-127">Next steps</span></span>

* [<span data-ttu-id="19a32-128">Развертывание tooService контейнера Windows Fabric на Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="19a32-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="19a32-129">Развертывание tooService контейнера Docker структуры в Linux</span><span class="sxs-lookup"><span data-stu-id="19a32-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
