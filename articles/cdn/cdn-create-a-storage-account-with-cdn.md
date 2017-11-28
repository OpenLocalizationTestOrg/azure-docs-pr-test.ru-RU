---
title: "Интеграция учетной записи хранения Azure с Azure CDN | Документация Майкрософт"
description: "Узнайте, как использовать сеть доставки содержимого (CDN) Azure для доставки больших объемов контента с помощью кэширования BLOB-объектов в службе хранилища Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="29e0b-103">Интеграция учетной записи хранения Azure с Azure CDN</span><span class="sxs-lookup"><span data-stu-id="29e0b-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="29e0b-104">CDN можно включить для кэширования содержимого из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="29e0b-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="29e0b-105">Она предоставляет разработчикам глобальное решение для доставки большого объема содержимого с возможностью кэширования больших двоичных объектов и статического содержимого на физических узлах в США, Европе, Азии, Австралии и Южной Америке.</span><span class="sxs-lookup"><span data-stu-id="29e0b-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="29e0b-106">Шаг 1. Создание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="29e0b-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="29e0b-107">Чтобы создать новую учетную запись хранения для подписки Azure, воспользуйтесь следующей процедурой.</span><span class="sxs-lookup"><span data-stu-id="29e0b-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="29e0b-108">Учетная запись хранения предоставляет доступ к службам хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="29e0b-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="29e0b-109">Учетная запись хранения представляет собой высший уровень пространства имен для доступа ко всем компонентам службы хранения Azure: службам BLOB-объектов, службам очередей и службам таблиц.</span><span class="sxs-lookup"><span data-stu-id="29e0b-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="29e0b-110">Дополнительные сведения см. в статье [Введение в хранилище Microsoft Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29e0b-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="29e0b-111">Чтобы создать учетную запись хранения, вы должны быть администратором службы или соадминистратором для связанной подписки.</span><span class="sxs-lookup"><span data-stu-id="29e0b-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="29e0b-112">Существует несколько способов, которые можно использовать для создания учетной записи хранения. В их число входят портал Azure и Powershell.</span><span class="sxs-lookup"><span data-stu-id="29e0b-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="29e0b-113">В этом учебнике мы будем использовать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="29e0b-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="29e0b-114">**Создание учетной записи хранения для подписки Azure**</span><span class="sxs-lookup"><span data-stu-id="29e0b-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="29e0b-115">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="29e0b-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="29e0b-116">В нижнем левом углу щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="29e0b-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="29e0b-117">В диалоговом окне **Создать** выберите **Данные + хранилище**, затем щелкните **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="29e0b-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="29e0b-118">Появится колонка **Учетная запись хранения** .</span><span class="sxs-lookup"><span data-stu-id="29e0b-118">The **Create storage account** blade appears.</span></span>   

    ![Учетная запись хранения][create-new-storage-account]  

3. <span data-ttu-id="29e0b-120">В поле **Имя** введите имя поддомена.</span><span class="sxs-lookup"><span data-stu-id="29e0b-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="29e0b-121">Запись может содержать от 3 до 24 строчных букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="29e0b-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="29e0b-122">Это значение станет именем узла в URI, который используется для адресации ресурсов большого двоичного объекта, очереди и таблицы в подписке.</span><span class="sxs-lookup"><span data-stu-id="29e0b-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="29e0b-123">Чтобы обратиться по адресу ресурса контейнера в службе BLOB-объектов, следует использовать URI в следующем формате, где *&lt;StorageAccountLabel&gt;* указывает значение, которое вы ввели в поле **Введите URL-адрес**:</span><span class="sxs-lookup"><span data-stu-id="29e0b-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="29e0b-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;мой_контейнер&gt;*</span><span class="sxs-lookup"><span data-stu-id="29e0b-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="29e0b-125">**Важно!** Метка URL-адреса образует поддомен URI учетной записи хранения и должна быть уникальной на уровне всех размещенных служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="29e0b-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="29e0b-126">Это значение также используется как имя этой учетной записи хранения на портале или при доступе к данной учетной записи программным способом.</span><span class="sxs-lookup"><span data-stu-id="29e0b-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="29e0b-127">Оставьте значения по умолчанию для **модели развертывания**, **типа учетной записи**, **производительности** и **репликации**.</span><span class="sxs-lookup"><span data-stu-id="29e0b-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="29e0b-128">Выберите **подписку** , с которой будет использоваться данная учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="29e0b-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="29e0b-129">Выберите или создайте **группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="29e0b-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="29e0b-130">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="29e0b-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="29e0b-131">Выберите расположение для вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="29e0b-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="29e0b-132">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="29e0b-132">Click **Create**.</span></span> <span data-ttu-id="29e0b-133">Процесс создания учетной записи хранения может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="29e0b-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="29e0b-134">Шаг 2. Включение CDN для учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="29e0b-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="29e0b-135">Благодаря последней интеграции теперь можно включать CDN для вашей учетной записи хранения, не выходя из расширения портала хранилища.</span><span class="sxs-lookup"><span data-stu-id="29e0b-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="29e0b-136">Выберите учетную запись хранения, выполните поиск по запросу "CDN" или прокрутите меню навигации слева и щелкните Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="29e0b-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="29e0b-137">Откроется колонка **Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="29e0b-137">The **Azure CDN** blade appears.</span></span>

    ![Навигация для включения CDN][cdn-enable-navigation]
    
2. <span data-ttu-id="29e0b-139">Создайте новую конечную точку, указав необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="29e0b-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="29e0b-140">**Профиль CDN**. Вы можете создать новый профиль или использовать существующий.</span><span class="sxs-lookup"><span data-stu-id="29e0b-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="29e0b-141">**Ценовая категория**. Ценовую категорию необходимо выбрать, только если вы создаете новый профиль CDN.</span><span class="sxs-lookup"><span data-stu-id="29e0b-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="29e0b-142">**Имя конечной точки CDN**. Введите имя конечной точки.</span><span class="sxs-lookup"><span data-stu-id="29e0b-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="29e0b-143">Созданная конечная точка CDN использует имя узла учетной записи хранения как источник по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="29e0b-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="29e0b-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="29e0b-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="29e0b-145">После создания новая конечная точка отобразится в списке конечных точек.</span><span class="sxs-lookup"><span data-stu-id="29e0b-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![Новая конечная точка хранилища CDN][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="29e0b-147">Также для включения CDN можно перейти к расширению Azure CDN. [Руководство](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="29e0b-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="29e0b-148">Шаг 3. Включение дополнительных функций CDN</span><span class="sxs-lookup"><span data-stu-id="29e0b-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="29e0b-149">В колонке Azure CDN учетной записи хранения щелкните в списке конечную точку CDN, чтобы открыть колонку конфигурации CDN.</span><span class="sxs-lookup"><span data-stu-id="29e0b-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="29e0b-150">Можно включить дополнительные функции CDN, например сжатие, строку запроса, геофильтрацию.</span><span class="sxs-lookup"><span data-stu-id="29e0b-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="29e0b-151">Можно также добавить сопоставление личного домена для конечной точки CDN и включить личный домен HTTPS.</span><span class="sxs-lookup"><span data-stu-id="29e0b-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![Конфигурация CDN хранилища CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="29e0b-153">Шаг 4. Доступ к содержимому CDN</span><span class="sxs-lookup"><span data-stu-id="29e0b-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="29e0b-154">Для доступа к кэшированному содержимому в сети CDN воспользуйтесь URL-адресом CDN, отображаемым в портале.</span><span class="sxs-lookup"><span data-stu-id="29e0b-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="29e0b-155">Адрес для кэшированного BLOB-объекта будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="29e0b-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="29e0b-156">http://<*имя_конечной_точки*\>.azureedge.net/<*общедоступный_контейнер*\>/<*имя_большого_двоичного_объекта*\></span><span class="sxs-lookup"><span data-stu-id="29e0b-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="29e0b-157">После включения доступа CDN к учетной записи хранения все общедоступные объекты будут пригодны для пограничного кэширования CDN.</span><span class="sxs-lookup"><span data-stu-id="29e0b-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="29e0b-158">Если изменить объект, находящийся в данный момент в кэше сети CDN, новое содержимое будет недоступно через сеть CDN до обновления содержимого CDN по истечении срока действия кэшированного содержимого.</span><span class="sxs-lookup"><span data-stu-id="29e0b-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="29e0b-159">Шаг 5. Удаление содержимого из сети CDN</span><span class="sxs-lookup"><span data-stu-id="29e0b-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="29e0b-160">Если кэширование объекта в сети CDN Azure больше не требуется, можно выполнить одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="29e0b-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="29e0b-161">Можно сделать контейнер закрытым, а не общедоступным.</span><span class="sxs-lookup"><span data-stu-id="29e0b-161">You can make the container private instead of public.</span></span> <span data-ttu-id="29e0b-162">Дополнительные сведения см. в статье [Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам](../storage/blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="29e0b-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="29e0b-163">Вы можете отключить или удалить конечную точку CDN на портале управления.</span><span class="sxs-lookup"><span data-stu-id="29e0b-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="29e0b-164">Вы можете изменить размещенную службу, чтобы она перестала отвечать на запросы объекта.</span><span class="sxs-lookup"><span data-stu-id="29e0b-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="29e0b-165">Объект, уже кэшированный в сети CDN, останется в кэше до истечения срока действия этого объекта или до удаления конечной точки.</span><span class="sxs-lookup"><span data-stu-id="29e0b-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="29e0b-166">По истечении срока действия CDN выполнит проверку конечной точки CDN, чтобы выяснить, что она еще действует и объект по-прежнему находится в анонимном доступе.</span><span class="sxs-lookup"><span data-stu-id="29e0b-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="29e0b-167">Если это не так, объект больше не будет кэшироваться.</span><span class="sxs-lookup"><span data-stu-id="29e0b-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29e0b-168">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="29e0b-168">Additional resources</span></span>
* [<span data-ttu-id="29e0b-169">Сопоставление содержимого CDN с пользовательским доменом</span><span class="sxs-lookup"><span data-stu-id="29e0b-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="29e0b-170">Включение протокола HTTPS для личного домена Azure CDN</span><span class="sxs-lookup"><span data-stu-id="29e0b-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
