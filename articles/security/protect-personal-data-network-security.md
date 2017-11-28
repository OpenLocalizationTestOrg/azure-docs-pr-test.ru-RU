---
title: "Защита персональных данных с помощью функций безопасности сети Azure | Документация Майкрософт"
description: "Сведения о защите персональных данных с помощью функций безопасности сети Azure."
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
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: b7a6343f37f890b65d9536eac34e1069d24ad97e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a><span data-ttu-id="16778-103">Защита персональных данных с помощью функций безопасности сети Azure: шлюз приложений и группы безопасности сети Azure</span><span class="sxs-lookup"><span data-stu-id="16778-103">Protect personal data with network security features: Azure Application Gateway and Network Security Groups</span></span>

<span data-ttu-id="16778-104">В этой статье представлены сведения и процедуры, которые помогут защитить персональные данные с помощью шлюза приложений и групп безопасности сети Azure.</span><span class="sxs-lookup"><span data-stu-id="16778-104">This article provides information and procedures that will help you use Azure Application Gateway and Network Security Groups to protect personal data.</span></span>

<span data-ttu-id="16778-105">Важный элемент многоуровневой стратегии защиты конфиденциальности персональных данных — это защита от распространенных уязвимостей, таких как атака путем внедрения кода SQL или атака с выполнением межсайтовых сценариев.</span><span class="sxs-lookup"><span data-stu-id="16778-105">An important element in a multi-layered security strategy to protect the privacy of personal data is a defense against common vulnerability exploits such as SQL injection or cross-site scripting.</span></span> <span data-ttu-id="16778-106">Устранение нежелательного сетевого трафика из виртуальной сети Azure помогает защититься от потенциальных нарушений безопасности конфиденциальных данных, а Microsoft Azure предоставляет инструменты защиты данных от злоумышленников.</span><span class="sxs-lookup"><span data-stu-id="16778-106">Keeping unwanted network traffic out of your Azure virtual network helps protect against potential compromise of sensitive data, and Microsoft Azure gives you tools to help protect your data against attackers.</span></span>

## <a name="scenario"></a><span data-ttu-id="16778-107">Сценарий</span><span class="sxs-lookup"><span data-stu-id="16778-107">Scenario</span></span>

<span data-ttu-id="16778-108">Большая круизная компания, расположенная в США, расширяет масштабы своей деятельности и предлагает маршруты в Средиземном, Адриатическом и Балтийском морях, а также на Британских островах.</span><span class="sxs-lookup"><span data-stu-id="16778-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="16778-109">Чтобы реализовать эту возможность, компания приобрела несколько небольших круизных организаций, расположенных в Италии, Германии, Дании и Великобритании.</span><span class="sxs-lookup"><span data-stu-id="16778-109">In furtherance of those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="16778-110">Корпоративные данные компании хранятся в облаке Microsoft Azure, а их обработка и доступ к ним осуществляются с помощью приложений на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="16778-110">The company uses Microsoft Azure to store corporate data in the cloud and run applications on virtual machines that process and access this data.</span></span> <span data-ttu-id="16778-111">К этим данным относятся персональные данные, позволяющие установить личность, например имена, адреса, номера телефонов и данные кредитной карты в глобальной клиентской базе.</span><span class="sxs-lookup"><span data-stu-id="16778-111">This data includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="16778-112">Он также включает традиционные информацию о персонале, например адреса, номера телефонов, идентификационные номера налога и медицинские сведения о сотрудниках компании во всех расположениях.</span><span class="sxs-lookup"><span data-stu-id="16778-112">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="16778-113">Круизная компания также содержит большую базу данных участников программ лояльности и программ скидок, которая, в свою очередь, содержит персональные данные, позволяющие отслеживать связи с текущими и бывшими клиентами.</span><span class="sxs-lookup"><span data-stu-id="16778-113">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="16778-114">Сотрудники компании получают доступ к сети из удаленных филиалов, а туристические агентства, расположенные по всему миру, имеют доступ к отдельным ресурсам, к которым они подключаются через веб-приложения, размещенные на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="16778-114">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources and use web-based applications hosted in Azure VMs to interact with it.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="16778-115">Проблема</span><span class="sxs-lookup"><span data-stu-id="16778-115">Problem statement</span></span>

<span data-ttu-id="16778-116">Компания должна защищать конфиденциальность персональных данных клиентов и сотрудников от злоумышленников, которые используют уязвимости программного обеспечения и выполняют вредоносный код. Все это может нарушать безопасность персональных данных, которые хранятся в облачных приложениях компании или используются ими.</span><span class="sxs-lookup"><span data-stu-id="16778-116">The company must protect the privacy of customers’ and employees’ personal data from attackers who exploit software vulnerabilities to run malicious code that could expose personal data stored or used by the company’s cloud-based applications.</span></span>

## <a name="company-goal"></a><span data-ttu-id="16778-117">Цель компании</span><span class="sxs-lookup"><span data-stu-id="16778-117">Company goal</span></span>

<span data-ttu-id="16778-118">Компания должна гарантировать защиту корпоративных виртуальных сетей Azure от доступа посторонних лиц, а также защиту приложений и данных от распространенных уязвимостей.</span><span class="sxs-lookup"><span data-stu-id="16778-118">The company’s goal to ensure that unauthorized persons cannot access corporate Azure Virtual Networks and the applications and data that reside there by exploiting common vulnerabilities.</span></span> 

## <a name="solutions"></a><span data-ttu-id="16778-119">Решения</span><span class="sxs-lookup"><span data-stu-id="16778-119">Solutions</span></span>

<span data-ttu-id="16778-120">Microsoft Azure предоставляет механизмы безопасности, которые позволяют предотвратить попадание нежелательного трафика в виртуальные сети Azure.</span><span class="sxs-lookup"><span data-stu-id="16778-120">Microsoft Azure provides security mechanisms to help prevent unwanted traffic from entering Azure Virtual Networks.</span></span> <span data-ttu-id="16778-121">Управление исходящим и входящим трафиком обычно осуществляется брандмауэрами.</span><span class="sxs-lookup"><span data-stu-id="16778-121">Control of inbound and outbound traffic is traditionally performed by firewalls.</span></span> <span data-ttu-id="16778-122">В Azure шлюз приложений можно использовать с брандмауэром веб-приложения и группами безопасности сети (NSG), которые действуют как простой распределенный брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="16778-122">In Azure, you can use the Application Gateway with the Web Application Firewall and Network Security Groups (NSG), which act as a simple distributed firewall.</span></span> <span data-ttu-id="16778-123">Эти инструменты позволяют определять и блокировать нежелательный сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="16778-123">These tools enable you to detect and block unwanted network traffic.</span></span>

### <a name="application-gatewayweb-application-firewall"></a><span data-ttu-id="16778-124">Шлюз приложений или брандмауэр веб-приложения</span><span class="sxs-lookup"><span data-stu-id="16778-124">Application Gateway/Web Application Firewall</span></span>

<span data-ttu-id="16778-125">Компонент [брандмауэра веб-приложения](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) [шлюза приложений Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) защищает веб-приложения, на которые часто направлены вредоносные атаки, использующие распространенные уязвимости.</span><span class="sxs-lookup"><span data-stu-id="16778-125">The [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) component of the [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protects web applications, which are increasingly targets of malicious attacks that exploit common known vulnerabilities.</span></span> <span data-ttu-id="16778-126">Централизованный брандмауэр веб-приложения обеспечивает защиту от атак и упрощает управление безопасностью без каких-либо изменений приложения.</span><span class="sxs-lookup"><span data-stu-id="16778-126">A centralized WAF both protects against web attacks and simplifies security management without requiring any application changes.</span></span>

<span data-ttu-id="16778-127">Брандмауэр веб-приложения Azure защищает от различных категорий атак, в том числе атаки путем внедрения кода SQL, атаки с выполнением межсайтовых сценариев, нарушения протокола HTTP, аномалии, боты, программы-обходчики, сканеры, распространенные неправильные настройки приложений, отказ в обслуживании HTTP, а также других распространенных атак, таких как внедрение команд, несанкционированные HTTP-запросы, разделение HTTP-запросов и атаки с включением удаленного файла.</span><span class="sxs-lookup"><span data-stu-id="16778-127">Azure WAF addresses various attack categories including SQL injection, cross site scripting, HTTP protocol violations and anomalies, bots, crawlers, scanners, common application misconfigurations, HTTP Denial of Service, and other common attacks such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attacks.</span></span> 

<span data-ttu-id="16778-128">Вы можете создать шлюз приложений с брандмауэром веб-приложения или добавить его в имеющийся шлюз.</span><span class="sxs-lookup"><span data-stu-id="16778-128">You can create an application gateway with WAF, or add WAF to an existing application gateway.</span></span> <span data-ttu-id="16778-129">В любом случае шлюзу приложений Azure требуется собственная подсеть.</span><span class="sxs-lookup"><span data-stu-id="16778-129">In either case, Azure Application Gateway requires its own subnet.</span></span>

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a><span data-ttu-id="16778-130">Создание шлюза приложений с WAF</span><span class="sxs-lookup"><span data-stu-id="16778-130">How do I create an application gateway with WAF?</span></span> 

<span data-ttu-id="16778-131">Чтобы создать шлюз приложений с включенным WAF, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="16778-131">To create a new application gateway with WAF enabled, do the following:</span></span>

1. <span data-ttu-id="16778-132">Войдите на портал Azure. В области **Избранное** выберите **Создать**</span><span class="sxs-lookup"><span data-stu-id="16778-132">Log in to the Azure portal and in the **Favorites** pane of the portal, click **New**</span></span>

2. <span data-ttu-id="16778-133">В колонке **Создать** щелкните **Сети**.</span><span class="sxs-lookup"><span data-stu-id="16778-133">In the **New** blade, click **Networking**.</span></span>

3. <span data-ttu-id="16778-134">Щелкните **Шлюз приложений**.</span><span class="sxs-lookup"><span data-stu-id="16778-134">Click **Application Gateway**.</span></span>

4. <span data-ttu-id="16778-135">Перейдите на портал Azure и выберите **Создать \> Сети \> Шлюз приложений**.</span><span class="sxs-lookup"><span data-stu-id="16778-135">Navigate to the Azure portal, **click New \> Networking \> Application Gateway.**</span></span>

   ![Создание шлюзов приложений](media/protect-netsec/app-gateway-01.png)

5. <span data-ttu-id="16778-137">В открывшейся колонке **Основные сведения** введите значения для следующих полей: "Имя", "Уровень" (стандартный или WAF), "Размер номера SKU" (маленький, средний или большой), "Число экземпляров" (2 для высокой доступности), "Подписка", "Группа ресурсов" и "Расположение".</span><span class="sxs-lookup"><span data-stu-id="16778-137">In the **Basics** blade that appears, enter the values for the following fields: Name, Tier (Standard or WAF), SKU size (Small, Medium, or Large),  Instance count (2 for high availability), Subscription, Resource group, and Location.</span></span>

6. <span data-ttu-id="16778-138">В колонке **Параметры**, которая отображается под областью **Виртуальная сеть**, щелкните **Выберите виртуальную сеть**.</span><span class="sxs-lookup"><span data-stu-id="16778-138">In the **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="16778-139">Откроется колонка "Выбрать виртуальную сеть".</span><span class="sxs-lookup"><span data-stu-id="16778-139">This step opens enter the Choose virtual network blade.</span></span>

7. <span data-ttu-id="16778-140">Щелкните **Создать**, чтобы открыть колонку **Создание виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="16778-140">Click **Create new** to open the **Create virtual network** blade.</span></span>

8. <span data-ttu-id="16778-141">Введите следующие значения: "Имя", "Пространство адресов", "Имя подсети", "Диапазон адресов подсети".</span><span class="sxs-lookup"><span data-stu-id="16778-141">Enter the following values: Name, Address space, Subnet name, Subnet address range.</span></span> <span data-ttu-id="16778-142">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="16778-142">Click **OK**.</span></span>

9. <span data-ttu-id="16778-143">В колонке **Параметры** в разделе **Интерфейсная IP-конфигурация** выберите тип IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="16778-143">On the **Settings** blade under **Frontend IP configuration**, choose the IP address type.</span></span>

10. <span data-ttu-id="16778-144">Щелкните **Выберите общедоступный IP-адрес**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="16778-144">Click **Choose a public IP address,** then **Create new.**</span></span>

11. <span data-ttu-id="16778-145">Примите значение по умолчанию и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="16778-145">Accept the default value, and click **OK.**</span></span>

12. <span data-ttu-id="16778-146">В колонке **Параметры** в разделе **Конфигурация прослушивателя** для параметра **Протокол** установите значение HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="16778-146">On the **Settings** blade under **Listener configuration**, select to use HTTP or HTTPS under **Protocol**.</span></span> <span data-ttu-id="16778-147">Чтобы использовать HTTPS, требуется сертификат.</span><span class="sxs-lookup"><span data-stu-id="16778-147">To use HTTPS, a certificate is required.</span></span>

13. <span data-ttu-id="16778-148">Настройте определенные параметры WAF: **Состояние брандмауэра** (**Включено**) и **Режим брандмауэра** (**Предотвращение**).</span><span class="sxs-lookup"><span data-stu-id="16778-148">Configure the WAF specific settings: **Firewall status** (**Enabled**) and **Firewall mode** (**Prevention**).</span></span> <span data-ttu-id="16778-149">При выборе режима **Обнаружение** записывается только трафик.</span><span class="sxs-lookup"><span data-stu-id="16778-149">If you choose **Detection** as the mode, traffic is only logged.</span></span>

14. <span data-ttu-id="16778-150">Просмотрите страницу **сводки** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="16778-150">Review the **Summary** page and click **OK**.</span></span> <span data-ttu-id="16778-151">Теперь шлюз приложений поставлен в очередь и создан.</span><span class="sxs-lookup"><span data-stu-id="16778-151">Now the application gateway is queued up and created.</span></span>

<span data-ttu-id="16778-152">После создания шлюза приложений перейдите к нему на портале, чтобы продолжить его настройку.</span><span class="sxs-lookup"><span data-stu-id="16778-152">After the application gateway has been created, you can navigate to it in the portal and continue configuration of the application gateway.</span></span>

![Созданный шлюз приложений](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-to-an-existing-application"></a><span data-ttu-id="16778-154">Добавление WAF в имеющееся приложение</span><span class="sxs-lookup"><span data-stu-id="16778-154">How do I add WAF to an existing application?</span></span>

<span data-ttu-id="16778-155">Чтобы реализовать поддержку WAF в режиме предотвращения в имеющемся шлюзе приложений, выполните такие действия:</span><span class="sxs-lookup"><span data-stu-id="16778-155">To update an existing application gateway to support WAF in prevention mode, do the following:</span></span>

1. <span data-ttu-id="16778-156">На портале Azure в области **Избранное** щелкните **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="16778-156">In the Azure portal **Favorites** pane, click **All resources**.</span></span>

2. <span data-ttu-id="16778-157">Выберите существующий шлюз приложений в колонке **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="16778-157">Click the existing Application Gateway in the **All resources** blade.</span></span> 
>[!NOTE]
<span data-ttu-id="16778-158">Примечание. Если выбранная подписка имеет несколько ресурсов, в поле "Фильтровать по имени..." введите имя,</span><span class="sxs-lookup"><span data-stu-id="16778-158">Note: If the subscription you selected already has several resources in it, you can enter the name in the Filter by name…</span></span> <span data-ttu-id="16778-159">чтобы быстро получить доступ к необходимой зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="16778-159">box to easily access the DNS zone.</span></span>
3. <span data-ttu-id="16778-160">Щелкните **Брандмауэр веб-приложения** и обновите параметры шлюза приложений: **Обновление до уровня WAF** ("проверено"), **Состояние брандмауэра** ("включено"), **Режим брандмауэра** ("Предотвращение").</span><span class="sxs-lookup"><span data-stu-id="16778-160">Click **Web application firewall** and update the application gateway settings: **Upgrade to WAF Tier** (checked), **Firewall status** (enabled),     **Firewall mode** (Prevention).</span></span> <span data-ttu-id="16778-161">Необходимо также настроить набор правил и отключенные правила.</span><span class="sxs-lookup"><span data-stu-id="16778-161">You also need to configure the rule set, and configure disabled rules.</span></span>

<span data-ttu-id="16778-162">Дополнительные сведения о создании шлюза приложений с WAF и добавлении WAF в имеющийся шлюз приложений см. в статье [Создание шлюза приложений с брандмауэром веб-приложения с помощью портала](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal).</span><span class="sxs-lookup"><span data-stu-id="16778-162">For more detailed information on how to create a new application gateway with WAF and how to add WAF to an existing application gateway, see [Create an application gateway with web application firewall by using the portal.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="16778-163">группы сетевой безопасности;</span><span class="sxs-lookup"><span data-stu-id="16778-163">Network Security Groups</span></span>

<span data-ttu-id="16778-164">[Группы безопасности сети](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) содержат перечень правил безопасности, которые разрешают или запрещают передачу сетевого трафика к ресурсам, подключенным к [виртуальным сетям Azure](https://docs.microsoft.com/azure/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="16778-164">A [network security group](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contains a list of security rules that allow or deny network traffic to resources connected to [Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span></span> <span data-ttu-id="16778-165">Их можно связать с подсетями или отдельными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="16778-165">NSGs can be associated to subnets or individual VMs.</span></span> <span data-ttu-id="16778-166">Если группа безопасности сети связана с подсетью, эти правила применяются ко всем ресурсам в подсети.</span><span class="sxs-lookup"><span data-stu-id="16778-166">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> <span data-ttu-id="16778-167">Кроме того, трафик можно ограничить, связав группу безопасности сети с отдельной виртуальной машиной или сетевым интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="16778-167">Traffic can further be restricted by also associating an NSG to a VM or NIC.</span></span>

<span data-ttu-id="16778-168">Группы безопасности сети содержат четыре свойства: "Имя", "Область", "Группа ресурсов" и "Правила".</span><span class="sxs-lookup"><span data-stu-id="16778-168">NSGs contain four properties: Name, Region, Resource group, and Rules.</span></span>
>[!Note]
<span data-ttu-id="16778-169">Несмотря на то что группа NSG входит в определенную группу ресурсов, ее можно связать с ресурсами в любой другой группе при условии, что ресурс находится в одном регионе Azure с группой NSG.</span><span class="sxs-lookup"><span data-stu-id="16778-169">Although an NSG exists in a resource group, it can be associated to resources in any resource group, as long as the resource is part of the same Azure region as the NSG.</span></span>

<span data-ttu-id="16778-170">Правила NSG содержат девять свойств: "Имя", "Протокол" (TCP, UDP или \*, которые включают ICMP а также UDP и TCP), "Диапазон исходных портов", "Диапазон портов назначения", Source address prefix (Префикс адреса источника), Destination address prefix (Префикс адреса назначения), "Направление" (входящие или исходящие), "Приоритет" (между 100 и 4096) и "Тип доступа" (разрешить или запретить).</span><span class="sxs-lookup"><span data-stu-id="16778-170">NSG rules contain nine properties: Name, Protocol (TCP, UDP, or \*, which includes ICMP as well as UDP and TCP), Source port range, Destination port range, Source address prefix, Destination address prefix, Direction (inbound or outbound), Priority (between 100 and 4096) and Access type (allow or deny).</span></span> <span data-ttu-id="16778-171">Все группы безопасности сети содержат набор правил по умолчанию, который можно удалить или переопределить с помощью созданных правил.</span><span class="sxs-lookup"><span data-stu-id="16778-171">All NSGs contain a set of default rules that can be deleted, or overridden by the rules you create.</span></span>

#### <a name="how-do-i-implement-nsgs"></a><span data-ttu-id="16778-172">Реализация групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="16778-172">How do I implement NSGs?</span></span>

<span data-ttu-id="16778-173">Реализация NSG требует тщательного планирования. При этом необходимо принимать во внимание несколько аспектов.</span><span class="sxs-lookup"><span data-stu-id="16778-173">Implementing NSGs requires planning, and there are several design considerations you need to take into account.</span></span> <span data-ttu-id="16778-174">К ним относятся ограничение числа NSG на подписку и правил на подписки; проектирование подсетей и виртуальных сетей, специальные правила, трафик ICMP, изоляция уровней с помощью подсетей, подсистемы балансировки нагрузки и многое другое.</span><span class="sxs-lookup"><span data-stu-id="16778-174">These include limits on the number of NSGs per subscription and rules per NSG; VNet and subnet design, special rules, ICMP traffic, isolation of tiers with subnets, load balancers, and more.</span></span>

<span data-ttu-id="16778-175">Дополнительные сведения о планировании и реализации NSG, а также примеры сценариев развертывания см. в статье [Фильтрация сетевого трафика с помощью групп безопасности сети](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).</span><span class="sxs-lookup"><span data-stu-id="16778-175">For more guidance in planning and implementing NSGs, and a sample deployment scenario, see [Filter network traffic with network security groups.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)</span></span>

#### <a name="how-do-i-create-rules-in-an-nsg"></a><span data-ttu-id="16778-176">Создание правила NSG</span><span class="sxs-lookup"><span data-stu-id="16778-176">How do I create rules in an NSG?</span></span>

<span data-ttu-id="16778-177">Чтобы создать правила для входящего трафика в имеющейся группе безопасности сети, выполните такие действия:</span><span class="sxs-lookup"><span data-stu-id="16778-177">To create inbound rules in an existing NSG, do the following:</span></span>

1. <span data-ttu-id="16778-178">Щелкните **Обзор**, а затем выберите **Группы безопасности сети**.</span><span class="sxs-lookup"><span data-stu-id="16778-178">Click **Browse**, and then **Network security groups**.</span></span>

2. <span data-ttu-id="16778-179">В списке групп безопасности сети выберите **NSG-FrontEnd**, а затем щелкните **Правила безопасности для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="16778-179">In the list of NSGs, click **NSG-FrontEnd**, and then **Inbound security rules.**</span></span>

3. <span data-ttu-id="16778-180">В списке правил безопасности для входящего трафика щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="16778-180">In the list of Inbound security rules, click **Add.**</span></span>

4. <span data-ttu-id="16778-181">Введите значения в следующие поля: "Имя", "Приоритет", "Источник", "Протокол", "Исходный диапазон", "Назначения", "Диапазон портов назначения" и "Действие".</span><span class="sxs-lookup"><span data-stu-id="16778-181">Enter the values in the following fields: Name, Priority, Source, Protocol, Source range, Destination, Destination port range, and Action.</span></span>

<span data-ttu-id="16778-182">Через несколько секунд в NGS появится новое правило.</span><span class="sxs-lookup"><span data-stu-id="16778-182">The new rule will appear in the NSG after a few seconds.</span></span>

![Правила безопасности сети](media/protect-netsec/inbound-security.png)

<span data-ttu-id="16778-184">Дополнительные сведения о создании NGS в подсетях, правил и связывании NGS с интерфейсными и внутренними подсетями см. в статье [Создание групп безопасности сети с помощью портала Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal).</span><span class="sxs-lookup"><span data-stu-id="16778-184">For more instructions on how to create NSGs in subnets, create rules, and associate an NSG with a front-end and back-end subnet, see [Create network security groups using the Azure portal.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span></span>

## <a name="next-steps"></a><span data-ttu-id="16778-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16778-185">Next steps</span></span>

[<span data-ttu-id="16778-186">Сетевая безопасность Azure</span><span class="sxs-lookup"><span data-stu-id="16778-186">Azure Network Security</span></span>](https://azure.microsoft.com/blog/azure-network-security/)

[<span data-ttu-id="16778-187">Рекомендации по обеспечению безопасности в сети Azure</span><span class="sxs-lookup"><span data-stu-id="16778-187">Azure Network Security Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[<span data-ttu-id="16778-188">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="16778-188">Get information about a network security group</span></span>](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[<span data-ttu-id="16778-189">Брандмауэр веб-приложения (WAF)</span><span class="sxs-lookup"><span data-stu-id="16778-189">Web application firewall (WAF)</span></span>](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
