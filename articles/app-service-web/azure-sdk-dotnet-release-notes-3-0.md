---
title: "Заметки о выпуске пакета Azure SDK для .NET 3.0 | Документы Майкрософт"
description: "Заметки о выпуске пакета Azure SDK для .NET 3.0"
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
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: eea4e569ac2d0192ed7872d2fcb9bed03614832b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="01cad-103">Заметки о выпуске пакета Azure SDK для .NET 3.0</span><span class="sxs-lookup"><span data-stu-id="01cad-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="01cad-104">В этой статье содержатся заметки о выпуске пакета Azure SDK версий 3.0 и 2.9.6 для .NET.</span><span class="sxs-lookup"><span data-stu-id="01cad-104">This topic includes release notes for version 3.0 of the Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="01cad-105">Сводные данные о выпуске пакета Azure SDK для .NET 3.0</span><span class="sxs-lookup"><span data-stu-id="01cad-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="01cad-106">Дата выпуска: 07.03.2017</span><span class="sxs-lookup"><span data-stu-id="01cad-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="01cad-107">В этом выпуске нет никаких критических изменений пакета Azure SDK 3.0.</span><span class="sxs-lookup"><span data-stu-id="01cad-107">No breaking changes to the Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="01cad-108">Для использования этого пакета SDK с имеющимися проектами облачной службы также не требуется выполнять обновление.</span><span class="sxs-lookup"><span data-stu-id="01cad-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="01cad-109">Чтобы пакет SDK для Azure 3.0 мог использоваться без необходимости обновления, он устанавливается в те же каталоги, что и пакет SDK для Azure 2.9.</span><span class="sxs-lookup"><span data-stu-id="01cad-109">To allow use of the Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs to the same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="01cad-110">Основной номер версии большинства компонентов не изменился (т. е. остался равным 2.9), но обновился их номер сборки.</span><span class="sxs-lookup"><span data-stu-id="01cad-110">Most the components did not change the major version from 2.9 but instead just updated the build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="01cad-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="01cad-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="01cad-112">В Visual Studio 2017 этот выпуск пакета Azure SDK для .NET встроен в рабочую нагрузку Azure.</span><span class="sxs-lookup"><span data-stu-id="01cad-112">In Visual Studio 2017, this release of the Azure SDK for .NET is built in to the Azure Workload.</span></span> <span data-ttu-id="01cad-113">Все средства, необходимые для разработки Azure, будут входить в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="01cad-113">All the tools you need to do Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="01cad-114">Для Visual Studio 2015 пакет SDK по-прежнему будет доступен через WebPI.</span><span class="sxs-lookup"><span data-stu-id="01cad-114">For Visual Studio 2015 the SDK will still be available through WebPI.</span></span> <span data-ttu-id="01cad-115">Мы вывели из использования выпуски пакета Azure SDK для .NET для Visual Studio 2013, так как теперь вышла версия Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="01cad-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="01cad-116">Диагностика Azure</span><span class="sxs-lookup"><span data-stu-id="01cad-116">Azure Diagnostics</span></span>

- <span data-ttu-id="01cad-117">Теперь сохраняется только частичная строка подключения к хранилищу для диагностики облачных служб с маркером вместо ключа.</span><span class="sxs-lookup"><span data-stu-id="01cad-117">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="01cad-118">Фактический ключ к хранилищу данных теперь хранится в папке профиля пользователя, поэтому доступ к нему можно контролировать.</span><span class="sxs-lookup"><span data-stu-id="01cad-118">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="01cad-119">Visual Studio будет считывать этот ключ для локальной отладки и процедуры публикации.</span><span class="sxs-lookup"><span data-stu-id="01cad-119">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="01cad-120">В ответ на описанные выше изменения группа разработчиков Visual Studio Online усовершенствовала шаблон задачи развертывания облачных служб Azure. Теперь пользователи могут указать ключ к хранилищу данных, чтобы настроить расширение системы диагностики во время публикации в Azure при непрерывной интеграции и развертывании.</span><span class="sxs-lookup"><span data-stu-id="01cad-120">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="01cad-121">Мы сделали так, что стало возможно хранить безопасную строку подключения и разметку для системы диагностики Azure (WAD), чтобы устранить проблемы с конфигурацией в средах.</span><span class="sxs-lookup"><span data-stu-id="01cad-121">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="01cad-122">Виртуальные машины Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="01cad-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="01cad-123">Visual Studio теперь поддерживает развертывание облачных служб на виртуальных машинах с операционной системой из семейства версии 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="01cad-123">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="01cad-124">Для имеющихся облачных служб можно изменить параметры, чтобы использовать новую ОС из семейства версий.</span><span class="sxs-lookup"><span data-stu-id="01cad-124">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="01cad-125">Если для создания облачных служб вы решили использовать .NET 4.6 или более поздней версии, по умолчанию для службы будет использоваться ОС из семейства версий 5.</span><span class="sxs-lookup"><span data-stu-id="01cad-125">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="01cad-126">Дополнительные сведения см. в статье [Таблица совместимости выпусков гостевых ОС Azure и пакетов SDK](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="01cad-126">For more information, you can review the [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="01cad-127">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="01cad-127">Known issues</span></span>

- <span data-ttu-id="01cad-128">В пакете SDK Azure 3.0 для .NET возникала проблема при удалении Visual Studio 2017 в параллельной конфигурации с Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="01cad-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="01cad-129">Если у вас установлен пакет SDK Azure для Visual Studio 2015, при удалении Visual Studio 2017 будут удалены эмулятор хранения Microsoft Azure и эмулятор вычислений Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="01cad-129">If you have the Azure SDK installed for Visual Studio 2015, the Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="01cad-130">Это приведет к ошибке при создании и отладке новых проектов облачных служб в Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="01cad-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="01cad-131">Чтобы устранить эту проблему, переустановите пакет Azure SDK из установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="01cad-131">In order to fix this issue,  reinstall the Azure SDK from the Web Platform Installer.</span></span>  <span data-ttu-id="01cad-132">Проблема будет устранена в следующем обновлении Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="01cad-132">The issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="01cad-133">.</span><span class="sxs-lookup"><span data-stu-id="01cad-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="01cad-134">Кэш роли Azure</span><span class="sxs-lookup"><span data-stu-id="01cad-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="01cad-135">Поддержка кэша роли Azure завершилась 30 ноября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="01cad-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="01cad-136">Дополнительные сведения см. [здесь](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="01cad-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>




