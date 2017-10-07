---
title: "aaaAzure мониторинг и виртуальных машинах | Документы Microsoft"
description: "Руководство по мониторингу виртуальных машин Windows с помощью Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>Мониторинг виртуальных машин Windows с помощью Azure PowerShell

Мониторинг Azure использует агенты toocollect загрузки и данные о производительности из виртуальных машин Azure, сохранение этих данных в хранилище Azure и сделать доступными через портал, модуля Azure PowerShell hello и hello Azure CLI. Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Включение диагностики загрузки на виртуальной машине
> * Просмотр диагностики загрузки
> * Просмотр метрик узла виртуальной машины
> * Установка расширения диагностики hello
> * Просмотр метрик виртуальной машины
> * Создание оповещения
> * Настройка расширенного мониторинга.

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).

Пример hello toocomplete в этом учебнике, необходимо иметь существующую виртуальную машину. Этот [пример сценария](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) позволяет создать ее при необходимости. При работе в учебнике hello, замените hello группы ресурсов, имя виртуальной Машины и расположение при необходимости.

## <a name="view-boot-diagnostics"></a>Просмотр диагностики загрузки

Как загрузиться виртуальных машинах агент диагностики загрузки hello захватывает экране, который можно использовать для устранения неполадок цели. Эта возможность включена по умолчанию. Hello захвата экрана, снимки хранятся в учетной записи хранилища Azure, которая также создается по умолчанию. 

Можно получить данные диагностики загрузки hello с hello [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) команды. В следующем примере hello, диагностика загрузки являются корнем загруженный toohello hello * c:\* диска. 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>Просмотр метрик узла.

Виртуальная машина Windows имеет выделенный узел виртуальной машины в Azure, с которым она взаимодействует. Метрики автоматически собираются для hello узла и могут просматриваться в hello портал Azure.

1. В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.
2. Нажмите кнопку **метрики** на hello колонки виртуальной Машины, а затем выберите любой из метрик узла hello под **доступные метрики** toosee, как работает hello виртуальной Машины для узла.

    ![Просмотр метрик узла.](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>Установка расширения диагностики

Hello узла основные метрики доступны, но toosee более детального и метрики конкретной виртуальной Машины, вы tooneed tooinstall hello Azure расширение диагностики в hello виртуальной Машины. Hello расширения службы диагностики Azure позволяет дополнительные функции мониторинга и диагностики toobe данные, полученные из hello виртуальной Машины. Можно просматривать эти метрики производительности и создание предупреждений в зависимости от того, как выполняется hello виртуальной Машины. Hello диагностического расширения устанавливаются с помощью портала Azure hello следующим образом:

1. В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.
2. Щелкните **Параметры диагностики**. Показывает, что список Hello *загрузки диагностики* уже включены в предыдущем разделе hello. Установите флажок hello для *базовые показатели*.
3. Нажмите кнопку hello **Включите мониторинг на уровне гостя** кнопки.

    ![Просмотр метрик диагностики](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>Просмотр метрик виртуальной машины

Можно просмотреть метрики виртуальной Машины hello в hello просмотрены показателей виртуальной Машины узла hello следующим образом:

1. В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.
2. toosee о выполнении hello виртуальной Машины, щелкните **метрики** на hello колонки виртуальной Машины, а затем выберите любой из метрик hello диагностики в разделе **доступные метрики**.

    ![Просмотр метрик виртуальной машины](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>Создание оповещений

На основе метрик производительности можно создавать оповещения. Предупреждения может быть используется toonotify, когда средняя загрузка ЦП превышает пороговое значение или свободного дискового пространства падает ниже определенного, например. Оповещения отображаются в hello портал Azure или могут отправляться по электронной почте. Вы можете запускать Runbook автоматизации Azure или логику приложения Azure в создаваемый tooalerts ответа.

Hello следующий пример создает оповещение о среднем использовании ЦП.

1. В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.
2. Нажмите кнопку **предупреждения правила** hello колонки виртуальной Машины, затем щелкните **добавить оповещение метрики** hello верхней части колонки hello предупреждения.
4. Укажите **имя** оповещения, например *myAlertRule*.
5. tootrigger предупреждение, если процент использования ЦП превышает 1.0 на пять минут, оставьте hello все остальные значения по умолчанию выбран.
6. При необходимости установите флажок "hello" для *электронной почты, владельцы, участники и читатели* toosend уведомление по электронной почте. Действие по умолчанию Hello — toopresent уведомления на портале hello.
7. Нажмите кнопку hello **ОК** кнопки.

## <a name="advanced-monitoring"></a>Расширенный мониторинг 

Более сложный мониторинг виртуальной машины можно выполнить с помощью [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Зарегистрируйтесь для получения [бесплатной пробной версии](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) Operations Management Suite, если вы еще не сделали этого.

При наличии портал OMS toohello доступа hello идентификатор рабочей области ключ и рабочей области можно найти в колонке параметров hello. Используйте hello [набор AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) toohello cmmand tootooadd hello OMS расширения виртуальной Машины. Переменная hello обновления значений в hello ниже образце tooreflect вы рабочей идентификатор и ключ рабочей области OMS  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

Через несколько минут вы увидите hello новой виртуальной Машины в рабочей области OMS hello. 

![Колонка OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Дальнейшие действия
В этом руководстве вы выполнили настройку и проверку виртуальных машин с помощью центра безопасности Azure. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создать виртуальную сеть
> * Создание группы ресурсов и виртуальной машины 
> * Включить диагностику загрузки на hello виртуальной Машины
> * Просмотр диагностики загрузки
> * Просмотр метрик узла.
> * Установка расширения диагностики hello
> * Просмотр метрик виртуальной машины
> * Создание оповещения
> * Настройка расширенного мониторинга.

Переместить следующий учебник toolearn toohello относительно центра безопасности Azure.

> [!div class="nextstepaction"]
> [Мониторинг защиты виртуальных машин с помощью центра безопасности Azure](./tutorial-azure-security.md)