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
ms.openlocfilehash: c704ee189072ce8ed196d1ef0a23edd528a10025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="7c8e4-103">Включение доменных служб Azure Active Directory (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="7c8e4-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="7c8e4-104">Задача 4. Обновление настроек DNS для виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="7c8e4-104">Task 4: update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="7c8e4-105">В предыдущих задачах по настройке вы успешно включили доменные службы Azure Active Directory для своего каталога.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="7c8e4-106">Следующая задача — сделать так, чтобы компьютеры в виртуальной сети могли подключаться к этим службам и использовать их.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="7c8e4-107">В этой статье мы обновим параметры DNS-сервера для виртуальной сети, указав два IP-адреса, по которым доменные службы Azure Active Directory доступны в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

<span data-ttu-id="7c8e4-108">Чтобы обновить параметр DNS-сервера для виртуальной сети, в которой включены доменные службы Azure Active Directory, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-108">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="7c8e4-109">На вкладке **Обзор** отображается набор **требуемых шагов конфигурации**, которые следует выполнить после полной подготовки управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-109">The **Overview** tab lists a set of **Required configuration steps** to be performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="7c8e4-110">Первый шаг конфигурации — **обновление параметров DNS-сервера для виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-110">The first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Доменные службы — вкладка "Обзор" после полной подготовки](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="7c8e4-112">По завершении полной подготовки домена на этой плитке отобразятся два IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="7c8e4-113">Каждый IP-адрес представляет контроллер домена для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="7c8e4-114">Чтобы скопировать первый IP-адрес в буфер обмена, нажмите кнопку копирования рядом с адресом.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-114">To copy the first IP address to clipboard, click the copy button next to it.</span></span> <span data-ttu-id="7c8e4-115">Затем нажмите кнопку **Настроить DNS-серверы**.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-115">Then click the **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="7c8e4-116">Вставьте первый IP-адрес в текстовое поле **Добавить DNS-сервер** в колонке **DNS-серверы**.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-116">Paste the first IP address into the **Add DNS server** textbox in the **DNS servers** blade.</span></span> <span data-ttu-id="7c8e4-117">Прокрутите по горизонтали влево, чтобы скопировать второй IP-адрес. Вставьте его в текстовое поле **Добавить DNS-сервер**.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-117">Scroll horizontally to the left to copy the second IP address and paste it into the **Add DNS server** textbox.</span></span>

    ![Доменные службы — обновление DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="7c8e4-119">После обновления DNS-серверов для виртуальной сети нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-119">Click **Save** when you are done to update the DNS servers for the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="7c8e4-120">Виртуальные машины в сети получат новые параметры DNS только после перезапуска.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="7c8e4-121">Чтобы получить обновленные параметры DNS сразу, активируйте перезапуск с помощью портала, PowerShell или CLI.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="7c8e4-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c8e4-122">Next step</span></span>
[<span data-ttu-id="7c8e4-123">Задача 5. Включение синхронизации паролей с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c8e4-123">Task 5: enable password synchronization to Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
