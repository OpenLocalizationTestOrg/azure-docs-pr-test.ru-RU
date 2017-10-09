---
title: "aaaHow toosecure доступа tooAzure данных каталога | Документы Microsoft"
description: "В этой статье объясняется, как toosecure данных каталога и его ресурсы данных."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="39971-103">Как toosecure доступ к ресурсам каталога toodata</span><span class="sxs-lookup"><span data-stu-id="39971-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="39971-104">Эта функция доступна только в выпуске standard hello каталога данных Azure.</span><span class="sxs-lookup"><span data-stu-id="39971-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="39971-105">Каталог данных Azure позволяет toospecify, кто имеет доступ к каталогу данных hello и что операций (регистрировать, аннотировать, стать владельцем) они могут выполнять на метаданные в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="39971-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="39971-106">Пользователи каталога и разрешения</span><span class="sxs-lookup"><span data-stu-id="39971-106">Catalog users and permissions</span></span>
<span data-ttu-id="39971-107">toogive пользователем или hello группы доступа к каталогу данных tooa и задайте разрешения:</span><span class="sxs-lookup"><span data-stu-id="39971-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="39971-108">На hello [Домашняя страница данных каталога](http://www.azuredatacatalog.com), нажмите кнопку **параметры** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="39971-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![Каталог данных: параметры](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="39971-110">На странице "Параметры" hello раскройте hello **пользователей каталога** раздела.</span><span class="sxs-lookup"><span data-stu-id="39971-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="39971-111">![Пользователи каталога - Добавление](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="39971-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="39971-112">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="39971-112">Click **Add**.</span></span>
4. <span data-ttu-id="39971-113">Введите полное hello **имя пользователя** или имя hello **группы безопасности** в Azure Active Directory (AAD) связанные с каталогом hello hello.</span><span class="sxs-lookup"><span data-stu-id="39971-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="39971-114">Используйте запятую (",") в качестве разделителя при добавлении нескольких пользователей или групп.</span><span class="sxs-lookup"><span data-stu-id="39971-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="39971-115">![Пользователи каталога: пользователи или группы](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="39971-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="39971-116">Нажмите клавишу **ввод** или **ВКЛАДКЕ** за пределы hello текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="39971-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="39971-117">Убедитесь, что все разрешения (**заметки**, **зарегистрировать**, и **Take Ownership**) назначаются toothese пользователям или группам по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="39971-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="39971-118">То есть можно hello пользователю или группе [зарегистрировать ресурсов данных]( data-catalog-how-to-register.md), [заметки ресурсов данных]( data-catalog-how-to-annotate.md), и [распоряжаться ресурсами данных]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="39971-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="39971-119">![Пользователи каталога: разрешения по умолчанию](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="39971-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="39971-120">toogive пользователя или группы, только на hello чтение каталога toohello доступ, снимите hello **заметки** параметр для этого пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="39971-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="39971-121">При этом hello пользователь или группа не может пометить ресурсов данных в каталоге hello, но они могут просматривать их.</span><span class="sxs-lookup"><span data-stu-id="39971-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="39971-122">toodeny пользователя или группы из регистрация данных ресурсов, снимите hello **зарегистрировать** параметр для этого пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="39971-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="39971-123">toodeny пользователю изменять владельца ресурса данных, снимите флажок hello **распоряжаться** параметр для этого пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="39971-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="39971-124">Щелкните пользователя или группу из каталога пользователей, toodelete **x** для пользователя или группы hello hello нижней части списка hello.</span><span class="sxs-lookup"><span data-stu-id="39971-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="39971-125">![Каталог пользователей: удаление пользователя](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="39971-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="39971-126">Рекомендуется добавить пользователей toocatalog группы безопасности вместо добавления пользователей непосредственно и назначить разрешения.</span><span class="sxs-lookup"><span data-stu-id="39971-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="39971-127">Затем добавьте группы безопасности toohello пользователей, которые соответствуют их ролей и их каталогов toohello необходимый уровень доступа.</span><span class="sxs-lookup"><span data-stu-id="39971-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="39971-128">Специальные рекомендации</span><span class="sxs-lookup"><span data-stu-id="39971-128">Special considerations</span></span>

- <span data-ttu-id="39971-129">Hello разрешения назначены toosecurity группы являются аддитивными.</span><span class="sxs-lookup"><span data-stu-id="39971-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="39971-130">Предположим, что пользователь входит в две группы.</span><span class="sxs-lookup"><span data-stu-id="39971-130">Say, a user is in two groups.</span></span> <span data-ttu-id="39971-131">Одна группа имеет разрешение на добавление заметок, а другая группа — нет.</span><span class="sxs-lookup"><span data-stu-id="39971-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="39971-132">Тогда у пользователя будет разрешение на добавление заметок.</span><span class="sxs-lookup"><span data-stu-id="39971-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="39971-133">Hello разрешения явно tooa пользователя переопределение hello разрешения, назначенные toogroups toowhich hello пользователь принадлежит.</span><span class="sxs-lookup"><span data-stu-id="39971-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="39971-134">В предыдущем примере hello, скажем, явно добавленные пользователи toocatalog пользователя hello и не предоставляйте разрешения заметки.</span><span class="sxs-lookup"><span data-stu-id="39971-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="39971-135">Несмотря на то, что пользователь hello является членом группы, которая имеет аннотировать разрешения пользователя Hello невозможно добавить заметки к ресурсов данных.</span><span class="sxs-lookup"><span data-stu-id="39971-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39971-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="39971-136">Next steps</span></span>
- [<span data-ttu-id="39971-137">Начало работы с каталогом данных Azure</span><span class="sxs-lookup"><span data-stu-id="39971-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

