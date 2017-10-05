---
title: "Заметки о выпуске пакета SDK для Azure для .NET 2.9"
description: "Заметки о выпуске пакета SDK для Azure для .NET 2.9"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 199f0906f73d693d7cd4b73c928f23ae83b99596
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="a7f76-103">Заметки о выпуске пакета Azure SDK для .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="a7f76-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="a7f76-104">В этой статье содержатся заметки о выпуске для версий 2.9 и 2.9.6 пакета Azure SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="a7f76-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="a7f76-105">Сведения о выпуске Azure SDK для .NET 2.9.6</span><span class="sxs-lookup"><span data-stu-id="a7f76-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="a7f76-106">Дата выпуска: 16.11.2016</span><span class="sxs-lookup"><span data-stu-id="a7f76-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="a7f76-107">В этом выпуске нет никаких критических изменений пакета Azure SDK 2.9.</span><span class="sxs-lookup"><span data-stu-id="a7f76-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="a7f76-108">Для использования этого пакета SDK с имеющимися проектами облачной службы также не требуется выполнять обновление.</span><span class="sxs-lookup"><span data-stu-id="a7f76-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="a7f76-109">релиз-кандидат Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a7f76-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="a7f76-110">В версии-кандидате Visual Studio 2017 этот выпуск пакета Azure SDK для .NET встроен в рабочую нагрузку Azure.</span><span class="sxs-lookup"><span data-stu-id="a7f76-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="a7f76-111">Все средства, необходимые для разработки Azure, будут входить в эту версию.</span><span class="sxs-lookup"><span data-stu-id="a7f76-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="a7f76-112">Для Visual Studio 2015 и Visual Studio 2013 пакет SDK по-прежнему будет доступен через WebPI.</span><span class="sxs-lookup"><span data-stu-id="a7f76-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="a7f76-113">Когда Visual Studio 2017 будет выпущен в качестве конечного продукта, версии пакета Azure SDK для .NET больше не будут доступны для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="a7f76-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="a7f76-114">Чтобы скачать версию-кандидат Visual Studio 2017, перейдите по этой ссылке: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="a7f76-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="a7f76-115">Диагностика Azure</span><span class="sxs-lookup"><span data-stu-id="a7f76-115">Azure Diagnostics</span></span>

- <span data-ttu-id="a7f76-116">Теперь сохраняется только частичная строка подключения к хранилищу для диагностики облачных служб с маркером вместо ключа.</span><span class="sxs-lookup"><span data-stu-id="a7f76-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="a7f76-117">Фактический ключ к хранилищу данных теперь хранится в папке профиля пользователя, поэтому доступ к нему можно контролировать.</span><span class="sxs-lookup"><span data-stu-id="a7f76-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="a7f76-118">Visual Studio будет считывать этот ключ для локальной отладки и процедуры публикации.</span><span class="sxs-lookup"><span data-stu-id="a7f76-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="a7f76-119">В ответ на описанные выше изменения группа разработчиков Visual Studio Online усовершенствовала шаблон задачи развертывания облачных служб Azure. Теперь пользователи могут указать ключ к хранилищу данных, чтобы настроить расширение системы диагностики во время публикации в Azure при непрерывной интеграции и развертывании.</span><span class="sxs-lookup"><span data-stu-id="a7f76-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="a7f76-120">Мы сделали так, что стало возможно хранить безопасную строку подключения и разметку для системы диагностики Azure (WAD), чтобы устранить проблемы с конфигурацией в средах.</span><span class="sxs-lookup"><span data-stu-id="a7f76-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="a7f76-121">Виртуальные машины Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a7f76-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="a7f76-122">Visual Studio теперь поддерживает развертывание облачных служб на виртуальных машинах с операционной системой из семейства версии 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="a7f76-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="a7f76-123">Для имеющихся облачных служб можно изменить параметры, чтобы использовать новую ОС из семейства версий.</span><span class="sxs-lookup"><span data-stu-id="a7f76-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="a7f76-124">Если для создания облачных служб вы решили использовать .NET 4.6 или более поздней версии, по умолчанию для службы будет использоваться ОС из семейства версий 5.</span><span class="sxs-lookup"><span data-stu-id="a7f76-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="a7f76-125">Дополнительные сведения см. в статье [Таблица совместимости выпусков гостевых ОС Azure и пакетов SDK](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="a7f76-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="a7f76-126">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="a7f76-126">Known issues</span></span>

- <span data-ttu-id="a7f76-127">В пакете SDK Azure для .NET 2.9.6 введено ограничение, который блокирует развертывание проектов, использующих неподдерживаемые платформы .NET Framework (например, .NET 4.6) для любого семейства ОС, предшествующего версии 5.</span><span class="sxs-lookup"><span data-stu-id="a7f76-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="a7f76-128">Обходной путь описан [здесь](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="a7f76-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="a7f76-129">Кэш роли Azure</span><span class="sxs-lookup"><span data-stu-id="a7f76-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="a7f76-130">Поддержка кэша роли Azure закончилась 30 ноября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="a7f76-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="a7f76-131">Дополнительные сведения см. [здесь](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="a7f76-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="a7f76-132">Шаблоны Azure Resource Manager для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a7f76-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="a7f76-133">Мы представляем Azure Stack как целевой объект развертывания для шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7f76-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="a7f76-134">Сводка о пакете Azure SDK для .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="a7f76-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="a7f76-135">Обзор</span><span class="sxs-lookup"><span data-stu-id="a7f76-135">Overview</span></span>
<span data-ttu-id="a7f76-136">Этот документ содержит заметки о выпуске для пакета Azure SDK для .NET версии 2.9.</span><span class="sxs-lookup"><span data-stu-id="a7f76-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="a7f76-137">Дополнительные сведения об обновлениях в этом выпуске см. в [объявлении о пакете SDK для Azure 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="a7f76-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="a7f76-138">Azure SDK 2.9 для Visual Studio 2015 с обновлением 2 и Visual Studio "15" (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="a7f76-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="a7f76-139">Это обновление содержит следующие исправления ошибок:</span><span class="sxs-lookup"><span data-stu-id="a7f76-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="a7f76-140">Проблема, связанная с созданием клиента REST API, в котором строка "Unknown Type" (Неизвестный тип) будет использоваться в качестве имени папки, созданной кодом, и/или имени пространства имен в созданном коде.</span><span class="sxs-lookup"><span data-stu-id="a7f76-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="a7f76-141">Проблема, связанная с запланированными веб-заданиями, в которых сведения проверки подлинности не удалось передать в процесс подготовки планировщика.</span><span class="sxs-lookup"><span data-stu-id="a7f76-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="a7f76-142">Это обновление содержит следующий новый компонент:</span><span class="sxs-lookup"><span data-stu-id="a7f76-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="a7f76-143">Поддержка дополнительных служб приложений на вкладке "Службы" в диалоговом окне подготовки служб приложений.</span><span class="sxs-lookup"><span data-stu-id="a7f76-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="a7f76-144">Средства озера данных Azure для Visual Studio 2015 с обновлением 2</span><span class="sxs-lookup"><span data-stu-id="a7f76-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="a7f76-145">Эти обновления включают следующее:</span><span class="sxs-lookup"><span data-stu-id="a7f76-145">This updates includes the following:</span></span>

* <span data-ttu-id="a7f76-146">**Средства озера данных Azure** для Visual Studio теперь объединены в пакет SDK для Azure для версии .NET.</span><span class="sxs-lookup"><span data-stu-id="a7f76-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="a7f76-147">Этот инструмент автоматически устанавливается при установке пакета SDK для Azure.</span><span class="sxs-lookup"><span data-stu-id="a7f76-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="a7f76-148">Этот инструмент постоянно обновляется. Получить обновления можно [здесь](http://aka.ms/datalaketool).</span><span class="sxs-lookup"><span data-stu-id="a7f76-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="a7f76-149">**Обозреватель сервера** теперь позволяет просматривать все сущности метаданных U-SQL и обновлять некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="a7f76-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="a7f76-150">Дополнительную информацию см. в [этом](https://azure.microsoft.com/documentation/services/data-lake-analytics/) блоге.</span><span class="sxs-lookup"><span data-stu-id="a7f76-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="a7f76-151">Средства HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7f76-151">HDInsight Tools</span></span>
<span data-ttu-id="a7f76-152">**Средства HDInsight** для Visual Studio теперь поддерживают HDInsight версии 3.3, включая показ графики Tez и другие языковые исправления.</span><span class="sxs-lookup"><span data-stu-id="a7f76-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="a7f76-153">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a7f76-153">Azure Resource Manager</span></span>
<span data-ttu-id="a7f76-154">В этом выпуске добавлена поддержка [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) для шаблонов Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7f76-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="a7f76-155">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a7f76-155">See also</span></span>
[<span data-ttu-id="a7f76-156">Объявление о пакете SDK Azure 2.9</span><span class="sxs-lookup"><span data-stu-id="a7f76-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

