---
title: "Часто задаваемые вопросы по отчетам Azure Active Directory | Документация Майкрософт"
description: "Часто задаваемые вопросы об отчетах Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: accf292f70bf0eafdefc00c3feeaf8e346605401
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="c2e6c-103">Часто задаваемые вопросы об отчетах Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2e6c-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="c2e6c-104">Эта статья содержит ответы на часто задаваемые вопросы об отчетах Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="c2e6c-105">Дополнительные сведения см. в разделе [Отчеты в Azure Active Directory — предварительная версия](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c2e6c-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="c2e6c-106">**Вопрос. Что такое период хранения данных журналов действий (аудита и входа в систему) на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="c2e6c-107">**Ответ.** Мы храним данные клиентов с бесплатной лицензией в течение 7 дней, а перейдя на лицензию Azure AD Premium 1 или Premium 2, вы сможете использовать данные в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span></span> <span data-ttu-id="c2e6c-108">Дополнительные сведения о периоде хранения см. в статье [Политики хранения отчетов Azure Active Directory](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="c2e6c-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="c2e6c-109">**Вопрос. Какова задержка перед отображением данных действия после выполнения моей задачи?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="c2e6c-110">**Ответ.** Для журналов аудита действий эта задержка составляет от 15 минут до часа.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span></span> <span data-ttu-id="c2e6c-111">Для журналов действий входа в систему это задержка составляет от 15 минут для большинства записей и до 2 часов для некоторых записей.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span></span>

---

<span data-ttu-id="c2e6c-112">**Вопрос. Нужно ли быть глобальным администратором, чтобы просмотреть журналы действий на портале Azure или получить их данные через API?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span></span>

<span data-ttu-id="c2e6c-113">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-113">**A:** No.</span></span> <span data-ttu-id="c2e6c-114">Для просмотра данных отчетов на портале Azure или обращения к ним через API достаточно быть **читателем безопасности**, **администратором безопасности** или **глобальным администратором**.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span></span>

---

<span data-ttu-id="c2e6c-115">**Вопрос. Можно ли получить данные журнала действий Office 365 на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="c2e6c-116">**Ответ.** Хотя в журналах действий Office 365 и Azure AD совместно используется много ресурсов каталога, если требуется получить полное представление журналов действий Office 365, то следует перейти в Центр администрирования Office 365 и там получить данные журналов действий Office 365.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="c2e6c-117">**Вопрос. Какие интерфейсы API используются для получения данных журналов активности Office 365?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="c2e6c-118">**Ответ.** Используйте интерфейсы API управления Office 365 для доступа к [журналам действий Office 365 с помощью API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="c2e6c-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="c2e6c-119">**Вопрос. Сколько записей можно скачать с портала Azure?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="c2e6c-120">**Ответ.** С портала Azure можно скачать до 120 тыс. записей.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-120">**A:** You can download up to 120K records from the Azure portal.</span></span> <span data-ttu-id="c2e6c-121">Записи отсортированы по *убыванию даты и времени* по умолчанию, и вы получите 120 тыс. самых последних записей.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span></span> 

---

<span data-ttu-id="c2e6c-122">**Вопрос. Сколько записей можно запрашивать через API действий?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-122">**Q: How many records can I query through the activities API?**</span></span>

<span data-ttu-id="c2e6c-123">**Ответ.** Можно запрашивать до 1 миллиона записей (если вы не используете оператор top, который сортирует записи по убыванию даты и времени).</span><span class="sxs-lookup"><span data-stu-id="c2e6c-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span></span> <span data-ttu-id="c2e6c-124">При использовании оператора top можно запросить до 500 тыс. записей.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-124">If you do use the “top” operator, you can query up to 500K records.</span></span> <span data-ttu-id="c2e6c-125">Примеры запросов с использованием API можно найти [здесь](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c2e6c-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="c2e6c-126">**Вопрос. Как получить лицензию уровня Premium?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="c2e6c-127">**Ответ.** Ответ на этот вопрос есть в разделе [Приступая к работе с Azure Active Directory Premium](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="c2e6c-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="c2e6c-128">**Вопрос. Как скоро после получения лицензии Premium я увижу данные действий?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="c2e6c-129">**Ответ.** Если вас уже есть данные действий с бесплатной лицензией, то вы увидите те же данные.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-129">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="c2e6c-130">Если у вас нет данных, то потребуется один или два дня.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="c2e6c-131">**Вопрос. Увижу ли я данные за прошлый месяц после получения лицензии Azure AD Premium?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="c2e6c-132">**Ответ**. Если вы недавно перешли на версию Premium (включая пробную версию), то первоначально сможете увидеть данные за 7 дней.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-132">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="c2e6c-133">По мере накопления данных этот период увеличится до 30 дней.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-133">When data accumulates, you will see up to 30 days.</span></span>

---

<span data-ttu-id="c2e6c-134">**Вопрос. В службе защиты идентификации имеется событие риска, но я не вижу соответствующей операции входа в списке всех операций входа. Так и должно быть?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="c2e6c-135">**Ответ**. Да, служба защиты идентификации оценивает степень риска для всех процессов проверки подлинности, как интерактивных, так и неинтерактивных.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="c2e6c-136">Однако в списке всех операций входа показаны только интерактивные операции входа.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-136">However, all sign-ins only report shows only the interactive sign-ins.</span></span>

---

<span data-ttu-id="c2e6c-137">**Вопрос. Как скачать отчет "Пользователи, находящиеся в группе риска" на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-137">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="c2e6c-138">**Ответ**. Команда для скачивания отчета *Пользователи, находящиеся в группе риска* будет добавлена в ближайшем будущем.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-138">**A:** The option to download *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="c2e6c-139">**Вопрос. Как узнать, почему операция входа или пользователь были помечены как рискованные на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-139">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span></span>

<span data-ttu-id="c2e6c-140">**Ответ**. Если у вас выпуск Premium, вы можете получить дополнительные сведения о событиях риска, щелкнув пользователя в отчете "Пользователи, находящиеся в группе риска" или щелкнув "Рискованные входы в систему".</span><span class="sxs-lookup"><span data-stu-id="c2e6c-140">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span></span> <span data-ttu-id="c2e6c-141">Пользователи выпуска Free или Basic не могут просматривать сведения о событиях риска, связанных с пользователями в группе риска и рискованными операциями входа.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-141">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span></span>

---

<span data-ttu-id="c2e6c-142">**Вопрос. Как вычисляются IP-адреса в отчете о событиях входа и событиях входа, представляющих риск?**</span><span class="sxs-lookup"><span data-stu-id="c2e6c-142">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="c2e6c-143">**Ответ.** IP-адреса выдаются таким образом, что определенная связь между IP-адресом и физическим расположением компьютера с этим адресом отсутствует.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span></span> <span data-ttu-id="c2e6c-144">Это осложняется тем, что поставщики мобильной связи и виртуальные частные сети выдают IP-адреса из центральных пулов, которые нередко находятся очень далеко от места, где фактически используется клиентское устройство.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span></span> <span data-ttu-id="c2e6c-145">Учитывая все вышесказанное, преобразование IP-адреса в физическое расположение не гарантируется и осуществляется на основе трассировок, данных реестра, обратных просмотров и других сведений.</span><span class="sxs-lookup"><span data-stu-id="c2e6c-145">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
