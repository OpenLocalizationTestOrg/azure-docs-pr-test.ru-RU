---
title: "Проверьте aaaVerify трафика с потоком IP Наблюдатель сети Azure - портал Azure | Документы Microsoft"
description: "В этой статье описывается как toocheck, если разрешен или запрещен трафик tooor из виртуальной машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="d3e9e-103">Проверьте, если трафик разрешен или запрещен tooor из виртуальной Машины с IP потока проверить компонент Наблюдатель сети Azure</span><span class="sxs-lookup"><span data-stu-id="d3e9e-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d3e9e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d3e9e-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="d3e9e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3e9e-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="d3e9e-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="d3e9e-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="d3e9e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3e9e-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="d3e9e-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="d3e9e-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="d3e9e-109">Проверьте IP потока — это функция Наблюдатель сети, который позволяет вам tooverify, если трафик tooor из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="d3e9e-110">Hello проверку можно провести для входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="d3e9e-111">Этот сценарий является полезным tooget текущее состояние ли виртуальная машина может обмениваться информацией tooan внешний ресурс или другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="d3e9e-112">Проверьте IP потока может быть tooverify используется, если правила группы безопасности сети (NSG) правильно настроены и устранение неполадок потоки, которые заблокированы правила NSG.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="d3e9e-113">Кроме того, использует IP-адрес потока проверки tooensure трафика, что требуется заблокированных блокировано правильно hello NSG.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d3e9e-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d3e9e-114">Before you begin</span></span>

<span data-ttu-id="d3e9e-115">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети или иметь существующий экземпляр Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="d3e9e-116">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="d3e9e-117">Сценарий</span><span class="sxs-lookup"><span data-stu-id="d3e9e-117">Scenario</span></span>

<span data-ttu-id="d3e9e-118">В этом сценарии используется tooverify потока проверьте IP, если виртуальная машина может обмениваться информацией машины tooanother через порт 443.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="d3e9e-119">Если трафик hello запрещен, он возвращает hello правило безопасности, блокирующее, трафик.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="d3e9e-120">Посетите toolearn Дополнительные сведения о IP потока проверить, [Обзор потока проверьте IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d3e9e-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="d3e9e-121">Выполнение проверки IP-потока</span><span class="sxs-lookup"><span data-stu-id="d3e9e-121">Run IP flow verify</span></span>

<span data-ttu-id="d3e9e-122">Найдите tooyour Наблюдатель сети и нажмите кнопку **проверить поток IP**.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="d3e9e-123">Выберите виртуальную машину hello и сетевой интерфейс нужные tooverify трафик от.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="d3e9e-124">Введите дополнительную информацию для фильтрации и нажмите кнопку **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="d3e9e-125">После нажатия кнопки **проверьте**, проверяется на основе указанных критериев hello потока hello.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="d3e9e-126">Hello результатом является либо **разрешенного доступа** или **отказано в доступе**.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="d3e9e-127">Если доступ запрещен, hello группы безопасности сети (NSG) и правила безопасности, блокирующих трафик предоставляется.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="d3e9e-128">Если отказ hello трафика результат является ожидаемым, hello правила выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="d3e9e-129">Проверьте потока IP требует, что выделена hello ресурса виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="d3e9e-130">Как видно из hello после изображения, была разрешена hello исходящего трафика HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![Обзор результатов проверки потока IP-адресов][1]

<span data-ttu-id="d3e9e-132">По результатам hello после изображения, изменяется трафика tooinbound и hello входящих too123 изменить порт.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="d3e9e-133">Теперь запрещен трафик, приветственное сообщение «Доступ запрещен» предоставляется вместе с hello правило сетевой безопасности группы и безопасности, запрещать трафик hello.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![Результаты проверки потока IP-адресов][2]

## <a name="next-steps"></a><span data-ttu-id="d3e9e-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3e9e-135">Next steps</span></span>

<span data-ttu-id="d3e9e-136">Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, определенных.</span><span class="sxs-lookup"><span data-stu-id="d3e9e-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













