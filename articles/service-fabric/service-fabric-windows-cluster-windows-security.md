---
title: "aaaSecure в кластер, запущенный в Windows с помощью средств безопасности Windows | Документы Microsoft"
description: "Узнайте, как tooconfigure на автономный узел узел и узел клиента безопасности кластера под управлением Windows с помощью средств безопасности Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="cfba9-103">Защита изолированного кластера под управлением Windows с помощью системы безопасности Windows</span><span class="sxs-lookup"><span data-stu-id="cfba9-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="cfba9-104">tooprevent несанкционированный доступ кластера Service Fabric tooa, необходимо обеспечить безопасность кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cfba9-104">tooprevent unauthorized access tooa Service Fabric cluster, you must secure hello cluster.</span></span> <span data-ttu-id="cfba9-105">Безопасность особенно важна, запускаемый рабочих нагрузок кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cfba9-105">Security is especially important when hello cluster runs production workloads.</span></span> <span data-ttu-id="cfba9-106">В этой статье описывается как tooconfigure безопасности узла на узел и узел клиента с помощью системы безопасности Windows в hello *ClusterConfig.JSON* файла.</span><span class="sxs-lookup"><span data-stu-id="cfba9-106">This article describes how tooconfigure node-to-node and client-to-node security by using Windows security in hello *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="cfba9-107">процесс Hello соответствует toohello настройки безопасности шага [создать автономный кластер, запущенный в Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="cfba9-107">hello process corresponds toohello configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="cfba9-108">Дополнительные сведения об использовании системы безопасности Windows в Service Fabric см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="cfba9-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cfba9-109">Выбор hello безопасности узла на узел следует внимательно рассмотреть так существует не поддерживается обновление кластера из одного tooanother Выбор безопасности.</span><span class="sxs-lookup"><span data-stu-id="cfba9-109">You should consider hello selection of node-to-node security carefully because there is no cluster upgrade from one security choice tooanother.</span></span> <span data-ttu-id="cfba9-110">Выбор безопасности toochange hello, у вас есть полный кластера toorebuild hello.</span><span class="sxs-lookup"><span data-stu-id="cfba9-110">toochange hello security selection, you have toorebuild hello full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="cfba9-111">Настройка безопасности Windows с помощью групповой управляемой учетной записи службы</span><span class="sxs-lookup"><span data-stu-id="cfba9-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="cfba9-112">Образец Hello *ClusterConfig.gMSA.Windows.MultiMachine.JSON* загрузить файл конфигурации с hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. Почтовый](http://go.microsoft.com/fwlink/?LinkId=730690) изолированный пакет кластера содержит шаблон для настройки безопасности Windows с помощью [групповой управляемой учетной записи службы (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="cfba9-112">hello sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="cfba9-113">**Параметр конфигурации**</span><span class="sxs-lookup"><span data-stu-id="cfba9-113">**Configuration Setting**</span></span> | <span data-ttu-id="cfba9-114">**Описание**</span><span class="sxs-lookup"><span data-stu-id="cfba9-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="cfba9-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="cfba9-115">WindowsIdentities</span></span> |<span data-ttu-id="cfba9-116">Содержит идентификаторы hello кластера и клиента.</span><span class="sxs-lookup"><span data-stu-id="cfba9-116">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="cfba9-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="cfba9-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="cfba9-118">Настраивает безопасность обмена данными между узлами.</span><span class="sxs-lookup"><span data-stu-id="cfba9-118">Configures node-to-node security.</span></span> <span data-ttu-id="cfba9-119">Групповая управляемая учетная запись службы.</span><span class="sxs-lookup"><span data-stu-id="cfba9-119">A group managed service account.</span></span> |  
| <span data-ttu-id="cfba9-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="cfba9-120">ClusterSPN</span></span> |<span data-ttu-id="cfba9-121">Полное доменное имя субъекта-службы для групповой управляемой учетной записи службы</span><span class="sxs-lookup"><span data-stu-id="cfba9-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="cfba9-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="cfba9-122">ClientIdentities</span></span> |<span data-ttu-id="cfba9-123">Настраивает безопасность обмена данными между клиентами и узлами.</span><span class="sxs-lookup"><span data-stu-id="cfba9-123">Configures client-to-node security.</span></span> <span data-ttu-id="cfba9-124">Массив учетных записей клиентов.</span><span class="sxs-lookup"><span data-stu-id="cfba9-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="cfba9-125">Удостоверение</span><span class="sxs-lookup"><span data-stu-id="cfba9-125">Identity</span></span> |<span data-ttu-id="cfba9-126">удостоверение клиента Hello, пользователя домена.</span><span class="sxs-lookup"><span data-stu-id="cfba9-126">hello client identity, a domain user.</span></span> |  
| <span data-ttu-id="cfba9-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="cfba9-127">IsAdmin</span></span> |<span data-ttu-id="cfba9-128">Значение true указывает, что пользователь домена hello не клиентского доступа администратора, false для клиентского доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfba9-128">True specifies that hello domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="cfba9-129">[Узел безопасности toonode](service-fabric-cluster-security.md#node-to-node-security) настроить, задав **ClustergMSAIdentity** структуры службы, когда потребуется toorun под групповой управляемой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cfba9-129">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs toorun under gMSA.</span></span> <span data-ttu-id="cfba9-130">В порядке toobuild отношений доверия между узлами они должны быть в курсе друг с другом.</span><span class="sxs-lookup"><span data-stu-id="cfba9-130">In order toobuild trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="cfba9-131">Это можно сделать двумя способами: указать hello группы управляемых учетных записей служб, включающий все узлы в кластере hello или группу домена машины hello, которая включает все узлы в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="cfba9-131">This can be accomplished in two different ways: Specify hello Group Managed Service Account that includes all nodes in hello cluster or Specify hello domain machine group that includes all nodes in hello cluster.</span></span> <span data-ttu-id="cfba9-132">Настоятельно рекомендуется использовать hello [групповой управляемой учетной записи службы (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) подход, особенно для больших кластеров (более 10 узлов) или для кластеров, которые, скорее всего, toogrow или сжатия.</span><span class="sxs-lookup"><span data-stu-id="cfba9-132">We strongly recommend using hello [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely toogrow or shrink.</span></span>  
<span data-ttu-id="cfba9-133">Этот подход не требует создания hello группы домена, для которого администратор кластера были предоставлены tooadd права доступа и удалять элементы.</span><span class="sxs-lookup"><span data-stu-id="cfba9-133">This approach does not require hello creation of a domain group for which cluster administrators have been granted access rights tooadd and remove members.</span></span> <span data-ttu-id="cfba9-134">Эти учетные записи также можно использовать для автоматического управления паролями.</span><span class="sxs-lookup"><span data-stu-id="cfba9-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="cfba9-135">Дополнительные сведения см. в статье [Начало работы с групповыми управляемыми учетными записями служб](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfba9-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="cfba9-136">[Клиент toonode безопасности](service-fabric-cluster-security.md#client-to-node-security) настраивается с помощью **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="cfba9-136">[Client toonode security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="cfba9-137">В порядке tooestablish отношения доверия между клиентом и hello кластера необходимо настроить tooknow кластера hello идентификаторы, которые клиент, он может доверять.</span><span class="sxs-lookup"><span data-stu-id="cfba9-137">In order tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow which client identities that it can trust.</span></span> <span data-ttu-id="cfba9-138">Это можно сделать двумя способами: указать hello пользователи группы домена, можно подключиться, или указать hello узел пользователей домена, которые могут подключаться.</span><span class="sxs-lookup"><span data-stu-id="cfba9-138">This can be done in two different ways: Specify hello domain group users that can connect or specify hello domain node users that can connect.</span></span> <span data-ttu-id="cfba9-139">Service Fabric поддерживает два типа элемента управления различный уровень доступа для клиентов, подключенных tooa кластера Service Fabric: администратора и пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfba9-139">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="cfba9-140">Управление доступом предоставляет возможность hello hello кластера администратора toolimit доступа toocertain типы операций кластера для разных групп пользователей, повышение безопасности кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cfba9-140">Access control provides hello ability for hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, making hello cluster more secure.</span></span>  <span data-ttu-id="cfba9-141">Администраторы имеют полный доступ toomanagement возможности (включая возможности чтения и записи).</span><span class="sxs-lookup"><span data-stu-id="cfba9-141">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="cfba9-142">Пользователи, по умолчанию имеют только доступ на чтение toomanagement возможности (например, возможности работы с запросами), hello возможность tooresolve, приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="cfba9-142">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span> <span data-ttu-id="cfba9-143">Дополнительные сведения о ролях доступа см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="cfba9-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="cfba9-144">Hello в следующем примере **безопасности** раздел настраивает безопасность Windows, с помощью управляемой и указывает, что hello компьютеров в *ServiceFabric.clusterA.contoso.com* gMSA являются частью кластера hello и что *CONTOSO\usera* имеет доступ администратора клиента:</span><span class="sxs-lookup"><span data-stu-id="cfba9-144">hello following example **security** section configures Windows security using gMSA and specifies that hello machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of hello cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="cfba9-145">Настройка безопасности Windows с использованием группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="cfba9-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="cfba9-146">Образец Hello *ClusterConfig.Windows.MultiMachine.JSON* загрузить файл конфигурации с hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. Почтовый](http://go.microsoft.com/fwlink/?LinkId=730690) изолированный пакет кластера содержит шаблон для настройки безопасности Windows.</span><span class="sxs-lookup"><span data-stu-id="cfba9-146">hello sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="cfba9-147">Безопасность Windows настраивается в hello **свойства** раздела:</span><span class="sxs-lookup"><span data-stu-id="cfba9-147">Windows security is configured in hello **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="cfba9-148">**Параметр конфигурации**</span><span class="sxs-lookup"><span data-stu-id="cfba9-148">**Configuration setting**</span></span> | <span data-ttu-id="cfba9-149">**Описание**</span><span class="sxs-lookup"><span data-stu-id="cfba9-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="cfba9-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="cfba9-150">ClusterCredentialType</span></span> |<span data-ttu-id="cfba9-151">**ClusterCredentialType** задано слишком*Windows* Если ClusterIdentity указывает имя группы компьютеров Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cfba9-151">**ClusterCredentialType** is set too*Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="cfba9-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="cfba9-152">ServerCredentialType</span></span> |<span data-ttu-id="cfba9-153">Значение слишком*Windows* tooenable безопасности Windows для клиентов.</span><span class="sxs-lookup"><span data-stu-id="cfba9-153">Set too*Windows* tooenable Windows security for clients.</span></span><br /><br /><span data-ttu-id="cfba9-154">Это означает, что выполнение клиентов hello hello кластера и самого кластера hello в домене Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cfba9-154">This indicates that hello clients of hello cluster and hello cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="cfba9-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="cfba9-155">WindowsIdentities</span></span> |<span data-ttu-id="cfba9-156">Содержит идентификаторы hello кластера и клиента.</span><span class="sxs-lookup"><span data-stu-id="cfba9-156">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="cfba9-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="cfba9-157">ClusterIdentity</span></span> |<span data-ttu-id="cfba9-158">Используйте имя группы компьютеров, domain\machinegroup, tooconfigure безопасности узла на узел.</span><span class="sxs-lookup"><span data-stu-id="cfba9-158">Use a machine group name, domain\machinegroup, tooconfigure node-to-node security.</span></span> |  
| <span data-ttu-id="cfba9-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="cfba9-159">ClientIdentities</span></span> |<span data-ttu-id="cfba9-160">Настраивает безопасность обмена данными между клиентами и узлами.</span><span class="sxs-lookup"><span data-stu-id="cfba9-160">Configures client-to-node security.</span></span> <span data-ttu-id="cfba9-161">Массив учетных записей клиентов.</span><span class="sxs-lookup"><span data-stu-id="cfba9-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="cfba9-162">Удостоверение</span><span class="sxs-lookup"><span data-stu-id="cfba9-162">Identity</span></span> |<span data-ttu-id="cfba9-163">Добавьте пользователя домена hello домен\имя пользователя для удостоверения клиента hello.</span><span class="sxs-lookup"><span data-stu-id="cfba9-163">Add hello domain user, domain\username, for hello client identity.</span></span> |  
| <span data-ttu-id="cfba9-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="cfba9-164">IsAdmin</span></span> |<span data-ttu-id="cfba9-165">Набор tootrue toospecify, hello пользователя домена имеет доступ администратора клиента или false для клиентского доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfba9-165">Set tootrue toospecify that hello domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="cfba9-166">[Узел безопасности toonode](service-fabric-cluster-security.md#node-to-node-security) настраивается с помощью параметра **ClusterIdentity** Если toouse группу компьютеров в домене Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cfba9-166">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want toouse a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="cfba9-167">Дополнительные сведения см. в статье [How to Create a Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx) (Как создать группу компьютеров в Active Directory).</span><span class="sxs-lookup"><span data-stu-id="cfba9-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="cfba9-168">[Защиту обмена данными между клиентом и узлом](service-fabric-cluster-security.md#client-to-node-security) можно настроить с помощью параметра **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="cfba9-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="cfba9-169">tooestablish доверие между клиентом и hello кластера, необходимо настроить клиент hello tooknow кластера hello, можно доверять удостоверений, которые hello кластера.</span><span class="sxs-lookup"><span data-stu-id="cfba9-169">tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow hello client identities that hello cluster can trust.</span></span> <span data-ttu-id="cfba9-170">Установить отношения доверия можно двумя разными способами:</span><span class="sxs-lookup"><span data-stu-id="cfba9-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="cfba9-171">Укажите пользователи группы домена hello, которые могут подключаться.</span><span class="sxs-lookup"><span data-stu-id="cfba9-171">Specify hello domain group users that can connect.</span></span>
- <span data-ttu-id="cfba9-172">Укажите узел пользователи hello домена, которые могут подключаться.</span><span class="sxs-lookup"><span data-stu-id="cfba9-172">Specify hello domain node users that can connect.</span></span>

<span data-ttu-id="cfba9-173">Service Fabric поддерживает два типа элемента управления различный уровень доступа для клиентов, подключенных tooa кластера Service Fabric: администратора и пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfba9-173">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="cfba9-174">Контроль доступа позволяет hello кластера администратора toolimit доступа toocertain типы операций кластера для разных групп пользователей, что делает более безопасные hello кластера.</span><span class="sxs-lookup"><span data-stu-id="cfba9-174">Access control enables hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, which makes hello cluster more secure.</span></span>  <span data-ttu-id="cfba9-175">Администраторы имеют полный доступ toomanagement возможности (включая возможности чтения и записи).</span><span class="sxs-lookup"><span data-stu-id="cfba9-175">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="cfba9-176">Пользователи, по умолчанию имеют только доступ на чтение toomanagement возможности (например, возможности работы с запросами), hello возможность tooresolve, приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="cfba9-176">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>  

<span data-ttu-id="cfba9-177">Hello в следующем примере **безопасности** раздел, предназначенный для настройки безопасности Windows, указывает, что hello компьютеров в *ServiceFabric/clusterA.contoso.com* являются частью кластера hello и указывает, что  *CONTOSO\usera* имеет доступ администратора клиента:</span><span class="sxs-lookup"><span data-stu-id="cfba9-177">hello following example **security** section configures Windows security, specifies that hello machines in *ServiceFabric/clusterA.contoso.com* are part of hello cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="cfba9-178">Службу Service Fabric не нужно развертывать на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="cfba9-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="cfba9-179">Убедитесь в том, что ClusterConfig.json не включать hello IP-адрес контроллера домена hello, при использовании группу компьютеров или группы управляемой учетной записи службы (gMSA).</span><span class="sxs-lookup"><span data-stu-id="cfba9-179">Make sure that ClusterConfig.json does not include hello IP address of hello domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="cfba9-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfba9-180">Next steps</span></span>
<span data-ttu-id="cfba9-181">После настройки безопасности Windows в hello *ClusterConfig.JSON* файла, возобновить процесс создания кластера hello в [создать автономный кластер, запущенный в Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="cfba9-181">After configuring Windows security in hello *ClusterConfig.JSON* file, resume hello cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="cfba9-182">Дополнительные сведения о защите обмена данными между узлами, между клиентом и узлом и об управлении доступом на основе ролей см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="cfba9-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="cfba9-183">В разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md) примеры соединения с помощью PowerShell или FabricClient.</span><span class="sxs-lookup"><span data-stu-id="cfba9-183">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
