---
title: "Получение значений для аутентификации приложения для подключения к базе данных SQL Azure | Документация Майкрософт"
description: "Создание субъекта-службы для получения доступа к базе данных SQL из кода."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Inactive
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: e76144bcb65da992c6d723d7333b4db8aa1ca488
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2017
---
# <a name="get-the-required-values-for-authenticating-an-application-to-access-sql-database-from-code"></a>Получение необходимых значений для проверки подлинности приложения при предоставлении доступа к базе данных SQL из кода
Чтобы создать базу данных SQL и управлять ею из кода, необходимо зарегистрировать приложение в домене Azure Active Directory (AAD) в подписке, где были созданы ресурсы Azure.

## <a name="create-a-service-principal-to-access-resources-from-an-application"></a>Создание субъекта-службы для доступа к ресурсам из приложения
Установите и запустите последнюю версию [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx). Дополнительные сведения можно узнать в статье [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).

Следующий сценарий PowerShell создает приложение Active Directory (AD) и субъект-службу, которые необходимы для проверки подлинности нашего приложения C#. Сценарий выводит значения, необходимые для предыдущего примера на C#. Дополнительные сведения см. в статье [Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a>Дополнительные материалы
* [Создание базы данных SQL с помощью C#](sql-database-get-started-csharp.md)
* [Подключение к базе данных SQL с использованием проверки подлинности Azure Active Directory](sql-database-aad-authentication.md)

