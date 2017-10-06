---
title: "брандмауэр веб-приложения в центр безопасности Azure aaaAdd | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** добавьте web приложение брандмауэра ** и ** Finalize приложения защиты **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="de528-103">Добавление брандмауэра веб-приложения в Центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="de528-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="de528-104">Центр безопасности Azure может рекомендуем добавить брандмауэр веб-приложения (WAF) от партнера Майкрософт toosecure веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="de528-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner toosecure your web applications.</span></span> <span data-ttu-id="de528-105">В этом документе описан процесс пример tooapply этой рекомендации.</span><span class="sxs-lookup"><span data-stu-id="de528-105">This document walks you through an example of how tooapply this recommendation.</span></span>

<span data-ttu-id="de528-106">Рекомендация развернуть WAF отображается для любого общедоступного IP-адреса (IP-адреса уровня экземпляра или IP-адреса с балансировкой нагрузки), имеющего связанную группу безопасности сети с открытыми входящими веб-портами (80, 443).</span><span class="sxs-lookup"><span data-stu-id="de528-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="de528-107">Центр обеспечения безопасности, корпорация Майкрософт рекомендует, что подготовки WAF toohelp защиту от атак на веб-приложений на виртуальных машинах и в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="de528-107">Security Center recommends that you provision a WAF toohelp defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="de528-108">Среда службы приложений (ASE) — это параметр плана обслуживания [Премиум](https://azure.microsoft.com/pricing/details/app-service/) в службе приложений Azure. Она обеспечивает полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="de528-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="de528-109">toolearn Дополнительные сведения о ASE, в разделе hello [документация среды службы приложения](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="de528-109">toolearn more about ASE, see hello [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="de528-110">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="de528-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="de528-111">Этот документ не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="de528-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="de528-112">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="de528-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="de528-113">В hello **рекомендации** колонке выберите **защитить веб-приложение, используя брандмауэр веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="de528-113">In hello **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="de528-114">![Защищенное веб-приложение][1]</span><span class="sxs-lookup"><span data-stu-id="de528-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="de528-115">В hello **защиты веб-приложений с помощью брандмауэр веб-приложения** колонке выберите веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="de528-115">In hello **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="de528-116">Hello **добавьте брандмауэр веб-приложения** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="de528-116">hello **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="de528-117">![Добавление брандмауэра веб-приложения][2]</span><span class="sxs-lookup"><span data-stu-id="de528-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="de528-118">Вы можете toouse существующие брандмауэр веб-приложения при наличии или можно создать новую.</span><span class="sxs-lookup"><span data-stu-id="de528-118">You can choose toouse an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="de528-119">В этом примере нет доступных WAF, поэтому мы его создадим.</span><span class="sxs-lookup"><span data-stu-id="de528-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="de528-120">toocreate WAF, выберите решение из списка hello интеграции партнеров.</span><span class="sxs-lookup"><span data-stu-id="de528-120">toocreate a WAF, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="de528-121">В этом примере выберите **Barracuda Web Application Firewall**.</span><span class="sxs-lookup"><span data-stu-id="de528-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="de528-122">Hello **брандмауэр Barracuda веб-приложения** открывает колонку обеспечивает сведения о решении hello партнера.</span><span class="sxs-lookup"><span data-stu-id="de528-122">hello **Barracuda Web Application Firewall** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="de528-123">Выберите **создать** в колонке сведения hello.</span><span class="sxs-lookup"><span data-stu-id="de528-123">Select **Create** in hello information blade.</span></span>

   ![Колонка со сведениями о брандмауэре][3]

6. <span data-ttu-id="de528-125">Hello **новый брандмауэр веб-приложения** открывает колонку, где можно выполнить **конфигурацию виртуальной Машины** шаги, чтобы предоставить **WAF сведения**.</span><span class="sxs-lookup"><span data-stu-id="de528-125">hello **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="de528-126">Выберите **Конфигурация виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="de528-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="de528-127">В hello **конфигурацию виртуальной Машины** колонки, введите сведения, необходимые toospin hello виртуальной машины, работающей hello WAF.</span><span class="sxs-lookup"><span data-stu-id="de528-127">In hello **VM Configuration** blade, you enter information required toospin up hello virtual machine that runs hello WAF.</span></span>
   <span data-ttu-id="de528-128">![VM configuration][4]</span><span class="sxs-lookup"><span data-stu-id="de528-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="de528-129">Вернуть toohello **новый брандмауэр веб-приложения** и выберите **WAF сведения**.</span><span class="sxs-lookup"><span data-stu-id="de528-129">Return toohello **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="de528-130">В hello **WAF сведения** колонке Настройка WAF hello сам.</span><span class="sxs-lookup"><span data-stu-id="de528-130">In hello **WAF Information** blade, you configure hello WAF itself.</span></span> <span data-ttu-id="de528-131">Шаг 7 позволяет tooconfigure hello виртуальной машины, на какие hello WAF запуски и шаг 8 позволяет hello tooprovision WAF сам.</span><span class="sxs-lookup"><span data-stu-id="de528-131">Step 7 allows you tooconfigure hello virtual machine on which hello WAF runs and step 8 enables you tooprovision hello WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="de528-132">Завершение подготовки защиты приложений</span><span class="sxs-lookup"><span data-stu-id="de528-132">Finalize application protection</span></span>
1. <span data-ttu-id="de528-133">Вернуть toohello **рекомендации** колонку.</span><span class="sxs-lookup"><span data-stu-id="de528-133">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="de528-134">Была создана новая запись после создания WAF hello, вызывается **завершить подготовку защиты приложения**.</span><span class="sxs-lookup"><span data-stu-id="de528-134">A new entry was generated after you created hello WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="de528-135">Эта запись позволяет узнать необходимые toocomplete hello процесс фактически подключения вверх hello WAF внутри hello виртуальной сети Azure, чтобы его можно защищать приложения hello.</span><span class="sxs-lookup"><span data-stu-id="de528-135">This entry lets you know that you need toocomplete hello process of actually wiring up hello WAF within hello Azure Virtual Network so that it can protect hello application.</span></span>

   ![Завершение подготовки защиты приложений][5]

2. <span data-ttu-id="de528-137">Выберите **Завершение подготовки защиты приложений**.</span><span class="sxs-lookup"><span data-stu-id="de528-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="de528-138">Откроется новая панель.</span><span class="sxs-lookup"><span data-stu-id="de528-138">A new blade opens.</span></span> <span data-ttu-id="de528-139">Вы увидите, что имеется веб-приложения, который должен toohave свой трафик пересылаются.</span><span class="sxs-lookup"><span data-stu-id="de528-139">You can see that there is a web application that needs toohave its traffic rerouted.</span></span>
3. <span data-ttu-id="de528-140">Выберите веб-приложение hello.</span><span class="sxs-lookup"><span data-stu-id="de528-140">Select hello web application.</span></span> <span data-ttu-id="de528-141">Откроется панель приведены пошаговые инструкции для доработки Настройка брандмауэра для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="de528-141">A blade opens that gives you steps for finalizing hello web application firewall setup.</span></span> <span data-ttu-id="de528-142">Выполните шаги hello, а затем выберите **трафика**.</span><span class="sxs-lookup"><span data-stu-id="de528-142">Complete hello steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="de528-143">Центр обеспечения безопасности hello коммутируемого подключения автоматически.</span><span class="sxs-lookup"><span data-stu-id="de528-143">Security Center then does hello wiring-up for you.</span></span>

   ![Ограничение трафика][6]

> [!NOTE]
> <span data-ttu-id="de528-145">Вы можете защитить несколько веб-приложений в центре безопасности, добавив эти приложения tooyour существующие WAF развертывания.</span><span class="sxs-lookup"><span data-stu-id="de528-145">You can protect multiple web applications in Security Center by adding these applications tooyour existing WAF deployments.</span></span>
>
>

<span data-ttu-id="de528-146">Теперь полностью интегрирован Hello журналы с этой WAF.</span><span class="sxs-lookup"><span data-stu-id="de528-146">hello logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="de528-147">Центр обеспечения безопасности можно запустить автоматически сбор и анализ журналов hello, чтобы его можно выявить tooyou предупреждения системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="de528-147">Security Center can start automatically gathering and analyzing hello logs so that it can surface important security alerts tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de528-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de528-148">Next steps</span></span>
<span data-ttu-id="de528-149">В этом документе показано, как tooimplement hello рекомендации центра обеспечения безопасности «Добавить веб-приложение».</span><span class="sxs-lookup"><span data-stu-id="de528-149">This document showed you how tooimplement hello Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="de528-150">toolearn подробные сведения о настройке брандмауэр веб-приложения, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="de528-150">toolearn more about configuring a web application firewall, see hello following:</span></span>

* [<span data-ttu-id="de528-151">Настройка брандмауэра веб-приложения (WAF) для среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="de528-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="de528-152">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="de528-152">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="de528-153">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="de528-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="de528-154">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="de528-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="de528-155">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="de528-155">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="de528-156">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="de528-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="de528-157">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="de528-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="de528-158">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="de528-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
