---
title: "Выполнение сборки для Azure с помощью командной строки | Документация Майкрософт"
description: "Создание сборки для Azure с помощью командной строки"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 5fe910e2757dd5ec783538e23e7f52e2f5725b39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="building-azure-projects-from-the-command-line"></a><span data-ttu-id="ab54a-103">Создание проектов Azure с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="ab54a-103">Building Azure projects from the command line</span></span>
<span data-ttu-id="ab54a-104">С помощью Microsoft Build Engine (MSBuild) можно выполнять сборку продуктов в лабораторных средах, где приложение Visual Studio не установлено.</span><span class="sxs-lookup"><span data-stu-id="ab54a-104">Using the Microsoft Build Engine (MSBuild), you can build products in build-lab environments where Visual Studio is not installed.</span></span> <span data-ttu-id="ab54a-105">MSBuild использует для файлов проекта расширяемый формат XML, который полностью поддерживается Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ab54a-105">MSBuild uses an XML format for project files that's extensible and fully supported by Microsoft.</span></span> <span data-ttu-id="ab54a-106">С помощью формата файлов MSBuild вы можете описать, какие именно элементы должны быть собраны для одной или нескольких платформ и конфигураций.</span><span class="sxs-lookup"><span data-stu-id="ab54a-106">Using the MSBuild file format, you can describe what items must be built for one or more platforms and configurations.</span></span>

<span data-ttu-id="ab54a-107">MSBuild можно также запускать из командной строки. В этой статье описывается именно такой метод.</span><span class="sxs-lookup"><span data-stu-id="ab54a-107">You can also run MSBuild at the command line, and this topic describes that approach.</span></span> <span data-ttu-id="ab54a-108">Задавая свойства в командной строке, вы можете собирать те или иные конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="ab54a-108">By setting properties on the command line, you can build specific configurations of a project.</span></span> <span data-ttu-id="ab54a-109">Точно так же вы можете определять объекты, которые создает MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ab54a-109">Similarly, you can also define the targets that MSBuild builds.</span></span> <span data-ttu-id="ab54a-110">Дополнительные сведения о параметрах командной строки и MSBuild см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab54a-110">For more information about command-line parameters and MSBuild, see [MSBuild Command-Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

## <a name="msbuild-parameters"></a><span data-ttu-id="ab54a-111">Параметры MSBuild</span><span class="sxs-lookup"><span data-stu-id="ab54a-111">MSBuild parameters</span></span>
<span data-ttu-id="ab54a-112">Самый простой способ создать пакет — запустить MSBuild с параметром `/t:Publish` .</span><span class="sxs-lookup"><span data-stu-id="ab54a-112">The simplest way to create a package is to run MSBuild with the `/t:Publish` option.</span></span> <span data-ttu-id="ab54a-113">По умолчанию эта команда создает каталог в зависимости от корневой папки для проекта, например `<ProjectDirectory>\bin\Configuration\app.publish\`.</span><span class="sxs-lookup"><span data-stu-id="ab54a-113">By default, this command creates a directory in relation to the root folder for the project, such as `<ProjectDirectory>\bin\Configuration\app.publish\`.</span></span> <span data-ttu-id="ab54a-114">При сборке проекта Azure создается два файла — собственно файл пакета и сопутствующий файл конфигурации:</span><span class="sxs-lookup"><span data-stu-id="ab54a-114">When you build an Azure project, two files are generated: the package file itself and the accompanying configuration file:</span></span>

* <span data-ttu-id="ab54a-115">файл пакета (`project.cspkg`);</span><span class="sxs-lookup"><span data-stu-id="ab54a-115">Package File (`project.cspkg`)</span></span>
* <span data-ttu-id="ab54a-116">файл конфигурации (`ServiceConfiguration.TargetProfile.cscfg`).</span><span class="sxs-lookup"><span data-stu-id="ab54a-116">Configuration File (`ServiceConfiguration.TargetProfile.cscfg`)</span></span>

<span data-ttu-id="ab54a-117">По умолчанию каждый проект Azure включает в себя один файл конфигурации службы для локальных сборок (отладка) и один — для облачных (промежуточное хранение или производство).</span><span class="sxs-lookup"><span data-stu-id="ab54a-117">By default, each Azure project includes one service-configuration file for local (debugging) builds and another for cloud (staging or production) builds.</span></span> <span data-ttu-id="ab54a-118">Но файлы конфигурации службы можно добавлять или удалять по необходимости.</span><span class="sxs-lookup"><span data-stu-id="ab54a-118">However, you can add or remove service-configuration files as needed.</span></span> <span data-ttu-id="ab54a-119">При сборке пакета в Visual Studio вам предлагается выбрать файл конфигурации службы для включения в пакет.</span><span class="sxs-lookup"><span data-stu-id="ab54a-119">When you build a package within Visual Studio, you are asked which service-configuration file to include alongside the package.</span></span> <span data-ttu-id="ab54a-120">При сборке пакета с помощью MSBuild файл конфигурации локальной службы добавляется по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ab54a-120">When you build a package by using MSBuild, the local service-configuration file is included by default.</span></span> <span data-ttu-id="ab54a-121">Чтобы добавить другой файл конфигурации, задайте свойство `TargetProfile` команды MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span><span class="sxs-lookup"><span data-stu-id="ab54a-121">To include a different service-configuration file, set the `TargetProfile` property of the MSBuild command (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span></span>

<span data-ttu-id="ab54a-122">Если вы хотите использовать другой каталог для хранения пакета и файлов конфигурации, задайте путь с помощью параметра `/p:PublishDir=Directory\` (включая разделитель в виде обратной косой черты в конце).</span><span class="sxs-lookup"><span data-stu-id="ab54a-122">If you want to use an alternate directory for the stored package and configuration files, set the path by using the `/p:PublishDir=Directory\` option, including the trailing backslash separator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab54a-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab54a-123">Next steps</span></span>
<span data-ttu-id="ab54a-124">Когда пакет скомпилирован, его можно развернуть в Azure.</span><span class="sxs-lookup"><span data-stu-id="ab54a-124">After the package is built, you can deploy it to Azure.</span></span> <span data-ttu-id="ab54a-125">Руководство, демонстрирующее автоматизацию этого процесса, содержится в статье [Непрерывная доставка для облачных служб в Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="ab54a-125">For a tutorial that demonstrates how to automate that process, see [Continuous Delivery for Cloud Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span></span>

