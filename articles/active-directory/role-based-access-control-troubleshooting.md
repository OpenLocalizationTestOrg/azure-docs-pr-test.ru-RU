---
title: "Устранение неполадок управления доступом на основе ролей Azure | Документация Майкрософт"
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
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="24f84-103">Устранение неполадок при управлении доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="24f84-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="24f84-104">В этой статье содержатся ответы на часто задаваемые вопросы об определенных правах доступа, которые предоставляются с помощью ролей. Вы узнаете, какие ситуации возможны при использовании ролей на портале Azure, а также сможете устранить неполадки, связанные с доступом.</span><span class="sxs-lookup"><span data-stu-id="24f84-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="24f84-105">Следующие три роли охватывают все типы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="24f84-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="24f84-106">Владелец</span><span class="sxs-lookup"><span data-stu-id="24f84-106">Owner</span></span>  
* <span data-ttu-id="24f84-107">участник;</span><span class="sxs-lookup"><span data-stu-id="24f84-107">Contributor</span></span>  
* <span data-ttu-id="24f84-108">читатель.</span><span class="sxs-lookup"><span data-stu-id="24f84-108">Reader</span></span>  

<span data-ttu-id="24f84-109">Владельцы и участники обладают полным доступом к действиям по управлению, но участник не может предоставлять доступ другим пользователям или группам.</span><span class="sxs-lookup"><span data-stu-id="24f84-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="24f84-110">С ролью читателя не все так просто, поэтому мы уделим ей больше внимания.</span><span class="sxs-lookup"><span data-stu-id="24f84-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="24f84-111">Дополнительные сведения о предоставлении доступа см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24f84-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="24f84-112">Рабочие нагрузки службы приложений</span><span class="sxs-lookup"><span data-stu-id="24f84-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="24f84-113">Возможности доступа на запись</span><span class="sxs-lookup"><span data-stu-id="24f84-113">Write access capabilities</span></span>
<span data-ttu-id="24f84-114">Если предоставить пользователю доступ только для чтения к одному веб-приложению, некоторые компоненты могут неожиданно отключиться.</span><span class="sxs-lookup"><span data-stu-id="24f84-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="24f84-115">Перечисленные ниже возможности управления требуют доступа к веб-приложению с правом **записи** (роль участника или владельца), поэтому они недоступны при наличии прав только на чтение.</span><span class="sxs-lookup"><span data-stu-id="24f84-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="24f84-116">Команды (такие как запуск, остановка и т. д.).</span><span class="sxs-lookup"><span data-stu-id="24f84-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="24f84-117">Изменение параметров, таких как общие параметры конфигурации, параметры масштабирования, резервного копирования и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="24f84-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="24f84-118">Доступ к учетным данным для публикации и другим секретным сведениям, например к параметрам приложений и строкам подключения.</span><span class="sxs-lookup"><span data-stu-id="24f84-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="24f84-119">Журналы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="24f84-119">Streaming logs</span></span>
* <span data-ttu-id="24f84-120">Конфигурация журналов диагностики.</span><span class="sxs-lookup"><span data-stu-id="24f84-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="24f84-121">Консоль (командная строка).</span><span class="sxs-lookup"><span data-stu-id="24f84-121">Console (command prompt)</span></span>
* <span data-ttu-id="24f84-122">Активные и недавние развертывания (для локального непрерывного развертывания Git).</span><span class="sxs-lookup"><span data-stu-id="24f84-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="24f84-123">Приблизительные затраты.</span><span class="sxs-lookup"><span data-stu-id="24f84-123">Estimated spend</span></span>
* <span data-ttu-id="24f84-124">Веб-тесты</span><span class="sxs-lookup"><span data-stu-id="24f84-124">Web tests</span></span>
* <span data-ttu-id="24f84-125">Виртуальная сеть (видна читателю только в том случае, если ранее была настроена пользователем с доступом на запись).</span><span class="sxs-lookup"><span data-stu-id="24f84-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="24f84-126">Если у вас нет доступа ни к одной из этих плиток, попросите администратора предоставить вам доступ к веб-приложению с правами участника.</span><span class="sxs-lookup"><span data-stu-id="24f84-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="24f84-127">Работа со связанными ресурсами</span><span class="sxs-lookup"><span data-stu-id="24f84-127">Dealing with related resources</span></span>
<span data-ttu-id="24f84-128">Работа с веб-приложениями осложняется наличием нескольких взаимосвязанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24f84-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="24f84-129">Вот типичная группа ресурсов, связанная с несколькими веб-сайтами:</span><span class="sxs-lookup"><span data-stu-id="24f84-129">Here is a typical resource group with a couple websites:</span></span>

![Группа ресурсов веб-приложений](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="24f84-131">В результате, если вы предоставите кому-либо доступ только к веб-приложению, многие функции в колонке веб-сайта на портале Azure будут отключены.</span><span class="sxs-lookup"><span data-stu-id="24f84-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="24f84-132">Для этих элементов требуется доступ на **запись** к **плану службы приложений**, который соответствует вашему веб-сайту:</span><span class="sxs-lookup"><span data-stu-id="24f84-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="24f84-133">просмотр ценовой категории веб-приложения (например "Бесплатный" или "Стандартный");</span><span class="sxs-lookup"><span data-stu-id="24f84-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="24f84-134">параметры масштабирования (число экземпляров, размер виртуальной машины, настройки автоматического масштабирования);</span><span class="sxs-lookup"><span data-stu-id="24f84-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="24f84-135">квоты (квоты хранилища, пропускной способности, ресурсов ЦП).</span><span class="sxs-lookup"><span data-stu-id="24f84-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="24f84-136">Элементы, требующие доступа на **запись** ко всей **группе ресурсов**, которая содержит веб-сайт:</span><span class="sxs-lookup"><span data-stu-id="24f84-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="24f84-137">SSL-сертификаты и привязки (SSL-сертификаты могут совместно использоваться сайтами, относящимися к одной группе ресурсов и находящимися в одном географическом расположении);</span><span class="sxs-lookup"><span data-stu-id="24f84-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="24f84-138">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="24f84-138">Alert rules</span></span>  
* <span data-ttu-id="24f84-139">параметры автоматического масштабирования;</span><span class="sxs-lookup"><span data-stu-id="24f84-139">Autoscale settings</span></span>  
* <span data-ttu-id="24f84-140">компоненты Application Insights;</span><span class="sxs-lookup"><span data-stu-id="24f84-140">Application insights components</span></span>  
* <span data-ttu-id="24f84-141">Веб-тесты</span><span class="sxs-lookup"><span data-stu-id="24f84-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="24f84-142">Рабочие нагрузки виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="24f84-142">Virtual machine workloads</span></span>
<span data-ttu-id="24f84-143">Как и в случае с веб-приложениями, для некоторых функций в колонке виртуальной машины нужен доступ к виртуальной машине или другим ресурсам в группе ресурсов с правами на запись.</span><span class="sxs-lookup"><span data-stu-id="24f84-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="24f84-144">Виртуальные машины связаны с доменными именами, виртуальными сетями, учетными записями хранения и правилами оповещений.</span><span class="sxs-lookup"><span data-stu-id="24f84-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="24f84-145">Элементы, требующие доступа к **виртуальной** машине с правом **записи**:</span><span class="sxs-lookup"><span data-stu-id="24f84-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="24f84-146">Endpoints</span><span class="sxs-lookup"><span data-stu-id="24f84-146">Endpoints</span></span>  
* <span data-ttu-id="24f84-147">IP-адреса;</span><span class="sxs-lookup"><span data-stu-id="24f84-147">IP addresses</span></span>  
* <span data-ttu-id="24f84-148">диски;</span><span class="sxs-lookup"><span data-stu-id="24f84-148">Disks</span></span>  
* <span data-ttu-id="24f84-149">расширения.</span><span class="sxs-lookup"><span data-stu-id="24f84-149">Extensions</span></span>  

<span data-ttu-id="24f84-150">Элементы, требующие доступа на **запись** как к **виртуальной машине**, так и к **группе ресурсов**, в которой она находится (а также к доменному имени):</span><span class="sxs-lookup"><span data-stu-id="24f84-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="24f84-151">группа доступности;</span><span class="sxs-lookup"><span data-stu-id="24f84-151">Availability set</span></span>  
* <span data-ttu-id="24f84-152">набор балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="24f84-152">Load balanced set</span></span>  
* <span data-ttu-id="24f84-153">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="24f84-153">Alert rules</span></span>  

<span data-ttu-id="24f84-154">Если у вас нет доступа ни к одному из этих элементов, попросите администратора предоставить вам права участника для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24f84-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="24f84-155">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="24f84-155">See more</span></span>
* <span data-ttu-id="24f84-156">[Управление доступом на основе ролей.](role-based-access-control-configure.md) Начало работы с RBAC на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="24f84-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="24f84-157">[Встроенные роли.](role-based-access-built-in-roles.md) Сведения о стандартных ролях в RBAC.</span><span class="sxs-lookup"><span data-stu-id="24f84-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="24f84-158">[Пользовательские роли в Azure RBAC](role-based-access-control-custom-roles.md). Сведения о создании пользовательских ролей в соответствии с потребностями доступа.</span><span class="sxs-lookup"><span data-stu-id="24f84-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="24f84-159">[Создание отчета по журналу изменений доступа](role-based-access-control-access-change-history-report.md). Отслеживание изменения назначений ролей в RBAC.</span><span class="sxs-lookup"><span data-stu-id="24f84-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

