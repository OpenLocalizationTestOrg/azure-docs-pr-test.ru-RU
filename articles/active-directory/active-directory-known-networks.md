---
title: "Известные сети на классическом портале Azure | Документация Майкрософт"
description: "Настроив известные сети, вы избавитесь от ситуации, при которой IP-адреса вашей организации попадают в отчеты \"Операции входа из нескольких географических регионов\" и \"Операции входа с IP-адресов с подозрительными действиями\"."
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="99560-103">Известные сети</span><span class="sxs-lookup"><span data-stu-id="99560-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="99560-104">классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="99560-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="99560-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="99560-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="99560-106">Вы можете использовать отчеты об использовании и получении доступа Azure Active Directory, чтобы получить информацию о целостности и безопасности каталога вашей организации.</span><span class="sxs-lookup"><span data-stu-id="99560-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="99560-107">C помощью этой информации администратор каталога может более точно определить источники возможных угроз безопасности, что позволяет правильно спланировать их устранение.</span><span class="sxs-lookup"><span data-stu-id="99560-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="99560-108">Возможна ситуация, при которой в отчеты "*Операции входа из нескольких географических регионов*" и "*Входы с IP-адресов с подозрительными действиями*" могут ошибочно попасть IP-адреса, фактически принадлежащие вашей организации.</span><span class="sxs-lookup"><span data-stu-id="99560-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="99560-109">Например, это может произойти, когда:</span><span class="sxs-lookup"><span data-stu-id="99560-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="99560-110">пользователь в офисе в Бостоне удаленно подключился к центру обработки данных в Сан-Франциско, что привело к появлению отчета "Операции входа из нескольких географических регионов";</span><span class="sxs-lookup"><span data-stu-id="99560-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="99560-111">пользователь вашей организации пытается войти несколько раз, указывая неправильный пароль, что приводит к появлению отчета "Операции входа с IP-адресов с подозрительными действиями".</span><span class="sxs-lookup"><span data-stu-id="99560-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="99560-112">Чтобы в таких случаях не создавались ложные отчеты системы безопасности, следует добавить известные диапазоны IP-адресов в список общедоступных IP-адресов вашей организации.</span><span class="sxs-lookup"><span data-stu-id="99560-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="99560-113">Чтобы добавить диапазоны IP-адресов в список общедоступных IP-адресов вашей организации, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="99560-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="99560-114">Войдите в [портал управления Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="99560-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="99560-115">В левой панели щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99560-115">In the left pane, click **Active Directory**.</span></span> 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="99560-117">На вкладке **Каталог** выберите требуемый каталог.</span><span class="sxs-lookup"><span data-stu-id="99560-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="99560-118">В верхнем меню щелкните **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="99560-118">In the menu on the top, click **Configure**.</span></span> 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="99560-120">На вкладке "Настройка" перейдите в **диапазоны общедоступных IP-адресов вашей организации**.</span><span class="sxs-lookup"><span data-stu-id="99560-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="99560-122">Щелкните **Добавьте известные диапазоны IP-адресов**.</span><span class="sxs-lookup"><span data-stu-id="99560-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="99560-123">Добавьте диапазоны адресов в появившемся диалоговом окне и нажмите кнопку "Проверить".</span><span class="sxs-lookup"><span data-stu-id="99560-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![Известные сети](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="99560-125">**Дополнительные ресурсы:**</span><span class="sxs-lookup"><span data-stu-id="99560-125">**Additional resources:**</span></span>

* [<span data-ttu-id="99560-126">Просмотр отчетов о доступе и использовании</span><span class="sxs-lookup"><span data-stu-id="99560-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="99560-127">Операции входа с IP-адресов с подозрительными действиями</span><span class="sxs-lookup"><span data-stu-id="99560-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="99560-128">Операции входа из нескольких географических регионов</span><span class="sxs-lookup"><span data-stu-id="99560-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

