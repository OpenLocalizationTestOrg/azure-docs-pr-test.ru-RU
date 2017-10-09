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
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Создание пользовательских артефактов для виртуальной машины DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Обзор
**Артефакты** используется toodeploy и настроить приложение после подготовки виртуальной Машины. Артефакт состоит из файла определения артефакта и других файлов скриптов, которые хранятся в папке в репозитории Git. Файлы определения артефакта состоят из JSON и выражений, которые можно использовать toospecify выберите tooinstall на виртуальной Машине. Например можно определить имя артефакта, toorun команд и параметров, которые становятся доступными при выполнении команды hello hello. Файлы скриптов tooother в файле определения артефакта hello можно ссылаться по имени.

## <a name="artifact-definition-file-format"></a>Формат файла определения артефакта
Hello ниже приведен пример hello разделов, которые составляют hello базовая структура файла определения.

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

| Имя элемента | Обязательный? | Описание |
| --- | --- | --- |
| $schema |Нет |Расположение файла схемы JSON hello, который помогает в тестировании hello допустимость файла определения hello. |
| title |Да |Имя отображается в лаборатории hello артефакта hello. |
| Описание |Да |Описание отображается в лаборатории hello артефакта hello. |
| iconUri |Нет |URI hello значка, отображаемого в лаборатории hello. |
| targetOsType |Да |Операционная система виртуальной Машины, где установлен артефакта hello. Поддерживаемые параметры: Windows и Linux. |
| parameters |Нет |Значения, предоставляемые, когда на компьютере выполняется команда установки артефакта. Помогает при настройке артефакта. |
| runCommand |Да |Команда установки артефакта, выполняемая на виртуальной машине. |

### <a name="artifact-parameters"></a>Параметры артефакта
В разделе параметров hello файла определения hello укажите значения, которые пользователь может ввести при установке на артефакт. Можно ссылаться toothese значения в команду установки hello артефакта.

Определить параметры с hello следующие структуры:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Имя элемента | Обязательный? | Описание |
| --- | --- | --- |
| type |Да |Тип значения параметра. В разделе hello после списка для hello допустимые типы: |
| displayName |Да |Имя параметра hello, отображаемых tooa пользователя в лаборатории hello. | |
| Описание |Да |Описание параметра hello, отображаемый в лаборатории hello. |

Hello разрешен типы:

* string — любая допустимая строка JSON;
* int — любое допустимое целое число JSON;
* bool — любое допустимое логическое значение JSON;
* array — любой допустимый массив JSON.

## <a name="artifact-expressions-and-functions"></a>Выражения и функции артефактов
Можно использовать выражение и команда установки функции tooconstruct hello артефакта.
Выражения заключены в квадратные скобки ([и]) и оцениваются при установке артефактов hello. Выражения могут встречаться в любом месте строкового значения JSON и всегда возвращают другое значение JSON. Если необходимо toouse строковый литерал, который начинается с квадратная скобка [, необходимо использовать две квадратные скобки [[.
Как правило выражения используются с функциями tooconstruct значение. Как и в языке JavaScript, вызовы функций форматируются в виде functionName(arg1,arg2,arg3).

Hello ниже перечислены основные функции.

* Parameters(ParameterName) - возвращает значение параметра, предоставляется при выполнении команды артефакта hello.
* concat(arg1,arg2,arg3, …..) — объединяет несколько строковых значений. Эта функция может принимать любое количество аргументов.

Следующий пример показывает как Hello toouse выражения и функции tooconstruct значение:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Создание пользовательского артефакта
Для создания пользовательского артефакта выполните следующие действия:

1. Установка редактора JSON — нужно toowork редактор JSON с файлами определения артефакта. Рекомендуем использовать [код Visual Studio](https://code.visualstudio.com/), доступный для Windows, Linux и OS X.
2. Get artifactfile.json образца - извлечение hello артефакты, созданные Azure DevTest Labs команды на наш [репозитории GitHub](https://github.com/Azure/azure-devtestlab), в котором был создан широкую библиотеку артефактов, которые позволяют создать собственную артефакты. Загрузите файл определения артефактов и внесите изменения tooit toocreate собственные артефакты.
3. Пользоваться IntelliSense - допустимые элементы toosee использование IntelliSense, которые могут быть tooconstruct используется файл определения артефакта. Также вы увидите hello различные варианты значения элемента. Например, IntelliSense Показать hello два варианта Windows или Linux, при редактировании hello **targetOsType** элемента.
4. Хранилище артефактов hello в [репозитории](devtest-lab-add-artifact-repo.md).
   
   1. Создайте отдельный каталог для каждого артефакта, где имя каталога hello hello же, как имя артефакта hello.
   2. Сохранить файл определения артефакта hello (artifactfile.json) в созданный каталог hello.
   3. Команда установки сценарии hello хранилища, на которые ссылаются из артефактов hello.
      
      Вот как может выглядеть папка артефакта:
      
      ![Пример репозитория артефактов Git](./media/devtest-lab-artifact-author/git-repo.png)
5. Добавление репозитория toohello hello артефакты лаборатории — см. в статье toohello [добавьте репозитория артефактов и шаблоны](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Связанные статьи
* [Как toodiagnose сбоев артефакта в DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Присоединение виртуальной Машины tooexisting домена AD, с помощью шаблона диспетчера ресурсов в Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[добавьте лаборатории tooa репозитории артефактов Git](devtest-lab-add-artifact-repo.md).

