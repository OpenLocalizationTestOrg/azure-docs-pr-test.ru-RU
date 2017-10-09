---
title: "aaaCreate пользовательские артефакты для виртуальной Машины DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooauthor собственные артефактов для использования с DevTest Labs"
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
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="65b92-103">Создание пользовательских артефактов для виртуальной машины DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="65b92-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="65b92-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="65b92-104">Overview</span></span>
<span data-ttu-id="65b92-105">**Артефакты** используется toodeploy и настроить приложение после подготовки виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="65b92-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="65b92-106">Артефакт состоит из файла определения артефакта и других файлов скриптов, которые хранятся в папке в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="65b92-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="65b92-107">Файлы определения артефакта состоят из JSON и выражений, которые можно использовать toospecify выберите tooinstall на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="65b92-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="65b92-108">Например можно определить имя артефакта, toorun команд и параметров, которые становятся доступными при выполнении команды hello hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="65b92-109">Файлы скриптов tooother в файле определения артефакта hello можно ссылаться по имени.</span><span class="sxs-lookup"><span data-stu-id="65b92-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="65b92-110">Формат файла определения артефакта</span><span class="sxs-lookup"><span data-stu-id="65b92-110">Artifact definition file format</span></span>
<span data-ttu-id="65b92-111">Hello ниже приведен пример hello разделов, которые составляют hello базовая структура файла определения.</span><span class="sxs-lookup"><span data-stu-id="65b92-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

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

| <span data-ttu-id="65b92-112">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="65b92-112">Element name</span></span> | <span data-ttu-id="65b92-113">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="65b92-113">Required?</span></span> | <span data-ttu-id="65b92-114">Описание</span><span class="sxs-lookup"><span data-stu-id="65b92-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="65b92-115">$schema</span><span class="sxs-lookup"><span data-stu-id="65b92-115">$schema</span></span> |<span data-ttu-id="65b92-116">Нет</span><span class="sxs-lookup"><span data-stu-id="65b92-116">No</span></span> |<span data-ttu-id="65b92-117">Расположение файла схемы JSON hello, который помогает в тестировании hello допустимость файла определения hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="65b92-118">title</span><span class="sxs-lookup"><span data-stu-id="65b92-118">title</span></span> |<span data-ttu-id="65b92-119">Да</span><span class="sxs-lookup"><span data-stu-id="65b92-119">Yes</span></span> |<span data-ttu-id="65b92-120">Имя отображается в лаборатории hello артефакта hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="65b92-121">Описание</span><span class="sxs-lookup"><span data-stu-id="65b92-121">description</span></span> |<span data-ttu-id="65b92-122">Да</span><span class="sxs-lookup"><span data-stu-id="65b92-122">Yes</span></span> |<span data-ttu-id="65b92-123">Описание отображается в лаборатории hello артефакта hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="65b92-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="65b92-124">iconUri</span></span> |<span data-ttu-id="65b92-125">Нет</span><span class="sxs-lookup"><span data-stu-id="65b92-125">No</span></span> |<span data-ttu-id="65b92-126">URI hello значка, отображаемого в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="65b92-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="65b92-127">targetOsType</span></span> |<span data-ttu-id="65b92-128">Да</span><span class="sxs-lookup"><span data-stu-id="65b92-128">Yes</span></span> |<span data-ttu-id="65b92-129">Операционная система виртуальной Машины, где установлен артефакта hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="65b92-130">Поддерживаемые параметры: Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="65b92-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="65b92-131">parameters</span><span class="sxs-lookup"><span data-stu-id="65b92-131">parameters</span></span> |<span data-ttu-id="65b92-132">Нет</span><span class="sxs-lookup"><span data-stu-id="65b92-132">No</span></span> |<span data-ttu-id="65b92-133">Значения, предоставляемые, когда на компьютере выполняется команда установки артефакта.</span><span class="sxs-lookup"><span data-stu-id="65b92-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="65b92-134">Помогает при настройке артефакта.</span><span class="sxs-lookup"><span data-stu-id="65b92-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="65b92-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="65b92-135">runCommand</span></span> |<span data-ttu-id="65b92-136">Да</span><span class="sxs-lookup"><span data-stu-id="65b92-136">Yes</span></span> |<span data-ttu-id="65b92-137">Команда установки артефакта, выполняемая на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="65b92-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="65b92-138">Параметры артефакта</span><span class="sxs-lookup"><span data-stu-id="65b92-138">Artifact parameters</span></span>
<span data-ttu-id="65b92-139">В разделе параметров hello файла определения hello укажите значения, которые пользователь может ввести при установке на артефакт.</span><span class="sxs-lookup"><span data-stu-id="65b92-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="65b92-140">Можно ссылаться toothese значения в команду установки hello артефакта.</span><span class="sxs-lookup"><span data-stu-id="65b92-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="65b92-141">Определить параметры с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="65b92-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="65b92-142">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="65b92-142">Element name</span></span> | <span data-ttu-id="65b92-143">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="65b92-143">Required?</span></span> | <span data-ttu-id="65b92-144">Описание</span><span class="sxs-lookup"><span data-stu-id="65b92-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="65b92-145">type</span><span class="sxs-lookup"><span data-stu-id="65b92-145">type</span></span> |<span data-ttu-id="65b92-146">Да</span><span class="sxs-lookup"><span data-stu-id="65b92-146">Yes</span></span> |<span data-ttu-id="65b92-147">Тип значения параметра.</span><span class="sxs-lookup"><span data-stu-id="65b92-147">Type of parameter value.</span></span> <span data-ttu-id="65b92-148">В разделе hello после списка для hello допустимые типы:</span><span class="sxs-lookup"><span data-stu-id="65b92-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="65b92-149">displayName</span><span class="sxs-lookup"><span data-stu-id="65b92-149">displayName</span></span> |<span data-ttu-id="65b92-150">Да</span><span class="sxs-lookup"><span data-stu-id="65b92-150">Yes</span></span> |<span data-ttu-id="65b92-151">Имя параметра hello, отображаемых tooa пользователя в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="65b92-152">Описание</span><span class="sxs-lookup"><span data-stu-id="65b92-152">description</span></span> |<span data-ttu-id="65b92-153">Да</span><span class="sxs-lookup"><span data-stu-id="65b92-153">Yes</span></span> |<span data-ttu-id="65b92-154">Описание параметра hello, отображаемый в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="65b92-155">Hello разрешен типы:</span><span class="sxs-lookup"><span data-stu-id="65b92-155">hello allowed types are:</span></span>

* <span data-ttu-id="65b92-156">string — любая допустимая строка JSON;</span><span class="sxs-lookup"><span data-stu-id="65b92-156">string – any valid JSON string</span></span>
* <span data-ttu-id="65b92-157">int — любое допустимое целое число JSON;</span><span class="sxs-lookup"><span data-stu-id="65b92-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="65b92-158">bool — любое допустимое логическое значение JSON;</span><span class="sxs-lookup"><span data-stu-id="65b92-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="65b92-159">array — любой допустимый массив JSON.</span><span class="sxs-lookup"><span data-stu-id="65b92-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="65b92-160">Выражения и функции артефактов</span><span class="sxs-lookup"><span data-stu-id="65b92-160">Artifact expressions and functions</span></span>
<span data-ttu-id="65b92-161">Можно использовать выражение и команда установки функции tooconstruct hello артефакта.</span><span class="sxs-lookup"><span data-stu-id="65b92-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="65b92-162">Выражения заключены в квадратные скобки ([и]) и оцениваются при установке артефактов hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="65b92-163">Выражения могут встречаться в любом месте строкового значения JSON и всегда возвращают другое значение JSON.</span><span class="sxs-lookup"><span data-stu-id="65b92-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="65b92-164">Если необходимо toouse строковый литерал, который начинается с квадратная скобка [, необходимо использовать две квадратные скобки [[.</span><span class="sxs-lookup"><span data-stu-id="65b92-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="65b92-165">Как правило выражения используются с функциями tooconstruct значение.</span><span class="sxs-lookup"><span data-stu-id="65b92-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="65b92-166">Как и в языке JavaScript, вызовы функций форматируются в виде functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="65b92-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="65b92-167">Hello ниже перечислены основные функции.</span><span class="sxs-lookup"><span data-stu-id="65b92-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="65b92-168">Parameters(ParameterName) - возвращает значение параметра, предоставляется при выполнении команды артефакта hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="65b92-169">concat(arg1,arg2,arg3, …..) — объединяет несколько строковых значений.</span><span class="sxs-lookup"><span data-stu-id="65b92-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="65b92-170">Эта функция может принимать любое количество аргументов.</span><span class="sxs-lookup"><span data-stu-id="65b92-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="65b92-171">Следующий пример показывает как Hello toouse выражения и функции tooconstruct значение:</span><span class="sxs-lookup"><span data-stu-id="65b92-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="65b92-172">Создание пользовательского артефакта</span><span class="sxs-lookup"><span data-stu-id="65b92-172">Create a custom artifact</span></span>
<span data-ttu-id="65b92-173">Для создания пользовательского артефакта выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="65b92-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="65b92-174">Установка редактора JSON — нужно toowork редактор JSON с файлами определения артефакта.</span><span class="sxs-lookup"><span data-stu-id="65b92-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="65b92-175">Рекомендуем использовать [код Visual Studio](https://code.visualstudio.com/), доступный для Windows, Linux и OS X.</span><span class="sxs-lookup"><span data-stu-id="65b92-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="65b92-176">Get artifactfile.json образца - извлечение hello артефакты, созданные Azure DevTest Labs команды на наш [репозитории GitHub](https://github.com/Azure/azure-devtestlab), в котором был создан широкую библиотеку артефактов, которые позволяют создать собственную артефакты.</span><span class="sxs-lookup"><span data-stu-id="65b92-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="65b92-177">Загрузите файл определения артефактов и внесите изменения tooit toocreate собственные артефакты.</span><span class="sxs-lookup"><span data-stu-id="65b92-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="65b92-178">Пользоваться IntelliSense - допустимые элементы toosee использование IntelliSense, которые могут быть tooconstruct используется файл определения артефакта.</span><span class="sxs-lookup"><span data-stu-id="65b92-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="65b92-179">Также вы увидите hello различные варианты значения элемента.</span><span class="sxs-lookup"><span data-stu-id="65b92-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="65b92-180">Например, IntelliSense Показать hello два варианта Windows или Linux, при редактировании hello **targetOsType** элемента.</span><span class="sxs-lookup"><span data-stu-id="65b92-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="65b92-181">Хранилище артефактов hello в [репозитории](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="65b92-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="65b92-182">Создайте отдельный каталог для каждого артефакта, где имя каталога hello hello же, как имя артефакта hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="65b92-183">Сохранить файл определения артефакта hello (artifactfile.json) в созданный каталог hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="65b92-184">Команда установки сценарии hello хранилища, на которые ссылаются из артефактов hello.</span><span class="sxs-lookup"><span data-stu-id="65b92-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="65b92-185">Вот как может выглядеть папка артефакта:</span><span class="sxs-lookup"><span data-stu-id="65b92-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Пример репозитория артефактов Git](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="65b92-187">Добавление репозитория toohello hello артефакты лаборатории — см. в статье toohello [добавьте репозитория артефактов и шаблоны](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="65b92-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="65b92-188">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="65b92-188">Related articles</span></span>
* [<span data-ttu-id="65b92-189">Как toodiagnose сбоев артефакта в DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="65b92-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="65b92-190">Присоединение виртуальной Машины tooexisting домена AD, с помощью шаблона диспетчера ресурсов в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="65b92-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="65b92-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65b92-191">Next steps</span></span>
* <span data-ttu-id="65b92-192">Узнайте, каким образом слишком[добавьте лаборатории tooa репозитории артефактов Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="65b92-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

