---
title: "Безопасность контейнеров Azure Service Fabric | Документация Майкрософт"
description: "Узнайте, как защитить службы контейнеров."
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
ms.openlocfilehash: 75faca1e827a0eca6b97adcb2e1c6ca72b3364d6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="container-security"></a><span data-ttu-id="c9dcb-103">Безопасность контейнера</span><span class="sxs-lookup"><span data-stu-id="c9dcb-103">Container security</span></span>

<span data-ttu-id="c9dcb-104">Service Fabric предоставляет для служб в контейнере механизм, который обеспечивает доступ к сертификату, установленному на узлах кластера Windows или Linux (версии 5.7 или выше).</span><span class="sxs-lookup"><span data-stu-id="c9dcb-104">Service Fabric provides a mechanism for services inside a container to access a certificate that is installed on the nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="c9dcb-105">Кроме того, Service Fabric поддерживает групповые управляемые учетные записи службы (gMSA) для контейнеров Windows.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="c9dcb-106">Управление сертификатами для контейнеров</span><span class="sxs-lookup"><span data-stu-id="c9dcb-106">Certificate management for containers</span></span>

<span data-ttu-id="c9dcb-107">Службы контейнеров можно защитить с помощью сертификата.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="c9dcb-108">Этот сертификат должен быть установлен на узлах в кластере.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-108">The certificate must be installed on the nodes of the cluster.</span></span> <span data-ttu-id="c9dcb-109">Сведения о сертификате указываются в манифесте приложения после тега `ContainerHostPolicies`, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="c9dcb-109">The certificate information is provided in the application manifest under the `ContainerHostPolicies` tag as the following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="c9dcb-110">При запуске приложения в среде выполнения считываются сертификаты, создается PFX-файл и пароль для каждого сертификата.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-110">When starting the application, the runtime reads the certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="c9dcb-111">Доступ к PFX-файлу и паролю в контейнере можно получить с помощью следующих переменных среды:</span><span class="sxs-lookup"><span data-stu-id="c9dcb-111">This PFX file and password are accessible inside the container using the following environment variables:</span></span> 

* <span data-ttu-id="c9dcb-112">**Certificate_[CodePackageName]_[CertName]_PFX**;</span><span class="sxs-lookup"><span data-stu-id="c9dcb-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="c9dcb-113">**Certificate_[CodePackageName]_[CertName]_Password**.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="c9dcb-114">Импорт PFX-файла в контейнер выполняется с помощью службы контейнеров или процесса контейнера.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-114">The container service or process is responsible for importing the PFX file into the container.</span></span> <span data-ttu-id="c9dcb-115">Для импорта сертификата можно использовать скрипты `setupentrypoint.sh` или пользовательский исполняемый код в процессе контейнера.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-115">To import the certificate, you can use `setupentrypoint.sh` scripts or executed custom code within the container process.</span></span> <span data-ttu-id="c9dcb-116">Ниже приведен пример кода C# для импорта PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-116">Sample code in C# for importing the PFX file follows:</span></span>

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
<span data-ttu-id="c9dcb-117">Этот PFX-сертификат можно использовать для проверки подлинности приложения или службы, а также для безопасного обмена данными с другими службами.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-117">This PFX certificate can be used for authenticate the application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="c9dcb-118">Настройка gMSA для контейнеров Windows</span><span class="sxs-lookup"><span data-stu-id="c9dcb-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="c9dcb-119">Чтобы настроить gMSA, необходимо разместить файл спецификаций учетных данных (`credspec`) на всех узлах в кластере.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-119">To set up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in the cluster.</span></span> <span data-ttu-id="c9dcb-120">Вы можете скопировать файл на все узлы, используя расширение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-120">The file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="c9dcb-121">Файл `credspec` должен содержать информацию об учетной записи gMSA.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-121">The `credspec` file must contain the gMSA account information.</span></span> <span data-ttu-id="c9dcb-122">Дополнительные сведения о файле `credspec` см. в статье [об учетных записях службы](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="c9dcb-122">For more information on the `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="c9dcb-123">Спецификация учетных данных и тег `Hostname` указаны в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-123">The credential specification and the `Hostname` tag are specified in the application manifest.</span></span> <span data-ttu-id="c9dcb-124">Тег `Hostname` должен соответствовать имени учетной записи gMSA, которая используется для запуска контейнера.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-124">The `Hostname` tag must match the gMSA account name that the container runs under.</span></span>  <span data-ttu-id="c9dcb-125">Тег `Hostname` позволяет контейнеру автоматически проходить проверку подлинности в других службах в домене с помощью проверки подлинности Kerberos.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-125">The `Hostname` tag allows the container to authenticate itself to other services in the domain using Kerberos authentication.</span></span>  <span data-ttu-id="c9dcb-126">В следующем фрагменте кода показан пример с указанием тегов `Hostname` и `credspec` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="c9dcb-126">A sample for specifying the `Hostname` and the `credspec` in the application manifest is shown in the following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="c9dcb-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9dcb-127">Next steps</span></span>

* [<span data-ttu-id="c9dcb-128">Развертывание контейнера Windows в Service Fabric на платформе Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c9dcb-128">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="c9dcb-129">Развертывание контейнера Docker в Service Fabric на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="c9dcb-129">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
