---
title: "aaaScale облачной службы Azure в Windows PowerShell | Документы Microsoft"
description: "(классические) Узнайте, как toouse PowerShell tooscale веб-роли или рабочей роли или уменьшить в Azure."
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
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="5dd7a-103">Как tooscale облачной службы в PowerShell</span><span class="sxs-lookup"><span data-stu-id="5dd7a-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="5dd7a-104">Можно использовать Windows PowerShell tooscale веб-роли или рабочей роли in или out, добавив или удалив экземпляры.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="5dd7a-105">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="5dd7a-105">Log in tooAzure</span></span>

<span data-ttu-id="5dd7a-106">Прежде чем выполнять какие-либо операции с подпиской с помощью PowerShell, вы должны войти в систему.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="5dd7a-107">Если у вас несколько подписок, связанных с учетной записью, может потребоваться toochange hello текущей подписки в зависимости от того, где находится облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="5dd7a-108">toocheck hello текущей подписке запуска:</span><span class="sxs-lookup"><span data-stu-id="5dd7a-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="5dd7a-109">Если вам требуется toochange hello текущую подписку, выполните:</span><span class="sxs-lookup"><span data-stu-id="5dd7a-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="5dd7a-110">Проверьте hello текущее количество экземпляров для роли</span><span class="sxs-lookup"><span data-stu-id="5dd7a-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="5dd7a-111">Выполните toocheck hello вашей роли в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="5dd7a-112">Следует вернуть сведения о роли hello, включая его текущей операционной системы версии и число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="5dd7a-113">В этом случае имеется один экземпляр роли hello.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-113">In this case, hello role has a single instance.</span></span>

![Сведения о роли hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="5dd7a-115">Расширение роли hello, добавив дополнительные экземпляры</span><span class="sxs-lookup"><span data-stu-id="5dd7a-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="5dd7a-116">tooscale какая-то роль hello проход требуемого числа экземпляров как hello **число** toohello параметр **AzureRole набор** командлета:</span><span class="sxs-lookup"><span data-stu-id="5dd7a-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="5dd7a-117">блоки командлет Hello моментально при новые экземпляры hello подготавливаются и запущен.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="5dd7a-118">В течение этого времени, при открытии нового окна PowerShell и вызовите **Get-AzureRole** как показано выше, вы увидите hello. количество новых целевой экземпляр.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="5dd7a-119">И если проверить состояние роли hello hello портала вы увидите новый экземпляр hello запуска:</span><span class="sxs-lookup"><span data-stu-id="5dd7a-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![Запуск экземпляра виртуальной машины на портале](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="5dd7a-121">После запуска экземпляров новый hello hello командлет возвращает успешно:</span><span class="sxs-lookup"><span data-stu-id="5dd7a-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![Успешное увеличение числа экземпляров роли](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="5dd7a-123">Масштабировать, удалив экземпляры роли hello</span><span class="sxs-lookup"><span data-stu-id="5dd7a-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="5dd7a-124">Можно масштабировать в роли путем удаления экземпляров hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="5dd7a-125">Набор hello **число** параметр на **AzureRole набор** toohello число экземпляров требуется toohave после масштабирования hello в операции.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dd7a-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5dd7a-126">Next steps</span></span>

<span data-ttu-id="5dd7a-127">Не является автоматически масштабировать возможных tooconfigure для облачных служб из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dd7a-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="5dd7a-128">toodo, в разделе [облачную службу, как масштабировать tooauto](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5dd7a-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
