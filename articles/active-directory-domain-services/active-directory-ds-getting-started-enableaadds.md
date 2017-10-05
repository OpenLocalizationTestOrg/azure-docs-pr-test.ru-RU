---
title: "Доменные службы Azure Active Directory: включение доменных служб Azure Active Directory | Документация Майкрософт"
description: "Включение доменных служб Azure Active Directory с помощью классического портала Azure"
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
ms.openlocfilehash: ed72325ca9db99405c6173eb882a92f80cd77f47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="349c3-103">Включение доменных служб Azure Active Directory с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="349c3-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="349c3-104">Задача 3. Включение доменных служб Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="349c3-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="349c3-105">Здесь мы включим доменные службы Azure Active Directory (Azure AD) для каталога. Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="349c3-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing the following steps:</span></span>

1. <span data-ttu-id="349c3-106">Войдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="349c3-106">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="349c3-107">В области слева нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="349c3-107">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="349c3-108">Выберите клиент Azure Active Directory (каталог), для которого требуется включить доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="349c3-108">Select the Azure Active Directory (Azure AD) tenant (directory) for which you want to enable Azure AD DS.</span></span>

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="349c3-110">На странице **предварительного просмотра каталога** щелкните вкладку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="349c3-110">On the **preview directory** page, click the **Configure** tab.</span></span>

    ![Вкладка "Настройка" каталога](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="349c3-112">В разделе **Доменные службы** установите для параметра **Включение доменных служб для этого каталога** значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="349c3-112">Under **domain services**, change the **Enable domain services for this directory** option to **Yes**.</span></span>  
    <span data-ttu-id="349c3-113">На странице появятся дополнительные параметры конфигурации для доменных служб Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="349c3-113">Additional Azure Active Directory Domain Services configuration options appear on the page.</span></span>

    ![Включение доменных служб](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="349c3-115">При включении доменных служб Azure Active Directory для вашего клиента Azure AD создает и сохраняет хэши учетных данных Kerberos и NTLM, необходимые для проверки подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="349c3-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="349c3-116">Укажите **Имя домена DNS для доменных служб**.</span><span class="sxs-lookup"><span data-stu-id="349c3-116">Specify the **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="349c3-117">По умолчанию выбирается доменное имя для каталога (с суффиксом **.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="349c3-117">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="349c3-118">В списке перечислены все домены, которые были настроены для вашего каталога Azure AD, включая проверяемые и непроверяемые, которые были настроены на вкладке **Домены**.</span><span class="sxs-lookup"><span data-stu-id="349c3-118">The list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on the **Domains** tab.</span></span>

   * <span data-ttu-id="349c3-119">Можно также ввести имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="349c3-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="349c3-120">В этом примере в качестве имени пользовательского домена мы используем *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="349c3-120">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="349c3-121">Длина указанного префикса доменного имени (например, *contoso100* для доменного имени *contoso100.com*) не должна превышать 15 символов.</span><span class="sxs-lookup"><span data-stu-id="349c3-121">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="349c3-122">Вы не сможете создать домен доменных служб Azure Active Directory, если префикс доменного имени превышает 15 символов.</span><span class="sxs-lookup"><span data-stu-id="349c3-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="349c3-123">Убедитесь, что выбранное имя домена DNS для управляемого домена не существует в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="349c3-123">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="349c3-124">В частности, проверьте, что:</span><span class="sxs-lookup"><span data-stu-id="349c3-124">Specifically, check to see whether:</span></span>

   * <span data-ttu-id="349c3-125">в виртуальной сети уже существует домен с таким же DNS-именем домена;</span><span class="sxs-lookup"><span data-stu-id="349c3-125">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="349c3-126">для выбранной виртуальной сети установлено VPN-подключение к локальной сети, а в вашей локальной сети есть домен с таким же DNS-именем домена;</span><span class="sxs-lookup"><span data-stu-id="349c3-126">The virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="349c3-127">в виртуальной сети существует облачная служба с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="349c3-127">You have an existing cloud service with that name on the virtual network.</span></span>
8. <span data-ttu-id="349c3-128">Выберите виртуальную сеть, в которой должны быть доступны доменные службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="349c3-128">Select a virtual network on which you want Azure Active Directory Domain Services to be available.</span></span> <span data-ttu-id="349c3-129">Выберите созданную виртуальную сеть и созданную вами выделенную подсеть в раскрывающемся списке **Подключение доменных служб к виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="349c3-129">Select the virtual network and dedicated subnet you created in the **Connect domain services to this virtual network** drop-down list.</span></span> <span data-ttu-id="349c3-130">Учтите также следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="349c3-130">Also consider the following:</span></span>

   * <span data-ttu-id="349c3-131">Убедитесь, что указанная виртуальная сеть принадлежит региону Azure, который поддерживается доменными службами Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="349c3-131">Ensure that the virtual network that you have specified belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="349c3-132">Перейдите на страницу [служб Azure по регионам](https://azure.microsoft.com/regions/#services/), чтобы просмотреть список регионов Azure, в которых доступны доменные службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="349c3-132">To ascertain the Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="349c3-133">Если виртуальные сети находятся в регионе, в котором не поддерживаются доменные службы Azure Active Directory, эти сети не будут отображаться в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="349c3-133">Virtual networks that belong to a region where Azure Active Directory Domain Services is not supported do not show up in the drop-down list.</span></span>

   * <span data-ttu-id="349c3-134">Используйте выделенную подсеть в виртуальной сети для доменных служб Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="349c3-134">Use a dedicated subnet within the virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="349c3-135">*Не* выбирайте подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="349c3-135">Do *not* select the gateway subnet.</span></span> <span data-ttu-id="349c3-136">См. [рекомендации по работе с сетями](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="349c3-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="349c3-137">Точно так же виртуальные сети, созданные с помощью Azure Resource Manager, не отображаются в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="349c3-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in the drop-down list.</span></span> <span data-ttu-id="349c3-138">Виртуальные сети на базе Resource Manager в настоящее время не поддерживаются доменными службами Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="349c3-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="349c3-139">Чтобы включить доменные службы Azure Active Directory, щелкните **Сохранить** в области задач в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="349c3-139">To enable Azure Active Directory Domain Services, in the task pane at the bottom of the page, click **Save**.</span></span>
    * <span data-ttu-id="349c3-140">Пока доменные службы Azure Active Directory включаются для вашего каталога, на странице отображается состояние *Ожидание*.</span><span class="sxs-lookup"><span data-stu-id="349c3-140">While Azure Active Directory Domain Services is being enabled for your directory, the page displays a status of *Pending*.</span></span>

        ![Окно с параметром включения доменных служб](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="349c3-142">Доменные службы Azure Active Directory обеспечивают высокий уровень доступности для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="349c3-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="349c3-143">Когда вы включите доменные службы Azure Active Directory, IP-адреса, по которым доменные службы доступны в виртуальной сети, будут отображаться последовательно.</span><span class="sxs-lookup"><span data-stu-id="349c3-143">After you enable Azure Active Directory Domain Services, the IP addresses at which domain services are available on the virtual network are displayed one at a time.</span></span> <span data-ttu-id="349c3-144">Второй IP-адрес появляется через некоторое время после первого, когда служба включает высокий уровень доступности для вашего домена.</span><span class="sxs-lookup"><span data-stu-id="349c3-144">The second IP address is displayed shortly after the first, as soon the service enables high availability for your domain.</span></span> <span data-ttu-id="349c3-145">Когда высокий уровень доступности настроен и активен для вашего домена, в разделе **Доменные службы** на вкладке **Настройка** будут отображаться два IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="349c3-145">When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="349c3-146">Через 20–30 минут первый из этих IP-адресов доменных служб в виртуальной сети отобразится в поле **IP-адрес** на странице **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="349c3-146">After about 20 to 30 minutes, the first IP address at which domain services are available on your virtual network in the **IP address** field on the **Configure** page.</span></span>

        ![Окно "Доменные службы", в котором отображается первый подготовленный IP-адрес](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="349c3-148">Когда активируется высокий уровень доступности для вашего домена, вы увидите на этой странице два IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="349c3-148">When high availability is operational for your domain, two IP addresses are displayed on the page.</span></span> <span data-ttu-id="349c3-149">Управляемый домен доступен в выбранной виртуальной сети по этим двум IP-адресам.</span><span class="sxs-lookup"><span data-stu-id="349c3-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="349c3-150">Запишите эти два IP-адреса, чтобы обновить параметры DNS для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="349c3-150">Note the two IP addresses so that you can update the DNS settings for your virtual network.</span></span> <span data-ttu-id="349c3-151">Это позволяет виртуальным машинам в виртуальной сети подключиться к домену для таких операций, как присоединение к домену.</span><span class="sxs-lookup"><span data-stu-id="349c3-151">Doing so enables virtual machines on the virtual network to connect to the domain for operations such as domain join.</span></span>

    ![Окно "Доменные службы", в котором отображаются оба подготовленных IP-адреса](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="349c3-153">В зависимости от размера вашего клиента Azure AD (например, количество пользователей или групп) синхронизация с управляемым доменом может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="349c3-153">Depending on the size of your Azure AD tenant (for example, the number of users or groups), synchronization to your managed domain takes a while.</span></span> <span data-ttu-id="349c3-154">Этот процесс синхронизации происходит в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="349c3-154">This synchronization process happens in the background.</span></span> <span data-ttu-id="349c3-155">В случае с крупными клиентами с десятками тысяч объектов синхронизация всех пользователей, групп и учетных данных может длиться один-два дня.</span><span class="sxs-lookup"><span data-stu-id="349c3-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials to be synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="349c3-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="349c3-156">Next step</span></span>
[<span data-ttu-id="349c3-157">Задача 4. Обновление настроек DNS для виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="349c3-157">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
