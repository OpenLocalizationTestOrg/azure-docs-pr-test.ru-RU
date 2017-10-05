---
title: "Масштабирование облачной службы Azure в Windows PowerShell | Документация Майкрософт"
description: "(Классическая модель.) Узнайте, как использовать PowerShell для масштабирования веб-роли или рабочей роли в Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="499d4-103">Как масштабировать облачную службу в PowerShell</span><span class="sxs-lookup"><span data-stu-id="499d4-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="499d4-104">Масштабировать веб-роль или рабочую роль с помощью Windows PowerShell можно, добавляя или удаляя экземпляры.</span><span class="sxs-lookup"><span data-stu-id="499d4-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="499d4-105">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="499d4-105">Log in to Azure</span></span>

<span data-ttu-id="499d4-106">Прежде чем выполнять какие-либо операции с подпиской с помощью PowerShell, вы должны войти в систему.</span><span class="sxs-lookup"><span data-stu-id="499d4-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="499d4-107">Если с вашей учетной записью связано несколько подписок, может потребоваться сменить текущую подписку. Это зависит от того, где находится ваша облачная служба.</span><span class="sxs-lookup"><span data-stu-id="499d4-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="499d4-108">Чтобы проверить, какая подписка используется в данный момент, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="499d4-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="499d4-109">Если необходимо сменить текущую подписку, выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="499d4-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="499d4-110">Проверка текущего количества экземпляров для роли</span><span class="sxs-lookup"><span data-stu-id="499d4-110">Check the current instance count for your role</span></span>

<span data-ttu-id="499d4-111">Чтобы проверить текущее состояние роли, выполните приведенную команду.</span><span class="sxs-lookup"><span data-stu-id="499d4-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="499d4-112">Должна отобразиться информация о роли, включая версию ее текущей операционной системы и число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="499d4-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="499d4-113">В этом случае у роли имеется один экземпляр.</span><span class="sxs-lookup"><span data-stu-id="499d4-113">In this case, the role has a single instance.</span></span>

![Информация о роли](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="499d4-115">Развертывание роли путем добавления дополнительных экземпляров</span><span class="sxs-lookup"><span data-stu-id="499d4-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="499d4-116">Чтобы развернуть роль, передайте нужное число экземпляров как параметр **Count** командлета **Set-AzureRole**.</span><span class="sxs-lookup"><span data-stu-id="499d4-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="499d4-117">Командлет мгновенно блокируется, пока готовятся и запускаются новые экземпляры.</span><span class="sxs-lookup"><span data-stu-id="499d4-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="499d4-118">Если в это время открыть новое окно PowerShell и вызвать **Get-AzureRole**, как показано выше, то вы увидите новое целевое число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="499d4-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="499d4-119">И если просмотреть состояние роли на портале, то вы увидите, что запускается новый экземпляр.</span><span class="sxs-lookup"><span data-stu-id="499d4-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![Запуск экземпляра виртуальной машины на портале](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="499d4-121">После запуска новых экземпляров командлет отобразит сообщение об успешном выполнении.</span><span class="sxs-lookup"><span data-stu-id="499d4-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![Успешное увеличение числа экземпляров роли](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="499d4-123">Свертывание роли путем удаления экземпляров</span><span class="sxs-lookup"><span data-stu-id="499d4-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="499d4-124">Точно так же можно свернуть роль, удаляя экземпляры.</span><span class="sxs-lookup"><span data-stu-id="499d4-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="499d4-125">Задайте для параметра **Count** командлета **Set-AzureRole** число экземпляров, которые должны остаться после операции свертывания.</span><span class="sxs-lookup"><span data-stu-id="499d4-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="499d4-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="499d4-126">Next steps</span></span>

<span data-ttu-id="499d4-127">Настроить автомасштабирование для облачных служб из PowerShell невозможно.</span><span class="sxs-lookup"><span data-stu-id="499d4-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="499d4-128">Об этом можно узнать в разделе [Автомасштабирование облачной службы](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="499d4-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
