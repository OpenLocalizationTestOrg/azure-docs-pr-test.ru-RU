---
title: "Обновление кластера Azure Service Fabric | Документация Майкрософт"
description: "Обновление кода и (или) конфигурации Service Fabric, под управлением которой работает кластер Service Fabric, в том числе изменение режима обновления кластера, обновление сертификатов, добавление портов приложений, применение исправлений для ОС и т. д. Чего можно ожидать при выполнении обновлений?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 7ea71ab891583c51b3c07a4d0a9f0b4f54e56669
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a><span data-ttu-id="927c2-104">Обновление кластера Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="927c2-104">Upgrade an Azure Service Fabric cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="927c2-105">Кластер Azure</span><span class="sxs-lookup"><span data-stu-id="927c2-105">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="927c2-106">Автономный кластер</span><span class="sxs-lookup"><span data-stu-id="927c2-106">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

<span data-ttu-id="927c2-107">Для любой современной системы разработка с учетом возможности модернизации является неотъемлемой составляющей успеха продукта.</span><span class="sxs-lookup"><span data-stu-id="927c2-107">For any modern system, designing for upgradability is key to achieving long-term success of your product.</span></span> <span data-ttu-id="927c2-108">Кластер Service Fabric Azure представляет собой ресурс, который принадлежит вам, но частично управляется корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="927c2-108">An Azure Service Fabric cluster is a resource that you own, but is partly managed by Microsoft.</span></span> <span data-ttu-id="927c2-109">В этой статье содержатся сведения о компонентах, управляемых автоматически, и о том, что можно настроить самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="927c2-109">This article describes what is managed automatically and what you can configure yourself.</span></span>

## <a name="controlling-the-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="927c2-110">Управление версиями Service Fabric в кластере</span><span class="sxs-lookup"><span data-stu-id="927c2-110">Controlling the fabric version that runs on your Cluster</span></span>
<span data-ttu-id="927c2-111">Вы можете настроить для кластера автоматическое обновление Service Fabric по мере выпуска новых версий корпорацией Майкрософт или выбрать поддерживаемую версию, в которой должен работать ваш кластер.</span><span class="sxs-lookup"><span data-stu-id="927c2-111">You can set your cluster to receive automatic fabric upgrades as they are released by Microsoft or you can select a supported fabric version you want your cluster to be on.</span></span>

<span data-ttu-id="927c2-112">Для этого нужно настроить параметр upgradeMode в конфигурации кластера с помощью портала или Resource Manager. Это можно сделать как при создания кластера, так и во время его работы.</span><span class="sxs-lookup"><span data-stu-id="927c2-112">You do this by setting the "upgradeMode" cluster configuration on the portal or using Resource Manager at the time of creation or later on a live cluster</span></span> 

> [!NOTE]
> <span data-ttu-id="927c2-113">Обязательно следите за тем, чтобы кластер работал под управлением поддерживаемой версии Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="927c2-113">Make sure to keep your cluster running a supported fabric version always.</span></span> <span data-ttu-id="927c2-114">Когда мы объявляем о выпуске новой версии Service Fabric, для предыдущей версии определяется срок завершения жизненного цикла. Этот срок составляет по меньшей мере 60 дней.</span><span class="sxs-lookup"><span data-stu-id="927c2-114">As and when we announce the release of a new version of service fabric, the previous version is marked for end of support after a minimum of 60 days from that date.</span></span> <span data-ttu-id="927c2-115">О доступности новых выпусков сообщается в [блоге группы разработчиков Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="927c2-115">the  The new releases are announced [on the service fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="927c2-116">после чего вы можете использовать их.</span><span class="sxs-lookup"><span data-stu-id="927c2-116">The new release is available to choose then.</span></span> 
> 
> 

<span data-ttu-id="927c2-117">За 14 дней до истечения жизненного цикла выпуска, под управлением которого работает ваш кластер, будет создано событие работоспособности, которое переводит кластер в состояние предупреждения.</span><span class="sxs-lookup"><span data-stu-id="927c2-117">14 days prior to the expiry of the release your cluster is running, a health event is generated that puts your cluster into a warning health state.</span></span> <span data-ttu-id="927c2-118">Состояние предупреждения изменится, когда кластер будет обновлен до поддерживаемой версии.</span><span class="sxs-lookup"><span data-stu-id="927c2-118">The cluster remains in a warning state until you upgrade to a supported fabric version.</span></span>

### <a name="setting-the-upgrade-mode-via-portal"></a><span data-ttu-id="927c2-119">Настройка режима обновления через портал</span><span class="sxs-lookup"><span data-stu-id="927c2-119">Setting the upgrade mode via portal</span></span>
<span data-ttu-id="927c2-120">При создании кластера вы можете выбрать режим обновления: автоматический или вручную.</span><span class="sxs-lookup"><span data-stu-id="927c2-120">You can set the cluster to automatic or manual when you are creating the cluster.</span></span>

![Create_Manualmode][Create_Manualmode]

<span data-ttu-id="927c2-122">Эти варианты режима обновления можно также указать для работающего кластера, используя интерфейс управления.</span><span class="sxs-lookup"><span data-stu-id="927c2-122">You can set the cluster to automatic or manual when on a live cluster, using the manage experience.</span></span> 

#### <a name="upgrading-to-a-new-version-on-a-cluster-that-is-set-to-manual-mode-via-portal"></a><span data-ttu-id="927c2-123">Обновление кластера, для которого установлен режим обновления вручную, с помощью портала.</span><span class="sxs-lookup"><span data-stu-id="927c2-123">Upgrading to a new version on a cluster that is set to Manual mode via portal.</span></span>
<span data-ttu-id="927c2-124">Чтобы обновить кластер до новой версии, нужно просто выбрать доступную версию в раскрывающемся списке и сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="927c2-124">To upgrade to a new version, all you need to do is select the available version from the dropdown and save.</span></span> <span data-ttu-id="927c2-125">Обновление Service Fabric запустится автоматически.</span><span class="sxs-lookup"><span data-stu-id="927c2-125">The Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="927c2-126">В ходе обновления соблюдаются все политики работоспособности кластера (политики, определяющие состояние работоспособности для узлов и всех приложений, выполняющихся в кластере).</span><span class="sxs-lookup"><span data-stu-id="927c2-126">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="927c2-127">Если требования политик работоспособности кластера не реализуются, выполняется откат обновления.</span><span class="sxs-lookup"><span data-stu-id="927c2-127">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="927c2-128">Прокрутите этот документ вниз, чтобы узнать о том, как настроить пользовательские политики работоспособности.</span><span class="sxs-lookup"><span data-stu-id="927c2-128">Scroll down this document to read more on how to set those custom health policies.</span></span> 

<span data-ttu-id="927c2-129">Устранив проблемы, которые привели к откату, запустите обновление снова, выполнив те же действия.</span><span class="sxs-lookup"><span data-stu-id="927c2-129">Once you have fixed the issues that resulted in the rollback, you need to initiate the upgrade again, by following the same steps as before.</span></span>

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-the-upgrade-mode-via-a-resource-manager-template"></a><span data-ttu-id="927c2-131">Настройка режима обновления с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="927c2-131">Setting the upgrade mode via a Resource Manager template</span></span>
<span data-ttu-id="927c2-132">Добавьте параметр upgradeMode к определению ресурса Microsoft.ServiceFabric/clusters, а для параметра clusterCodeVersion установите значение одной из поддерживаемых версий Service Fabric, как показано ниже, а затем разверните шаблон.</span><span class="sxs-lookup"><span data-stu-id="927c2-132">Add the "upgradeMode" configuration to the Microsoft.ServiceFabric/clusters resource definition and set the "clusterCodeVersion" to one of the supported fabric versions as shown below and then deploy the template.</span></span> <span data-ttu-id="927c2-133">Для параметра upgradeMode поддерживаются значения Manual и Automatic.</span><span class="sxs-lookup"><span data-stu-id="927c2-133">The valid values for "upgradeMode" are "Manual" or "Automatic"</span></span>

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-to-a-new-version-on-a-cluster-that-is-set-to-manual-mode-via-a-resource-manager-template"></a><span data-ttu-id="927c2-135">Обновление кластера, для которого установлен режим обновления вручную, с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="927c2-135">Upgrading to a new version on a cluster that is set to Manual mode via a Resource Manager template.</span></span>
<span data-ttu-id="927c2-136">Чтобы обновить до новой версии кластер, для которого установлен режим обновления вручную, замените значение параметра clusterCodeVersion значением поддерживаемой версии и разверните шаблон.</span><span class="sxs-lookup"><span data-stu-id="927c2-136">When the cluster is in Manual mode, to upgrade to a new version, change the "clusterCodeVersion" to a supported version and deploy it.</span></span> <span data-ttu-id="927c2-137">Развертывание шаблона автоматически запускает обновление Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="927c2-137">The deployment of the template, kicks of the Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="927c2-138">В ходе обновления соблюдаются все политики работоспособности кластера (политики, определяющие состояние работоспособности для узлов и всех приложений, выполняющихся в кластере).</span><span class="sxs-lookup"><span data-stu-id="927c2-138">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="927c2-139">Если требования политик работоспособности кластера не реализуются, выполняется откат обновления.</span><span class="sxs-lookup"><span data-stu-id="927c2-139">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="927c2-140">Прокрутите этот документ вниз, чтобы узнать о том, как настроить пользовательские политики работоспособности.</span><span class="sxs-lookup"><span data-stu-id="927c2-140">Scroll down this document to read more on how to set those custom health policies.</span></span> 

<span data-ttu-id="927c2-141">Устранив проблемы, которые привели к откату, запустите обновление снова, выполнив те же действия.</span><span class="sxs-lookup"><span data-stu-id="927c2-141">Once you have fixed the issues that resulted in the rollback, you need to initiate the upgrade again, by following the same steps as before.</span></span>

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a><span data-ttu-id="927c2-142">Получение списка всех доступных версий для всех сред в указанной подписке</span><span class="sxs-lookup"><span data-stu-id="927c2-142">Get list of all available version for all environments for a given subscription</span></span>
<span data-ttu-id="927c2-143">Запустите следующую команду, и вы увидите результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="927c2-143">Run the following command, and you should get an output similar to this.</span></span>

<span data-ttu-id="927c2-144">Параметр supportExpiryUtc сообщает, когда истекает или истек срок действия текущей версии.</span><span class="sxs-lookup"><span data-stu-id="927c2-144">"supportExpiryUtc" tells your when a given release is expiring or has expired.</span></span> <span data-ttu-id="927c2-145">Для последнего выпуска нет допустимой даты, то есть параметр имеет значение 9999-12-31T23:59:59.9999999. Это означает, что дата окончания срока действия еще не определена.</span><span class="sxs-lookup"><span data-stu-id="927c2-145">The latest release does not have a valid date - it has a value of "9999-12-31T23:59:59.9999999", which just means that the expiry date is not yet set.</span></span>

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-the-cluster-upgrade-mode-is-automatic"></a><span data-ttu-id="927c2-146">Обновление настроек Service Fabric для кластера с автоматическим режимом обновления</span><span class="sxs-lookup"><span data-stu-id="927c2-146">Fabric upgrade behavior when the cluster Upgrade Mode is Automatic</span></span>
<span data-ttu-id="927c2-147">Майкрософт поддерживает код и конфигурацию системы Service Fabric, которая выполняется в кластере Azure.</span><span class="sxs-lookup"><span data-stu-id="927c2-147">Microsoft maintains the fabric code and configuration that runs in an Azure cluster.</span></span> <span data-ttu-id="927c2-148">По мере необходимости мы выполняем автоматические контролируемые обновления программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="927c2-148">We perform automatic monitored upgrades to the software on an as-needed basis.</span></span> <span data-ttu-id="927c2-149">Эти обновления могут затрагивать код, конфигурацию или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="927c2-149">These upgrades could be code, configuration, or both.</span></span> <span data-ttu-id="927c2-150">Чтобы обновления не затрагивали приложение или оказывали на него минимальное влияние, обновление выполняется поэтапно.</span><span class="sxs-lookup"><span data-stu-id="927c2-150">To make sure that your application suffers no impact or minimal impact due to these upgrades, we perform the upgrades in the following phases:</span></span>

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a><span data-ttu-id="927c2-151">Этап 1. Выполнение обновления с помощью всех политик работоспособности кластера</span><span class="sxs-lookup"><span data-stu-id="927c2-151">Phase 1: An upgrade is performed by using all cluster health policies</span></span>
<span data-ttu-id="927c2-152">В ходе этого этапа обновления применяются к одному домену обновления за раз, а приложения, которые были запущены в кластере, продолжают работать без простоев.</span><span class="sxs-lookup"><span data-stu-id="927c2-152">During this phase, the upgrades proceed one upgrade domain at a time, and the applications that were running in the cluster continue to run without any downtime.</span></span> <span data-ttu-id="927c2-153">В ходе обновления соблюдаются все политики работоспособности кластера (политики, определяющие состояние работоспособности для узлов и всех приложений, выполняющихся в кластере).</span><span class="sxs-lookup"><span data-stu-id="927c2-153">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to during the upgrade.</span></span>

<span data-ttu-id="927c2-154">Если требования политик работоспособности кластера не реализуются, выполняется откат обновления.</span><span class="sxs-lookup"><span data-stu-id="927c2-154">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="927c2-155">Затем владельцу подписки отправляется сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="927c2-155">Then an email is sent to the owner of the subscription.</span></span> <span data-ttu-id="927c2-156">Оно содержит следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="927c2-156">The email contains the following information:</span></span>

* <span data-ttu-id="927c2-157">Уведомление о том, что нам пришлось выполнить откат обновления кластера.</span><span class="sxs-lookup"><span data-stu-id="927c2-157">Notification that we had to roll back a cluster upgrade.</span></span>
* <span data-ttu-id="927c2-158">Рекомендуемые действия по решению проблемы, при их наличии.</span><span class="sxs-lookup"><span data-stu-id="927c2-158">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="927c2-159">Количество дней (n) до выполнения этапа 2.</span><span class="sxs-lookup"><span data-stu-id="927c2-159">The number of days (n) until we execute Phase 2.</span></span>

<span data-ttu-id="927c2-160">Мы постараемся выполнить аналогичное обновление еще несколько раз в случае, если причины неудачи связаны с инфраструктурой.</span><span class="sxs-lookup"><span data-stu-id="927c2-160">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="927c2-161">Через n дней с момента отправки сообщения мы переходим к этапу 2.</span><span class="sxs-lookup"><span data-stu-id="927c2-161">After the n days from the date the email was sent, we proceed to Phase 2.</span></span>

<span data-ttu-id="927c2-162">Если политики работоспособности кластера соблюдены, обновление считается успешным и помечается как завершенное.</span><span class="sxs-lookup"><span data-stu-id="927c2-162">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="927c2-163">Это может произойти во время первоначального или повторного запусков обновлений на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="927c2-163">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="927c2-164">В случае успешного выполнения сообщение с подтверждением не отправляется.</span><span class="sxs-lookup"><span data-stu-id="927c2-164">There is no email confirmation of a successful run.</span></span> <span data-ttu-id="927c2-165">Это позволяет избежать отправки чрезмерного количества сообщений. Получение сообщения следует рассматривать как исключение из обычного режима.</span><span class="sxs-lookup"><span data-stu-id="927c2-165">This is to avoid sending you too many emails--receiving an email should be seen as an exception to normal.</span></span> <span data-ttu-id="927c2-166">Мы надеемся, что большинство обновлений кластера будет выполнено без ущерба для доступности вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="927c2-166">We expect most of the cluster upgrades to succeed without impacting your application availability.</span></span>

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a><span data-ttu-id="927c2-167">Этап 2. Выполнение обновления с помощью только политик работоспособности по умолчанию</span><span class="sxs-lookup"><span data-stu-id="927c2-167">Phase 2: An upgrade is performed by using default health policies only</span></span>
<span data-ttu-id="927c2-168">Политики работоспособности на этом этапе задаются таким образом, что ряд приложений, которые были работоспособны в начале обновления, остаются неизменными в течение всего процесса обновления.</span><span class="sxs-lookup"><span data-stu-id="927c2-168">The health policies in this phase are set in such a way that the number of applications that were healthy at the beginning of the upgrade remains the same for the duration of the upgrade process.</span></span> <span data-ttu-id="927c2-169">Как и в ходе этапа 1, на этапе 2 обновления применяются к одному домену обновления за раз, а приложения, которые были запущены в кластере, продолжают работать без простоев.</span><span class="sxs-lookup"><span data-stu-id="927c2-169">As in Phase 1, the Phase 2 upgrades proceed one upgrade domain at a time, and the applications that were running in the cluster continue to run without any downtime.</span></span> <span data-ttu-id="927c2-170">В течение применения обновления действуют политики работоспособности кластера (это сочетание состояния работоспособности узла и всех приложений, выполняющихся в кластере).</span><span class="sxs-lookup"><span data-stu-id="927c2-170">The cluster health policies (a combination of node health and the health all the applications running in the cluster) are adhered to for the duration of the upgrade.</span></span>

<span data-ttu-id="927c2-171">Если применяемые политики работоспособности кластера фактически не соблюдаются, выполняется откат обновления.</span><span class="sxs-lookup"><span data-stu-id="927c2-171">If the cluster health policies in effect are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="927c2-172">Затем владельцу подписки отправляется сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="927c2-172">Then an email is sent to the owner of the subscription.</span></span> <span data-ttu-id="927c2-173">Оно содержит следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="927c2-173">The email contains the following information:</span></span>

* <span data-ttu-id="927c2-174">Уведомление о том, что нам пришлось выполнить откат обновления кластера.</span><span class="sxs-lookup"><span data-stu-id="927c2-174">Notification that we had to roll back a cluster upgrade.</span></span>
* <span data-ttu-id="927c2-175">Рекомендуемые действия по решению проблемы, при их наличии.</span><span class="sxs-lookup"><span data-stu-id="927c2-175">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="927c2-176">Количество дней (n) до выполнения этапа 3.</span><span class="sxs-lookup"><span data-stu-id="927c2-176">The number of days (n) until we execute Phase 3.</span></span>

<span data-ttu-id="927c2-177">Мы постараемся выполнить аналогичное обновление еще несколько раз в случае, если причины неудачи связаны с инфраструктурой.</span><span class="sxs-lookup"><span data-stu-id="927c2-177">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="927c2-178">За несколько дней до назначенного срока владельцу подписки отправляется сообщение с напоминанием.</span><span class="sxs-lookup"><span data-stu-id="927c2-178">A reminder email is sent a couple of days before n days are up.</span></span> <span data-ttu-id="927c2-179">Через n дней с момента отправки сообщения мы переходим к этапу 3.</span><span class="sxs-lookup"><span data-stu-id="927c2-179">After the n days from the date the email was sent, we proceed to Phase 3.</span></span> <span data-ttu-id="927c2-180">К сообщениям, которые отправляются на этапе 2, следует отнестись серьезно и выполнить действия по устранению ошибок.</span><span class="sxs-lookup"><span data-stu-id="927c2-180">The emails we send you in Phase 2 must be taken seriously and remedial actions must be taken.</span></span>

<span data-ttu-id="927c2-181">Если политики работоспособности кластера соблюдены, обновление считается успешным и помечается как завершенное.</span><span class="sxs-lookup"><span data-stu-id="927c2-181">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="927c2-182">Это может произойти во время первоначального или повторного запусков обновлений на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="927c2-182">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="927c2-183">В случае успешного выполнения сообщение с подтверждением не отправляется.</span><span class="sxs-lookup"><span data-stu-id="927c2-183">There is no email confirmation of a successful run.</span></span>

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a><span data-ttu-id="927c2-184">Этап 3. Выполнение обновления с помощью жестких политик работоспособности кластера</span><span class="sxs-lookup"><span data-stu-id="927c2-184">Phase 3: An upgrade is performed by using aggressive health policies</span></span>
<span data-ttu-id="927c2-185">Эти политики работоспособности на данном этапе предназначены для выполнения обновления, а не обеспечения работоспособности приложений.</span><span class="sxs-lookup"><span data-stu-id="927c2-185">These health policies in this phase are geared towards completion of the upgrade rather than the health of the applications.</span></span> <span data-ttu-id="927c2-186">Этот этап очень редко применяется для обновления кластера.</span><span class="sxs-lookup"><span data-stu-id="927c2-186">Very few cluster upgrades end up in this phase.</span></span> <span data-ttu-id="927c2-187">Если ваш кластер достигает этого этапа, есть высокая вероятность того, что ваше приложение перейдет в неработоспособное состояние и (или) будет недоступно.</span><span class="sxs-lookup"><span data-stu-id="927c2-187">If your cluster gets to this phase, there is a good chance that your application becomes unhealthy and/or lose availability.</span></span>

<span data-ttu-id="927c2-188">Как и на других двух этапах, обновления на этапе 3 применяются к одному домену обновления за раз.</span><span class="sxs-lookup"><span data-stu-id="927c2-188">Similar to the other two phases, Phase 3 upgrades proceed one upgrade domain at a time.</span></span>

<span data-ttu-id="927c2-189">Если требования политик работоспособности кластера не реализуются, выполняется откат обновления.</span><span class="sxs-lookup"><span data-stu-id="927c2-189">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="927c2-190">Мы постараемся выполнить аналогичное обновление еще несколько раз в случае, если причины неудачи связаны с инфраструктурой.</span><span class="sxs-lookup"><span data-stu-id="927c2-190">We try to execute the same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="927c2-191">После этого кластер закрепляется и больше не будет получать поддержку и обновления.</span><span class="sxs-lookup"><span data-stu-id="927c2-191">After that, the cluster is pinned, so that it will no longer receive support and/or upgrades.</span></span>

<span data-ttu-id="927c2-192">Сообщение с этими сведениями и корректирующими действиями отправляется владельцу подписки.</span><span class="sxs-lookup"><span data-stu-id="927c2-192">An email with this information is sent to the subscription owner, along with the remedial actions.</span></span> <span data-ttu-id="927c2-193">Мы не ожидаем перехода кластеров в состояние, в котором произошел сбой этапа 3.</span><span class="sxs-lookup"><span data-stu-id="927c2-193">We do not expect any clusters to get into a state where Phase 3 has failed.</span></span>

<span data-ttu-id="927c2-194">Если политики работоспособности кластера соблюдены, обновление считается успешным и помечается как завершенное.</span><span class="sxs-lookup"><span data-stu-id="927c2-194">If the cluster health policies are met, the upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="927c2-195">Это может произойти во время первоначального или повторного запусков обновлений на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="927c2-195">This can happen during the initial upgrade or any of the upgrade reruns in this phase.</span></span> <span data-ttu-id="927c2-196">В случае успешного выполнения сообщение с подтверждением не отправляется.</span><span class="sxs-lookup"><span data-stu-id="927c2-196">There is no email confirmation of a successful run.</span></span>

## <a name="cluster-configurations-that-you-control"></a><span data-ttu-id="927c2-197">Управляемая пользователем конфигурация кластера</span><span class="sxs-lookup"><span data-stu-id="927c2-197">Cluster configurations that you control</span></span>
<span data-ttu-id="927c2-198">Наряду с настройкой режима обновления для работающего кластера можно изменить следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="927c2-198">In addition to the ability to set the cluster upgrade mode, Here are the configurations that you can change on a live cluster.</span></span>

### <a name="certificates"></a><span data-ttu-id="927c2-199">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="927c2-199">Certificates</span></span>
<span data-ttu-id="927c2-200">На портале можно добавить новые или удалить имеющиеся сертификаты для кластера и клиента.</span><span class="sxs-lookup"><span data-stu-id="927c2-200">You can add new or delete certificates for the cluster and client via the portal easily.</span></span> <span data-ttu-id="927c2-201">Ознакомьтесь с [подробными инструкциями в этом документе](service-fabric-cluster-security-update-certs-azure.md)</span><span class="sxs-lookup"><span data-stu-id="927c2-201">Refer to [this document for detailed instructions](service-fabric-cluster-security-update-certs-azure.md)</span></span>

![Снимок экрана, демонстрирующий отпечатки сертификатов на портале Azure.][CertificateUpgrade]

### <a name="application-ports"></a><span data-ttu-id="927c2-203">Порты приложения</span><span class="sxs-lookup"><span data-stu-id="927c2-203">Application ports</span></span>
<span data-ttu-id="927c2-204">Порты приложения можно изменить путем изменения свойств ресурса балансировщика нагрузки, связанных с типом узла.</span><span class="sxs-lookup"><span data-stu-id="927c2-204">You can change application ports by changing the Load Balancer resource properties that are associated with the node type.</span></span> <span data-ttu-id="927c2-205">Для этого можно использовать портал или диспетчер ресурсов PowerShell напрямую.</span><span class="sxs-lookup"><span data-stu-id="927c2-205">You can use the portal, or you can use Resource Manager PowerShell directly.</span></span>

<span data-ttu-id="927c2-206">Чтобы открыть новый порт на всех виртуальных машинах в типе узла, необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="927c2-206">To open a new port on all VMs in a node type, do the following:</span></span>

1. <span data-ttu-id="927c2-207">Добавьте новую проверку к соответствующему балансировщику нагрузки.</span><span class="sxs-lookup"><span data-stu-id="927c2-207">Add a new probe to the appropriate load balancer.</span></span>
   
    <span data-ttu-id="927c2-208">Если вы развернули кластер с помощью портала, то балансировщикам нагрузки присваиваются имена "LB-<имя_группы_ресурсов>-<имя_типа_узла>" и т. д. по одному для каждого типа узла.</span><span class="sxs-lookup"><span data-stu-id="927c2-208">If you deployed your cluster by using the portal, the load balancers are named "LB-name of the Resource group-NodeTypename", one for each node type.</span></span> <span data-ttu-id="927c2-209">Поскольку имена балансировщиков нагрузки являются уникальными только в группе ресурсов, рекомендуется искать их в данной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="927c2-209">Since the load balancer names are unique only within a resource group, it is best if you search for them under a specific resource group.</span></span>
   
    ![Снимок экрана, демонстрирующий добавление проверки в балансировщик нагрузки на портале.][AddingProbes]
2. <span data-ttu-id="927c2-211">Добавьте новое правило к балансировщику нагрузки.</span><span class="sxs-lookup"><span data-stu-id="927c2-211">Add a new rule to the load balancer.</span></span>
   
    <span data-ttu-id="927c2-212">Добавьте новое правило в тот же балансировщик нагрузки, используя проверку, созданную на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="927c2-212">Add a new rule to the same load balancer by using the probe that you created in the previous step.</span></span>
   
    ![Добавление нового правила в подсистему балансировки нагрузки на портале][AddingLBRules]

### <a name="placement-properties"></a><span data-ttu-id="927c2-214">Свойства размещения</span><span class="sxs-lookup"><span data-stu-id="927c2-214">Placement properties</span></span>
<span data-ttu-id="927c2-215">Для каждого типа узла можно добавить настраиваемые свойства размещения, которые будут использоваться в приложениях.</span><span class="sxs-lookup"><span data-stu-id="927c2-215">For each of the node types, you can add custom placement properties that you want to use in your applications.</span></span> <span data-ttu-id="927c2-216">NodeType — это свойство по умолчанию, которое можно использовать без его явного добавления.</span><span class="sxs-lookup"><span data-stu-id="927c2-216">NodeType is a default property that you can use without adding it explicitly.</span></span>

> [!NOTE]
> <span data-ttu-id="927c2-217">Дополнительные сведения об использовании ограничений на размещение, свойствах узла и способах их определения см. в разделе "Ограничения на размещение и свойства узлов" в документе по диспетчеру кластерных ресурсов Service Fabric на странице [Описание кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="927c2-217">For details on the use of placement constraints, node properties, and how to define them, refer to the section "Placement Constraints and Node Properties" in the Service Fabric Cluster Resource Manager Document on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>
> 
> 

### <a name="capacity-metrics"></a><span data-ttu-id="927c2-218">Метрики емкости</span><span class="sxs-lookup"><span data-stu-id="927c2-218">Capacity metrics</span></span>
<span data-ttu-id="927c2-219">Для каждого типа узла можно добавить настраиваемые метрики емкости, которые будут использоваться в приложениях для передачи данных о нагрузке.</span><span class="sxs-lookup"><span data-stu-id="927c2-219">For each of the node types, you can add custom capacity metrics that you want to use in your applications to report load.</span></span> <span data-ttu-id="927c2-220">Дополнительные сведения об использовании метрик емкости для отчетах о нагрузке см. в документах по диспетчеру кластерных ресурсов Service Fabric на страницах [Описание кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md) и [Управление потреблением ресурсов и нагрузкой в Service Fabric с помощью метрик](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="927c2-220">For details on the use of capacity metrics to report load, refer to the Service Fabric Cluster Resource Manager Documents on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md) and [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md).</span></span>

### <a name="fabric-upgrade-settings---health-polices"></a><span data-ttu-id="927c2-221">Параметры обновления Service Fabric — политики работоспособности</span><span class="sxs-lookup"><span data-stu-id="927c2-221">Fabric upgrade settings - Health polices</span></span>
<span data-ttu-id="927c2-222">Вы можете указать пользовательские политики работоспособности для обновления Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="927c2-222">You can specify custom health polices for fabric upgrade.</span></span> <span data-ttu-id="927c2-223">Если для кластера выбран режим автоматического обновления, эти политики применяются на первом этапе автоматического обновления Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="927c2-223">If you have set your cluster to Automatic fabric upgrades, then these policies get applied to the Phase-1 of the automatic fabric upgrades.</span></span>
<span data-ttu-id="927c2-224">Если для кластера указано обновление вручную, эти политики применяются при каждом выборе новой версии, когда запускается обновление Service Fabric в кластере.</span><span class="sxs-lookup"><span data-stu-id="927c2-224">If you have set your cluster for Manual fabric upgrades, then these policies get applied each time you select a new version triggering the system to kick off the fabric upgrade in your cluster.</span></span> <span data-ttu-id="927c2-225">Если политики не переопределить, будут использоваться значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="927c2-225">If you do not override the policies, the defaults are used.</span></span>

<span data-ttu-id="927c2-226">Определить пользовательские политики работоспособности или просмотреть текущие параметры можно в колонке "Обновление Service Fabric", выбрав расширенные параметры обновления.</span><span class="sxs-lookup"><span data-stu-id="927c2-226">You can specify the custom health policies or review the current settings under the "fabric upgrade" blade, by selecting the advanced upgrade settings.</span></span> <span data-ttu-id="927c2-227">Как это сделать, показано ниже.</span><span class="sxs-lookup"><span data-stu-id="927c2-227">Review the following picture on how to.</span></span> 

![Управление пользовательскими политиками работоспособности][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a><span data-ttu-id="927c2-229">Настройка параметров Service Fabric для кластера</span><span class="sxs-lookup"><span data-stu-id="927c2-229">Customize Fabric settings for your cluster</span></span>
<span data-ttu-id="927c2-230">В [этой статье](service-fabric-cluster-fabric-settings.md) описаны разные варианты настройки Service Fabric для кластера.</span><span class="sxs-lookup"><span data-stu-id="927c2-230">Refer to [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md) on what and how you can customize them.</span></span>

### <a name="os-patches-on-the-vms-that-make-up-the-cluster"></a><span data-ttu-id="927c2-231">Исправления ОС на виртуальных машинах, составляющих кластер</span><span class="sxs-lookup"><span data-stu-id="927c2-231">OS patches on the VMs that make up the cluster</span></span>
<span data-ttu-id="927c2-232">[Приложение для управления исправлениями](service-fabric-patch-orchestration-application.md), которое можно развернуть в кластере, позволяет устанавливать исправления из Центра обновления Windows контролируемым образом, не нарушая доступность служб.</span><span class="sxs-lookup"><span data-stu-id="927c2-232">Refer to [Patch Orchestration Application](service-fabric-patch-orchestration-application.md) which can be deployed on your cluster to install patches from Windows Update in an orchestrated manner, keeping the services available all the time.</span></span> 

### <a name="os-upgrades-on-the-vms-that-make-up-the-cluster"></a><span data-ttu-id="927c2-233">Обновления ОС на виртуальных машинах, составляющих кластер</span><span class="sxs-lookup"><span data-stu-id="927c2-233">OS upgrades on the VMs that make up the cluster</span></span>
<span data-ttu-id="927c2-234">Вы должны обновить образ ОС на виртуальных машинах кластера; поочередно для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="927c2-234">If you must upgrade the OS image on the virtual machines of the cluster, you must do it one VM at a time.</span></span> <span data-ttu-id="927c2-235">За это обновление отвечаете вы: в настоящее время автоматизация этой функции отсутствует.</span><span class="sxs-lookup"><span data-stu-id="927c2-235">You are responsible for this upgrade--there is currently no automation for this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="927c2-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="927c2-236">Next steps</span></span>
* <span data-ttu-id="927c2-237">Узнайте, как настроить некоторые [параметры Service Fabric для кластера](service-fabric-cluster-fabric-settings.md)</span><span class="sxs-lookup"><span data-stu-id="927c2-237">Learn how to customize some of the [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md)</span></span>
* <span data-ttu-id="927c2-238">Ознакомьтесь с концепцией [масштабирования кластера](service-fabric-cluster-scale-up-down.md)</span><span class="sxs-lookup"><span data-stu-id="927c2-238">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md)</span></span>
* <span data-ttu-id="927c2-239">Узнайте об [обновлениях приложений](service-fabric-application-upgrade.md)</span><span class="sxs-lookup"><span data-stu-id="927c2-239">Learn about [application upgrades](service-fabric-application-upgrade.md)</span></span>

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
