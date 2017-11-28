---
title: "aaaProtect личных данных с помощью центра безопасности Azure | Документы Microsoft"
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
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="410b6-103">Защита персональных данных от атак и брешей в системе безопасности с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="410b6-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="410b6-104">Данная статья поможет вам понять, как нарушения toouse центра безопасности Azure tooprotect персональные данные из и атак.</span><span class="sxs-lookup"><span data-stu-id="410b6-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="410b6-105">Сценарий</span><span class="sxs-lookup"><span data-stu-id="410b6-105">Scenario</span></span> 

<span data-ttu-id="410b6-106">Большой прогулка по организации, штаб-квартира компании в США, hello развернут расписаниям toooffer его операций в hello морская, балтийские компании seas, а также hello Британские острова.</span><span class="sxs-lookup"><span data-stu-id="410b6-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="410b6-107">в этих усилиях toohelp, он получил несколько небольших строк прогулка по в Италии, Германии, Дания и hello Великобритания</span><span class="sxs-lookup"><span data-stu-id="410b6-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="410b6-108">Hello компания использует Microsoft Azure toostore корпоративных данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="410b6-109">Сюда входят персональные данные, позволяющие установить личность, например имена, адреса, номера телефонов и данные кредитной карты.</span><span class="sxs-lookup"><span data-stu-id="410b6-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="410b6-110">К ним также относятся:</span><span class="sxs-lookup"><span data-stu-id="410b6-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="410b6-111">Адреса</span><span class="sxs-lookup"><span data-stu-id="410b6-111">Addresses</span></span>
- <span data-ttu-id="410b6-112">номера телефонов;</span><span class="sxs-lookup"><span data-stu-id="410b6-112">Phone numbers</span></span>
- <span data-ttu-id="410b6-113">идентификационные номера налогоплательщиков;</span><span class="sxs-lookup"><span data-stu-id="410b6-113">Tax identification numbers</span></span>
- <span data-ttu-id="410b6-114">медицинские сведения.</span><span class="sxs-lookup"><span data-stu-id="410b6-114">Medical information</span></span>

<span data-ttu-id="410b6-115">Строка Hello прогулка по также хранится большой базы данных вознаграждения и постоянных элементов программы.</span><span class="sxs-lookup"><span data-stu-id="410b6-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="410b6-116">Сотрудники предприятий сети hello доступ из удаленных офисов и путешествий hello компании расположены по всему Здравствуй, мир! имеют доступ к ресурсам компании toosome.</span><span class="sxs-lookup"><span data-stu-id="410b6-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="410b6-117">Персональные данные передаваемого по сети hello между этими расположения и hello центр обработки данных.</span><span class="sxs-lookup"><span data-stu-id="410b6-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="410b6-118">Проблема</span><span class="sxs-lookup"><span data-stu-id="410b6-118">Problem statement</span></span>

<span data-ttu-id="410b6-119">Компания Hello беспокоит hello угрозы атак на свои ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="410b6-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="410b6-120">Должен быть раскрытия tooprevent лиц toounauthorized персональные данные сотрудников и клиентов.</span><span class="sxs-lookup"><span data-stu-id="410b6-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="410b6-121">Должен быть рекомендации по и предотвращения и ответа или исправление, а также эффективным способом toomonitor hello безопасности облачными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="410b6-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="410b6-122">Кроме того, ей нужна надежная защита, которая может противостоять современным сложным методам организованного взлома.</span><span class="sxs-lookup"><span data-stu-id="410b6-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="410b6-123">Цель компании</span><span class="sxs-lookup"><span data-stu-id="410b6-123">Company goal</span></span>

<span data-ttu-id="410b6-124">Одна из целей компании hello — tooensure hello конфиденциальность сотрудников и клиентов личных данных, защищая от угроз.</span><span class="sxs-lookup"><span data-stu-id="410b6-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="410b6-125">Одна из их целей — toorespond немедленно toosigns из toomitigate нарушения hello влияния.</span><span class="sxs-lookup"><span data-stu-id="410b6-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="410b6-126">Требуется способ tooassess hello текущее состояние безопасности, выявления конфигурации уязвимых мест и исправлять их.</span><span class="sxs-lookup"><span data-stu-id="410b6-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="410b6-127">Решения</span><span class="sxs-lookup"><span data-stu-id="410b6-127">Solutions</span></span>

<span data-ttu-id="410b6-128">Центр безопасности Microsoft Azure (ASC) предоставляет встроенное решение по мониторингу системы безопасности и управлению политиками.</span><span class="sxs-lookup"><span data-stu-id="410b6-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="410b6-129">Это решение предоставляет простые в использовании и эффективные возможности предотвращения, обнаружения и устранения угроз.</span><span class="sxs-lookup"><span data-stu-id="410b6-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="410b6-130">Предотвращение</span><span class="sxs-lookup"><span data-stu-id="410b6-130">Prevention</span></span>

<span data-ttu-id="410b6-131">ASC помогает предотвращения угроз, позволяя tooset политики безопасности, обеспечивают доступ в времени и реализовать рекомендации по безопасности.</span><span class="sxs-lookup"><span data-stu-id="410b6-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="410b6-132">Политика безопасности определяет набор элементов управления, рекомендуется для ресурсов в пределах указанного hello hello подписки.</span><span class="sxs-lookup"><span data-stu-id="410b6-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="410b6-133">На момент времени доступ может быть используется toolock вниз tooyour входящего трафика виртуальных машин Azure, уменьшая tooattacks раскрытия.</span><span class="sxs-lookup"><span data-stu-id="410b6-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="410b6-134">Рекомендации по обеспечению безопасности создаются ASC после анализа состояния безопасности hello ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="410b6-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="410b6-135">Настройка политик безопасности в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="410b6-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="410b6-136">Политики безопасности можно настроить для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="410b6-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="410b6-137">toomodify политику безопасности, необходимо быть владельцем или участником этой подписки.</span><span class="sxs-lookup"><span data-stu-id="410b6-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="410b6-138">В hello портал Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="410b6-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="410b6-139">Выберите **политики** в панели мониторинга ASC hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="410b6-140">Выберите подписку hello, на котором будет tooenable hello политики.</span><span class="sxs-lookup"><span data-stu-id="410b6-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="410b6-141">Выберите **политика предотвращения** tooconfigure политики на одну подписку.</span><span class="sxs-lookup"><span data-stu-id="410b6-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="410b6-142">**Сбор данных из виртуальных машин** должно быть задано слишком**на.**</span><span class="sxs-lookup"><span data-stu-id="410b6-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="410b6-143">В hello **политика предотвращения** параметры, выберите **на** tooenable hello безопасности рекомендаций, относящихся к подписке hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="410b6-144">Более подробные инструкции и описание каждого hello политики рекомендаций, которые могут быть включены см. в разделе [Установка политики безопасности в центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="410b6-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="410b6-145">Настройка JIT-доступа</span><span class="sxs-lookup"><span data-stu-id="410b6-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="410b6-146">Если включена JIT-компилятора, центр обеспечения безопасности блокирует tooyour входящий трафик виртуальных машин Azure путем создания правила NSG.</span><span class="sxs-lookup"><span data-stu-id="410b6-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="410b6-147">Выберите порты hello на toowhich ВМ hello входящий трафик блокируется вниз.</span><span class="sxs-lookup"><span data-stu-id="410b6-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="410b6-148">toouse JIT доступ, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="410b6-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="410b6-149">Выберите hello **непосредственно на плитке доступа виртуальной Машины времени** колонке ASC hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="410b6-150">Выберите hello **рекомендуется** вкладки.</span><span class="sxs-lookup"><span data-stu-id="410b6-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="410b6-151">В разделе **виртуальные машины**, выберите hello виртуальных машин, которые должны tooenable.</span><span class="sxs-lookup"><span data-stu-id="410b6-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="410b6-152">Этот запрос помещает флажок Далее tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="410b6-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="410b6-153">Выберите **Включить JIT на виртуальных машинах**.</span><span class="sxs-lookup"><span data-stu-id="410b6-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="410b6-154">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="410b6-154">Select **Save**.</span></span>

<span data-ttu-id="410b6-155">Это позволит отобразить hello номера портов, которые рекомендует ASC Включение JIT-компилятора.</span><span class="sxs-lookup"><span data-stu-id="410b6-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="410b6-156">Кроме того, можно добавить и настроить новый порт, на котором будет hello tooenable только в решении, время.</span><span class="sxs-lookup"><span data-stu-id="410b6-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="410b6-157">Hello **непосредственно в ВМ доступа на время** отражает в hello центра обеспечения безопасности hello число виртуальных машин, настроенных для JIT-компилятора доступа.</span><span class="sxs-lookup"><span data-stu-id="410b6-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="410b6-158">Она также отображает hello число доступа утвержденных запросов, выполненных в hello прошлой неделе.</span><span class="sxs-lookup"><span data-stu-id="410b6-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="410b6-159">Дополнительные сведения о toodo, и просмотреть дополнительные сведения о непосредственно в доступ во время [управление доступом к виртуальной машине с помощью на момент времени.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="410b6-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="410b6-160">Реализация рекомендаций по безопасности ASC</span><span class="sxs-lookup"><span data-stu-id="410b6-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="410b6-161">Когда Центр безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации.</span><span class="sxs-lookup"><span data-stu-id="410b6-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="410b6-162">рекомендации Hello начнется процесс настройки элементов управления требуется hello hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="410b6-163">Выберите hello **рекомендации** плитки на панели мониторинга ASC hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="410b6-164">Просмотр рекомендаций hello, которые отображаются в виде таблицы, где каждая строка представляет одна рекомендация.</span><span class="sxs-lookup"><span data-stu-id="410b6-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="410b6-165">Выберите рекомендации toofilter **фильтра** и выберите hello серьезность и состояние значения, нужно toosee.</span><span class="sxs-lookup"><span data-stu-id="410b6-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="410b6-166">toodismiss рекомендации, которые не применяется, можно правой кнопкой мыши и выберите **прекратить.**</span><span class="sxs-lookup"><span data-stu-id="410b6-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="410b6-167">Решите, какие рекомендации следует применить первыми.</span><span class="sxs-lookup"><span data-stu-id="410b6-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="410b6-168">Применение рекомендаций hello в порядке приоритета.</span><span class="sxs-lookup"><span data-stu-id="410b6-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="410b6-169">Список возможных рекомендации и руководства пользователя о том, как tooapply каждого, в разделе [управление рекомендации по обеспечению безопасности в центр безопасности Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="410b6-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="410b6-170">Обнаружение и ответные меры</span><span class="sxs-lookup"><span data-stu-id="410b6-170">Detection and Response</span></span>

<span data-ttu-id="410b6-171">Обнаружение и ответ сочетаются, необходимо toorespond как можно быстрее после обнаружения угрозу.</span><span class="sxs-lookup"><span data-stu-id="410b6-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="410b6-172">Обнаружение угроз ASC работает автоматически собирает сведения о безопасности с ресурсы Azure, сети hello и решения партнеров подключенной.</span><span class="sxs-lookup"><span data-stu-id="410b6-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="410b6-173">Поэтому, когда злоумышленники создают все более сложные эксплойты, центр безопасности обновляет свои алгоритмы обнаружения максимально оперативно.</span><span class="sxs-lookup"><span data-stu-id="410b6-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="410b6-174">Дополнительные сведения о способах обнаружения угроз в центре безопасности см. в статье [Возможности обнаружения центра безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="410b6-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="410b6-175">Как управлять и отвечать toosecurity оповещения?</span><span class="sxs-lookup"><span data-stu-id="410b6-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="410b6-176">Список оповещений системы безопасности упорядоченный отображается в центре безопасности вместе с hello информацию, необходимую tooquickly Исследуйте проблему hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="410b6-177">Центр обеспечения безопасности также представлены рекомендации tooremediate атаки.</span><span class="sxs-lookup"><span data-stu-id="410b6-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="410b6-178">предупреждения безопасности, выполните следующие hello toomanage:</span><span class="sxs-lookup"><span data-stu-id="410b6-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="410b6-179">Выберите hello **оповещений системы безопасности** плитки на панели мониторинга ASC hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="410b6-180">Отобразятся данные по каждому оповещению.</span><span class="sxs-lookup"><span data-stu-id="410b6-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="410b6-181">Выберите toofilter оповещения на основе даты, состояние и уровень серьезности, **фильтра** и выберите hello значениями, toosee.</span><span class="sxs-lookup"><span data-stu-id="410b6-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="410b6-182">toorespond tooan предупреждение, выберите его и просмотреть сведения о hello, выберите ресурс hello, который был атаке.</span><span class="sxs-lookup"><span data-stu-id="410b6-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="410b6-183">В hello **описание** будет отображен сведения, включая Рекомендуемые исправления.</span><span class="sxs-lookup"><span data-stu-id="410b6-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="410b6-184">Более подробные инструкции по отвечает toosecurity предупреждений см. в разделе [toosecurity управление и отвечает на запросы предупреждения в центр безопасности Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="410b6-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="410b6-185">Для получения дополнительных сведений в исследовании оповещений системы безопасности компании hello можно интегрировать оповещения ASC собственное решение SIEM с помощью [интеграции Azure журнала](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="410b6-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="410b6-186">Управление инцидентами безопасности</span><span class="sxs-lookup"><span data-stu-id="410b6-186">How do I manage security incidents?</span></span>

<span data-ttu-id="410b6-187">Инцидент безопасности — это совокупность всех оповещений для ресурса, сопоставимых со схемами нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="410b6-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="410b6-188">Инцидент будет открывать связанные предупреждения список hello, который позволяет вам tooobtain дополнительную информацию о каждое вхождение.</span><span class="sxs-lookup"><span data-stu-id="410b6-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="410b6-189">Инциденты отображаются в приветствия плитку оповещений системы безопасности и колонки.</span><span class="sxs-lookup"><span data-stu-id="410b6-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="410b6-190">tooreview и управлять угрозы безопасности, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="410b6-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="410b6-191">Выберите hello **оповещений системы безопасности** плитки.</span><span class="sxs-lookup"><span data-stu-id="410b6-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="410b6-192">При обнаружении угрозы безопасности, он отобразится в график предупреждения безопасности hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="410b6-193">Его значок отличается от других оповещений.</span><span class="sxs-lookup"><span data-stu-id="410b6-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="410b6-194">Выберите Дополнительные сведения об инциденте безопасности инцидента toosee hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="410b6-195">Дополнительные сведения включают его полное описание, его важность, его текущее состояние, hello атаке ресурсов, действия по исправлению hello инциденте hello и hello оповещения, которые были включены в этот инцидент.</span><span class="sxs-lookup"><span data-stu-id="410b6-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="410b6-196">Вы можете фильтровать toosee **только инциденты**, **оповещения только**, или **оба**.</span><span class="sxs-lookup"><span data-stu-id="410b6-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="410b6-197">Как получить доступ к hello отчет по аналитике угрозой?</span><span class="sxs-lookup"><span data-stu-id="410b6-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="410b6-198">ASC анализирует сведения из нескольких источников tooidentify угроз.</span><span class="sxs-lookup"><span data-stu-id="410b6-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="410b6-199">команды реагирования tooassist исследовать и устранять угрозы, центр обеспечения безопасности включает отчет аналитики угроз, содержащий сведения об угрозах hello, обнаруженного.</span><span class="sxs-lookup"><span data-stu-id="410b6-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="410b6-200">Центр безопасности предусматривает три типа отчетов об угрозах, которые могут различаться в зависимости от атаки.</span><span class="sxs-lookup"><span data-stu-id="410b6-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="410b6-201">имеются следующие отчеты Hello:</span><span class="sxs-lookup"><span data-stu-id="410b6-201">hello reports available are:</span></span>

- <span data-ttu-id="410b6-202">Отчет о группе действий, в котором предоставлен подробный анализ злоумышленников, их целей и примененных тактик.</span><span class="sxs-lookup"><span data-stu-id="410b6-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="410b6-203">Отчет о кампании, сосредоточенный на определенных кампаниях атак.</span><span class="sxs-lookup"><span data-stu-id="410b6-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="410b6-204">Сводный отчет угроз: охватывает все элементы в предыдущих двух отчетов hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="410b6-205">Этот тип данных очень полезно во время процесса реагирования на события hello, которого в настоящее время исследования toounderstand hello источник атаки hello hello причин появления злоумышленника и какие toomitigate toodo выполните перемещение вперед.</span><span class="sxs-lookup"><span data-stu-id="410b6-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="410b6-206">Анализ угроз hello tooaccess отчетов, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="410b6-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="410b6-207">Выберите hello **оповещений системы безопасности** плитки на панели мониторинга ASC hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="410b6-208">Выберите hello предупреждения системы безопасности, для которого требуется tooobtain Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="410b6-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="410b6-209">В hello **отчеты** щелкните отчет по аналитике hello ссылку toohello угроз.</span><span class="sxs-lookup"><span data-stu-id="410b6-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="410b6-210">Откроется файл PDF hello, который можно загрузить.</span><span class="sxs-lookup"><span data-stu-id="410b6-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="410b6-211">Дополнительные сведения о hello отчет по аналитике угроз ASC см [отчет аналитики угроз центра безопасности Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="410b6-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="410b6-212">Оценка</span><span class="sxs-lookup"><span data-stu-id="410b6-212">Assessment</span></span>

<span data-ttu-id="410b6-213">toohelp тестирование, оценки и вычисления уровня безопасности ASC предоставляет для оценки уязвимости интеграции с Компанию Qualys агенты облака, как часть его компоненте рекомендации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="410b6-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="410b6-214">Уязвимость toohello Компанию Qualys платформу управления данными, который затем отправляет уязвимости и данные мониторинга работоспособности обратно tooASC подчиняется агент Компанию Qualys Hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="410b6-215">Здравствуйте рекомендация tooadd решения по оценке уязвимости отображается в hello **рекомендации** колонка на панели мониторинга ASC hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="410b6-216">После установки решения по оценке уязвимости hello на целевом сервере hello ВМ центра обеспечения безопасности hello toodetect ВМ и определение уязвимостей системы и приложений.</span><span class="sxs-lookup"><span data-stu-id="410b6-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="410b6-217">Обнаружены проблемы, отображаются под hello **виртуальных машин рекомендации** параметр.</span><span class="sxs-lookup"><span data-stu-id="410b6-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="410b6-218">Реализация решения по оценке уязвимостей</span><span class="sxs-lookup"><span data-stu-id="410b6-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="410b6-219">Если на виртуальной машине не установлено интегрированное решение по оценке уязвимостей, центр безопасности рекомендует установить его.</span><span class="sxs-lookup"><span data-stu-id="410b6-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="410b6-220">В панели мониторинга ASC hello на hello **рекомендации** колонке выберите **добавления решения оценки уязвимости.**</span><span class="sxs-lookup"><span data-stu-id="410b6-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="410b6-221">Выберите нужное решение для оценки уязвимости hello tooinstall ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="410b6-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="410b6-222">Щелкните **Установить на следующем количестве виртуальных машин: [количество]**.</span><span class="sxs-lookup"><span data-stu-id="410b6-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="410b6-223">Выберите решение партнера в hello Azure Marketplace или в разделе **использовать существующее решение** выберите **Компанию Qualys.**</span><span class="sxs-lookup"><span data-stu-id="410b6-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="410b6-224">Можно включить настройки автоматического обновления hello и отключение hello **решения партнеров** колонку.</span><span class="sxs-lookup"><span data-stu-id="410b6-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="410b6-225">Дополнительную информацию о том, как tooimplement решение для оценки уязвимости, в разделе [оценки уязвимости в центр безопасности Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="410b6-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="410b6-226">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="410b6-226">Next steps</span></span>

- [<span data-ttu-id="410b6-227">Краткое руководство по центру безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="410b6-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="410b6-228">Введение tooAzure центра обеспечения безопасности</span><span class="sxs-lookup"><span data-stu-id="410b6-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="410b6-229">Интеграция оповещений центра безопасности Azure с помощью интеграции журналов Azure</span><span class="sxs-lookup"><span data-stu-id="410b6-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- <span data-ttu-id="410b6-230">[Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/) (Расширение возможностей центра безопасности Azure с помощью интегрированного решения по оценке уязвимостей)</span><span class="sxs-lookup"><span data-stu-id="410b6-230">[Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)</span></span>
