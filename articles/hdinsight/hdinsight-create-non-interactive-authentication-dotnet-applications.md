---
title: "Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности в Azure | Документы Майкрософт"
description: "Узнайте, как создавать приложения .NET HDInsight с неинтерактивной проверкой подлинности."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="ee3a4-103">Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="ee3a4-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="ee3a4-104">Приложение .NET Azure HDInsight можно запустить с помощью его собственного удостоверения (неинтерактивный режим) или удостоверения пользователя, вошедшего в приложение (интерактивный режим).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="ee3a4-105">Пример интерактивного приложения см. в разделе [Подключение к Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="ee3a4-106">В этой статье описано, как создать приложение .NET с неинтерактивной аутентификацией для подключения к Azure и управления HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="ee3a4-107">Из неинтерактивного приложения .NET, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="ee3a4-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="ee3a4-108">Идентификатор клиента для подписки Azure (то есть идентификатор каталога).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="ee3a4-109">Дополнительные сведения см. в разделе [Получение идентификатора клиента](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="ee3a4-110">Идентификатор клиента для приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="ee3a4-111">Дополнительные сведения см. в разделах [Создание приложения Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) и [Получение идентификатора приложения и ключа проверки подлинности](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="ee3a4-112">Секретный ключ для приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="ee3a4-113">Дополнительные сведения см. в разделе [Получение идентификатора приложения и ключа аутентификации](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee3a4-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ee3a4-114">Prerequisites</span></span>
* <span data-ttu-id="ee3a4-115">Кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-115">HDInsight cluster.</span></span> <span data-ttu-id="ee3a4-116">Дополнительные сведения см. в [руководстве по началу работы](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="ee3a4-117">Назначение приложения Azure AD роли</span><span class="sxs-lookup"><span data-stu-id="ee3a4-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="ee3a4-118">Необходимо назначить приложение [роли](../active-directory/role-based-access-built-in-roles.md) , чтобы предоставить ему разрешения для выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="ee3a4-119">Вы можете задать область действия на уровне подписки, группы ресурсов или ресурса.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="ee3a4-120">Разрешения наследуются на более низких уровнях области действия (например, добавление приложения в роль читателя для группы ресурсов означает, что оно может считывать группу ресурсов и все содержащиеся в ней ресурсы).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="ee3a4-121">В этом учебнике описано, как задать область действия на уровне группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="ee3a4-122">Дополнительные сведения см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="ee3a4-123">**Добавление роли владельца в приложение Azure AD**</span><span class="sxs-lookup"><span data-stu-id="ee3a4-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="ee3a4-124">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee3a4-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ee3a4-125">Щелкните **Группа ресурсов** на левой панели.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="ee3a4-126">Выберите группу ресурсов с кластером HDInsight, где позднее будет выполняться ваш запрос Hive.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="ee3a4-127">Если имеется слишком много групп ресурсов, можно использовать фильтр.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="ee3a4-128">В меню группы ресурсов щелкните **Управление доступом (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="ee3a4-129">В колонке **Пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="ee3a4-130">Следуйте инструкциям, чтобы добавить роль **Владелец** в приложение Azure AD, созданное в предыдущей процедуре.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="ee3a4-131">После успешного выполнения этой процедуры приложение должно появиться в колонке "Пользователи" с ролью "Владелец".</span><span class="sxs-lookup"><span data-stu-id="ee3a4-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="ee3a4-132">Разработка клиентского приложения HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee3a4-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="ee3a4-133">Создайте консольное приложение на C#.</span><span class="sxs-lookup"><span data-stu-id="ee3a4-133">Create a C# console application.</span></span>
2. <span data-ttu-id="ee3a4-134">Добавьте следующие пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="ee3a4-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="ee3a4-135">Используйте следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="ee3a4-135">Use the following code sample:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter the Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a><span data-ttu-id="ee3a4-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee3a4-136">Next steps</span></span>
* [<span data-ttu-id="ee3a4-137">Создание приложения Azure Active Directory и субъекта-службы с помощью портала</span><span class="sxs-lookup"><span data-stu-id="ee3a4-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="ee3a4-138">Проверка подлинности субъекта-службы в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee3a4-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="ee3a4-139">Управление доступом на основе ролей в Azure</span><span class="sxs-lookup"><span data-stu-id="ee3a4-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
