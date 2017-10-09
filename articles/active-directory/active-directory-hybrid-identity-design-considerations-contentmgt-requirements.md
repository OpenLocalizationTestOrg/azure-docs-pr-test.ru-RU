---
title: "Вопросы проектирования identity гибридных Active Directory aaaAzure - определить требования к управлению содержимым | Документы Microsoft"
description: "Позволяет контролировать способ toodetermine hello управления содержимым требований бизнеса. Обычно пользователь имеет свой собственный устройства он может иметь также несколько учетные данные, которые будут чередующихся соответствующим toohello приложение, которое он использует. Это важные toodifferentiate какие содержимое было создано с использованием личных учетных данных и hello из них, созданных с помощью корпоративных учетных данных. Решение удостоверение должно быть может toointeract с tooprovide облачных служб конечного пользователя toohello легкое взаимодействие при его защиту и увеличить hello защиты от утечки данных."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="bcf80-106">Определение требований к управлению содержимым для решения гибридной идентификации</span><span class="sxs-lookup"><span data-stu-id="bcf80-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="bcf80-107">Управление содержимым hello общее представление о требованиях для вашей организации могут направлять повлиять на решение на какие toouse гибридное удостоверение решения.</span><span class="sxs-lookup"><span data-stu-id="bcf80-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="bcf80-108">С hello распространение несколько устройств и возможности пользователей toobring hello свои собственные устройства ([BYOD](http://aka.ms/byodcg)), hello компании должны защищать свои собственные данные, но его также необходимо сохранить конфиденциальность пользователя без изменений.</span><span class="sxs-lookup"><span data-stu-id="bcf80-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="bcf80-109">Обычно пользователь имеет свой собственный устройства он может иметь также несколько учетные данные, которые будут чередующихся соответствующим toohello приложение, которое он использует.</span><span class="sxs-lookup"><span data-stu-id="bcf80-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="bcf80-110">Это важные toodifferentiate какие содержимое было создано с использованием личных учетных данных и hello из них, созданных с помощью корпоративных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="bcf80-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="bcf80-111">Решение удостоверение должно быть может toointeract с tooprovide облачных служб конечного пользователя toohello легкое взаимодействие при его защиту и увеличить hello защиты от утечки данных.</span><span class="sxs-lookup"><span data-stu-id="bcf80-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="bcf80-112">Решении для удостоверений будет использоваться в различных технических средств в управление содержимым tooprovide заказ как показано на следующем рисунке hello:</span><span class="sxs-lookup"><span data-stu-id="bcf80-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="bcf80-113">**Элементы управления безопасности, которые будут использовать вашу систему управления идентификацией**</span><span class="sxs-lookup"><span data-stu-id="bcf80-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="bcf80-114">В общем случае требования к управлению содержимым будет использовать вашей системой управления удостоверениями в hello в следующих областях:</span><span class="sxs-lookup"><span data-stu-id="bcf80-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="bcf80-115">Конфиденциальность: Идентификация hello пользователь, владеющий ресурсом и применение целостности toomaintain hello соответствующие элементы управления.</span><span class="sxs-lookup"><span data-stu-id="bcf80-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="bcf80-116">Классификация данных: Определите hello пользователя или группы и уровне в соответствии с классификацией tooits объекта tooan доступа.</span><span class="sxs-lookup"><span data-stu-id="bcf80-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="bcf80-117">Защита от утечки данных: управление безопасностью, ответственность за защиту tooavoid утечки данных потребуется toointeract с идентификатором hello удостоверения toovalidate hello пользователя системы.</span><span class="sxs-lookup"><span data-stu-id="bcf80-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="bcf80-118">Это также важно для аудита.</span><span class="sxs-lookup"><span data-stu-id="bcf80-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="bcf80-119">Дополнительная информация о рекомендациях и руководствах по классификации данных содержится в статье [Классификация данных для обеспечения готовности облака](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) .</span><span class="sxs-lookup"><span data-stu-id="bcf80-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="bcf80-120">При планировании гибридного решения для удостоверений убедитесь, hello следующие ответы в соответствии с требованиями организации tooyour:</span><span class="sxs-lookup"><span data-stu-id="bcf80-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="bcf80-121">Имеется средства безопасности в компании конфиденциальность данных tooenforce месте?</span><span class="sxs-lookup"><span data-stu-id="bcf80-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="bcf80-122">Если Да, эти элементы управления безопасности будет может toointegrate с hello гибридного решения по идентификации, которые будет tooadopt?</span><span class="sxs-lookup"><span data-stu-id="bcf80-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="bcf80-123">Пользуется ли ваша компания классификацией данных?</span><span class="sxs-lookup"><span data-stu-id="bcf80-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="bcf80-124">Если Да, то есть hello текущее решение будет toointegrate с hello гибридного решения по идентификации, которые будет tooadopt?</span><span class="sxs-lookup"><span data-stu-id="bcf80-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="bcf80-125">Есть ли у вашей компании какое-либо решение для борьбы с утечкой данных?</span><span class="sxs-lookup"><span data-stu-id="bcf80-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="bcf80-126">Если Да, то есть hello текущее решение будет toointegrate с hello гибридного решения по идентификации, которые будет tooadopt?</span><span class="sxs-lookup"><span data-stu-id="bcf80-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="bcf80-127">Требуется ли вашей компании tooresources tooaudit доступа?</span><span class="sxs-lookup"><span data-stu-id="bcf80-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="bcf80-128">Если да, то для какого типа ресурсов?</span><span class="sxs-lookup"><span data-stu-id="bcf80-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="bcf80-129">Если да, то какой уровень информирования необходим?</span><span class="sxs-lookup"><span data-stu-id="bcf80-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="bcf80-130">Если Да, где должны размещаться hello журнал аудита?</span><span class="sxs-lookup"><span data-stu-id="bcf80-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="bcf80-131">Локально или в облаке hello?</span><span class="sxs-lookup"><span data-stu-id="bcf80-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="bcf80-132">Нужна ли вашей компании tooencrypt все сообщения электронной почты, содержащие конфиденциальные данные (SSN, номера кредитных карт и т. д)?</span><span class="sxs-lookup"><span data-stu-id="bcf80-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="bcf80-133">Нужна ли вашей компании tooencrypt все документы или содержимое совместно с внешними партнерами?</span><span class="sxs-lookup"><span data-stu-id="bcf80-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="bcf80-134">Нужна ли вашей компании tooenforce корпоративных политик на некоторые виды сообщений электронной почты (все ответ, не пересылать)?</span><span class="sxs-lookup"><span data-stu-id="bcf80-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="bcf80-135">Убедитесь, что заметки tootake все ответы и постарайтесь понять hello стоит за hello ответов.</span><span class="sxs-lookup"><span data-stu-id="bcf80-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="bcf80-136">[Определение стратегии защиты данных](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) будут рассмотрены доступные варианты hello, а также преимущества и недостатки каждого варианта.</span><span class="sxs-lookup"><span data-stu-id="bcf80-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="bcf80-137">Ответив на эти вопросы, вы сможете выбрать тот вариант, который лучше всего подходит для вашего бизнеса.</span><span class="sxs-lookup"><span data-stu-id="bcf80-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="bcf80-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bcf80-138">Next steps</span></span>
[<span data-ttu-id="bcf80-139">Определение требований к контролю доступа</span><span class="sxs-lookup"><span data-stu-id="bcf80-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="bcf80-140">См. также</span><span class="sxs-lookup"><span data-stu-id="bcf80-140">See Also</span></span>
[<span data-ttu-id="bcf80-141">Обзор рекомендаций по проектированию</span><span class="sxs-lookup"><span data-stu-id="bcf80-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

