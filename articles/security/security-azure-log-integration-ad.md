---
title: "aaaAzure журнала интеграция с журналы аудита Azure Active Directory | Документы Microsoft"
description: "Узнайте, как tooinstall hello службы интеграции журналов Azure и интегрировать журналы из журналов аудита Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="72da9-103">Интеграция журналов аудита Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72da9-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="72da9-104">События аудита Azure Active Directory (Azure AD) помогают определить привилегированные действия, выполняемые в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="72da9-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="72da9-105">Можно просматривать hello типы событий, которые можно отследить, просмотрев [события отчетов аудита Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="72da9-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="72da9-106">Прежде чем hello действия, описанные в этой статье, необходимо просмотреть hello [начать](security-azure-log-integration-get-started.md) статью и завершить там шаги hello.</span><span class="sxs-lookup"><span data-stu-id="72da9-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="72da9-107">Журналы аудита Azure Active directory toointegrate действия</span><span class="sxs-lookup"><span data-stu-id="72da9-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="72da9-108">Откройте командную строку hello и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72da9-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="72da9-109">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72da9-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="72da9-110">Эта команда запрашивает имя для входа Azure.</span><span class="sxs-lookup"><span data-stu-id="72da9-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="72da9-111">Hello команда создает Azure Active Directory участника-службы в клиентов hello Azure AD, на которых размещены hello в какой hello вошедшего в систему пользователя — администратора, соадминистратора или владелец подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="72da9-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="72da9-112">Hello команда завершится ошибкой, если hello вошедшего в систему пользователя только пользователя guest в клиенте Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="72da9-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="72da9-113">TooAzure проверка подлинности выполняется с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72da9-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="72da9-114">При создании субъекта-службы для интеграции Azure журнала создается hello удостоверений Azure AD, которому дано tooread доступ из подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="72da9-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="72da9-115">Запустите следующие команды tooprovide hello свой идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="72da9-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="72da9-116">Требуется член toobe hello клиента администратора роли toorun hello команды.</span><span class="sxs-lookup"><span data-stu-id="72da9-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="72da9-117">Пример:</span><span class="sxs-lookup"><span data-stu-id="72da9-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="72da9-118">Убедитесь, что в них создаются следующие папки tooconfirm, hello файлы JSON журналов аудита Azure Active Directory hello:</span><span class="sxs-lookup"><span data-stu-id="72da9-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="72da9-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="72da9-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="72da9-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="72da9-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="72da9-121">Hello следующем видеоролике показано hello шаги, описанные в данной статье:</span><span class="sxs-lookup"><span data-stu-id="72da9-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="72da9-122">За инструкциями по приведению hello сведения в файлах JSON hello в сведения о безопасности и системных событий управления (SIEM) обратитесь к поставщику SIEM.</span><span class="sxs-lookup"><span data-stu-id="72da9-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="72da9-123">Помощь сообщества доступна через hello [форум MSDN интеграции Azure журнала](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="72da9-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="72da9-124">Этот форум позволяет пользователям в toosupport сообщества интеграции Azure журнала hello, друг с другом в вопросы, ответы, советы и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="72da9-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="72da9-125">Кроме того команды hello интеграции журналов Azure отслеживает этот форум и помогает всякий раз, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="72da9-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="72da9-126">Можно также отправить [запрос в службу поддержки](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="72da9-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="72da9-127">Выберите **интеграции журнала** как служба hello, для которого запрашивается поддержка.</span><span class="sxs-lookup"><span data-stu-id="72da9-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72da9-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="72da9-128">Next steps</span></span>
<span data-ttu-id="72da9-129">toolearn Дополнительные сведения о журнале интеграции Azure, см.:</span><span class="sxs-lookup"><span data-stu-id="72da9-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="72da9-130">[Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) (Служба интеграции журналов Microsoft Azure). На этой странице Центра загрузки можно получить дополнительные сведения, изучить требования к системе и получить инструкции по установке службы интеграции журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="72da9-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="72da9-131">[Введение tooAzure интеграции журнала](security-azure-log-integration-overview.md): в этой статье описаны tooAzure интеграции журнала, его основные возможности и как он работает.</span><span class="sxs-lookup"><span data-stu-id="72da9-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="72da9-132">[Действия по настройке партнера](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): в этой записи блога показано, как решения Splunk, разработанное HP и IBM QRadar партнеров tooconfigure toowork интеграции Azure журнала с.</span><span class="sxs-lookup"><span data-stu-id="72da9-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="72da9-133">[Интеграция журналов Azure: часто задаваемые вопросы](security-azure-log-integration-faq.md). В этой статье содержатся ответы на часто задаваемые вопросы об интеграции журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="72da9-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="72da9-134">[Интеграция с интеграцией журнала Azure оповещения центра обеспечения безопасности](../security-center/security-center-integrating-alerts-with-log-integration.md): в этой статье показано, как оповещения центра обеспечения безопасности toosync, вместе с собранными диагностики Azure и журналы аудита Azure, с помощью вашей аналитики журналов событий безопасности виртуальной машины или Решения SIEM.</span><span class="sxs-lookup"><span data-stu-id="72da9-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="72da9-135">[Новые возможности диагностики Azure и Azure журналы аудита](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): в этой записи блога представлены tooAzure журналы аудита, а также другие средства, помогающие анализировать hello операций с ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="72da9-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
