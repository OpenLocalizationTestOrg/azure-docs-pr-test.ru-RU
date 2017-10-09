---
title: "aaaRun задачи, связанные с учетными записями пользователей в пакете Azure | Документы Microsoft"
description: "Настройка учетных записей пользователей для выполнения задач в пакетной службе Azure."
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="8f8ab-103">Выполнение задач с учетными записями пользователей в пакетной службе</span><span class="sxs-lookup"><span data-stu-id="8f8ab-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="8f8ab-104">Задача в пакетной службе Azure всегда выполняется с учетной записью пользователя.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="8f8ab-105">По умолчанию задачи выполняются со стандартными учетными записями пользователей без разрешений администратора.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="8f8ab-106">Как правило, параметров этих учетных записей пользователей по умолчанию достаточно.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="8f8ab-107">Для определенных сценариев Однако это полезно toobe учетной записи для пользователя может tooconfigure hello в которой вы хотите toorun задачи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="8f8ab-108">В этой статье рассматриваются типы hello учетных записей пользователей и настройке их для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="8f8ab-109">Типы учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="8f8ab-109">Types of user accounts</span></span>

<span data-ttu-id="8f8ab-110">В пакетной службе Azure доступны два типа учетных записей пользователей:</span><span class="sxs-lookup"><span data-stu-id="8f8ab-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="8f8ab-111">**Автоматические учетные записи пользователей.**</span><span class="sxs-lookup"><span data-stu-id="8f8ab-111">**Auto-user accounts.**</span></span> <span data-ttu-id="8f8ab-112">Учетные записи пользователей автоматически являются встроенные учетные записи пользователей, создаваемых автоматически hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="8f8ab-113">По умолчанию задачи выполняются с автоматической учетной записью пользователя.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="8f8ab-114">Вы можете настроить hello спецификации tooindicate задачи, с какой пользователь автоматически должна выполняться задача учетной записи пользователя автоматически.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="8f8ab-115">Спецификация автоматического пользователя Hello позволяет toospecify уровня прав hello и область действия учетной записи пользователя автоматически hello, который будет выполняться задача hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="8f8ab-116">**Именованная учетная запись пользователя.**</span><span class="sxs-lookup"><span data-stu-id="8f8ab-116">**A named user account.**</span></span> <span data-ttu-id="8f8ab-117">При создании пула hello, можно указать один или несколько учетных записей пользователей с именем для пула.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="8f8ab-118">Каждая учетная запись создается на каждом узле hello пула.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="8f8ab-119">В дополнение к этому toohello имя учетной записи, укажите пароль учетной записи пользователя hello, повышение уровня, а также для Linux пулах, hello закрытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="8f8ab-120">При добавлении задачи, можно указать с именем учетной записи пользователя, с которым должна выполняться эта задача hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="8f8ab-121">версия обновления пакета Hello 2017 г-01-01.4.0 содержит критические изменения, необходимо обновить ваш код toocall этой версии.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="8f8ab-122">Если перенос кода из более старой версии пакета, обратите внимание, что hello **runElevated** свойство больше не поддерживается в клиентских библиотек hello API-интерфейса REST или пакета.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="8f8ab-123">Используйте hello новый **Удостоверение_пользователя** свойства задачи toospecify повышение уровня.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="8f8ab-124">См. раздел hello [обновление библиотеки клиента последней пакета кода toohello](#update-your-code-to-the-latest-batch-client-library) быстрого инструкции для обновления кода пакета, если вы используете одну из библиотек клиентских hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="8f8ab-125">учетные записи пользователей Hello, рассматриваемые в данной статье не поддерживают протокол удаленного рабочего стола (RDP) или Secure Shell (SSH), по соображениям безопасности.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="8f8ab-126">. в разделе tooconnect tooa узел выполняющегося hello Linux конфигурации виртуальной машины через SSH, [tooa использование удаленного рабочего стола виртуальной Машины Linux в Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="8f8ab-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="8f8ab-127">см. под управлением Windows с помощью протокола RDP, toonodes tooconnect [подключения tooa виртуальной Машины Windows Server](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="8f8ab-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="8f8ab-128">в разделе tooconnect tooa узел выполняющегося hello конфигурацию облачной службы по этому Протоколу, [включить удаленный рабочий стол для роли в облачных службах Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8f8ab-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="8f8ab-129">Toofiles доступа учетной записи пользователя и каталогов</span><span class="sxs-lookup"><span data-stu-id="8f8ab-129">User account access toofiles and directories</span></span>

<span data-ttu-id="8f8ab-130">Учетная запись пользователя автоматически и учетной записи пользователя с именем имеют задаче для чтения и записи доступа toohello рабочий каталог, общий каталог и каталог задачи нескольких экземпляров.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="8f8ab-131">Обоих типов учетных записей имеют доступ на чтение toohello запуска задания подготовки каталоги и.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="8f8ab-132">Если задача запускается с hello же учетная запись, которая использовалась для запуска задачи запуска, задачу hello имеет доступ на чтение запись toohello начала задачи каталог.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="8f8ab-133">Аналогично, если задача запускается с hello же учетная запись, использованная для выполнения задачи подготовки задания, задачу hello имеет каталог задач подготовки задания toohello доступ для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="8f8ab-134">Если задача выполняется с другой учетной записью, чем hello запуска задачи или задачи подготовки задания, задачу hello имеет только доступ на чтение toohello соответствующий каталог.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="8f8ab-135">Дополнительные сведения о доступе к файлам и каталогам из задачи см. в разделе [Разработка решений для крупномасштабных параллельных вычислений с использованием пакетной службы](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="8f8ab-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="8f8ab-136">Повышенные права доступа для задач</span><span class="sxs-lookup"><span data-stu-id="8f8ab-136">Elevated access for tasks</span></span> 

<span data-ttu-id="8f8ab-137">Повышение уровня учетной записи пользователя Hello указывает, выполняется ли задача с повышенными правами доступа.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="8f8ab-138">Автоматическая и именованная учетная запись пользователя могут выполнять задачи с повышенными правами доступа.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="8f8ab-139">Ниже приведены два варианта Hello для повышения уровня:</span><span class="sxs-lookup"><span data-stu-id="8f8ab-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="8f8ab-140">**NonAdmin:** задачу hello выполняется как обычный пользователь без повышенных прав привилегированного доступа.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="8f8ab-141">всегда является Hello уровня прав по умолчанию для учетной записи пользователя пакета **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="8f8ab-142">**Администрирование:** задачу hello запускается от имени пользователя с повышенными правами доступа и работает с полными правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="8f8ab-143">Автоматические учетные записи пользователей</span><span class="sxs-lookup"><span data-stu-id="8f8ab-143">Auto-user accounts</span></span>

<span data-ttu-id="8f8ab-144">По умолчанию задачи выполняются в пакетной службе с автоматической учетной записью пользователя от имени стандартного пользователя без повышенных прав доступа и в области задачи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="8f8ab-145">При настройке hello пользователя автоматически спецификации для области задач hello пакетная служба создает для этой задачи только учетную запись пользователя автоматически.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="8f8ab-146">Hello альтернативных tootask область — область пула.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="8f8ab-147">При настройке hello пользователя автоматически спецификации задачи для области пула задачу hello выполняется под учетной записью пользователя автоматически, доступных tooany задач в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="8f8ab-148">Дополнительные сведения об области пула разделе hello [выполнение задачи, как hello auto пользователя с областью видимости пула](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="8f8ab-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="8f8ab-149">область по умолчанию Hello отличается на узлах Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="8f8ab-150">На узлах Windows задачи выполняются в области задачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="8f8ab-151">Узлы Linux всегда выполняют задачи в области пула.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="8f8ab-152">Существует четыре возможных конфигурации для спецификации пользователя автоматически hello, каждое из которых соответствует tooa уникальную auto-учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="8f8ab-153">Доступ без прав администратора с областью задач (определение пользователя автоматически hello по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="8f8ab-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="8f8ab-154">Доступ от имени администратора (с повышенными правами) с областью задачи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="8f8ab-155">Доступ от имени стандартного пользователя с областью пула.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="8f8ab-156">Доступ от имени администратора с областью пула.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="8f8ab-157">Задачи, выполняемые в области задач нет фактически доступ tooother задачи на узле.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="8f8ab-158">Тем не менее злонамеренный пользователь с учетной записью доступа toohello удалось обойти это ограничение, отправляя задачу, которая выполняется с правами администратора и получает доступ к другим каталогам задачи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="8f8ab-159">Пользователь-злоумышленник также можно использовать узел tooa tooconnect RDP или SSH.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="8f8ab-160">Это важные tooprotect доступа tooyour пакета ключей учетной записи tooprevent такой сценарий.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="8f8ab-161">Если есть подозрение, что ваша учетная запись была скомпрометирована, быть tooregenerate убедиться, что ваши ключи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="8f8ab-162">Выполнение задачи от имени автоматического пользователя с повышенными правами доступа</span><span class="sxs-lookup"><span data-stu-id="8f8ab-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="8f8ab-163">При необходимости toorun задачи с помощью повышенные права доступа, можно настроить hello спецификации автоматически пользователя права администратора.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="8f8ab-164">Например задача запуска может понадобиться программного обеспечения tooinstall повышенные права доступа на узле hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="8f8ab-165">Как правило, лучше всего подходит toouse расширенные права доступа только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="8f8ab-166">Рекомендуется предоставление hello минимальными правами доступа необходимые tooachieve hello желаемого результата.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="8f8ab-167">Например если начальная задача устанавливает программное обеспечение для текущего пользователя hello, вместо того, для всех пользователей может быть доступ tooavoid предоставление tootasks повышенные права доступа.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="8f8ab-168">Вы можете настроить hello спецификации автоматически пользователя для доступа к области и не являющихся администраторами пула для всех задач, требующих toorun в учетную запись, включая задачи запуска hello hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="8f8ab-169">Hello следующие фрагменты кода показывают, как tooconfigure hello спецификации пользователя автоматически.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="8f8ab-170">Примеры Hello уровень hello повышение слишком`Admin` и hello области слишком`Task`.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="8f8ab-171">Область задач установлен по умолчанию hello, но включается в список ради hello примера.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="8f8ab-172">.NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f8ab-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="8f8ab-173">Java для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f8ab-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="8f8ab-174">Python для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f8ab-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="8f8ab-175">Выполнение задачи от имени автоматического пользователя с областью пула</span><span class="sxs-lookup"><span data-stu-id="8f8ab-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="8f8ab-176">При подготовке узла две всему пулу auto-учетные записи пользователей создаются на каждом узле в пуле hello, с повышенные права доступа и без повышенных прав привилегированного доступа.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="8f8ab-177">Настройка области toopool области hello auto пользователя для данной задачи запускает задачу hello в одном из этих учетных записей два пользователя автоматически всему пулу.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="8f8ab-178">При указании области пула для hello auto пользователя всех задач, которые выполняются с правами администратора запускаться hello одной учетной записи пользователя автоматически всему пулу.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="8f8ab-179">Аналогичным образом задачи, которые выполняются без разрешений администратора, также выполняются с одной автоматической учетной записью пользователя пула.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="8f8ab-180">два пользователя автоматически всему пулу Hello представляют отдельные учетные записи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="8f8ab-181">Задачи, выполняемые в группе hello пула административных учетных записей не может обмениваться данными задачи, выполняемые hello стандартной учетной записью и наоборот.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="8f8ab-182">Здравствуйте, преимущество toorunning под одной учетной записи пользователя автоматически является задачи могли tooshare данных с помощью других задач, выполняющихся на hello hello того же узла.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="8f8ab-183">Общий доступ к секретной информации между задачами-один сценарий, когда выполнение задачи, связанные с одной из учетных записей пользователей автоматически всему пулу hello двух полезно.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="8f8ab-184">Например предположим, что задача запуска должен tooprovision секрет на узле hello, можно использовать другие задачи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="8f8ab-185">Можно использовать hello API защиты данных Windows (DPAPI), но он требует наличия прав администратора.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="8f8ab-186">Вместо этого можно защитить секрет hello на уровне пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="8f8ab-187">Секрет без повышенных прав привилегированного доступа hello задач, выполняемых в рамках hello, можно получить доступ к одной учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="8f8ab-188">Совместное использование другой сценарий, где вы можете toorun задачи, связанные с учетной записи пользователя автоматически с областью видимости пул — это файл интерфейса передачи сообщений (MPI).</span><span class="sxs-lookup"><span data-stu-id="8f8ab-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="8f8ab-189">Общий файловый ресурс MPI полезно в том случае, если узлы hello в toowork необходимость задача hello MPI на hello и те же данные файла.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="8f8ab-190">Hello головного узла создает общую папку, hello дочерние узлы можно получить доступ, если они выполняются в рамках hello же учетной записи пользователя автоматически.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="8f8ab-191">Следующий фрагмент кода Hello устанавливается область toopool область hello auto пользователя для задачи в пакете .NET.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="8f8ab-192">Повышение уровня Hello опущен, поэтому задачу hello запускается под учетной записью обычного пользователя автоматически всему пулу hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="8f8ab-193">Именованные учетные записи пользователей</span><span class="sxs-lookup"><span data-stu-id="8f8ab-193">Named user accounts</span></span>

<span data-ttu-id="8f8ab-194">При создании пула можно определить именованные учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="8f8ab-195">Для именованной учетной записи пользователя указываются имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="8f8ab-196">Можно указать hello уровня прав для учетной записи пользователя с именем.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="8f8ab-197">Для узлов Linux можно также предоставить закрытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="8f8ab-198">Учетную запись пользователя с именем существует на всех узлах в кластере hello и задачи доступны tooall работает на этих узлах.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="8f8ab-199">Для пула можно определить любое число именованных пользователей.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="8f8ab-200">При добавлении задачи или коллекцию задач, можно указать, что задача hello будет запускаться под одной из учетных записей пользователей, определенных для пула hello с именем hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="8f8ab-201">Учетную запись пользователя с именем полезен при необходимости toorun всех задач в задании в разделе hello же учетной записью пользователя, но изолировать их друг от задачи, выполняемые в других заданиях на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="8f8ab-202">Например, можно создать именованного пользователя для каждого задания и выполнять задачи каждого задания с этой именованной учетной записью пользователя.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="8f8ab-203">В этом случае каждое задание сможет передать секрет своим задачам, но не задачам, выполняемым в других заданиях.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="8f8ab-204">Можно также использовать toorun учетной записи пользователя с именем задачу, которая задает разрешения на внешние ресурсы, такие как общие файловые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="8f8ab-205">С учетной записью пользователя с именем контролировать удостоверение пользователя hello и можно использовать разрешения tooset удостоверение этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="8f8ab-206">Применяя именованные учетные записи пользователей, можно обеспечить SSH-подключение без пароля между узлами Linux.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="8f8ab-207">Можно использовать учетную запись пользователя с именем с узлами Linux, требующие toorun многоэкземплярные задачи.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="8f8ab-208">Каждый узел в пул hello можно выполнять задачи с учетной записью пользователя, определенные для всего пула hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="8f8ab-209">Дополнительные сведения о задачах нескольких экземпляров см. в разделе [используется несколькими\-экземпляр задачи приложений MPI toorun](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="8f8ab-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="8f8ab-210">Создание именованных учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="8f8ab-210">Create named user accounts</span></span>

<span data-ttu-id="8f8ab-211">toocreate с именем учетные записи пользователей в пакете, добавить коллекцию пула toohello учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="8f8ab-212">Hello следующих фрагментах кода показано, как учетные записи пользователей в .NET, Java и Python с именем toocreate.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="8f8ab-213">Эти Показать фрагменты кода как toocreate администратора и учетные записи в пуле с именем без прав администратора.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="8f8ab-214">Примеры Hello создавать пулы с использованием hello конфигурацию облачной службы, но использовать же подход при создании пула Windows или Linux с помощью конфигурации виртуальной машины hello hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="8f8ab-215">Пример использования .NET в пакетной службе (Windows)</span><span class="sxs-lookup"><span data-stu-id="8f8ab-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="8f8ab-216">Пример использования .NET в пакетной службе (Linux)</span><span class="sxs-lookup"><span data-stu-id="8f8ab-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="8f8ab-217">Пример на Java для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f8ab-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="8f8ab-218">Пример на Python для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f8ab-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="8f8ab-219">Выполнение задачи с именованной учетной записью пользователя с повышенными правами доступа</span><span class="sxs-lookup"><span data-stu-id="8f8ab-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="8f8ab-220">toorun задачи как с повышенными правами пользователя, задачу hello набор **Удостоверение_пользователя** tooa свойство с именем учетной записи пользователя, который был создан с его **ElevationLevel** значение свойства слишком`Admin`.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="8f8ab-221">Этот фрагмент кода указывает, что задача hello должны выполняться под учетной записью пользователя с именем.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="8f8ab-222">Эта учетная запись пользователя с именем был определен в пуле hello при создании пула hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="8f8ab-223">В этом случае hello с именем учетной записи пользователя была создана с правами администратора:</span><span class="sxs-lookup"><span data-stu-id="8f8ab-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="8f8ab-224">Обновление библиотеки клиента последней пакета кода toohello</span><span class="sxs-lookup"><span data-stu-id="8f8ab-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="8f8ab-225">2017 г-01-01.4.0 содержит критические изменения, заменив hello версия обновления пакета Hello **runElevated** свойства доступны в предыдущих версиях с hello **Удостоверение_пользователя** свойство.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="8f8ab-226">следующие таблицы Hello предоставляют простой сопоставления, которые можно использовать tooupdate кода из более ранних версий клиентских библиотек hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="8f8ab-227">.NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f8ab-227">Batch .NET</span></span>

| <span data-ttu-id="8f8ab-228">Если в коде используется…</span><span class="sxs-lookup"><span data-stu-id="8f8ab-228">If your code uses...</span></span>                  | <span data-ttu-id="8f8ab-229">Замените его на…</span><span class="sxs-lookup"><span data-stu-id="8f8ab-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="8f8ab-230">Свойство `CloudTask.RunElevated` не указано</span><span class="sxs-lookup"><span data-stu-id="8f8ab-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="8f8ab-231">Обновление не требуется.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="8f8ab-232">Java для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f8ab-232">Batch Java</span></span>

| <span data-ttu-id="8f8ab-233">Если в коде используется…</span><span class="sxs-lookup"><span data-stu-id="8f8ab-233">If your code uses...</span></span>                      | <span data-ttu-id="8f8ab-234">Замените его на…</span><span class="sxs-lookup"><span data-stu-id="8f8ab-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="8f8ab-235">Свойство `CloudTask.withRunElevated` не указано</span><span class="sxs-lookup"><span data-stu-id="8f8ab-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="8f8ab-236">Обновление не требуется.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="8f8ab-237">Python для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f8ab-237">Batch Python</span></span>

| <span data-ttu-id="8f8ab-238">Если в коде используется…</span><span class="sxs-lookup"><span data-stu-id="8f8ab-238">If your code uses...</span></span>                      | <span data-ttu-id="8f8ab-239">Замените его на…</span><span class="sxs-lookup"><span data-stu-id="8f8ab-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="8f8ab-240">`user_identity=user`, where</span><span class="sxs-lookup"><span data-stu-id="8f8ab-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="8f8ab-241">`user_identity=user`, where</span><span class="sxs-lookup"><span data-stu-id="8f8ab-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="8f8ab-242">Свойство `run_elevated` не указано</span><span class="sxs-lookup"><span data-stu-id="8f8ab-242">`run_elevated` not specified</span></span> | <span data-ttu-id="8f8ab-243">Обновление не требуется.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="8f8ab-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f8ab-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="8f8ab-245">Форум по Пакетной службе</span><span class="sxs-lookup"><span data-stu-id="8f8ab-245">Batch Forum</span></span>

<span data-ttu-id="8f8ab-246">Hello [форум по пакетной Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) на сайте MSDN — лучшие поместите toodiscuss пакета и ответы на вопросы о службе hello.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="8f8ab-247">Изучайте полезные закрепленные сообщения и задавайте вопросы, возникающие во время сборки пакетных решений.</span><span class="sxs-lookup"><span data-stu-id="8f8ab-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
