---
title: "Синхронизация Azure AD Connect: рабочие задачи и рекомендации | Документация Майкрософт"
description: "В этой статье описываются рабочие задачи служб синхронизации Azure AD Connect и подготовка к работе с этим компонентом."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: b7583a1556bb1113f349a78890768451e39c6878
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="eb69b-103">Службы синхронизации Azure AD Connect: рабочие задачи и рекомендации</span><span class="sxs-lookup"><span data-stu-id="eb69b-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="eb69b-104">В этой статье описаны рабочие задачи служб синхронизации Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="eb69b-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="eb69b-105">Промежуточный режим</span><span class="sxs-lookup"><span data-stu-id="eb69b-105">Staging mode</span></span>
<span data-ttu-id="eb69b-106">Промежуточный режим может использоваться в нескольких ситуациях, например:</span><span class="sxs-lookup"><span data-stu-id="eb69b-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="eb69b-107">обеспечение высокой доступности;</span><span class="sxs-lookup"><span data-stu-id="eb69b-107">High availability.</span></span>
* <span data-ttu-id="eb69b-108">тестирование и развертывание новых изменений в конфигурации;</span><span class="sxs-lookup"><span data-stu-id="eb69b-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="eb69b-109">введение в эксплуатацию нового сервера и списание старого.</span><span class="sxs-lookup"><span data-stu-id="eb69b-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="eb69b-110">Когда сервер работает в промежуточном режиме, вы можете вносить изменения в конфигурацию и просматривать их, прежде чем активировать сервер.</span><span class="sxs-lookup"><span data-stu-id="eb69b-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="eb69b-111">Этот режим также позволяет запустить полный импорт и полную синхронизацию, чтобы проверить, все ли изменения имеют нужный вид, прежде чем вносить их в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="eb69b-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="eb69b-112">Во время установки для сервера можно выбрать **промежуточный режим**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="eb69b-113">В таком случае сервер будет выполнять импорт и синхронизацию, но не будет выполнять операции экспорта.</span><span class="sxs-lookup"><span data-stu-id="eb69b-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="eb69b-114">Сервер в промежуточном режиме не выполняет синхронизацию и обратную запись паролей, даже если эти функции активированы при установке.</span><span class="sxs-lookup"><span data-stu-id="eb69b-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="eb69b-115">При отключении промежуточного режима сервер начнет выполнять экспорт, а также синхронизацию и обратную запись паролей.</span><span class="sxs-lookup"><span data-stu-id="eb69b-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="eb69b-116">Вы по-прежнему можете выполнить экспорт принудительно с помощью Synchronization Service Manager.</span><span class="sxs-lookup"><span data-stu-id="eb69b-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="eb69b-117">Сервер в промежуточном режиме продолжает получать изменения из Active Directory и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb69b-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="eb69b-118">На сервере всегда есть копии последних изменений, и он сможет очень быстро принять на себя функции другого сервера.</span><span class="sxs-lookup"><span data-stu-id="eb69b-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="eb69b-119">При внесении изменений в конфигурацию сервера-источника обязательно внесите те же изменения в конфигурацию серверов в промежуточном режиме.</span><span class="sxs-lookup"><span data-stu-id="eb69b-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="eb69b-120">Тем, кто знаком с более ранними технологиями синхронизации, следует помнить об отличиях промежуточного режима, поскольку сервер имеет собственную базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="eb69b-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="eb69b-121">Благодаря такой архитектуре сервер в промежуточном режиме может располагаться в другом центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="eb69b-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="eb69b-122">Проверка конфигурации сервера</span><span class="sxs-lookup"><span data-stu-id="eb69b-122">Verify the configuration of a server</span></span>
<span data-ttu-id="eb69b-123">Чтобы использовать этот метод, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="eb69b-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="eb69b-124">Подготовка</span><span class="sxs-lookup"><span data-stu-id="eb69b-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="eb69b-125">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="eb69b-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="eb69b-126">Импорт и синхронизация</span><span class="sxs-lookup"><span data-stu-id="eb69b-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="eb69b-127">Проверка</span><span class="sxs-lookup"><span data-stu-id="eb69b-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="eb69b-128">Переключение активного сервера</span><span class="sxs-lookup"><span data-stu-id="eb69b-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="eb69b-129">Подготовка.</span><span class="sxs-lookup"><span data-stu-id="eb69b-129">Prepare</span></span>
1. <span data-ttu-id="eb69b-130">Установите Azure AD Connect, выберите **промежуточный режим** и снимите флажок **Запустить синхронизацию** на последней странице мастера установки.</span><span class="sxs-lookup"><span data-stu-id="eb69b-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="eb69b-131">В этом режиме можно вручную запустить модуль синхронизации.</span><span class="sxs-lookup"><span data-stu-id="eb69b-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="eb69b-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="eb69b-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="eb69b-133">Выйдите из системы и снова войдите в нее, а затем в меню "Пуск" выберите пункт **Служба синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="eb69b-134">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="eb69b-134">Configuration</span></span>
<span data-ttu-id="eb69b-135">Если вы внесли какие-либо изменения на сервере-источнике и хотите сравнить конфигурацию с промежуточным сервером, то воспользуйтесь [средством документирования конфигураций Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="eb69b-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="eb69b-136">Импорт и синхронизация</span><span class="sxs-lookup"><span data-stu-id="eb69b-136">Import and Synchronize</span></span>
1. <span data-ttu-id="eb69b-137">Щелкните **Соединители** и выберите первый соединитель типа **Доменные службы Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="eb69b-138">Щелкните **Запуск**, выберите **Полный импорт** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="eb69b-139">Проделайте это для всех соединителей данного типа.</span><span class="sxs-lookup"><span data-stu-id="eb69b-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="eb69b-140">Выберите соединитель типа **Azure Active Directory (Майкрософт)**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="eb69b-141">Щелкните **Запуск**, выберите **Полный импорт** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="eb69b-142">Убедитесь, что все еще выбрана вкладка "Соединители".</span><span class="sxs-lookup"><span data-stu-id="eb69b-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="eb69b-143">Для каждого соединителя типа **Доменные службы Active Directory** щелкните **Запуск**, выберите **Синхронизация изменений** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="eb69b-144">Выберите соединитель типа **Azure Active Directory (Майкрософт)**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="eb69b-145">Щелкните **Запуск**, выберите**Синхронизация изменений**) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="eb69b-146">Теперь изменения экспорта размещены в Azure AD и локальном каталоге AD (если используется гибридное развертывание Exchange).</span><span class="sxs-lookup"><span data-stu-id="eb69b-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="eb69b-147">С помощью описанных далее действий вы сможете проверить предстоящие изменения, прежде чем фактически запустить экспорт в каталоги.</span><span class="sxs-lookup"><span data-stu-id="eb69b-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="eb69b-148">Проверка</span><span class="sxs-lookup"><span data-stu-id="eb69b-148">Verify</span></span>
1. <span data-ttu-id="eb69b-149">Откройте командную строку и перейдите в каталог `%ProgramFiles%\Microsoft Azure AD Sync\bin`.</span><span class="sxs-lookup"><span data-stu-id="eb69b-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="eb69b-150">Выполните команду `csexport "Name of Connector" %temp%\export.xml /f:x`. Имя соединителя можно найти в службе синхронизации.</span><span class="sxs-lookup"><span data-stu-id="eb69b-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="eb69b-151">Это будет имя наподобие "contoso.com — AAD" для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb69b-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="eb69b-152">Скопируйте сценарий PowerShell из раздела [CSAnalyzer](#appendix-csanalyzer) в файл `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="eb69b-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="eb69b-153">Откройте окно PowerShell и перейдите в папку, в которой вы создали сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb69b-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="eb69b-154">Выполните команду `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="eb69b-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="eb69b-155">Теперь у вас есть файл **processedusers1.csv**, который можно просмотреть в Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="eb69b-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="eb69b-156">В этом файле находятся все изменения, предназначенные для экспорта в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb69b-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="eb69b-157">Внесите необходимые изменения в данные и конфигурацию и выполните описанные выше действия (импорт, синхронизация и проверка) повторно, чтобы привести изменения, которые предстоит экспортировать, в нужный вид.</span><span class="sxs-lookup"><span data-stu-id="eb69b-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="eb69b-158">Переключение активного сервера</span><span class="sxs-lookup"><span data-stu-id="eb69b-158">Switch active server</span></span>
1. <span data-ttu-id="eb69b-159">Отключите текущий сервер (DirSync, FIM или Azure AD Sync), чтобы он не выполнял экспорт в Azure AD, или переведите его в промежуточный режим (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="eb69b-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="eb69b-160">Запустите мастер установки на сервере в **промежуточном режиме** и отключите **промежуточный режим**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="eb69b-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="eb69b-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="eb69b-162">Аварийное восстановление</span><span class="sxs-lookup"><span data-stu-id="eb69b-162">Disaster recovery</span></span>
<span data-ttu-id="eb69b-163">Реализация предусматривает возможность планирования действий в случае потери подключения к серверу синхронизации.</span><span class="sxs-lookup"><span data-stu-id="eb69b-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="eb69b-164">Вы можете воспользоваться одной из нескольких моделей. Выбор зависит от ответов на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="eb69b-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="eb69b-165">Насколько приемлема для вас ситуация, когда вы не можете вносить изменения в объекты в Azure AD во время простоя?</span><span class="sxs-lookup"><span data-stu-id="eb69b-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="eb69b-166">Если вы используете синхронизацию паролей, согласятся ли пользователи использовать старые пароли в Azure AD в случае их изменения в локальной среде?</span><span class="sxs-lookup"><span data-stu-id="eb69b-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="eb69b-167">Зависите ли вы от выполняемых в реальном времени операций, таких как обратная запись паролей?</span><span class="sxs-lookup"><span data-stu-id="eb69b-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="eb69b-168">В зависимости от политики вашей организации и ответов на эти вопросы можно реализовать одну из следующих стратегий:</span><span class="sxs-lookup"><span data-stu-id="eb69b-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="eb69b-169">Восстановление при необходимости.</span><span class="sxs-lookup"><span data-stu-id="eb69b-169">Rebuild when needed.</span></span>
* <span data-ttu-id="eb69b-170">Наличие запасного резервного сервера ( **промежуточный режим**).</span><span class="sxs-lookup"><span data-stu-id="eb69b-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="eb69b-171">Использование виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="eb69b-171">Use virtual machines.</span></span>

<span data-ttu-id="eb69b-172">Если встроенная база данных SQL Express не используется, просмотрите раздел [Высокий уровень доступности сервера SQL](#sql-high-availability) .</span><span class="sxs-lookup"><span data-stu-id="eb69b-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="eb69b-173">Восстановление при необходимости</span><span class="sxs-lookup"><span data-stu-id="eb69b-173">Rebuild when needed</span></span>
<span data-ttu-id="eb69b-174">Одна из эффективных стратегий заключается в возможности восстановления сервера при необходимости.</span><span class="sxs-lookup"><span data-stu-id="eb69b-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="eb69b-175">Обычно установка модуля синхронизации и выполнение начального импорта и синхронизации занимают несколько часов.</span><span class="sxs-lookup"><span data-stu-id="eb69b-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="eb69b-176">Если нет резервного сервера, модуль синхронизации можно временно разместить на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="eb69b-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="eb69b-177">Сервер модуля синхронизации не сохраняет состояние объектов, поэтому базу данных можно восстановить из данных в Active Directory и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb69b-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="eb69b-178">Для объединения объектов из локальной среды и облака используется атрибут **sourceAnchor** .</span><span class="sxs-lookup"><span data-stu-id="eb69b-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="eb69b-179">Если восстанавливается сервер с имеющимися объектами в локальной среде и в облаке, то при повторной установке модуль синхронизации повторно сопоставляет эти объекты.</span><span class="sxs-lookup"><span data-stu-id="eb69b-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="eb69b-180">Изменения в конфигурации сервера, в частности изменения в правилах фильтрации и синхронизации, необходимо задокументировать и сохранить.</span><span class="sxs-lookup"><span data-stu-id="eb69b-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="eb69b-181">Эти пользовательские конфигурации необходимо применить повторно перед началом синхронизации.</span><span class="sxs-lookup"><span data-stu-id="eb69b-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="eb69b-182">Наличие запасного резервного сервера (промежуточный режим)</span><span class="sxs-lookup"><span data-stu-id="eb69b-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="eb69b-183">В более сложной среде рекомендуется использовать один или несколько резервных серверов.</span><span class="sxs-lookup"><span data-stu-id="eb69b-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="eb69b-184">Во время установки один из серверов можно перевести в **промежуточный режим**.</span><span class="sxs-lookup"><span data-stu-id="eb69b-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="eb69b-185">Дополнительные сведения см. в разделе [Промежуточный режим](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="eb69b-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="eb69b-186">Использование виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="eb69b-186">Use virtual machines</span></span>
<span data-ttu-id="eb69b-187">Также поддерживается распространенный метод, предусматривающий работу модуля синхронизации на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="eb69b-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="eb69b-188">Если на узле возникнут проблемы, образ сервера с модулем синхронизации можно будет перенести на другой сервер.</span><span class="sxs-lookup"><span data-stu-id="eb69b-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="eb69b-189">Высокий уровень доступности сервера SQL</span><span class="sxs-lookup"><span data-stu-id="eb69b-189">SQL High Availability</span></span>
<span data-ttu-id="eb69b-190">Если вы не используете выпуск SQL Server Express, входящий в Azure AD Connect, вам следует также рассмотреть обеспечение высокого уровня доступности для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eb69b-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="eb69b-191">Поддерживаются такие решения высокого уровня доступности, как кластеры SQL и группы доступности AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="eb69b-191">The high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="eb69b-192">Такие решения, как зеркальное отображение, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="eb69b-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="eb69b-193">Поддержка групп доступности AlwaysOn SQL добавлена в Azure AD Connect в версии 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="eb69b-193">Support for SQL AOA was added to Azure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="eb69b-194">Перед установкой Azure AD Connect включите группы доступности AlwaysOn SQL.</span><span class="sxs-lookup"><span data-stu-id="eb69b-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="eb69b-195">При установке Azure AD Connect определяет, включена ли в указанном экземпляре SQL функция SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="eb69b-195">During installation, Azure AD Connect detects whether the SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="eb69b-196">Если функция SQL AOA включена, то Azure AD Connect определяет, какая в SQL AOA настроена репликация (синхронная или асинхронная).</span><span class="sxs-lookup"><span data-stu-id="eb69b-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured to use synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="eb69b-197">При настройке прослушивателя группы доступности рекомендуется задать свойству RegisterAllProvidersIP значение 0.</span><span class="sxs-lookup"><span data-stu-id="eb69b-197">When setting up the Availability Group Listener, it is recommended that you set the RegisterAllProvidersIP property to 0.</span></span> <span data-ttu-id="eb69b-198">Это требуется то той причине, что для подключения к SQL служба Azure AD Connect сейчас использует SQL Native Client, а SQL Native Client не поддерживает свойство MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="eb69b-198">This is because Azure AD Connect currently uses SQL Native Client to connect to SQL and SQL Native Client does not support the use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="eb69b-199">Приложение CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="eb69b-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="eb69b-200">Сведения об использовании этого сценария см. в разделе [Проверка](#verify).</span><span class="sxs-lookup"><span data-stu-id="eb69b-200">See the section [verify](#verify) on how to use this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have the basics, go get the details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="eb69b-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb69b-201">Next steps</span></span>
<span data-ttu-id="eb69b-202">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="eb69b-202">**Overview topics**</span></span>  

* [<span data-ttu-id="eb69b-203">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="eb69b-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="eb69b-204">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb69b-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
