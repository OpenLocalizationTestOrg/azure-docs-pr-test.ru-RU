---
title: "aaaPublish-WebApplicationVM | Документы Microsoft"
description: "Узнайте, как toodeploy виртуальная машина web tooa приложения. Этот скрипт создает hello необходимые ресурсы в подписке Azure, если они не существуют."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="ac6a8-104">Publish-WebApplicationVM (сценарий Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ac6a8-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="ac6a8-105">Развертывание виртуальной машины web tooa приложений.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="ac6a8-106">Hello скрипт создает hello необходимые ресурсы в подписке Azure, если они не существуют.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="ac6a8-107">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="ac6a8-107">Configuration</span></span>
<span data-ttu-id="ac6a8-108">Hello путь toohello файл конфигурации JSON, описывающий сведения hello hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="ac6a8-109">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ac6a8-109">Aliases</span></span> | <span data-ttu-id="ac6a8-110">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="ac6a8-111">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-111">Required?</span></span> |<span data-ttu-id="ac6a8-112">Да</span><span class="sxs-lookup"><span data-stu-id="ac6a8-112">true</span></span> |
| <span data-ttu-id="ac6a8-113">Позиция</span><span class="sxs-lookup"><span data-stu-id="ac6a8-113">Position</span></span> |<span data-ttu-id="ac6a8-114">именованная</span><span class="sxs-lookup"><span data-stu-id="ac6a8-114">named</span></span> |
| <span data-ttu-id="ac6a8-115">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ac6a8-115">Default value</span></span> |<span data-ttu-id="ac6a8-116">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-116">none</span></span> |
| <span data-ttu-id="ac6a8-117">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-117">Accept pipeline input?</span></span> |<span data-ttu-id="ac6a8-118">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-118">false</span></span> |
| <span data-ttu-id="ac6a8-119">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-119">Accept wildcard characters?</span></span> |<span data-ttu-id="ac6a8-120">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="ac6a8-121">Параметр SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="ac6a8-121">SubscriptionName</span></span>
<span data-ttu-id="ac6a8-122">Имя Hello hello подписки Azure, в котором нужно toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="ac6a8-123">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ac6a8-123">Aliases</span></span> | <span data-ttu-id="ac6a8-124">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="ac6a8-125">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-125">Required?</span></span> |<span data-ttu-id="ac6a8-126">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-126">false</span></span> |
| <span data-ttu-id="ac6a8-127">Позиция</span><span class="sxs-lookup"><span data-stu-id="ac6a8-127">Position</span></span> |<span data-ttu-id="ac6a8-128">именованная</span><span class="sxs-lookup"><span data-stu-id="ac6a8-128">named</span></span> |
| <span data-ttu-id="ac6a8-129">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ac6a8-129">Default value</span></span> |<span data-ttu-id="ac6a8-130">Использует первую подписку hello в файле подписки hello</span><span class="sxs-lookup"><span data-stu-id="ac6a8-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="ac6a8-131">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-131">Accept pipeline input?</span></span> |<span data-ttu-id="ac6a8-132">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-132">false</span></span> |
| <span data-ttu-id="ac6a8-133">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-133">Accept wildcard characters?</span></span> |<span data-ttu-id="ac6a8-134">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="ac6a8-135">Параметр WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="ac6a8-135">WebDeployPackage</span></span>
<span data-ttu-id="ac6a8-136">Hello путь toohello развертывания пакета toopublish toohello виртуальная машина web.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="ac6a8-137">Этот пакет можно создать с помощью мастера публикации веб-сайта hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="ac6a8-138">Ознакомьтесь со статьей [Как создать пакет веб-развертывания в Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac6a8-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="ac6a8-139">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ac6a8-139">Aliases</span></span> | <span data-ttu-id="ac6a8-140">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="ac6a8-141">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-141">Required?</span></span> |<span data-ttu-id="ac6a8-142">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-142">false</span></span> |
| <span data-ttu-id="ac6a8-143">Позиция</span><span class="sxs-lookup"><span data-stu-id="ac6a8-143">Position</span></span> |<span data-ttu-id="ac6a8-144">именованная</span><span class="sxs-lookup"><span data-stu-id="ac6a8-144">named</span></span> |
| <span data-ttu-id="ac6a8-145">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ac6a8-145">Default value</span></span> |<span data-ttu-id="ac6a8-146">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-146">none</span></span> |
| <span data-ttu-id="ac6a8-147">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-147">Accept pipeline input?</span></span> |<span data-ttu-id="ac6a8-148">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-148">false</span></span> |
| <span data-ttu-id="ac6a8-149">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-149">Accept wildcard characters?</span></span> |<span data-ttu-id="ac6a8-150">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="ac6a8-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="ac6a8-151">AllowUntrusted</span></span>
<span data-ttu-id="ac6a8-152">Если значение равно true, разрешить использование hello сертификаты, которые не были подписаны доверенным корневым центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="ac6a8-153">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ac6a8-153">Aliases</span></span> | <span data-ttu-id="ac6a8-154">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="ac6a8-155">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-155">Required?</span></span> |<span data-ttu-id="ac6a8-156">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-156">false</span></span> |
| <span data-ttu-id="ac6a8-157">Позиция</span><span class="sxs-lookup"><span data-stu-id="ac6a8-157">Position</span></span> |<span data-ttu-id="ac6a8-158">именованная</span><span class="sxs-lookup"><span data-stu-id="ac6a8-158">named</span></span> |
| <span data-ttu-id="ac6a8-159">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ac6a8-159">Default value</span></span> |<span data-ttu-id="ac6a8-160">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-160">false</span></span> |
| <span data-ttu-id="ac6a8-161">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-161">Accept pipeline input?</span></span> |<span data-ttu-id="ac6a8-162">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-162">false</span></span> |
| <span data-ttu-id="ac6a8-163">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-163">Accept wildcard characters?</span></span> |<span data-ttu-id="ac6a8-164">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="ac6a8-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="ac6a8-165">VMPassword</span></span>
<span data-ttu-id="ac6a8-166">Hello учетные данные для учетной записи виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="ac6a8-167">Пример: - VMPassword @{Name = «admin»; Пароль = «password»}</span><span class="sxs-lookup"><span data-stu-id="ac6a8-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="ac6a8-168">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ac6a8-168">Aliases</span></span> | <span data-ttu-id="ac6a8-169">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="ac6a8-170">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-170">Required?</span></span> |<span data-ttu-id="ac6a8-171">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-171">false</span></span> |
| <span data-ttu-id="ac6a8-172">Позиция</span><span class="sxs-lookup"><span data-stu-id="ac6a8-172">Position</span></span> |<span data-ttu-id="ac6a8-173">именованная</span><span class="sxs-lookup"><span data-stu-id="ac6a8-173">named</span></span> |
| <span data-ttu-id="ac6a8-174">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ac6a8-174">Default value</span></span> |<span data-ttu-id="ac6a8-175">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-175">none</span></span> |
| <span data-ttu-id="ac6a8-176">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-176">Accept pipeline input?</span></span> |<span data-ttu-id="ac6a8-177">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-177">false</span></span> |
| <span data-ttu-id="ac6a8-178">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-178">Accept wildcard characters?</span></span> |<span data-ttu-id="ac6a8-179">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="ac6a8-180">Параметр DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="ac6a8-180">DatabaseServerPassword</span></span>
<span data-ttu-id="ac6a8-181">Hello учетные данные для hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="ac6a8-182">Пример: - DatabaseServerPassword @{Name = «admin»; Пароль = «password»}</span><span class="sxs-lookup"><span data-stu-id="ac6a8-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="ac6a8-183">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ac6a8-183">Aliases</span></span> | <span data-ttu-id="ac6a8-184">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="ac6a8-185">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-185">Required?</span></span> |<span data-ttu-id="ac6a8-186">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-186">false</span></span> |
| <span data-ttu-id="ac6a8-187">Позиция</span><span class="sxs-lookup"><span data-stu-id="ac6a8-187">Position</span></span> |<span data-ttu-id="ac6a8-188">именованная</span><span class="sxs-lookup"><span data-stu-id="ac6a8-188">named</span></span> |
| <span data-ttu-id="ac6a8-189">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ac6a8-189">Default value</span></span> |<span data-ttu-id="ac6a8-190">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-190">none</span></span> |
| <span data-ttu-id="ac6a8-191">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-191">Accept pipeline input?</span></span> |<span data-ttu-id="ac6a8-192">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-192">false</span></span> |
| <span data-ttu-id="ac6a8-193">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-193">Accept wildcard characters?</span></span> |<span data-ttu-id="ac6a8-194">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="ac6a8-195">Параметр SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="ac6a8-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="ac6a8-196">Значение true, если поток вывода для печати сообщения из скрипта toohello hello.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="ac6a8-197">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ac6a8-197">Aliases</span></span> | <span data-ttu-id="ac6a8-198">Нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="ac6a8-199">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-199">Required?</span></span> |<span data-ttu-id="ac6a8-200">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-200">false</span></span> |
| <span data-ttu-id="ac6a8-201">Позиция</span><span class="sxs-lookup"><span data-stu-id="ac6a8-201">Position</span></span> |<span data-ttu-id="ac6a8-202">именованная</span><span class="sxs-lookup"><span data-stu-id="ac6a8-202">named</span></span> |
| <span data-ttu-id="ac6a8-203">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ac6a8-203">Default value</span></span> |<span data-ttu-id="ac6a8-204">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-204">false</span></span> |
| <span data-ttu-id="ac6a8-205">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-205">Accept pipeline input?</span></span> |<span data-ttu-id="ac6a8-206">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-206">false</span></span> |
| <span data-ttu-id="ac6a8-207">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ac6a8-207">Accept wildcard characters?</span></span> |<span data-ttu-id="ac6a8-208">нет</span><span class="sxs-lookup"><span data-stu-id="ac6a8-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="ac6a8-209">Примечания</span><span class="sxs-lookup"><span data-stu-id="ac6a8-209">Remarks</span></span>
<span data-ttu-id="ac6a8-210">Полное описание toouse hello сценария toocreate разработки и тестовой среде. в статье [tooDev tooPublish с помощью сценариев Windows PowerShell и тестовых средах](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="ac6a8-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="ac6a8-211">файл конфигурации JSON Hello указывает hello сведения о том, что будет toobe развертывания.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="ac6a8-212">Он включает сведения hello, указанный при создании проекта hello, такие как имя hello, территориальная группа, образ виртуального жесткого диска и размер виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="ac6a8-213">Также включает hello конечных точек на виртуальной машине hello, tooprovision hello баз данных, если таковые имеются и параметры веб-развертываний.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="ac6a8-214">После кода Hello показан пример файла конфигурации JSON:</span><span class="sxs-lookup"><span data-stu-id="ac6a8-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="ac6a8-215">Вы можете изменить состав подготовки файла toochange hello JSON конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="ac6a8-216">Виртуальная машина и облачная служба обязательны, но hello раздел базы данных является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ac6a8-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

