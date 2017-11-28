---
title: "Настройка безопасных подключений кластера Azure Service Fabric | Документация Майкрософт"
description: "Узнайте о том, как использовать Visual Studio для настройки безопасных подключений, поддерживаемых кластером Azure Service Fabric."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: dc07b2f38d6fd2de941ebbe99303f6e63cbf122d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-connections-to-a-service-fabric-cluster-from-visual-studio"></a><span data-ttu-id="e4c98-103">Настройка безопасных подключений к кластеру Service Fabric из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e4c98-103">Configure secure connections to a Service Fabric cluster from Visual Studio</span></span>
<span data-ttu-id="e4c98-104">Узнайте, как использовать Azure Visual Studio для безопасного доступа к кластеру Service Fabric с настроенной политикой контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e4c98-104">Learn how to use Visual Studio to securely access an Azure Service Fabric cluster with access control policies configured.</span></span>

## <a name="cluster-connection-types"></a><span data-ttu-id="e4c98-105">Типы подключения кластера</span><span class="sxs-lookup"><span data-stu-id="e4c98-105">Cluster connection types</span></span>
<span data-ttu-id="e4c98-106">Кластер Azure Service Fabric поддерживает два типа соединений: **небезопасные** соединения и безопасные соединения **на основе сертификата x509**.</span><span class="sxs-lookup"><span data-stu-id="e4c98-106">Two types of connections are supported by the Azure Service Fabric cluster: **non-secure** connections and **x509 certificate-based** secure connections.</span></span> <span data-ttu-id="e4c98-107">(Кластеры Service Fabric, размещенные локально, также поддерживают проверку подлинности **Windows** и **dSTS**.) Тип подключения кластера необходимо настроить при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="e4c98-107">(For Service Fabric clusters hosted on-premises, **Windows** and **dSTS** authentications are also supported.) You have to configure the cluster connection type when the cluster is being created.</span></span> <span data-ttu-id="e4c98-108">После создания изменить тип подключения нельзя.</span><span class="sxs-lookup"><span data-stu-id="e4c98-108">Once it's created, the connection type can’t be changed.</span></span>

<span data-ttu-id="e4c98-109">Средства Service Fabric Visual Studio поддерживают все типы проверки подлинности для подключения к кластеру для публикации.</span><span class="sxs-lookup"><span data-stu-id="e4c98-109">The Visual Studio Service Fabric tools support all authentication types for connecting to a cluster for publishing.</span></span> <span data-ttu-id="e4c98-110">Инструкции по настройке безопасного кластера Service Fabric см. в статье [Создание кластера Service Fabric в Azure с помощью портала Azure](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e4c98-110">See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for instructions on how to set up a secure Service Fabric cluster.</span></span>

## <a name="configure-cluster-connections-in-publish-profiles"></a><span data-ttu-id="e4c98-111">Настройка подключения кластера в профилях публикации</span><span class="sxs-lookup"><span data-stu-id="e4c98-111">Configure cluster connections in publish profiles</span></span>
<span data-ttu-id="e4c98-112">При публикации проекта Service Fabric из Visual Studio в диалоговом окне **Опубликовать приложение Service Fabric** можно выберите кластер Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e4c98-112">If you publish a Service Fabric project from Visual Studio, use the **Publish Service Fabric Application** dialog box to choose an Azure Service Fabric cluster.</span></span> <span data-ttu-id="e4c98-113">В разделе **Конечная точка подключения** выберите кластер в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="e4c98-113">Under **Connection endpoint**, select an existing cluster under your subscription.</span></span>

![Диалоговое окно **Опубликовать приложение Service Fabric** позволяет настроить подключение к Service Fabric.][publishdialog]

<span data-ttu-id="e4c98-115">В диалоговом окне **Опубликовать приложение Service Fabric** автоматически будет проверено подключение к кластеру.</span><span class="sxs-lookup"><span data-stu-id="e4c98-115">The **Publish Service Fabric Application** dialog box automatically validates the cluster connection.</span></span> <span data-ttu-id="e4c98-116">Если отобразится запрос на вход в учетную запись Azure, выполните его.</span><span class="sxs-lookup"><span data-stu-id="e4c98-116">If prompted, sign in to your Azure account.</span></span> <span data-ttu-id="e4c98-117">Если проверка проходит успешно, это означает, что в системе установлены необходимые сертификаты для безопасного подключения к кластеру или то, что кластер не является безопасным.</span><span class="sxs-lookup"><span data-stu-id="e4c98-117">If validation passes, it means that your system has the correct certificates installed to connect to the cluster securely, or your cluster is non-secure.</span></span> <span data-ttu-id="e4c98-118">Неудачный результат проверки может быть вызван проблемами с сетью или неправильной настройкой системы для безопасного подключения к кластеру.</span><span class="sxs-lookup"><span data-stu-id="e4c98-118">Validation failures can be caused by network issues or by not having your system correctly configured to connect to a secure cluster.</span></span>

![В диалоговом окне **Опубликовать приложение Service Fabric** проверяется имеющееся правильно настроенное подключение к кластеру Service Fabric.][selectsfcluster]

### <a name="to-connect-to-a-secure-cluster"></a><span data-ttu-id="e4c98-120">Безопасное подключение к кластеру</span><span class="sxs-lookup"><span data-stu-id="e4c98-120">To connect to a secure cluster</span></span>
1. <span data-ttu-id="e4c98-121">Убедитесь, что вам доступен один из клиентских сертификатов, которым доверяет целевой кластер.</span><span class="sxs-lookup"><span data-stu-id="e4c98-121">Make sure you can access one of the client certificates that the destination cluster trusts.</span></span> <span data-ttu-id="e4c98-122">Сертификат обычно распространяется в виде файла обмена персональной информацией (.pfx).</span><span class="sxs-lookup"><span data-stu-id="e4c98-122">The certificate is usually shared as a Personal Information Exchange (.pfx) file.</span></span> <span data-ttu-id="e4c98-123">Руководство по настройке доступа клиента к серверу см. в статье [Создание кластера Service Fabric в Azure с помощью портала Azure](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e4c98-123">See [Setting up a Service Fabric cluster from the Azure portal](service-fabric-cluster-creation-via-portal.md) for how to configure the server to grant access to a client.</span></span>
2. <span data-ttu-id="e4c98-124">Установите доверенный сертификат.</span><span class="sxs-lookup"><span data-stu-id="e4c98-124">Install the trusted certificate.</span></span> <span data-ttu-id="e4c98-125">Для этого дважды щелкните PFX-файл или импортируйте сертификаты с помощью сценария PowerShell PfxCertificate.</span><span class="sxs-lookup"><span data-stu-id="e4c98-125">To do this, double-click the .pfx file, or use the PowerShell script Import-PfxCertificate to import the certificates.</span></span> <span data-ttu-id="e4c98-126">Установите сертификат в каталог **Cert:\LocalMachine\My**.</span><span class="sxs-lookup"><span data-stu-id="e4c98-126">Install the certificate to **Cert:\LocalMachine\My**.</span></span> <span data-ttu-id="e4c98-127">При импорте сертификата можно принять все настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e4c98-127">It's OK to accept all default settings while importing the certificate.</span></span>
3. <span data-ttu-id="e4c98-128">Выберите **Опубликовать** в контекстном меню проекта, чтобы открыть диалоговое окно **Опубликовать приложение Azure**, а затем выберите целевой кластер.</span><span class="sxs-lookup"><span data-stu-id="e4c98-128">Choose the **Publish...** command on the shortcut menu of the project to open the **Publish Azure Application** dialog box and then select the target cluster.</span></span> <span data-ttu-id="e4c98-129">Средство автоматически разрешает подключение и сохраняет параметры безопасного подключения в профиле публикации.</span><span class="sxs-lookup"><span data-stu-id="e4c98-129">The tool automatically resolves the connection and saves the secure connection parameters in the publish profile.</span></span>
4. <span data-ttu-id="e4c98-130">Можно изменить профиль публикации, чтобы указать безопасное подключение к кластеру (необязательно).</span><span class="sxs-lookup"><span data-stu-id="e4c98-130">Optional: You can edit the publish profile to specify a secure cluster connection.</span></span>
   
   <span data-ttu-id="e4c98-131">Так как вы добавляете информацию о сертификате в XML-файл профиля публикации вручную, запишите имя хранилища сертификатов, расположение хранилища и отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="e4c98-131">Since you're manually editing the Publish Profile XML file to specify the certificate information, be sure to note the certificate store name, store location, and certificate thumbprint.</span></span> <span data-ttu-id="e4c98-132">Эти значения нужно будет указать в качестве имени и расположения хранилища сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e4c98-132">You'll need to provide these values for the certificate's store name and store location.</span></span> <span data-ttu-id="e4c98-133">Дополнительные сведения см. в статье [Практическое руководство. Извлечение отпечатка сертификата](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e4c98-133">See [How to: Retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) for more information.</span></span>
   
   <span data-ttu-id="e4c98-134">Параметры *ClusterConnectionParameters* позволяют задать параметры PowerShell для подключения к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e4c98-134">You can use the *ClusterConnectionParameters* parameters to specify the PowerShell parameters to use when connecting to the Service Fabric cluster.</span></span> <span data-ttu-id="e4c98-135">Допустимы все значения параметров, которые принимаются командлетом Connect-ServiceFabricCluster.</span><span class="sxs-lookup"><span data-stu-id="e4c98-135">Valid parameters are any that are accepted by the Connect-ServiceFabricCluster cmdlet.</span></span> <span data-ttu-id="e4c98-136">Список доступных параметров см. в статье [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4c98-136">See [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) for a list of available parameters.</span></span>
   
   <span data-ttu-id="e4c98-137">При публикации на удаленный кластер необходимо указать соответствующие параметры для этого конкретного кластера.</span><span class="sxs-lookup"><span data-stu-id="e4c98-137">If you’re publishing to a remote cluster, you need to specify the appropriate parameters for that specific cluster.</span></span> <span data-ttu-id="e4c98-138">Ниже приведен пример небезопасного подключения к кластеру:</span><span class="sxs-lookup"><span data-stu-id="e4c98-138">The following is an example of connecting to a non-secure cluster:</span></span>
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   <span data-ttu-id="e4c98-139">Ниже приведен пример для безопасного подключения к кластеру на основе сертификатов x509:</span><span class="sxs-lookup"><span data-stu-id="e4c98-139">Here’s an example for connecting to an x509 certificate-based secure cluster:</span></span>
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. <span data-ttu-id="e4c98-140">Измените другие необходимые параметры, такие как параметры обновления и расположение файла параметров приложения, и снова опубликуйте приложение из диалогового окна **Публикация приложения Service Fabric** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4c98-140">Edit any other necessary settings, such as upgrade parameters and Application Parameter file location, and then publish your application from the **Publish Service Fabric Application** dialog box in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4c98-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4c98-141">Next steps</span></span>
<span data-ttu-id="e4c98-142">Дополнительные сведения о доступе к кластерам Service Fabric см. в статье [Визуализация кластера с помощью Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e4c98-142">For more information about accessing Service Fabric clusters, see [Visualizing your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
