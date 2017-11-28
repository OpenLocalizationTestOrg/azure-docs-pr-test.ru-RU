---
title: "Синхронизация Azure AD Connect: рабочие задачи и рекомендации | Документация Майкрософт"
description: "В этом разделе описываются рабочие задачи в Azure AD Connect sync и как tooprepare для работы этого компонента."
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
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="53a44-103">Службы синхронизации Azure AD Connect: рабочие задачи и рекомендации</span><span class="sxs-lookup"><span data-stu-id="53a44-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="53a44-104">Hello цель этого раздела — toodescribe рабочие задачи синхронизации Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="53a44-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="53a44-105">Промежуточный режим</span><span class="sxs-lookup"><span data-stu-id="53a44-105">Staging mode</span></span>
<span data-ttu-id="53a44-106">Промежуточный режим может использоваться в нескольких ситуациях, например:</span><span class="sxs-lookup"><span data-stu-id="53a44-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="53a44-107">обеспечение высокой доступности;</span><span class="sxs-lookup"><span data-stu-id="53a44-107">High availability.</span></span>
* <span data-ttu-id="53a44-108">тестирование и развертывание новых изменений в конфигурации;</span><span class="sxs-lookup"><span data-stu-id="53a44-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="53a44-109">Ввести новый сервер и списать старый hello.</span><span class="sxs-lookup"><span data-stu-id="53a44-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="53a44-110">С сервером в промежуточный режим можно изменять toohello изменения конфигурации и предварительного просмотра hello прежде чем вносить active hello server.</span><span class="sxs-lookup"><span data-stu-id="53a44-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="53a44-111">Оно также позволяет toorun полный импорт и полную синхронизацию tooverify ожидается все изменения, прежде чем использовать эти изменения в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="53a44-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="53a44-112">Во время установки можно выбрать toobe сервера hello в **промежуточный режим**.</span><span class="sxs-lookup"><span data-stu-id="53a44-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="53a44-113">Это действие hello сервер становится активной для импорта и синхронизации, но не выполняется никаким экспортам.</span><span class="sxs-lookup"><span data-stu-id="53a44-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="53a44-114">Сервер в промежуточном режиме не выполняет синхронизацию и обратную запись паролей, даже если эти функции активированы при установке.</span><span class="sxs-lookup"><span data-stu-id="53a44-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="53a44-115">Если отключить промежуточный режим hello server начинается экспорт, включает синхронизацию паролей и включает обратную запись паролей.</span><span class="sxs-lookup"><span data-stu-id="53a44-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="53a44-116">Экспорт по-прежнему можно принудительно с помощью диспетчера службы синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="53a44-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="53a44-117">На сервере в режиме промежуточного по-прежнему tooreceive изменения из Active Directory и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53a44-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="53a44-118">Он всегда имеет копию hello последних изменений и может очень быстро примите через обязанности hello другого сервера.</span><span class="sxs-lookup"><span data-stu-id="53a44-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="53a44-119">При внесении изменения конфигурации: tooyour основной сервер, это toomake вашей обязанностью hello того же сервера toohello изменения в промежуточный режим.</span><span class="sxs-lookup"><span data-stu-id="53a44-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="53a44-120">Для тех, кто с использованием сведений из старых технологий синхронизации hello промежуточный режим отличается, так как сервер hello имеет собственную базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="53a44-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="53a44-121">Такая архитектура позволяет hello промежуточных toobe режим сервера, расположенный в другом центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="53a44-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="53a44-122">Проверка конфигурации hello сервера</span><span class="sxs-lookup"><span data-stu-id="53a44-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="53a44-123">tooapply этот метод, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="53a44-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="53a44-124">Подготовка</span><span class="sxs-lookup"><span data-stu-id="53a44-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="53a44-125">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="53a44-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="53a44-126">Импорт и синхронизация</span><span class="sxs-lookup"><span data-stu-id="53a44-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="53a44-127">Проверка</span><span class="sxs-lookup"><span data-stu-id="53a44-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="53a44-128">Переключение активного сервера</span><span class="sxs-lookup"><span data-stu-id="53a44-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="53a44-129">Подготовка.</span><span class="sxs-lookup"><span data-stu-id="53a44-129">Prepare</span></span>
1. <span data-ttu-id="53a44-130">Установить Azure AD Connect, выберите **промежуточный режим**и отмените выделение **начать синхронизацию** на последней странице приветствия мастера установки hello.</span><span class="sxs-lookup"><span data-stu-id="53a44-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="53a44-131">Этот режим позволяет подсистема синхронизации hello toorun вручную.</span><span class="sxs-lookup"><span data-stu-id="53a44-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="53a44-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="53a44-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="53a44-133">Знак off/входа и выберите в меню Пуск hello **служба синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="53a44-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="53a44-134">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="53a44-134">Configuration</span></span>
<span data-ttu-id="53a44-135">Если были внесены пользовательские изменения toohello основного сервера и конфигурации hello toocompare выполнялись с тестового сервера hello, используйте [Архивариус конфигурации Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="53a44-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="53a44-136">Импорт и синхронизация</span><span class="sxs-lookup"><span data-stu-id="53a44-136">Import and Synchronize</span></span>
1. <span data-ttu-id="53a44-137">Выберите **соединители**, и выберите hello первый соединитель с типом hello **доменных служб Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53a44-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="53a44-138">Щелкните **Запуск**, выберите **Полный импорт** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="53a44-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="53a44-139">Проделайте это для всех соединителей данного типа.</span><span class="sxs-lookup"><span data-stu-id="53a44-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="53a44-140">Выберите hello соединитель с типом **Azure Active Directory (Майкрософт)**.</span><span class="sxs-lookup"><span data-stu-id="53a44-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="53a44-141">Щелкните **Запуск**, выберите **Полный импорт** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="53a44-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="53a44-142">Убедитесь, что по-прежнему выбрана вкладка hello соединители.</span><span class="sxs-lookup"><span data-stu-id="53a44-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="53a44-143">Для каждого соединителя типа **Доменные службы Active Directory** щелкните **Запуск**, выберите **Синхронизация изменений** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="53a44-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="53a44-144">Выберите hello соединитель с типом **Azure Active Directory (Майкрософт)**.</span><span class="sxs-lookup"><span data-stu-id="53a44-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="53a44-145">Щелкните **Запуск**, выберите**Синхронизация изменений**) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="53a44-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="53a44-146">У вас теперь промежуточные экспорта изменяет tooAzure AD и локальной AD (при использовании гибридного развертывания Exchange).</span><span class="sxs-lookup"><span data-stu-id="53a44-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="53a44-147">Дальнейшие действия Hello разрешить tooinspect, что такое о toochange перед запуском hello Экспорт toohello каталогов.</span><span class="sxs-lookup"><span data-stu-id="53a44-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="53a44-148">Проверка.</span><span class="sxs-lookup"><span data-stu-id="53a44-148">Verify</span></span>
1. <span data-ttu-id="53a44-149">Запустите командную строку и перейдите в слишком`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="53a44-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="53a44-150">Запуск: `csexport "Name of Connector" %temp%\export.xml /f:x` имя hello hello соединителя можно найти в службе синхронизации.</span><span class="sxs-lookup"><span data-stu-id="53a44-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="53a44-151">Она имеет аналогичные too"contoso.com имя — AAD» для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53a44-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="53a44-152">Скопируйте сценарий PowerShell hello из раздела hello [CSAnalyzer](#appendix-csanalyzer) tooa файл с именем `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="53a44-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="53a44-153">Откройте окно PowerShell и найдите папку toohello, где создан сценарий PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="53a44-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="53a44-154">Выполните команду `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="53a44-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="53a44-155">Теперь у вас есть файл **processedusers1.csv**, который можно просмотреть в Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="53a44-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="53a44-156">В этом файле находятся tooAzure toobe экспортировать все промежуточные изменения AD.</span><span class="sxs-lookup"><span data-stu-id="53a44-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="53a44-157">Внесите необходимые изменения toohello данные или конфигурация и выполните эти шаги еще раз (импорта и синхронизации и проверьте) пока ожидаются изменения, которые будут экспортированы toobe приветствия.</span><span class="sxs-lookup"><span data-stu-id="53a44-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="53a44-158">Переключение активного сервера</span><span class="sxs-lookup"><span data-stu-id="53a44-158">Switch active server</span></span>
1. <span data-ttu-id="53a44-159">На сервере активной hello Выключите сервер hello (DirSync/FIM/Azure AD Sync), поэтому он не выполняет экспорт tooAzure AD или установите его в промежуточный режим (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="53a44-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="53a44-160">Запустите мастер установки hello на сервере hello в **промежуточный режим** и отключить **промежуточный режим**.</span><span class="sxs-lookup"><span data-stu-id="53a44-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="53a44-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="53a44-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="53a44-162">Аварийное восстановление</span><span class="sxs-lookup"><span data-stu-id="53a44-162">Disaster recovery</span></span>
<span data-ttu-id="53a44-163">Реализация конструктора hello входит tooplan для какой toodo в случае аварии где потерять hello сервера синхронизации.</span><span class="sxs-lookup"><span data-stu-id="53a44-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="53a44-164">Существуют различные модели toouse и какие один toouse зависит от нескольких факторов, включая:</span><span class="sxs-lookup"><span data-stu-id="53a44-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="53a44-165">Что такое допустимым не может делать изменений tooobjects в Azure AD во время простоя hello</span><span class="sxs-lookup"><span data-stu-id="53a44-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="53a44-166">При использовании синхронизации паролей пользователей hello принимаете наличие toouse Здравствуй, старый пароль в Azure AD в случае, если они изменяются в локальной среде?</span><span class="sxs-lookup"><span data-stu-id="53a44-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="53a44-167">Зависите ли вы от выполняемых в реальном времени операций, таких как обратная запись паролей?</span><span class="sxs-lookup"><span data-stu-id="53a44-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="53a44-168">В зависимости от hello ответы toothese вопросы и политике вашей организации можно реализовать одним из следующих стратегий hello:</span><span class="sxs-lookup"><span data-stu-id="53a44-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="53a44-169">Восстановление при необходимости.</span><span class="sxs-lookup"><span data-stu-id="53a44-169">Rebuild when needed.</span></span>
* <span data-ttu-id="53a44-170">Наличие запасного резервного сервера ( **промежуточный режим**).</span><span class="sxs-lookup"><span data-stu-id="53a44-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="53a44-171">Использование виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="53a44-171">Use virtual machines.</span></span>

<span data-ttu-id="53a44-172">Если hello встроенной базы данных SQL Express не используется, то следует также просмотреть hello [высокого уровня доступности SQL](#sql-high-availability) раздела.</span><span class="sxs-lookup"><span data-stu-id="53a44-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="53a44-173">Восстановление при необходимости</span><span class="sxs-lookup"><span data-stu-id="53a44-173">Rebuild when needed</span></span>
<span data-ttu-id="53a44-174">Стратегии реальную — tooplan для перестроения сервера, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="53a44-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="53a44-175">Как правило установке hello подсистема синхронизации и hello первоначального импорта и синхронизации можно выполнить в течение нескольких часов.</span><span class="sxs-lookup"><span data-stu-id="53a44-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="53a44-176">Если запасной сервер недоступен, это возможных tootemporarily использовать механизм синхронизации toohost hello домена контроллера.</span><span class="sxs-lookup"><span data-stu-id="53a44-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="53a44-177">сервер подсистемы синхронизации Hello не хранят любое состояние, об объектах hello, hello базы данных можно восстановить из данных hello в Active Directory и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53a44-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="53a44-178">Hello **sourceAnchor** атрибута является используемым toojoin hello объекты из локальной и облачной hello.</span><span class="sxs-lookup"><span data-stu-id="53a44-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="53a44-179">При повторном построении сервера hello с существующие объекты в локальной и hello облака, а затем hello синхронизирует engine совпадения этих объектов в повторной установки еще раз.</span><span class="sxs-lookup"><span data-stu-id="53a44-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="53a44-180">Hello требуется toodocument и сохранить обстоятельства hello общий доступ к изменениям конфигурации сервера toohello, такие как правила фильтрации и синхронизации.</span><span class="sxs-lookup"><span data-stu-id="53a44-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="53a44-181">Эти пользовательские конфигурации необходимо применить повторно перед началом синхронизации.</span><span class="sxs-lookup"><span data-stu-id="53a44-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="53a44-182">Наличие запасного резервного сервера (промежуточный режим)</span><span class="sxs-lookup"><span data-stu-id="53a44-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="53a44-183">В более сложной среде рекомендуется использовать один или несколько резервных серверов.</span><span class="sxs-lookup"><span data-stu-id="53a44-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="53a44-184">Во время установки, можно включить сервер toobe в **промежуточный режим**.</span><span class="sxs-lookup"><span data-stu-id="53a44-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="53a44-185">Дополнительные сведения см. в разделе [Промежуточный режим](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="53a44-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="53a44-186">Использование виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="53a44-186">Use virtual machines</span></span>
<span data-ttu-id="53a44-187">Общие и поддерживаемый метод — подсистема синхронизации hello toorun на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="53a44-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="53a44-188">В случае узла hello имеется проблема, hello изображения с сервера ядра СУБД hello синхронизации может быть перенесенных tooanother сервер.</span><span class="sxs-lookup"><span data-stu-id="53a44-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="53a44-189">Высокий уровень доступности сервера SQL</span><span class="sxs-lookup"><span data-stu-id="53a44-189">SQL High Availability</span></span>
<span data-ttu-id="53a44-190">Высокий уровень доступности для SQL Server следует также рассматривать, если не используется SQL Server Express, входящий в состав Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="53a44-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="53a44-191">решения высокого уровня доступности Hello поддерживается включают кластеры SQL и AOA (группы доступности AlwaysOn).</span><span class="sxs-lookup"><span data-stu-id="53a44-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="53a44-192">Такие решения, как зеркальное отображение, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="53a44-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="53a44-193">Поддержка SQL AOA была добавлена tooAzure AD Connect версии 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="53a44-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="53a44-194">Перед установкой Azure AD Connect включите функцию SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="53a44-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="53a44-195">Во время установки Azure AD Connect определяет, включен ли указанный экземпляр SQL hello для SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="53a44-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="53a44-196">При включении SQL AOA дальнейшей Azure AD Connect определяет, является ли SQL AOA настроенных toouse Синхронная репликация или асинхронная репликация.</span><span class="sxs-lookup"><span data-stu-id="53a44-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="53a44-197">При настройке прослушивателя группы доступности hello, рекомендуется установить свойство too0 hello RegisterAllProvidersIP.</span><span class="sxs-lookup"><span data-stu-id="53a44-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="53a44-198">Это так, как Azure AD Connect в настоящее время использует собственный клиент SQL tooconnect tooSQL и собственный клиент SQL не поддерживает использование hello MultiSubNetFailover свойства.</span><span class="sxs-lookup"><span data-stu-id="53a44-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="53a44-199">Приложение CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="53a44-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="53a44-200">В разделе hello [проверить](#verify) о том, как toouse этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="53a44-200">See hello section [verify](#verify) on how toouse this script.</span></span>

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

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
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

    #now that we have hello basics, go get hello details

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

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="53a44-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53a44-201">Next steps</span></span>
<span data-ttu-id="53a44-202">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="53a44-202">**Overview topics**</span></span>  

* [<span data-ttu-id="53a44-203">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="53a44-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="53a44-204">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53a44-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
