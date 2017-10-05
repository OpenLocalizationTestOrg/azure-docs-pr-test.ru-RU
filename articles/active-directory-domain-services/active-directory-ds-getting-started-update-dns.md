---
title: "Доменные службы Azure Active Directory: обновление настроек DNS для виртуальной сети Azure | Документация Майкрософт"
description: "Приступая к работе с доменными службами Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 8bee2a25f196d645b27f30f21305b1550e44e07a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="24eb6-103">Обновление настроек DNS для виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="24eb6-103">Update DNS settings for the Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="24eb6-104">Задача 4. Обновление настроек DNS для виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="24eb6-104">Task 4: Update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="24eb6-105">В предыдущих задачах по настройке вы успешно включили доменные службы Azure Active Directory для своего каталога.</span><span class="sxs-lookup"><span data-stu-id="24eb6-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="24eb6-106">Следующая задача — сделать так, чтобы компьютеры в виртуальной сети могли подключаться к этим службам и использовать их.</span><span class="sxs-lookup"><span data-stu-id="24eb6-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="24eb6-107">В этой статье мы обновим параметры DNS-сервера для виртуальной сети, указав два IP-адреса, по которым доменные службы Azure Active Directory доступны в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="24eb6-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="24eb6-108">После включения доменных служб Azure Active Directory для каталога запишите IP-адреса доменных служб Azure Active Directory, которые отображаются на вкладке **Настройка** вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="24eb6-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="24eb6-109">Чтобы обновить параметр DNS-сервера для виртуальной сети, в которой включены доменные службы Azure Active Directory, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="24eb6-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="24eb6-110">Войдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="24eb6-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="24eb6-111">В левой области щелкните **Сети**.</span><span class="sxs-lookup"><span data-stu-id="24eb6-111">In the left pane, select **Networks**.</span></span>  
    <span data-ttu-id="24eb6-112">Откроется окно **Сети**.</span><span class="sxs-lookup"><span data-stu-id="24eb6-112">The **Networks** window opens.</span></span>

    ![Окно виртуальных сетей](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="24eb6-114">На вкладке **Виртуальные сети** выберите виртуальную сеть, в которой были включены доменные службы Azure Active Directory, чтобы просмотреть ее свойства.</span><span class="sxs-lookup"><span data-stu-id="24eb6-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span></span>
4. <span data-ttu-id="24eb6-115">Выберите вкладку **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="24eb6-115">Click the **Configure** tab.</span></span>

    ![Окно виртуальных сетей](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="24eb6-117">В разделе **DNS-серверы** введите оба IP-адреса, которые отображались в разделе **Доменные службы** на вкладке **Настройка** вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="24eb6-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="24eb6-118">Чтобы сохранить параметры DNS-сервера для этой виртуальной сети, на панели задач в нижней части страницы щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="24eb6-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span></span>

   ![Обновление параметров DNS-сервера для виртуальной сети.](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="24eb6-120">Виртуальные машины в сети получат новые параметры DNS только после перезапуска.</span><span class="sxs-lookup"><span data-stu-id="24eb6-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="24eb6-121">Чтобы получить обновленные параметры DNS сразу, активируйте перезапуск с помощью портала, PowerShell или CLI.</span><span class="sxs-lookup"><span data-stu-id="24eb6-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="24eb6-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="24eb6-122">Next steps</span></span>
<span data-ttu-id="24eb6-123">Задача 5. [Включение синхронизации паролей с доменными службами Azure AD](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="24eb6-123">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
