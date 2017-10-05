---
title: "Управление учетной записью Azure Cosmos DB на портале Azure | Документация Майкрософт"
description: "Узнайте, как управлять учетной записью Azure Cosmos DB на портале Azure. Изучите руководство по использованию портала Azure для просмотра, копирования, удаления учетной записи и доступа к ней."
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
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="3730f-105">Как управлять учетной записью Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3730f-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="3730f-106">Узнайте, как задать глобальную согласованность, как работать с ключами и как удалить учетную запись Azure Cosmos DB на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3730f-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="3730f-107"><a id="consistency"></a>Управление параметрами согласованности Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3730f-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="3730f-108">Выбор правильного уровня согласованности зависит от семантики вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="3730f-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="3730f-109">Сведения о доступных настраиваемых уровнях согласованности данных в Azure Cosmos DB см. в [этой статье][consistency].</span><span class="sxs-lookup"><span data-stu-id="3730f-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="3730f-110">Azure Cosmos DB предоставляет гарантии согласованности, доступности и производительности для любого уровня согласованности, доступного учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="3730f-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="3730f-111">Чтобы настроить для учетной записи базы данных строгий уровень согласованности, требуется, чтобы данные находились только в одном регионе Azure и не были глобально доступны.</span><span class="sxs-lookup"><span data-stu-id="3730f-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="3730f-112">С другой стороны, нестрогие уровни согласованности (с ограниченным устареванием, уровня сеанса или согласованность в конечном счете) дают возможность связать любое количество регионов Azure с учетной записью базы данных.</span><span class="sxs-lookup"><span data-stu-id="3730f-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="3730f-113">Следующие простые действия показывают, как выбрать уровень согласованности по умолчанию для учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="3730f-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="3730f-114">Установка согласованности по умолчанию для учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3730f-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="3730f-115">Войдите в свою учетную запись Azure Cosmos DB на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3730f-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="3730f-116">В колонке учетной записи щелкните **Согласованность по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="3730f-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="3730f-117">В колонке **Согласованность по умолчанию** выберите новый уровень согласованности и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3730f-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="3730f-118">![Сеанс согласованности по умолчанию][5]</span><span class="sxs-lookup"><span data-stu-id="3730f-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="3730f-119"><a id="keys"></a>Просмотр, копирование и повторное создание ключей доступа</span><span class="sxs-lookup"><span data-stu-id="3730f-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="3730f-120">При создании учетной записи Azure Cosmos DB служба создает два главных ключа доступа, которые можно использовать для проверки подлинности при доступе к учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3730f-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="3730f-121">Предоставляя два ключа, Azure Cosmos DB позволяет вам повторно создавать ключи без перерывов в работе учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3730f-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="3730f-122">На [портале Azure](https://portal.azure.com/) откройте колонку **Ключи** из меню ресурсов в колонке **учетной записи Azure Cosmos DB**, чтобы получить возможность просмотра, копирования и повторного создания ключей доступа, используемых для доступа к вашей учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3730f-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Снимок экрана портала Azure, колонка «Ключи»](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="3730f-124">Колонка **Ключи** также содержит первичную и вторичную строки подключения, используемые для подключения к учетной записи из [средства переноса данных](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="3730f-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="3730f-125">В этой колонке также доступны ключи только для чтения.</span><span class="sxs-lookup"><span data-stu-id="3730f-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="3730f-126">Чтение и запросы являются операциями только для чтения, а создание, удаление и замена — нет.</span><span class="sxs-lookup"><span data-stu-id="3730f-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="3730f-127">Копирование ключа доступа на портале Azure</span><span class="sxs-lookup"><span data-stu-id="3730f-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="3730f-128">В колонке **Ключи** нажмите кнопку **Копировать** справа от того ключа, который требуется скопировать.</span><span class="sxs-lookup"><span data-stu-id="3730f-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![Просмотр и копирование ключа доступа на портале Azure, колонка «Ключи»](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="3730f-130">Повторное создание ключей доступа</span><span class="sxs-lookup"><span data-stu-id="3730f-130">Regenerate access keys</span></span>
<span data-ttu-id="3730f-131">Вам следует периодически менять ключи доступа для своей учетной записи Azure Cosmos DB, чтобы повысить уровень безопасности соединений.</span><span class="sxs-lookup"><span data-stu-id="3730f-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="3730f-132">Назначается два ключа доступа, что позволяет поддерживать подключения к учетной записи Azure Cosmos DB с помощью одного ключа, одновременно повторно создавая второй ключ.</span><span class="sxs-lookup"><span data-stu-id="3730f-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="3730f-133">Повторное создание ключей доступа влияет на все приложения, которые зависят от текущего ключа.</span><span class="sxs-lookup"><span data-stu-id="3730f-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="3730f-134">Необходимо обновить все клиенты, использующие ключ доступа для обращения к учетной записи Azure Cosmos DB, чтобы они использовали новый ключ.</span><span class="sxs-lookup"><span data-stu-id="3730f-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="3730f-135">Если имеются приложения или облачные службы, использующие учетную запись Azure Cosmos DB, вы потеряете эти подключения при повторном создании ключей, пока не возобновите ключи.</span><span class="sxs-lookup"><span data-stu-id="3730f-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="3730f-136">Ниже описан процесс возобновления ключей.</span><span class="sxs-lookup"><span data-stu-id="3730f-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="3730f-137">Обновите ключ доступа в коде приложения, чтобы задать ссылку на дополнительный ключ доступа учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3730f-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="3730f-138">Повторно создайте главный ключ доступа для своей учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3730f-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="3730f-139">Войдите в свою учетную запись Azure Cosmos DB на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3730f-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="3730f-140">В колонке **учетной записи Azure Cosmos DB** щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="3730f-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="3730f-141">В колонке **Ключи** нажмите кнопку "Повторно создать", а затем кнопку **ОК**, чтобы подтвердить создание ключа.</span><span class="sxs-lookup"><span data-stu-id="3730f-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="3730f-142">![Повторное создание ключей доступа](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="3730f-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="3730f-143">Убедившись, что новый ключ доступен для использования (примерно через 5 минут после повторного создания), обновите ключ доступа в коде приложения, чтобы задать ссылку на новый главный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="3730f-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="3730f-144">Повторно создайте дополнительный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="3730f-144">Regenerate the secondary access key.</span></span>
   
    ![Повторное создание ключей доступа](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="3730f-146">Для использования нового ключа для доступа к учетной записи Azure Cosmos DB может потребоваться подождать несколько минут.</span><span class="sxs-lookup"><span data-stu-id="3730f-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="3730f-147">Получение строки подключения</span><span class="sxs-lookup"><span data-stu-id="3730f-147">Get the  connection string</span></span>
<span data-ttu-id="3730f-148">Чтобы получить строку подключения, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="3730f-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="3730f-149">Войдите в свою учетную запись Azure Cosmos DB на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3730f-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="3730f-150">В меню ресурсов выберите **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="3730f-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="3730f-151">Нажмите кнопку **Копировать** рядом с полем **Первичная строка подключения** или **Вторичная строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="3730f-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="3730f-152">Если вы используете строку подключения в [средстве миграции базы данных Azure Cosmos DB](import-data.md), добавьте имя базы данных в конец строки подключения.</span><span class="sxs-lookup"><span data-stu-id="3730f-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="3730f-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="3730f-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="3730f-154"><a id="delete"></a>Удаление учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3730f-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="3730f-155">Чтобы удалить учетную запись Azure Cosmos DB, которая больше не нужна, щелкните правой кнопкой мыши имя учетной записи и выберите команду **Удалить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="3730f-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![Как удалить учетную запись Azure Cosmos DB на портале Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="3730f-157">На [портале Azure](https://portal.azure.com/) перейдите в учетную запись Azure Cosmos DB, которую необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="3730f-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="3730f-158">В колонке **учетной записи Azure Cosmos DB** щелкните правой кнопкой мыши учетную запись и выберите команду **Удалить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="3730f-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="3730f-159">В появившейся колонке подтверждения введите имя учетной записи Azure Cosmos DB, чтобы подтвердить ее удаление.</span><span class="sxs-lookup"><span data-stu-id="3730f-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="3730f-160">Нажмите кнопку **Удалить** .</span><span class="sxs-lookup"><span data-stu-id="3730f-160">Click the **Delete** button.</span></span>

![Как удалить учетную запись Azure Cosmos DB на портале Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="3730f-162"><a id="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3730f-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="3730f-163">Узнайте о том, как [приступить к работе с учетной записью Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="3730f-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
