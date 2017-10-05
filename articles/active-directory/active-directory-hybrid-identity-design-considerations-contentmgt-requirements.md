---
title: "Рекомендации по разработке архитектуры гибридной идентификации в Azure Active Directory ― определение требований к управлению содержимым | Документация Майкрософт"
description: "Содержит информацию о том, как определить требования к управлению содержимым для вашего бизнеса. Обычно когда у пользователя есть собственное устройство, он также может иметь несколько учетных записей, которые изменяются в зависимости от используемого приложения. Важно различать, какое содержимое было создано с помощью личных учетных данных и какое — с помощью корпоративных учетных данных. Ваше решение для идентификации должно иметь возможность взаимодействия с облачной службой для обеспечения эффективной работы конечного пользователя и одновременной защиты его конфиденциальности и усиления защиты от утечки данных."
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
ms.openlocfilehash: 840de1e1fcba74285788d51d8f544375f0affa77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="20d14-106">Определение требований к управлению содержимым для решения гибридной идентификации</span><span class="sxs-lookup"><span data-stu-id="20d14-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="20d14-107">Понимание требований управления содержимым для вашего бизнеса может напрямую повлиять на то, каким решением для гибридной идентификации воспользоваться.</span><span class="sxs-lookup"><span data-stu-id="20d14-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="20d14-108">С распространением большого количества устройств и возможностью пользователей приносить собственные устройства ([BYOD](http://aka.ms/byodcg)) компания должна защищать свои собственные данные, но также сохранять и конфиденциальность пользователя.</span><span class="sxs-lookup"><span data-stu-id="20d14-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="20d14-109">Обычно когда у пользователя есть собственное устройство, он также может иметь несколько учетных записей, которые изменяются в зависимости от используемого приложения.</span><span class="sxs-lookup"><span data-stu-id="20d14-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="20d14-110">Важно различать, какое содержимое было создано с помощью личных учетных данных и какое — с помощью корпоративных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="20d14-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="20d14-111">Ваше решение для идентификации должно иметь возможность взаимодействия с облачной службой для обеспечения эффективной работы конечного пользователя и одновременной защиты его конфиденциальности и усиления защиты от утечки данных.</span><span class="sxs-lookup"><span data-stu-id="20d14-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="20d14-112">Ваше решение для идентификации будет использоваться различными техническими компонентами для управления содержимым, как показано на рисунке ниже:</span><span class="sxs-lookup"><span data-stu-id="20d14-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="20d14-113">**Элементы управления безопасности, которые будут использовать вашу систему управления идентификацией**</span><span class="sxs-lookup"><span data-stu-id="20d14-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="20d14-114">В общем случае требования к управлению содержимым будет использовать вашу систему управления идентификацией в следующих областях:</span><span class="sxs-lookup"><span data-stu-id="20d14-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="20d14-115">Конфиденциальность: идентификация пользователя, которому принадлежит ресурс, и применение соответствующих элементов управления для сохранения целостности данных.</span><span class="sxs-lookup"><span data-stu-id="20d14-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="20d14-116">Классификация данных: идентификация пользователя или группы и уровня доступа к объекту в соответствии с его классификацией.</span><span class="sxs-lookup"><span data-stu-id="20d14-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="20d14-117">Защита от утечки данных: элементы управления безопасности, отвечающие за защиту данных во избежание утечки, должны взаимодействовать с системой идентификации для проверки удостоверения пользователя.</span><span class="sxs-lookup"><span data-stu-id="20d14-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="20d14-118">Это также важно для аудита.</span><span class="sxs-lookup"><span data-stu-id="20d14-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="20d14-119">Дополнительная информация о рекомендациях и руководствах по классификации данных содержится в статье [Классификация данных для обеспечения готовности облака](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) .</span><span class="sxs-lookup"><span data-stu-id="20d14-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="20d14-120">При планировании гибридного решения для идентификации обязательно дайте ответы на следующие вопросы в соответствии с требованиями вашей организации:</span><span class="sxs-lookup"><span data-stu-id="20d14-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="20d14-121">Имеет ли ваша компания средства управления безопасностью для обеспечения конфиденциальности данных?</span><span class="sxs-lookup"><span data-stu-id="20d14-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="20d14-122">Если да, то можно ли интегрировать эти средства с решением для гибридной идентификации, которое вы собираетесь применить?</span><span class="sxs-lookup"><span data-stu-id="20d14-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="20d14-123">Пользуется ли ваша компания классификацией данных?</span><span class="sxs-lookup"><span data-stu-id="20d14-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="20d14-124">Если да, то можно ли интегрировать текущее решение с решением для гибридной идентификации, которое вы собираетесь применить?</span><span class="sxs-lookup"><span data-stu-id="20d14-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="20d14-125">Есть ли у вашей компании какое-либо решение для борьбы с утечкой данных?</span><span class="sxs-lookup"><span data-stu-id="20d14-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="20d14-126">Если да, то можно ли интегрировать текущее решение с решением для гибридной идентификации, которое вы собираетесь применить?</span><span class="sxs-lookup"><span data-stu-id="20d14-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="20d14-127">Нужно ли вашей компании вести аудит доступа к ресурсам?</span><span class="sxs-lookup"><span data-stu-id="20d14-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="20d14-128">Если да, то для какого типа ресурсов?</span><span class="sxs-lookup"><span data-stu-id="20d14-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="20d14-129">Если да, то какой уровень информирования необходим?</span><span class="sxs-lookup"><span data-stu-id="20d14-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="20d14-130">Если да, то где должен располагаться журнал аудита?</span><span class="sxs-lookup"><span data-stu-id="20d14-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="20d14-131">Локально или в облаке?</span><span class="sxs-lookup"><span data-stu-id="20d14-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="20d14-132">Требуется ли для шифрование сообщений электронной почты, содержащих конфиденциальные данные (SSN, номера кредитных карт и т. д.)?</span><span class="sxs-lookup"><span data-stu-id="20d14-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="20d14-133">Нужно ли шифровать все документы и содержимое, которыми ваша компания обменивается с внешними деловыми партнерами?</span><span class="sxs-lookup"><span data-stu-id="20d14-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="20d14-134">Нужно ли вашей компании внедрить корпоративные политики для определенного типа сообщений электронной почты (не отвечать всем, не перенаправлять)?</span><span class="sxs-lookup"><span data-stu-id="20d14-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="20d14-135">Составьте письменный ответ на каждый вопрос и убедитесь, что он логически обоснован.</span><span class="sxs-lookup"><span data-stu-id="20d14-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="20d14-136">[Определение стратегии защиты данных](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) .</span><span class="sxs-lookup"><span data-stu-id="20d14-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="20d14-137">Ответив на эти вопросы, вы сможете выбрать тот вариант, который лучше всего подходит для вашего бизнеса.</span><span class="sxs-lookup"><span data-stu-id="20d14-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="20d14-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20d14-138">Next steps</span></span>
[<span data-ttu-id="20d14-139">Определение требований к контролю доступа</span><span class="sxs-lookup"><span data-stu-id="20d14-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="20d14-140">См. также</span><span class="sxs-lookup"><span data-stu-id="20d14-140">See Also</span></span>
[<span data-ttu-id="20d14-141">Обзор рекомендаций по проектированию</span><span class="sxs-lookup"><span data-stu-id="20d14-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

