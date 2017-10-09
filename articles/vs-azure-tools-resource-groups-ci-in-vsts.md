---
title: "Интеграция aaaContinuous в VS Team Services с помощью проектов группы ресурсов Azure | Документы Microsoft"
description: "Описывает, каким образом tooset непрерывной интеграции в Visual Studio Team Services с помощью развертывания группы ресурсов Azure для проектов в Visual Studio."
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Непрерывная интеграция в Visual Studio Team Services с использованием проектов развертывания группы ресурсов Azure
toodeploy шаблон Azure, выполнении задач на разных этапах: сборки, тестирования, tooAzure копии (также называется «Промежуточный») и развертывания шаблона. Существует два способа toodeploy шаблоны tooVisual Studio Team Services (VS Team Services). Оба метода предоставляют одинаковые результаты hello, поэтому нажмите hello, который наилучшим образом соответствует рабочего процесса.

1. Добавьте определение сборки tooyour одного шага, которое запускает сценарий PowerShell hello, включенный в проект развертывания группы ресурсов Azure hello (Deploy-AzureResourceGroup.ps1). Hello скрипт копирует артефакты, а затем развертывает hello шаблона.
2. Добавьте несколько этапов сборки VSTS, на каждом из которых выполняется одна задача этапа.

В этой статье показаны оба варианта. Первый вариант Hello имеет преимущество hello помощью hello же скрипт используется разработчиками в Visual Studio и позволяет обеспечить согласованность на протяжении жизненного цикла hello. Второй параметр Hello предлагает удобный альтернативный toohello Встроенные скрипта. Обе процедуры предполагают, что проект развертывания Visual Studio записан после изменения в VS Team Services.

## <a name="copy-artifacts-tooazure"></a>Копирование артефактов tooAzure
Независимо от того, сценарий hello Если у вас есть все артефакты, необходимые для развертывания шаблона необходимо предоставить toothem доступ диспетчера ресурсов Azure. Эти артефакты могут включить такие файлы:

* вложенные шаблоны;
* сценарии конфигурации и DSC;
* двоичные файлы приложения.

### <a name="nested-templates-and-configuration-scripts"></a>Вложенные шаблоны и сценарии конфигурации
При использовании шаблонов hello, предоставляемые Visual Studio (или, созданного с помощью Visual Studio фрагменты) hello сценарий PowerShell не только готовит hello артефакты, он также выполняет параметризацию hello URI для hello ресурсов для различных развертываний. сценарий Hello затем копирует hello артефакты tooa безопасный контейнер в Azure, создает маркер SaS для контейнера и затем передает данные на toohello шаблона-развертывания. В разделе [Создание шаблона-развертывания](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn Дополнительные сведения о вложенных шаблонов.  При использовании задачи в VS Team Services, необходимо выбрать соответствующие задачи hello для развертывания шаблона и при необходимости передавать значения параметров из промежуточного шага развертывания шаблона toohello hello.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>Настройка непрерывного развертывания в VSTS
Сценарий PowerShell toocall hello в VS Team Services, необходимо tooupdate определение сборки. Вкратце hello показаны следующие действия. 

1. Измените определение сборки hello.
2. Настроить авторизацию Azure в VSTS.
3. Добавьте шаг построения Azure PowerShell, который ссылается на сценарий PowerShell hello в проект развертывания группы ресурсов Azure hello.
4. Задайте значение hello hello *- ArtifactsStagingDirectory* toowork параметр с проекта, созданного в VS Team Services.

### <a name="detailed-walkthrough-for-option-1"></a>Подробное пошаговое руководство для варианта 1
Hello следующие процедуры описывают hello действия необходимые tooconfigure непрерывного развертывания в VS Team Services с помощью одна задача, которая запускает сценарий PowerShell hello в своем проекте. 

1. Измените определение сборки VSTS и добавьте этап сборки Azure PowerShell. Выберите определение сборки hello под hello **определений сборки** категорию и выберите hello **изменить** ссылку.
   
   ![Изменение определения сборки][0]
2. Добавьте новый **Azure PowerShell** определение построения toohello шаг построения, а затем выберите hello **добавить шаг сборки...** .
   
   ![Добавление шага сборки][1]
3. Выберите hello **задачи развертывания** категории, выберите hello **Azure PowerShell** задач, а затем выберите его **добавить** кнопки.
   
   ![Добавление задач][2]
4. Выберите hello **Azure PowerShell** шаг сборки и заполните его значения.
   
   1. Если у вас уже есть конечной точки службы Azure добавлен tooVS Team Services, выберите подписку hello в hello **подписки Azure** раскрывающегося списка и нажмите кнопку Пропустить toohello следующего раздела. 
      
      Если нет конечной точки службы Azure в VS Team Services, необходимо tooadd один. В этом подразделе описывается процесс hello. Если учетная запись Azure использует учетную запись Майкрософт (например, Hotmail), необходимо выполнить следующие шаги tooget hello проверку подлинности субъекта-службы.
   2. Выберите hello **управление** ссылку Далее toohello **подписки Azure** раскрывающегося списка.
      
      ![Управление подписками Azure][3]
   3. Выберите **Azure** в hello **новую конечную точку службы** раскрывающегося списка.
      
      ![Новая конечная точка службы][4]
   4. В hello **добавления подписки Azure** диалоговое окно, выберите hello **участника-службы** параметр.
      
      ![Параметр субъекта-службы][5]
   5. Добавить сведения о вашей подписке Azure toohello **добавления подписки Azure** диалоговое окно. Требуется tooprovide hello следующих элементов:
      
      * идентификатор подписки;
      * Название подписки
      * идентификатор субъекта-службы;
      * ключ субъекта-службы;
      * Идентификатор клиента
   6. Добавьте имя вашего выбора toohello **подписки** поле «имя». Это значение отображается в hello **подписки Azure** раскрывающегося списка в VS Team Services. 
   7. Если вы не знаете идентификатор подписки Azure, можно использовать один из следующих команд tooretrieve hello его.
      
      Для сценариев Azure PowerShell:
      
      `Get-AzureRmSubscription`
      
      Для интерфейса командной строки Azure:
      
      `azure account show`
   8. tooget идентификатор субъекта-службы ключ субъекта-службы и идентификатор клиента, выполните процедуру hello в [Active Directory, создать приложение и участника службы с помощью портала](resource-group-create-service-principal-portal.md) или [участника службы с проверкой подлинности Диспетчер ресурсов Azure](resource-group-authenticate-service-principal.md).
   9. Добавить hello идентификатор участника службы, ключ субъекта-службы и идентификатор клиента toohello значения **добавления подписки Azure** диалоговое окно и выбрать hello **ОК** кнопки.
      
      Теперь у вас есть hello toorun допустимый toouse участника-службы скрипт Azure PowerShell.
5. Изменить определение сборки hello и выберите hello **Azure PowerShell** шаг сборки. Выберите подписку hello в hello **подписки Azure** раскрывающегося списка. (Если hello подписки не отображается, выберите hello **обновление** кнопку Далее hello **управление** ссылку.) 
   
   ![Настройка задачи сборки Azure PowerShell][8]
6. Укажите путь toohello сценарий Deploy-AzureResourceGroup.ps1 PowerShell. toodo это, выберите toohello далее кнопку с многоточием (...) hello **путь к скрипту** перейдите toohello сценария PowerShell Deploy-AzureResourceGroup.ps1 в hello **сценариев** папки проекта, выберите его, а затем выберите hello **ОК** кнопки.    
   
   ![Выберите путь tooscript][9]
7. После выбора сценария hello hello путь toohello скрипт обновления, чтобы ее запуск выполняется из hello Build.StagingDirectory (hello же каталоге, *ArtifactsLocation* имеет значение). Это можно сделать, добавив «$(Build.StagingDirectory)/ «toohello начало путь к скрипту hello.
   
    ![Измените путь tooscript][10]
8. В hello **аргументы сценария** введите hello следующие параметры (в одной строке). При запуске скрипта hello в Visual Studio, можно увидеть, как используется VS hello параметров в hello **вывода** окна. Это можно использовать в качестве отправной точки для задания значений параметров hello в этапа построения.
   
   | Параметр | Описание |
   | --- | --- |
   | -ResourceGroupLocation |Здравствуйте, значение географического расположения, где hello находится группа ресурсов, таких как **eastus** или **«Восток США»**. (Добавить одинарные кавычки, если имеется пробел в имени hello.) Дополнительные сведения см. в статье о [регионах Azure](https://azure.microsoft.com/en-us/regions/). |
   | -ResourceGroupName |Имя группы ресурсов hello, используемой для этого развертывания Hello. |
   | -UploadArtifacts |Этот параметр, если присутствует, указывает, артефакты, которые должны toobe загружен tooAzure из локальной системы hello. Только tooset данный параметр необходим, если развертывание шаблона требует дополнительных артефактов, которые должны toostage, с помощью сценария PowerShell hello (например, сценарии настройки или вложенные шаблоны). |
   | -StorageAccountName |Имя учетной записи хранилища hello Hello используется toostage артефакты для этого развертывания. Этот параметр используется только в том случае, если применяется промежуточное хранение артефактов для развертывания. Если этот параметр задан, новую учетную запись хранения создается в том случае, если скрипт hello не создан во время предыдущего развертывания. Если указан параметр hello, hello учетной записи хранения уже должна существовать. |
   | -StorageAccountResourceGroupName |Имя группы ресурсов hello, связанный с учетной записью хранения hello Hello. Этот параметр является обязательным только в том случае, если указать значение для параметра StorageAccountName hello. |
   | -TemplateFile |Hello путь к файлу шаблона toohello в проект развертывания группы ресурсов Azure hello. гибкость tooenhance, используйте путь для этого параметра, toohello относительное расположение hello сценарий PowerShell, а не является абсолютным. |
   | -TemplateParametersFile |Hello путь к файлу параметров toohello в проект развертывания группы ресурсов Azure hello. гибкость tooenhance, используйте путь для этого параметра, toohello относительное расположение hello сценарий PowerShell, а не является абсолютным. |
   | -ArtifactStagingDirectory |Этот параметр позволяет сценарий PowerShell hello знать hello папки, из которой следует копировать двоичные файлы проекта hello. Это значение переопределяет значение по умолчанию hello, используемые hello сценарий PowerShell. Для использования VS Team Services, установите значение hello: $(Build.StagingDirectory) - ArtifactStagingDirectory |
   
   Ниже приведен пример аргументов сценария (разрывы строк — для удобства чтения):
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   После завершения hello **аргументы сценария** поле должен быть похож на следующий список hello:
   
   ![Аргументы сценария][11]
9. После добавления всех hello Azure PowerShell шага построения toohello необходимые элементы, выберите hello **очереди** построения проекта hello toobuild кнопки. Hello **построения** экрана показаны выходные данные hello hello сценарий PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Подробное пошаговое руководство для варианта 2
Hello следующие процедуры описывают hello действия необходимые tooconfigure непрерывного развертывания в VS Team Services с помощью встроенных задач hello.

1. Изменение вашей VS Team Services определения tooadd две новые сборки этапы построения. Выберите определение сборки hello под hello **определений сборки** категорию и выберите hello **изменить** ссылку.
   
   ![Изменение определения сборки][12]
2. Hello добавить новые шаги построения toohello определение сборки, с помощью hello **добавить шаг сборки...** .
   
   ![Добавление шага сборки][13]
3. Выберите hello **развернуть** категории задач, выберите hello **копирование файлов Azure** задач, а затем выберите его **добавить** кнопки.
   
   ![Добавление задачи копирования файлов Azure][14]
4. Выберите hello **развертывания группы ресурсов Azure** задач, а затем выберите его **добавить** кнопки и затем **закрыть** hello **задачи каталога**.
   
   ![Добавление задачи развертывания группы ресурсов Azure][15]
5. Выберите hello **копирование файлов Azure** задач и заполните его значения.
   
   Если у вас уже есть конечной точки службы Azure добавлен tooVS Team Services, выберите подписку hello в hello **подписки Azure** раскрывающегося списка. Если у вас нет подписки, ознакомьтесь с [вариантом 1](#detailed-walkthrough-for-option-1), чтобы получить инструкции по ее настройке в VS Team Services.
   
   * "Источник": введите **$(Build.StagingDirectory)**.
   * "Тип подключения Azure": выберите **Azure Resource Manager**.
   * Подписка Azure RM - выберите hello подписки для учетной записи хранения hello требуется toouse в hello **подписки Azure** раскрывающегося списка. Если подписка hello не отображается, выберите hello **обновление** кнопку Далее hello **управление** ссылку.
   * "Тип назначения": выберите **BLOB-объект Azure**.
   * RM учетной записи хранения - выберите учетную запись хранилища hello, вы хотите toouse для промежуточных артефактов
   * Имя контейнера — введите имя hello контейнера hello хотелось бы toouse для промежуточного хранения; она может быть любое допустимое имя контейнера, но использовать одно определение построения выделенный toothis
   
   Для вывода значений hello:
   
   * "Код URI контейнера хранилища": введите **artifactsLocation**.
   * "Токен SAS контейнера хранилища": введите **artifactsLocationSasToken**.
   
   ![Настройка задачи копирования файлов Azure][16]
6. Выберите hello **развертывания группы ресурсов Azure** шаг сборки и заполните его значения.
   
   * "Тип подключения Azure": выберите **Azure Resource Manager**.
   * Подписка Azure RM - hello выберите подписку для развертывания в hello **подписки Azure** раскрывающегося списка. В предыдущем шаге hello обычно это будет использовать ту же подписку hello
   * "Действие": выберите **Create or Update Resource Group** (Создание или изменение группы ресурсов).
   * Группа ресурсов — выберите группу ресурсов или введите hello имя группы ресурсов для развертывания hello
   * Расположение — hello выберите расположение для группы ресурсов hello
   * Шаблон - введите hello путь и имя для добавляя toobe развертывания шаблона hello **$(Build.StagingDirectory)**, например: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Введите параметры шаблона - hello путь и имя toobe параметры hello используется, добавляя **$(Build.StagingDirectory)**, например: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Переопределение параметров шаблона — введите или скопируйте и вставьте следующий код hello:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Настройка задачи развертывания группы ресурсов Azure][17]
7. После добавления всех элементов hello требуется сохранить определение сборки hello и выберите **в очередь новую сборку** вверху hello.

## <a name="next-steps"></a>Дальнейшие действия
Чтение [Обзор диспетчера ресурсов Azure](azure-resource-manager/resource-group-overview.md) toolearn Дополнительные сведения о диспетчере ресурсов Azure и группы ресурсов Azure.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
