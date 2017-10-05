---
title: "Защита персональных данных с помощью центра безопасности Azure | Документация Майкрософт"
description: "Сведения о защите персональных данных с помощью центра безопасности Azure."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3a941389713a4d3dbffbbfe8a717409927d85c6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="2c422-103">Защита персональных данных от атак и брешей в системе безопасности с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="2c422-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="2c422-104">Эта статья поможет вам понять, как защитить персональные данные от атак и брешей в системе безопасности с помощью центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="2c422-104">This article will help you understand how to use Azure Security Center to protect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="2c422-105">Сценарий</span><span class="sxs-lookup"><span data-stu-id="2c422-105">Scenario</span></span> 

<span data-ttu-id="2c422-106">Большая круизная компания, расположенная в США, расширяет масштабы своей деятельности, чтобы предоставлять маршруты в Средиземном и Балтийском морях, а также на Британских островах.</span><span class="sxs-lookup"><span data-stu-id="2c422-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="2c422-107">Чтобы реализовать эту программу, компания приобрела несколько небольших круизных фирм, расположенных в Италии, Германии, Дании и Великобритании.</span><span class="sxs-lookup"><span data-stu-id="2c422-107">To help in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="2c422-108">Корпоративные данные компании хранятся в облаке Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2c422-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="2c422-109">Сюда входят персональные данные, позволяющие установить личность, например имена, адреса, номера телефонов и данные кредитной карты.</span><span class="sxs-lookup"><span data-stu-id="2c422-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="2c422-110">К ним также относятся:</span><span class="sxs-lookup"><span data-stu-id="2c422-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="2c422-111">Адреса</span><span class="sxs-lookup"><span data-stu-id="2c422-111">Addresses</span></span>
- <span data-ttu-id="2c422-112">номера телефонов;</span><span class="sxs-lookup"><span data-stu-id="2c422-112">Phone numbers</span></span>
- <span data-ttu-id="2c422-113">идентификационные номера налогоплательщиков;</span><span class="sxs-lookup"><span data-stu-id="2c422-113">Tax identification numbers</span></span>
- <span data-ttu-id="2c422-114">медицинские сведения.</span><span class="sxs-lookup"><span data-stu-id="2c422-114">Medical information</span></span>

<span data-ttu-id="2c422-115">Круизная компания также содержит большую базу данных участников программ лояльности и программ скидок.</span><span class="sxs-lookup"><span data-stu-id="2c422-115">The cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="2c422-116">Сотрудники компании получают доступ к сети из удаленных филиалов, а туристические агентства, расположенные по всему миру, имеют доступ к отдельным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="2c422-116">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>
<span data-ttu-id="2c422-117">Персональные данные передаются по сети между этими расположениями и центром обработки данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2c422-117">Personal data travels across the network between these locations and the Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="2c422-118">Проблема</span><span class="sxs-lookup"><span data-stu-id="2c422-118">Problem statement</span></span>

<span data-ttu-id="2c422-119">Компания обеспокоена тем, что ее ресурсы Azure могут подвергнуться атаке злоумышленников, и</span><span class="sxs-lookup"><span data-stu-id="2c422-119">The company is concerned about the threat of attacks on their Azure resources.</span></span> <span data-ttu-id="2c422-120">хочет предотвратить доступ сторонних лиц к персональным данным клиентов и сотрудников.</span><span class="sxs-lookup"><span data-stu-id="2c422-120">They want to prevent exposure of customers’ and employees’ personal data to unauthorized persons.</span></span> <span data-ttu-id="2c422-121">Она нуждается в решении, способном обезопасить и восстановить базу данных, а также в эффективном способе мониторинга текущего уровня безопасности своих облачных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2c422-121">They want guidance on both prevention and response/remediation, as well as an effective way to monitor the ongoing security of their cloud resources.</span></span>
<span data-ttu-id="2c422-122">Кроме того, ей нужна надежная защита, которая может противостоять современным сложным методам организованного взлома.</span><span class="sxs-lookup"><span data-stu-id="2c422-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="2c422-123">Цель компании</span><span class="sxs-lookup"><span data-stu-id="2c422-123">Company goal</span></span>

<span data-ttu-id="2c422-124">Одна из целей компании — обеспечить конфиденциальность персональных данных клиентов и сотрудников и защитить их от угроз.</span><span class="sxs-lookup"><span data-stu-id="2c422-124">One of the company’s goals is to ensure the privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="2c422-125">Кроме того, им нужно решение, позволяющее немедленно реагировать на бреши в системе безопасности.</span><span class="sxs-lookup"><span data-stu-id="2c422-125">One of their goals is to respond immediately to signs of breach to mitigate the impact.</span></span> <span data-ttu-id="2c422-126">Компания должна иметь возможность оценивать текущее состояние системы безопасности, определять уязвимые конфигурации и устранять их.</span><span class="sxs-lookup"><span data-stu-id="2c422-126">It requires a way to assess the current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="2c422-127">Решения</span><span class="sxs-lookup"><span data-stu-id="2c422-127">Solutions</span></span>

<span data-ttu-id="2c422-128">Центр безопасности Microsoft Azure (ASC) предоставляет встроенное решение по мониторингу системы безопасности и управлению политиками.</span><span class="sxs-lookup"><span data-stu-id="2c422-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="2c422-129">Это решение предоставляет простые в использовании и эффективные возможности предотвращения, обнаружения и устранения угроз.</span><span class="sxs-lookup"><span data-stu-id="2c422-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="2c422-130">Предотвращение</span><span class="sxs-lookup"><span data-stu-id="2c422-130">Prevention</span></span>

<span data-ttu-id="2c422-131">ASC помогает предотвратить возникновение брешей в системе безопасности, позволяя устанавливать политики безопасности, обеспечивать JIT-доступ и реализовать рекомендации по безопасности.</span><span class="sxs-lookup"><span data-stu-id="2c422-131">ASC helps you prevent breaches by enabling you to set security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="2c422-132">Политика безопасности определяет набор элементов управления, рекомендованных для ресурсов в указанной подписке.</span><span class="sxs-lookup"><span data-stu-id="2c422-132">A security policy defines the set of controls recommended for resources within the specified subscription.</span></span> <span data-ttu-id="2c422-133">JIT-доступ позволяет блокировать входящий трафик виртуальных машин Azure, уменьшая за счет этого подверженность атакам.</span><span class="sxs-lookup"><span data-stu-id="2c422-133">Just in time access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks.</span></span> <span data-ttu-id="2c422-134">ASC создает рекомендации по обеспечению безопасности после анализа состояния безопасности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="2c422-134">Security recommendations are created by ASC after analyzing the security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="2c422-135">Настройка политик безопасности в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="2c422-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="2c422-136">Политики безопасности можно настроить для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="2c422-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="2c422-137">Изменить политику безопасности может пользователь с правами владельца или участника этой подписки.</span><span class="sxs-lookup"><span data-stu-id="2c422-137">To modify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="2c422-138">На портале Azure выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2c422-138">In the Azure portal, do the following:</span></span>

1. <span data-ttu-id="2c422-139">На панели мониторинга ASC выберите **политику**.</span><span class="sxs-lookup"><span data-stu-id="2c422-139">Select **Policy** in the ASC dashboard.</span></span>

2. <span data-ttu-id="2c422-140">Выберите подписку, для которой вы хотите включить политику.</span><span class="sxs-lookup"><span data-stu-id="2c422-140">Select the subscription on which you want to enable the policy.</span></span>

3. <span data-ttu-id="2c422-141">Выберите **политику предотвращения**, чтобы настроить политики для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="2c422-141">Choose **Prevention policy** to configure policies per subscription.</span></span> <span data-ttu-id="2c422-142">Установите переключатель **Сбор данных с виртуальных машин** в положение **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="2c422-142">**Collect data from virtual machines** should be set to **On.**</span></span>

4. <span data-ttu-id="2c422-143">В колонке **Политика предотвращения** установите переключатель в положение **Вкл.**, чтобы включить рекомендации по безопасности, соответствующие этой подписке.</span><span class="sxs-lookup"><span data-stu-id="2c422-143">In the **Prevention policy** options, select **On** to enable the security recommendations that are relevant for the subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="2c422-144">Подробные инструкции и сведения о каждой из рекомендаций по безопасности, которые можно включить, см. в разделе [Установка политик безопасности](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="2c422-144">For more detailed instructions and an explanation of each of the policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="2c422-145">Настройка JIT-доступа</span><span class="sxs-lookup"><span data-stu-id="2c422-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="2c422-146">Если JIT-доступ включен, центр безопасности блокирует входящий трафик виртуальной машины Azure путем создания правила группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="2c422-146">When JIT is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="2c422-147">Вы выбираете порты на виртуальной машине, для которых будет заблокирован входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="2c422-147">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="2c422-148">Чтобы включить JIT-доступ, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2c422-148">To use JIT access, do the following:</span></span>

1. <span data-ttu-id="2c422-149">В колонке ASC выберите **JIT-доступ к виртуальным машинам**.</span><span class="sxs-lookup"><span data-stu-id="2c422-149">Select the **Just in time VM access tile** on the ASC blade.</span></span>

2. <span data-ttu-id="2c422-150">Перейдите на вкладку **Рекомендуется**.</span><span class="sxs-lookup"><span data-stu-id="2c422-150">Select the **Recommended** tab.</span></span>

3. <span data-ttu-id="2c422-151">В разделе **Виртуальные машины** выберите виртуальные машины, для которых вы хотите включить JIT-доступ.</span><span class="sxs-lookup"><span data-stu-id="2c422-151">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="2c422-152">При этом устанавливается флажок рядом с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="2c422-152">This puts a checkmark next to a VM.</span></span> 
4. <span data-ttu-id="2c422-153">Выберите **Включить JIT на виртуальных машинах**.</span><span class="sxs-lookup"><span data-stu-id="2c422-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="2c422-154">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2c422-154">Select **Save**.</span></span>

<span data-ttu-id="2c422-155">Это позволит отобразить номера портов, для которых ASC рекомендует включить JIT.</span><span class="sxs-lookup"><span data-stu-id="2c422-155">Then you can see the default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="2c422-156">Вы также можете добавить и настроить новый порт, в котором необходимо включить JIT-доступ.</span><span class="sxs-lookup"><span data-stu-id="2c422-156">You can also add and configure a new port on which you want to enable the just in time solution.</span></span> <span data-ttu-id="2c422-157">На плитке **JIT-доступ к виртуальным машинам** в центре безопасности отображается количество виртуальных машин, на которых реализован JIT-доступ,</span><span class="sxs-lookup"><span data-stu-id="2c422-157">The **Just in time VM access** tile in the Security Center shows the number of VMs configured for JIT access.</span></span> <span data-ttu-id="2c422-158">а также число утвержденных запросов на доступ за последнюю неделю.</span><span class="sxs-lookup"><span data-stu-id="2c422-158">It also shows the number of approved access requests made in the last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="2c422-159">Инструкции по реализации JIT-доступа и дополнительные сведения об этой возможности см. в статье [Управление доступом к виртуальным машинам с помощью JIT](https://docs.microsoft.com/azure/security-center/security-center-just-in-time).</span><span class="sxs-lookup"><span data-stu-id="2c422-159">For instructions on how to do this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="2c422-160">Реализация рекомендаций по безопасности ASC</span><span class="sxs-lookup"><span data-stu-id="2c422-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="2c422-161">Когда Центр безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации.</span><span class="sxs-lookup"><span data-stu-id="2c422-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="2c422-162">Рекомендации помогают настраивать необходимые элементы управления.</span><span class="sxs-lookup"><span data-stu-id="2c422-162">The recommendations guide you through the process of configuring the needed controls.</span></span> 
1. <span data-ttu-id="2c422-163">На панели мониторинга ASC выберите **Рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="2c422-163">Select the **Recommendations** tile on the ASC dashboard.</span></span>

2. <span data-ttu-id="2c422-164">Рекомендации отображаются в табличном формате, где каждая строка представляет одну конкретную рекомендацию.</span><span class="sxs-lookup"><span data-stu-id="2c422-164">View the recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="2c422-165">Чтобы отфильтровать рекомендации, выберите **Фильтр** и укажите значения серьезности и состояния, которые вы хотите просмотреть.</span><span class="sxs-lookup"><span data-stu-id="2c422-165">To filter recommendations, select **Filter** and select the severity and state values you wish to see.</span></span>

4. <span data-ttu-id="2c422-166">Чтобы отклонить рекомендации, которые не применяются, щелкните правой кнопкой мыши и выберите **Отклонить**.</span><span class="sxs-lookup"><span data-stu-id="2c422-166">To dismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="2c422-167">Решите, какие рекомендации следует применить первыми.</span><span class="sxs-lookup"><span data-stu-id="2c422-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="2c422-168">Применяйте рекомендации в порядке приоритета.</span><span class="sxs-lookup"><span data-stu-id="2c422-168">Apply the recommendations in order of priority.</span></span>

<span data-ttu-id="2c422-169">Список возможных рекомендаций и руководства по их применению см. в статье [Управление рекомендациями по безопасности в Центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-recommendations).</span><span class="sxs-lookup"><span data-stu-id="2c422-169">For a list of possible recommendations and walk-throughs on how to apply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="2c422-170">Обнаружение и ответные меры</span><span class="sxs-lookup"><span data-stu-id="2c422-170">Detection and Response</span></span>

<span data-ttu-id="2c422-171">Обнаружение и ответные меры сочетаются, так как после обнаружения угрозы требуется как можно быстрее отреагировать на нее.</span><span class="sxs-lookup"><span data-stu-id="2c422-171">Detection and response go together, as you want to respond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="2c422-172">Функция обнаружения угроз в центре безопасности автоматически собирает данные о безопасности из ваших ресурсов Azure, сети и подключенных партнерских решений.</span><span class="sxs-lookup"><span data-stu-id="2c422-172">ASC threat detection works by automatically collecting security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="2c422-173">Поэтому, когда злоумышленники создают все более сложные эксплойты, центр безопасности обновляет свои алгоритмы обнаружения максимально оперативно.</span><span class="sxs-lookup"><span data-stu-id="2c422-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="2c422-174">Дополнительные сведения о способах обнаружения угроз в центре безопасности см. в статье [Возможности обнаружения центра безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="2c422-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-to-security-alerts"></a><span data-ttu-id="2c422-175">Управление оповещениями системы безопасности и реагирование на них</span><span class="sxs-lookup"><span data-stu-id="2c422-175">How do I manage and respond to security alerts?</span></span>

<span data-ttu-id="2c422-176">Список приоритетных оповещений системы безопасности отображается в центре безопасности вместе с данными, необходимыми для быстрого анализа проблемы.</span><span class="sxs-lookup"><span data-stu-id="2c422-176">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem.</span></span> <span data-ttu-id="2c422-177">Центр безопасности также предоставляет рекомендации по устранению атак.</span><span class="sxs-lookup"><span data-stu-id="2c422-177">Security Center also includes recommendations for how to remediate an attack.</span></span> <span data-ttu-id="2c422-178">Чтобы управлять оповещениями системы безопасности, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2c422-178">To manage your security alerts, do the following:</span></span>

1. <span data-ttu-id="2c422-179">Щелкните плитку **Оповещений системы безопасности** на панели мониторинга ASC.</span><span class="sxs-lookup"><span data-stu-id="2c422-179">Select the **Security alerts** tile in the ASC dashboard.</span></span> <span data-ttu-id="2c422-180">Отобразятся данные по каждому оповещению.</span><span class="sxs-lookup"><span data-stu-id="2c422-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="2c422-181">Чтобы фильтровать оповещения по дате, состоянию и степени серьезности, выберите **Фильтр**, а затем выберите значения, которые нужно просмотреть.</span><span class="sxs-lookup"><span data-stu-id="2c422-181">To filter alerts based on date, state, and severity, select **Filter** and then select the values you want to see.</span></span>

3. <span data-ttu-id="2c422-182">Чтобы ответить на оповещение, выберите его и просмотрите сведения, а затем выберите ресурс, на который направлялась атака.</span><span class="sxs-lookup"><span data-stu-id="2c422-182">To respond to an alert, select it and review the information, then select the resource that was attacked.</span></span>

4. <span data-ttu-id="2c422-183">В поле **Описание** вы увидите подробные сведения, в том числе рекомендуемые исправления.</span><span class="sxs-lookup"><span data-stu-id="2c422-183">In the **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="2c422-184">Подробные инструкции по управлению оповещениями системы безопасности см. в статье [Управление оповещениями безопасности в центре безопасности Azure и реагирование на них](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="2c422-184">For more detailed instructions on responding to security alerts, see [Managing and responding to security alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="2c422-185">Для дальнейшей помощи в изучении оповещений системы безопасности компания может интегрировать оповещения ASC с собственным решением SIEM, используя [интеграцию журналов Azure](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="2c422-185">For further help in investigating security alerts, the company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="2c422-186">Управление инцидентами безопасности</span><span class="sxs-lookup"><span data-stu-id="2c422-186">How do I manage security incidents?</span></span>

<span data-ttu-id="2c422-187">Инцидент безопасности — это совокупность всех оповещений для ресурса, сопоставимых со схемами нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="2c422-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="2c422-188">Инцидент содержит список соответствующих оповещений, который позволяет получить дополнительные сведения о каждом происшествии.</span><span class="sxs-lookup"><span data-stu-id="2c422-188">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span> <span data-ttu-id="2c422-189">Инциденты отображаются на плитке "Оповещения системы безопасности" и в одноименной колонке.</span><span class="sxs-lookup"><span data-stu-id="2c422-189">Incidents appear in the Security Alerts tile and blade.</span></span>

<span data-ttu-id="2c422-190">Чтобы просмотреть инциденты безопасности и управлять ими, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2c422-190">To review and manage security incidents, do the following:</span></span>

1. <span data-ttu-id="2c422-191">Щелкните плитку **Оповещения системы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="2c422-191">Select the **Security alerts** tile.</span></span> <span data-ttu-id="2c422-192">Обнаруженный инцидент отобразится под диаграммой предупреждений безопасности.</span><span class="sxs-lookup"><span data-stu-id="2c422-192">if a security incident is detected, it will appear under the security alerts graph.</span></span> <span data-ttu-id="2c422-193">Его значок отличается от других оповещений.</span><span class="sxs-lookup"><span data-stu-id="2c422-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="2c422-194">Выберите инцидент, чтобы просмотреть дополнительные сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="2c422-194">Select the incident to see more details about this security incident.</span></span> <span data-ttu-id="2c422-195">К дополнительным сведениям относятся полное описание, серьезность, текущее состояние, атакуемый ресурс, шаги исправления и оповещения, полученные с этим инцидентом.</span><span class="sxs-lookup"><span data-stu-id="2c422-195">Additional details include its full description, its severity, its current state, the attacked resource, the remediation steps for the incident, and the alerts that were included in this incident.</span></span>

<span data-ttu-id="2c422-196">Вы можете применить фильтр и просмотреть **только инциденты**, **только оповещения** или **и то, и другое**.</span><span class="sxs-lookup"><span data-stu-id="2c422-196">You can filter to see **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-the-threat-intelligence-report"></a><span data-ttu-id="2c422-197">Получение доступа к отчету об анализе угроз</span><span class="sxs-lookup"><span data-stu-id="2c422-197">How do I access the Threat Intelligence Report?</span></span>

<span data-ttu-id="2c422-198">ASC анализирует сведения из разных источников и определяет угрозы.</span><span class="sxs-lookup"><span data-stu-id="2c422-198">ASC analyzes information from multiple sources to identify threats.</span></span> <span data-ttu-id="2c422-199">Чтобы упростить исследование и устранение угроз для групп реагирования на инциденты, в центре безопасности формируется отчет об анализе угроз.</span><span class="sxs-lookup"><span data-stu-id="2c422-199">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected.</span></span>

<span data-ttu-id="2c422-200">Центр безопасности предусматривает три типа отчетов об угрозах, которые могут различаться в зависимости от атаки.</span><span class="sxs-lookup"><span data-stu-id="2c422-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="2c422-201">а именно:</span><span class="sxs-lookup"><span data-stu-id="2c422-201">The reports available are:</span></span>

- <span data-ttu-id="2c422-202">Отчет о группе действий, в котором предоставлен подробный анализ злоумышленников, их целей и примененных тактик.</span><span class="sxs-lookup"><span data-stu-id="2c422-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="2c422-203">Отчет о кампании, сосредоточенный на определенных кампаниях атак.</span><span class="sxs-lookup"><span data-stu-id="2c422-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="2c422-204">Сводный отчет об угрозах, который включает в себя все элементы двух предыдущих отчетов.</span><span class="sxs-lookup"><span data-stu-id="2c422-204">Threat Summary Report: covers all items in the previous two reports.</span></span>

<span data-ttu-id="2c422-205">Эти сведения очень полезны в процессе реагирования на инцидент, когда ведется исследование, чтобы понять источник атаки, мотивацию злоумышленника и то, как избежать этой проблемы в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="2c422-205">This type of information is very useful during the incident response process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

1. <span data-ttu-id="2c422-206">Получение доступа к отчету об анализе угроз</span><span class="sxs-lookup"><span data-stu-id="2c422-206">To access the threat intelligence report, do the following:</span></span>

2. <span data-ttu-id="2c422-207">На панели мониторинга ASC щелкните плитку **Оповещений системы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="2c422-207">Select the **Security alerts** tile on the ASC dashboard.</span></span>

3. <span data-ttu-id="2c422-208">Выберите оповещение системы безопасности, сведения о котором вы хотите получить.</span><span class="sxs-lookup"><span data-stu-id="2c422-208">Select the security alert for which you want to obtain more information.</span></span>

4. <span data-ttu-id="2c422-209">В поле **Отчеты** щелкните ссылку на отчет об анализе угроз.</span><span class="sxs-lookup"><span data-stu-id="2c422-209">In the **Reports** field, click the link to the threat intelligence report.</span></span>

5. <span data-ttu-id="2c422-210">Откроется PDF-файл, который можно скачать.</span><span class="sxs-lookup"><span data-stu-id="2c422-210">This will open the PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="2c422-211">Дополнительные сведения об отчете ASC об анализе угроз см. в статье [Отчет об анализе угроз, предоставляемый центром безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-threat-report).</span><span class="sxs-lookup"><span data-stu-id="2c422-211">For additional information about the ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="2c422-212">Оценка</span><span class="sxs-lookup"><span data-stu-id="2c422-212">Assessment</span></span>

<span data-ttu-id="2c422-213">Чтобы упростить тестирование и оценку состояния вашей системы безопасности, ASC обеспечивает интегрированное решение оценки уязвимостей с облачными агентами Qualys в составе компонента рекомендаций по виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="2c422-213">To help with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="2c422-214">Агент Qualys передает данные об уязвимостях на платформу управления Qualys, которая затем отправляет данные мониторинга уязвимостей и работоспособности в ASC.</span><span class="sxs-lookup"><span data-stu-id="2c422-214">The Qualys agent reports vulnerability data to the Qualys management platform, which then sends vulnerability and health monitoring data back to ASC.</span></span> <span data-ttu-id="2c422-215">Рекомендация по добавлению решения оценки уязвимости отображается в колонке **Рекомендации** на панели управления ASC.</span><span class="sxs-lookup"><span data-stu-id="2c422-215">The recommendation to add a vulnerability assessment solution is displayed in the **Recommendations** blade on the ASC dashboard.</span></span>

<span data-ttu-id="2c422-216">Когда решение для оценки уязвимостей будет установлено на целевой ВМ, центром безопасности будет запущено сканирование ВМ для поиска и определения уязвимостей в системе и приложениях.</span><span class="sxs-lookup"><span data-stu-id="2c422-216">After the vulnerability assessment solution is installed on the target VM, Security Center scans the VM to detect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="2c422-217">Обнаруженные проблемы выводятся в разделе с **рекомендациями для ВМ**.</span><span class="sxs-lookup"><span data-stu-id="2c422-217">Detected issues are shown under the **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="2c422-218">Реализация решения по оценке уязвимостей</span><span class="sxs-lookup"><span data-stu-id="2c422-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="2c422-219">Если на виртуальной машине не установлено интегрированное решение по оценке уязвимостей, центр безопасности рекомендует установить его.</span><span class="sxs-lookup"><span data-stu-id="2c422-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="2c422-220">В колонке **Рекомендации** выберите **Добавление решения по оценке уязвимостей**.</span><span class="sxs-lookup"><span data-stu-id="2c422-220">In the ASC dashboard, on the **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="2c422-221">Выберите виртуальные машины, на которых вы хотите установить решение по оценке уязвимостей.</span><span class="sxs-lookup"><span data-stu-id="2c422-221">Select the VMs where you want to install the vulnerability assessment solution.</span></span>

3. <span data-ttu-id="2c422-222">Щелкните **Установить на следующем количестве виртуальных машин: [количество]**.</span><span class="sxs-lookup"><span data-stu-id="2c422-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="2c422-223">Выберите решение партнера в Azure Marketplace или выберите **Qualys** в разделе **Использование существующего решения**.</span><span class="sxs-lookup"><span data-stu-id="2c422-223">Select a partner solution in the Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="2c422-224">Вы можете включить параметры автоматического обновления в колонке **Решения партнеров**.</span><span class="sxs-lookup"><span data-stu-id="2c422-224">You can turn the auto update settings on or off in the **Partner Solutions** blade.</span></span>

<span data-ttu-id="2c422-225">Инструкции по реализации решения по оценке уязвимостей см. в статье [Оценка уязвимостей в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations).</span><span class="sxs-lookup"><span data-stu-id="2c422-225">For further instructions on how to implement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c422-226">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c422-226">Next steps</span></span>

- [<span data-ttu-id="2c422-227">Краткое руководство по центру безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="2c422-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="2c422-228">Введение в Центр безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="2c422-228">Introduction to Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="2c422-229">Интеграция оповещений центра безопасности Azure с помощью интеграции журналов Azure</span><span class="sxs-lookup"><span data-stu-id="2c422-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- <span data-ttu-id="2c422-230">[Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/) (Расширение возможностей центра безопасности Azure с помощью интегрированного решения по оценке уязвимостей)</span><span class="sxs-lookup"><span data-stu-id="2c422-230">[Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)</span></span>
