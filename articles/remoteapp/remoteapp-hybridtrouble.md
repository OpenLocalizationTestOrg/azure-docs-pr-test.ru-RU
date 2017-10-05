---
title: "Устранение неполадок при создании гибридных коллекций RemoteApp | Документация Майкрософт"
description: "Устранение неполадок при сбоях создания гибридной коллекции RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="f5eb5-103">Устранение неполадок создания гибридных коллекций Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f5eb5-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f5eb5-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f5eb5-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="f5eb5-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f5eb5-106">Гибридная коллекция размещается и хранит данные в облаке Azure, но также предоставляет пользователям доступ к данным и ресурсам, размещенным в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="f5eb5-107">Пользователи могут получать доступ к приложениям, выполняя вход с помощью своих корпоративных учетных данных, синхронизированных с Azure Active Directory с федерацией.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="f5eb5-108">Вы можете развернуть гибридную коллекцию, которая использует существующую виртуальную сеть Azure, или создать новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="f5eb5-109">Рекомендуем создать или использовать подсеть виртуальной сети с достаточно большим диапазоном CIDR, рассчитанным на ожидаемый в будущем рост для Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="f5eb5-110">Еще не создали свою коллекцию?</span><span class="sxs-lookup"><span data-stu-id="f5eb5-110">Haven't created your collection yet?</span></span> <span data-ttu-id="f5eb5-111">Сведения о требуемых действиях см. в статье [Создание гибридной коллекции для Azure RemoteApp](remoteapp-create-hybrid-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f5eb5-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="f5eb5-112">Если при создании коллекции возникают неполадки или коллекция работает неправильно, просмотрите приведенные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="f5eb5-113">Недопустимый образ</span><span class="sxs-lookup"><span data-stu-id="f5eb5-113">Your image is invalid</span></span>
<span data-ttu-id="f5eb5-114">Если во время ожидания подготовки вашей коллекции к работе службой Azure появляется такое сообщение, как "GoldImageInvalid", значит ваш образ шаблона не соответствует [определенным требованиям к образам](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="f5eb5-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="f5eb5-115">Поэтому прочитайте [эти требования](remoteapp-imagereqs.md), исправьте образ и попробуйте создать коллекцию еще раз.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="f5eb5-116">Определены ли группы безопасности сети для вашей виртуальной сети?</span><span class="sxs-lookup"><span data-stu-id="f5eb5-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="f5eb5-117">Если в подсети, используемой для вашей коллекции, определены группы безопасности сети, проследите, чтобы из этой подсети были доступны следующие [URL-адреса и порты](remoteapp-ports.md) .</span><span class="sxs-lookup"><span data-stu-id="f5eb5-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="f5eb5-118">Можно добавить дополнительные группы безопасности сети к виртуальным машинам, развернутым в подсети, для обеспечения более жесткого контроля.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="f5eb5-119">Используете ли вы собственные DNS-серверы?</span><span class="sxs-lookup"><span data-stu-id="f5eb5-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="f5eb5-120">Доступны ли они из вашей подсети виртуальной сети?</span><span class="sxs-lookup"><span data-stu-id="f5eb5-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="f5eb5-121">Проследите, чтобы DNS-серверы в виртуальной сети всегда работали и всегда были в состоянии правильно обрабатывать адреса виртуальных машин, размещенных в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="f5eb5-122">Не используйте Google DNS для этого.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="f5eb5-123">Для гибридных коллекций используйте собственные DNS-серверы.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="f5eb5-124">Их можно указать в схеме конфигурации сети или на портале управления при создании виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="f5eb5-125">DNS-серверы используются в том порядке, в котором они указаны, в режиме отработки отказа (в отличие от циклического перебора).</span><span class="sxs-lookup"><span data-stu-id="f5eb5-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="f5eb5-126">Ознакомьтесь с разделом [Разрешение имен для ВМ и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) , чтобы убедиться, что ваши DNS-серверы настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="f5eb5-127">Убедитесь, что DNS-серверы для коллекции работают и доступны из подсети виртуальной сети, указанной для этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="f5eb5-128">Например:</span><span class="sxs-lookup"><span data-stu-id="f5eb5-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Определение DNS-сервера](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="f5eb5-130">Используется ли в вашей коллекции контроллер домена Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f5eb5-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="f5eb5-131">В настоящее время с Azure RemoteApp можно связать только один домен Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="f5eb5-132">Гибридная коллекция поддерживает только те учетные записи Azure Active Directory, которые были синхронизированы с помощью средства DirSync из развертывания Windows Server Active Directory. В частности, они могут быть синхронизированы с помощью параметра "Синхронизация паролей" или служб федерации Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="f5eb5-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="f5eb5-133">Необходимо создать пользовательский домен, который совпадает с суффиксом домена UPN для локального домена, и настроить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="f5eb5-134">Дополнительные сведения см. в статье [Требования Azure AD + Active Directory для Azure RemoteApp](remoteapp-ad.md).</span><span class="sxs-lookup"><span data-stu-id="f5eb5-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="f5eb5-135">Убедитесь, что предоставленные сведения о домене являются допустимыми, а контроллер домена доступен из виртуальных машин, созданных в той подсети, которая используется для Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="f5eb5-136">Убедитесь также, что предоставленные учетные данные учетной записи службы имеют разрешения на добавление компьютеров в указанный домен и что указанное имя AD можно разрешить с DNS-сервера, предоставленного в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="f5eb5-137">Какое имя домена было указано при создании коллекции?</span><span class="sxs-lookup"><span data-stu-id="f5eb5-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="f5eb5-138">Созданное или добавленное имя домена должно быть внутренним именем домена (а не именем домена Azure AD) и иметь разрешимый формат DNS (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="f5eb5-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="f5eb5-139">Например, если у вас имеется внутреннее имя Active Directory (contoso.local) и имя участника-пользователя Active Directory (contoso.com), при создании коллекции необходимо использовать внутреннее имя.</span><span class="sxs-lookup"><span data-stu-id="f5eb5-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>

