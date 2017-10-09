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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности
Можно запустить приложение .NET Azure HDInsight (неинтерактивной) удостоверением приложения или удостоверением "hello" hello пользователя, выполнившего вход (интерактивные) приложения hello. Образец hello интерактивных приложений см. в разделе [подключения tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). В этой статье показано, как toocreate неинтерактивной проверки подлинности .NET приложения tooconnect tooAzure и управления HDInsight.

Из неинтерактивного приложения .NET, вам потребуется следующее:

* Идентификатор клиента для подписки Azure (то есть идентификатор каталога). Дополнительные сведения см. в разделе [Получение идентификатора клиента](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* Идентификатор клиента приложения Azure Active Directory Hello. Дополнительные сведения см. в разделах [Создание приложения Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) и [Получение идентификатора приложения и ключа проверки подлинности](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).
* Hello Azure Active Directory секретный ключ приложения. Дополнительные сведения см. в разделе [Получение идентификатора приложения и ключа аутентификации](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

## <a name="prerequisites"></a>Предварительные требования
* Кластер HDInsight. Дополнительные сведения см. в [руководстве по началу работы](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-toorole"></a>Назначьте toorole приложения Azure AD
Необходимо назначить tooa приложения hello [роли](../active-directory/role-based-access-built-in-roles.md) toogrant его разрешения для выполнения действий. Можно установить область hello на уровне hello hello подписки, группы ресурсов или ресурсов. Hello разрешения, наследуемые toolower уровни области действия (например, Добавление роли модуля чтения toohello приложения для группы ресурсов значит, что возможно чтение группы ресурсов hello и все ресурсы, которые он содержит). В этом учебнике будет настраивать hello область на уровне группы ресурсов hello. Дополнительные сведения см. в разделе [использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](../active-directory/role-based-access-control-configure.md)

**hello tooadd приложения Azure AD toohello владельца роли**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Нажмите кнопку **группы ресурсов** hello левой панели.
3. Щелкните группу ресурсов hello, содержащую hello кластера HDInsight, где будет выполняться запрос Hive далее в этом учебнике. Если слишком много групп ресурсов, можно использовать фильтр hello.
4. Нажмите кнопку **(IAM) управления доступом к** hello ресурсов группы меню.
5. Нажмите кнопку **добавить** из hello **пользователей** колонку.
6. Выполните hello инструкция tooadd hello **владельца** toohello роли приложения Azure AD, созданный в последней процедуре hello. Если завершаются успешно, вы увидите, что приложения hello, перечисленных в колонке hello пользователи с ролью владельца hello.

## <a name="develop-hdinsight-client-application"></a>Разработка клиентского приложения HDInsight

1. Создайте консольное приложение на C#.
2. Добавьте следующие пакеты Nuget hello:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Используйте следующий пример кода hello.

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

## <a name="next-steps"></a>Дальнейшие действия
* [Создание приложения Azure Active Directory и субъекта-службы с помощью портала](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Проверка подлинности субъекта-службы в Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Управление доступом на основе ролей в Azure](../active-directory/role-based-access-control-configure.md)
