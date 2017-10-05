---
title: "Защита персональных данных при передаче с помощью шифрования в Azure | Документация Майкрософт"
description: "Сведения о защите персональных данных с помощью шифрования в Azure."
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
ms.openlocfilehash: 99e40b8a09a2f151e7f83fbb58bdfc00ae4b1268
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="b915b-103">Технологии шифрования Azure. Защита неактивных персональных данных при передаче с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="b915b-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="b915b-104">Эта статья поможет понять, как защитить данные при передаче на основе технологий шифрования Azure.</span><span class="sxs-lookup"><span data-stu-id="b915b-104">This article will help you understand and use Azure encryption technologies to secure data in transit.</span></span> 

<span data-ttu-id="b915b-105">Защита конфиденциальности персональных данных во время их передачи по сети — это важная часть многоуровневой эшелонированной стратегии защиты.</span><span class="sxs-lookup"><span data-stu-id="b915b-105">Protecting the privacy of personal data as it travels across the network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="b915b-106">Шифрование при передаче не позволяет злоумышленнику, перехватывающему передачи, просматривать или использовать данные.</span><span class="sxs-lookup"><span data-stu-id="b915b-106">Encryption in transit is designed to prevent an attacker who intercepts transmissions from being able to view or use the data.</span></span>

## <a name="scenario"></a><span data-ttu-id="b915b-107">Сценарий</span><span class="sxs-lookup"><span data-stu-id="b915b-107">Scenario</span></span>

<span data-ttu-id="b915b-108">Большая круизная компания, расположенная в США, расширяет масштабы своей деятельности и предлагает маршруты в Средиземном, Адриатическом и Балтийском морях, а также на Британских островах.</span><span class="sxs-lookup"><span data-stu-id="b915b-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="b915b-109">Чтобы реализовать эту программу, компания приобрела несколько небольших круизных фирм, расположенных в Италии, Германии, Дании и Великобритании.</span><span class="sxs-lookup"><span data-stu-id="b915b-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="b915b-110">Корпоративные данные компании хранятся в облаке Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b915b-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="b915b-111">Сюда входят персональные данные, позволяющие установить личность, например имена, адреса, номера телефонов и данные кредитной карты в глобальной клиентской базе.</span><span class="sxs-lookup"><span data-stu-id="b915b-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="b915b-112">Он также включает традиционные персоналом сведения, например адреса, номера телефонов, идентификационные номера налога и медицинские сведения о сотрудниках компании во всех расположениях.</span><span class="sxs-lookup"><span data-stu-id="b915b-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="b915b-113">Круизная компания также содержит большую базу данных участников программ лояльности и программ скидок, которая, в свою очередь, содержит персональные данные, позволяющие отслеживать связи с текущими и бывшими клиентами.</span><span class="sxs-lookup"><span data-stu-id="b915b-113">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="b915b-114">Персональные данные клиентов вводятся в базу данных из филиалов компании и туристических агентств, расположенных по всему миру.</span><span class="sxs-lookup"><span data-stu-id="b915b-114">Personal data of customers is entered in the database from the company’s remote offices and from travel agents located around the world.</span></span> <span data-ttu-id="b915b-115">Документы, содержащие сведения о клиенте передаются по сети в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="b915b-115">Documents containing customer information are transferred across the network to Azure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="b915b-116">Проблема</span><span class="sxs-lookup"><span data-stu-id="b915b-116">Problem statement</span></span>

<span data-ttu-id="b915b-117">Компания должна защищать конфиденциальность персональных данных клиентов и сотрудников при передаче в службы Azure и из них.</span><span class="sxs-lookup"><span data-stu-id="b915b-117">The company must protect the privacy of customers’ and employees’ personal data while it is in transit to and from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="b915b-118">Цель компании</span><span class="sxs-lookup"><span data-stu-id="b915b-118">Company goal</span></span>

<span data-ttu-id="b915b-119">Компания должна гарантировать шифрование персональных данных при передаче.</span><span class="sxs-lookup"><span data-stu-id="b915b-119">The company goal to ensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="b915b-120">Если посторонние лица перехватят эти данные, благодаря шифрованию, они не смогут прочитать их.</span><span class="sxs-lookup"><span data-stu-id="b915b-120">If unauthorized persons intercept the off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="b915b-121">Применение шифрования должно быть простым или полностью прозрачным для пользователей и администраторов.</span><span class="sxs-lookup"><span data-stu-id="b915b-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="b915b-122">Решения</span><span class="sxs-lookup"><span data-stu-id="b915b-122">Solutions</span></span>

<span data-ttu-id="b915b-123">Службы Azure предоставляют несколько инструментов и технологий защиты персональных данных при передаче.</span><span class="sxs-lookup"><span data-stu-id="b915b-123">Azure services provide multiple tools and technologies to help you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="b915b-124">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="b915b-124">Azure Storage</span></span>

<span data-ttu-id="b915b-125">Данные, хранящиеся в облаке, должны переместиться с клиента, который может физически располагаться в любой точке мира, в центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="b915b-125">Data that is stored in the cloud must travel from the client, which can be physically located anywhere in the world, to the Azure data center.</span></span> <span data-ttu-id="b915b-126">После извлечения данных пользователями они возвращаются в обратном направлении.</span><span class="sxs-lookup"><span data-stu-id="b915b-126">When that data is retrieved by users, it travels again, in the opposite direction.</span></span> <span data-ttu-id="b915b-127">При передаче данных через общедоступный Интернет всегда есть риск их перехвата злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="b915b-127">Data that is in transit over the public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="b915b-128">Очень важно защитить конфиденциальность персональных данных с помощью шифрования на транспортном уровне. Это позволяет обеспечить безопасность при перемещении между расположениями.</span><span class="sxs-lookup"><span data-stu-id="b915b-128">It is important to protect the privacy of personal data by using transport-level encryption to secure it as it moves between locations.</span></span>

<span data-ttu-id="b915b-129">Протокол HTTPS предоставляет безопасный, зашифрованный коммуникационный канал через Интернет.</span><span class="sxs-lookup"><span data-stu-id="b915b-129">The HTTPS protocol provides a secure, encrypted communications channel over the Internet.</span></span> <span data-ttu-id="b915b-130">При получении доступа к объектам в службе хранилища Azure и вызове REST API должен использоваться протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b915b-130">HTTPS should be used to access objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="b915b-131">Он применяется при использовании [подписанного URL-адреса](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS), обеспечивающего делегирование доступа к объектам службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b915b-131">You enforce use of the HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) to delegate access to Azure Storage objects.</span></span> <span data-ttu-id="b915b-132">Существует два типа SAS: уровня службы и учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b915b-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="b915b-133">Создание подписанного URL-адреса уровня службы</span><span class="sxs-lookup"><span data-stu-id="b915b-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="b915b-134">SAS уровня службы делегирует доступ к ресурсу только в одной из служб хранения: службе BLOB-объектов, очередей, таблиц или файлов.</span><span class="sxs-lookup"><span data-stu-id="b915b-134">A Service SAS delegates access to a resource in just one of the storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="b915b-135">Чтобы создать подписанный URL-адрес уровня службы, выполните такие действия:</span><span class="sxs-lookup"><span data-stu-id="b915b-135">To construct a Service SAS, do the following:</span></span>

1. <span data-ttu-id="b915b-136">Укажите поле подписанной версии.</span><span class="sxs-lookup"><span data-stu-id="b915b-136">Specify the Signed Version Field</span></span>

2. <span data-ttu-id="b915b-137">Укажите подписанный ресурс (только служба BLOB-объектов и файлов).</span><span class="sxs-lookup"><span data-stu-id="b915b-137">Specify the Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="b915b-138">Укажите параметры запроса переопределения заголовков объекта (только служба BLOB-объектов и служба файлов).</span><span class="sxs-lookup"><span data-stu-id="b915b-138">Specify Query Parameters to Override Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="b915b-139">Укажите имя таблицы (только служба таблиц).</span><span class="sxs-lookup"><span data-stu-id="b915b-139">Specify the Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="b915b-140">Укажите политику доступа.</span><span class="sxs-lookup"><span data-stu-id="b915b-140">Specify the Access Policy</span></span>

6. <span data-ttu-id="b915b-141">Укажите период действия подписи.</span><span class="sxs-lookup"><span data-stu-id="b915b-141">Specify the Signature Validity Interval</span></span>

8. <span data-ttu-id="b915b-142">Укажите разрешения.</span><span class="sxs-lookup"><span data-stu-id="b915b-142">Specify Permissions</span></span>

9. <span data-ttu-id="b915b-143">Укажите IP-адрес или диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="b915b-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="b915b-144">Укажите протокол HTTP.</span><span class="sxs-lookup"><span data-stu-id="b915b-144">Specify the HTTP Protocol</span></span>

11. <span data-ttu-id="b915b-145">Укажите диапазон доступа к таблицам.</span><span class="sxs-lookup"><span data-stu-id="b915b-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="b915b-146">Укажите идентификатор подписи.</span><span class="sxs-lookup"><span data-stu-id="b915b-146">Specify the Signed Identifier</span></span>

13. <span data-ttu-id="b915b-147">Укажите подпись.</span><span class="sxs-lookup"><span data-stu-id="b915b-147">Specify the Signature</span></span>

<span data-ttu-id="b915b-148">Дополнительные сведения см. в статье [Создание подписанного URL-адреса уровня службы](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="b915b-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="b915b-149">Создание подписанного URL-адреса уровня учетной записи</span><span class="sxs-lookup"><span data-stu-id="b915b-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="b915b-150">SAS уровня учетной записи делегирует доступ к ресурсам в одной или нескольких службах хранилища.</span><span class="sxs-lookup"><span data-stu-id="b915b-150">An Account SAS delegates access to resources in one or more of the storage services.</span></span> <span data-ttu-id="b915b-151">Вы также можете делегировать доступ к операциям чтения, записи и удаления в контейнерах больших двоичных объектов, таблицах, очередях и общих папках, которые запрещены в SAS службы.</span><span class="sxs-lookup"><span data-stu-id="b915b-151">You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="b915b-152">Создание SAS уровня учетной записи аналогично созданию SAS уровня службы.</span><span class="sxs-lookup"><span data-stu-id="b915b-152">Construction of an Account SAS is similar to that of a Service SAS.</span></span> <span data-ttu-id="b915b-153">Дополнительные сведения см. в статье [Создание подписанного URL-адреса уровня учетной записи](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="b915b-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="b915b-154">Принудительное использование HTTPS при вызове REST API</span><span class="sxs-lookup"><span data-stu-id="b915b-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="b915b-155">Чтобы принудительно задать использование протокола HTTPS при вызове REST API для доступа к объектам в учетных записях хранения, можно включить параметр "Требуется безопасное перемещение" в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b915b-155">To enforce the use of HTTPS when calling REST APIs to access objects in storage accounts, you can enable Secure Transfer Required for the storage account.</span></span> 

1. <span data-ttu-id="b915b-156">На портале Azure выберите **Создание учетной записи хранения**. Если у вас уже есть учетная запись хранения, выберите **Параметры**, а затем — **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="b915b-156">In the Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="b915b-157">В разделе **Требуется безопасное перемещение** выберите **Включено**.</span><span class="sxs-lookup"><span data-stu-id="b915b-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Создание учетной записи хранения](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="b915b-159">Дополнительные сведения, в том числе способы включения параметра "Требуется безопасное перемещение" программным способом, см. в статье [Требование безопасной передачи](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="b915b-159">For more detailed instructions, including how to enable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="b915b-160">Шифрование данных в хранилище файлов Azure</span><span class="sxs-lookup"><span data-stu-id="b915b-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="b915b-161">Чтобы реализовать шифрование данных при передаче с помощью [хранилища файлов Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), вы можете использовать SMB 3.x с Windows 8, 8.1 и 10, и Windows Server 2012 R2 и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b915b-161">To encrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="b915b-162">Кроме того, если этот параметр включен, то при использовании службы файлов Azure любое подключение без шифрования завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="b915b-162">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="b915b-163">Это относится к сценариям, включающим в себя SMB 2.1, SMB 3.0 без шифрования и некоторые конфигурации SMB-клиента Linux.</span><span class="sxs-lookup"><span data-stu-id="b915b-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="b915b-164">Шифрование Azure на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="b915b-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="b915b-165">Еще один вариант защиты персональных данных при переносе между клиентскими приложениями и службой хранилища Azure — [шифрование на стороне клиента](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="b915b-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="b915b-166">В этом случае данные шифруются перед передачей в службу хранилища Azure, а при их извлечении они расшифровываются на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="b915b-166">The data is encrypted before being transferred into Azure Storage and when you retrieve the data from Azure Storage, the data is decrypted after it is received on the client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="b915b-167">VPN типа "сеть — сеть" Azure</span><span class="sxs-lookup"><span data-stu-id="b915b-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="b915b-168">Эффективный способ защиты персональных данных при передаче между корпоративной сетью или пользователем и виртуальной сетью Azure — использование виртуальной частной сети типа ["сеть — сеть"](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) или ["точка — сеть"](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal).</span><span class="sxs-lookup"><span data-stu-id="b915b-168">An effective way to protect personal data in transit between a corporate network or user and the Azure virtual network is to use a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="b915b-169">VPN-подключение создает зашифрованный безопасный туннель через Интернет.</span><span class="sxs-lookup"><span data-stu-id="b915b-169">A VPN connection creates a secure encrypted tunnel across the Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="b915b-170">Создание VPN-подключения типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="b915b-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="b915b-171">VPN типа "сеть — сеть" подключает нескольких пользователей корпоративной сети к Azure.</span><span class="sxs-lookup"><span data-stu-id="b915b-171">A site-to-site VPN connects multiple users on the corporate network to Azure.</span></span> <span data-ttu-id="b915b-172">Чтобы создать подключение этого типа на портале Azure, выполните такие действия:</span><span class="sxs-lookup"><span data-stu-id="b915b-172">To create a site-to-site connection in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="b915b-173">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="b915b-173">Create a virtual network.</span></span>

2. <span data-ttu-id="b915b-174">Укажите DNS-сервер</span><span class="sxs-lookup"><span data-stu-id="b915b-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="b915b-175">Создайте подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="b915b-175">Create the gateway subnet.</span></span>

4. <span data-ttu-id="b915b-176">Создайте шлюз VPN.</span><span class="sxs-lookup"><span data-stu-id="b915b-176">Create the VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="b915b-177">Создайте локальный сетевой шлюз.</span><span class="sxs-lookup"><span data-stu-id="b915b-177">Create the local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="b915b-178">Настройте устройство VPN.</span><span class="sxs-lookup"><span data-stu-id="b915b-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="b915b-179">Создайте VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="b915b-179">Create the VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="b915b-180">Проверьте VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="b915b-180">Verify the VPN connection.</span></span>

<span data-ttu-id="b915b-181">Дополнительные сведения о том, как создавать подключения типа "сеть — сеть" на портале Azure, см. в [этой статье] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal).</span><span class="sxs-lookup"><span data-stu-id="b915b-181">For more detailed instructions on how to create a site-to-site connection in the Azure portal, see [Create a Site-to-Site  connection in the Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="b915b-182">Создание VPN-подключения типа "точка — сеть"</span><span class="sxs-lookup"><span data-stu-id="b915b-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="b915b-183">VPN-подключение типа "точка — сеть" создает защищенное подключение к виртуальной сети с отдельного клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="b915b-183">A Point-to-Site VPN creates a secure connection from an individual client computer to a virtual network.</span></span> <span data-ttu-id="b915b-184">Это полезно в том случае, если нужно подключиться к Azure из удаленного расположения, например из дома, гостиницы или конференц-зала.</span><span class="sxs-lookup"><span data-stu-id="b915b-184">This is useful when you  want to connect to Azure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="b915b-185">Чтобы создать VPN-подключение типа "точка — сеть" на портале Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b915b-185">To create a point-to-site  connection in the Azure portal,</span></span>

1. <span data-ttu-id="b915b-186">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="b915b-186">Create a virtual network.</span></span>

2. <span data-ttu-id="b915b-187">Добавьте подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="b915b-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="b915b-188">Укажите DNS-сервер</span><span class="sxs-lookup"><span data-stu-id="b915b-188">Specify a DNS server.</span></span> <span data-ttu-id="b915b-189">(необязательно).</span><span class="sxs-lookup"><span data-stu-id="b915b-189">(optional)</span></span>

4. <span data-ttu-id="b915b-190">Создайте шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b915b-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="b915b-191">Создайте сертификаты.</span><span class="sxs-lookup"><span data-stu-id="b915b-191">Generate certificates.</span></span>

6. <span data-ttu-id="b915b-192">Добавьте пулы адресов клиента.</span><span class="sxs-lookup"><span data-stu-id="b915b-192">Add the client address pool.</span></span>

7. <span data-ttu-id="b915b-193">Отправьте данные об открытом ключе корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="b915b-193">Upload the root certificate public certificate data.</span></span>

8. <span data-ttu-id="b915b-194">Создайте и установите пакет конфигурации VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="b915b-194">Generate and install the VPN client configuration package.</span></span>

9. <span data-ttu-id="b915b-195">Установите экспортированный сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="b915b-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="b915b-196">Подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="b915b-196">Connect to Azure.</span></span>

11. <span data-ttu-id="b915b-197">Проверьте подключение.</span><span class="sxs-lookup"><span data-stu-id="b915b-197">Verify your connection.</span></span>

<span data-ttu-id="b915b-198">Дополнительные сведения см. в статье [Настройка подключения типа "точка — сеть" к виртуальной сети с помощью проверки подлинности на основе сертификата, используя портал Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal).</span><span class="sxs-lookup"><span data-stu-id="b915b-198">For more detailed instructions, see [Configure a Point-to-Site connection to a VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="b915b-199">Протокол SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="b915b-199">SSL/TLS</span></span>

<span data-ttu-id="b915b-200">Корпорация Майкрософт рекомендует всегда использовать протоколы SSL и TLS при обмене данными между разными расположениями.</span><span class="sxs-lookup"><span data-stu-id="b915b-200">Microsoft recommends that you always use SSL/TLS protocols to exchange data across different locations.</span></span> <span data-ttu-id="b915b-201">Организации, перемещающие большие наборы данных через выделенный высокоскоростной канал WAN с помощью [ExpressRoute](https://docs.microsoft.com/azure/expressroute/), могут также шифровать данные на уровне приложения, используя SSL, TLS или другие протоколы для дополнительной защиты.</span><span class="sxs-lookup"><span data-stu-id="b915b-201">Organizations that choose to use [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) to move large data sets over a dedicated high-speed WAN link can also encrypt the data at the application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="b915b-202">Шифрование по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b915b-202">Encryption by default</span></span>

<span data-ttu-id="b915b-203">Корпорация Майкрософт использует шифрование для защиты данных при передаче между клиентами и облачными служба Azure.</span><span class="sxs-lookup"><span data-stu-id="b915b-203">Microsoft uses encryption to protect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="b915b-204">Если вы обращаетесь к службе хранилища Azure через портал Azure, все транзакции проходят по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b915b-204">If you are interacting with Azure Storage through the Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="b915b-205">[Протокол TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) — это протокол, который центры обработки данных Майкрософт попытаются согласовать с клиентскими системами, подключенными к облачным службам (Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="b915b-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is the protocol that Microsoft data centers will attempt to negotiate with client systems that connect to Microsoft cloud services.</span></span> <span data-ttu-id="b915b-206">TLS обеспечивает надежную аутентификацию, конфиденциальность сообщений, целостность (включая обнаружение незаконного изменения, перехвата и подделки сообщений), взаимодействие, гибкость алгоритма, простоту развертывания и использования.</span><span class="sxs-lookup"><span data-stu-id="b915b-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="b915b-207">[Полная безопасность пересылки](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS), которая также применяется, позволяет защитить соединения между клиентскими системами заказчиков и облачными службами (Майкрософт) с помощью уникальных ключей.</span><span class="sxs-lookup"><span data-stu-id="b915b-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="b915b-208">При подключении к облачным службам (Майкрософт) также используются ключи шифрования на 2048 бит на основе RSA.</span><span class="sxs-lookup"><span data-stu-id="b915b-208">Connections to Microsoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="b915b-209">Сочетание протокола TLS, ключей шифрования на 2048 бит на основе RSA и PFS значительно усложняет перехват и получение доступа к данным, которые передаются между облачными службами (Майкрософт) и клиентами.</span><span class="sxs-lookup"><span data-stu-id="b915b-209">The combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone to intercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="b915b-210">Данные при передаче всегда шифруются в [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="b915b-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="b915b-211">Данные не только шифруются перед сохранением на постоянный носитель. Они также всегда защищены при передаче благодаря использованию протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b915b-211">In addition to encrypting data prior to storing to persistent media, the data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="b915b-212">HTTPS — единственный протокол, который поддерживают интерфейсы REST в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b915b-212">HTTPS is the only protocol that is supported for the Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="b915b-213">Сводка</span><span class="sxs-lookup"><span data-stu-id="b915b-213">Summary</span></span>

<span data-ttu-id="b915b-214">Компания может достичь своей цели (защиты персональных данных и их конфиденциальности), применяя подключения HTTPS к службе хранилища Azure, используя подписанные URL-адреса и включив параметр "Требуется безопасное перемещение" в учетных записях хранения.</span><span class="sxs-lookup"><span data-stu-id="b915b-214">The company can accomplish its goal of protecting personal data and the privacy of such data by enforcing HTTPS connections to Azure Storage, using Shared Access Signatures and enabling Secure Transfer Required on the storage accounts.</span></span> <span data-ttu-id="b915b-215">Кроме того, компания сможет защищать персональные данные с помощью подключений SMB 3.0 и реализации шифрования на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="b915b-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="b915b-216">VPN-подключения типа "сеть — сеть" из корпоративной сети к виртуальной сети Azure и VPN-подключения типа "точка — сеть" от отдельных пользователей создадут защищенный туннель для безопасной передачи персональных данных.</span><span class="sxs-lookup"><span data-stu-id="b915b-216">Site-to-site VPN connections from the corporate network to the Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="b915b-217">Стандартные методы шифрования корпорации Майкрософт по-прежнему будут защищать конфиденциальность персональных данных.</span><span class="sxs-lookup"><span data-stu-id="b915b-217">Microsoft’s default encryption practices will further protect the privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b915b-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b915b-218">Next steps</span></span>

- [<span data-ttu-id="b915b-219">Рекомендации по защите и шифрованию данных в Azure</span><span class="sxs-lookup"><span data-stu-id="b915b-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="b915b-220">Планирование и проектирование VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="b915b-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="b915b-221">VPN-шлюз: вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="b915b-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="b915b-222">Приобретение и настройка сертификата SSL для службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b915b-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
