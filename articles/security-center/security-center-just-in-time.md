---
title: "доступ к aaaJust время виртуальной машине в центр безопасности Azure | Документы Microsoft"
description: "В этом документе описывается как на момент времени доступа к ВМ в центр безопасности Azure позволяет управлять доступ к tooyour Azure виртуальные машины."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="65b30-103">Управление доступом к виртуальным машинам с помощью JIT</span><span class="sxs-lookup"><span data-stu-id="65b30-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="65b30-104">На время виртуальной машины (VM) доступ может быть используется toolock вниз tooyour входящего трафика виртуальных машин Azure, уменьшить уязвимость tooattacks то же время предоставляя tooVMs tooconnect удобно, если это требуется.</span><span class="sxs-lookup"><span data-stu-id="65b30-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="65b30-105">Hello только в функции времени находится в предварительной версии и доступна на hello стандартный уровень центра обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="65b30-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="65b30-106">В разделе [цены](security-center-pricing.md) toolearn Дополнительные сведения о центре безопасности ценовым категориям.</span><span class="sxs-lookup"><span data-stu-id="65b30-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="65b30-107">Сценарий атаки</span><span class="sxs-lookup"><span data-stu-id="65b30-107">Attack scenario</span></span>

<span data-ttu-id="65b30-108">Подбора часто атаки целевых портов управления как tooa доступа toogain означает виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="65b30-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="65b30-109">В случае успешного выполнения злоумышленник можно установить контроль над hello ВМ и установить злоумышленника в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="65b30-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="65b30-110">Одним из способов tooreduce раскрытия tooa методом подбора — toolimit hello время, порт открыт.</span><span class="sxs-lookup"><span data-stu-id="65b30-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="65b30-111">Порты для управления не требуется открыть toobe сделать в любое время.</span><span class="sxs-lookup"><span data-stu-id="65b30-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="65b30-112">Им требуется toobe открытым во время являются toohello подключенных виртуальных Машин, например tooperform управления или служебных задач.</span><span class="sxs-lookup"><span data-stu-id="65b30-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="65b30-113">При включенной на момент времени, центр обеспечения безопасности используются [сетевой группы безопасности](../virtual-network/virtual-networks-nsg.md) (NSG) правила, которые ограничивают toomanagement порты доступа, поэтому они не может быть объектом атак злоумышленников.</span><span class="sxs-lookup"><span data-stu-id="65b30-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Сценарий JIT][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="65b30-115">Как работает доступ JIT?</span><span class="sxs-lookup"><span data-stu-id="65b30-115">How does just in time access work?</span></span>

<span data-ttu-id="65b30-116">При включении на момент времени, центр обеспечения безопасности блокирует tooyour входящий трафик виртуальных машин Azure путем создания правила NSG.</span><span class="sxs-lookup"><span data-stu-id="65b30-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="65b30-117">Выберите порты hello на toowhich ВМ hello входящий трафик блокируется вниз.</span><span class="sxs-lookup"><span data-stu-id="65b30-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="65b30-118">Эти порты определяются hello только в решении, время.</span><span class="sxs-lookup"><span data-stu-id="65b30-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="65b30-119">Когда пользователь запрашивает доступ tooa виртуальной Машины, центр обеспечения безопасности проверяет этот пользователь hello [управление доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md) разрешения, которые предоставляют доступ на запись для hello ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="65b30-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="65b30-120">Если они имеют разрешения на запись, hello запрос утверждается и центр обеспечения безопасности автоматически настраивает hello группы безопасности сети (Nsg) tooallow входящие порты управления toohello трафика для hello объем указанное время.</span><span class="sxs-lookup"><span data-stu-id="65b30-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="65b30-121">По прошествии времени hello центра обеспечения безопасности восстанавливает hello Nsg tootheir предыдущих состояний.</span><span class="sxs-lookup"><span data-stu-id="65b30-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="65b30-122">JIT-доступ с использованием центра безопасности сейчас поддерживается только для виртуальных машин, развернутых с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65b30-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="65b30-123">см. Дополнительные сведения о классическом hello и модели развертывания диспетчера ресурсов toolearn [диспетчера ресурсов Azure и классическое развертывание](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="65b30-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="65b30-124">Использование JIT-доступа</span><span class="sxs-lookup"><span data-stu-id="65b30-124">Using just in time access</span></span>

<span data-ttu-id="65b30-125">Hello **непосредственно в ВМ доступа на время** плитки приветствия **центра обеспечения безопасности** колонке номер hello виртуальными машинами, настроенными для вовремя, время доступа и hello число утвержденных доступа запросов в hello прошлой неделе.</span><span class="sxs-lookup"><span data-stu-id="65b30-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="65b30-126">Выберите hello **непосредственно в ВМ доступа на время** плитки и hello **непосредственно в ВМ доступа на время** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="65b30-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Элемент "JIT-доступ к виртуальной машине"][2]

<span data-ttu-id="65b30-128">Hello **непосредственно в ВМ доступа на время** колонке предоставляет сведения о состоянии hello виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="65b30-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="65b30-129">**Настроить** -виртуальных машин, которые были настроенных toosupport на время доступа к ВМ.</span><span class="sxs-lookup"><span data-stu-id="65b30-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="65b30-130">Hello данные, представленные для hello прошлой недели и включает для каждой виртуальной Машины hello число утвержденных запросов дату последнего доступа и и времени последнего пользователя.</span><span class="sxs-lookup"><span data-stu-id="65b30-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="65b30-131">**Рекомендуемые** — виртуальные машины, которые поддерживают JIT-доступ, но для которых он не настроен.</span><span class="sxs-lookup"><span data-stu-id="65b30-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="65b30-132">Рекомендуется включить JIT-доступ для этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="65b30-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="65b30-133">См. раздел [Включение JIT-доступа к виртуальной машине](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="65b30-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="65b30-134">**Рекомендации отсутствуют** -причины, которые могут привести к виртуальной Машине не toobe рекомендуется:</span><span class="sxs-lookup"><span data-stu-id="65b30-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="65b30-135">Отсутствует NSG - hello только в решении, время требуются toobe NSG на месте.</span><span class="sxs-lookup"><span data-stu-id="65b30-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="65b30-136">Классическая виртуальная машина — JIT-доступ с использованием центра безопасности сейчас поддерживается только для виртуальных машин, развернутых с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65b30-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="65b30-137">Классическое развертывание hello только в решении, время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="65b30-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="65b30-138">Другой - виртуальной Машины — в этой категории, если hello своевременно решения отключена в политике безопасности hello hello подписки или группа ресурсов hello или этой виртуальной Машины hello отсутствует общедоступный IP-адрес и не имеет NSG на месте.</span><span class="sxs-lookup"><span data-stu-id="65b30-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="65b30-139">Настройка политики JIT-доступа</span><span class="sxs-lookup"><span data-stu-id="65b30-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="65b30-140">hello tooselect виртуальных машин, которые должны tooenable:</span><span class="sxs-lookup"><span data-stu-id="65b30-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="65b30-141">На hello **непосредственно в ВМ доступа на время** колонки, выберите hello **рекомендуется** вкладки.</span><span class="sxs-lookup"><span data-stu-id="65b30-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Включение JIT-доступа][3]

2. <span data-ttu-id="65b30-143">В разделе **виртуальные машины**, выберите hello виртуальных машин, которые должны tooenable.</span><span class="sxs-lookup"><span data-stu-id="65b30-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="65b30-144">Этот запрос помещает флажок Далее tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="65b30-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="65b30-145">Выберите **Включить JIT-доступ для виртуальных машин**.</span><span class="sxs-lookup"><span data-stu-id="65b30-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="65b30-146">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="65b30-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="65b30-147">Номера портов по умолчанию</span><span class="sxs-lookup"><span data-stu-id="65b30-147">Default ports</span></span>

<span data-ttu-id="65b30-148">Вы увидите порты по умолчанию hello, центр обеспечения безопасности рекомендует включить на момент времени.</span><span class="sxs-lookup"><span data-stu-id="65b30-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="65b30-149">На hello **непосредственно в ВМ доступа на время** колонки, выберите hello **рекомендуется** вкладки.</span><span class="sxs-lookup"><span data-stu-id="65b30-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Отображение номеров портов по умолчанию][6]

2. <span data-ttu-id="65b30-151">В разделе **Виртуальные машины** выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="65b30-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="65b30-152">Этот запрос помещает флажок Далее toohello ВМ и открывает hello **конфигурации доступа JIT-компилятора виртуальной Машины** колонку.</span><span class="sxs-lookup"><span data-stu-id="65b30-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="65b30-153">Эта колонка отображает порты по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="65b30-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="65b30-154">Добавление портов</span><span class="sxs-lookup"><span data-stu-id="65b30-154">Add ports</span></span>

<span data-ttu-id="65b30-155">Из hello **конфигурации доступа JIT-компилятора виртуальной Машины** колонки, можно также добавить и настроить новый порт, на котором будет hello tooenable только в решении, время.</span><span class="sxs-lookup"><span data-stu-id="65b30-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="65b30-156">На hello **конфигурации доступа JIT-компилятора виртуальной Машины** колонке выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="65b30-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="65b30-157">При этом откроется hello **Конфигурация порта добавить** колонку.</span><span class="sxs-lookup"><span data-stu-id="65b30-157">This opens hello **Add port configuration** blade.</span></span>

  ![Конфигурация порта][7]

2. <span data-ttu-id="65b30-159">На **Конфигурация порта добавить** колонки, необходимо указать порт hello, тип протокола, открывают IP-адресов источника и максимальное время запроса.</span><span class="sxs-lookup"><span data-stu-id="65b30-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="65b30-160">Допускается IP-адресов источника — hello IP-диапазонов разрешенных tooget доступу после утверждения запроса.</span><span class="sxs-lookup"><span data-stu-id="65b30-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="65b30-161">Максимальное время запроса — окно hello максимальное время, что можно открыть конкретный порт.</span><span class="sxs-lookup"><span data-stu-id="65b30-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="65b30-162">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="65b30-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="65b30-163">Запрашивает доступ tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="65b30-163">Requesting access tooa VM</span></span>

<span data-ttu-id="65b30-164">tooa доступа toorequest виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="65b30-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="65b30-165">На hello **непосредственно в ВМ доступа на время** колонки, выберите hello **настроенный** вкладки.</span><span class="sxs-lookup"><span data-stu-id="65b30-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="65b30-166">В разделе **виртуальные машины**, выберите hello виртуальных машин, что вы хотите получить доступ tooenable.</span><span class="sxs-lookup"><span data-stu-id="65b30-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="65b30-167">Этот запрос помещает флажок Далее tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="65b30-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="65b30-168">Выберите **Запросить доступ**.</span><span class="sxs-lookup"><span data-stu-id="65b30-168">Select **Request access**.</span></span> <span data-ttu-id="65b30-169">При этом откроется hello **запроса доступа** колонку.</span><span class="sxs-lookup"><span data-stu-id="65b30-169">This opens hello **Request access** blade.</span></span>

  ![Запрос доступа tooa виртуальной Машины][4]

4. <span data-ttu-id="65b30-171">На hello **запроса доступа** колонки, можно настроить tooopen порты hello каждой виртуальной Машины, вместе с hello исходный IP-адрес, порт hello открыто окно времени hello tooand, для которых Привет открыть порт.</span><span class="sxs-lookup"><span data-stu-id="65b30-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="65b30-172">Вы можете запросить доступ только toohello портам, настроенным в hello только в политике времени.</span><span class="sxs-lookup"><span data-stu-id="65b30-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="65b30-173">У каждого порта имеется максимально допустимое время, производным от hello только в политике времени.</span><span class="sxs-lookup"><span data-stu-id="65b30-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="65b30-174">Выберите **Открыть порты**.</span><span class="sxs-lookup"><span data-stu-id="65b30-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="65b30-175">Изменение политики JIT-доступа</span><span class="sxs-lookup"><span data-stu-id="65b30-175">Editing a just in time access policy</span></span>

<span data-ttu-id="65b30-176">Можно изменить существующие Виртуальной машины только в политике времени путем добавления и настройки нового tooopen порта для виртуальных Машин или путем изменения любого другого параметра, связанные tooan уже защищен порта.</span><span class="sxs-lookup"><span data-stu-id="65b30-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="65b30-177">Чтобы tooedit существующий только в политике время виртуальной машины, hello **настроенный** вкладка используется:</span><span class="sxs-lookup"><span data-stu-id="65b30-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="65b30-178">В разделе **виртуальные машины**, выберите tooadd ВМ tooby порт, щелкнув hello трех точек в строке приветствия для этой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="65b30-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="65b30-179">Откроется меню.</span><span class="sxs-lookup"><span data-stu-id="65b30-179">This opens a menu.</span></span>
2. <span data-ttu-id="65b30-180">Выберите **изменить** в меню hello.</span><span class="sxs-lookup"><span data-stu-id="65b30-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="65b30-181">При этом откроется hello **конфигурации доступа JIT-компилятора виртуальной Машины** колонку.</span><span class="sxs-lookup"><span data-stu-id="65b30-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![Изменение политики][8]

3. <span data-ttu-id="65b30-183">На hello **конфигурации доступа JIT-компилятора виртуальной Машины** колонке hello существующие параметры уже защищенном порта можно изменить, щелкнув его порт, или можно выбрать **добавить**.</span><span class="sxs-lookup"><span data-stu-id="65b30-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="65b30-184">При этом откроется hello **Конфигурация порта добавить** колонку.</span><span class="sxs-lookup"><span data-stu-id="65b30-184">This opens hello **Add port configuration** blade.</span></span>

  ![Добавление порта][7]

4. <span data-ttu-id="65b30-186">На **Конфигурация порта добавить** колонке идентификации hello порт, тип протокола, разрешенных IP-адресов источника и максимальное время запроса.</span><span class="sxs-lookup"><span data-stu-id="65b30-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="65b30-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="65b30-187">Select **OK**.</span></span>
6. <span data-ttu-id="65b30-188">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="65b30-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="65b30-189">Аудит действий JIT-доступа</span><span class="sxs-lookup"><span data-stu-id="65b30-189">Auditing just in time access activity</span></span>

<span data-ttu-id="65b30-190">Для просмотра действий виртуальной машины можно воспользоваться поиском по журналам.</span><span class="sxs-lookup"><span data-stu-id="65b30-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="65b30-191">журналы tooview:</span><span class="sxs-lookup"><span data-stu-id="65b30-191">tooview logs:</span></span>

1. <span data-ttu-id="65b30-192">На hello **непосредственно в ВМ доступа на время** колонки, выберите hello **настроенный** вкладки.</span><span class="sxs-lookup"><span data-stu-id="65b30-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="65b30-193">В разделе **виртуальные машины**, выберите tooview данных виртуальной Машины о, щелкнув hello трех точек в строке приветствия для этой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="65b30-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="65b30-194">Откроется меню.</span><span class="sxs-lookup"><span data-stu-id="65b30-194">This opens a menu.</span></span>
3. <span data-ttu-id="65b30-195">Выберите **журнал действий** в меню hello.</span><span class="sxs-lookup"><span data-stu-id="65b30-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="65b30-196">При этом откроется hello **журнал действий** колонку.</span><span class="sxs-lookup"><span data-stu-id="65b30-196">This opens hello **Activity log** blade.</span></span>

![Выбор журнала действий][9]

<span data-ttu-id="65b30-198">Hello **журнал действий** стоечный модуль обеспечивает отфильтрованное представление предыдущих операций для этой виртуальной Машины, а также даты, времени и подписки.</span><span class="sxs-lookup"><span data-stu-id="65b30-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Просмотр журнала действий][5]

<span data-ttu-id="65b30-200">Можно загрузить сведения о журнале hello, выбрав **щелкните здесь toodownload все элементы hello как CSV**.</span><span class="sxs-lookup"><span data-stu-id="65b30-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="65b30-201">Изменение фильтров hello и выберите **применить** toocreate поиска и журнала.</span><span class="sxs-lookup"><span data-stu-id="65b30-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="65b30-202">Использование JIT-доступа через PowerShell</span><span class="sxs-lookup"><span data-stu-id="65b30-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="65b30-203">В порядке hello toouse только в решении времени через PowerShell, убедитесь, что у вас есть hello [последнюю](/powershell/azure/install-azurerm-ps) версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65b30-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="65b30-204">После этого необходимо tooinstall hello [последние](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) центра безопасности Azure из коллекции PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="65b30-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="65b30-205">Настройка политики JIT-доступа для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="65b30-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="65b30-206">только что tooconfigure политику времени на определенную виртуальную Машину, нужен toorun эту команду в сеансе PowerShell: ASCJITAccessPolicy набор.</span><span class="sxs-lookup"><span data-stu-id="65b30-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="65b30-207">Выполните дополнительные toolearn документации командлет hello.</span><span class="sxs-lookup"><span data-stu-id="65b30-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="65b30-208">Запрашивает доступ tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="65b30-208">Requesting access tooa VM</span></span>

<span data-ttu-id="65b30-209">tooaccess определенной виртуальной Машине с защитой hello только в решении, время, вы должны toorun эту команду в сеансе PowerShell: вызов ASCJITAccess.</span><span class="sxs-lookup"><span data-stu-id="65b30-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="65b30-210">Выполните дополнительные toolearn документации командлет hello.</span><span class="sxs-lookup"><span data-stu-id="65b30-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65b30-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65b30-211">Next steps</span></span>
<span data-ttu-id="65b30-212">В этой статье вы узнали, как на момент времени доступа к ВМ в центр обеспечения безопасности помогает контролировать доступ tooyour Azure виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="65b30-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="65b30-213">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="65b30-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="65b30-214">[Установка политики безопасности](security-center-policies.md) — Узнайте как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="65b30-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="65b30-215">[Управление рекомендациями по безопасности](security-center-recommendations.md) — сведения об использовании рекомендаций для защиты ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="65b30-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="65b30-216">[Наблюдение за работоспособностью безопасности](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="65b30-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="65b30-217">[Управление и отвечать на запросы оповещения toosecurity](security-center-managing-and-responding-alerts.md) — Дополнительные сведения как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="65b30-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="65b30-218">[Мониторинг решений партнера](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="65b30-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="65b30-219">[Центр обеспечения безопасности часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="65b30-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="65b30-220">[Блог по безопасности Azure](https://blogs.msdn.microsoft.com/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="65b30-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
