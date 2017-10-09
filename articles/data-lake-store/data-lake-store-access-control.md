---
title: "aaaOverview управления доступом в хранилище Озера данных | Документы Microsoft"
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
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="331a7-103">Контроль доступа в Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="331a7-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="331a7-104">Хранилище Озера данных Azure реализует модель управления доступом, производный от HDFS, который в свою очередь является производным от модели управления доступом hello POSIX.</span><span class="sxs-lookup"><span data-stu-id="331a7-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="331a7-105">В этой статье приведены основные принципы hello hello модель управления доступом для хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="331a7-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="331a7-106">toolearn Дополнительные сведения о модели управления доступом hello HDFS, в разделе [HDFS разрешения руководства](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="331a7-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="331a7-107">Списки управления доступом для файлов и папок</span><span class="sxs-lookup"><span data-stu-id="331a7-107">Access control lists on files and folders</span></span>

<span data-ttu-id="331a7-108">Существует два типа списков управления доступом (ACL): **ACL для доступа** и **ACL по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="331a7-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="331a7-109">**Доступ к ACL**: эти объект tooan доступа элемента управления.</span><span class="sxs-lookup"><span data-stu-id="331a7-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="331a7-110">Списки ACL для доступа позволяют управлять доступом как к файлам, так и к папкам.</span><span class="sxs-lookup"><span data-stu-id="331a7-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="331a7-111">**По умолчанию списки управления доступом**: «Шаблон» списков управления доступом связанный с папкой, которые определяют hello доступа ACL для дочерних элементов, которые создаются в этой папке.</span><span class="sxs-lookup"><span data-stu-id="331a7-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="331a7-112">Файлы не имеют ACL по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="331a7-112">Files do not have Default ACLs.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="331a7-114">Списки ACL для доступа и списки управления доступом по умолчанию имеют hello одинаковую структуру.</span><span class="sxs-lookup"><span data-stu-id="331a7-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="331a7-116">Изменение списка управления Доступом по умолчанию hello в родительском элементе не влияет на hello доступом ACL или по умолчанию ACL дочерних элементов, которые уже существуют.</span><span class="sxs-lookup"><span data-stu-id="331a7-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="331a7-117">Пользователи и удостоверения</span><span class="sxs-lookup"><span data-stu-id="331a7-117">Users and identities</span></span>

<span data-ttu-id="331a7-118">Каждый файл или папка имеет отдельные разрешения для следующих удостоверений:</span><span class="sxs-lookup"><span data-stu-id="331a7-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="331a7-119">Привет, которой принадлежит пользователь hello файла</span><span class="sxs-lookup"><span data-stu-id="331a7-119">hello owning user of hello file</span></span>
* <span data-ttu-id="331a7-120">Владелец группы Hello</span><span class="sxs-lookup"><span data-stu-id="331a7-120">hello owning group</span></span>
* <span data-ttu-id="331a7-121">именованные пользователи;</span><span class="sxs-lookup"><span data-stu-id="331a7-121">Named users</span></span>
* <span data-ttu-id="331a7-122">именованные группы;</span><span class="sxs-lookup"><span data-stu-id="331a7-122">Named groups</span></span>
* <span data-ttu-id="331a7-123">все остальные пользователи.</span><span class="sxs-lookup"><span data-stu-id="331a7-123">All other users</span></span>

<span data-ttu-id="331a7-124">удостоверения Azure Active Directory (Azure AD), Hello удостоверения пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="331a7-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="331a7-125">Если не указано иное, «пользователь,» в контексте hello хранилища Озера данных, можно либо означает, что пользователь Azure AD или группы безопасности Azure AD.</span><span class="sxs-lookup"><span data-stu-id="331a7-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="331a7-126">Разрешения</span><span class="sxs-lookup"><span data-stu-id="331a7-126">Permissions</span></span>

<span data-ttu-id="331a7-127">Hello разрешения на объект файловой системы, **чтения**, **записи**, и **Execute**, и их можно использовать для файлов и папок, как показано в следующей таблице hello:</span><span class="sxs-lookup"><span data-stu-id="331a7-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="331a7-128">Файл</span><span class="sxs-lookup"><span data-stu-id="331a7-128">File</span></span>     |   <span data-ttu-id="331a7-129">Папка</span><span class="sxs-lookup"><span data-stu-id="331a7-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="331a7-130">**Разрешение на чтение (R)**</span><span class="sxs-lookup"><span data-stu-id="331a7-130">**Read (R)**</span></span> | <span data-ttu-id="331a7-131">Можно считать содержимое файла hello</span><span class="sxs-lookup"><span data-stu-id="331a7-131">Can read hello contents of a file</span></span> | <span data-ttu-id="331a7-132">Требуется **чтения** и **Execute** toolist hello содержимое папки hello</span><span class="sxs-lookup"><span data-stu-id="331a7-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="331a7-133">**Разрешение на запись (W)**</span><span class="sxs-lookup"><span data-stu-id="331a7-133">**Write (W)**</span></span> | <span data-ttu-id="331a7-134">Можно создать или добавить файл tooa</span><span class="sxs-lookup"><span data-stu-id="331a7-134">Can write or append tooa file</span></span> | <span data-ttu-id="331a7-135">Требуется **записи** и **Execute** toocreate дочерних элементов в папке</span><span class="sxs-lookup"><span data-stu-id="331a7-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="331a7-136">**Разрешение на выполнение (X)**</span><span class="sxs-lookup"><span data-stu-id="331a7-136">**Execute (X)**</span></span> | <span data-ttu-id="331a7-137">Не означает, что-либо в контексте hello хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="331a7-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="331a7-138">Требуется tootraverse hello дочерних элементов папки</span><span class="sxs-lookup"><span data-stu-id="331a7-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="331a7-139">Сокращения для разрешений</span><span class="sxs-lookup"><span data-stu-id="331a7-139">Short forms for permissions</span></span>

<span data-ttu-id="331a7-140">**RWX** — используется tooindicate **чтение + запись и выполнение**.</span><span class="sxs-lookup"><span data-stu-id="331a7-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="331a7-141">В которой существует более краткие цифровая форма **чтения = 4**, **записи = 2**, и **Execute = 1**, сумма hello, из которых представляет hello разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="331a7-142">Ниже приводятся некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="331a7-142">Following are some examples.</span></span>

| <span data-ttu-id="331a7-143">Цифровая форма</span><span class="sxs-lookup"><span data-stu-id="331a7-143">Numeric form</span></span> | <span data-ttu-id="331a7-144">Краткая форма</span><span class="sxs-lookup"><span data-stu-id="331a7-144">Short form</span></span> |      <span data-ttu-id="331a7-145">Значение</span><span class="sxs-lookup"><span data-stu-id="331a7-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="331a7-146">7</span><span class="sxs-lookup"><span data-stu-id="331a7-146">7</span></span>            | <span data-ttu-id="331a7-147">RWX</span><span class="sxs-lookup"><span data-stu-id="331a7-147">RWX</span></span>        | <span data-ttu-id="331a7-148">чтение, запись и выполнение</span><span class="sxs-lookup"><span data-stu-id="331a7-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="331a7-149">5</span><span class="sxs-lookup"><span data-stu-id="331a7-149">5</span></span>            | <span data-ttu-id="331a7-150">R-X</span><span class="sxs-lookup"><span data-stu-id="331a7-150">R-X</span></span>        | <span data-ttu-id="331a7-151">Чтение + выполнение</span><span class="sxs-lookup"><span data-stu-id="331a7-151">Read + Execute</span></span>         |
| <span data-ttu-id="331a7-152">4</span><span class="sxs-lookup"><span data-stu-id="331a7-152">4</span></span>            | <span data-ttu-id="331a7-153">R--</span><span class="sxs-lookup"><span data-stu-id="331a7-153">R--</span></span>        | <span data-ttu-id="331a7-154">чтение</span><span class="sxs-lookup"><span data-stu-id="331a7-154">Read</span></span>                   |
| <span data-ttu-id="331a7-155">0</span><span class="sxs-lookup"><span data-stu-id="331a7-155">0</span></span>            | ---        | <span data-ttu-id="331a7-156">Нет разрешений</span><span class="sxs-lookup"><span data-stu-id="331a7-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="331a7-157">Разрешения не наследуются</span><span class="sxs-lookup"><span data-stu-id="331a7-157">Permissions do not inherit</span></span>

<span data-ttu-id="331a7-158">В модели POSIX стиле hello, которая используется хранилище Озера данных разрешения для элемента, хранятся на сам элемент hello.</span><span class="sxs-lookup"><span data-stu-id="331a7-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="331a7-159">Другими словами разрешения для элемента не может наследоваться от hello родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="331a7-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="331a7-160">Общие toopermissions связанные сценарии</span><span class="sxs-lookup"><span data-stu-id="331a7-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="331a7-161">Ниже приведены некоторые распространенные сценарии toohelp понять, какие разрешения, необходимые tooperform определенные операции в учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="331a7-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="331a7-162">Разрешения, необходимые tooread файла</span><span class="sxs-lookup"><span data-stu-id="331a7-162">Permissions needed tooread a file</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="331a7-164">Для toobe файл hello чтения, hello потребностей вызывающий объект **чтения** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="331a7-165">Для всех hello папок hello структуры папок, содержащих файл hello, hello потребностей вызывающий объект **Execute** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="331a7-166">Файл tooa tooappend необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="331a7-166">Permissions needed tooappend tooa file</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="331a7-168">Для добавляемый файл toobe hello hello потребностей вызывающий объект **записи** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="331a7-169">Для всех hello папок, содержащих файл hello, hello потребностей вызывающий объект **Execute** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="331a7-170">Разрешения, необходимые toodelete файла</span><span class="sxs-lookup"><span data-stu-id="331a7-170">Permissions needed toodelete a file</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="331a7-172">Hello родительской папке, hello потребностей вызывающий объект **записи + выполнение** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="331a7-173">Для всех hello другие папки в пути к файлу hello, hello потребностей вызывающий объект **Execute** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="331a7-174">Записи разрешений на файл hello не требуется toodelete его при условии, что hello предыдущие два условия верны.</span><span class="sxs-lookup"><span data-stu-id="331a7-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="331a7-175">Разрешения, необходимые tooenumerate папки</span><span class="sxs-lookup"><span data-stu-id="331a7-175">Permissions needed tooenumerate a folder</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="331a7-177">Для tooenumerate папки hello, hello потребностей вызывающий объект **чтения + Execute** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="331a7-178">Для всех hello папки предка, hello потребностей вызывающий объект **Execute** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="331a7-179">Просмотр разрешений в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="331a7-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="331a7-180">Из hello **обозреватель данных** колонке hello учетной записи хранилища Озера данных, нажмите кнопку **доступа** toosee hello списки управления доступом для файла или папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="331a7-181">Нажмите кнопку **доступа** toosee hello списки управления доступом для hello **каталога** папку hello **mydatastore** учетной записи.</span><span class="sxs-lookup"><span data-stu-id="331a7-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="331a7-183">В этой колонке hello верхнем разделе приведен обзор hello разрешений пользователя.</span><span class="sxs-lookup"><span data-stu-id="331a7-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="331a7-184">(На снимке экрана приветствия пользователя hello — Боб). После этого отображаются hello разрешения на доступ.</span><span class="sxs-lookup"><span data-stu-id="331a7-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="331a7-185">После этого hello **доступа** колонка, щелкните **простое представление** toosee Здравствуйте, чтобы упростить внешний вид.</span><span class="sxs-lookup"><span data-stu-id="331a7-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="331a7-187">Нажмите кнопку **расширенное представление** toosee hello более расширенное представление, где показаны основные понятия hello по умолчанию списки управления доступом, маска и суперпользователя.</span><span class="sxs-lookup"><span data-stu-id="331a7-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="331a7-189">Hello суперпользователя</span><span class="sxs-lookup"><span data-stu-id="331a7-189">hello super-user</span></span>

<span data-ttu-id="331a7-190">Супертипом пользователь имеет права на большинстве всех пользователей hello hello в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="331a7-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="331a7-191">Суперпользователь:</span><span class="sxs-lookup"><span data-stu-id="331a7-191">A super-user:</span></span>

* <span data-ttu-id="331a7-192">Имеет разрешения RWX слишком**все** файлы и папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="331a7-193">Можно изменить разрешения hello любой файл или папку.</span><span class="sxs-lookup"><span data-stu-id="331a7-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="331a7-194">Можно изменить hello, которой принадлежит пользователь или владелец группы любой файл или папку.</span><span class="sxs-lookup"><span data-stu-id="331a7-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="331a7-195">В учетной записи Azure Data Lake Store предусмотрено несколько ролей Azure, в том числе:</span><span class="sxs-lookup"><span data-stu-id="331a7-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="331a7-196">владельцы;</span><span class="sxs-lookup"><span data-stu-id="331a7-196">Owners</span></span>
* <span data-ttu-id="331a7-197">участники;</span><span class="sxs-lookup"><span data-stu-id="331a7-197">Contributors</span></span>
* <span data-ttu-id="331a7-198">читатели;</span><span class="sxs-lookup"><span data-stu-id="331a7-198">Readers</span></span>

<span data-ttu-id="331a7-199">Все сотрудники hello **владельцев** роли для учетной записи хранилища Озера данных которого автоматически суперпользователя для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="331a7-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="331a7-200">toolearn более, в разделе [управления доступом на основе ролей](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="331a7-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="331a7-201">Если требуется toocreate пользовательского элемента управления на основе доступа ролей (RBAC) роли, имеющей разрешения суперпользователя, он должен быть hello toohave следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="331a7-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="331a7-202">Microsoft.DataLakeStore/accounts/Superuser/action;</span><span class="sxs-lookup"><span data-stu-id="331a7-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="331a7-203">Microsoft.Authorization/roleAssignments/write.</span><span class="sxs-lookup"><span data-stu-id="331a7-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="331a7-204">Hello владеющего пользователя</span><span class="sxs-lookup"><span data-stu-id="331a7-204">hello owning user</span></span>

<span data-ttu-id="331a7-205">Hello пользователя, создавшего элемент hello автоматически — hello, которой принадлежит пользователь hello элемента.</span><span class="sxs-lookup"><span data-stu-id="331a7-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="331a7-206">Владелец может:</span><span class="sxs-lookup"><span data-stu-id="331a7-206">An owning user can:</span></span>

* <span data-ttu-id="331a7-207">Изменение разрешений hello, включенного файла.</span><span class="sxs-lookup"><span data-stu-id="331a7-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="331a7-208">Изменить владельца группы файла, который имеет владельца, при условии, что hello владеющего пользователя также является членом группы целевых hello hello.</span><span class="sxs-lookup"><span data-stu-id="331a7-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="331a7-209">Привет, которой принадлежит пользователь *нельзя* изменить hello, которой принадлежит пользователь другого владельца файла.</span><span class="sxs-lookup"><span data-stu-id="331a7-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="331a7-210">Только супертипом пользователи могут изменять hello, которой принадлежит пользователь, файла или папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="331a7-211">Владелец группы Hello</span><span class="sxs-lookup"><span data-stu-id="331a7-211">hello owning group</span></span>

<span data-ttu-id="331a7-212">Каждый пользователь hello ACL POSIX, не связан с «основная группа».</span><span class="sxs-lookup"><span data-stu-id="331a7-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="331a7-213">Например пользователь «alice» может быть участником группы «Финансы» toohello.</span><span class="sxs-lookup"><span data-stu-id="331a7-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="331a7-214">Алиса также может быть участником группы toomultiple, но одна группа всегда назначается свой основной группой.</span><span class="sxs-lookup"><span data-stu-id="331a7-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="331a7-215">В POSIX Если Алиса создает файл, hello, которой принадлежит группе этого файла задается tooher основную группу, что в данном случае является «finance».</span><span class="sxs-lookup"><span data-stu-id="331a7-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="331a7-216">При создании нового элемента filesystem хранилища Озера данных присваивает значение toohello, которой принадлежит группе.</span><span class="sxs-lookup"><span data-stu-id="331a7-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="331a7-217">**Вариант 1**: hello корневую папку «/».</span><span class="sxs-lookup"><span data-stu-id="331a7-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="331a7-218">Эта папка создается при создании учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="331a7-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="331a7-219">В этом случае владелец группы hello задается toohello пользователя, создавшего hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="331a7-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="331a7-220">**Вариант 2** (всех остальных случаях): при создании нового элемента, владеющего группа hello копируется из hello родительской папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="331a7-221">можно изменить владельца группы Hello с:</span><span class="sxs-lookup"><span data-stu-id="331a7-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="331a7-222">одним из суперпользователей;</span><span class="sxs-lookup"><span data-stu-id="331a7-222">Any super-users.</span></span>
* <span data-ttu-id="331a7-223">Здравствуйте, которой принадлежит пользователь, если hello владеющего пользователя также является членом группы целевых hello.</span><span class="sxs-lookup"><span data-stu-id="331a7-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="331a7-224">Алгоритм проверки доступа</span><span class="sxs-lookup"><span data-stu-id="331a7-224">Access check algorithm</span></span>

<span data-ttu-id="331a7-225">Привет, Следующая иллюстрация представляет hello алгоритм проверки доступа для учетных записей хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="331a7-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Алгоритм работы списков управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="331a7-227">Маска Hello и «действующие разрешения»</span><span class="sxs-lookup"><span data-stu-id="331a7-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="331a7-228">Hello **маска** является RWX значения, используемые toolimit доступ для **пользователей с именем**, hello **владелец группы**, и **с именем группы** после выполнение hello алгоритм проверки доступа.</span><span class="sxs-lookup"><span data-stu-id="331a7-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="331a7-229">Ниже приведены основные понятия hello для hello маски.</span><span class="sxs-lookup"><span data-stu-id="331a7-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="331a7-230">Маска Hello создает «действующие разрешения».</span><span class="sxs-lookup"><span data-stu-id="331a7-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="331a7-231">То есть он изменяет разрешения hello во время проверки доступа hello.</span><span class="sxs-lookup"><span data-stu-id="331a7-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="331a7-232">Маска Hello могут непосредственно изменять владельца файла hello и супер пользователей.</span><span class="sxs-lookup"><span data-stu-id="331a7-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="331a7-233">Маска Hello можно удалить разрешения toocreate hello действующее разрешение.</span><span class="sxs-lookup"><span data-stu-id="331a7-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="331a7-234">Маска Hello *нельзя* добавить разрешения toohello действующее разрешение.</span><span class="sxs-lookup"><span data-stu-id="331a7-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="331a7-235">Рассмотрим несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="331a7-235">Let's look at some examples.</span></span> <span data-ttu-id="331a7-236">В следующем примере hello, маска hello задано слишком**RWX**, что означает, что маска hello не удаляет какие-либо разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="331a7-237">действующие разрешения с именем пользователя, владеющего группы и группы с именем hello Hello не изменяются во время проверки доступа hello.</span><span class="sxs-lookup"><span data-stu-id="331a7-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="331a7-239">В следующем примере hello, маска hello задано слишком**R-X**.</span><span class="sxs-lookup"><span data-stu-id="331a7-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="331a7-240">Это означает, что он **отключает разрешения на запись hello** для **с именем пользователя**, **владелец группы**, и **группы с именем** во время hello доступа Проверка.</span><span class="sxs-lookup"><span data-stu-id="331a7-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="331a7-242">Для ссылки Вот расположения hello маску для файла или папки в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="331a7-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="331a7-244">Для получения новой учетной записи хранилища Озера данных, hello маску для hello Доступом и ACL по умолчанию hello корневого папка («/») по умолчанию tooRWX.</span><span class="sxs-lookup"><span data-stu-id="331a7-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="331a7-245">Разрешения для новых файлов и папок</span><span class="sxs-lookup"><span data-stu-id="331a7-245">Permissions on new files and folders</span></span>

<span data-ttu-id="331a7-246">При создании нового файла или папки внутри существующей папки определяет hello по умолчанию ACL для hello родительской папки:</span><span class="sxs-lookup"><span data-stu-id="331a7-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="331a7-247">список ACL для доступа и список ACL по умолчанию для дочерней папки;</span><span class="sxs-lookup"><span data-stu-id="331a7-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="331a7-248">список ACL для доступа для дочернего файла (файлы не имеют списка ACL по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="331a7-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="331a7-249">Hello Доступом дочернего файла или папки</span><span class="sxs-lookup"><span data-stu-id="331a7-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="331a7-250">При создании дочернего файла или папки, список управления Доступом по умолчанию hello родительского копируются как hello Доступом hello дочернего файла или папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="331a7-251">Кроме того Если **других** пользователь имеет разрешения RWX по умолчанию hello родительского списка управления Доступом, он удаляется из списка ACL для доступа к hello дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="331a7-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="331a7-253">В большинстве случаев данные, полученные ранее hello —, все необходимые tooknow о том, как определяется Доступом дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="331a7-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="331a7-254">Тем не менее, если вы знакомы с POSIX системами и хотите toounderstand подробные как достигается это преобразование, в разделе hello [Umask его роль в создании hello доступом ACL для новых файлов и папок](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="331a7-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="331a7-255">ACL по умолчанию для дочерней папки</span><span class="sxs-lookup"><span data-stu-id="331a7-255">A child folder's Default ACL</span></span>

<span data-ttu-id="331a7-256">При создании дочерней папкой в родительской папке hello родительской папки по умолчанию ACL копируется через как toohello дочернюю папку по умолчанию ACL.</span><span class="sxs-lookup"><span data-stu-id="331a7-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="331a7-258">Темы для углубленного изучения принципов работы со списками ACL в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="331a7-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="331a7-259">Ниже приведены некоторые дополнительные разделы toohelp, вы понимаете, как определяется ACL для хранилища Озера данных файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="331a7-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="331a7-260">Umask его роль в создании hello доступом ACL для новых файлов и папок</span><span class="sxs-lookup"><span data-stu-id="331a7-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="331a7-261">В POSIX-совместимая система, общий принцип hello является, umask 9-разрядное значение при hello родительской папки, применяющее разрешение hello tootransform **ответственный пользователь**, **владелец группы**, и  **другие** на hello Доступом нового дочернего файла или папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="331a7-262">биты Hello umask идентификации какие биты tooturn off в Доступом hello дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="331a7-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="331a7-263">Таким образом используется hello перенос разрешений для предотвращения tooselectively **ответственный пользователь**, **владелец группы**, и **других**.</span><span class="sxs-lookup"><span data-stu-id="331a7-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="331a7-264">В системе HDFS hello umask обычно является параметр конфигурации на всем сайте, который управляется администраторами.</span><span class="sxs-lookup"><span data-stu-id="331a7-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="331a7-265">Data Lake Store использует маску **umask уровня учетной записи** , которую нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="331a7-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="331a7-266">Следующая таблица показывает hello Hello снимите маску для хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="331a7-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="331a7-267">Группа пользователя</span><span class="sxs-lookup"><span data-stu-id="331a7-267">User group</span></span>  | <span data-ttu-id="331a7-268">Настройка</span><span class="sxs-lookup"><span data-stu-id="331a7-268">Setting</span></span> | <span data-ttu-id="331a7-269">Влияние на ACL для доступа для нового дочернего элемента</span><span class="sxs-lookup"><span data-stu-id="331a7-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="331a7-270">владельца</span><span class="sxs-lookup"><span data-stu-id="331a7-270">Owning user</span></span> | ---     | <span data-ttu-id="331a7-271">Не влияет</span><span class="sxs-lookup"><span data-stu-id="331a7-271">No effect</span></span>                             |
| <span data-ttu-id="331a7-272">группы владельцев</span><span class="sxs-lookup"><span data-stu-id="331a7-272">Owning group</span></span>| ---     | <span data-ttu-id="331a7-273">Не влияет</span><span class="sxs-lookup"><span data-stu-id="331a7-273">No effect</span></span>                             |
| <span data-ttu-id="331a7-274">другой</span><span class="sxs-lookup"><span data-stu-id="331a7-274">Other</span></span>       | <span data-ttu-id="331a7-275">RWX</span><span class="sxs-lookup"><span data-stu-id="331a7-275">RWX</span></span>     | <span data-ttu-id="331a7-276">Удаление разрешения на чтение, запись и выполнение</span><span class="sxs-lookup"><span data-stu-id="331a7-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="331a7-277">Hello следующие иллюстрации показан этот umask в действии.</span><span class="sxs-lookup"><span data-stu-id="331a7-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="331a7-278">конечным итогом Hello является tooremove **чтение + запись и выполнение** для **других** пользователя.</span><span class="sxs-lookup"><span data-stu-id="331a7-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="331a7-279">Поскольку hello umask не указала бит для **ответственный пользователь** и **владелец группы**, эти разрешения не преобразуются.</span><span class="sxs-lookup"><span data-stu-id="331a7-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Списки управления доступом в Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="331a7-281">закрепленные бит Hello</span><span class="sxs-lookup"><span data-stu-id="331a7-281">hello sticky bit</span></span>

<span data-ttu-id="331a7-282">закрепленные бит Hello является еще одна возможность POSIX filesystem.</span><span class="sxs-lookup"><span data-stu-id="331a7-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="331a7-283">В контексте hello хранилища Озера данных скорее всего, потребуется обновить закрепленные разряда hello.</span><span class="sxs-lookup"><span data-stu-id="331a7-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="331a7-284">Hello следующей таблице показано, как прикрепленные бит hello работает в хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="331a7-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="331a7-285">Группа пользователя</span><span class="sxs-lookup"><span data-stu-id="331a7-285">User group</span></span>         | <span data-ttu-id="331a7-286">Файл</span><span class="sxs-lookup"><span data-stu-id="331a7-286">File</span></span>    | <span data-ttu-id="331a7-287">Папка</span><span class="sxs-lookup"><span data-stu-id="331a7-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="331a7-288">Бит фиксации **выключен**</span><span class="sxs-lookup"><span data-stu-id="331a7-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="331a7-289">Не влияет</span><span class="sxs-lookup"><span data-stu-id="331a7-289">No effect</span></span>   | <span data-ttu-id="331a7-290">Не влияет</span><span class="sxs-lookup"><span data-stu-id="331a7-290">No effect.</span></span>           |
| <span data-ttu-id="331a7-291">Бит фиксации **включен**</span><span class="sxs-lookup"><span data-stu-id="331a7-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="331a7-292">Не влияет</span><span class="sxs-lookup"><span data-stu-id="331a7-292">No effect</span></span>   | <span data-ttu-id="331a7-293">Не позволяет другим пользователям, за исключением **супер пользователей** и hello **ответственный пользователь** дочернего элемента, удаление или переименование этого дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="331a7-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="331a7-294">закрепленные бит Hello в hello портал Azure не отображается.</span><span class="sxs-lookup"><span data-stu-id="331a7-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="331a7-295">Общие вопросы о списках ACL в хранилище Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="331a7-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="331a7-296">Ниже приведены ответы на часто задаваемые вопросы, возникающие при работе со списками ACL в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="331a7-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="331a7-297">У tooenable поддержка списки управления доступом?</span><span class="sxs-lookup"><span data-stu-id="331a7-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="331a7-298">Нет.</span><span class="sxs-lookup"><span data-stu-id="331a7-298">No.</span></span> <span data-ttu-id="331a7-299">Контроль доступа к учетной записи Data Lake Store с помощью ACL всегда включен.</span><span class="sxs-lookup"><span data-stu-id="331a7-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="331a7-300">Разрешения, необходимые toorecursively удалить папку и ее содержимое?</span><span class="sxs-lookup"><span data-stu-id="331a7-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="331a7-301">должен иметь родительскую папку Hello **записи + выполнение** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="331a7-302">Здравствуйте toobe папка удалена, и каждую папку внутри нее, требует **чтение + запись и выполнение** разрешения.</span><span class="sxs-lookup"><span data-stu-id="331a7-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="331a7-303">Не требуется разрешение на запись toodelete файлы в папках.</span><span class="sxs-lookup"><span data-stu-id="331a7-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="331a7-304">Кроме того, hello корневую папку «/» можно **никогда не** удалены.</span><span class="sxs-lookup"><span data-stu-id="331a7-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="331a7-305">Кто является hello владельца файла или папки?</span><span class="sxs-lookup"><span data-stu-id="331a7-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="331a7-306">hello владельцем становится Hello создателя файла или папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="331a7-307">Группу, которой назначается hello владельца файла или папки при создании группы?</span><span class="sxs-lookup"><span data-stu-id="331a7-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="331a7-308">Владелец группы Hello копируется из hello, которой принадлежит группе hello родительской папке, в рамках которой hello создается новый файл или папку.</span><span class="sxs-lookup"><span data-stu-id="331a7-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="331a7-309">Я хочу hello, которой принадлежит пользователь файла при отсутствии hello RWX разрешения, которые требуются.</span><span class="sxs-lookup"><span data-stu-id="331a7-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="331a7-310">Что делать?</span><span class="sxs-lookup"><span data-stu-id="331a7-310">What do I do?</span></span>

<span data-ttu-id="331a7-311">Hello владельца пользователь может изменить разрешения hello toogive файл hello сами любые RWX разрешения, необходимые им.</span><span class="sxs-lookup"><span data-stu-id="331a7-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="331a7-312">При просмотре списки управления доступом в hello портале Azure отображаются имена пользователей, но через API-интерфейсы, отображаются идентификаторы GUID, чем это?</span><span class="sxs-lookup"><span data-stu-id="331a7-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="331a7-313">Записи в ACL hello хранятся как идентификаторы GUID, которые соответствуют toousers в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="331a7-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="331a7-314">Hello API-интерфейсы возвращают идентификаторы GUID hello как есть.</span><span class="sxs-lookup"><span data-stu-id="331a7-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="331a7-315">Hello портал Azure пытается проще toouse toomake списки управления доступом, перевод hello идентификаторы GUID в понятные имена, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="331a7-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="331a7-316">Иногда осталась GUID в ACL hello при использовании hello портал Azure?</span><span class="sxs-lookup"><span data-stu-id="331a7-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="331a7-317">Идентификатор GUID отображается в том случае, когда пользователь hello не существует в Azure AD больше.</span><span class="sxs-lookup"><span data-stu-id="331a7-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="331a7-318">Обычно это происходит, когда hello пользователь покидает компанию hello или если их учетная запись была удалена в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="331a7-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="331a7-319">Поддерживает ли Data Lake Store наследование списков ACL?</span><span class="sxs-lookup"><span data-stu-id="331a7-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="331a7-320">Нет.</span><span class="sxs-lookup"><span data-stu-id="331a7-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="331a7-321">Что такое hello разницу между маски и umask?</span><span class="sxs-lookup"><span data-stu-id="331a7-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="331a7-322">маска</span><span class="sxs-lookup"><span data-stu-id="331a7-322">mask</span></span> | <span data-ttu-id="331a7-323">umask</span><span class="sxs-lookup"><span data-stu-id="331a7-323">umask</span></span>|
|------|------|
| <span data-ttu-id="331a7-324">Hello **маска** свойство доступно для каждого файла и папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="331a7-325">Hello **umask** является свойством hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="331a7-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="331a7-326">Поэтому имеется только один umask в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="331a7-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="331a7-327">свойство маски Hello для файла или папки может быть изменено, hello, которой принадлежит пользователь или владелец группы файла или суперпользователя.</span><span class="sxs-lookup"><span data-stu-id="331a7-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="331a7-328">Нельзя изменить свойство umask Hello любым пользователем, даже суперпользователя.</span><span class="sxs-lookup"><span data-stu-id="331a7-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="331a7-329">Это неизменяемая постоянная величина.</span><span class="sxs-lookup"><span data-stu-id="331a7-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="331a7-330">свойство маски Hello используется во время hello алгоритм проверки доступа во время выполнения toodetermine, имеет ли пользователь hello правой tooperform операции для файла или папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="331a7-331">роль Hello маски hello — toocreate «действующие разрешения» во время проверки доступа hello.</span><span class="sxs-lookup"><span data-stu-id="331a7-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="331a7-332">во всех Hello umask не используется во время проверки доступа.</span><span class="sxs-lookup"><span data-stu-id="331a7-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="331a7-333">Hello umask — используется toodetermine hello Доступом новых дочерних элементов папки.</span><span class="sxs-lookup"><span data-stu-id="331a7-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="331a7-334">Маска Hello является 3-битовое значение RWX, применяет toonamed пользователь, группа с именем и владеющего пользователя во время проверки доступа hello.</span><span class="sxs-lookup"><span data-stu-id="331a7-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="331a7-335">Hello umask представляет собой 9-разрядное значение, применяющий toohello, которой принадлежит пользователь, группа, которой принадлежит и **других** нового дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="331a7-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="331a7-336">Где можно получить дополнительную информацию о модели контроля доступа POSIX?</span><span class="sxs-lookup"><span data-stu-id="331a7-336">Where can I learn more about POSIX access control model?</span></span>

* <span data-ttu-id="331a7-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html) (Списки управления доступом POSIX для Linux)</span><span class="sxs-lookup"><span data-stu-id="331a7-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)</span></span>

* <span data-ttu-id="331a7-338">[HDFS Permission Guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html) (Руководство по разрешениям в HDFS)</span><span class="sxs-lookup"><span data-stu-id="331a7-338">[HDFS permission guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)</span></span>

* [<span data-ttu-id="331a7-339">POSIX FAQ (POSIX: вопросы и ответы)</span><span class="sxs-lookup"><span data-stu-id="331a7-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="331a7-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="331a7-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="331a7-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="331a7-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="331a7-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="331a7-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* <span data-ttu-id="331a7-343">[POSIX ACL on Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs) (POSIX ACL для Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="331a7-343">[POSIX ACL on Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs)</span></span>

* <span data-ttu-id="331a7-344">[ACL: Using Access Control Lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/) (ACL: использование списков управления доступом в Linux)</span><span class="sxs-lookup"><span data-stu-id="331a7-344">[ACL using access control lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)</span></span>

## <a name="see-also"></a><span data-ttu-id="331a7-345">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="331a7-345">See also</span></span>

* [<span data-ttu-id="331a7-346">Обзор хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="331a7-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
