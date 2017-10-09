---
title: "пиринг виртуальная сеть Azure - aaaCreate развертывания моделей - разных подписок | Документы Microsoft"
description: "Узнайте, как toocreate пиринг между виртуальными сетями виртуальная сеть создана с помощью модели развертывания Azure, существующих в разных подписках Azure."
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Создание пиринга виртуальных сетей с разными моделями развертывания в разных подписках

В этом учебнике вы узнаете, toocreate виртуальную сеть пиринга между виртуальными сетями, созданные с помощью модели развертывания. Hello виртуальные сети существуют в разных подписках. Пиринг два ресурса включает виртуальные сети в разных виртуальных сетей toocommunicate друг с другом и с hello же полосы пропускания и задержки, как будто hello ресурсы в hello одной виртуальной сети. Узнайте больше о [пиринге виртуальных сетей](virtual-network-peering-overview.md). 

Hello действия toocreate виртуальную сеть пиринга различаются, в зависимости от того, являются ли виртуальные сети hello hello в одном или разных, подписки и который [модели развертывания Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello виртуальные сети создаются через. Узнайте, как toocreate в виртуальной сети пиринг в других сценариях, щелкнув hello сценарий из hello в следующей таблице:

|Модель развертывания Azure  | Подписка Azure.  |
|--------- |---------|
|[Обе виртуальные сети Resource Manager](virtual-network-create-peering.md) |Аналогично|
|[Обе виртуальные сети Resource Manager](create-peering-different-subscriptions.md) |Разные|
|[Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть](create-peering-different-deployment-models.md) |Аналогично|

Невозможно создать виртуальную сеть пиринга между двумя виртуальными сетями, развернутые с помощью hello классической модели развертывания. Пиринг виртуальной сети могут быть созданы только между двумя виртуальными сетями, существующие в hello же регионе Azure. При создании виртуальной сети между виртуальными сетями, которые существуют в разных подписок, подписки должны быть приветствия пиринг связанной toohello же клиент Azure Active Directory. Если у вас еще нет клиента Azure Active Directory, можно быстро [создать его](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Если вам требуется tooconnect виртуальных сетей, оба созданным с помощью hello классической модели развертывания, или, существующие в разных регионах Azure, существующие в подписки связанные toodifferent клиентов Azure Active Directory, можно использовать Azure [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello виртуальных сетей. 

> [!WARNING]
> Функция создания пиринга между виртуальными сетями, созданными с помощью разных моделей развертывания Azure, которые существуют в разных подписках Azure, сейчас находится на этапе предварительной версии. Не может иметь пиринги виртуальных сетей, созданных в этом сценарии hello одинаковый уровень доступности и надежность, как создание виртуальной сети, пиринг в сценарии в целом доступности выпуска. Пиринги виртуальных сетей, создаваемые в этом сценарии, могут поддерживаться, обеспечивать все возможности или быть доступны не во всех регионах Azure. Hello последних уведомлений на доступность и состояние этой функцией, проверьте hello [виртуальной сети Azure обновляет](https://azure.microsoft.com/updates/?product=virtual-network) страницы.

Можно использовать hello [портал Azure](#portal), hello Azure [интерфейс командной строки](#cli) (CLI), или Azure [PowerShell](#powershell) toocreate пиринг виртуальной сети. Щелкните любой hello предыдущего средства ссылки toogo напрямую toohello шаги для создания виртуальной сети пиринг с помощью нравятся.

## <a name="register"></a>Зарегистрируйтесь для предварительного просмотра hello

tooregister для предварительного просмотра hello завершения hello, описанных ниже для обеих подписок, содержащих виртуальные сети hello требуется toopeer. Hello только tooregister можно использовать для предварительного просмотра hello оно PowerShell.

1. Установите последнюю версию hello hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля. Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Запустите сеанс PowerShell и войдите с помощью hello tooAzure `login-azurermaccount` команды.
3. Зарегистрируйте подписку для предварительной версии hello, введя hello, следующие команды:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    Не завершите hello hello портала, PowerShell или Azure CLI подразделах этой статьи до hello **RegistrationState** вывода появляется после ввода hello следующую команду **зарегистрированные** для обеих подписок:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>Создание пиринга с помощью портала Azure

В этом руководстве используются разные учетные записи для каждой подписки. При использовании учетной записи, имеющей разрешения tooboth подписки можно использовать hello же учетную запись для всех шагов, пропустите шаги hello для ведения журнала из портала hello и пропустите шаги hello для назначения другого пользователя разрешения toohello виртуальных сетей. Перед выполнением действий hello, выполнив действия, необходимо зарегистрировать для предварительного просмотра hello. tooregister, hello завершения шагов в hello [Зарегистрируйтесь для предварительного просмотра hello](#register) этой статьи. Не продолжайте hello, оставшиеся действия, пока обе подписки зарегистрированы для предварительного просмотра hello.
 
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
8. В hello **выберите** , пользователь б Выберите или введите toosearch адрес электронной почты пользователя UserB для него. Hello списка пользователей показано является hello того же клиента Azure Active Directory, что виртуальная сеть hello вы устанавливаете hello пиринг для. Щелкните UserB, когда он появится в списке hello.
9. Щелкните **Сохранить**.
10. Выйдите из портала hello как UserA, а затем войдите в систему как пользователь б.
11. Нажмите кнопку **+ создать**, тип *виртуальная сеть* в hello **поиска hello Marketplace** , а затем нажмите кнопку **виртуальная сеть** в результатах поиска hello .
12. В hello **виртуальной сети** колонки, отображается, выберите **классический** в hello **выберите модель развертывания** , а затем нажмите кнопку **создать**.
13.   Hello Создание виртуальной сети (классические) введите в поле, отображается hello следующие значения:

    - **Имя**: *myVnetB*.
    - **Адресное пространство**: *10.1.0.0/16*.
    - **Имя подсети**: *по умолчанию*.
    - **Диапазон адресов подсети:** *10.1.0.0/24*.
    - **Подписка**: выберите подписку B.
    - **Группа ресурсов**: установите флажок **Создать** и введите *myResourceGroupB*.
    - **Расположение**: *Восточная часть США*.

14. В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myVnetB*. Нажмите кнопку **myVnetB** когда он появится в результатах поиска hello. Стоечный модуль появится для hello **myVnetB** виртуальной сети.
15. В hello **myVnetB** колонки, отображается, нажмите кнопку **свойства** hello вертикальной списке вариантов на hello левая сторона колонка hello. Копировать hello **идентификатор РЕСУРСА**, которое используется в более позднем этапе. Идентификатор ресурса Hello — примерно toohello следующий пример: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. Выполните шаги 5–9 для myVnetB, указав **пользователя A** на шаге 8.
17. Выйдите из портала hello как пользователь б и войдите в систему как пользователь UserA.
18. В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myVnetA*. Нажмите кнопку **myVnetA** когда он появится в результатах поиска hello. Стоечный модуль появится для hello **myVnet** виртуальной сети.
19. Щелкните **myVnetA**.
20. В hello **myVnetA** колонки, отображается, нажмите кнопку **Пиринги** из hello вертикальной список параметров в hello левая сторона колонка hello.
21. В hello **myVnetA - Пиринги** колонки, которое было открыто, нажмите кнопку **+ добавить**
22. В hello **пиринг добавить** колонки, отображается, введите, или выберите hello следующие параметры, а затем нажмите кнопку **ОК**:
     - **Имя**: *myVnetAToMyVnetB*.
     - **Модель развертывания виртуальной сети**: выберите **Классический**.
     - **Я знаю идентификатор ресурса**: установите этот флажок.
     - **Идентификатор ресурса**: Введите идентификатор ресурса hello myVnetB из шаг 15.
     - **Разрешить доступ к виртуальным сетям**: убедитесь, что выбрано значение **Включено**.
    Другие параметры в этом руководстве не используются. чтение toolearn обо всех параметрах пиринга, [управления пиринги виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
23. После нажатия кнопки **ОК** hello в предыдущем шаге, hello **пиринг добавить** колонке закрывается, и вы увидите hello **myVnetA - Пиринги** колонке еще раз. Через несколько секунд hello пиринг был создан появится в колонке hello. **Подключение** перечисленные в hello **ПИРИНГ состояние** столбца для hello **myVnetAToMyVnetB** пиринг можно создать. Hello пиринг установлен. Нет необходимости toopeer hello виртуальной сети (классические) toohello виртуальная сеть не (диспетчера ресурсов).

    Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
25. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в hello [удаление ресурсов](#delete-portal) этой статьи.

## <a name="cli"></a>Создание пиринга с помощью Azure CLI

В этом руководстве используются разные учетные записи для каждой подписки. При использовании учетной записи, имеющей разрешения tooboth подписки можно использовать hello же учетной записи для всех шагов, пропустите шаги hello для ведения журнала из Azure и удаления строк hello сценария, создайте назначения ролей. Замените UserA@azure.com и UserB@azure.com во всех следующих сценариев с помощью приветствия имен пользователей, вы используете для пользователя UserA и UserB hello. 

Перед выполнением действий hello, выполнив действия, необходимо зарегистрировать для предварительного просмотра hello. tooregister, hello завершения шагов в hello [Зарегистрируйтесь для предварительного просмотра hello](#register) этой статьи. Не продолжайте hello, оставшиеся действия, пока обе подписки зарегистрированы для предварительного просмотра hello.

1. [Установка](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello виртуальной сети (классические).
2. Откройте сеанс CLI и вход tooAzure как с помощью hello UserB `azure login` команды.
3. Запустите hello CLI в режиме управления службой, введя hello `azure config mode asm` команды.
4. Введите следующую команду, toocreate hello виртуальной сети (классические) hello:
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. Привет, оставшиеся шаги необходимо выполнить с помощью команд bash с hello Azure CLI 2.0.4 или более поздней версии [установлен](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), или с помощью hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. Нажмите кнопку hello **опробовать** кнопку в hello скрипты, которые открывает оболочку облака, которое входе tooyour учетная запись Azure. Параметры, на котором установлена bash сценариев CLI на клиенте Windows, см. в разделе [работающих в Windows Azure CLI hello](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Скопируйте следующий скрипт tooa текстовый редактор на вашем ПК hello. Замените `<SubscriptionB-Id>` идентификатором своей подписки. Если вы не знаете идентификатор подписки, введите hello `az account show` команды. Здравствуйте, значение для **идентификатор** в hello выходные данные являются идентификатор вашей подписки. Скопируйте скрипт изменения hello, вставьте его в сеансе tooyour CLI 2.0 и нажмите клавишу `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    При создании виртуальной сети hello (классической) на шаге 4, Azure создан hello виртуальной сети в hello *сети по умолчанию* группы ресурсов.
7. Вход UserB за пределами Azure и войти в качестве UserA hello CLI 2.0.
8. Создайте группу ресурсов и виртуальную сеть Resource Manager. Копирования hello следующий скрипт, вставьте его в сеансе CLI tooyour и нажмите клавишу `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Создайте виртуальную сеть пиринга между hello двух виртуальных сетей создана с помощью модели развертывания hello. Скопируйте следующий скрипт tooa текстовый редактор на вашем ПК hello. Замените `<SubscriptionB-id>` идентификатором своей подписки. Если вы не знаете идентификатор подписки, введите hello `az account show` команды. Здравствуйте, значение для **идентификатор** в hello выходные данные являются идентификатор вашей подписки. Azure создан hello виртуальной сети (классические) был создан на шаге 4 в группе ресурсов с именем *сети по умолчанию*. Вставьте скрипт hello изменения в текущем сеансе CLI и нажмите клавишу `Enter`.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. После выполнения скрипта hello, просмотрите hello пиринг для hello виртуальной сети (диспетчера ресурсов). Скопируйте следующий скрипт hello и вставьте его в текущем сеансе CLI:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    Hello выходных данных указывается **подключен** в hello **PeeringState** столбца.

    Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
12. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-cli) в этой статье.

## <a name="powershell"></a>Создание пиринга с помощью PowerShell

В этом руководстве используются разные учетные записи для каждой подписки. При использовании учетной записи, имеющей разрешения tooboth подписки можно использовать hello же учетной записи для всех шагов, пропустите шаги hello для ведения журнала из Azure и удаления строк hello сценария, создайте назначения ролей. Замените UserA@azure.com и UserB@azure.com во всех следующих сценариев с помощью приветствия имен пользователей, вы используете для пользователя UserA и UserB hello. 

Перед выполнением действий hello, выполнив действия, необходимо зарегистрировать для предварительного просмотра hello. tooregister, hello завершения шагов в hello [Зарегистрируйтесь для предварительного просмотра hello](#register) этой статьи. Не продолжайте hello, оставшиеся действия, пока обе подписки зарегистрированы для предварительного просмотра hello.

1. Установите последнюю версию hello hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) и [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модулей. Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Запустите сеанс PowerShell.
3. В PowerShell, войдите в tooUserB по подписке, что пользователь б, указав hello `Add-AzureAccount` команды.
4. toocreate виртуальной сети (классической) с помощью PowerShell, необходимо создать новую или изменить существующий файл конфигурации сети. Узнайте, каким образом слишком[экспорт, обновления и импорт файлов конфигурации сети](virtual-networks-using-network-configuration-file.md). Hello файл должен содержать следующие hello **VirtualNetworkSite** элемент для hello виртуальной сети, используемые в этом учебнике:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Импорт файла конфигурации сети измененные может привести к изменения tooexisting виртуальные сети (классической) для вашей подписки. Убедитесь в добавлении hello предыдущих виртуальной сети и не изменить или удалить все существующие виртуальные сети из подписки. 

5. Войдите в подписке tooUserB как пользователь б toouse диспетчера ресурсов команды, указав hello `login-azurermaccount` команды.
6. Toovirtual назначение UserA разрешения сети б. копирование hello следующую скрипта текстовый редактор tooa на ПК и замените `<SubscriptionB-id>` с Идентификатором hello подписки б. Если вы не знаете идентификатор подписки hello, введите hello `Get-AzureRmSubscription` команда tooview его. Здравствуйте, значение для **идентификатор** в hello возвращаются выводится идентификатор вашей подписки. Azure создан hello виртуальной сети (классические) был создан на шаге 4 в группе ресурсов с именем *сети по умолчанию*. сценарий tooexecute hello, hello копирования изменить скрипт, вставьте его в tooPowerShell и нажмите клавишу `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. Выйдите из Azure в качестве пользователей UserB и войдите в подписке tooUserA UserA, введя hello `login-azurermaccount` команды. Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
8. Создайте виртуальную сеть hello (диспетчера ресурсов), скопировав hello следующий скрипт, вставив tooPowerShell, а затем нажать клавишу `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. Назначьте пользователей UserB toomyVnetA разрешения. Копировать hello следующую скрипта текстовый редактор tooa на ПК и замените `<SubscriptionA-Id>` с Идентификатором hello подписки A. Если вы не знаете идентификатор подписки hello, введите hello `Get-AzureRmSubscription` команда tooview его. Здравствуйте, значение для **идентификатор** в hello возвращаются выводится идентификатор вашей подписки. Вставьте измененную версию сценария hello hello в PowerShell и нажмите клавишу `Enter` tooexecute его.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Копировать hello следующую скрипта текстовый редактор tooa на ПК и замените `<SubscriptionB-id>` с Идентификатором hello подписки B. toopeer myVnetA toomyVNetB, скопируйте скрипт изменения hello, вставьте его в tooPowerShell и нажмите клавишу `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Просмотр состояния пиринга hello myVnetA путем копирования hello следующий сценарий, в PowerShell и нажав клавишу `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    находится в состоянии Hello **подключен**. Он изменяет слишком**подключен** после установки hello пиринга toomyVnetA из myVnetB.

    Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
13. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-powershell) в этой статье.

## <a name="permissions"></a>Разрешения

Привет, используется toocreate пиринг виртуальной сети должны иметь hello необходимые роли и разрешения. Например если две виртуальные сети с именем myVnetA и myVnetB пиринг, учетной записи должно быть назначено hello следующие минимальные роли или разрешения для каждой виртуальной сети:
    
|Виртуальная сеть|Модель развертывания|Роль|Разрешения|
|---|---|---|---|
|myVnetA|Диспетчер ресурсов|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Классический|[Участник классической сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Недоступно|
|myVnetB|Диспетчер ресурсов|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Классический|[Участник классической сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Дополнительные сведения о [встроенные роли](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) и назначение разрешений для конкретного слишком[пользовательские роли](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (только для диспетчера ресурсов).

## <a name="delete"></a>Удаление ресурсов
После завершения этого учебника вы можете toodelete hello ресурсы, созданный в учебнике hello, поэтому не приводит к дополнительным расходам. При удалении группы ресурсов также удаляются все ресурсы, которые находятся в группе ресурсов hello.

### <a name="delete-portal"></a>Портал Azure

1. Введите в поле поиска портала hello, **myResourceGroupA**. В результатах поиска hello, нажмите кнопку **myResourceGroupA**.
2. На hello **myResourceGroupA** колонка, щелкните hello **удалить** значок.
3. Удаление hello tooconfirm, в hello **ТИПА hello имя группы РЕСУРСОВ** введите **myResourceGroupA**и нажмите кнопку **удалить**.
4. В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myVnetB*. Нажмите кнопку **myVnetB** когда он появится в результатах поиска hello. Стоечный модуль появится для hello **myVnetB** виртуальной сети.
5. В hello **myVnetB** колонка, щелкните **удалить**.
6. tooconfirm hello удаления, нажмите кнопку **Да** в hello **удаления виртуальной сети** поле.

### <a name="delete-cli"></a>Интерфейс командной строки Azure

1. Вход с помощью hello tooAzure CLI 2.0 toodelete hello виртуальной сети (диспетчера ресурсов) с hello следующую команду:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Вход с помощью hello tooAzure Azure CLI 1.0 toodelete hello виртуальной сети (классические) с hello, следующие команды:

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Hello PowerShell командной строки введите следующую команду, toodelete hello виртуальной сети (диспетчера ресурсов) hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete hello виртуальной сети (классической) с помощью PowerShell, необходимо изменить существующий файл конфигурации сети. Узнайте, каким образом слишком[экспорт, обновления и импорт файлов конфигурации сети](virtual-networks-using-network-configuration-file.md). Удалите следующий элемент VirtualNetworkSite для hello виртуальной сети, используемые в этом учебнике hello:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Импорт файла конфигурации сети измененные может привести к изменения tooexisting виртуальные сети (классической) для вашей подписки. Убедитесь в удалении hello предыдущих виртуальной сети и не изменить или удалить любые другие существующие виртуальные сети из подписки. 

## <a name="next-steps"></a>Дальнейшие действия

- Внимательно ознакомьтесь с важными [ограничениями и особенностями работы пиринга виртуальных сетей](virtual-network-manage-peering.md#requirements-and-constraints), прежде чем создавать пиринг виртуальных сетей для рабочей среды.
- Узнайте о [параметрах пиринга виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
- Узнайте, каким образом слишком[создать концентратор и топология сети резервный](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) с пиринг виртуальной сети.
