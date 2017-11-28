---
title: "aaaKnown сетей в hello классический портал Azure | Документы Microsoft"
description: "Настроив известных сетей, можно избежать необходимости IP-адресов, которые принадлежат вашей организации, включенных в hello входы из нескольких географических регионов и входы с IP-адресов с подозрительной активности отчеты."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="1f73c-103">Известные сети</span><span class="sxs-lookup"><span data-stu-id="1f73c-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f73c-104">классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="1f73c-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="1f73c-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1f73c-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="1f73c-106">Можно использовать доступа Azure Active Directory и видимость toogain отчеты об использовании hello целостности и безопасности каталога вашей организации.</span><span class="sxs-lookup"><span data-stu-id="1f73c-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="1f73c-107">С этой информацией администратор каталога может лучше определить, где могут возникнуть риски безопасности, чтобы их можно создать соответствующий план toomitigate этих рисков.</span><span class="sxs-lookup"><span data-stu-id="1f73c-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="1f73c-108">Возможно, что hello»*входа из нескольких географических регионов*«и»*входы с IP-адресов с подозрительными действиями*«отчеты неправильно флаг IP-адресов, которые принадлежат фактически вашей организация.</span><span class="sxs-lookup"><span data-stu-id="1f73c-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="1f73c-109">Например, это может произойти, когда:</span><span class="sxs-lookup"><span data-stu-id="1f73c-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="1f73c-110">Пользователь в вашем офисе Бостоне вход в удаленно tooyour центр обработки данных в Сан-Франциско триггеры hello отчета «Входы из нескольких географических регионов»</span><span class="sxs-lookup"><span data-stu-id="1f73c-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="1f73c-111">Пользователь организации пытается подключиться через toosign несколько раз с помощью неправильного пароля триггеры hello отчета «Входы с IP-адресов с подозрительными действиями»</span><span class="sxs-lookup"><span data-stu-id="1f73c-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="1f73c-112">сообщает этих случаях от создания пользователя в заблуждение безопасность tooprevent, следует добавить известных toohello список диапазонов IP-адресов вашей организации общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="1f73c-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="1f73c-113">диапазоны tooadd общедоступный IP-адрес вашей организации, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1f73c-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="1f73c-114">Toohello входа [портала управления Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1f73c-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="1f73c-115">Hello левой панели щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f73c-115">In hello left pane, click **Active Directory**.</span></span> 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="1f73c-117">В hello **каталога** вкладке, выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="1f73c-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="1f73c-118">В меню в верхней части hello hello выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="1f73c-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="1f73c-120">На вкладке "Настройка" hello, переход слишком**вашей организации общих IP-адресов**</span><span class="sxs-lookup"><span data-stu-id="1f73c-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="1f73c-122">Щелкните **Добавьте известные диапазоны IP-адресов**.</span><span class="sxs-lookup"><span data-stu-id="1f73c-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="1f73c-123">Добавьте в hello появившемся диапазонов адресов и нажмите кнопку "Проверить" hello, после завершения.</span><span class="sxs-lookup"><span data-stu-id="1f73c-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="1f73c-125">**Дополнительные ресурсы:**</span><span class="sxs-lookup"><span data-stu-id="1f73c-125">**Additional resources:**</span></span>

* [<span data-ttu-id="1f73c-126">Просмотр отчетов о доступе и использовании</span><span class="sxs-lookup"><span data-stu-id="1f73c-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="1f73c-127">Операции входа с IP-адресов с подозрительными действиями</span><span class="sxs-lookup"><span data-stu-id="1f73c-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="1f73c-128">Операции входа из нескольких географических регионов</span><span class="sxs-lookup"><span data-stu-id="1f73c-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

