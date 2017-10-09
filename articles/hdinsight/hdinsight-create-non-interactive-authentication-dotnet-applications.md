---
title: "проверки подлинности неинтерактивной aaaCreate applciations .NET HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как приложения .NET HDInsight toocreate обычную проверку подлинности."
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
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="11b99-103">Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="11b99-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="11b99-104">Можно запустить приложение .NET Azure HDInsight (неинтерактивной) удостоверением приложения или удостоверением "hello" hello пользователя, выполнившего вход (интерактивные) приложения hello.</span><span class="sxs-lookup"><span data-stu-id="11b99-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="11b99-105">Образец hello интерактивных приложений см. в разделе [подключения tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="11b99-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="11b99-106">В этой статье показано, как toocreate неинтерактивной проверки подлинности .NET приложения tooconnect tooAzure и управления HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11b99-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="11b99-107">Из неинтерактивного приложения .NET, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="11b99-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="11b99-108">Идентификатор клиента для подписки Azure (то есть идентификатор каталога).</span><span class="sxs-lookup"><span data-stu-id="11b99-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="11b99-109">Дополнительные сведения см. в разделе [Получение идентификатора клиента](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="11b99-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="11b99-110">Идентификатор клиента приложения Azure Active Directory Hello.</span><span class="sxs-lookup"><span data-stu-id="11b99-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="11b99-111">Дополнительные сведения см. в разделах [Создание приложения Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) и [Получение идентификатора приложения и ключа проверки подлинности](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="11b99-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="11b99-112">Hello Azure Active Directory секретный ключ приложения.</span><span class="sxs-lookup"><span data-stu-id="11b99-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="11b99-113">Дополнительные сведения см. в разделе [Получение идентификатора приложения и ключа аутентификации](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="11b99-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11b99-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="11b99-114">Prerequisites</span></span>
* <span data-ttu-id="11b99-115">Кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11b99-115">HDInsight cluster.</span></span> <span data-ttu-id="11b99-116">Дополнительные сведения см. в [руководстве по началу работы](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="11b99-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="11b99-117">Назначьте toorole приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b99-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="11b99-118">Необходимо назначить tooa приложения hello [роли](../active-directory/role-based-access-built-in-roles.md) toogrant его разрешения для выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="11b99-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="11b99-119">Можно установить область hello на уровне hello hello подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="11b99-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="11b99-120">Hello разрешения, наследуемые toolower уровни области действия (например, Добавление роли модуля чтения toohello приложения для группы ресурсов значит, что возможно чтение группы ресурсов hello и все ресурсы, которые он содержит).</span><span class="sxs-lookup"><span data-stu-id="11b99-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="11b99-121">В этом учебнике будет настраивать hello область на уровне группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="11b99-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="11b99-122">Дополнительные сведения см. в разделе [использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="11b99-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="11b99-123">**hello tooadd приложения Azure AD toohello владельца роли**</span><span class="sxs-lookup"><span data-stu-id="11b99-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="11b99-124">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="11b99-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="11b99-125">Нажмите кнопку **группы ресурсов** hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="11b99-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="11b99-126">Щелкните группу ресурсов hello, содержащую hello кластера HDInsight, где будет выполняться запрос Hive далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="11b99-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="11b99-127">Если слишком много групп ресурсов, можно использовать фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="11b99-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="11b99-128">Нажмите кнопку **(IAM) управления доступом к** hello ресурсов группы меню.</span><span class="sxs-lookup"><span data-stu-id="11b99-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="11b99-129">Нажмите кнопку **добавить** из hello **пользователей** колонку.</span><span class="sxs-lookup"><span data-stu-id="11b99-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="11b99-130">Выполните hello инструкция tooadd hello **владельца** toohello роли приложения Azure AD, созданный в последней процедуре hello.</span><span class="sxs-lookup"><span data-stu-id="11b99-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="11b99-131">Если завершаются успешно, вы увидите, что приложения hello, перечисленных в колонке hello пользователи с ролью владельца hello.</span><span class="sxs-lookup"><span data-stu-id="11b99-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="11b99-132">Разработка клиентского приложения HDInsight</span><span class="sxs-lookup"><span data-stu-id="11b99-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="11b99-133">Создайте консольное приложение на C#.</span><span class="sxs-lookup"><span data-stu-id="11b99-133">Create a C# console application.</span></span>
2. <span data-ttu-id="11b99-134">Добавьте следующие пакеты Nuget hello:</span><span class="sxs-lookup"><span data-stu-id="11b99-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="11b99-135">Используйте следующий пример кода hello.</span><span class="sxs-lookup"><span data-stu-id="11b99-135">Use hello following code sample:</span></span>

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
                private static string secretKey = "<Enter hello Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
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

## <a name="next-steps"></a><span data-ttu-id="11b99-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11b99-136">Next steps</span></span>
* [<span data-ttu-id="11b99-137">Создание приложения Azure Active Directory и субъекта-службы с помощью портала</span><span class="sxs-lookup"><span data-stu-id="11b99-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="11b99-138">Проверка подлинности субъекта-службы в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="11b99-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="11b99-139">Управление доступом на основе ролей в Azure</span><span class="sxs-lookup"><span data-stu-id="11b99-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
