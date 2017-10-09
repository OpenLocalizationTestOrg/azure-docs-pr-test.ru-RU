---
title: "aaaTroubleshoot RBAC Azure. | Документы Microsoft"
description: "Справка по проблемам при управлении доступом к ресурсам на основе ролей и ответы на распространенные вопросы."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="4e72d-103">Устранение неполадок при управлении доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="4e72d-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="4e72d-104">В этой статье документа ответы на общие вопросы о hello определенные права доступа, предоставленные с ролями, известно, какие tooexpect при использовании hello ролей в hello портал Azure и устранения неполадок с доступом.</span><span class="sxs-lookup"><span data-stu-id="4e72d-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="4e72d-105">Следующие три роли охватывают все типы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="4e72d-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="4e72d-106">Владелец</span><span class="sxs-lookup"><span data-stu-id="4e72d-106">Owner</span></span>  
* <span data-ttu-id="4e72d-107">участник;</span><span class="sxs-lookup"><span data-stu-id="4e72d-107">Contributor</span></span>  
* <span data-ttu-id="4e72d-108">читатель.</span><span class="sxs-lookup"><span data-stu-id="4e72d-108">Reader</span></span>  

<span data-ttu-id="4e72d-109">Владельцы и сотрудники имеют полный доступ toohello управления возникают, но участник не может предоставить доступ tooother пользователей или групп.</span><span class="sxs-lookup"><span data-stu-id="4e72d-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="4e72d-110">Интереснее немного с hello роль модуля чтения, то есть, где будет потратить некоторое время.</span><span class="sxs-lookup"><span data-stu-id="4e72d-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="4e72d-111">В разделе hello [статье get-started управления доступом на основе ролей](role-based-access-control-configure.md) сведения о том, как получить доступ к toogrant.</span><span class="sxs-lookup"><span data-stu-id="4e72d-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="4e72d-112">Рабочие нагрузки службы приложений</span><span class="sxs-lookup"><span data-stu-id="4e72d-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="4e72d-113">Возможности доступа на запись</span><span class="sxs-lookup"><span data-stu-id="4e72d-113">Write access capabilities</span></span>
<span data-ttu-id="4e72d-114">Если предоставить пользователю доступ только для чтения tooa одного веб-приложения, некоторые компоненты отключены, могут не ожидать.</span><span class="sxs-lookup"><span data-stu-id="4e72d-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="4e72d-115">требуются следующие возможности управления Hello **записи** доступ к веб-приложения tooa (сотрудник или владелец) и не будут доступны в любом сценарии, только для чтения.</span><span class="sxs-lookup"><span data-stu-id="4e72d-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="4e72d-116">Команды (такие как запуск, остановка и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4e72d-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="4e72d-117">Изменение параметров, таких как общие параметры конфигурации, параметры масштабирования, резервного копирования и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="4e72d-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="4e72d-118">Доступ к учетным данным для публикации и другим секретным сведениям, например к параметрам приложений и строкам подключения.</span><span class="sxs-lookup"><span data-stu-id="4e72d-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="4e72d-119">Журналы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="4e72d-119">Streaming logs</span></span>
* <span data-ttu-id="4e72d-120">Конфигурация журналов диагностики.</span><span class="sxs-lookup"><span data-stu-id="4e72d-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="4e72d-121">Консоль (командная строка).</span><span class="sxs-lookup"><span data-stu-id="4e72d-121">Console (command prompt)</span></span>
* <span data-ttu-id="4e72d-122">Активные и недавние развертывания (для локального непрерывного развертывания Git).</span><span class="sxs-lookup"><span data-stu-id="4e72d-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="4e72d-123">Приблизительные затраты.</span><span class="sxs-lookup"><span data-stu-id="4e72d-123">Estimated spend</span></span>
* <span data-ttu-id="4e72d-124">Веб-тесты</span><span class="sxs-lookup"><span data-stu-id="4e72d-124">Web tests</span></span>
* <span data-ttu-id="4e72d-125">Виртуальная сеть (только видимым tooa чтения если виртуальной сети была настроена ранее пользователь с доступом для записи).</span><span class="sxs-lookup"><span data-stu-id="4e72d-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="4e72d-126">Если вы не может получить доступ к любой из этих плиток, необходимо tooask администратору для участника доступ toohello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4e72d-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="4e72d-127">Работа со связанными ресурсами</span><span class="sxs-lookup"><span data-stu-id="4e72d-127">Dealing with related resources</span></span>
<span data-ttu-id="4e72d-128">Веб-приложений осложняется наличие нескольких различных ресурсов, которые взаимозависимость hello.</span><span class="sxs-lookup"><span data-stu-id="4e72d-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="4e72d-129">Вот типичная группа ресурсов, связанная с несколькими веб-сайтами:</span><span class="sxs-lookup"><span data-stu-id="4e72d-129">Here is a typical resource group with a couple websites:</span></span>

![Группа ресурсов веб-приложений](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="4e72d-131">В результате Если вы предоставляете доступ toojust hello веб-приложения, большая часть функций hello на колонки веб-сайта hello в hello портал Azure отключена.</span><span class="sxs-lookup"><span data-stu-id="4e72d-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="4e72d-132">Эти элементы требуется **записи** доступ к toohello **план служб приложений** , соответствующий tooyour веб-сайта:</span><span class="sxs-lookup"><span data-stu-id="4e72d-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="4e72d-133">Просмотр hello веб-приложения в ценовой категории (Free или Standard)</span><span class="sxs-lookup"><span data-stu-id="4e72d-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="4e72d-134">параметры масштабирования (число экземпляров, размер виртуальной машины, настройки автоматического масштабирования);</span><span class="sxs-lookup"><span data-stu-id="4e72d-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="4e72d-135">квоты (квоты хранилища, пропускной способности, ресурсов ЦП).</span><span class="sxs-lookup"><span data-stu-id="4e72d-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="4e72d-136">Эти элементы требуется **записи** toohello доступа всей **группы ресурсов** , содержащий веб-сайта:</span><span class="sxs-lookup"><span data-stu-id="4e72d-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="4e72d-137">Сертификаты SSL и привязки (SSL-сертификаты могут передаваться между сайтами в hello же группу ресурсов и географическое расположение)</span><span class="sxs-lookup"><span data-stu-id="4e72d-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="4e72d-138">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="4e72d-138">Alert rules</span></span>  
* <span data-ttu-id="4e72d-139">параметры автоматического масштабирования;</span><span class="sxs-lookup"><span data-stu-id="4e72d-139">Autoscale settings</span></span>  
* <span data-ttu-id="4e72d-140">компоненты Application Insights;</span><span class="sxs-lookup"><span data-stu-id="4e72d-140">Application insights components</span></span>  
* <span data-ttu-id="4e72d-141">Веб-тесты</span><span class="sxs-lookup"><span data-stu-id="4e72d-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="4e72d-142">Рабочие нагрузки виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4e72d-142">Virtual machine workloads</span></span>
<span data-ttu-id="4e72d-143">Гораздо как для веб-приложений, некоторые функции hello колонке виртуальной машины требуется доступ на запись toohello виртуальной машины, а tooother ресурсы в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="4e72d-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="4e72d-144">Виртуальные машины находятся имена связанных tooDomain, виртуальных сетей, учетные записи хранения и правила оповещений.</span><span class="sxs-lookup"><span data-stu-id="4e72d-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="4e72d-145">Эти элементы требуется **записи** доступ к toohello **виртуальной машины**:</span><span class="sxs-lookup"><span data-stu-id="4e72d-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="4e72d-146">Endpoints</span><span class="sxs-lookup"><span data-stu-id="4e72d-146">Endpoints</span></span>  
* <span data-ttu-id="4e72d-147">IP-адреса;</span><span class="sxs-lookup"><span data-stu-id="4e72d-147">IP addresses</span></span>  
* <span data-ttu-id="4e72d-148">диски;</span><span class="sxs-lookup"><span data-stu-id="4e72d-148">Disks</span></span>  
* <span data-ttu-id="4e72d-149">расширения.</span><span class="sxs-lookup"><span data-stu-id="4e72d-149">Extensions</span></span>  

<span data-ttu-id="4e72d-150">Эти обновления требуют **записи** hello доступа tooboth **виртуальной машины**и hello **группы ресурсов** (вместе с hello доменное имя), что он находится в:</span><span class="sxs-lookup"><span data-stu-id="4e72d-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="4e72d-151">группа доступности;</span><span class="sxs-lookup"><span data-stu-id="4e72d-151">Availability set</span></span>  
* <span data-ttu-id="4e72d-152">набор балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="4e72d-152">Load balanced set</span></span>  
* <span data-ttu-id="4e72d-153">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="4e72d-153">Alert rules</span></span>  

<span data-ttu-id="4e72d-154">Если вы не может получить доступ к любой из этих плиток, обратитесь к администратору для группы ресурсов toohello доступа участника.</span><span class="sxs-lookup"><span data-stu-id="4e72d-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="4e72d-155">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="4e72d-155">See more</span></span>
* <span data-ttu-id="4e72d-156">[Управление доступом на основе ролей](role-based-access-control-configure.md): Приступая к работе с RBAC в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4e72d-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="4e72d-157">[Встроенные роли](role-based-access-built-in-roles.md): получение сведений о ролях hello, которые поставляются в RBAC.</span><span class="sxs-lookup"><span data-stu-id="4e72d-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="4e72d-158">[Пользовательские роли в Azure RBAC](role-based-access-control-custom-roles.md): Узнайте, как toofit toocreate пользовательские роли доступ к должен.</span><span class="sxs-lookup"><span data-stu-id="4e72d-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="4e72d-159">[Создание отчета по журналу изменений доступа](role-based-access-control-access-change-history-report.md). Отслеживание изменения назначений ролей в RBAC.</span><span class="sxs-lookup"><span data-stu-id="4e72d-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

