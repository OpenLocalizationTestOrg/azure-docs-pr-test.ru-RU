---
title: "Azure доменных служб Active Directory: Обновить параметры DNS для hello виртуальной сети Azure | Документы Microsoft"
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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="ab66a-103">Обновите параметры DNS для hello виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="ab66a-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="ab66a-104">Задача 4: Обновите параметры DNS для hello виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="ab66a-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="ab66a-105">Hello предшествующей задачи настройки вы включили успешно Azure доменных служб Active Directory для вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="ab66a-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="ab66a-106">Следующая задача Hello-tooensure, что компьютеры в hello виртуальной сети могут подключаться и этих служб.</span><span class="sxs-lookup"><span data-stu-id="ab66a-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="ab66a-107">В этой статье обновление hello параметры DNS-сервера для вашей виртуальной сети toopoint toohello два IP-адреса доменных служб Active Directory Azure доступно hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ab66a-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="ab66a-108">После включения Azure доменных служб Active Directory для каталога hello, обратите внимание, hello IP-адресов для Azure доменных служб Active Directory, которые отображаются на hello **Настройка** вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="ab66a-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="ab66a-109">tooupdate hello параметров сервера DNS для hello виртуальной сети, в котором требуется включить Azure доменных служб Active Directory, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ab66a-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="ab66a-110">Go toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ab66a-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ab66a-111">Выберите в левой области hello **сетей**.</span><span class="sxs-lookup"><span data-stu-id="ab66a-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="ab66a-112">Hello **сетей** открывается окно.</span><span class="sxs-lookup"><span data-stu-id="ab66a-112">hello **Networks** window opens.</span></span>

    ![Окно виртуальных сетей](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="ab66a-114">На hello **виртуальных сетей** вкладке, выберите hello виртуальной сети, в котором требуется включить tooview доменных служб Active Directory Azure его свойства.</span><span class="sxs-lookup"><span data-stu-id="ab66a-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="ab66a-115">Нажмите кнопку hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ab66a-115">Click hello **Configure** tab.</span></span>

    ![Окно виртуальных сетей](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="ab66a-117">В hello **DNS-серверы** введите оба hello IP-адресов, которые отображались в hello **доменных служб** раздела, посвященного hello **Настройка** вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="ab66a-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="ab66a-118">Нажмите кнопку Параметры toosave hello DNS-сервера для этой виртуальной сети, в области задач hello hello нижней части окна hello **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ab66a-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![Обновите параметры DNS-сервера hello для hello виртуальной сети](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="ab66a-120">Виртуальные машины в сети hello hello новых параметров DNS получить только после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="ab66a-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="ab66a-121">Если они вам требуются параметры DNS tooget hello обновить прямо сейчас, включать перезапуск портала hello, PowerShell или hello CLI.</span><span class="sxs-lookup"><span data-stu-id="ab66a-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ab66a-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab66a-122">Next steps</span></span>
<span data-ttu-id="ab66a-123">Задача 5. [включить синхронизацию паролей tooAzure доменных служб Active Directory](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="ab66a-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
