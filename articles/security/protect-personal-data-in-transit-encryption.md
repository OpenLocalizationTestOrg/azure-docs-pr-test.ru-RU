---
title: "aaaProtect личных данных во время передачи с помощью шифрования в Azure | Документы Microsoft"
description: "С помощью шифрования в Azure tooprotect персональные данные"
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
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="a73a2-103">Технологии шифрования Azure. Защита неактивных персональных данных при передаче с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="a73a2-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="a73a2-104">Эта статья поможет вам понять и использовать данные toosecure технологии Azure шифрования во время передачи.</span><span class="sxs-lookup"><span data-stu-id="a73a2-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="a73a2-105">Защита конфиденциальности hello личных данных при пересылке через сеть hello является важной частью стратегии безопасности многоуровневый глубокой обороны.</span><span class="sxs-lookup"><span data-stu-id="a73a2-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="a73a2-106">Шифрование при передаче — спроектированный tooprevent злоумышленник перехватывает данные, передаваемые от может tooview или используйте hello данным.</span><span class="sxs-lookup"><span data-stu-id="a73a2-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="a73a2-107">Сценарий</span><span class="sxs-lookup"><span data-stu-id="a73a2-107">Scenario</span></span>

<span data-ttu-id="a73a2-108">Компании больших прогулка по, рядом с офисом в Соединенных Штатах Америки hello, развернут расписаниям toooffer его операций в морская hello, Adriatic и Балтийский компании seas, а также Британские острова hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="a73a2-109">toosupport эти усилия, он получил несколько небольших строк прогулка по в Италии, Германии, Дания и hello Великобритания</span><span class="sxs-lookup"><span data-stu-id="a73a2-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="a73a2-110">Hello компания использует Microsoft Azure toostore корпоративных данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="a73a2-111">Сюда входят персональные данные, позволяющие установить личность, например имена, адреса, номера телефонов и данные кредитной карты в глобальной клиентской базе.</span><span class="sxs-lookup"><span data-stu-id="a73a2-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="a73a2-112">Он также включает традиционные персоналом сведения, например адреса, номера телефонов, идентификационные номера налога и медицинские сведения о сотрудниках компании во всех расположениях.</span><span class="sxs-lookup"><span data-stu-id="a73a2-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="a73a2-113">Строка Hello прогулка по также хранится большой базы данных вознаграждения и постоянных элементов программы, содержат персональные данные tootrack связи с клиентами, текущие и прошлые.</span><span class="sxs-lookup"><span data-stu-id="a73a2-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="a73a2-114">Персональные данные клиентов вводится в базе данных hello из удаленных офисов компании hello и путешествий расположены по всему Здравствуй, мир!.</span><span class="sxs-lookup"><span data-stu-id="a73a2-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="a73a2-115">Документы, содержащие сведения о пользователе передаются hello сетевые tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="a73a2-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="a73a2-116">Проблема</span><span class="sxs-lookup"><span data-stu-id="a73a2-116">Problem statement</span></span>

<span data-ttu-id="a73a2-117">Hello компании должны защищать конфиденциальность клиентов hello и персональные данные сотрудников во время его находится в пути tooand из служб Azure.</span><span class="sxs-lookup"><span data-stu-id="a73a2-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="a73a2-118">Цель компании</span><span class="sxs-lookup"><span data-stu-id="a73a2-118">Company goal</span></span>

<span data-ttu-id="a73a2-119">Здравствуйте, tooensure цель компании, персональные данные шифруются при отключать диск.</span><span class="sxs-lookup"><span data-stu-id="a73a2-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="a73a2-120">Если посторонних перехвата hello отключение диска личных данных, ее необходимо в форме, которая сделает его может быть прочитан.</span><span class="sxs-lookup"><span data-stu-id="a73a2-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="a73a2-121">Применение шифрования должно быть простым или полностью прозрачным для пользователей и администраторов.</span><span class="sxs-lookup"><span data-stu-id="a73a2-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="a73a2-122">Решения</span><span class="sxs-lookup"><span data-stu-id="a73a2-122">Solutions</span></span>

<span data-ttu-id="a73a2-123">Службы Azure предоставляют несколько средств и технологий toohelp защиты личных данных во время передачи.</span><span class="sxs-lookup"><span data-stu-id="a73a2-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="a73a2-124">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="a73a2-124">Azure Storage</span></span>

<span data-ttu-id="a73a2-125">Данные, хранящиеся в облаке hello должны передаваться из hello клиентом, при которых могут находиться в любом месте в Здравствуй, мир, toohello центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a73a2-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="a73a2-126">При извлечении данных пользователями, он проходит еще раз, за hello противоположного направления.</span><span class="sxs-lookup"><span data-stu-id="a73a2-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="a73a2-127">Данные, во время передачи через hello общедоступный Интернет всегда являются риску перехвата злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="a73a2-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="a73a2-128">Это важные tooprotect hello конфиденциальность личных данных с помощью toosecure шифрование на уровне транспорта, как оно перемещается между расположениями.</span><span class="sxs-lookup"><span data-stu-id="a73a2-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="a73a2-129">Hello протокол HTTPS обеспечивает канал связи безопасный, зашифрованный hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="a73a2-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="a73a2-130">HTTPS должен быть tooaccess используемые объекты в хранилище Azure и, при вызове API REST.</span><span class="sxs-lookup"><span data-stu-id="a73a2-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="a73a2-131">Предписывает использование протокола HTTPS hello, при использовании [подписей общего доступа](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) toodelegate доступа (SAS) tooAzure-объектов хранилища.</span><span class="sxs-lookup"><span data-stu-id="a73a2-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="a73a2-132">Существует два типа SAS: уровня службы и учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a73a2-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="a73a2-133">Создание подписанного URL-адреса уровня службы</span><span class="sxs-lookup"><span data-stu-id="a73a2-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="a73a2-134">Служба SAS делегаты доступа tooa ресурс в одном из службы хранилища hello (служба BLOB-объектов, очередей, таблицы или файла).</span><span class="sxs-lookup"><span data-stu-id="a73a2-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="a73a2-135">tooconstruct службы SAS, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a73a2-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="a73a2-136">Укажите поля версии Signed hello</span><span class="sxs-lookup"><span data-stu-id="a73a2-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="a73a2-137">Укажите hello Signed ресурсов (больших двоичных объектов и файла только служба)</span><span class="sxs-lookup"><span data-stu-id="a73a2-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="a73a2-138">Укажите параметры запроса заголовки ответа tooOverride (службы BLOB-объектов и файла только служба)</span><span class="sxs-lookup"><span data-stu-id="a73a2-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="a73a2-139">Укажите имя таблицы (таблицы только служба) hello</span><span class="sxs-lookup"><span data-stu-id="a73a2-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="a73a2-140">Укажите hello политики доступа</span><span class="sxs-lookup"><span data-stu-id="a73a2-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="a73a2-141">Укажите период действия подписи hello</span><span class="sxs-lookup"><span data-stu-id="a73a2-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="a73a2-142">Укажите разрешения.</span><span class="sxs-lookup"><span data-stu-id="a73a2-142">Specify Permissions</span></span>

9. <span data-ttu-id="a73a2-143">Укажите IP-адрес или диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a73a2-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="a73a2-144">Укажите hello протокола HTTP</span><span class="sxs-lookup"><span data-stu-id="a73a2-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="a73a2-145">Укажите диапазон доступа к таблицам.</span><span class="sxs-lookup"><span data-stu-id="a73a2-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="a73a2-146">Укажите подписанный идентификатор hello</span><span class="sxs-lookup"><span data-stu-id="a73a2-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="a73a2-147">Укажите hello подписи</span><span class="sxs-lookup"><span data-stu-id="a73a2-147">Specify hello Signature</span></span>

<span data-ttu-id="a73a2-148">Дополнительные сведения см. в статье [Создание подписанного URL-адреса уровня службы](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="a73a2-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="a73a2-149">Создание подписанного URL-адреса уровня учетной записи</span><span class="sxs-lookup"><span data-stu-id="a73a2-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="a73a2-150">Учетная запись SAS делегирует tooresources доступ в одном или нескольких служб хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="a73a2-151">Вы также можете делегировать доступ tooread, запись и операции удаления контейнеров больших двоичных объектов, таблиц, очередей и общие файловые ресурсы, не допускается в отношении службы SAS.</span><span class="sxs-lookup"><span data-stu-id="a73a2-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="a73a2-152">Учетной записи сопоставления безопасности является аналогичные toothat подписанный URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="a73a2-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="a73a2-153">Дополнительные сведения см. в статье [Создание подписанного URL-адреса уровня учетной записи](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="a73a2-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="a73a2-154">Принудительное использование HTTPS при вызове REST API</span><span class="sxs-lookup"><span data-stu-id="a73a2-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="a73a2-155">Использование hello tooenforce HTTPS при вызове API-интерфейс REST tooaccess объектов в учетных записях хранения, можно включить Secure передачи необходимых для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="a73a2-156">В hello портал Azure, выберите **создать учетную запись хранилища**, или существующую учетную запись хранилища, выберите **параметры** и затем **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="a73a2-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="a73a2-157">В разделе **Требуется безопасное перемещение** выберите **Включено**.</span><span class="sxs-lookup"><span data-stu-id="a73a2-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Создание учетной записи хранения](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="a73a2-159">Более подробные инструкции, включая способ защиты передачи обязательно программно, см. tooenable [требуют безопасного передачи](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="a73a2-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="a73a2-160">Шифрование данных в хранилище файлов Azure</span><span class="sxs-lookup"><span data-stu-id="a73a2-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="a73a2-161">tooencrypt данных во время передачи с [хранилище файлов Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), можно использовать SMB 3.x с Windows 8, 8.1 и 10 и Windows Server 2012 R2 и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a73a2-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="a73a2-162">При использовании службы файлов Azure hello любое соединение без шифрования происходит сбой при включении «Защита передачи, требуемая».</span><span class="sxs-lookup"><span data-stu-id="a73a2-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="a73a2-163">К ним относятся сценарии с использованием SMB 2.1, SMB 3.0 без шифрования и некоторые виды hello Linux SMB-клиент.</span><span class="sxs-lookup"><span data-stu-id="a73a2-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="a73a2-164">Шифрование Azure на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="a73a2-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="a73a2-165">Еще один вариант защиты персональных данных при переносе между клиентскими приложениями и службой хранилища Azure — [шифрование на стороне клиента](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="a73a2-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="a73a2-166">Hello данные шифруются перед передачей в хранилище Azure и расшифровываются при hello данные извлекаются из хранилища Azure, hello после получения hello клиентской стороны.</span><span class="sxs-lookup"><span data-stu-id="a73a2-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="a73a2-167">VPN типа "сеть — сеть" Azure</span><span class="sxs-lookup"><span data-stu-id="a73a2-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="a73a2-168">Эффективным способом tooprotect личных данных при передаче между корпоративной сети или пользователя и hello виртуальная сеть Azure — toouse [сайт сайт](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) или [точки сайтами](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) виртуальную частную сеть (VPN).</span><span class="sxs-lookup"><span data-stu-id="a73a2-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="a73a2-169">VPN-подключения создается защищенный туннель зашифрованные через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="a73a2-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="a73a2-170">Создание VPN-подключения типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="a73a2-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="a73a2-171">Сеть сеть VPN подключается нескольких пользователей на tooAzure hello корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="a73a2-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="a73a2-172">toocreate подключения сеть сеть в hello портал Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a73a2-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="a73a2-173">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="a73a2-173">Create a virtual network.</span></span>

2. <span data-ttu-id="a73a2-174">Укажите DNS-сервер</span><span class="sxs-lookup"><span data-stu-id="a73a2-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="a73a2-175">Создайте подсеть шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="a73a2-176">Создание шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="a73a2-177">Создание шлюза локальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="a73a2-178">Настройте устройство VPN.</span><span class="sxs-lookup"><span data-stu-id="a73a2-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="a73a2-179">Создание VPN-подключения hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="a73a2-180">Проверьте hello VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="a73a2-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="a73a2-181">На более подробные инструкции, как соединение toocreate сайта для сайта в hello Azure портала, см. в разделе [создание сайта для сайта соединение в hello портала Azure.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="a73a2-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="a73a2-182">Создание VPN-подключения типа "точка — сеть"</span><span class="sxs-lookup"><span data-stu-id="a73a2-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="a73a2-183">VPN-Подключение точка-сайт создает безопасное подключение отдельных клиентских компьютеров tooa в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a73a2-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="a73a2-184">Это полезно при необходимости tooAzure tooconnect из удаленного расположения, например, из дома или гостиницы или конференции центра.</span><span class="sxs-lookup"><span data-stu-id="a73a2-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="a73a2-185">toocreate подключение точка сеть в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a73a2-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="a73a2-186">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="a73a2-186">Create a virtual network.</span></span>

2. <span data-ttu-id="a73a2-187">Добавьте подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="a73a2-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="a73a2-188">Укажите DNS-сервер</span><span class="sxs-lookup"><span data-stu-id="a73a2-188">Specify a DNS server.</span></span> <span data-ttu-id="a73a2-189">(необязательно).</span><span class="sxs-lookup"><span data-stu-id="a73a2-189">(optional)</span></span>

4. <span data-ttu-id="a73a2-190">Создайте шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a73a2-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="a73a2-191">Создайте сертификаты.</span><span class="sxs-lookup"><span data-stu-id="a73a2-191">Generate certificates.</span></span>

6. <span data-ttu-id="a73a2-192">Добавление пула адресов клиента hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="a73a2-193">Отправьте данные сертификата открытого hello корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="a73a2-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="a73a2-194">Создать и установить пакет конфигурации VPN-клиента hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="a73a2-195">Установите экспортированный сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="a73a2-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="a73a2-196">Подключите tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a73a2-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="a73a2-197">Проверьте подключение.</span><span class="sxs-lookup"><span data-stu-id="a73a2-197">Verify your connection.</span></span>

<span data-ttu-id="a73a2-198">Более подробные инструкции см. в разделе [Настройка tooa подключение точка-сайт виртуальной сети с использованием проверки подлинности сертификата: портал Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="a73a2-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="a73a2-199">Протокол SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="a73a2-199">SSL/TLS</span></span>

<span data-ttu-id="a73a2-200">Корпорация Майкрософт рекомендует использовать данные tooexchange протоколов SSL/TLS в разных расположениях.</span><span class="sxs-lookup"><span data-stu-id="a73a2-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="a73a2-201">Организации, выберите toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove больших наборов данных по выделенному каналу WAN высокоскоростной также можно шифровать данные hello в hello с помощью SSL/TLS или другие протоколы для дополнительной защиты на уровне приложений.</span><span class="sxs-lookup"><span data-stu-id="a73a2-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="a73a2-202">Шифрование по умолчанию</span><span class="sxs-lookup"><span data-stu-id="a73a2-202">Encryption by default</span></span>

<span data-ttu-id="a73a2-203">Корпорация Майкрософт использует шифрование tooprotect данных во время передачи между клиентами и облачных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="a73a2-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="a73a2-204">Если взаимодействуют со службой хранилища Azure через портал Azure hello всех транзакций выполняется через HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a73a2-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="a73a2-205">[Безопасность транспортного уровня](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) — что центрах обработки данных Майкрософт попытается toonegotiate с клиентскими компьютерами, которые подключаются tooMicrosoft облачные службы протокола hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="a73a2-206">TLS обеспечивает надежную аутентификацию, конфиденциальность сообщений, целостность (включая обнаружение незаконного изменения, перехвата и подделки сообщений), взаимодействие, гибкость алгоритма, простоту развертывания и использования.</span><span class="sxs-lookup"><span data-stu-id="a73a2-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="a73a2-207">[Полная безопасность пересылки](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS), которая также применяется, позволяет защитить соединения между клиентскими системами заказчиков и облачными службами (Майкрософт) с помощью уникальных ключей.</span><span class="sxs-lookup"><span data-stu-id="a73a2-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="a73a2-208">Длина ключа подключения tooMicrosoft облачных служб также воспользоваться преимуществами шифрования на основе RSA 2048 бит.</span><span class="sxs-lookup"><span data-stu-id="a73a2-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="a73a2-209">Здравствуйте, сочетание TLS, длины ключей RSA 2048 бит и PFS делает его более сложной для кого-либо toointercept и доступ к данным, находящегося в пути между облачными службами Майкрософт и клиентами.</span><span class="sxs-lookup"><span data-stu-id="a73a2-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="a73a2-210">Данные при передаче всегда шифруются в [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="a73a2-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="a73a2-211">Кроме tooencrypting данных предыдущих toostoring toopersistent мультимедиа, hello данных всегда также обеспечивается во время передачи по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a73a2-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="a73a2-212">HTTPS — hello единственный протокол, который поддерживается для приветствия интерфейсы REST хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="a73a2-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="a73a2-213">Сводка</span><span class="sxs-lookup"><span data-stu-id="a73a2-213">Summary</span></span>

<span data-ttu-id="a73a2-214">Hello компании можно выполнить его цель защиты личных данных и hello конфиденциальности таких данных путем применения tooAzure подключений HTTPS хранилища, с помощью подписей общего доступа и включение защиты передачи требуется об учетных записях хранения hello.</span><span class="sxs-lookup"><span data-stu-id="a73a2-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="a73a2-215">Кроме того, компания сможет защищать персональные данные с помощью подключений SMB 3.0 и реализации шифрования на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="a73a2-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="a73a2-216">Сеть сеть VPN-подключение с hello корпоративной сети toohello виртуальной сети Azure, и точка сеть VPN-подключение с отдельным пользователям будет создания защищенного туннеля, через который безопасной передачи личных данных.</span><span class="sxs-lookup"><span data-stu-id="a73a2-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="a73a2-217">Шифрования рекомендации корпорации Майкрософт по умолчанию для дальнейшей защиты hello конфиденциальность личных данных.</span><span class="sxs-lookup"><span data-stu-id="a73a2-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a73a2-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a73a2-218">Next steps</span></span>

- [<span data-ttu-id="a73a2-219">Рекомендации по защите и шифрованию данных в Azure</span><span class="sxs-lookup"><span data-stu-id="a73a2-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="a73a2-220">Планирование и проектирование VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="a73a2-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="a73a2-221">VPN-шлюз: вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="a73a2-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="a73a2-222">Приобретение и настройка сертификата SSL для службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a73a2-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
