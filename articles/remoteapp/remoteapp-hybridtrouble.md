---
title: "Создание гибридной коллекции RemoteApp aaaTroubleshoot | Документы Microsoft"
description: "Узнайте, как сбои при создании коллекции гибридного tootroubleshoot удаленных приложений RemoteApp"
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
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="10a44-103">Устранение неполадок создания гибридных коллекций Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="10a44-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="10a44-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="10a44-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="10a44-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="10a44-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="10a44-106">Размещается в гибридной коллекции и сохраняет данные в облако Azure hello, но также позволяет пользователям обращаться к данным и ресурсам, хранимым в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="10a44-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="10a44-107">Пользователи могут получать доступ к приложениям, выполняя вход с помощью своих корпоративных учетных данных, синхронизированных с Azure Active Directory с федерацией.</span><span class="sxs-lookup"><span data-stu-id="10a44-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="10a44-108">Вы можете развернуть гибридную коллекцию, которая использует существующую виртуальную сеть Azure, или создать новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="10a44-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="10a44-109">Рекомендуем создать или использовать подсеть виртуальной сети с достаточно большим диапазоном CIDR, рассчитанным на ожидаемый в будущем рост для Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="10a44-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="10a44-110">Еще не создали свою коллекцию?</span><span class="sxs-lookup"><span data-stu-id="10a44-110">Haven't created your collection yet?</span></span> <span data-ttu-id="10a44-111">В разделе [Создание гибридной коллекции](remoteapp-create-hybrid-deployment.md) hello шагов.</span><span class="sxs-lookup"><span data-stu-id="10a44-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="10a44-112">Если возникают проблемы при создании коллекции или если коллекция hello не работает способом hello, вы считаете, что он должен, извлечь hello следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="10a44-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="10a44-113">Недопустимый образ</span><span class="sxs-lookup"><span data-stu-id="10a44-113">Your image is invalid</span></span>
<span data-ttu-id="10a44-114">При появлении сообщения, как «GoldImageInvalid», когда ожидается для Azure tooprovision вашей коллекции, это означает, что образ шаблона не соответствует hello [определенные требования изображения](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="10a44-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="10a44-115">Начинаем, читать их [требования](remoteapp-imagereqs.md), исправьте образ и повторите попытку коллекции toocreate.</span><span class="sxs-lookup"><span data-stu-id="10a44-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="10a44-116">Определены ли группы безопасности сети для вашей виртуальной сети?</span><span class="sxs-lookup"><span data-stu-id="10a44-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="10a44-117">При наличии сетевых групп безопасности, определенные в подсети hello, вы используете для коллекции, убедитесь, что они [URL-адреса и порты](remoteapp-ports.md) осуществляется из подсети.</span><span class="sxs-lookup"><span data-stu-id="10a44-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="10a44-118">Можно добавить дополнительный сетевой безопасности группы toohello развернуты виртуальные машины вами в подсети hello более жесткий контроль.</span><span class="sxs-lookup"><span data-stu-id="10a44-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="10a44-119">Используете ли вы собственные DNS-серверы?</span><span class="sxs-lookup"><span data-stu-id="10a44-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="10a44-120">Доступны ли они из вашей подсети виртуальной сети?</span><span class="sxs-lookup"><span data-stu-id="10a44-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="10a44-121">У вас есть toomake приветствия убедиться, что DNS-серверы в сети, всегда являются вверх и всегда будет tooresolve hello виртуальных машин, размещенных в hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="10a44-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="10a44-122">Не используйте Google DNS для этого.</span><span class="sxs-lookup"><span data-stu-id="10a44-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="10a44-123">Для гибридных коллекций используйте собственные DNS-серверы.</span><span class="sxs-lookup"><span data-stu-id="10a44-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="10a44-124">Можно указать их в схеме конфигурации сети или через портал управления hello при создании виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="10a44-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="10a44-125">DNS-серверы используются в порядке hello, они указаны в виде перехода на другой ресурс (в противоположность tooround циклический перебор).</span><span class="sxs-lookup"><span data-stu-id="10a44-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="10a44-126">См. слишком[разрешение имен для виртуальных машин и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake убедиться, что DNS-серверы, настроенные correcly.</span><span class="sxs-lookup"><span data-stu-id="10a44-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="10a44-127">Убедитесь, что hello DNS-серверов для вашей коллекции доступны через hello подсети виртуальной сети, указанное для этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="10a44-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="10a44-128">Например:</span><span class="sxs-lookup"><span data-stu-id="10a44-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Определение DNS-сервера](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="10a44-130">Используется ли в вашей коллекции контроллер домена Active Directory?</span><span class="sxs-lookup"><span data-stu-id="10a44-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="10a44-131">В настоящее время с Azure RemoteApp можно связать только один домен Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10a44-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="10a44-132">Hello гибридного коллекция поддерживает только Azure Active Directory учетные записи, которые были синхронизированы с помощью средства DirSync из развертывания Windows Server Active Directory; в частности либо синхронизирован с параметром синхронизации паролей hello синхронизированы с федерацией служб федерации Active Directory (AD FS) настроен.</span><span class="sxs-lookup"><span data-stu-id="10a44-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="10a44-133">Требуется toocreate настраиваемый домен, который соответствует hello суффикс домена имени участника-пользователя для локального домена и настройка интеграции каталогов.</span><span class="sxs-lookup"><span data-stu-id="10a44-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="10a44-134">Дополнительные сведения см. в статье [Требования Azure AD + Active Directory для Azure RemoteApp](remoteapp-ad.md).</span><span class="sxs-lookup"><span data-stu-id="10a44-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="10a44-135">Убедитесь, что указаны допустимые сведения домена hello и hello контроллер домена доступен из hello создания виртуальной Машины в подсети hello, используемой для удаленного приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="10a44-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="10a44-136">Также убедитесь, что hello учетной записи службы, предоставленные учетные данные предоставлены разрешения tooadd компьютеров toohello домена и что hello имя AD, предоставляемые разрешается из hello DNS в hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="10a44-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="10a44-137">Какое имя домена было указано при создании коллекции?</span><span class="sxs-lookup"><span data-stu-id="10a44-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="10a44-138">имя домена Hello, создании или добавлено должно быть внутреннее имя домена (не имя домена Azure AD) и должно быть в разрешимом формате DNS (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="10a44-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="10a44-139">Например имеется внутреннее имя Active Directory (contoso.local) и Active Directory имя участника-пользователя (contoso.com) - имеется toouse hello внутреннее имя при создании коллекции.</span><span class="sxs-lookup"><span data-stu-id="10a44-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

