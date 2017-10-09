---
title: "aaaManage учетную запись Azure Cosmos DB через hello портал Azure | Документы Microsoft"
description: "Узнайте, как toomanage базы данных Azure Cosmos учетной записи через портал Azure hello. Найти руководство по использованию tooview hello портал Azure, копирования, удаления и доступа учетных записей."
keywords: "Портал Azure, DocumentDB, Azure, Microsoft Azure"
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="414f6-105">Как toomanage учетную запись Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="414f6-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="414f6-106">Узнайте, как работать с ключами tooset глобальной согласованности и удалить учетную запись Azure Cosmos DB в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="414f6-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="414f6-107"><a id="consistency"></a>Управление параметрами согласованности Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="414f6-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="414f6-108">При выборе уровня согласованности правой hello зависит от hello семантику приложения.</span><span class="sxs-lookup"><span data-stu-id="414f6-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="414f6-109">Следует ознакомиться с уровнями hello доступных согласованности в базе данных Azure Cosmos, считывая [согласованности с помощью уровней toomaximize доступности и производительности в базе данных Azure Cosmos][consistency].</span><span class="sxs-lookup"><span data-stu-id="414f6-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="414f6-110">Azure Cosmos DB предоставляет гарантии согласованности, доступности и производительности для любого уровня согласованности, доступного учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="414f6-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="414f6-111">Настройка учетной записи базы данных с уровнем достоверности строгих требует данных пропущенные tooa один регион Azure, но не глобально доступны.</span><span class="sxs-lookup"><span data-stu-id="414f6-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="414f6-112">На Здравствуйте другой стороны, hello уровни согласованности ослабленной - ограниченным устареванием, session или окончательной enable вы tooassociate любое количество областей Azure с вашей учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="414f6-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="414f6-113">Привет, выполнив простые действия показывают, как tooselect hello уровень согласованности по умолчанию для учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="414f6-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="414f6-114">согласованность по умолчанию hello toospecify для учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="414f6-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="414f6-115">В hello [портал Azure](https://portal.azure.com/), доступ к учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="414f6-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="414f6-116">В колонке hello учетной записи, нажмите кнопку **по умолчанию согласованности**.</span><span class="sxs-lookup"><span data-stu-id="414f6-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="414f6-117">В hello **согласованности по умолчанию** колонки, новый уровень согласованности выберите hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="414f6-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="414f6-118">![Сеанс согласованности по умолчанию][5]</span><span class="sxs-lookup"><span data-stu-id="414f6-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="414f6-119"><a id="keys"></a>Просмотр, копирование и повторное создание ключей доступа</span><span class="sxs-lookup"><span data-stu-id="414f6-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="414f6-120">При создании учетной записи Azure Cosmos DB hello service создает два ключа master доступа, которые могут использоваться для проверки подлинности при доступе к учетной записи Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="414f6-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="414f6-121">Предоставляя два ключа доступа, Azure Cosmos DB включает ключи hello tooregenerate с без прерывания tooyour учетная запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="414f6-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="414f6-122">В hello [портал Azure](https://portal.azure.com/), hello доступа **ключей** колонки ресурсов меню hello hello **учетная запись Azure Cosmos DB** tooview колонки, копирования и повторное создание hello ключей доступа — Это используемые tooaccess учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="414f6-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Снимок экрана портала Azure, колонка «Ключи»](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="414f6-124">Hello **ключей** колонке также включает первичный и строки соединения получателей, которые можно использовать tooconnect tooyour учетной записи из hello [средство переноса данных](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="414f6-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="414f6-125">В этой колонке также доступны ключи только для чтения.</span><span class="sxs-lookup"><span data-stu-id="414f6-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="414f6-126">Чтение и запросы являются операциями только для чтения, а создание, удаление и замена — нет.</span><span class="sxs-lookup"><span data-stu-id="414f6-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="414f6-127">Скопируйте ключ доступа в hello портала Azure</span><span class="sxs-lookup"><span data-stu-id="414f6-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="414f6-128">На hello **ключей** колонка, щелкните hello **копирования** toohello кнопку справа от ключа hello нужно toocopy.</span><span class="sxs-lookup"><span data-stu-id="414f6-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![Просмотр и копирование клавиши доступа в hello портал Azure, ключи колонку](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="414f6-130">Повторное создание ключей доступа</span><span class="sxs-lookup"><span data-stu-id="414f6-130">Regenerate access keys</span></span>
<span data-ttu-id="414f6-131">Следует изменить учетную запись Azure Cosmos DB tooyour ключи доступа hello периодически toohelp безопасность подключений.</span><span class="sxs-lookup"><span data-stu-id="414f6-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="414f6-132">Два ключа доступа, назначенные tooenable вы toomaintain подключений toohello с помощью одного ключа доступа при повторном создании учетной записи Azure Cosmos DB hello другого ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="414f6-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="414f6-133">Повторное создание ключей доступа влияет на все приложения, которые зависят от текущего ключа hello.</span><span class="sxs-lookup"><span data-stu-id="414f6-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="414f6-134">Все клиенты, использующие учетную запись Azure Cosmos DB hello hello доступа tooaccess ключа должен быть обновленные toouse hello новый ключ.</span><span class="sxs-lookup"><span data-stu-id="414f6-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="414f6-135">При наличии приложения или облачные службы с использованием учетной записи Azure Cosmos DB hello, будут потеряны hello подключений при повторном создании ключей, если откат ключей.</span><span class="sxs-lookup"><span data-stu-id="414f6-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="414f6-136">Hello ниже описывается процесс hello, участвующих в развертывании вашего ключей.</span><span class="sxs-lookup"><span data-stu-id="414f6-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="414f6-137">Обновите ключ доступа hello в вашего приложения код tooreference hello вторичный ключ доступа для учетной записи Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="414f6-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="414f6-138">Повторное создание hello первичный ключ доступа для учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="414f6-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="414f6-139">В hello [портала Azure](https://portal.azure.com/), доступ к учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="414f6-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="414f6-140">В hello **учетную запись Azure Cosmos DB** колонка, щелкните **ключей**.</span><span class="sxs-lookup"><span data-stu-id="414f6-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="414f6-141">На hello **ключей** колонке нажмите кнопку повторное создание hello, а затем нажмите кнопку **ОК** tooconfirm, что требуется toogenerate новый ключ.</span><span class="sxs-lookup"><span data-stu-id="414f6-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="414f6-142">![Повторное создание ключей доступа](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="414f6-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="414f6-143">После проверки того, что новый ключ, hello доступна для использования (около 5 минут после нее), обновить ключ доступа hello в приложение код tooreference hello новый первичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="414f6-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="414f6-144">Повторное создание hello вторичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="414f6-144">Regenerate hello secondary access key.</span></span>
   
    ![Повторное создание ключей доступа](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="414f6-146">Он может занять несколько минут перед tooaccess используется вновь созданный ключ учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="414f6-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="414f6-147">Получить строку подключения hello</span><span class="sxs-lookup"><span data-stu-id="414f6-147">Get hello  connection string</span></span>
<span data-ttu-id="414f6-148">tooretrieve подключение строка, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="414f6-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="414f6-149">В hello [портал Azure](https://portal.azure.com), доступ к учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="414f6-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="414f6-150">В меню ресурса hello, щелкните **ключей**.</span><span class="sxs-lookup"><span data-stu-id="414f6-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="414f6-151">Щелкните hello **копирования** кнопку Далее toohello **основной строка подключения** или **вторичная строка подключения** поле.</span><span class="sxs-lookup"><span data-stu-id="414f6-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="414f6-152">Если вы используете строку подключения hello hello [Миграция в Azure DB Cosmos базы данных](import-data.md), добавьте hello базы данных имя toohello конец строки подключения hello.</span><span class="sxs-lookup"><span data-stu-id="414f6-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="414f6-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="414f6-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="414f6-154"><a id="delete"></a>Удаление учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="414f6-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="414f6-155">tooremove Cosmos Azure DB учетной записи из hello портал Azure, больше не используется, имя учетной записи щелкните правой кнопкой мыши hello и нажмите кнопку **удалить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="414f6-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![Как toodelete Cosmos Azure DB учетной записи в hello портала Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="414f6-157">В hello [портал Azure](https://portal.azure.com/), доступ к учетной записи Azure Cosmos DB hello, нужно toodelete.</span><span class="sxs-lookup"><span data-stu-id="414f6-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="414f6-158">На hello **учетная запись Azure Cosmos DB** колонка, щелкните правой кнопкой мыши учетную запись hello и нажмите кнопку **удаление учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="414f6-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="414f6-159">Hello полученный колонке подтверждения введите, требуется учетная запись hello toodelete имя tooconfirm hello Azure Cosmos DB учетной записи.</span><span class="sxs-lookup"><span data-stu-id="414f6-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="414f6-160">Нажмите кнопку hello **удалить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="414f6-160">Click hello **Delete** button.</span></span>

![Как toodelete Cosmos Azure DB учетной записи в hello портала Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="414f6-162"><a id="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="414f6-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="414f6-163">Узнайте, каким образом слишком[приступить к работе с учетной записью Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="414f6-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
