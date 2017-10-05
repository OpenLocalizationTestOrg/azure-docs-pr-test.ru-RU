---
title: "Publish-WebApplicationWebSite (сценарий Windows PowerShell) | Документация Майкрософт"
description: "Узнайте, как опубликовать веб-проект на веб-сайте Azure. Этот сценарий создает необходимые ресурсы в подписке Azure, если они еще не созданы."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 07d21b7ce6cd8aee1cff704d316e7a2ca8c00437
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="4de47-104">Publish-WebApplicationWebSite (сценарий Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="4de47-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="4de47-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="4de47-105">Syntax</span></span>
<span data-ttu-id="4de47-106">Этот сценарий публикует веб-проект на веб-сайте Azure</span><span class="sxs-lookup"><span data-stu-id="4de47-106">Publishes a web project to an Azure website.</span></span> <span data-ttu-id="4de47-107">и создает необходимые ресурсы в подписке Azure, если они еще не созданы.</span><span class="sxs-lookup"><span data-stu-id="4de47-107">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="4de47-108">Параметр Configuration</span><span class="sxs-lookup"><span data-stu-id="4de47-108">Configuration</span></span>
<span data-ttu-id="4de47-109">Путь к файлу конфигурации JSON, содержащему подробные сведения о развертывании.</span><span class="sxs-lookup"><span data-stu-id="4de47-109">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="4de47-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="4de47-110">Parameter</span></span> | <span data-ttu-id="4de47-111">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4de47-112">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="4de47-112">Aliases</span></span> |<span data-ttu-id="4de47-113">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-113">none</span></span> |
| <span data-ttu-id="4de47-114">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="4de47-114">Required?</span></span> |<span data-ttu-id="4de47-115">Да</span><span class="sxs-lookup"><span data-stu-id="4de47-115">true</span></span> |
| <span data-ttu-id="4de47-116">Позиция</span><span class="sxs-lookup"><span data-stu-id="4de47-116">Position</span></span> |<span data-ttu-id="4de47-117">именованная</span><span class="sxs-lookup"><span data-stu-id="4de47-117">named</span></span> |
| <span data-ttu-id="4de47-118">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-118">Default value</span></span> |<span data-ttu-id="4de47-119">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-119">none</span></span> |
| <span data-ttu-id="4de47-120">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4de47-120">Accept pipeline input?</span></span> |<span data-ttu-id="4de47-121">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-121">false</span></span> |
| <span data-ttu-id="4de47-122">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4de47-122">Accept wildcard characters?</span></span> |<span data-ttu-id="4de47-123">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="4de47-124">Параметр SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="4de47-124">SubscriptionName</span></span>
<span data-ttu-id="4de47-125">Имя подписки Azure, в которой необходимо создать веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="4de47-125">The name of the Azure subscription that you want to create the website in.</span></span>

| <span data-ttu-id="4de47-126">Параметр</span><span class="sxs-lookup"><span data-stu-id="4de47-126">Parameter</span></span> | <span data-ttu-id="4de47-127">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4de47-128">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="4de47-128">Aliases</span></span> |<span data-ttu-id="4de47-129">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-129">none</span></span> |
| <span data-ttu-id="4de47-130">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="4de47-130">Required?</span></span> |<span data-ttu-id="4de47-131">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-131">false</span></span> |
| <span data-ttu-id="4de47-132">Позиция</span><span class="sxs-lookup"><span data-stu-id="4de47-132">Position</span></span> |<span data-ttu-id="4de47-133">именованная</span><span class="sxs-lookup"><span data-stu-id="4de47-133">named</span></span> |
| <span data-ttu-id="4de47-134">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-134">Default value</span></span> |<span data-ttu-id="4de47-135">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-135">none</span></span> |
| <span data-ttu-id="4de47-136">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4de47-136">Accept pipeline input?</span></span> |<span data-ttu-id="4de47-137">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-137">false</span></span> |
| <span data-ttu-id="4de47-138">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4de47-138">Accept wildcard characters?</span></span> |<span data-ttu-id="4de47-139">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="4de47-140">Параметр WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="4de47-140">WebDeployPackage</span></span>
<span data-ttu-id="4de47-141">Путь к пакету веб-развертывания для публикации на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="4de47-141">The path to the web deployment package to publish to the website.</span></span> <span data-ttu-id="4de47-142">Этот пакет можно создать с помощью мастера «Публикация веб-сайта» в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4de47-142">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="4de47-143">Дополнительные сведения можно найти в статье [Начало работы с облачными службами Azure и ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="4de47-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="4de47-144">Параметр</span><span class="sxs-lookup"><span data-stu-id="4de47-144">Parameter</span></span> | <span data-ttu-id="4de47-145">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4de47-146">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="4de47-146">Aliases</span></span> |<span data-ttu-id="4de47-147">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-147">none</span></span> |
| <span data-ttu-id="4de47-148">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="4de47-148">Required?</span></span> |<span data-ttu-id="4de47-149">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-149">false</span></span> |
| <span data-ttu-id="4de47-150">Позиция</span><span class="sxs-lookup"><span data-stu-id="4de47-150">Position</span></span> |<span data-ttu-id="4de47-151">именованная</span><span class="sxs-lookup"><span data-stu-id="4de47-151">named</span></span> |
| <span data-ttu-id="4de47-152">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-152">Default value</span></span> |<span data-ttu-id="4de47-153">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-153">none</span></span> |
| <span data-ttu-id="4de47-154">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4de47-154">Accept pipeline input?</span></span> |<span data-ttu-id="4de47-155">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-155">false</span></span> |
| <span data-ttu-id="4de47-156">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4de47-156">Accept wildcard characters?</span></span> |<span data-ttu-id="4de47-157">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="4de47-158">Параметр DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="4de47-158">DatabaseServerPassword</span></span>
<span data-ttu-id="4de47-159">Имя и пароль администратора базы данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="4de47-159">The username and password for the SQL database in Azure.</span></span>

| <span data-ttu-id="4de47-160">Параметр</span><span class="sxs-lookup"><span data-stu-id="4de47-160">Parameter</span></span> | <span data-ttu-id="4de47-161">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4de47-162">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="4de47-162">Aliases</span></span> |<span data-ttu-id="4de47-163">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-163">none</span></span> |
| <span data-ttu-id="4de47-164">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="4de47-164">Required?</span></span> |<span data-ttu-id="4de47-165">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-165">false</span></span> |
| <span data-ttu-id="4de47-166">Позиция</span><span class="sxs-lookup"><span data-stu-id="4de47-166">Position</span></span> |<span data-ttu-id="4de47-167">именованная</span><span class="sxs-lookup"><span data-stu-id="4de47-167">named</span></span> |
| <span data-ttu-id="4de47-168">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-168">Default value</span></span> |<span data-ttu-id="4de47-169">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-169">none</span></span> |
| <span data-ttu-id="4de47-170">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4de47-170">Accept pipeline input?</span></span> |<span data-ttu-id="4de47-171">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-171">false</span></span> |
| <span data-ttu-id="4de47-172">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4de47-172">Accept wildcard characters?</span></span> |<span data-ttu-id="4de47-173">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="4de47-174">Параметр SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="4de47-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="4de47-175">Если установлено значение true, оправляет сообщения из сценария в поток вывода.</span><span class="sxs-lookup"><span data-stu-id="4de47-175">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="4de47-176">Параметр</span><span class="sxs-lookup"><span data-stu-id="4de47-176">Parameter</span></span> | <span data-ttu-id="4de47-177">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4de47-178">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="4de47-178">Aliases</span></span> |<span data-ttu-id="4de47-179">Нет</span><span class="sxs-lookup"><span data-stu-id="4de47-179">none</span></span> |
| <span data-ttu-id="4de47-180">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="4de47-180">Required?</span></span> |<span data-ttu-id="4de47-181">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-181">false</span></span> |
| <span data-ttu-id="4de47-182">Позиция</span><span class="sxs-lookup"><span data-stu-id="4de47-182">Position</span></span> |<span data-ttu-id="4de47-183">именованная</span><span class="sxs-lookup"><span data-stu-id="4de47-183">named</span></span> |
| <span data-ttu-id="4de47-184">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4de47-184">Default value</span></span> |<span data-ttu-id="4de47-185">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-185">false</span></span> |
| <span data-ttu-id="4de47-186">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4de47-186">Accept pipeline input?</span></span> |<span data-ttu-id="4de47-187">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-187">false</span></span> |
| <span data-ttu-id="4de47-188">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4de47-188">Accept wildcard characters?</span></span> |<span data-ttu-id="4de47-189">нет</span><span class="sxs-lookup"><span data-stu-id="4de47-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="4de47-190">Примечания</span><span class="sxs-lookup"><span data-stu-id="4de47-190">Remarks</span></span>
<span data-ttu-id="4de47-191">Подробное описание того, как использовать сценарий для создания сред разработки и тестирования, см. в статье [Использование скриптов Windows PowerShell для публикации в среды разработки и тестирования](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="4de47-191">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="4de47-192">В файле конфигурации JSON указаны данные объектов, которые необходимо развернуть.</span><span class="sxs-lookup"><span data-stu-id="4de47-192">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="4de47-193">Он содержит сведения, указанные при создании проекта, такие как имя веб-сайта и имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="4de47-193">It includes the information that you specified when you created the project, such as the name and username for the website.</span></span> <span data-ttu-id="4de47-194">Он также содержит сведения о базе данных, которую нужно подготовить (если она есть).</span><span class="sxs-lookup"><span data-stu-id="4de47-194">It also includes the database to provision, if any.</span></span> <span data-ttu-id="4de47-195">В следующем коде показан пример файла конфигурации JSON.</span><span class="sxs-lookup"><span data-stu-id="4de47-195">The following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="4de47-196">В файле конфигурации JSON можно изменить объекты, которые подлежат развертыванию.</span><span class="sxs-lookup"><span data-stu-id="4de47-196">You can edit the JSON configuration file to change what is deployed.</span></span> <span data-ttu-id="4de47-197">Раздел webSite является обязательным, а раздел database — необязательным.</span><span class="sxs-lookup"><span data-stu-id="4de47-197">A webSite section is required, but the database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4de47-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4de47-198">Next steps</span></span>
<span data-ttu-id="4de47-199">Дополнительные сведения см. в статье [Publish-WebApplicationVM (сценарий Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="4de47-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

