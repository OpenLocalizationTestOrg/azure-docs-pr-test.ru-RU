---
title: "aaaAzure Active Directory отчетов часто задаваемые вопросы | Документы Microsoft"
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
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="a9cce-103">Часто задаваемые вопросы об отчетах Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9cce-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="a9cce-104">Эта статья содержит ответы toofrequently, задаваемые вопросы (FAQ) о работе с отчетами Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a9cce-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="a9cce-105">Дополнительные сведения см. в разделе [Отчеты в Azure Active Directory — предварительная версия](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a9cce-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="a9cce-106">**Вопрос. что такое hello хранение данных для журналов действий (аудита и входа в систему) hello портал Azure?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="a9cce-107">**Ответ** мы предоставляем 7 дней данных клиентам бесплатно и переключив tooan Azure AD Premium 1 или Premium 2 лицензирования, можно получить доступ к данным вверх too30 дней.</span><span class="sxs-lookup"><span data-stu-id="a9cce-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="a9cce-108">Дополнительные сведения о периоде хранения см. в статье [Политики хранения отчетов Azure Active Directory](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="a9cce-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="a9cce-109">**Вопрос. как долго, пока не отображаются данные о действиях hello после завершения задач?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="a9cce-110">**Ответ** журналы действий аудита имеют задержку, в диапазоне от 15 минут tooan час.</span><span class="sxs-lookup"><span data-stu-id="a9cce-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="a9cce-111">Журналы действия при входе имеют задержку, в диапазоне от 15 минут для большинства записей и too2 часов для несколько записей.</span><span class="sxs-lookup"><span data-stu-id="a9cce-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="a9cce-112">**Вопрос. необходимо toobe журналы действие hello toosee глобального администратора в hello портала Azure или tooget данных с помощью hello API?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="a9cce-113">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="a9cce-113">**A:** No.</span></span> <span data-ttu-id="a9cce-114">Может быть **чтения безопасности**, **администратору безопасности** или **глобального администратора** toosee reporting данные на портале Azure, либо доступ к ним через hello API.</span><span class="sxs-lookup"><span data-stu-id="a9cce-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="a9cce-115">**Вопрос. можно получить сведения о журнале действия Office 365 через портал Azure hello**</span><span class="sxs-lookup"><span data-stu-id="a9cce-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="a9cce-116">**Ответ** несмотря на то что действие Office 365 и общей папки журналов Azure AD действия много ресурсов каталога hello, если требуется полное представление Здравствуйте журналы действий Office 365, следует передать сведения о журнале Office 365 действия tooget toohello Центр администрирования Office 365.</span><span class="sxs-lookup"><span data-stu-id="a9cce-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="a9cce-117">**В. какой интерфейсы API использовать tooget сведения о журналах активности Office 365?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="a9cce-118">**Ответ** используйте hello API управления Office 365 tooaccess hello [регистрирует действия Office 365 через API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="a9cce-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="a9cce-119">**Вопрос. Сколько записей можно скачать с портала Azure?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="a9cce-120">**Ответ** можно загрузить too120K записей из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a9cce-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="a9cce-121">Hello записи сортируются по *последних* по умолчанию, вы получаете записи hello последние 120 КБ.</span><span class="sxs-lookup"><span data-stu-id="a9cce-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="a9cce-122">**В. сколько записей можно запросить через hello действия API**</span><span class="sxs-lookup"><span data-stu-id="a9cce-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="a9cce-123">**Ответ** можно запросить too1 миллионов записей (Если вы не используете оператор top hello, сортирующий hello записи с помощью большинства последних).</span><span class="sxs-lookup"><span data-stu-id="a9cce-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="a9cce-124">При использовании оператора «top» hello, можно запросить too500K записей.</span><span class="sxs-lookup"><span data-stu-id="a9cce-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="a9cce-125">Примеры запросов на как toouse hello API, здесь можно найти [здесь](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a9cce-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="a9cce-126">**Вопрос. Как получить лицензию уровня Premium?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="a9cce-127">**Ответ** разделе [Приступая к работе с Azure Active Directory Premium](active-directory-get-started-premium.md) для вопроса toothis ответов.</span><span class="sxs-lookup"><span data-stu-id="a9cce-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="a9cce-128">**Вопрос. Как скоро после получения лицензии Premium я увижу данные действий?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="a9cce-129">**Ответ** Если уже имеются данные действия как бесплатной лицензии, то можно увидеть hello и тех же данных.</span><span class="sxs-lookup"><span data-stu-id="a9cce-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="a9cce-130">Если у вас нет данных, то потребуется один или два дня.</span><span class="sxs-lookup"><span data-stu-id="a9cce-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="a9cce-131">**Вопрос. Увижу ли я данные за прошлый месяц после получения лицензии Azure AD Premium?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="a9cce-132">**Ответ** Если недавно переключения tooa расширенной версии (включая пробной версии), можно будет просматривать данные копии дней too7 изначально.</span><span class="sxs-lookup"><span data-stu-id="a9cce-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="a9cce-133">Собирает данные, появится вверх too30 дней.</span><span class="sxs-lookup"><span data-stu-id="a9cce-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="a9cce-134">**Вопрос есть события риска в защиту учетных данных, но я не вижу соответствующего вход в hello все входы. Так и должно быть?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="a9cce-135">**Ответ**. Да, служба защиты идентификации оценивает степень риска для всех процессов проверки подлинности, как интерактивных, так и неинтерактивных.</span><span class="sxs-lookup"><span data-stu-id="a9cce-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="a9cce-136">Тем не менее все входа в систему только отчете только hello интерактивного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="a9cce-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="a9cce-137">**Вопрос. как можно загрузить отчет «Пользователи с отметкой риск» hello на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="a9cce-138">**Ответ** toodownload параметр hello *пользователей с отметкой риск* скоро будет добавлен отчет.</span><span class="sxs-lookup"><span data-stu-id="a9cce-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="a9cce-139">**Вопрос. как узнать, почему в процесс входа или пользователя были отмечен в hello Azure portal рискованным?**</span><span class="sxs-lookup"><span data-stu-id="a9cce-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="a9cce-140">**Ответ** Premium edition клиентам Дополнительные сведения о hello базового события рисков, щелкнув пользователя hello в «Пользователи с отметкой риск» или щелкнув hello «Рискованные входа в систему».</span><span class="sxs-lookup"><span data-stu-id="a9cce-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="a9cce-141">Выпуск свободного и основные клиенты получали пользователей под риском toosee hello и входа в систему без hello базовые сведения о событиях риска.</span><span class="sxs-lookup"><span data-stu-id="a9cce-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="a9cce-142">**Вопрос. как IP-адреса, вычисляются в hello входов и рискованно входы отчетов??**</span><span class="sxs-lookup"><span data-stu-id="a9cce-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="a9cce-143">**Ответ** IP-адреса, выданные таким образом, что отсутствует определенный подключение между IP-адрес и где физически расположен hello компьютер с таким адресом.</span><span class="sxs-lookup"><span data-stu-id="a9cce-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="a9cce-144">Это осложняется факторы, например мобильные поставщиков и виртуальные частные сети, очень часто выдача IP-адресов из центра пулы далеко от которых фактически используется hello клиентского устройства.</span><span class="sxs-lookup"><span data-stu-id="a9cce-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="a9cce-145">Имея hello выше, преобразование физическое расположение IP адрес tooa — максимум усилий на основе трассировки, данные реестра, обратную просмотров и другие сведения.</span><span class="sxs-lookup"><span data-stu-id="a9cce-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
