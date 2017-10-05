---
title: "Обзор контроля доступа в Data Lake Store | Документация Майкрософт"
description: "В этой статье описаны принципы контроля доступа в Azure Data Lake Store."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 99fbad770290d280bdec490d988391ad276ce1ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="644f0-103">Контроль доступа в Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="644f0-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="644f0-104">В хранилище Azure Data Lake Store реализована модель контроля доступа на базе HDFS, которая в свою очередь основана на модели контроля доступа POSIX.</span><span class="sxs-lookup"><span data-stu-id="644f0-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from the POSIX access control model.</span></span> <span data-ttu-id="644f0-105">В этой статье приведены общие сведения о модели контроля доступа в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-105">This article summarizes the basics of the access control model for Data Lake Store.</span></span> <span data-ttu-id="644f0-106">Подробная информация о модели контроля доступа на базе HDFS представлена в [руководстве по разрешениям в HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="644f0-106">To learn more about the HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="644f0-107">Списки управления доступом для файлов и папок</span><span class="sxs-lookup"><span data-stu-id="644f0-107">Access control lists on files and folders</span></span>

<span data-ttu-id="644f0-108">Существует два типа списков управления доступом (ACL): **ACL для доступа** и **ACL по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="644f0-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="644f0-109">**ACL для доступа.** Эти списки позволяют управлять доступом к объекту.</span><span class="sxs-lookup"><span data-stu-id="644f0-109">**Access ACLs**: These control access to an object.</span></span> <span data-ttu-id="644f0-110">Списки ACL для доступа позволяют управлять доступом как к файлам, так и к папкам.</span><span class="sxs-lookup"><span data-stu-id="644f0-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="644f0-111">**ACL по умолчанию.** "Шаблон" списков управления доступом, связанных с папкой, определяющей списки ACL для доступа любого дочернего элемента, созданного в этой папке.</span><span class="sxs-lookup"><span data-stu-id="644f0-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine the Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="644f0-112">Файлы не имеют ACL по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="644f0-112">Files do not have Default ACLs.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="644f0-114">Списки ACL для доступа и ACL по умолчанию имеют одинаковую структуру.</span><span class="sxs-lookup"><span data-stu-id="644f0-114">Both Access ACLs and Default ACLs have the same structure.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="644f0-116">Изменение ACL по умолчанию в родительском объекте не оказывает влияния на ACL для доступа или ACL по умолчанию для уже существующих дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="644f0-116">Changing the Default ACL on a parent does not affect the Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="644f0-117">Пользователи и удостоверения</span><span class="sxs-lookup"><span data-stu-id="644f0-117">Users and identities</span></span>

<span data-ttu-id="644f0-118">Каждый файл или папка имеет отдельные разрешения для следующих удостоверений:</span><span class="sxs-lookup"><span data-stu-id="644f0-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="644f0-119">владелец файла;</span><span class="sxs-lookup"><span data-stu-id="644f0-119">The owning user of the file</span></span>
* <span data-ttu-id="644f0-120">группа владельцев;</span><span class="sxs-lookup"><span data-stu-id="644f0-120">The owning group</span></span>
* <span data-ttu-id="644f0-121">именованные пользователи;</span><span class="sxs-lookup"><span data-stu-id="644f0-121">Named users</span></span>
* <span data-ttu-id="644f0-122">именованные группы;</span><span class="sxs-lookup"><span data-stu-id="644f0-122">Named groups</span></span>
* <span data-ttu-id="644f0-123">все остальные пользователи.</span><span class="sxs-lookup"><span data-stu-id="644f0-123">All other users</span></span>

<span data-ttu-id="644f0-124">Удостоверения пользователей и групп являются удостоверениями Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="644f0-124">The identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="644f0-125">Если не указано иное, "пользователь" в контексте Data Lake Store может означать либо пользователя AAD, либо группу безопасности AAD.</span><span class="sxs-lookup"><span data-stu-id="644f0-125">So unless otherwise noted, a "user," in the context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="644f0-126">Разрешения</span><span class="sxs-lookup"><span data-stu-id="644f0-126">Permissions</span></span>

<span data-ttu-id="644f0-127">Разрешения для объекта файловой системы делятся на **разрешения на чтение**, **разрешения на запись** и **разрешения на выполнение**. Разрешения применяются к файлам и папкам, как показано в таблице ниже:</span><span class="sxs-lookup"><span data-stu-id="644f0-127">The permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in the following table:</span></span>

|            |    <span data-ttu-id="644f0-128">Файл</span><span class="sxs-lookup"><span data-stu-id="644f0-128">File</span></span>     |   <span data-ttu-id="644f0-129">Папка</span><span class="sxs-lookup"><span data-stu-id="644f0-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="644f0-130">**Разрешение на чтение (R)**</span><span class="sxs-lookup"><span data-stu-id="644f0-130">**Read (R)**</span></span> | <span data-ttu-id="644f0-131">Чтение содержимого файла</span><span class="sxs-lookup"><span data-stu-id="644f0-131">Can read the contents of a file</span></span> | <span data-ttu-id="644f0-132">Для просмотра содержимого папки требуются **разрешения на чтение** и **выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-132">Requires **Read** and **Execute** to list the contents of the folder</span></span>|
| <span data-ttu-id="644f0-133">**Разрешение на запись (W)**</span><span class="sxs-lookup"><span data-stu-id="644f0-133">**Write (W)**</span></span> | <span data-ttu-id="644f0-134">Запись или добавление данных в файл</span><span class="sxs-lookup"><span data-stu-id="644f0-134">Can write or append to a file</span></span> | <span data-ttu-id="644f0-135">Для создания дочерних элементов в папке требуются **разрешения на запись** и **выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-135">Requires **Write** and **Execute** to create child items in a folder</span></span> |
| <span data-ttu-id="644f0-136">**Разрешение на выполнение (X)**</span><span class="sxs-lookup"><span data-stu-id="644f0-136">**Execute (X)**</span></span> | <span data-ttu-id="644f0-137">Не имеет значения в контексте Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="644f0-137">Does not mean anything in the context of Data Lake Store</span></span> | <span data-ttu-id="644f0-138">Требуется для просмотра дочерних элементов папки.</span><span class="sxs-lookup"><span data-stu-id="644f0-138">Required to traverse the child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="644f0-139">Сокращения для разрешений</span><span class="sxs-lookup"><span data-stu-id="644f0-139">Short forms for permissions</span></span>

<span data-ttu-id="644f0-140">**RWX** означает разрешения на **чтение, запись и выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-140">**RWX** is used to indicate **Read + Write + Execute**.</span></span> <span data-ttu-id="644f0-141">Существует еще более краткая форма — цифровая, согласно которой **чтение = 4**, **запись = 2**, **выполнение = 1**, а их сумма выражает предоставленные разрешения.</span><span class="sxs-lookup"><span data-stu-id="644f0-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, the sum of which represents the permissions.</span></span> <span data-ttu-id="644f0-142">Ниже приводятся некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="644f0-142">Following are some examples.</span></span>

| <span data-ttu-id="644f0-143">Цифровая форма</span><span class="sxs-lookup"><span data-stu-id="644f0-143">Numeric form</span></span> | <span data-ttu-id="644f0-144">Краткая форма</span><span class="sxs-lookup"><span data-stu-id="644f0-144">Short form</span></span> |      <span data-ttu-id="644f0-145">Значение</span><span class="sxs-lookup"><span data-stu-id="644f0-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="644f0-146">7</span><span class="sxs-lookup"><span data-stu-id="644f0-146">7</span></span>            | <span data-ttu-id="644f0-147">RWX</span><span class="sxs-lookup"><span data-stu-id="644f0-147">RWX</span></span>        | <span data-ttu-id="644f0-148">чтение, запись и выполнение</span><span class="sxs-lookup"><span data-stu-id="644f0-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="644f0-149">5</span><span class="sxs-lookup"><span data-stu-id="644f0-149">5</span></span>            | <span data-ttu-id="644f0-150">R-X</span><span class="sxs-lookup"><span data-stu-id="644f0-150">R-X</span></span>        | <span data-ttu-id="644f0-151">Чтение + выполнение</span><span class="sxs-lookup"><span data-stu-id="644f0-151">Read + Execute</span></span>         |
| <span data-ttu-id="644f0-152">4</span><span class="sxs-lookup"><span data-stu-id="644f0-152">4</span></span>            | <span data-ttu-id="644f0-153">R--</span><span class="sxs-lookup"><span data-stu-id="644f0-153">R--</span></span>        | <span data-ttu-id="644f0-154">чтение</span><span class="sxs-lookup"><span data-stu-id="644f0-154">Read</span></span>                   |
| <span data-ttu-id="644f0-155">0</span><span class="sxs-lookup"><span data-stu-id="644f0-155">0</span></span>            | ---        | <span data-ttu-id="644f0-156">Нет разрешений</span><span class="sxs-lookup"><span data-stu-id="644f0-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="644f0-157">Разрешения не наследуются</span><span class="sxs-lookup"><span data-stu-id="644f0-157">Permissions do not inherit</span></span>

<span data-ttu-id="644f0-158">В модели на основе POSIX, используемой в Data Lake Store, разрешения для элемента хранятся в самом элементе.</span><span class="sxs-lookup"><span data-stu-id="644f0-158">In the POSIX-style model that's used by Data Lake Store, permissions for an item are stored on the item itself.</span></span> <span data-ttu-id="644f0-159">Другими словами, разрешения на доступ к элементу не могут быть унаследованы от родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="644f0-159">In other words, permissions for an item cannot be inherited from the parent items.</span></span>

## <a name="common-scenarios-related-to-permissions"></a><span data-ttu-id="644f0-160">Типовые сценарии в зависимости от разрешений</span><span class="sxs-lookup"><span data-stu-id="644f0-160">Common scenarios related to permissions</span></span>

<span data-ttu-id="644f0-161">Ниже показано несколько типовых сценариев для наглядного представления того, какие разрешения требуются для выполнения отдельных операций в учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-161">Following are some common scenarios to help you understand which permissions are needed to perform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-to-read-a-file"></a><span data-ttu-id="644f0-162">Разрешения, необходимые для чтения файла</span><span class="sxs-lookup"><span data-stu-id="644f0-162">Permissions needed to read a file</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="644f0-164">Для чтения файла вызывающей стороне требуются разрешения на **чтение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-164">For the file to be read, the caller needs **Read** permissions.</span></span>
* <span data-ttu-id="644f0-165">Для доступа ко всем подпапкам в папке, содержащей файл, вызывающей стороне требуются разрешения на **выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-165">For all the folders in the folder structure that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-append-to-a-file"></a><span data-ttu-id="644f0-166">Разрешения, необходимые для добавления данных в файл</span><span class="sxs-lookup"><span data-stu-id="644f0-166">Permissions needed to append to a file</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="644f0-168">Для добавления данных в файл вызывающей стороне требуются разрешения на **запись**.</span><span class="sxs-lookup"><span data-stu-id="644f0-168">For the file to be appended to, the caller needs **Write** permissions.</span></span>
* <span data-ttu-id="644f0-169">Для доступа ко всем папкам, содержащим файл, вызывающей стороне требуются разрешения на **выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-169">For all the folders that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-delete-a-file"></a><span data-ttu-id="644f0-170">Разрешения, необходимые для удаления файла</span><span class="sxs-lookup"><span data-stu-id="644f0-170">Permissions needed to delete a file</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="644f0-172">Для доступа к родительской папке вызывающей стороне требуются разрешения на **запись и выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-172">For the parent folder, the caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="644f0-173">Для доступа ко всем папкам, указанным в пути к файлу, вызывающей стороне требуются разрешения на **выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-173">For all the other folders in the file’s path, the caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="644f0-174">Для удаления файла разрешения на запись не требуются, если выполняются два предыдущих условия.</span><span class="sxs-lookup"><span data-stu-id="644f0-174">Write permissions on the file are not required to delete it as long as the previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-to-enumerate-a-folder"></a><span data-ttu-id="644f0-175">Разрешения, необходимые для перечисления папки</span><span class="sxs-lookup"><span data-stu-id="644f0-175">Permissions needed to enumerate a folder</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="644f0-177">Для перечисления папки вызывающей стороне требуются разрешения на **чтение и выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-177">For the folder to enumerate, the caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="644f0-178">Для доступа ко всем предыдущим папкам вызывающей стороне требуются разрешения на **выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-178">For all the ancestor folders, the caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-the-azure-portal"></a><span data-ttu-id="644f0-179">Просмотр разрешений на портале Azure</span><span class="sxs-lookup"><span data-stu-id="644f0-179">Viewing permissions in the Azure portal</span></span>

<span data-ttu-id="644f0-180">В колонке **Обозреватель данных** учетной записи Data Lake Store щелкните **Доступ**, чтобы просмотреть списки ACL для файла или папки.</span><span class="sxs-lookup"><span data-stu-id="644f0-180">From the **Data Explorer** blade of the Data Lake Store account, click **Access** to see the ACLs for a file or a folder.</span></span> <span data-ttu-id="644f0-181">При выборе команды **Доступ** вы получите списки ACL для папки **catalog** из учетной записи **mydatastore**.</span><span class="sxs-lookup"><span data-stu-id="644f0-181">Click **Access** to see the ACLs for the **catalog** folder under the **mydatastore** account.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="644f0-183">В верхней части этой колонки указаны имеющиеся разрешения.</span><span class="sxs-lookup"><span data-stu-id="644f0-183">On this blade, the top section shows an overview of the permissions that you have.</span></span> <span data-ttu-id="644f0-184">(На снимке экрана в качестве пользователя указан Боб.) Ниже показаны разрешения на доступ.</span><span class="sxs-lookup"><span data-stu-id="644f0-184">(In the screenshot, the user is Bob.) Following that, the access permissions are shown.</span></span> <span data-ttu-id="644f0-185">Затем в колонке **Доступ** выберите **Простое представление** для просмотра списка в упрощенном виде.</span><span class="sxs-lookup"><span data-stu-id="644f0-185">After that, from the **Access** blade, click **Simple View** to see the simpler view.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="644f0-187">Щелкните **Расширенное представление**, чтобы просмотреть дополнительное представление, в котором содержатся списки ACL по умолчанию, маска и суперпользователь.</span><span class="sxs-lookup"><span data-stu-id="644f0-187">Click **Advanced View** to see the more advanced view, where the concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="the-super-user"></a><span data-ttu-id="644f0-189">Суперпользователь</span><span class="sxs-lookup"><span data-stu-id="644f0-189">The super-user</span></span>

<span data-ttu-id="644f0-190">Суперпользователь обладает самыми широкими правами среди всех пользователей хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-190">A super-user has the most rights of all the users in the Data Lake Store.</span></span> <span data-ttu-id="644f0-191">Суперпользователь:</span><span class="sxs-lookup"><span data-stu-id="644f0-191">A super-user:</span></span>

* <span data-ttu-id="644f0-192">обладает разрешениями RWX для **всех** файлов и папок;</span><span class="sxs-lookup"><span data-stu-id="644f0-192">Has RWX Permissions to **all** files and folders.</span></span>
* <span data-ttu-id="644f0-193">может изменять разрешения для любых файлов или папок;</span><span class="sxs-lookup"><span data-stu-id="644f0-193">Can change the permissions on any file or folder.</span></span>
* <span data-ttu-id="644f0-194">может изменять владельца или группу владельцев любого файла или папки.</span><span class="sxs-lookup"><span data-stu-id="644f0-194">Can change the owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="644f0-195">В учетной записи Azure Data Lake Store предусмотрено несколько ролей Azure, в том числе:</span><span class="sxs-lookup"><span data-stu-id="644f0-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="644f0-196">владельцы;</span><span class="sxs-lookup"><span data-stu-id="644f0-196">Owners</span></span>
* <span data-ttu-id="644f0-197">участники;</span><span class="sxs-lookup"><span data-stu-id="644f0-197">Contributors</span></span>
* <span data-ttu-id="644f0-198">читатели;</span><span class="sxs-lookup"><span data-stu-id="644f0-198">Readers</span></span>

<span data-ttu-id="644f0-199">Каждому пользователю с ролью **Владелец** учетной записи Data Lake Store автоматически присваивается статус суперпользователя этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="644f0-199">Everyone in the **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="644f0-200">Дополнительные сведения см. в статье об [управлении доступом на основе ролей](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="644f0-200">To learn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="644f0-201">Если требуется создать пользовательскую роль RBAC с разрешениями суперпользователя, назначьте ей следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="644f0-201">If you want to create a custom role-based-access control (RBAC) role that has super-user permissions, it needs to have the following permissions:</span></span>
- <span data-ttu-id="644f0-202">Microsoft.DataLakeStore/accounts/Superuser/action;</span><span class="sxs-lookup"><span data-stu-id="644f0-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="644f0-203">Microsoft.Authorization/roleAssignments/write.</span><span class="sxs-lookup"><span data-stu-id="644f0-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="the-owning-user"></a><span data-ttu-id="644f0-204">Владелец</span><span class="sxs-lookup"><span data-stu-id="644f0-204">The owning user</span></span>

<span data-ttu-id="644f0-205">Пользователь, создавший элемент, автоматически становится владельцем элемента.</span><span class="sxs-lookup"><span data-stu-id="644f0-205">The user who created the item is automatically the owning user of the item.</span></span> <span data-ttu-id="644f0-206">Владелец может:</span><span class="sxs-lookup"><span data-stu-id="644f0-206">An owning user can:</span></span>

* <span data-ttu-id="644f0-207">изменять разрешения файла, владельцем которого он является;</span><span class="sxs-lookup"><span data-stu-id="644f0-207">Change the permissions of a file that is owned.</span></span>
* <span data-ttu-id="644f0-208">изменять группу владельцев файла, владельцем которого он является, если владелец файла одновременно является участником целевой группы.</span><span class="sxs-lookup"><span data-stu-id="644f0-208">Change the owning group of a file that is owned, as long as the owning user is also a member of the target group.</span></span>

> [!NOTE]
> <span data-ttu-id="644f0-209">Владелец *не может* изменить владельца другого файла.</span><span class="sxs-lookup"><span data-stu-id="644f0-209">The owning user *cannot* change the owning user of another owned file.</span></span> <span data-ttu-id="644f0-210">Изменить владельца файла или папки может только суперпользователь.</span><span class="sxs-lookup"><span data-stu-id="644f0-210">Only super-users can change the owning user of a file or folder.</span></span>
>
>

## <a name="the-owning-group"></a><span data-ttu-id="644f0-211">группа владельцев;</span><span class="sxs-lookup"><span data-stu-id="644f0-211">The owning group</span></span>

<span data-ttu-id="644f0-212">В списках управления доступом POSIX каждый пользователь связан с "основной группой".</span><span class="sxs-lookup"><span data-stu-id="644f0-212">In the POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="644f0-213">Например, пользователь Алиса принадлежит к группе finance.</span><span class="sxs-lookup"><span data-stu-id="644f0-213">For example, user "alice" might belong to the "finance" group.</span></span> <span data-ttu-id="644f0-214">Пользователь Aлиса может принадлежать к нескольким группам, но одна из них всегда назначается как основная.</span><span class="sxs-lookup"><span data-stu-id="644f0-214">Alice might also belong to multiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="644f0-215">В интерфейсе POSIX, когда пользователь Aлиса создает файл, группа владельцев этого файла задается для основной группы этого пользователя, которой в данном случае является группа finance.</span><span class="sxs-lookup"><span data-stu-id="644f0-215">In POSIX, when Alice creates a file, the owning group of that file is set to her primary group, which in this case is "finance."</span></span>

<span data-ttu-id="644f0-216">При создании нового элемента файловой системы служба Data Lake Store присваивает значение группе владельцев.</span><span class="sxs-lookup"><span data-stu-id="644f0-216">When a new filesystem item is created, Data Lake Store assigns a value to the owning group.</span></span>

* <span data-ttu-id="644f0-217">**Вариант 1.** Корневая папка "/".</span><span class="sxs-lookup"><span data-stu-id="644f0-217">**Case 1**: The root folder "/".</span></span> <span data-ttu-id="644f0-218">Эта папка создается при создании учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="644f0-219">В данном случае группа владельцев закрепляется за пользователем, создавшим эту учетную запись.</span><span class="sxs-lookup"><span data-stu-id="644f0-219">In this case, the owning group is set to the user who created the account.</span></span>
* <span data-ttu-id="644f0-220">**Вариант 2** (во всех остальных случаях). При создании элемента группа владельцев копируется из родительской папки.</span><span class="sxs-lookup"><span data-stu-id="644f0-220">**Case 2** (Every other case): When a new item is created, the owning group is copied from the parent folder.</span></span>

<span data-ttu-id="644f0-221">Группа владельцев может быть изменена:</span><span class="sxs-lookup"><span data-stu-id="644f0-221">The owning group can be changed by:</span></span>
* <span data-ttu-id="644f0-222">одним из суперпользователей;</span><span class="sxs-lookup"><span data-stu-id="644f0-222">Any super-users.</span></span>
* <span data-ttu-id="644f0-223">владельцем, если он является участником целевой группы.</span><span class="sxs-lookup"><span data-stu-id="644f0-223">The owning user, if the owning user is also a member of the target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="644f0-224">Алгоритм проверки доступа</span><span class="sxs-lookup"><span data-stu-id="644f0-224">Access check algorithm</span></span>

<span data-ttu-id="644f0-225">На рисунке ниже показан алгоритм проверки доступа к учетным записям Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-225">The following illustration represents the access check algorithm for Data Lake Store accounts.</span></span>

![Алгоритм работы списков управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="the-mask-and-effective-permissions"></a><span data-ttu-id="644f0-227">Маска и "действующие разрешения"</span><span class="sxs-lookup"><span data-stu-id="644f0-227">The mask and "effective permissions"</span></span>

<span data-ttu-id="644f0-228">**Маска** — это значение RWX, используемое с целью ограничения доступа для **именованных пользователей**, **группы владельцев** и **именованных групп** при выполнении алгоритма проверки доступа.</span><span class="sxs-lookup"><span data-stu-id="644f0-228">The **mask** is an RWX value that is used to limit access for **named users**, the **owning group**, and **named groups** when you're performing the access check algorithm.</span></span> <span data-ttu-id="644f0-229">Ниже представлены основные понятия о масках.</span><span class="sxs-lookup"><span data-stu-id="644f0-229">Here are the key concepts for the mask.</span></span>

* <span data-ttu-id="644f0-230">Маска создает "действующие разрешения",</span><span class="sxs-lookup"><span data-stu-id="644f0-230">The mask creates "effective permissions."</span></span> <span data-ttu-id="644f0-231">то есть изменяет разрешения при проверке доступа.</span><span class="sxs-lookup"><span data-stu-id="644f0-231">That is, it modifies the permissions at the time of access check.</span></span>
* <span data-ttu-id="644f0-232">Маску может изменять непосредственно владелец файла или суперпользователи.</span><span class="sxs-lookup"><span data-stu-id="644f0-232">The mask can be directly edited by the file owner and any super-users.</span></span>
* <span data-ttu-id="644f0-233">Маска может удалять разрешения для создания действующих разрешений.</span><span class="sxs-lookup"><span data-stu-id="644f0-233">The mask can remove permissions to create the effective permission.</span></span> <span data-ttu-id="644f0-234">Маска *не может* добавлять разрешения к действующим разрешениям.</span><span class="sxs-lookup"><span data-stu-id="644f0-234">The mask *cannot* add permissions to the effective permission.</span></span>

<span data-ttu-id="644f0-235">Рассмотрим несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="644f0-235">Let's look at some examples.</span></span> <span data-ttu-id="644f0-236">В следующем примере маска имеет значение **RWX**. Это означает, что она не может удалять какие-либо разрешения.</span><span class="sxs-lookup"><span data-stu-id="644f0-236">In the following example, the mask is set to **RWX**, which means that the mask does not remove any permissions.</span></span> <span data-ttu-id="644f0-237">Действующие разрешения для именованного пользователя, группы владельцев или именованной группы не меняются в процессе проверки доступа.</span><span class="sxs-lookup"><span data-stu-id="644f0-237">The effective permissions for the named user, owning group, and named group are not altered during the access check.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="644f0-239">В следующем примере для маски задано значение **R-X**.</span><span class="sxs-lookup"><span data-stu-id="644f0-239">In the following example, the mask is set to **R-X**.</span></span> <span data-ttu-id="644f0-240">Следовательно, маска **отключает разрешение на запись** для **именованного пользователя**, **группы владельцев** и **именованной группы** при проверке доступа.</span><span class="sxs-lookup"><span data-stu-id="644f0-240">This means that it **turns off the Write permissions** for **named user**, **owning group**, and **named group** at the time of access check.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="644f0-242">Вот как представлена маска файла или папки на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="644f0-242">For reference, here is where the mask for a file or folder appears in the Azure portal.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="644f0-244">В новой учетной записи Data Lake Store маске для списка ACL для доступа и ACL по умолчанию для корневой папки ("/") по умолчанию присваивается значение RWX.</span><span class="sxs-lookup"><span data-stu-id="644f0-244">For a new Data Lake Store account, the mask for the Access ACL and Default ACL of the root folder ("/") defaults to RWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="644f0-245">Разрешения для новых файлов и папок</span><span class="sxs-lookup"><span data-stu-id="644f0-245">Permissions on new files and folders</span></span>

<span data-ttu-id="644f0-246">При создании нового файла или подпапки в существующей папке список ACL по умолчанию для родительской папки определяет:</span><span class="sxs-lookup"><span data-stu-id="644f0-246">When a new file or folder is created under an existing folder, the Default ACL on the parent folder determines:</span></span>

- <span data-ttu-id="644f0-247">список ACL для доступа и список ACL по умолчанию для дочерней папки;</span><span class="sxs-lookup"><span data-stu-id="644f0-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="644f0-248">список ACL для доступа для дочернего файла (файлы не имеют списка ACL по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="644f0-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="the-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="644f0-249">Список ACL для доступа для дочернего файла или папки</span><span class="sxs-lookup"><span data-stu-id="644f0-249">The Access ACL of a child file or folder</span></span>

<span data-ttu-id="644f0-250">При создании дочернего файла или папки список ACL по умолчанию для родительской папки копируется в виде списка ACL для доступа для дочернего файла или папки.</span><span class="sxs-lookup"><span data-stu-id="644f0-250">When a child file or folder is created, the parent's Default ACL is copied as the Access ACL of the child file or folder.</span></span> <span data-ttu-id="644f0-251">Кроме того, если **другому** пользователю предоставлены разрешения RWX в списке ACL по умолчанию для родительской папки, он полностью удаляется из списка ACL для доступа для дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="644f0-251">Also, if **other** user has RWX permissions in the parent's default ACL, it is removed from the child item's Access ACL.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="644f0-253">В большинстве ситуаций предоставленной выше информации о том, как определяется список ACL для доступа для дочернего элемента, вполне достаточно.</span><span class="sxs-lookup"><span data-stu-id="644f0-253">In most scenarios, the previous information is all you need to know about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="644f0-254">Однако если вы знакомы с системами на базе POSIX и хотите узнать больше о том, как происходит эта трансформация, см. раздел [Роль umask в создании ACL для доступа к новым файлам и папкам](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="644f0-254">However, if you are familiar with POSIX systems and want to understand in-depth how this transformation is achieved, see the section [Umask’s role in creating the Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="644f0-255">ACL по умолчанию для дочерней папки</span><span class="sxs-lookup"><span data-stu-id="644f0-255">A child folder's Default ACL</span></span>

<span data-ttu-id="644f0-256">При создании дочерней папки в родительской папке список ACL по умолчанию для родительской папки копируется без изменений в список ACL по умолчанию для дочерней папки.</span><span class="sxs-lookup"><span data-stu-id="644f0-256">When a child folder is created under a parent folder, the parent folder's Default ACL is copied over as is to the child folder's Default ACL.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="644f0-258">Темы для углубленного изучения принципов работы со списками ACL в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="644f0-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="644f0-259">Ниже представлено несколько дополнительных разделов, в которых подробно описано, как определяются списки ACL для файлов или папок в хранилище Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-259">Following are some advanced topics to help you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-the-access-acl-for-new-files-and-folders"></a><span data-ttu-id="644f0-260">Роль umask в создании ACL для доступа для новых файлов и папок</span><span class="sxs-lookup"><span data-stu-id="644f0-260">Umask’s role in creating the Access ACL for new files and folders</span></span>

<span data-ttu-id="644f0-261">В POSIX-совместимой системе umask представляет собой 9-битное значение родительской папки, которое используется, чтобы преобразовать разрешения для **владельца**, **группы владельцев** и **остальных пользователей** в ACL для доступа для нового дочернего файла или папки.</span><span class="sxs-lookup"><span data-stu-id="644f0-261">In a POSIX-compliant system, the general concept is that umask is a 9-bit value on the parent folder that's used to transform the permission for **owning user**, **owning group**, and **other** on the Access ACL of a new child file or folder.</span></span> <span data-ttu-id="644f0-262">Биты umask определяют, какие биты ACL для доступа к дочернему элементу нужно отключить.</span><span class="sxs-lookup"><span data-stu-id="644f0-262">The bits of a umask identify which bits to turn off in the child item’s Access ACL.</span></span> <span data-ttu-id="644f0-263">Таким образом, эта маска используется, чтобы выборочно предотвращать распространение разрешений для **владельца**, **группы владельцев** или **остальных пользователей**.</span><span class="sxs-lookup"><span data-stu-id="644f0-263">Thus it is used to selectively prevent the propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="644f0-264">В системе HDFS umask, как правило, является параметром конфигурации уровня сайта, управляемым администраторами.</span><span class="sxs-lookup"><span data-stu-id="644f0-264">In an HDFS system, the umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="644f0-265">Data Lake Store использует маску **umask уровня учетной записи** , которую нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="644f0-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="644f0-266">В следующей таблице показана работа umask в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-266">The following table shows the unmask for Data Lake Store.</span></span>

| <span data-ttu-id="644f0-267">Группа пользователя</span><span class="sxs-lookup"><span data-stu-id="644f0-267">User group</span></span>  | <span data-ttu-id="644f0-268">Настройка</span><span class="sxs-lookup"><span data-stu-id="644f0-268">Setting</span></span> | <span data-ttu-id="644f0-269">Влияние на ACL для доступа для нового дочернего элемента</span><span class="sxs-lookup"><span data-stu-id="644f0-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="644f0-270">владельца</span><span class="sxs-lookup"><span data-stu-id="644f0-270">Owning user</span></span> | ---     | <span data-ttu-id="644f0-271">Не влияет</span><span class="sxs-lookup"><span data-stu-id="644f0-271">No effect</span></span>                             |
| <span data-ttu-id="644f0-272">группы владельцев</span><span class="sxs-lookup"><span data-stu-id="644f0-272">Owning group</span></span>| ---     | <span data-ttu-id="644f0-273">Не влияет</span><span class="sxs-lookup"><span data-stu-id="644f0-273">No effect</span></span>                             |
| <span data-ttu-id="644f0-274">другой</span><span class="sxs-lookup"><span data-stu-id="644f0-274">Other</span></span>       | <span data-ttu-id="644f0-275">RWX</span><span class="sxs-lookup"><span data-stu-id="644f0-275">RWX</span></span>     | <span data-ttu-id="644f0-276">Удаление разрешения на чтение, запись и выполнение</span><span class="sxs-lookup"><span data-stu-id="644f0-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="644f0-277">На следующем рисунке показано, как работает umask.</span><span class="sxs-lookup"><span data-stu-id="644f0-277">The following illustration shows this umask in action.</span></span> <span data-ttu-id="644f0-278">Конечным результатом является удаление разрешений на **чтение, запись и выполнение** для **остальных** пользователей.</span><span class="sxs-lookup"><span data-stu-id="644f0-278">The net effect is to remove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="644f0-279">Свойство umask не указывает биты для **владельца** и **группы владельцев**, поэтому эти разрешения не трансформируются.</span><span class="sxs-lookup"><span data-stu-id="644f0-279">Because the umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="the-sticky-bit"></a><span data-ttu-id="644f0-281">Бит фиксации</span><span class="sxs-lookup"><span data-stu-id="644f0-281">The sticky bit</span></span>

<span data-ttu-id="644f0-282">Бит фиксации является расширенной функцией файловой системы POSIX.</span><span class="sxs-lookup"><span data-stu-id="644f0-282">The sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="644f0-283">В контексте Data Lake Store потребность в использовании бита фиксации маловероятна.</span><span class="sxs-lookup"><span data-stu-id="644f0-283">In the context of Data Lake Store, it is unlikely that the sticky bit will be needed.</span></span>

<span data-ttu-id="644f0-284">В приведенной ниже таблице показано, как работает бит фиксации в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-284">The following table shows how the sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="644f0-285">Группа пользователя</span><span class="sxs-lookup"><span data-stu-id="644f0-285">User group</span></span>         | <span data-ttu-id="644f0-286">Файл</span><span class="sxs-lookup"><span data-stu-id="644f0-286">File</span></span>    | <span data-ttu-id="644f0-287">Папка</span><span class="sxs-lookup"><span data-stu-id="644f0-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="644f0-288">Бит фиксации **выключен**</span><span class="sxs-lookup"><span data-stu-id="644f0-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="644f0-289">Не влияет</span><span class="sxs-lookup"><span data-stu-id="644f0-289">No effect</span></span>   | <span data-ttu-id="644f0-290">Не влияет</span><span class="sxs-lookup"><span data-stu-id="644f0-290">No effect.</span></span>           |
| <span data-ttu-id="644f0-291">Бит фиксации **включен**</span><span class="sxs-lookup"><span data-stu-id="644f0-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="644f0-292">Не влияет</span><span class="sxs-lookup"><span data-stu-id="644f0-292">No effect</span></span>   | <span data-ttu-id="644f0-293">Предотвращает возможность удаления или переименования дочернего элемента кем-либо, кроме **суперпользователей** или **владельца** этого дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="644f0-293">Prevents anyone except **super-users** and the **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="644f0-294">Бит фиксации не отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="644f0-294">The sticky bit is not shown in the Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="644f0-295">Общие вопросы о списках ACL в хранилище Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="644f0-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="644f0-296">Ниже приведены ответы на часто задаваемые вопросы, возникающие при работе со списками ACL в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-to-enable-support-for-acls"></a><span data-ttu-id="644f0-297">Нужно ли мне активировать поддержку ACL?</span><span class="sxs-lookup"><span data-stu-id="644f0-297">Do I have to enable support for ACLs?</span></span>

<span data-ttu-id="644f0-298">Нет.</span><span class="sxs-lookup"><span data-stu-id="644f0-298">No.</span></span> <span data-ttu-id="644f0-299">Контроль доступа к учетной записи Data Lake Store с помощью ACL всегда включен.</span><span class="sxs-lookup"><span data-stu-id="644f0-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-to-recursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="644f0-300">Какие разрешения требуются для рекурсивного удаления папки и ее содержимого?</span><span class="sxs-lookup"><span data-stu-id="644f0-300">Which permissions are required to recursively delete a folder and its contents?</span></span>

* <span data-ttu-id="644f0-301">Для доступа к родительской папке требуются разрешения на **запись и выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-301">The parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="644f0-302">Чтобы удалить папку и все ее подпапки, требуются разрешения на **чтение, запись и выполнение**.</span><span class="sxs-lookup"><span data-stu-id="644f0-302">The folder to be deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="644f0-303">Для удаления файлов в папках не требуются разрешения на запись.</span><span class="sxs-lookup"><span data-stu-id="644f0-303">You do not need Write permissions to delete files in folders.</span></span> <span data-ttu-id="644f0-304">Обратите внимание, что корневую папку "/" удалить **невозможно**.</span><span class="sxs-lookup"><span data-stu-id="644f0-304">Also, the root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-the-owner-of-a-file-or-folder"></a><span data-ttu-id="644f0-305">Кто назначается владельцем файла или папки?</span><span class="sxs-lookup"><span data-stu-id="644f0-305">Who is the owner of a file or folder?</span></span>

<span data-ttu-id="644f0-306">Создатель файла или папки становится их владельцем.</span><span class="sxs-lookup"><span data-stu-id="644f0-306">The creator of a file or folder becomes the owner.</span></span>

### <a name="which-group-is-set-as-the-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="644f0-307">Как назначается группа владельцев файла или папки при их создании?</span><span class="sxs-lookup"><span data-stu-id="644f0-307">Which group is set as the owning group of a file or folder at creation?</span></span>

<span data-ttu-id="644f0-308">Группа владельцев копируется из родительской папки, в которой создан файл или папка.</span><span class="sxs-lookup"><span data-stu-id="644f0-308">The owning group is copied from the owning group of the parent folder under which the new file or folder is created.</span></span>

### <a name="i-am-the-owning-user-of-a-file-but-i-dont-have-the-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="644f0-309">Я являюсь владельцем файла, но у меня нет необходимых разрешений RWX.</span><span class="sxs-lookup"><span data-stu-id="644f0-309">I am the owning user of a file but I don’t have the RWX permissions I need.</span></span> <span data-ttu-id="644f0-310">Что делать?</span><span class="sxs-lookup"><span data-stu-id="644f0-310">What do I do?</span></span>

<span data-ttu-id="644f0-311">Владелец может изменить разрешения на доступ к файлу на любое из требуемых RWX-разрешений.</span><span class="sxs-lookup"><span data-stu-id="644f0-311">The owning user can change the permissions of the file to give themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-the-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="644f0-312">При просмотре списков ACL на портале Azure я вижу имена пользователей, а при просмотре в интерфейсе API — идентификаторы GUID. Почему так происходит?</span><span class="sxs-lookup"><span data-stu-id="644f0-312">When I look at ACLs in the Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="644f0-313">Записи в списках ACL хранятся в качестве идентификаторов GUID, соответствующих пользователям в AAD.</span><span class="sxs-lookup"><span data-stu-id="644f0-313">Entries in the ACLs are stored as GUIDs that correspond to users in Azure AD.</span></span> <span data-ttu-id="644f0-314">Интерфейсы API возвращают идентификаторы GUID без изменений.</span><span class="sxs-lookup"><span data-stu-id="644f0-314">The APIs return the GUIDs as is.</span></span> <span data-ttu-id="644f0-315">Портал Azure пытается упростить использование списков ACL, по возможности преобразовывая идентификаторы GUID в понятные имена.</span><span class="sxs-lookup"><span data-stu-id="644f0-315">The Azure portal tries to make ACLs easier to use by translating the GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-the-acls-when-im-using-the-azure-portal"></a><span data-ttu-id="644f0-316">Почему при просмотре на портале Azure для списков ACL иногда отображаются идентификаторы GUID?</span><span class="sxs-lookup"><span data-stu-id="644f0-316">Why do I sometimes see GUIDs in the ACLs when I'm using the Azure portal?</span></span>

<span data-ttu-id="644f0-317">GUID отображается, если пользователь не существует в AAD.</span><span class="sxs-lookup"><span data-stu-id="644f0-317">A GUID is shown when the user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="644f0-318">Как правило, это происходит, если пользователь уволился или его учетная запись удалена из AAD.</span><span class="sxs-lookup"><span data-stu-id="644f0-318">Usually this happens when the user has left the company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="644f0-319">Поддерживает ли Data Lake Store наследование списков ACL?</span><span class="sxs-lookup"><span data-stu-id="644f0-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="644f0-320">Нет.</span><span class="sxs-lookup"><span data-stu-id="644f0-320">No.</span></span>

### <a name="what-is-the-difference-between-mask-and-umask"></a><span data-ttu-id="644f0-321">В чем разница между маской и umask?</span><span class="sxs-lookup"><span data-stu-id="644f0-321">What is the difference between mask and umask?</span></span>

| <span data-ttu-id="644f0-322">маска</span><span class="sxs-lookup"><span data-stu-id="644f0-322">mask</span></span> | <span data-ttu-id="644f0-323">umask</span><span class="sxs-lookup"><span data-stu-id="644f0-323">umask</span></span>|
|------|------|
| <span data-ttu-id="644f0-324">Свойство **маски** доступно в любом файле или папке.</span><span class="sxs-lookup"><span data-stu-id="644f0-324">The **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="644f0-325">**Umask** является свойством учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="644f0-325">The **umask** is a property of the Data Lake Store account.</span></span> <span data-ttu-id="644f0-326">Таким образом, в Data Lake Store возможно только одно свойство umask.</span><span class="sxs-lookup"><span data-stu-id="644f0-326">So there is only a single umask in the Data Lake Store.</span></span>    |
| <span data-ttu-id="644f0-327">Свойство маски файла или папки может быть изменено владельцем или группой владельцев файла либо суперпользователем.</span><span class="sxs-lookup"><span data-stu-id="644f0-327">The mask property on a file or folder can be altered by the owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="644f0-328">Свойство umask не может изменить ни какой-либо пользователь, ни даже суперпользователь.</span><span class="sxs-lookup"><span data-stu-id="644f0-328">The umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="644f0-329">Это неизменяемая постоянная величина.</span><span class="sxs-lookup"><span data-stu-id="644f0-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="644f0-330">Свойство маски используется во время выполнения алгоритма проверки доступа, чтобы определить, имеет ли пользователь право выполнять операцию с файлом или папкой.</span><span class="sxs-lookup"><span data-stu-id="644f0-330">The mask property is used during the access check algorithm at runtime to determine whether a user has the right to perform on operation on a file or folder.</span></span> <span data-ttu-id="644f0-331">Роль маски заключается в создании "действующих разрешений" в ходе проверки доступа.</span><span class="sxs-lookup"><span data-stu-id="644f0-331">The role of the mask is to create "effective permissions" at the time of access check.</span></span> | <span data-ttu-id="644f0-332">Свойство umask не используется при проверке доступа.</span><span class="sxs-lookup"><span data-stu-id="644f0-332">The umask is not used during access check at all.</span></span> <span data-ttu-id="644f0-333">Umask используется для определения списков ACL для доступа для новых дочерних элементов папки.</span><span class="sxs-lookup"><span data-stu-id="644f0-333">The umask is used to determine the Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="644f0-334">Маска представляет собой 3-битное значение RWX, применимое к именованным пользователям, именованным группам и владельцам в процессе проверки доступа.</span><span class="sxs-lookup"><span data-stu-id="644f0-334">The mask is a 3-bit RWX value that applies to named user, named group, and owning user at the time of access check.</span></span>| <span data-ttu-id="644f0-335">Свойство umask — это 9-битное значение, применимое к владельцам, группам владельцев и **остальным пользователям** нового дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="644f0-335">The umask is a 9-bit value that applies to the owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="644f0-336">Где можно получить дополнительную информацию о модели контроля доступа POSIX?</span><span class="sxs-lookup"><span data-stu-id="644f0-336">Where can I learn more about POSIX access control model?</span></span>

* <span data-ttu-id="644f0-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html) (Списки управления доступом POSIX для Linux)</span><span class="sxs-lookup"><span data-stu-id="644f0-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)</span></span>

* <span data-ttu-id="644f0-338">[HDFS Permission Guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html) (Руководство по разрешениям в HDFS)</span><span class="sxs-lookup"><span data-stu-id="644f0-338">[HDFS permission guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)</span></span>

* [<span data-ttu-id="644f0-339">POSIX FAQ (POSIX: вопросы и ответы)</span><span class="sxs-lookup"><span data-stu-id="644f0-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="644f0-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="644f0-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="644f0-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="644f0-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="644f0-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="644f0-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* <span data-ttu-id="644f0-343">[POSIX ACL on Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs) (POSIX ACL для Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="644f0-343">[POSIX ACL on Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs)</span></span>

* <span data-ttu-id="644f0-344">[ACL: Using Access Control Lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/) (ACL: использование списков управления доступом в Linux)</span><span class="sxs-lookup"><span data-stu-id="644f0-344">[ACL using access control lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)</span></span>

## <a name="see-also"></a><span data-ttu-id="644f0-345">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="644f0-345">See also</span></span>

* [<span data-ttu-id="644f0-346">Обзор хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="644f0-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
