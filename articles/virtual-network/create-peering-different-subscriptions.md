---
title: "aaaCreate Azure виртуальные сети пиринг - диспетчера ресурсов - разных подписок | Документы Microsoft"
description: "Узнайте, как toocreate пиринг между виртуальными сетями виртуальная сеть создана через диспетчер ресурсов, существуют в разных подписках Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>Создание пиринга виртуальных сетей, развернутых с помощью Resource Manager в разных подписках 

В этом учебнике вы узнаете, toocreate виртуальную сеть пиринга между виртуальных сетей, созданные с помощью диспетчера ресурсов. Hello виртуальные сети существуют в разных подписках. Пиринг два ресурса включает виртуальные сети в разных виртуальных сетей toocommunicate друг с другом и с hello же полосы пропускания и задержки, как будто hello ресурсы в hello одной виртуальной сети. Узнайте больше о [пиринге виртуальных сетей](virtual-network-peering-overview.md). 

Hello действия toocreate виртуальную сеть пиринга различаются, в зависимости от того, являются ли виртуальные сети hello hello в одном или разных, подписки и который [модели развертывания Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello виртуальные сети создаются через. Узнайте, как toocreate в виртуальной сети пиринг в других сценариях, щелкнув hello сценарий из hello в следующей таблице:

|Модель развертывания Azure  | Подписка Azure.  |
|--------- |---------|
|[Обе виртуальные сети Resource Manager](virtual-network-create-peering.md) |Аналогично|
|[Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть](create-peering-different-deployment-models.md) |Аналогично|
|[Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть](create-peering-different-deployment-models-subscriptions.md) |Разные|

Невозможно создать виртуальную сеть пиринга между двумя виртуальными сетями, развернутые с помощью hello классической модели развертывания. Пиринг виртуальной сети могут быть созданы только между двумя виртуальными сетями, существующие в hello же регионе Azure. При создании виртуальной сети между виртуальными сетями, которые существуют в разных подписок, подписки должны быть приветствия пиринг связанной toohello же клиент Azure Active Directory. Если у вас еще нет клиента Azure Active Directory, можно быстро [создать его](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Если вам требуется tooconnect виртуальных сетей, оба созданным с помощью hello классической модели развертывания, или, существующие в разных регионах Azure, существующие в подписки связанные toodifferent клиентов Azure Active Directory, можно использовать Azure [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello виртуальных сетей. 

Можно использовать hello [портал Azure](#portal), hello Azure [интерфейс командной строки](#cli) (CLI), или Azure [PowerShell](#powershell) toocreate пиринг виртуальной сети. Щелкните любой hello предыдущего средства ссылки toogo напрямую toohello шаги для создания виртуальной сети пиринг с помощью нравятся.

## <a name="portal"></a>Создание пиринга с помощью портала Azure

В этом руководстве используются разные учетные записи для каждой подписки. При использовании учетной записи, имеющей разрешения tooboth подписки можно использовать hello же учетную запись для всех шагов, пропустите шаги hello для ведения журнала из портала hello и пропустите шаги hello для назначения другого пользователя разрешения toohello виртуальных сетей.

1. Войдите в toohello [портал Azure](https://portal.azure.com) учетной записью UserA. Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
2. Щелкните **+ Создать**, выберите **Сети** и щелкните **Виртуальная сеть**.
3. В hello **Создание виртуальной сети** колонки, введите, или выбрать значения для hello следующие параметры, а затем нажмите кнопку **создать**:
    - **Имя**: *myVnetA*.
    - **Адресное пространство**: *10.0.0.0/16*.
    - **Имя подсети**: *по умолчанию*.
    - **Диапазон адресов подсети**: *10.0.0.0/24*.
    - **Подписка**: выберите подписку A.
    - **Группа ресурсов**: установите флажок **Создать** и введите *myResourceGroupA*.
    - **Расположение**: *Восточная часть США*.
4. В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myVnetA*. Нажмите кнопку **myVnetA** когда он появится в результатах поиска hello. Стоечный модуль появится для hello **myVnetA** виртуальной сети.
5. В hello **myVnetA** колонки, отображается, нажмите кнопку **(IAM) управления доступом к** из hello вертикальной список параметров в hello левая сторона колонка hello.
6. В hello **myVnetA - контроля доступа (IAM)** колонки, отображается, нажмите кнопку **+ добавить**.
7. В hello **добавить разрешения** колонки, отображается, выберите **сети участника** в hello **роли** поле.
8. В hello **выберите** , пользователь б Выберите или введите toosearch адрес электронной почты пользователя UserB для него. Hello списка пользователей показано является hello того же клиента Azure Active Directory, что виртуальная сеть hello вы устанавливаете hello пиринг для.
9. Щелкните **Сохранить**.
10. В hello **myVnetA - контроля доступа (IAM)** колонке нажмите кнопку **свойства** hello вертикальной списке вариантов на hello левая сторона колонка hello. Копировать hello **идентификатор РЕСУРСА**, которое используется в более позднем этапе. Идентификатор ресурса Hello — примерно toohello следующий пример: /subscriptions/<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA.
11. Выйдите из портала hello как UserA, а затем войдите в систему как пользователь б.
12. Выполните шаги 2 и 3, ввода или выбора hello последующих значений на шаге 3.

    - **Имя**: *myVnetB*.
    - **Адресное пространство**: *10.1.0.0/16*.
    - **Имя подсети**: *по умолчанию*.
    - **Диапазон адресов подсети:** *10.1.0.0/24*.
    - **Подписка**: выберите подписку B.
    - **Группа ресурсов**: установите флажок **Создать** и введите *myResourceGroupB*.
    - **Расположение**: *Восточная часть США*.

13. В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myVnetB*. Нажмите кнопку **myVnetB** когда он появится в результатах поиска hello. Стоечный модуль появится для hello **myVnetB** виртуальной сети.
14. В hello **myVnetB** колонки, отображается, нажмите кнопку **свойства** hello вертикальной списке вариантов на hello левая сторона колонка hello. Копировать hello **идентификатор РЕСУРСА**, которое используется в более позднем этапе. Идентификатор ресурса Hello — примерно toohello следующий пример: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB.
15. Нажмите кнопку **(IAM) управления доступом к** в hello **myVnetB** колонки и затем выполните шаги 5 – 10 для myVnetB, введя **UserA** в шаге 8.
16. Выйдите из портала hello как пользователь б и войдите в систему как пользователь UserA.
17. В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myVnetA*. Нажмите кнопку **myVnetA** когда он появится в результатах поиска hello. Стоечный модуль появится для hello **myVnet** виртуальной сети.
18. Щелкните **myVnetA**.
19. В hello **myVnetA** колонки, отображается, нажмите кнопку **Пиринги** из hello вертикальной список параметров в hello левая сторона колонка hello.
20. В hello **myVnetA - Пиринги** колонки, которое было открыто, нажмите кнопку **+ добавить**
21. В hello **пиринг добавить** колонки, отображается, введите, или выберите hello следующие параметры, а затем нажмите кнопку **ОК**:
     - **Имя**: *myVnetAToMyVnetB*.
     - **Модель развертывания виртуальной сети**: выберите **Resource Manager**.
     - **Я знаю идентификатор ресурса**: установите этот флажок.
     - **Идентификатор ресурса**: Введите идентификатор ресурса hello из шага 14.
     - **Разрешить доступ к виртуальным сетям**: убедитесь, что выбрано значение **Включено**.
    Другие параметры в этом руководстве не используются. чтение toolearn обо всех параметрах пиринга, [управления пиринги виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
22. После нажатия кнопки **ОК** hello в предыдущем шаге, hello **пиринг добавить** колонке закрывается, и вы увидите hello **myVnetA - Пиринги** колонке еще раз. Через несколько секунд hello пиринг был создан появится в колонке hello. **Инициировано** перечисленные в hello **ПИРИНГ состояние** столбца для hello **myVnetAToMyVnetB** пиринг можно создать. Одноранговыми myVnetA toomyVnetB, но теперь необходимо однорангового узла myVnetB toomyVnetA. пиринг Hello должны создаваться в обоих направлениях tooenable ресурсов в виртуальные сети toocommunicate hello друг с другом.
23. Выйдите из портала hello как UserA и войдите в систему как пользователь б.
24. Выполните шаги 17–21 для myVnetB. В шаге 21 имя hello пиринг *myVnetBToMyVnetA*выберите *myVnetA* для **виртуальная сеть**и введите идентификатор hello в шаге 10 hello **идентификатор ресурса** поле.
25. Через несколько секунд после нажатия кнопки **ОК** toocreate hello пиринг для myVnetB, hello **myVnetBToMyVnetA** отмечены только что созданный план для пиринга **подключен** в hello  **СОСТОЯНИЕ ПИРИНГА** столбца.
26. Выйдите из портала hello как пользователь б и войдите в систему как пользователь UserA.
27. Выполните шаги 17–19 еще раз. Hello **ПИРИНГ состояние** для hello **myVnetAToVNetB** пиринг теперь также является **подключен**. пиринг Hello успешно установлено, проверив **подключен** в hello **ПИРИНГ состояние** столбца для обеих виртуальных сетей в пиринге hello. Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
28. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
29. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в hello [удаление ресурсов](#delete-portal) этой статьи.

## <a name="cli"></a>Создание пиринга с помощью Azure CLI

В этом руководстве используются разные учетные записи для каждой подписки. При использовании учетной записи, имеющей разрешения tooboth подписки можно использовать hello же учетной записи для всех шагов, пропустите шаги hello для ведения журнала из Azure и удаления строк hello сценария, создайте назначения ролей. Замените UserA@azure.com и UserB@azure.com во всех следующих сценариев с помощью приветствия имен пользователей, вы используете для пользователя UserA и UserB hello.

Здравствуйте, следующий скрипт:

- Требуется hello Azure CLI версия 2.0.4 или более поздней версии. версия toofind hello, запустите `az --version`. Получить tooupgrade [установить CLI Azure 2.0](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Этот сценарий работает в оболочке Bash. Параметры запуска на клиенте Windows Azure CLI скриптов см [работающих в Windows Azure CLI hello](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Вместо установки hello CLI и его зависимости, можно использовать hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. Нажмите кнопку hello **опробовать** кнопку сценария hello, ниже, которая вызывает оболочку облака, пользователи могут входить tooyour учетная запись Azure с. 

1. Откройте сеанс CLI и вход tooAzure как с помощью hello UserA `azure login` команды. Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
2. Скопируйте следующий скрипт tooa текстовый редактор на вашем ПК hello, замените `<SubscriptionA-Id>` с hello идентификатор SubscriptionA, затем hello копирования изменить скрипт, вставьте его в сеансе CLI и нажмите клавишу `Enter`. Если вы не знаете идентификатор подписки, введите команду «Показать az учетной записи» hello. Здравствуйте, значение для **идентификатор** в hello выходные данные являются идентификатор вашей подписки.

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     Hello назначение разрешения для пользователя UserB не требуется. Пиринг может быть установлено даже, если пользователи отдельно вызвать пиринга запросы для их соответствующих виртуальных сетей, при условии, что соответствие запрашивает hello. Добавление привилегированного пользователя myVNetB как участник локальной виртуальной сети hello сети позволяет упрощена Установка toodo hello.
3. Выйдите из Azure, как с помощью hello UserA `az logout` команды, а затем войдите в tooAzure как пользователь б. Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
4. Создайте виртуальную сеть myVnetB. Скопируйте содержимое сценария hello в шаге 2 tooa текстовом редакторе на вашем ПК. Замените `<SubscriptionA-Id>` с Идентификатором SubscriptionB hello. Измените 10.0.0.0/16 too10.1.0.0/16, измените все как tooB и все tooA Bs. Скопируйте скрипт изменения hello, вставьте его в сеансе tooyour CLI и нажмите клавишу `Enter`. 
5. Выйдите из Azure в качестве пользователей UserB и войдите в tooAzure учетной записью UserA.
6. Создайте виртуальную сеть пиринга из myVnetA toomyVnetB. Скопируйте следующий скрипт содержимое tooa текстовый редактор на вашем ПК hello. Замените `<SubscriptionB-Id>` с Идентификатором SubscriptionB hello. сценарий tooexecute hello, скопируйте скрипт изменения hello, вставьте его в ваш сеанс CLI и нажмите клавишу ВВОД.
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. Выводит состояние пиринга hello myVnetA.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    находится в состоянии Hello **инициировано**. Он изменяет слишком**подключен** после создания из myVnetB пиринга toomyVnetA hello.

8. Выйдите из системы пользователя UserA из Azure и войдите в tooAzure как пользователь б.
9. Создайте пиринг hello из myVnetB toomyVnetA. Скопируйте содержимое сценария hello в шаге 6 tooa текстовом редакторе на вашем ПК. Замените `<SubscriptionB-Id>` с Идентификатором hello для SubscriptionA и измените все как tooB и все tooA Bs. После внесения изменений hello hello копирования изменяется скрипт, вставьте его в сеансе CLI и нажмите клавишу `Enter`.
10. Выводит состояние пиринга hello myVnetB. Скопируйте содержимое сценария hello в шаге 7 tooa текстовом редакторе на вашем ПК. Изменить tooB для имен виртуальной сети и группа ресурсов hello, скопируйте скрипт hello, вставьте hello изменить скрипт в сеансе CLI tooyour и нажмите клавишу `Enter`. Hello пиринга находится в состоянии **подключен**. Здравствуйте myVnetA изменения пиринга состояния слишком**подключен** после создания hello пиринг из myVnetB toomyVnetA. Вы можете войти UserA обратно tooAzure и выполнения шага 7 снова tooverify hello пиринга состояние myVnetA. 

    > [!NOTE]
    > пиринг Hello не установлено, пока не находится в состоянии пиринга hello **подключен** для обеих виртуальных сетей.

11. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
12. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-cli) в этой статье.

Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
 
## <a name="powershell"></a>Создание пиринга с помощью PowerShell

В этом руководстве используются разные учетные записи для каждой подписки. При использовании учетной записи, имеющей разрешения tooboth подписки можно использовать hello же учетной записи для всех шагов, пропустите шаги hello для ведения журнала из Azure и удаления строк hello сценария, создайте назначения ролей. Замените UserA@azure.com и UserB@azure.com во всех следующих сценариев с помощью приветствия имен пользователей, вы используете для пользователя UserA и UserB hello.

1. Установите последнюю версию hello hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля. Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Запустите сеанс PowerShell.
3. В PowerShell, войдите в систему tooAzure как UserA, введя hello `login-azurermaccount` команды. Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
4. Создание группы ресурсов и виртуальной сети A. копирования hello после текста сценария tooa редактор на вашем ПК. Замените `<SubscriptionA-Id>` с Идентификатором SubscriptionA hello. Если вы не знаете идентификатор подписки, введите hello `Get-AzureRmSubscription` команда tooview его. Здравствуйте, значение для **идентификатор** в hello возвращаются выводится идентификатор вашей подписки. сценарий tooexecute hello, hello копирования изменить скрипт, вставьте его в tooPowerShell и нажмите клавишу `Enter`.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    Hello назначение разрешения для пользователя UserB не требуется. Пиринг может быть установлено даже, если пользователи отдельно вызвать пиринга запросы для их соответствующих виртуальных сетей, при условии, что соответствие запрашивает hello. Добавление привилегированного пользователя hello другой виртуальной сети, как пользователь в локальной виртуальной сети hello делает упрощена Установка toodo hello.
5. Выйдите из Azure как пользователь A и войдите качестве пользователя B. Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
6. Скопируйте содержимое сценария hello в шаге 4 tooa текстовом редакторе на вашем ПК. Замените `<SubscriptionA-Id>` с Идентификатором hello для подписки too10.1.0.0/16 10.0.0.0/16 б. изменение. Изменить все как tooB и все tooA Bs. сценарий tooexecute hello, hello копирования изменить скрипт, вставьте в PowerShell и нажмите клавишу `Enter`.
7. Выйдите из Azure как пользователь B и войдите в качестве пользователя A.
8. Создайте пиринг hello из myVnetA toomyVnetB. Скопируйте следующий скрипт tooa текстовый редактор на вашем ПК hello. Замените `<SubscriptionB-Id>` с Идентификатором hello подписки сценарий б. tooexecute hello, скопируйте скрипт изменения hello, вставьте в tooPowerShell и нажмите клавишу `Enter`.
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. Выводит состояние пиринга hello myVnetA.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    находится в состоянии Hello **инициировано**. Он изменяет слишком**подключен** после установки hello пиринга toomyVnetA из myVnetB.

10. Выйдите из Azure как пользователь A и войдите качестве пользователя B.
11. Создайте пиринг hello из myVnetB toomyVnetA. Скопируйте содержимое сценария hello в шаге 8 tooa текстовом редакторе на вашем ПК. Замените `<SubscriptionB-Id>` с Идентификатором hello подписки A и изменение A tooB и B все tooA. сценарий tooexecute hello, hello копирования изменить скрипт, вставьте его в tooPowerShell и нажмите клавишу `Enter`.
12. Выводит состояние пиринга hello myVnetB. Скопируйте содержимое сценария hello в шаге 9 tooa текстовом редакторе на вашем ПК. Измените tooB для группы ресурсов hello и имен виртуальной сети. сценарий tooexecute hello, вставьте hello изменить сценарий в PowerShell и нажмите клавишу `Enter`. находится в состоянии Hello **подключен**. Здравствуйте, пиринга состояние **myVnetA** изменяет слишком**подключен** после создания hello пиринг из **myVnetB** слишком**myVnetA**. Вы можете войти UserA обратно tooAzure и завершении шага 9 снова tooverify hello пиринга состояние myVnetA. 

    > [!NOTE]
    > пиринг Hello не установлено, пока не находится в состоянии пиринга hello **подключен** для обеих виртуальных сетей.

    Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

13. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
14. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-powershell) в этой статье.

## <a name="permissions"></a>Разрешения

Привет, используется toocreate пиринг виртуальной сети должны иметь hello необходимые роли и разрешения. Например, если пиринг две виртуальные сети с именем **myVnetA** и **myVnetB**, учетной записи необходимо назначить hello следующие минимальные роли или разрешения для каждой виртуальной сети:
    
|Виртуальная сеть|Роль|Разрешения|
|---|---|---|
|myVnetA|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Дополнительные сведения о [встроенные роли](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) и назначение разрешений для конкретного слишком[пользовательские роли](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (только для диспетчера ресурсов).

## <a name="delete"></a>Удаление ресурсов
После завершения этого учебника вы можете toodelete hello ресурсы, созданный в учебнике hello, поэтому не приводит к дополнительным расходам. При удалении группы ресурсов также удаляются все ресурсы, которые находятся в группе ресурсов hello.

### <a name="delete-portal"></a>Портал Azure

1. Войдите в систему toohello портал Azure как UserA.
2. Введите в поле поиска портала hello, **myResourceGroupA**. В результатах поиска hello, нажмите кнопку **myResourceGroupA**.
3. На hello **myResourceGroupA** колонка, щелкните hello **удалить** значок.
4. Удаление hello tooconfirm, в hello **ТИПА hello имя группы РЕСУРСОВ** введите **myResourceGroupA**и нажмите кнопку **удалить**.
5. Выйдите из портала hello как UserA и войдите в систему как пользователь б.
6. Выполните шаги 2–4 для группы ресурсов myResourceGroupB.

### <a name="delete-cli"></a>Интерфейс командной строки Azure

1. Вход tooAzure как UserA и выполните следующую команду hello:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. Выйдите из Azure как пользователь A, а затем войдите как пользователь B.
3. Выполните следующую команду hello:

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>PowerShell

1. Вход tooAzure как UserA и выполните следующую команду hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. Выйдите из Azure как пользователь A, а затем войдите как пользователь B.
3. Выполните следующую команду hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>Дальнейшие действия

- Внимательно ознакомьтесь с важными [ограничениями и особенностями работы пиринга виртуальных сетей](virtual-network-manage-peering.md#requirements-and-constraints), прежде чем создавать пиринг виртуальных сетей для рабочей среды.
- Узнайте о [параметрах пиринга виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
- Узнайте, каким образом слишком[создать концентратор и топология сети резервный](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) с пиринг виртуальной сети.
