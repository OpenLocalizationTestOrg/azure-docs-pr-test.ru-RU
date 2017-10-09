---
title: "Набор масштабирования виртуальных машин с помощью Visual Studio aaaDeploy | Документы Microsoft"
description: "Развертывание набора масштабирования виртуальных машин с помощью Visual Studio и шаблона Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a>Как toocreate набора масштабирования виртуальных машин с помощью Visual Studio
В этой статье показано, как toodeploy задать с помощью Visual Studio развертывания группы ресурсов Azure масштабирования виртуальных машин.

[Azure наборы масштабирования виртуальных машин](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) является toodeploy ресурсов вычислений Azure и управлять коллекцией подобных виртуальных машин с автоматически масштабировать и балансировки нагрузки. Масштабируемые наборы виртуальных машин можно подготавливать и развертывать с помощью [шаблонов Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates). Шаблоны Azure Resource Manager можно развертывать с помощью Azure CLI, PowerShell, REST, а также непосредственно из Visual Studio. Visual Studio предоставляет набор примеров шаблонов, которые можно развернуть в рамках проекта развертывания группы ресурсов Azure.

Развертывания группы ресурсов Azure являются toogroup способом и опубликовать набор связанных ресурсов Azure в одной операции развертывания. Дополнительные сведения о них можно получить в статье [Создание и развертывание групп ресурсов Azure с помощью Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="pre-requisites"></a>Предварительные требования
tooget при развертывании набора масштабирования виртуальной машины в Visual Studio, необходимо hello следующее:

* Visual Studio 2013 или более поздней версии
* Пакет SDK Azure версии 2.7, 2.8 или 2.9

>[!NOTE]
>При выполнении этих инструкций предполагается, что вы используете Visual Studio с [пакетом SDK Azure версии 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="creating-a-project"></a>Создание проекта
1. Создайте проект в Visual Studio, выбрав **Файл | Создать | Проект**.
   
    ![Создание файла][file_new]

2. В разделе **Visual C# | Облако**, выберите **диспетчера ресурсов Azure** toocreate проекта для развертывания шаблона диспетчера ресурсов Azure.
   
    ![Создание проекта][create_project]

3. Hello списке шаблонов выберите hello Linux или Windows шаблона набор масштабирования виртуальной машины.
   
   ![Выбор шаблона][select_Template]

4. После создания проекта можно увидеть PowerShell скрипты развертывания, шаблона диспетчера ресурсов Azure и файл параметров для набора масштабирования виртуальных машин hello.
   
    ![Обозреватель решений][solution_explorer]

## <a name="customize-your-project"></a>Настройка проекта
Теперь можно изменить шаблон toocustomize hello его для потребностей вашего приложения, такие как добавление свойств расширения виртуальной Машины или редактирования загрузить правила балансировки. По умолчанию hello шаблоны набор масштабирования виртуальных машин, настроенных toodeploy hello AzureDiagnostics расширения, которое делает его легко tooadd правил автомасштабирования. Кроме того, развертывается подсистема балансировки нагрузки с общедоступным IP-адресом, для которого настроены правила NAT для входящего трафика. 

Hello балансировки нагрузки позволяет соединить экземпляров виртуальных Машин toohello SSH (Linux) и протокола удаленного рабочего СТОЛА (Windows). Hello интерфейсный порт начинается с номера 50000. Для linux это означает, что если вы SSH tooport 50000, являются перенаправленное tooport 22 из hello первая виртуальная машина в наборе масштабирования hello. Подключение tooport 50001 — перенаправленное tooport 22 hello второй виртуальной Машины и т. д.

 Tooedit хорошим способом шаблонов с помощью Visual Studio — toouse hello структуры JSON tooorganize hello параметры, переменные и ресурсы. Изучив hello схемы Visual Studio можно указать ошибки в шаблоне перед ее развертыванием.

![Обозреватель JSON][json_explorer]

## <a name="deploy-hello-project"></a>Развертывание проекта hello
1. Развертывание ресурса набора масштабирования виртуальных машин hello шаблона Azure Resource Manager toocreate hello. Щелкните правой кнопкой мыши узел проекта hello и выберите **развертывание | Новое развертывание**.
   
    ![Развертывание шаблона][5deploy_Template]
    
2. Выберите подписку, в диалоговом окне «TooResource развернуть группу» hello.
   
    ![Развертывание шаблона][6deploy_Template]

3. Здесь можно создать группы ресурсов Azure toodeploy шаблоне.
   
    ![Создание группы ресурсов][new_resource]

4. Далее щелкните **изменение параметров** tooenter параметров, передаваемых tooyour шаблона. Укажите hello имя пользователя и пароль для hello операционной системы, который является обязательным toocreate hello развертывания. При отсутствии инструменты PowerShell для установки Visual Studio, рекомендуется toocheck **сохранить пароли** tooavoid скрытые PowerShell, Командная строка запроса или использовать [keyvault поддержки](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).
   
    ![Изменение параметров][edit_parameters]

5. Щелкните **Развернуть**. Hello **вывода** окно показывает ход выполнения развертывания hello. Обратите внимание, что hello действие выполняется hello **Deploy-AzureResourceGroup.ps1** сценария.
   
   ![Окно вывода][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a>Изучение масштабируемого набора виртуальных машин
После завершения развертывания hello, можно просмотреть hello новый набор масштабирования виртуальных машин в Visual Studio hello **Cloud Explorer** (список hello обновления). Обозреватель облака позволяет управлять ресурсами Azure в Visual Studio при разработке приложений. Можно также просмотреть набор масштабирования виртуальных машин в hello [портал Azure](https://portal.azure.com) и [обозревателя ресурсов Azure](https://resources.azure.com/).

![Cloud Explorer][cloud_explorer]

 Hello портал предоставляет toovisually управления Azure инфраструктурой веб-браузера, а обозревателя ресурсов Azure предоставляет простой способ tooexplore лучше всего hello и отладка ресурсы Azure, предоставляя окна в hello «Просмотр экземпляра» и демонстрируя PowerShell команды для hello ресурсы, которые вы наблюдаете.

## <a name="next-steps"></a>Дальнейшие действия
После успешного развертывания наборы масштабирования виртуальной машины через Visual Studio можно выполнить дальнейшую настройку вашего проекта toosuit требований приложения. Например, настройте автоматическое масштабирование, добавив **Insights** ресурса, добавление tooyour инфраструктуры шаблона (например, автономные виртуальные машины) или развертывании приложений с использованием hello расширение пользовательского скрипта. Хорошим примером шаблоны можно найти в hello [шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates) репозитории GitHub (выполните поиск «vmss»).

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
