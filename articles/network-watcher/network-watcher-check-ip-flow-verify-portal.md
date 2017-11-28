---
title: "Наблюдатель за сетями Azure: проверка трафика с помощью функции проверки потока IP-адресов | Документация Майкрософт"
description: "В этой статье описывается, как проверить состояние передачи входящего и исходящего трафика виртуальной машины: разрешен он или запрещен"
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
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="b6a2d-103">Проверка состояния входящего и исходящего трафика виртуальной машины (разрешен или запрещен) с помощью функции проверки потока IP-адресов службы наблюдения за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="b6a2d-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b6a2d-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b6a2d-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="b6a2d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6a2d-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="b6a2d-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="b6a2d-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="b6a2d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b6a2d-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="b6a2d-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="b6a2d-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="b6a2d-109">Проверка потока IP-адресов — это функция службы наблюдения за сетями (Наблюдатель за сетями), которая позволяет определить состояние трафика виртуальной машины: разрешен он или запрещен.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="b6a2d-110">Проверка может выполняться как для входящего, так и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="b6a2d-111">В этом сценарии можно получить сведения о текущем состоянии взаимодействия виртуальной машины с внешним ресурсом или другим ресурсом.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="b6a2d-112">С помощью проверки потока IP-адресов вы можете не только убедиться, что правила группы безопасности сети (NSG) настроены правильно, но и устранить неполадки с потоками, заблокированными этими правилами.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="b6a2d-113">Такая проверка также гарантирует, что NSG будет соответствующим образом блокировать трафик, который нужно заблокировать.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6a2d-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b6a2d-114">Before you begin</span></span>

<span data-ttu-id="b6a2d-115">В этом сценарии предполагается, что у вас уже есть Наблюдатель за сетями или что вы создали его в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="b6a2d-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="b6a2d-116">Предполагается также, что у вас имеется группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="b6a2d-117">Сценарий</span><span class="sxs-lookup"><span data-stu-id="b6a2d-117">Scenario</span></span>

<span data-ttu-id="b6a2d-118">В этом сценарии проверка потока IP-адресов помогает определить, может ли виртуальная машина обратиться к другой машине через порт 443.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="b6a2d-119">Если трафик отклоняется, возвращается правило безопасности, которое блокирует этот трафик.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="b6a2d-120">Дополнительные сведения о проверке потока IP-адресов см. в [этом обзоре](network-watcher-ip-flow-verify-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6a2d-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="b6a2d-121">Выполнение проверки потока IP-адресов</span><span class="sxs-lookup"><span data-stu-id="b6a2d-121">Run IP flow verify</span></span>

<span data-ttu-id="b6a2d-122">Откройте Наблюдатель за сетями и щелкните **Проверка IP-потока**.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="b6a2d-123">Выберите виртуальную машину и сетевой интерфейс, исходящий трафик для которых необходимо проверить.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="b6a2d-124">Введите дополнительную информацию для фильтрации и нажмите кнопку **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="b6a2d-125">После нажатия кнопки **Проверить** начнется проверка потока на основе заданных критериев.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="b6a2d-126">Результирующие значения: **Доступ разрешен** или **В доступе отказано**.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="b6a2d-127">Если доступ запрещен, вы увидите сведения о группе безопасности сети (NSG) и правиле безопасности, блокирующем трафик.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="b6a2d-128">Если запрет трафика ожидаемый, это значит, что правило выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="b6a2d-129">Для проверки потока для IP-адреса необходимо, чтобы ресурс виртуальной машины был выделен.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="b6a2d-130">На изображении ниже можно увидеть, что исходящий трафик HTTPS разрешен.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![Обзор результатов проверки потока IP-адресов][1]

<span data-ttu-id="b6a2d-132">На следующем изображении можно увидеть, что трафик был изменен на входящий, а порт — на 123.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="b6a2d-133">Теперь трафик запрещен. На экране отображается сообщение "В доступе отказано", а также указаны группа безопасности сети и правило безопасности, блокирующие трафик.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![Результаты проверки потока IP-адресов][2]

## <a name="next-steps"></a><span data-ttu-id="b6a2d-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6a2d-135">Next steps</span></span>

<span data-ttu-id="b6a2d-136">Если трафик блокируется, чего не должно быть, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md). В ней содержатся сведения об отслеживании группы безопасности сети и определенных правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="b6a2d-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













