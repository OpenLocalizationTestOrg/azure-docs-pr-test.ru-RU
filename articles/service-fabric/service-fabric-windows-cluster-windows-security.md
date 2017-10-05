---
title: "Защита кластера, работающего под управлением Windows, с помощью системы безопасности Windows | Документация Майкрософт"
description: "Узнайте, как настроить безопасность обмена данными между узлами или между клиентом и узлом в изолированном кластере, работающем под управлением Windows, с помощью системы безопасности Windows."
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
ms.openlocfilehash: e093a631b0cf81195981a8e3d345504ebce02723
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="aaffa-103">Защита изолированного кластера под управлением Windows с помощью системы безопасности Windows</span><span class="sxs-lookup"><span data-stu-id="aaffa-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="aaffa-104">Чтобы предотвратить несанкционированный доступ к кластеру Service Fabric, его необходимо защитить.</span><span class="sxs-lookup"><span data-stu-id="aaffa-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span></span> <span data-ttu-id="aaffa-105">Безопасность особенно важна при выполнении в кластере производственных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="aaffa-105">Security is especially important when the cluster runs production workloads.</span></span> <span data-ttu-id="aaffa-106">В этой статье описывается, как настроить безопасность обмена данными между узлами или между клиентом и узлом с помощью системы безопасности Windows и файла *ClusterConfig.JSON*.</span><span class="sxs-lookup"><span data-stu-id="aaffa-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="aaffa-107">Описываемый процесс соответствует шагу по настройке безопасности из раздела [Создание изолированного кластера под управлением Windows Server](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="aaffa-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="aaffa-108">Дополнительные сведения об использовании системы безопасности Windows в Service Fabric см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="aaffa-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aaffa-109">Выбирать способ защиты обмена данными между узлами следует внимательно, так как один способ защиты кластера невозможно будет сменить на другой.</span><span class="sxs-lookup"><span data-stu-id="aaffa-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span></span> <span data-ttu-id="aaffa-110">Чтобы изменить способ защиты, потребуется заново создать весь кластер.</span><span class="sxs-lookup"><span data-stu-id="aaffa-110">To change the security selection, you have to rebuild the full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="aaffa-111">Настройка безопасности Windows с помощью групповой управляемой учетной записи службы</span><span class="sxs-lookup"><span data-stu-id="aaffa-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="aaffa-112">В примере файла конфигурации *ClusterConfig.gMSA.Windows.MultiMachine.JSON*, скачанном с пакетом автономного кластера [Microsoft.Azure.ServiceFabric.WindowsServer<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690), содержится шаблон для настройки безопасности Windows с помощью [групповой управляемой учетной записи службы](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="aaffa-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

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
  
| <span data-ttu-id="aaffa-113">**Параметр конфигурации**</span><span class="sxs-lookup"><span data-stu-id="aaffa-113">**Configuration Setting**</span></span> | <span data-ttu-id="aaffa-114">**Описание**</span><span class="sxs-lookup"><span data-stu-id="aaffa-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="aaffa-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="aaffa-115">WindowsIdentities</span></span> |<span data-ttu-id="aaffa-116">Содержит удостоверения кластера и клиента.</span><span class="sxs-lookup"><span data-stu-id="aaffa-116">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="aaffa-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="aaffa-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="aaffa-118">Настраивает безопасность обмена данными между узлами.</span><span class="sxs-lookup"><span data-stu-id="aaffa-118">Configures node-to-node security.</span></span> <span data-ttu-id="aaffa-119">Групповая управляемая учетная запись службы.</span><span class="sxs-lookup"><span data-stu-id="aaffa-119">A group managed service account.</span></span> |  
| <span data-ttu-id="aaffa-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="aaffa-120">ClusterSPN</span></span> |<span data-ttu-id="aaffa-121">Полное доменное имя субъекта-службы для групповой управляемой учетной записи службы</span><span class="sxs-lookup"><span data-stu-id="aaffa-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="aaffa-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="aaffa-122">ClientIdentities</span></span> |<span data-ttu-id="aaffa-123">Настраивает безопасность обмена данными между клиентами и узлами.</span><span class="sxs-lookup"><span data-stu-id="aaffa-123">Configures client-to-node security.</span></span> <span data-ttu-id="aaffa-124">Массив учетных записей клиентов.</span><span class="sxs-lookup"><span data-stu-id="aaffa-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="aaffa-125">Удостоверение</span><span class="sxs-lookup"><span data-stu-id="aaffa-125">Identity</span></span> |<span data-ttu-id="aaffa-126">Удостоверение клиента, пользователь домена.</span><span class="sxs-lookup"><span data-stu-id="aaffa-126">The client identity, a domain user.</span></span> |  
| <span data-ttu-id="aaffa-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="aaffa-127">IsAdmin</span></span> |<span data-ttu-id="aaffa-128">Значение true указывает, что у пользователя домена есть клиентский доступ с правами администратора, а значение false — клиентский доступ с правами пользователя.</span><span class="sxs-lookup"><span data-stu-id="aaffa-128">True specifies that the domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="aaffa-129">[Безопасный обмен данными между узлами](service-fabric-cluster-security.md#node-to-node-security) можно настроить с помощью параметра **ClustergMSAIdentity**, когда Service Fabric необходимо использовать групповую управляемую учетную запись службы.</span><span class="sxs-lookup"><span data-stu-id="aaffa-129">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span></span> <span data-ttu-id="aaffa-130">Чтобы создать отношения доверия между узлами, им нужно сообщить друг о друге.</span><span class="sxs-lookup"><span data-stu-id="aaffa-130">In order to build trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="aaffa-131">Это можно сделать двумя разными способами: указав групповую управляемую учетную запись службы, которая включает все узлы в кластере, или указав группу компьютеров домена, которая включает все узлы в кластере.</span><span class="sxs-lookup"><span data-stu-id="aaffa-131">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span></span> <span data-ttu-id="aaffa-132">Настоятельно рекомендуем применять подход с использованием [групповой управляемой учетной записи службы](https://technet.microsoft.com/library/hh831782.aspx), в частности для больших кластеров (более 10 узлов) или для кластеров, размер которых может изменяться.</span><span class="sxs-lookup"><span data-stu-id="aaffa-132">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span></span>  
<span data-ttu-id="aaffa-133">Кроме того, этот подход не требует создания группы домена, администраторам кластера которой были предоставлены права доступа для добавления и удаления участников.</span><span class="sxs-lookup"><span data-stu-id="aaffa-133">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span></span> <span data-ttu-id="aaffa-134">Эти учетные записи также можно использовать для автоматического управления паролями.</span><span class="sxs-lookup"><span data-stu-id="aaffa-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="aaffa-135">Дополнительные сведения см. в статье [Начало работы с групповыми управляемыми учетными записями служб](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="aaffa-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="aaffa-136">[Безопасность обмена данными между клиентом и узлом](service-fabric-cluster-security.md#client-to-node-security) настраивается с помощью параметра **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="aaffa-136">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="aaffa-137">Чтобы установить отношение доверия между клиентом и кластером, необходимо настроить кластер таким образом, чтобы ему были известны удостоверения клиентов, которым можно доверять.</span><span class="sxs-lookup"><span data-stu-id="aaffa-137">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span></span> <span data-ttu-id="aaffa-138">Это можно сделать двумя разными способами: указав пользователей группы домена или узла домена, которые могут подключаться.</span><span class="sxs-lookup"><span data-stu-id="aaffa-138">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span></span> <span data-ttu-id="aaffa-139">Service Fabric поддерживает два разных типа контроля доступа для клиентов, подключенных к кластеру Service Fabric: администраторский и пользовательский.</span><span class="sxs-lookup"><span data-stu-id="aaffa-139">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="aaffa-140">Благодаря контролю доступа администратор кластера может ограничить доступ разных групп пользователей на выполнение определенных типов операций в кластере, повысив тем самым уровень безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="aaffa-140">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span></span>  <span data-ttu-id="aaffa-141">Администраторы имеют полный доступ к возможностям управления (включая возможности чтения и записи).</span><span class="sxs-lookup"><span data-stu-id="aaffa-141">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="aaffa-142">Пользователи по умолчанию имеют доступ только на чтение для управления (например, при работе с запросами) и возможность разрешения приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="aaffa-142">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span> <span data-ttu-id="aaffa-143">Дополнительные сведения о ролях доступа см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="aaffa-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="aaffa-144">В следующем примере раздела **security** настраивается безопасность Windows с помощью групповой управляемой учетной записи службы и указывается, что компьютеры в группе *ServiceFabric/clusterA.contoso.com* — это часть кластера, а также что у *CONTOSO\usera* есть клиентский доступ с правами администратора:</span><span class="sxs-lookup"><span data-stu-id="aaffa-144">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
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
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="aaffa-145">Настройка безопасности Windows с использованием группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="aaffa-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="aaffa-146">В примере файла конфигурации *ClusterConfig.Windows.MultiMachine.JSON*, скачанном с пакетом автономного кластера [Microsoft.Azure.ServiceFabric.WindowsServer<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690), содержится шаблон для настройки безопасности Windows.</span><span class="sxs-lookup"><span data-stu-id="aaffa-146">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="aaffa-147">Безопасность Windows настраивается в разделе **Properties** .</span><span class="sxs-lookup"><span data-stu-id="aaffa-147">Windows security is configured in the **Properties** section:</span></span> 

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

| <span data-ttu-id="aaffa-148">**Параметр конфигурации**</span><span class="sxs-lookup"><span data-stu-id="aaffa-148">**Configuration setting**</span></span> | <span data-ttu-id="aaffa-149">**Описание**</span><span class="sxs-lookup"><span data-stu-id="aaffa-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="aaffa-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="aaffa-150">ClusterCredentialType</span></span> |<span data-ttu-id="aaffa-151">Для параметра **ClusterCredentialType** задано значение *Windows*, если ClusterIdentity указывает имя группы компьютеров Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aaffa-151">**ClusterCredentialType** is set to *Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="aaffa-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="aaffa-152">ServerCredentialType</span></span> |<span data-ttu-id="aaffa-153">Задайте значение *Windows*, чтобы включить систему безопасности Windows для клиентов.</span><span class="sxs-lookup"><span data-stu-id="aaffa-153">Set to *Windows* to enable Windows security for clients.</span></span><br /><br /><span data-ttu-id="aaffa-154">Это указывает, что клиенты кластера и сам кластер работают внутри домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aaffa-154">This indicates that the clients of the cluster and the cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="aaffa-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="aaffa-155">WindowsIdentities</span></span> |<span data-ttu-id="aaffa-156">Содержит удостоверения кластера и клиента.</span><span class="sxs-lookup"><span data-stu-id="aaffa-156">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="aaffa-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="aaffa-157">ClusterIdentity</span></span> |<span data-ttu-id="aaffa-158">Используйте имя группы компьютеров "домен\группа_компьютеров", чтобы настроить защиту обмена данными между узлами.</span><span class="sxs-lookup"><span data-stu-id="aaffa-158">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span></span> |  
| <span data-ttu-id="aaffa-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="aaffa-159">ClientIdentities</span></span> |<span data-ttu-id="aaffa-160">Настраивает безопасность обмена данными между клиентами и узлами.</span><span class="sxs-lookup"><span data-stu-id="aaffa-160">Configures client-to-node security.</span></span> <span data-ttu-id="aaffa-161">Массив учетных записей клиентов.</span><span class="sxs-lookup"><span data-stu-id="aaffa-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="aaffa-162">Удостоверение</span><span class="sxs-lookup"><span data-stu-id="aaffa-162">Identity</span></span> |<span data-ttu-id="aaffa-163">Добавьте пользователя домена "домен\имя_пользователя" для удостоверения клиента.</span><span class="sxs-lookup"><span data-stu-id="aaffa-163">Add the domain user, domain\username, for the client identity.</span></span> |  
| <span data-ttu-id="aaffa-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="aaffa-164">IsAdmin</span></span> |<span data-ttu-id="aaffa-165">Задайте значение true, чтобы указать, что у пользователя домена есть клиентский доступ с правами администратора, или значение false, чтобы указать наличие клиентского доступа с правами пользователя.</span><span class="sxs-lookup"><span data-stu-id="aaffa-165">Set to true to specify that the domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="aaffa-166">[Безопасный обмен данными между узлами](service-fabric-cluster-security.md#node-to-node-security) можно настроить с помощью параметра **ClusterIdentity**, если вы хотите использовать группу компьютеров в домене Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aaffa-166">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="aaffa-167">Дополнительные сведения см. в статье [How to Create a Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx) (Как создать группу компьютеров в Active Directory).</span><span class="sxs-lookup"><span data-stu-id="aaffa-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="aaffa-168">[Защиту обмена данными между клиентом и узлом](service-fabric-cluster-security.md#client-to-node-security) можно настроить с помощью параметра **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="aaffa-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="aaffa-169">Чтобы установить отношения доверия между клиентом и кластером, необходимо настроить кластер таким образом, чтобы ему были известны удостоверения клиентов, которым можно доверять.</span><span class="sxs-lookup"><span data-stu-id="aaffa-169">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span></span> <span data-ttu-id="aaffa-170">Установить отношения доверия можно двумя разными способами:</span><span class="sxs-lookup"><span data-stu-id="aaffa-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="aaffa-171">указать пользователей группы домена, которые могут подключаться;</span><span class="sxs-lookup"><span data-stu-id="aaffa-171">Specify the domain group users that can connect.</span></span>
- <span data-ttu-id="aaffa-172">указать пользователей узла домена, которые могут подключаться.</span><span class="sxs-lookup"><span data-stu-id="aaffa-172">Specify the domain node users that can connect.</span></span>

<span data-ttu-id="aaffa-173">Service Fabric поддерживает два разных типа контроля доступа для клиентов, подключенных к кластеру Service Fabric: администраторский и пользовательский.</span><span class="sxs-lookup"><span data-stu-id="aaffa-173">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="aaffa-174">Благодаря контролю доступа администратор кластера может ограничить доступ разных групп пользователей к операциям определенных типов в кластере, повысив тем самым уровень его безопасности.</span><span class="sxs-lookup"><span data-stu-id="aaffa-174">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span></span>  <span data-ttu-id="aaffa-175">Администраторы имеют полный доступ к возможностям управления (включая возможности чтения и записи).</span><span class="sxs-lookup"><span data-stu-id="aaffa-175">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="aaffa-176">Пользователи по умолчанию имеют доступ только на чтение для управления (например, при работе с запросами) и возможность разрешения приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="aaffa-176">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>  

<span data-ttu-id="aaffa-177">В следующем примере раздела **security** настраивается система безопасности Windows и указывается, что компьютеры в *ServiceFabric/clusterA.contoso.com* — это часть кластера, а также что у *CONTOSO\usera* есть клиентский доступ с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="aaffa-177">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

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
> <span data-ttu-id="aaffa-178">Службу Service Fabric не нужно развертывать на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="aaffa-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="aaffa-179">Убедитесь, что ClusterConfig.json не содержит IP-адрес контроллера домена, если вы используете группы компьютеров или группу управляемых учетных записей службы (gMSA).</span><span class="sxs-lookup"><span data-stu-id="aaffa-179">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="aaffa-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaffa-180">Next steps</span></span>
<span data-ttu-id="aaffa-181">После настройки безопасности Windows в файле *ClusterConfig.JSON* возобновите процесс создания кластера, который описан в разделе [Создание кластера под управлением Windows Server и управление им](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="aaffa-181">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="aaffa-182">Дополнительные сведения о защите обмена данными между узлами, между клиентом и узлом и об управлении доступом на основе ролей см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="aaffa-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="aaffa-183">Примеры подключений с помощью PowerShell или FabricClient см. в статье [Безопасное подключение к кластеру без AAD](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="aaffa-183">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
