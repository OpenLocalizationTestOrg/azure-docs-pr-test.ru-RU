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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="9f4d8-103">Включение доменных служб Azure Active Directory (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="9f4d8-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="9f4d8-104">Задача 4: обновите параметры DNS для hello виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="9f4d8-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="9f4d8-105">Hello предшествующей задачи настройки вы включили успешно Azure доменных служб Active Directory для вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="9f4d8-106">Следующая задача Hello-tooensure, что компьютеры в hello виртуальной сети могут подключаться и этих служб.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="9f4d8-107">В этой статье обновление hello параметры DNS-сервера для вашей виртуальной сети toopoint toohello два IP-адреса доменных служб Active Directory Azure доступно hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="9f4d8-108">tooupdate hello параметров сервера DNS для hello виртуальной сети, в котором требуется включить Azure доменных служб Active Directory, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="9f4d8-109">Hello **Обзор** вкладке отображается набор **необходимые действия по настройке** toobe выполняется после полного выделения ресурсов для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="9f4d8-110">Сначала конфигурации Hello **параметры обновления DNS-сервера, для виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Доменные службы — вкладка "Обзор" после полной подготовки](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="9f4d8-112">По завершении полной подготовки домена на этой плитке отобразятся два IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="9f4d8-113">Каждый IP-адрес представляет контроллер домена для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="9f4d8-114">toocopy hello первый IP адрес tooclipboard, нажмите кнопку Далее tooit hello копирования кнопки.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="9f4d8-115">Нажмите кнопку hello **настроить DNS-серверы** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="9f4d8-116">Вставьте первый IP-адрес hello в hello **добавить DNS-сервер** текстовое поле в hello **DNS-серверы** колонку.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="9f4d8-117">Горизонтальная прокрутка toohello слева toocopy hello второй IP-адрес и вставьте его в hello **добавить DNS-сервер** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Доменные службы — обновление DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="9f4d8-119">Нажмите кнопку **Сохранить** после tooupdate hello DNS-серверов для виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="9f4d8-120">Виртуальные машины в сети hello hello новых параметров DNS получить только после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="9f4d8-121">Если они вам требуются параметры DNS tooget hello обновить прямо сейчас, включать перезапуск портала hello, PowerShell или hello CLI.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="9f4d8-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f4d8-122">Next step</span></span>
[<span data-ttu-id="9f4d8-123">Задача 5: Включение синхронизации паролей tooAzure доменных служб Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f4d8-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
