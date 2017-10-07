---
title: "aaaMonitor виртуальных машин Linux в Azure | Документы Microsoft"
description: "Узнайте, как toomonitor загружается диагностики и метрики производительности на виртуальной машине Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>Как toomonitor виртуальной машины Linux в Azure

tooensure виртуальных машин (ВМ) в Azure работают правильно, можно просмотреть Диагностика загрузки и метрики производительности. Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Включить диагностику загрузки на hello виртуальной Машины
> * Просмотр диагностики загрузки
> * Просмотр метрик узла.
> * Включить расширение диагностики в hello виртуальной Машины
> * Просмотр метрик виртуальной машины
> * Создание оповещений на основе метрик диагностики.
> * Настройка расширенного мониторинга.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-vm"></a>Создание виртуальной машины

Диагностика toosee и метрики в действии, необходимо виртуальной Машины. Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroupMonitor* в hello *eastus* расположение.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

Теперь создайте виртуальную машину командой [az vm create](https://docs.microsoft.com/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>Включение диагностики загрузки

При загрузке виртуальных машин Linux, hello загрузки диагностического расширения записывает выходные данные для загрузки и сохраняет его в хранилище Azure. Эти данные могут быть ошибки при загрузке используется tootroubleshoot виртуальной Машины. Диагностика загрузки не включается автоматически при создании ВМ Linux с помощью hello Azure CLI.

Перед включением Диагностика загрузки, учетную запись хранения должна toobe, созданные для хранения журналов загрузки. Имена учетных записей хранения должны быть глобально уникальными, иметь длину от 3 до 24 символов и содержать только цифры и буквы в нижнем регистре. Создать учетную запись хранилища с hello [создания учетной записи хранилища az](/cli/azure/storage/account#create) команды. В этом примере строка случайных — используется toocreate имя учетной записи хранилища с уникальным. 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

При включении Диагностика загрузки, необходим контейнер хранилища больших двоичных объектов toohello URI hello. Hello следующие запросы hello tooreturn учетной записи хранения этот URI. значение URI Hello хранится в именах переменных *bloburi*, которое используется в следующем шаге hello.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

Включите диагностику загрузки с помощью команды [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable). Hello `--storage` значение — hello больших двоичных объектов, собранные URI в предыдущем шаге hello.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>Просмотр диагностики загрузки

Если Диагностика загрузки включены, каждый раз, останавливать и запускать hello виртуальной Машины, сведения о процессе загрузки hello записывается tooa файла журнала. В этом примере сначала освободить hello виртуальной Машины с hello [ВМ az deallocate](/cli/azure/vm#deallocate) следующим образом:

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

Теперь запустите hello виртуальной Машины с hello [запуска виртуальной машины az]( /cli/azure/vm#stop) следующим образом:

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

Можно получить диагностические данные hello загрузки для *myVM* с hello [az ВМ Диагностика загрузки get загрузки журнал-](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) следующим образом:

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>Просмотр метрик узла.

Виртуальная машина Linux имеет выделенный узел в Azure, с которым она взаимодействует. Метрики автоматически собираются для узла hello и могут быть просмотрены в hello портал Azure следующим образом:

1. В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroupMonitor**и выберите **myVM** в список ресурсов hello.
1. toosee о выполнении hello узла виртуальной Машины, щелкните **метрики** hello колонке виртуальной Машины, затем выберите любой из hello *[узел]* метрики в списке **доступные метрики**.

    ![Просмотр метрик узла.](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>Установка расширения диагностики

> [!IMPORTANT]
> В этом документе описываются версии 2.3 hello диагностического расширения Linux, которое рекомендуется к использованию. Версия 2.3 будет поддерживаться до 30 июня 2018 г.
>
> Вместо этого можно включить версии 3.0 hello диагностического расширения для Linux. Дополнительные сведения см. в разделе [hello документации](./diagnostic-extension.md).

Hello узла основные метрики доступны, но toosee более детального и метрики конкретной виртуальной Машины, вы tooneed tooinstall hello Azure расширение диагностики в hello виртуальной Машины. Hello расширения службы диагностики Azure позволяет дополнительные функции мониторинга и диагностики toobe данные, полученные из hello виртуальной Машины. Можно просматривать эти метрики производительности и создание предупреждений в зависимости от того, как выполняется hello виртуальной Машины. Hello диагностического расширения устанавливаются с помощью портала Azure hello следующим образом:

1. В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.
1. Щелкните **Параметры диагностики**. Показывает, что список Hello *загрузки диагностики* уже включены в предыдущем разделе hello. Установите флажок hello для *базовые показатели*.
1. В hello *учетной записи хранилища* перейдите выберите hello tooand *mydiagdata [1234]* учетную запись, созданную в предыдущем разделе hello.
1. Нажмите кнопку hello **Сохранить** кнопки.

    ![Просмотр метрик диагностики](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>Просмотр метрик виртуальной машины

Можно просмотреть метрики виртуальной Машины hello в hello просмотрены показателей виртуальной Машины узла hello следующим образом:

1. В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.
1. toosee о выполнении hello виртуальной Машины, щелкните **метрики** на hello колонки виртуальной Машины, а затем выберите любой из метрик hello диагностики в разделе **доступные метрики**.

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

При наличии портал OMS toohello доступа hello идентификатор рабочей области ключ и рабочей области можно найти в колонке параметров hello. Замените < ключ рабочей области > и < идентификатор рабочей области > со значениями hello для из вашего OMS можно использовать рабочую область, а затем **набор расширения ВМ az** tooadd hello OMS расширения toohello виртуальной Машины:

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

В колонке поиска журналов hello hello портала OMS, вы увидите *myVM* как элементы, отображаемые в следующий рисунок hello:

![Колонка OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы выполнили настройку и проверку виртуальных машин с помощью центра безопасности Azure. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Включить диагностику загрузки на hello виртуальной Машины
> * Просмотр диагностики загрузки
> * Просмотр метрик узла.
> * Включить расширение диагностики в hello виртуальной Машины
> * Просмотр метрик виртуальной машины
> * Создание оповещений на основе метрик диагностики.
> * Настройка расширенного мониторинга.

Переместить следующий учебник toolearn toohello относительно центра безопасности Azure.

> [!div class="nextstepaction"]
> [Мониторинг защиты виртуальных машин с помощью центра безопасности Azure](./tutorial-azure-security.md)