---
title: "Настройка политики IPsec/IKE для VPN-подключений типа \"сеть — сеть\" или \"виртуальная сеть — виртуальная сеть\". Azure Resource Manager: PowerShell | Документация Майкрософт"
description: "В этой статье описана настройка политики IPsec/IKE для подключений типа \"сеть — сеть\" или \"виртуальная сеть — виртуальная сеть\" с VPN-шлюзами Azure с помощью Azure Resource Manager и PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="35e6b-103">Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="35e6b-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="35e6b-104">В этой статье рассматриваются tooconfigure hello действия политики IPsec/IKE для соединений через виртуальную Частную сеть для или виртуальной сети для виртуальной сети, с помощью модели развертывания диспетчера ресурсов hello и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="35e6b-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="35e6b-105"><a name="about"></a>Параметры политики IPsec и IKE для VPN-шлюзов Azure</span><span class="sxs-lookup"><span data-stu-id="35e6b-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="35e6b-106">Стандарт протоколов IPsec и IKE поддерживает широкий набор алгоритмов шифрования в различных сочетаниях.</span><span class="sxs-lookup"><span data-stu-id="35e6b-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="35e6b-107">См. слишком[о требованиях шифрования и VPN-шлюзы Azure](vpn-gateway-about-compliance-crypto.md) toosee, как это может помочь, обеспечивая между организациями и подключения к виртуальной сети для виртуальной сети удовлетворяют требованиям соответствия и безопасности.</span><span class="sxs-lookup"><span data-stu-id="35e6b-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="35e6b-108">В этой статье предоставляет toocreate инструкции и настроить политику IPsec/IKE и применить tooa существующего или нового соединения.</span><span class="sxs-lookup"><span data-stu-id="35e6b-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="35e6b-109">Часть 1 - toocreate рабочего процесса и задать политику IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="35e6b-110">Часть 2. Поддерживаемые алгоритмы шифрования и уровни стойкости ключей</span><span class="sxs-lookup"><span data-stu-id="35e6b-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="35e6b-111">Часть 3. Создание нового подключения VPN типа "сеть — сеть" с помощью политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="35e6b-112">Часть 4. Создание нового подключения VPN типа "виртуальная сеть — виртуальная сеть" с помощью политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="35e6b-113">Часть 5. Управление политикой IPsec/IKE (а также ее создание, добавление и удаление) для подключения</span><span class="sxs-lookup"><span data-stu-id="35e6b-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="35e6b-114">Обратите внимание, что политики IPsec/IKE работает только на hello, следуя SKU шлюза.</span><span class="sxs-lookup"><span data-stu-id="35e6b-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="35e6b-115">***VpnGw1, VpnGw2, VpnGw3*** (на основе маршрутов);</span><span class="sxs-lookup"><span data-stu-id="35e6b-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="35e6b-116">***Standard*** и ***HighPerformance*** (на основе маршрутов).</span><span class="sxs-lookup"><span data-stu-id="35e6b-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="35e6b-117">Можно указать только ***одну*** комбинацию политик для каждого подключения.</span><span class="sxs-lookup"><span data-stu-id="35e6b-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="35e6b-118">Вам следует указать все алгоритмы и параметры для IKE (основной режим) и IPsec (быстрый режим).</span><span class="sxs-lookup"><span data-stu-id="35e6b-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="35e6b-119">Указать частичную политику нельзя.</span><span class="sxs-lookup"><span data-stu-id="35e6b-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="35e6b-120">Обратитесь к спецификации поставщиков устройств VPN политики tooensure hello поддерживается на устройствах VPN локальной.</span><span class="sxs-lookup"><span data-stu-id="35e6b-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="35e6b-121">S2S или подключения к виртуальной сети для виртуальной сети не удается установить, если политики hello несовместимы.</span><span class="sxs-lookup"><span data-stu-id="35e6b-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="35e6b-122"><a name ="workflow"></a>Часть 1 - toocreate рабочего процесса и задать политику IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="35e6b-123">В этом разделе представлен краткий обзор hello политики рабочих процессов toocreate и обновление IPsec/IKE для подключения S2S VPN или виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="35e6b-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="35e6b-124">Создание виртуальной сети и VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="35e6b-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="35e6b-125">Создание шлюза локальной сети для локального подключения или другой виртуальной сети и шлюза для подключения типа "виртуальная сеть — виртуальная сеть".</span><span class="sxs-lookup"><span data-stu-id="35e6b-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="35e6b-126">Создание политики IPsec/IKE с выбранными алгоритмами и параметрами.</span><span class="sxs-lookup"><span data-stu-id="35e6b-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="35e6b-127">Создайте соединение (IPsec или VNet2VNet) с помощью политики IPsec/IKE hello</span><span class="sxs-lookup"><span data-stu-id="35e6b-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="35e6b-128">Добавление, обновление и удаление политики IPsec/IKE для существующего подключения.</span><span class="sxs-lookup"><span data-stu-id="35e6b-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="35e6b-129">инструкции Hello в этой статье поможет вам установить и настроить политики IPsec/IKE, как показано на диаграмме hello:</span><span class="sxs-lookup"><span data-stu-id="35e6b-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="35e6b-131"><a name ="params"></a>Часть 2. Поддерживаемые алгоритмы шифрования и уровни стойкости ключей</span><span class="sxs-lookup"><span data-stu-id="35e6b-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="35e6b-132">Hello следующей таблице перечислены hello поддерживается алгоритмов шифрования и значений длины ключа можно настроить hello клиентами.</span><span class="sxs-lookup"><span data-stu-id="35e6b-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="35e6b-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="35e6b-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="35e6b-134">**Варианты**</span><span class="sxs-lookup"><span data-stu-id="35e6b-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="35e6b-135">Шифрование IKEv2</span><span class="sxs-lookup"><span data-stu-id="35e6b-135">IKEv2 Encryption</span></span> | <span data-ttu-id="35e6b-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="35e6b-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="35e6b-137">Проверка целостности IKEv2</span><span class="sxs-lookup"><span data-stu-id="35e6b-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="35e6b-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="35e6b-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="35e6b-139">Группа DH</span><span class="sxs-lookup"><span data-stu-id="35e6b-139">DH Group</span></span>         | <span data-ttu-id="35e6b-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, нет</span><span class="sxs-lookup"><span data-stu-id="35e6b-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="35e6b-141">Шифрование IPsec</span><span class="sxs-lookup"><span data-stu-id="35e6b-141">IPsec Encryption</span></span> | <span data-ttu-id="35e6b-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, нет</span><span class="sxs-lookup"><span data-stu-id="35e6b-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="35e6b-143">Целостность IPsec</span><span class="sxs-lookup"><span data-stu-id="35e6b-143">IPsec Integrity</span></span>  | <span data-ttu-id="35e6b-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="35e6b-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="35e6b-145">Группа PFS</span><span class="sxs-lookup"><span data-stu-id="35e6b-145">PFS Group</span></span>        | <span data-ttu-id="35e6b-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, нет</span><span class="sxs-lookup"><span data-stu-id="35e6b-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="35e6b-147">Время существования QM SA</span><span class="sxs-lookup"><span data-stu-id="35e6b-147">QM SA Lifetime</span></span>   | <span data-ttu-id="35e6b-148">(**Необязательно** — используются значения по умолчанию, если не заданы другие значения.)</span><span class="sxs-lookup"><span data-stu-id="35e6b-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="35e6b-149">Секунды (целое число, **минимум 300**, по умолчанию — 27 000 с)</span><span class="sxs-lookup"><span data-stu-id="35e6b-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="35e6b-150">Килобайты (целое число, **минимум 1024**, по умолчанию — 102 400 000 КБ)</span><span class="sxs-lookup"><span data-stu-id="35e6b-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="35e6b-151">Селектор трафика</span><span class="sxs-lookup"><span data-stu-id="35e6b-151">Traffic Selector</span></span> | <span data-ttu-id="35e6b-152">UsePolicyBasedTrafficSelectors** ($True/$False; **необязательно** — по умолчанию используется значение $False, если не задано другое значение.)</span><span class="sxs-lookup"><span data-stu-id="35e6b-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="35e6b-153">**Если GCMAES используется как для алгоритма шифрования IPsec, необходимо выбрать hello того же алгоритма GCMAES и длину ключа для проверки целостности IPsec; Например с помощью GCMAES128 для обоих**</span><span class="sxs-lookup"><span data-stu-id="35e6b-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="35e6b-154">Время существования сопоставления безопасности основного режима IKEv2 имеет фиксированный размер 28800 секунд на шлюзах Azure VPN hello</span><span class="sxs-lookup"><span data-stu-id="35e6b-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="35e6b-155">Параметр «UsePolicyBasedTrafficSelectors» слишком $ значение True, если соединение будет настраивать hello Azure VPN шлюза tooconnect toopolicy VPN брандмауэр на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="35e6b-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="35e6b-156">При включении PolicyBasedTrafficSelectors необходимо tooensure устройство VPN имеет соответствующий трафик селекторы hello определенных все сочетания свои префиксы (шлюз локальной сети) в локальной сети из префиксов hello виртуальной сети Azure, Вместо any к any.</span><span class="sxs-lookup"><span data-stu-id="35e6b-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="35e6b-157">Например при свои префиксы в локальной сети, 10.1.0.0/16 и 10.2.0.0/16 и префиксы вашей виртуальной сети: 192.168.0.0/16 и 172.16.0.0/16, необходимо toospecify hello, следуя селекторы трафика:</span><span class="sxs-lookup"><span data-stu-id="35e6b-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="35e6b-158">10.1.0.0/16 <====> 192.168.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="35e6b-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="35e6b-159">10.1.0.0/16 <====> 172.16.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="35e6b-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="35e6b-160">10.2.0.0/16 <====> 192.168.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="35e6b-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="35e6b-161">10.2.0.0/16 <====> 172.16.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="35e6b-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="35e6b-162">Дополнительные сведения о селекторах трафика на основе политик см. в статье [Подключение VPN-шлюзов Azure к нескольким локальным VPN-устройствам на основе политики с помощью PowerShell](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="35e6b-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="35e6b-163">Привет, в следующей таблице перечислены hello соответствующие группы Диффи-Хелмана, поддерживаемых hello пользовательской политики:</span><span class="sxs-lookup"><span data-stu-id="35e6b-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="35e6b-164">**Группа Диффи-Хелмана**</span><span class="sxs-lookup"><span data-stu-id="35e6b-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="35e6b-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="35e6b-165">**DHGroup**</span></span>              | <span data-ttu-id="35e6b-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="35e6b-166">**PFSGroup**</span></span> | <span data-ttu-id="35e6b-167">**Длина ключа**</span><span class="sxs-lookup"><span data-stu-id="35e6b-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="35e6b-168">1</span><span class="sxs-lookup"><span data-stu-id="35e6b-168">1</span></span>                         | <span data-ttu-id="35e6b-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="35e6b-169">DHGroup1</span></span>                 | <span data-ttu-id="35e6b-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="35e6b-170">PFS1</span></span>         | <span data-ttu-id="35e6b-171">MODP (768 бит)</span><span class="sxs-lookup"><span data-stu-id="35e6b-171">768-bit MODP</span></span>   |
| <span data-ttu-id="35e6b-172">2</span><span class="sxs-lookup"><span data-stu-id="35e6b-172">2</span></span>                         | <span data-ttu-id="35e6b-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="35e6b-173">DHGroup2</span></span>                 | <span data-ttu-id="35e6b-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="35e6b-174">PFS2</span></span>         | <span data-ttu-id="35e6b-175">MODP (1024 бит)</span><span class="sxs-lookup"><span data-stu-id="35e6b-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="35e6b-176">14</span><span class="sxs-lookup"><span data-stu-id="35e6b-176">14</span></span>                        | <span data-ttu-id="35e6b-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="35e6b-177">DHGroup14</span></span><br><span data-ttu-id="35e6b-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="35e6b-178">DHGroup2048</span></span> | <span data-ttu-id="35e6b-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="35e6b-179">PFS2048</span></span>      | <span data-ttu-id="35e6b-180">MODP (2048 бит)</span><span class="sxs-lookup"><span data-stu-id="35e6b-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="35e6b-181">19</span><span class="sxs-lookup"><span data-stu-id="35e6b-181">19</span></span>                        | <span data-ttu-id="35e6b-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="35e6b-182">ECP256</span></span>                   | <span data-ttu-id="35e6b-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="35e6b-183">ECP256</span></span>       | <span data-ttu-id="35e6b-184">ECP (256 бит)</span><span class="sxs-lookup"><span data-stu-id="35e6b-184">256-bit ECP</span></span>    |
| <span data-ttu-id="35e6b-185">20</span><span class="sxs-lookup"><span data-stu-id="35e6b-185">20</span></span>                        | <span data-ttu-id="35e6b-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="35e6b-186">ECP384</span></span>                   | <span data-ttu-id="35e6b-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="35e6b-187">ECP284</span></span>       | <span data-ttu-id="35e6b-188">ECP (384 бит)</span><span class="sxs-lookup"><span data-stu-id="35e6b-188">384-bit ECP</span></span>    |
| <span data-ttu-id="35e6b-189">24</span><span class="sxs-lookup"><span data-stu-id="35e6b-189">24</span></span>                        | <span data-ttu-id="35e6b-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="35e6b-190">DHGroup24</span></span>                | <span data-ttu-id="35e6b-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="35e6b-191">PFS24</span></span>        | <span data-ttu-id="35e6b-192">MODP (2048 бит)</span><span class="sxs-lookup"><span data-stu-id="35e6b-192">2048-bit MODP</span></span>  |

<span data-ttu-id="35e6b-193">См. слишком[RFC3526](https://tools.ietf.org/html/rfc3526) и [RFC5114](https://tools.ietf.org/html/rfc5114) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="35e6b-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="35e6b-194"><a name ="crossprem"></a>Часть 3. Создание нового подключения VPN типа "сеть — сеть" с помощью политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="35e6b-195">В этом разделе содержится описание этапов hello создания с помощью политик IPsec/IKE S2S VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="35e6b-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="35e6b-196">Hello описанной ниже процедуре создается подключение hello согласно схеме hello:</span><span class="sxs-lookup"><span data-stu-id="35e6b-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="35e6b-198">Пошаговые инструкции по созданию VPN-подключения типа "сеть — сеть" см. в статье [Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="35e6b-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="35e6b-199"><a name="before"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="35e6b-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="35e6b-200">Убедитесь в том, что у вас уже есть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="35e6b-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="35e6b-201">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35e6b-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="35e6b-202">Установите командлеты PowerShell диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="35e6b-203">В разделе [Обзор Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="35e6b-204"><a name="createvnet1"></a>Шаг 1 — Создание hello виртуальной сети, шлюз виртуальной частной сети и шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="35e6b-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="35e6b-205">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="35e6b-205">1. Declare your variables</span></span>

<span data-ttu-id="35e6b-206">В этом упражнении мы начнем с объявления переменных.</span><span class="sxs-lookup"><span data-stu-id="35e6b-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="35e6b-207">Быть убедиться, что значения hello tooreplace собственными при настройке для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="35e6b-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="35e6b-208">2. Подключить tooyour подписки и создать новую группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="35e6b-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="35e6b-209">Убедитесь, что переключение tooPowerShell режим toouse hello командлеты диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="35e6b-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="35e6b-210">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="35e6b-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="35e6b-211">Откройте консоль PowerShell и подключить tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="35e6b-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="35e6b-212">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="35e6b-213">3. Создание виртуальной сети hello, шлюза VPN и шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="35e6b-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="35e6b-214">Следующий образец Hello создает виртуальную сеть hello, TestVNet1, три подсети и шлюз VPN hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="35e6b-215">При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="35e6b-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="35e6b-216">Если вы используете другое имя, создание шлюза завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="35e6b-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="35e6b-217"><a name="s2sconnection"></a>Шаг 2. Создание VPN-подключения типа "сеть — сеть" с помощью политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="35e6b-218">1. Создайте политику IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="35e6b-219">Следующий пример скрипта Hello создает политику IPsec/IKE с hello следующие алгоритмы и параметры:</span><span class="sxs-lookup"><span data-stu-id="35e6b-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="35e6b-220">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="35e6b-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="35e6b-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span><span class="sxs-lookup"><span data-stu-id="35e6b-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="35e6b-222">Если вы используете GCMAES для IPsec, необходимо использовать hello того же алгоритма GCMAES и длину ключа для шифрования IPsec и целостности данных, например:</span><span class="sxs-lookup"><span data-stu-id="35e6b-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="35e6b-223">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="35e6b-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="35e6b-224">IPsec: **GCMAES256, GCMAES256**, PFS24, время существования SA (7200 секунд), 2048 КБ</span><span class="sxs-lookup"><span data-stu-id="35e6b-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="35e6b-225">2. Создание hello S2S VPN-подключения с hello политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="35e6b-226">Подключение к S2S VPN создавать и применять политики IPsec/IKE hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="35e6b-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="35e6b-227">При необходимости можно добавить «-UsePolicyBasedTrafficSelectors $True» toohello создать подключение командлет tooenable Azure VPN шлюза tooconnect основе toopolicy VPN-устройства на локальном компьютере, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="35e6b-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="35e6b-228">После политику IPsec/IKE для подключения, hello VPN-шлюз Azure только отправить или принять предложение hello IPsec/IKE с указанным алгоритмов шифрования и значений длины ключа для этого конкретного соединения.</span><span class="sxs-lookup"><span data-stu-id="35e6b-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="35e6b-229">Убедитесь, что устройство VPN локальной для соединения hello использует или принимает сочетание hello точное политики, в противном случае не устанавливает туннель S2S VPN hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="35e6b-230"><a name ="vnet2vnet"></a>Часть 4. Создание нового подключения VPN типа "виртуальная сеть — виртуальная сеть" с помощью политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="35e6b-231">Hello шаги создания подключения виртуальной сети для виртуальной сети с помощью политик IPsec/IKE, аналогичные toothat S2S VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="35e6b-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="35e6b-232">Hello следующие примеры сценариев создайте hello подключение как показано на диаграмме hello:</span><span class="sxs-lookup"><span data-stu-id="35e6b-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="35e6b-234">Подробные инструкции по созданию подключения типа "виртуальная сеть — виртуальная сеть" см. в статье [Настройка подключения VPN-шлюза между виртуальными сетями с помощью PowerShell](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="35e6b-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="35e6b-235">Необходимо выполнить [часть 3](#crossprem) toocreate hello шлюза VPN и настроите TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="35e6b-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="35e6b-236"><a name="createvnet2"></a>Шаг 1 — Создание hello второй виртуальной сети и шлюза VPN</span><span class="sxs-lookup"><span data-stu-id="35e6b-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="35e6b-237">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="35e6b-237">1. Declare your variables</span></span>

<span data-ttu-id="35e6b-238">Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="35e6b-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="35e6b-239">2. Создание hello второй виртуальной сети и шлюза VPN в новую группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="35e6b-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="35e6b-240">Шаг 2 — Создание виртуальной сети toVNet соединение со hello политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="35e6b-241">Аналогичные toohello S2S VPN-подключения, создайте политику IPsec/IKE, а затем применить toopolicy toohello новое соединение.</span><span class="sxs-lookup"><span data-stu-id="35e6b-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="35e6b-242">1. Создайте политику IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="35e6b-243">Следующий пример скрипта Hello создает различные политики IPsec/IKE с hello следующие алгоритмы и параметры:</span><span class="sxs-lookup"><span data-stu-id="35e6b-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="35e6b-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="35e6b-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="35e6b-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span><span class="sxs-lookup"><span data-stu-id="35e6b-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="35e6b-246">2. Создание подключения к виртуальной сети для виртуальной сети с hello политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="35e6b-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="35e6b-247">Создание подключения VNet-VNet и применение hello созданной вами политикой IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="35e6b-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="35e6b-248">В этом примере обоих шлюзов находятся в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="35e6b-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="35e6b-249">Поэтому его невозможно toocreate и настроить оба соединения с hello же политики IPsec/IKE в hello одного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="35e6b-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="35e6b-250">После политику IPsec/IKE для подключения, hello VPN-шлюз Azure только отправить или принять предложение hello IPsec/IKE с указанным алгоритмов шифрования и значений длины ключа для этого конкретного соединения.</span><span class="sxs-lookup"><span data-stu-id="35e6b-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="35e6b-251">Убедитесь, что hello политики IPsec для оба соединения являются hello совпадают, в противном случае не будет установить подключение виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="35e6b-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="35e6b-252">После выполнения этих действий, hello подключения через несколько минут, и вы получите следующие топологии сети, как показано в начале hello hello:</span><span class="sxs-lookup"><span data-stu-id="35e6b-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="35e6b-254"><a name ="managepolicy"></a>Часть 5. Обновление политики IPsec/IKE для подключения</span><span class="sxs-lookup"><span data-stu-id="35e6b-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="35e6b-255">Hello последнего раздела показано, как toomanage политики IPsec/IKE для существующего подключения S2S или виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="35e6b-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="35e6b-256">Упражнение Hello ниже руководстве hello после операции подключения.</span><span class="sxs-lookup"><span data-stu-id="35e6b-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="35e6b-257">Показать политики IPsec/IKE hello соединения</span><span class="sxs-lookup"><span data-stu-id="35e6b-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="35e6b-258">Добавление или обновление подключения tooa политики IPsec/IKE hello</span><span class="sxs-lookup"><span data-stu-id="35e6b-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="35e6b-259">Удалить политику IPsec/IKE hello подключения</span><span class="sxs-lookup"><span data-stu-id="35e6b-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="35e6b-260">Hello же действия относятся tooboth S2S и подключения к виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="35e6b-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="35e6b-261">Политика IPsec/IKE поддерживается только для *стандартных* и *высокопроизводительных* VPN-шлюзов на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="35e6b-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="35e6b-262">Он не поддерживает hello базовый номер SKU шлюза или шлюза VPN на основе политики hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="35e6b-263">1. Показать политики IPsec/IKE hello соединения</span><span class="sxs-lookup"><span data-stu-id="35e6b-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="35e6b-264">Hello в следующем примере показано, как tooget hello политика IPsec/IKE на соединение.</span><span class="sxs-lookup"><span data-stu-id="35e6b-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="35e6b-265">сценарии Hello также продолжить из упражнения hello выше.</span><span class="sxs-lookup"><span data-stu-id="35e6b-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="35e6b-266">Последняя команда Hello список hello настроен для подключения hello текущую политику IPsec/IKE, если оно назначено.</span><span class="sxs-lookup"><span data-stu-id="35e6b-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="35e6b-267">Следующий пример выходных данных Hello предназначен для hello подключения:</span><span class="sxs-lookup"><span data-stu-id="35e6b-267">hello following sample output is for hello connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="35e6b-268">В случае без настроенной политики IPsec/IKE hello команды (PS > $connection6.policy) возвращает пустой возврата.</span><span class="sxs-lookup"><span data-stu-id="35e6b-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="35e6b-269">Это не означает IPsec/IKE не настроена на подключение hello, но это не настраиваемой политики IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="35e6b-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="35e6b-270">Hello фактическое соединение использует политику по умолчанию hello согласовывается между локальным устройством VPN и VPN-шлюз Azure hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="35e6b-271">2. Добавление или обновление политики IPsec/IKE для подключения</span><span class="sxs-lookup"><span data-stu-id="35e6b-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="35e6b-272">Hello шаги tooadd новой политики или обновление существующей политики на подключение, hello же: создать новую политику, а затем применить hello новое подключение toohello политики.</span><span class="sxs-lookup"><span data-stu-id="35e6b-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="35e6b-273">добавить tooenable «UsePolicyBasedTrafficSelectors» при подключении tooan локальных VPN-устройства на основе политик hello «-UsePolicyBaseTrafficSelectors» параметра toohello командлета, или задайте для него слишком параметр hello $False toodisable:</span><span class="sxs-lookup"><span data-stu-id="35e6b-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="35e6b-274">Можно получить подключение hello снова toocheck при обновлении политики hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="35e6b-275">Вы увидите hello вывод последнюю строку hello, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="35e6b-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="35e6b-276">3. Удаление политики IPsec/IKE из подключения</span><span class="sxs-lookup"><span data-stu-id="35e6b-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="35e6b-277">После удаления hello настраиваемой политики из соединения, hello VPN-шлюз Azure переходит назад toohello [по умолчанию список предложений IPsec/IKE](vpn-gateway-about-vpn-devices.md) и снова согласовывает с локальными VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="35e6b-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="35e6b-278">Можно использовать hello toocheck же скрипт, если политика hello удалена из соединения hello.</span><span class="sxs-lookup"><span data-stu-id="35e6b-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35e6b-279">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35e6b-279">Next steps</span></span>

<span data-ttu-id="35e6b-280">Дополнительные сведения о селекторах трафика на основе политик см. в статье [Подключение VPN-шлюзов Azure к нескольким локальным VPN-устройствам на основе политики с помощью PowerShell](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="35e6b-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="35e6b-281">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="35e6b-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="35e6b-282">Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35e6b-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
