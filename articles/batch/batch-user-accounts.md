---
title: "Выполнение задач с учетными записями пользователей в пакетной службе Azure | Документация Майкрософт"
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
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="d33c7-103">Выполнение задач с учетными записями пользователей в пакетной службе</span><span class="sxs-lookup"><span data-stu-id="d33c7-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="d33c7-104">Задача в пакетной службе Azure всегда выполняется с учетной записью пользователя.</span><span class="sxs-lookup"><span data-stu-id="d33c7-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="d33c7-105">По умолчанию задачи выполняются со стандартными учетными записями пользователей без разрешений администратора.</span><span class="sxs-lookup"><span data-stu-id="d33c7-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="d33c7-106">Как правило, параметров этих учетных записей пользователей по умолчанию достаточно.</span><span class="sxs-lookup"><span data-stu-id="d33c7-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="d33c7-107">Тем не менее, в определенных ситуациях полезно иметь возможность настроить учетную запись пользователя для выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="d33c7-108">В этой статье рассматриваются типы учетных записей пользователей и их настройка для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="d33c7-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="d33c7-109">Типы учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="d33c7-109">Types of user accounts</span></span>

<span data-ttu-id="d33c7-110">В пакетной службе Azure доступны два типа учетных записей пользователей:</span><span class="sxs-lookup"><span data-stu-id="d33c7-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="d33c7-111">**Автоматические учетные записи пользователей.**</span><span class="sxs-lookup"><span data-stu-id="d33c7-111">**Auto-user accounts.**</span></span> <span data-ttu-id="d33c7-112">Это встроенные учетные записи пользователей, создаваемые пакетной службой автоматически.</span><span class="sxs-lookup"><span data-stu-id="d33c7-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="d33c7-113">По умолчанию задачи выполняются с автоматической учетной записью пользователя.</span><span class="sxs-lookup"><span data-stu-id="d33c7-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="d33c7-114">Вы можете настроить спецификацию автоматических пользователей для задачи, чтобы указать, с какой учетной записью задача должна выполняться.</span><span class="sxs-lookup"><span data-stu-id="d33c7-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="d33c7-115">Спецификация автоматических пользователей позволяет указать уровень прав и область автоматической учетной записи пользователя для выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="d33c7-116">**Именованная учетная запись пользователя.**</span><span class="sxs-lookup"><span data-stu-id="d33c7-116">**A named user account.**</span></span> <span data-ttu-id="d33c7-117">При создании пула можно указать одну или несколько именованных учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="d33c7-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="d33c7-118">Каждая учетная запись пользователя создается на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="d33c7-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="d33c7-119">Помимо имени учетной записи указывается ее пароль и уровень прав, а также закрытый ключ SSH для пулов Linux.</span><span class="sxs-lookup"><span data-stu-id="d33c7-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="d33c7-120">При добавлении задачи можно указать именованную учетную запись пользователя, с которой должна выполняться эта задача.</span><span class="sxs-lookup"><span data-stu-id="d33c7-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d33c7-121">В пакетной службе версии 2017-01-01.4.0 введено критическое изменение, требующее обновления кода для вызова этой версии.</span><span class="sxs-lookup"><span data-stu-id="d33c7-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="d33c7-122">Если вы переносите код из более ранней версии пакетной службы, имейте ввиду, что свойство **runElevated** больше не поддерживается в клиентских библиотеках пакетной службы или REST API.</span><span class="sxs-lookup"><span data-stu-id="d33c7-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="d33c7-123">Используйте новое свойство задачи **userIdentity** для указания уровня прав.</span><span class="sxs-lookup"><span data-stu-id="d33c7-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="d33c7-124">В разделе [Обновление кода для использования последней версии клиентской библиотеки пакетной службы](#update-your-code-to-the-latest-batch-client-library) приведены краткие инструкции по обновлению кода для пакетной службы в случае, если используется одна из клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="d33c7-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="d33c7-125">Учетные записи пользователей, описанные в этой статье, не поддерживают протокол удаленного рабочего стола (RDP) или протокол Secure Shell (SSH) по соображениям безопасности.</span><span class="sxs-lookup"><span data-stu-id="d33c7-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="d33c7-126">Подключение к узлу с конфигурацией виртуальной машины Linux по протоколу SSH описывается в разделе [Установка и настройка удаленного рабочего стола для подключения к виртуальной машине Linux в Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="d33c7-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="d33c7-127">Подключение к узлам под управлением Windows по протоколу RDP описывается в разделе [Как подключиться к виртуальной машине Azure под управлением Windows и войти на нее](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="d33c7-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="d33c7-128">Чтобы подключиться к узлу, на котором выполняется конфигурация облачной службы, по протоколу RDP, ознакомьтесь с разделом [Включение подключения к удаленному рабочему столу для роли в облачных службах Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d33c7-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="d33c7-129">Доступ учетных записей пользователей к файлам и каталогам</span><span class="sxs-lookup"><span data-stu-id="d33c7-129">User account access to files and directories</span></span>

<span data-ttu-id="d33c7-130">Автоматические и именованные учетные записи пользователей имеют доступ на чтение и запись к рабочему каталогу задачи, общему каталогу и каталогу многоэкземплярных задач.</span><span class="sxs-lookup"><span data-stu-id="d33c7-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="d33c7-131">Учетные записи обоих типов имеют доступ на чтение к каталогам запуска и подготовки заданий.</span><span class="sxs-lookup"><span data-stu-id="d33c7-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="d33c7-132">Если задача выполняется с учетной записью, которая использовалась для выполнения задачи запуска, то у этой задачи есть доступ на чтение и запись к каталогу задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="d33c7-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="d33c7-133">Аналогично, если задача выполняется с учетной записью, которая использовалась для выполнения задачи подготовки заданий, то у этой задачи есть доступ на чтение и запись к каталогу задачи подготовки заданий.</span><span class="sxs-lookup"><span data-stu-id="d33c7-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="d33c7-134">Если задача выполняется с учетной записью, отличной от той, что использовалась для выполнения задачи запуска или задачи подготовки заданий, то у этой задачи есть доступ только для чтения к соответствующим каталогам.</span><span class="sxs-lookup"><span data-stu-id="d33c7-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="d33c7-135">Дополнительные сведения о доступе к файлам и каталогам из задачи см. в разделе [Разработка решений для крупномасштабных параллельных вычислений с использованием пакетной службы](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="d33c7-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="d33c7-136">Повышенные права доступа для задач</span><span class="sxs-lookup"><span data-stu-id="d33c7-136">Elevated access for tasks</span></span> 

<span data-ttu-id="d33c7-137">Уровень прав учетной записи пользователя показывает, выполняется ли задача с повышенными правами доступа.</span><span class="sxs-lookup"><span data-stu-id="d33c7-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="d33c7-138">Автоматическая и именованная учетная запись пользователя могут выполнять задачи с повышенными правами доступа.</span><span class="sxs-lookup"><span data-stu-id="d33c7-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="d33c7-139">Ниже приведены два варианта уровня прав.</span><span class="sxs-lookup"><span data-stu-id="d33c7-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="d33c7-140">**NonAdmin:** задача выполняется от имени стандартного пользователя, без повышения прав доступа.</span><span class="sxs-lookup"><span data-stu-id="d33c7-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="d33c7-141">Уровнем прав по умолчанию для учетной записи пользователя пакетной службы всегда является **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="d33c7-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="d33c7-142">**Admin:** задача запускается от имени пользователя с повышенными правами доступа и получает все разрешения администратора.</span><span class="sxs-lookup"><span data-stu-id="d33c7-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="d33c7-143">Автоматические учетные записи пользователей</span><span class="sxs-lookup"><span data-stu-id="d33c7-143">Auto-user accounts</span></span>

<span data-ttu-id="d33c7-144">По умолчанию задачи выполняются в пакетной службе с автоматической учетной записью пользователя от имени стандартного пользователя без повышенных прав доступа и в области задачи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="d33c7-145">Если для области задачи настроена спецификация автоматических пользователей, пакетная служба создает автоматическую учетную запись пользователя для выполнения только этой задачи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="d33c7-146">Альтернативой области задач является область пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="d33c7-147">Если для области пула настроена спецификация автоматических пользователей, задача выполняется с автоматической учетной записью пользователя, доступной для любой задачи в пуле.</span><span class="sxs-lookup"><span data-stu-id="d33c7-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="d33c7-148">Дополнительные сведения об области пула см. в разделе [Выполнение задачи от имени автоматического пользователя с областью пула](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="d33c7-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="d33c7-149">Область по умолчанию отличается на узлах Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="d33c7-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="d33c7-150">На узлах Windows задачи выполняются в области задачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d33c7-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="d33c7-151">Узлы Linux всегда выполняют задачи в области пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="d33c7-152">Существуют четыре возможные конфигурации для спецификации автоматических пользователей, каждая из которых соответствует уникальной автоматической учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="d33c7-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="d33c7-153">Доступ от имени стандартного пользователя с областью задачи (спецификация автоматических пользователей по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="d33c7-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="d33c7-154">Доступ от имени администратора (с повышенными правами) с областью задачи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="d33c7-155">Доступ от имени стандартного пользователя с областью пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="d33c7-156">Доступ от имени администратора с областью пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d33c7-157">Задачи, выполняемые в области задачи, фактически не имеют доступа к другим задачам на узле.</span><span class="sxs-lookup"><span data-stu-id="d33c7-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="d33c7-158">Тем не менее пользователь-злоумышленник, имеющий доступ к учетной записи, может обойти это ограничение, отправив задачу, которая запускается с привилегиями администратора и обращается к каталогам других задач.</span><span class="sxs-lookup"><span data-stu-id="d33c7-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="d33c7-159">Пользователь-злоумышленник может также использовать протокол RDP или SSH для подключения к узлу.</span><span class="sxs-lookup"><span data-stu-id="d33c7-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="d33c7-160">Очень важно защитить доступ к ключам учетной записи пакетной службы, чтобы предотвратить подобную ситуацию.</span><span class="sxs-lookup"><span data-stu-id="d33c7-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="d33c7-161">Если вы подозреваете, что ключ учетной записи был скомпрометирован, обязательно повторно создайте свои ключи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="d33c7-162">Выполнение задачи от имени автоматического пользователя с повышенными правами доступа</span><span class="sxs-lookup"><span data-stu-id="d33c7-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="d33c7-163">При необходимости выполнить задачу с повышенным уровнем доступа можно настроить спецификацию автоматических пользователей с привилегиями администратора.</span><span class="sxs-lookup"><span data-stu-id="d33c7-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="d33c7-164">Например, задаче запуска может потребоваться повышенный уровень доступа для установки программного обеспечения на узле.</span><span class="sxs-lookup"><span data-stu-id="d33c7-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="d33c7-165">В общем случае повышенный уровень доступа лучше использовать только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d33c7-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="d33c7-166">Рекомендуется предоставлять минимальные привилегии, необходимые для достижения желаемого результата.</span><span class="sxs-lookup"><span data-stu-id="d33c7-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="d33c7-167">Например, если задача запуска устанавливает программное обеспечение для текущего пользователя, а не для всех пользователей, можно избежать предоставления задачам повышенных прав доступа.</span><span class="sxs-lookup"><span data-stu-id="d33c7-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="d33c7-168">Вы можете настроить спецификацию автоматических пользователей для области пула и доступа от имени стандартного пользователя для всех задач, которые должны выполняться с одной и той же учетной записью, включая задачу запуска.</span><span class="sxs-lookup"><span data-stu-id="d33c7-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="d33c7-169">В следующих фрагментах кода показано, как настроить спецификацию автоматических пользователей.</span><span class="sxs-lookup"><span data-stu-id="d33c7-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="d33c7-170">В примерах задается уровень прав `Admin` и область `Task`.</span><span class="sxs-lookup"><span data-stu-id="d33c7-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="d33c7-171">Область задач является параметром по умолчанию, но приведена для примера.</span><span class="sxs-lookup"><span data-stu-id="d33c7-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="d33c7-172">.NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="d33c7-173">Java для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="d33c7-174">Python для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="d33c7-175">Выполнение задачи от имени автоматического пользователя с областью пула</span><span class="sxs-lookup"><span data-stu-id="d33c7-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="d33c7-176">При подготовке каждого узла в пуле на нем создаются две автоматические учетные записи пользователей, действующие во всем пуле: одна с повышенными правами доступа, а вторая — без повышенных прав доступа.</span><span class="sxs-lookup"><span data-stu-id="d33c7-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="d33c7-177">Если для выполнения задачи от имени автоматического пользователя указать область пула, то эта задача будет выполняться с одной из этих двух автоматических учетных записей пользователей пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="d33c7-178">Если указать область пула для автоматического пользователя, то все задачи, которые выполняются с правами администратора, выполняются с одной и той же автоматической учетной записью пользователя пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="d33c7-179">Аналогичным образом задачи, которые выполняются без разрешений администратора, также выполняются с одной автоматической учетной записью пользователя пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="d33c7-180">Две автоматические учетные записи пользователей пула — это отдельные учетные записи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="d33c7-181">Задачи, которые выполняются с учетной записью пула с правами администратора, не могут обмениваться данными с задачами, выполняемыми со стандартной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="d33c7-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="d33c7-182">Преимущество выполнения с одной автоматической учетной записью заключается в возможности обмениваться данными с другими задачами, выполняющимися на одном узле.</span><span class="sxs-lookup"><span data-stu-id="d33c7-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="d33c7-183">Совместное использование секретов задачами — один из сценариев, в которых удобно выполнять задачи в одной из двух автоматически учетных записей пользователей пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="d33c7-184">Для примера предположим, что задаче запуска необходимо подготовить секрет на узле, который могут использовать другие задачи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="d33c7-185">Можно использовать API защиты данных Windows (DPAPI), но это требует привилегий администратора.</span><span class="sxs-lookup"><span data-stu-id="d33c7-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="d33c7-186">Вместо этого вы можете защитить секрет на уровне пользователя.</span><span class="sxs-lookup"><span data-stu-id="d33c7-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="d33c7-187">Задачи, которые выполняются с одной учетной записью пользователя, могут обращаться к этому секрету без повышенных прав доступа.</span><span class="sxs-lookup"><span data-stu-id="d33c7-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="d33c7-188">Еще один сценарий, в котором требуется выполнять задачи с автоматической учетной записью пользователя с областью пула, — использование файлового ресурса MPI.</span><span class="sxs-lookup"><span data-stu-id="d33c7-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="d33c7-189">Файловый ресурс MPI удобно использовать, когда узлам в задаче MPI нужно работать с одними и теми же данными.</span><span class="sxs-lookup"><span data-stu-id="d33c7-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="d33c7-190">Головной узел создает файловый ресурс, доступ к которому дочерние узлы могут получить, если они работают с той же автоматической учетной записью пользователя.</span><span class="sxs-lookup"><span data-stu-id="d33c7-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="d33c7-191">В следующем фрагменте кода для выполнения задачи от имени автоматического пользователя задается область пула с помощью .NET пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d33c7-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="d33c7-192">Уровень прав пропущен, поэтому задача выполняется со стандартной автоматической учетной записью пользователя пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="d33c7-193">Именованные учетные записи пользователей</span><span class="sxs-lookup"><span data-stu-id="d33c7-193">Named user accounts</span></span>

<span data-ttu-id="d33c7-194">При создании пула можно определить именованные учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="d33c7-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="d33c7-195">Для именованной учетной записи пользователя указываются имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="d33c7-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="d33c7-196">Кроме того, для нее можно уровень прав.</span><span class="sxs-lookup"><span data-stu-id="d33c7-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="d33c7-197">Для узлов Linux можно также предоставить закрытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="d33c7-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="d33c7-198">Именованная учетная запись пользователя существует на всех узлах в пуле и доступна для всех задач на этих узлах.</span><span class="sxs-lookup"><span data-stu-id="d33c7-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="d33c7-199">Для пула можно определить любое число именованных пользователей.</span><span class="sxs-lookup"><span data-stu-id="d33c7-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="d33c7-200">При добавлении задачи или коллекции задач можно указать, что она выполняется с одной из именованных учетных записей пользователя, определенных в пуле.</span><span class="sxs-lookup"><span data-stu-id="d33c7-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="d33c7-201">Именованную учетную запись пользователя удобно использовать, если нужно выполнить все задачи в задании с одной учетной записью, но изолировать их от задач, параллельно выполняемых в других заданиях.</span><span class="sxs-lookup"><span data-stu-id="d33c7-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="d33c7-202">Например, можно создать именованного пользователя для каждого задания и выполнять задачи каждого задания с этой именованной учетной записью пользователя.</span><span class="sxs-lookup"><span data-stu-id="d33c7-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="d33c7-203">В этом случае каждое задание сможет передать секрет своим задачам, но не задачам, выполняемым в других заданиях.</span><span class="sxs-lookup"><span data-stu-id="d33c7-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="d33c7-204">Кроме того, именованную учетную запись пользователя можно использовать для выполнения задачи, которая устанавливает разрешения для внешних ресурсов, например файловых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d33c7-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="d33c7-205">С помощью именованной учетной записи пользователя можно контролировать удостоверение пользователя и использовать его для задания разрешений.</span><span class="sxs-lookup"><span data-stu-id="d33c7-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="d33c7-206">Применяя именованные учетные записи пользователей, можно обеспечить SSH-подключение без пароля между узлами Linux.</span><span class="sxs-lookup"><span data-stu-id="d33c7-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="d33c7-207">Именованную учетную запись пользователя можно использовать на узлах Linux, на которых требуется выполнять многоэкземплярные задачи.</span><span class="sxs-lookup"><span data-stu-id="d33c7-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="d33c7-208">Каждый узел в пуле может выполнять задачи с учетной записью пользователя, определенной для всего пула.</span><span class="sxs-lookup"><span data-stu-id="d33c7-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="d33c7-209">Дополнительные сведения о многоэкземплярных задачах см. в разделе [Использование задач с \-несколькими экземплярами для запуска приложений с интерфейсом передачи сообщений в пакетной службе](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="d33c7-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="d33c7-210">Создание именованных учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="d33c7-210">Create named user accounts</span></span>

<span data-ttu-id="d33c7-211">Чтобы создать именованные учетные записи пользователей в пакетной службе, добавьте коллекцию учетных записей пользователей в пул.</span><span class="sxs-lookup"><span data-stu-id="d33c7-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="d33c7-212">В следующих фрагментах кода показано создание именованных учетных записей пользователей на языках .NET, Java и Python.</span><span class="sxs-lookup"><span data-stu-id="d33c7-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="d33c7-213">Эти фрагменты кода демонстрируют создание именованной учетной записи администратора и стандартной именованной учетной записи в пуле.</span><span class="sxs-lookup"><span data-stu-id="d33c7-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="d33c7-214">Приведенные примеры создают пулы, используя конфигурацию облачной службы, но этот же подход используется при создании пула Windows или Linux с помощью конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d33c7-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="d33c7-215">Пример использования .NET в пакетной службе (Windows)</span><span class="sxs-lookup"><span data-stu-id="d33c7-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
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

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="d33c7-216">Пример использования .NET в пакетной службе (Linux)</span><span class="sxs-lookup"><span data-stu-id="d33c7-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
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

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="d33c7-217">Пример на Java для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="d33c7-218">Пример на Python для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="d33c7-219">Выполнение задачи с именованной учетной записью пользователя с повышенными правами доступа</span><span class="sxs-lookup"><span data-stu-id="d33c7-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="d33c7-220">Чтобы выполнить задачу от имени пользователя с повышенными правами, в ее свойстве **UserIdentity** укажите именованную учетную запись пользователя, при создании которой ее свойству **ElevationLevel** было присвоено значение `Admin`.</span><span class="sxs-lookup"><span data-stu-id="d33c7-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="d33c7-221">Этот фрагмент кода указывает, что задание должно выполняться с именованной учетной записью пользователя.</span><span class="sxs-lookup"><span data-stu-id="d33c7-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="d33c7-222">Эта именованная учетная запись пользователя была определен в пуле во время его создания.</span><span class="sxs-lookup"><span data-stu-id="d33c7-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="d33c7-223">В данном случае именованная учетная запись пользователя была создана с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="d33c7-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="d33c7-224">Обновление кода для использования последней версии клиентской библиотеки пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="d33c7-225">В пакетной службе версии 2017-01-01.4.0 введено критическое изменение: свойство **runElevated**, доступное в предыдущих версиях, заменено свойством **userIdentity**.</span><span class="sxs-lookup"><span data-stu-id="d33c7-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="d33c7-226">В следующих таблицах представлено простое сопоставление, которое можно использовать для обновления кода, использующего более ранние версии клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="d33c7-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="d33c7-227">.NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-227">Batch .NET</span></span>

| <span data-ttu-id="d33c7-228">Если в коде используется…</span><span class="sxs-lookup"><span data-stu-id="d33c7-228">If your code uses...</span></span>                  | <span data-ttu-id="d33c7-229">Замените его на…</span><span class="sxs-lookup"><span data-stu-id="d33c7-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="d33c7-230">Свойство `CloudTask.RunElevated` не указано</span><span class="sxs-lookup"><span data-stu-id="d33c7-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="d33c7-231">Обновление не требуется.</span><span class="sxs-lookup"><span data-stu-id="d33c7-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="d33c7-232">Java для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-232">Batch Java</span></span>

| <span data-ttu-id="d33c7-233">Если в коде используется…</span><span class="sxs-lookup"><span data-stu-id="d33c7-233">If your code uses...</span></span>                      | <span data-ttu-id="d33c7-234">Замените его на…</span><span class="sxs-lookup"><span data-stu-id="d33c7-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="d33c7-235">Свойство `CloudTask.withRunElevated` не указано</span><span class="sxs-lookup"><span data-stu-id="d33c7-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="d33c7-236">Обновление не требуется.</span><span class="sxs-lookup"><span data-stu-id="d33c7-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="d33c7-237">Python для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d33c7-237">Batch Python</span></span>

| <span data-ttu-id="d33c7-238">Если в коде используется…</span><span class="sxs-lookup"><span data-stu-id="d33c7-238">If your code uses...</span></span>                      | <span data-ttu-id="d33c7-239">Замените его на…</span><span class="sxs-lookup"><span data-stu-id="d33c7-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="d33c7-240">`user_identity=user`, where</span><span class="sxs-lookup"><span data-stu-id="d33c7-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="d33c7-241">`user_identity=user`, where</span><span class="sxs-lookup"><span data-stu-id="d33c7-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="d33c7-242">Свойство `run_elevated` не указано</span><span class="sxs-lookup"><span data-stu-id="d33c7-242">`run_elevated` not specified</span></span> | <span data-ttu-id="d33c7-243">Обновление не требуется.</span><span class="sxs-lookup"><span data-stu-id="d33c7-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="d33c7-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d33c7-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="d33c7-245">Форум по Пакетной службе</span><span class="sxs-lookup"><span data-stu-id="d33c7-245">Batch Forum</span></span>

<span data-ttu-id="d33c7-246">На [форуме по пакетной службе Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) на сайте MSDN можно обсудить пакетную службу и задать вопросы о ней.</span><span class="sxs-lookup"><span data-stu-id="d33c7-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="d33c7-247">Изучайте полезные закрепленные сообщения и задавайте вопросы, возникающие во время сборки пакетных решений.</span><span class="sxs-lookup"><span data-stu-id="d33c7-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>