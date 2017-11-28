---
title: "aaaPublish-WebApplicationWebSite (скрипт Windows PowerShell) | Документы Microsoft"
description: "Узнайте, как toopublish веб-узел проекта tooan веб-сайте Azure. Этот скрипт создает hello необходимые ресурсы в подписке Azure, если они не существуют."
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
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="9e3bf-104">Publish-WebApplicationWebSite (сценарий Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="9e3bf-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="9e3bf-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="9e3bf-105">Syntax</span></span>
<span data-ttu-id="9e3bf-106">Публикует tooan проект web веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="9e3bf-107">Hello скрипт создает hello необходимые ресурсы в подписке Azure, если они не существуют.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="9e3bf-108">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="9e3bf-108">Configuration</span></span>
<span data-ttu-id="9e3bf-109">Hello путь toohello файл конфигурации JSON, описывающий сведения hello hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="9e3bf-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="9e3bf-110">Parameter</span></span> | <span data-ttu-id="9e3bf-111">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9e3bf-112">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="9e3bf-112">Aliases</span></span> |<span data-ttu-id="9e3bf-113">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-113">none</span></span> |
| <span data-ttu-id="9e3bf-114">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-114">Required?</span></span> |<span data-ttu-id="9e3bf-115">Да</span><span class="sxs-lookup"><span data-stu-id="9e3bf-115">true</span></span> |
| <span data-ttu-id="9e3bf-116">Позиция</span><span class="sxs-lookup"><span data-stu-id="9e3bf-116">Position</span></span> |<span data-ttu-id="9e3bf-117">именованная</span><span class="sxs-lookup"><span data-stu-id="9e3bf-117">named</span></span> |
| <span data-ttu-id="9e3bf-118">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-118">Default value</span></span> |<span data-ttu-id="9e3bf-119">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-119">none</span></span> |
| <span data-ttu-id="9e3bf-120">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-120">Accept pipeline input?</span></span> |<span data-ttu-id="9e3bf-121">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-121">false</span></span> |
| <span data-ttu-id="9e3bf-122">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-122">Accept wildcard characters?</span></span> |<span data-ttu-id="9e3bf-123">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="9e3bf-124">Параметр SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="9e3bf-124">SubscriptionName</span></span>
<span data-ttu-id="9e3bf-125">Имя Hello hello подписки Azure, вы должны быть toocreate hello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="9e3bf-126">Параметр</span><span class="sxs-lookup"><span data-stu-id="9e3bf-126">Parameter</span></span> | <span data-ttu-id="9e3bf-127">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9e3bf-128">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="9e3bf-128">Aliases</span></span> |<span data-ttu-id="9e3bf-129">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-129">none</span></span> |
| <span data-ttu-id="9e3bf-130">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-130">Required?</span></span> |<span data-ttu-id="9e3bf-131">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-131">false</span></span> |
| <span data-ttu-id="9e3bf-132">Позиция</span><span class="sxs-lookup"><span data-stu-id="9e3bf-132">Position</span></span> |<span data-ttu-id="9e3bf-133">именованная</span><span class="sxs-lookup"><span data-stu-id="9e3bf-133">named</span></span> |
| <span data-ttu-id="9e3bf-134">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-134">Default value</span></span> |<span data-ttu-id="9e3bf-135">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-135">none</span></span> |
| <span data-ttu-id="9e3bf-136">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-136">Accept pipeline input?</span></span> |<span data-ttu-id="9e3bf-137">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-137">false</span></span> |
| <span data-ttu-id="9e3bf-138">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-138">Accept wildcard characters?</span></span> |<span data-ttu-id="9e3bf-139">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="9e3bf-140">Параметр WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="9e3bf-140">WebDeployPackage</span></span>
<span data-ttu-id="9e3bf-141">Hello путь toohello web развертывания пакета toopublish toohello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="9e3bf-142">Этот пакет можно создать с помощью мастера публикации веб-сайта hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="9e3bf-143">Дополнительные сведения можно найти в статье [Начало работы с облачными службами Azure и ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="9e3bf-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="9e3bf-144">Параметр</span><span class="sxs-lookup"><span data-stu-id="9e3bf-144">Parameter</span></span> | <span data-ttu-id="9e3bf-145">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9e3bf-146">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="9e3bf-146">Aliases</span></span> |<span data-ttu-id="9e3bf-147">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-147">none</span></span> |
| <span data-ttu-id="9e3bf-148">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-148">Required?</span></span> |<span data-ttu-id="9e3bf-149">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-149">false</span></span> |
| <span data-ttu-id="9e3bf-150">Позиция</span><span class="sxs-lookup"><span data-stu-id="9e3bf-150">Position</span></span> |<span data-ttu-id="9e3bf-151">именованная</span><span class="sxs-lookup"><span data-stu-id="9e3bf-151">named</span></span> |
| <span data-ttu-id="9e3bf-152">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-152">Default value</span></span> |<span data-ttu-id="9e3bf-153">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-153">none</span></span> |
| <span data-ttu-id="9e3bf-154">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-154">Accept pipeline input?</span></span> |<span data-ttu-id="9e3bf-155">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-155">false</span></span> |
| <span data-ttu-id="9e3bf-156">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-156">Accept wildcard characters?</span></span> |<span data-ttu-id="9e3bf-157">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="9e3bf-158">Параметр DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="9e3bf-158">DatabaseServerPassword</span></span>
<span data-ttu-id="9e3bf-159">Hello имя пользователя и пароль для hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="9e3bf-160">Параметр</span><span class="sxs-lookup"><span data-stu-id="9e3bf-160">Parameter</span></span> | <span data-ttu-id="9e3bf-161">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9e3bf-162">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="9e3bf-162">Aliases</span></span> |<span data-ttu-id="9e3bf-163">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-163">none</span></span> |
| <span data-ttu-id="9e3bf-164">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-164">Required?</span></span> |<span data-ttu-id="9e3bf-165">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-165">false</span></span> |
| <span data-ttu-id="9e3bf-166">Позиция</span><span class="sxs-lookup"><span data-stu-id="9e3bf-166">Position</span></span> |<span data-ttu-id="9e3bf-167">именованная</span><span class="sxs-lookup"><span data-stu-id="9e3bf-167">named</span></span> |
| <span data-ttu-id="9e3bf-168">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-168">Default value</span></span> |<span data-ttu-id="9e3bf-169">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-169">none</span></span> |
| <span data-ttu-id="9e3bf-170">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-170">Accept pipeline input?</span></span> |<span data-ttu-id="9e3bf-171">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-171">false</span></span> |
| <span data-ttu-id="9e3bf-172">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-172">Accept wildcard characters?</span></span> |<span data-ttu-id="9e3bf-173">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="9e3bf-174">Параметр SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="9e3bf-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="9e3bf-175">Значение true, если поток вывода для печати сообщения из скрипта toohello hello.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="9e3bf-176">Параметр</span><span class="sxs-lookup"><span data-stu-id="9e3bf-176">Parameter</span></span> | <span data-ttu-id="9e3bf-177">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="9e3bf-178">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="9e3bf-178">Aliases</span></span> |<span data-ttu-id="9e3bf-179">Нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-179">none</span></span> |
| <span data-ttu-id="9e3bf-180">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-180">Required?</span></span> |<span data-ttu-id="9e3bf-181">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-181">false</span></span> |
| <span data-ttu-id="9e3bf-182">Позиция</span><span class="sxs-lookup"><span data-stu-id="9e3bf-182">Position</span></span> |<span data-ttu-id="9e3bf-183">именованная</span><span class="sxs-lookup"><span data-stu-id="9e3bf-183">named</span></span> |
| <span data-ttu-id="9e3bf-184">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e3bf-184">Default value</span></span> |<span data-ttu-id="9e3bf-185">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-185">false</span></span> |
| <span data-ttu-id="9e3bf-186">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-186">Accept pipeline input?</span></span> |<span data-ttu-id="9e3bf-187">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-187">false</span></span> |
| <span data-ttu-id="9e3bf-188">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="9e3bf-188">Accept wildcard characters?</span></span> |<span data-ttu-id="9e3bf-189">нет</span><span class="sxs-lookup"><span data-stu-id="9e3bf-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="9e3bf-190">Примечания</span><span class="sxs-lookup"><span data-stu-id="9e3bf-190">Remarks</span></span>
<span data-ttu-id="9e3bf-191">Полное описание toouse hello сценария toocreate разработки и тестовой среде. в статье [tooDev tooPublish с помощью сценариев Windows PowerShell и тестовых средах](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="9e3bf-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="9e3bf-192">файл конфигурации JSON Hello указывает hello сведения о том, что будет toobe развертывания.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="9e3bf-193">Он включает сведения hello, указанный при создании проекта hello, такие как имя hello и имя пользователя для веб-сайта hello.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="9e3bf-194">Он также включает tooprovision hello базы данных, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="9e3bf-195">После кода Hello показан пример файла конфигурации JSON:</span><span class="sxs-lookup"><span data-stu-id="9e3bf-195">hello following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="9e3bf-196">Вы можете изменить состав развертывания файла toochange hello JSON конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="9e3bf-197">Раздел веб-сайта является обязательным, но hello раздел базы данных является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9e3bf-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e3bf-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e3bf-198">Next steps</span></span>
<span data-ttu-id="9e3bf-199">Дополнительные сведения см. в статье [Publish-WebApplicationVM (сценарий Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="9e3bf-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

