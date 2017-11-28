---
title: "Создание пользовательских артефактов для виртуальной машины DevTest Labs | Документация Майкрософт"
description: "Узнайте, как создавать собственные артефакты, которые можно использовать с помощью решения DevTest Lab."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2412033daa1d97860dd9f380178622b1ddc590c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="2f6ea-103">Создание пользовательских артефактов для виртуальной машины DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2f6ea-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="2f6ea-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2f6ea-104">Overview</span></span>
<span data-ttu-id="2f6ea-105">**Артефакты** используются для развертывания и настройки приложения после подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="2f6ea-106">Артефакт состоит из файла определения артефакта и других файлов скриптов, которые хранятся в папке в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="2f6ea-107">Файлы определения артефактов состоят из JSON и выражений, позволяющих указать, какие компоненты должны быть установлены на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="2f6ea-108">Например, можно определить имя артефакта, выполняемую команду и параметры, которые станут доступны после запуска команды.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-108">For example, you can define the name of an artifact, command to run, and parameters that are made available when the command is run.</span></span> <span data-ttu-id="2f6ea-109">В файле определения артефакта можно ссылаться на другие файлы скриптов, используя их имена.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-109">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="2f6ea-110">Формат файла определения артефакта</span><span class="sxs-lookup"><span data-stu-id="2f6ea-110">Artifact definition file format</span></span>
<span data-ttu-id="2f6ea-111">В следующем примере показаны разделы, составляющие базовую структуру файла определения:</span><span class="sxs-lookup"><span data-stu-id="2f6ea-111">The following example shows the sections that make up the basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="2f6ea-112">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="2f6ea-112">Element name</span></span> | <span data-ttu-id="2f6ea-113">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="2f6ea-113">Required?</span></span> | <span data-ttu-id="2f6ea-114">Описание</span><span class="sxs-lookup"><span data-stu-id="2f6ea-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f6ea-115">$schema</span><span class="sxs-lookup"><span data-stu-id="2f6ea-115">$schema</span></span> |<span data-ttu-id="2f6ea-116">Нет</span><span class="sxs-lookup"><span data-stu-id="2f6ea-116">No</span></span> |<span data-ttu-id="2f6ea-117">Расположение файла схемы JSON, позволяющего проверять подлинность файла определения.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span></span> |
| <span data-ttu-id="2f6ea-118">title</span><span class="sxs-lookup"><span data-stu-id="2f6ea-118">title</span></span> |<span data-ttu-id="2f6ea-119">Да</span><span class="sxs-lookup"><span data-stu-id="2f6ea-119">Yes</span></span> |<span data-ttu-id="2f6ea-120">Имя артефакта отображается в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-120">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="2f6ea-121">Описание</span><span class="sxs-lookup"><span data-stu-id="2f6ea-121">description</span></span> |<span data-ttu-id="2f6ea-122">Да</span><span class="sxs-lookup"><span data-stu-id="2f6ea-122">Yes</span></span> |<span data-ttu-id="2f6ea-123">Описание артефакта отображается в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-123">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="2f6ea-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="2f6ea-124">iconUri</span></span> |<span data-ttu-id="2f6ea-125">Нет</span><span class="sxs-lookup"><span data-stu-id="2f6ea-125">No</span></span> |<span data-ttu-id="2f6ea-126">URI значка отображается в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-126">Uri of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="2f6ea-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="2f6ea-127">targetOsType</span></span> |<span data-ttu-id="2f6ea-128">Да</span><span class="sxs-lookup"><span data-stu-id="2f6ea-128">Yes</span></span> |<span data-ttu-id="2f6ea-129">Операционная система виртуальной машины, на которую устанавливается артефакт.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-129">Operating system of the VM where artifact is installed.</span></span> <span data-ttu-id="2f6ea-130">Поддерживаемые параметры: Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="2f6ea-131">parameters</span><span class="sxs-lookup"><span data-stu-id="2f6ea-131">parameters</span></span> |<span data-ttu-id="2f6ea-132">Нет</span><span class="sxs-lookup"><span data-stu-id="2f6ea-132">No</span></span> |<span data-ttu-id="2f6ea-133">Значения, предоставляемые, когда на компьютере выполняется команда установки артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="2f6ea-134">Помогает при настройке артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="2f6ea-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="2f6ea-135">runCommand</span></span> |<span data-ttu-id="2f6ea-136">Да</span><span class="sxs-lookup"><span data-stu-id="2f6ea-136">Yes</span></span> |<span data-ttu-id="2f6ea-137">Команда установки артефакта, выполняемая на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="2f6ea-138">Параметры артефакта</span><span class="sxs-lookup"><span data-stu-id="2f6ea-138">Artifact parameters</span></span>
<span data-ttu-id="2f6ea-139">В разделе параметров файла определения указываются значения, которые пользователь может вводить при установке артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="2f6ea-140">Это значения можно использовать в команде установки артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-140">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="2f6ea-141">Параметры определяются с помощью следующей структуры.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-141">You define parameters with the following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="2f6ea-142">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="2f6ea-142">Element name</span></span> | <span data-ttu-id="2f6ea-143">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="2f6ea-143">Required?</span></span> | <span data-ttu-id="2f6ea-144">Описание</span><span class="sxs-lookup"><span data-stu-id="2f6ea-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f6ea-145">type</span><span class="sxs-lookup"><span data-stu-id="2f6ea-145">type</span></span> |<span data-ttu-id="2f6ea-146">Да</span><span class="sxs-lookup"><span data-stu-id="2f6ea-146">Yes</span></span> |<span data-ttu-id="2f6ea-147">Тип значения параметра.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-147">Type of parameter value.</span></span> <span data-ttu-id="2f6ea-148">Ниже приведен список допустимых типов.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-148">See the following list for the allowed types:</span></span> |
| <span data-ttu-id="2f6ea-149">displayName</span><span class="sxs-lookup"><span data-stu-id="2f6ea-149">displayName</span></span> |<span data-ttu-id="2f6ea-150">Да</span><span class="sxs-lookup"><span data-stu-id="2f6ea-150">Yes</span></span> |<span data-ttu-id="2f6ea-151">Имя параметра, отображаемое для пользователя в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-151">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="2f6ea-152">Описание</span><span class="sxs-lookup"><span data-stu-id="2f6ea-152">description</span></span> |<span data-ttu-id="2f6ea-153">Да</span><span class="sxs-lookup"><span data-stu-id="2f6ea-153">Yes</span></span> |<span data-ttu-id="2f6ea-154">Описание параметра, отображаемого в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-154">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="2f6ea-155">Допустимые типы:</span><span class="sxs-lookup"><span data-stu-id="2f6ea-155">The allowed types are:</span></span>

* <span data-ttu-id="2f6ea-156">string — любая допустимая строка JSON;</span><span class="sxs-lookup"><span data-stu-id="2f6ea-156">string – any valid JSON string</span></span>
* <span data-ttu-id="2f6ea-157">int — любое допустимое целое число JSON;</span><span class="sxs-lookup"><span data-stu-id="2f6ea-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="2f6ea-158">bool — любое допустимое логическое значение JSON;</span><span class="sxs-lookup"><span data-stu-id="2f6ea-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="2f6ea-159">array — любой допустимый массив JSON.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="2f6ea-160">Выражения и функции артефактов</span><span class="sxs-lookup"><span data-stu-id="2f6ea-160">Artifact expressions and functions</span></span>
<span data-ttu-id="2f6ea-161">Для ограничения команды установки артефактов можно использовать выражения и функции.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-161">You can use expression and functions to construct the artifact install command.</span></span>
<span data-ttu-id="2f6ea-162">Выражения заключаются в квадратные скобки ([ и ]) и вычисляются при установке артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="2f6ea-163">Выражения могут встречаться в любом месте строкового значения JSON и всегда возвращают другое значение JSON.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="2f6ea-164">Если нужно использовать строковый литерал, который начинается с квадратной скобки ([), необходимо указать две квадратные скобки ([[).</span><span class="sxs-lookup"><span data-stu-id="2f6ea-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="2f6ea-165">Как правило, для составления значения используются выражения с функциями.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-165">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="2f6ea-166">Как и в языке JavaScript, вызовы функций форматируются в виде functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="2f6ea-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="2f6ea-167">Ниже приведен список распространенных функций.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-167">The following list shows common functions:</span></span>

* <span data-ttu-id="2f6ea-168">parameters(parameterName) — возвращает значение параметра, предоставляемого при выполнении команды артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="2f6ea-169">concat(arg1,arg2,arg3, …..) — объединяет несколько строковых значений.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="2f6ea-170">Эта функция может принимать любое количество аргументов.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="2f6ea-171">В следующем примере показано, как составить значение, используя выражение и функции:</span><span class="sxs-lookup"><span data-stu-id="2f6ea-171">The following example shows how to use expression and functions to construct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="2f6ea-172">Создание пользовательского артефакта</span><span class="sxs-lookup"><span data-stu-id="2f6ea-172">Create a custom artifact</span></span>
<span data-ttu-id="2f6ea-173">Для создания пользовательского артефакта выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2f6ea-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="2f6ea-174">Установите редактор JSON — он требуется для работы с файлами определения артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-174">Install a JSON editor - You need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="2f6ea-175">Рекомендуем использовать [код Visual Studio](https://code.visualstudio.com/), доступный для Windows, Linux и OS X.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="2f6ea-176">Получите пример файла artifactfile.json — изучите артефакты, созданные командой Azure DevTest Labs, в [репозитории GitHub](https://github.com/Azure/azure-devtestlab). Он содержит богатую библиотеку артефактов, которая поможет вам создавать собственные артефакты.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="2f6ea-177">Загрузите файл определения артефакта и внесите в него изменения, чтобы создать свои собственные артефакты.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-177">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="2f6ea-178">Используйте IntelliSense — он позволяет просматривать элементы, которые можно использовать для создания файла определения артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span></span> <span data-ttu-id="2f6ea-179">Здесь же можно увидеть различные варианты значений каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-179">You can also see the different options for values of an element.</span></span> <span data-ttu-id="2f6ea-180">Например, при редактировании элемента **targetOsType** IntelliSense предлагает два варианта — Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span></span>
4. <span data-ttu-id="2f6ea-181">Сохраните артефакт в [репозитории Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ea-181">Store the artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="2f6ea-182">Создайте для каждого артефакта отдельный каталог, имя которого совпадает с именем артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span></span>
   2. <span data-ttu-id="2f6ea-183">Сохраните файл определения артефакта (artifactfile.json) в созданный каталог.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span></span>
   3. <span data-ttu-id="2f6ea-184">Сохранить скрипты, на которые ссылается команда установки артефакта.</span><span class="sxs-lookup"><span data-stu-id="2f6ea-184">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="2f6ea-185">Вот как может выглядеть папка артефакта:</span><span class="sxs-lookup"><span data-stu-id="2f6ea-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Пример репозитория артефактов Git](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="2f6ea-187">Добавьте репозиторий артефактов в лабораторию. Ознакомьтесь со статьей [Добавление репозитория Git для хранения пользовательских артефактов и шаблонов Azure Resource Manager в Azure DevTest Labs](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ea-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="2f6ea-188">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="2f6ea-188">Related articles</span></span>
* [<span data-ttu-id="2f6ea-189">Диагностика сбоев артефактов на виртуальной машине Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2f6ea-189">How to diagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* <span data-ttu-id="2f6ea-190">[Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs) (Присоединение виртуальной машины к существующему домену AD с помощью шаблона ARM в Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="2f6ea-190">[Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f6ea-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f6ea-191">Next steps</span></span>
* <span data-ttu-id="2f6ea-192">Узнайте, как [добавить репозиторий артефактов Git в лабораторию](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ea-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

