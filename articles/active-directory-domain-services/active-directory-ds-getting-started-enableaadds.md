---
title: "Доменные службы Azure Active Directory: включение доменных служб Azure Active Directory | Документация Майкрософт"
description: "Включение Azure доменных служб Active Directory с помощью hello классический портал Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="9482e-103">Включение Azure доменных служб Active Directory с помощью hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="9482e-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="9482e-104">Задача 3. Включение доменных служб Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9482e-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="9482e-105">В этой задаче Включение доменных служб Azure Active Directory (Azure AD DS) для каталога, выполнив следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9482e-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="9482e-106">Go toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9482e-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9482e-107">В левой области hello выберите hello **Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9482e-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="9482e-108">Выберите клиент Azure Active Directory (Azure AD) hello (каталог), для которого требуется tooenable Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="9482e-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="9482e-110">На hello **Предварительный просмотр каталога** щелкните hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9482e-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Вкладка "Настройка" каталога](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="9482e-112">В разделе **доменных служб**, измените hello **Включение доменных служб для этого каталога** параметр слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="9482e-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="9482e-113">На странице приветствия отображаются дополнительные параметры конфигурации доменных служб Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="9482e-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Включение доменных служб](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="9482e-115">При включении Azure доменных служб Active Directory для вашего клиента Azure AD создает и сохраняет hello Kerberos и NTLM хэши учетных данных, необходимые для проверки подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="9482e-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="9482e-116">Укажите hello **DNS-имя домена доменных служб**.</span><span class="sxs-lookup"><span data-stu-id="9482e-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="9482e-117">имя домена по умолчанию Hello hello каталога (с **. onmicrosoft.com** суффикс) выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9482e-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="9482e-118">Hello список содержит все домены, которые были настроены для вашего каталога Azure AD, включая проверены и не проверенные домены, настроенные на hello **домены** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9482e-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="9482e-119">Можно также ввести имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="9482e-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="9482e-120">В этом примере — hello пользовательское имя домена *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="9482e-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="9482e-121">Hello префикс к имени домена (например, *contoso100* в hello *contoso100.com* доменное имя) должно содержать не более 15 символов.</span><span class="sxs-lookup"><span data-stu-id="9482e-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="9482e-122">Вы не сможете создать домен доменных служб Azure Active Directory, если префикс доменного имени превышает 15 символов.</span><span class="sxs-lookup"><span data-stu-id="9482e-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="9482e-123">Убедитесь, что hello DNS-имя домена, выбранный для hello управляемого домена еще не существует в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="9482e-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="9482e-124">В частности проверьте toosee ли:</span><span class="sxs-lookup"><span data-stu-id="9482e-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="9482e-125">Уже имеется домен с hello же DNS-имя домена в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="9482e-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="9482e-126">Hello виртуальной сети, вы выбрали содержит VPN-подключение к локальной сети, и имеется домен с hello же DNS-имя домена в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="9482e-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="9482e-127">У вас есть существующей облачной службы с таким именем hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9482e-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="9482e-128">Выберите виртуальную сеть, на котором будет доступен toobe доменных служб Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="9482e-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="9482e-129">Выберите виртуальную сеть hello и выделенной подсетью, созданный в hello **подключение доменных служб виртуальной сети toothis** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="9482e-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="9482e-130">Необходимо учитывать следующие hello.</span><span class="sxs-lookup"><span data-stu-id="9482e-130">Also consider hello following:</span></span>

   * <span data-ttu-id="9482e-131">Убедитесь, что этот hello виртуальную сеть, которую вы указали принадлежит tooan регионе Azure, которая поддерживается Azure доменными службами Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9482e-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9482e-132">tooascertain hello регионах Azure, где находится доменных служб Active Directory Azure см. в разделе [служб Azure по регионам](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="9482e-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="9482e-133">Виртуальные сети, которые принадлежат tooa регион, где не поддерживается доменных служб Active Directory Azure не отображаются в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="9482e-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="9482e-134">Использование выделенной подсетью в виртуальной сети hello для доменных служб Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="9482e-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9482e-135">Сделать *не* выберите hello подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="9482e-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="9482e-136">См. [рекомендации по работе с сетями](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="9482e-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="9482e-137">Аналогичным образом виртуальные сети, которые были созданы с помощью диспетчера ресурсов Azure не отображаются в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="9482e-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="9482e-138">Виртуальные сети на базе Resource Manager в настоящее время не поддерживаются доменными службами Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9482e-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="9482e-139">tooenable Azure доменных служб Active Directory, в области задач hello hello нижней части страницы приветствия щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9482e-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="9482e-140">Хотя доменных служб Active Directory Azure включен для каталога, hello страницы будет отображаться состояние *ожидающие*.</span><span class="sxs-lookup"><span data-stu-id="9482e-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Окно с параметром включения доменных служб](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="9482e-142">Доменные службы Azure Active Directory обеспечивают высокий уровень доступности для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="9482e-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="9482e-143">После включения доменных служб Active Directory Azure hello IP-адресов, в какой домен службы доступны в виртуальной сети hello, отображаются на один одновременно.</span><span class="sxs-lookup"><span data-stu-id="9482e-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="9482e-144">Hello второй IP-адрес будет отображаться вскоре после hello во-первых, как скоро hello служба обеспечивает высокий уровень доступности для своего домена.</span><span class="sxs-lookup"><span data-stu-id="9482e-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="9482e-145">Высокий уровень доступности настраивается при активной для вашего домена, вы увидите два IP-адреса в hello **доменных служб** раздел hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9482e-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="9482e-146">После около 20 минут too30 hello первый IP-адрес в какой домен службы доступны в виртуальной сети hello **IP-адрес** на hello **Настройка** страницы.</span><span class="sxs-lookup"><span data-stu-id="9482e-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![Окно "Доменные службы", в котором отображается первый подготовленный IP-адрес](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="9482e-148">При высокой доступности работает для вашего домена, на странице приветствия отображаются два IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="9482e-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="9482e-149">Управляемый домен доступен в выбранной виртуальной сети по этим двум IP-адресам.</span><span class="sxs-lookup"><span data-stu-id="9482e-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="9482e-150">Запомните hello два IP-адреса можно обновлять hello параметры DNS для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9482e-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="9482e-151">Это позволяет виртуальным машинам в домене toohello tooconnect hello виртуальной сети для операций, например присоединения к домену.</span><span class="sxs-lookup"><span data-stu-id="9482e-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![Окно "Доменные службы", в котором отображаются оба подготовленных IP-адреса](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="9482e-153">В зависимости от размера hello вашего клиента Azure AD (например, hello количество пользователей или групп) управляемый домен tooyour синхронизации занимает некоторое время.</span><span class="sxs-lookup"><span data-stu-id="9482e-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="9482e-154">Этот процесс синхронизации происходит в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="9482e-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="9482e-155">Для больших клиентов с десятками тысяч объектов может занять один или два для всех пользователей, членство в группах и учетные данные toobe синхронизированы дня.</span><span class="sxs-lookup"><span data-stu-id="9482e-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="9482e-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9482e-156">Next step</span></span>
[<span data-ttu-id="9482e-157">Задача 4: обновите параметры DNS hello для hello виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="9482e-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
