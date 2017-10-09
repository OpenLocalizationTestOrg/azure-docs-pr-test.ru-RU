---
title: "aaaVerify трафика с Azure сети наблюдателя IP потока проверить - Azure CLI | Документы Microsoft"
description: "В этой статье описывается как toocheck, если разрешен или запрещен, с помощью Azure CLI tooor трафик от виртуальной машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="80870-103">Проверьте, если трафик разрешен или запрещен tooor из виртуальной Машины с IP потока проверить компонент Наблюдатель сети Azure</span><span class="sxs-lookup"><span data-stu-id="80870-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="80870-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="80870-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="80870-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80870-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="80870-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="80870-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="80870-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="80870-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="80870-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="80870-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="80870-109">Поток IP проверка — это функция Наблюдатель сети, который позволяет вам tooverify, если трафик tooor из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="80870-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="80870-110">Этот сценарий является полезным tooget текущее состояние ли виртуальной машины могут взаимодействовать tooan внешнего ресурса или внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="80870-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="80870-111">Проверьте IP потока может быть tooverify используется, если правила группы безопасности сети (NSG) правильно настроены и устранение неполадок потоки, которые заблокированы правила NSG.</span><span class="sxs-lookup"><span data-stu-id="80870-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="80870-112">Кроме того, использует IP-адрес потока проверки tooensure трафика, что требуется заблокированных блокировано правильно hello NSG.</span><span class="sxs-lookup"><span data-stu-id="80870-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="80870-113">В этой статье используется нашей следующего поколения CLI для модели развертывания управления ресурса hello Azure CLI 2.0, которая доступна для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="80870-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="80870-114">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="80870-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="80870-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="80870-115">Before you begin</span></span>

<span data-ttu-id="80870-116">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети или иметь существующий экземпляр Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="80870-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="80870-117">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="80870-117">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="80870-118">Сценарий</span><span class="sxs-lookup"><span data-stu-id="80870-118">Scenario</span></span>

<span data-ttu-id="80870-119">В этом сценарии используется tooverify потока проверьте IP, если виртуальная машина может обмениваться информацией tooa известного Bing IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="80870-119">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="80870-120">Если трафик hello запрещен, он возвращает hello правило безопасности, блокирующее, трафик.</span><span class="sxs-lookup"><span data-stu-id="80870-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="80870-121">Посетите toolearn Дополнительные сведения о IP потока проверить, [Обзор потока проверьте IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="80870-121">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="80870-122">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="80870-122">Get a VM</span></span>

<span data-ttu-id="80870-123">Поток IP проверьте tooor трафика тесты из IP-адреса виртуальной машины tooor из удаленного места назначения.</span><span class="sxs-lookup"><span data-stu-id="80870-123">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="80870-124">Идентификатор виртуальной машины является обязательным для командлета hello.</span><span class="sxs-lookup"><span data-stu-id="80870-124">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="80870-125">Если вы уже знаете идентификатор hello toouse hello виртуальной машины, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="80870-125">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a><span data-ttu-id="80870-126">Получить hello сетевых Адаптеров</span><span class="sxs-lookup"><span data-stu-id="80870-126">Get hello NICS</span></span>

<span data-ttu-id="80870-127">в этом примере мы получить hello сетевых адаптеров на виртуальной машине требуется Hello IP-адрес сетевого адаптера на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="80870-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="80870-128">Если вы уже знаете hello IP адрес, о котором требуется tootest на виртуальной машине hello, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="80870-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="80870-129">Выполнение проверки IP-потока</span><span class="sxs-lookup"><span data-stu-id="80870-129">Run IP flow verify</span></span>

<span data-ttu-id="80870-130">Теперь, когда есть hello сведения, необходимые toorun hello командлета, запустим hello `az network watcher test-ip-flow` командлет tootest hello трафика.</span><span class="sxs-lookup"><span data-stu-id="80870-130">Now that we have hello information needed toorun hello cmdlet, we run hello `az network watcher test-ip-flow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="80870-131">В этом примере мы используем hello первый IP-адрес первой hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="80870-131">In this example, we are using hello first IP address on hello first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="80870-132">Поток IP проверка требует, что toorun распределения ресурсов виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="80870-132">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="80870-133">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="80870-133">Review Results</span></span>

<span data-ttu-id="80870-134">После выполнения команды `az network watcher test-ip-flow` hello результаты возвращаются, hello следующий пример является hello результаты, возвращенные hello предыдущих шага.</span><span class="sxs-lookup"><span data-stu-id="80870-134">After running `az network watcher test-ip-flow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="80870-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80870-135">Next steps</span></span>

<span data-ttu-id="80870-136">Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, определенных.</span><span class="sxs-lookup"><span data-stu-id="80870-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="80870-137">Сведения tooaudit параметры NSG получить [аудита безопасности сети группы (NSG) с Наблюдатель сети](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="80870-137">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
