---
title: "aaaIntegrate учетной записи хранилища Azure с Azure CDN | Документы Microsoft"
description: "Узнайте, как содержимое toouse hello Azure сеть доставки содержимого (CDN) toodeliver высокой пропускной способностью путем кэширования больших двоичных объектов из хранилища Azure."
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
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="1c826-103">Интеграция учетной записи хранения Azure с Azure CDN</span><span class="sxs-lookup"><span data-stu-id="1c826-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="1c826-104">CDN может быть включено toocache содержимого из вашего хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1c826-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="1c826-105">Он предлагает разработчикам глобальное решение по доставке контента с высокой пропускной способностью путем кэширования BLOB-объекты и статическое содержимое вычислительных экземпляров в физических узлах в hello США, Европе, Азии, Австралии и Южной Америки.</span><span class="sxs-lookup"><span data-stu-id="1c826-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="1c826-106">Шаг 1. Создание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="1c826-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="1c826-107">Используйте следующие процедуры toocreate новой учетной записи хранения для подписки Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1c826-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="1c826-108">Учетная запись хранения предоставляет доступ к службам хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1c826-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="1c826-109">Hello учетной записи хранилища представляет высший уровень hello hello пространство имен для доступа ко всем hello компоненты службы хранилища Azure: BLOB-объект службы, службы очередей и таблиц.</span><span class="sxs-lookup"><span data-stu-id="1c826-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="1c826-110">Дополнительные сведения см. в разделе toohello [tooMicrosoft введение хранилища Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c826-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="1c826-111">toocreate учетной записи хранилища, необходимо быть Здравствуйте, администратор служб или администратором hello связанные подписки.</span><span class="sxs-lookup"><span data-stu-id="1c826-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1c826-112">Существует несколько способов, которые можно использовать toocreate учетной записи хранилища, включая hello портала Azure и Powershell.</span><span class="sxs-lookup"><span data-stu-id="1c826-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="1c826-113">В этом учебнике мы будем работать с hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1c826-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="1c826-114">**toocreate учетную запись хранения для подписки Azure**</span><span class="sxs-lookup"><span data-stu-id="1c826-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="1c826-115">Войдите в toohello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c826-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1c826-116">В верхнем левом углу hello, выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="1c826-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="1c826-117">В hello **New** диалоговое окно, выберите **данные + хранилище**, нажмите кнопку **учетной записи хранилища**.</span><span class="sxs-lookup"><span data-stu-id="1c826-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="1c826-118">Hello **создать учетную запись хранения** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="1c826-118">hello **Create storage account** blade appears.</span></span>   

    ![Учетная запись хранения][create-new-storage-account]  

3. <span data-ttu-id="1c826-120">В hello **имя** введите имя дочернего домена.</span><span class="sxs-lookup"><span data-stu-id="1c826-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="1c826-121">Запись может содержать от 3 до 24 строчных букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="1c826-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="1c826-122">Это значение становится именем узла hello в URI, который используется для адресации ресурсов больших двоичных объектов, очередей или таблиц для подписки hello hello.</span><span class="sxs-lookup"><span data-stu-id="1c826-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="1c826-123">Для обращения к ресурсу контейнера в hello службы BLOB-объектов, необходимо использовать URI в hello следующая формата, где  *&lt;StorageAccountLabel&gt;*  ссылается toohello значения, введенного в **введите URL-адрес**:</span><span class="sxs-lookup"><span data-stu-id="1c826-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="1c826-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;мой_контейнер&gt;*</span><span class="sxs-lookup"><span data-stu-id="1c826-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="1c826-125">**Важно:** hello URL-адрес метки формы hello дочерний домен учетной записи хранения hello URI и должно быть уникальным среди всех размещенных служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="1c826-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="1c826-126">Это значение также используется как hello имя этой учетной записи хранения в портале hello, или если программный доступ к этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1c826-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="1c826-127">Оставьте значения по умолчанию hello для **модель развертывания**, **учетной записи kind**, **производительности**, и **репликации**.</span><span class="sxs-lookup"><span data-stu-id="1c826-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="1c826-128">Выберите hello **подписки** использование учетной записи хранилища hello со.</span><span class="sxs-lookup"><span data-stu-id="1c826-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="1c826-129">Выберите или создайте **группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="1c826-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="1c826-130">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="1c826-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="1c826-131">Выберите расположение для вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="1c826-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="1c826-132">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1c826-132">Click **Create**.</span></span> <span data-ttu-id="1c826-133">Создание учетной записи хранения hello Hello процесс может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1c826-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="1c826-134">Шаг 2: Включение CDN для учетной записи хранения hello</span><span class="sxs-lookup"><span data-stu-id="1c826-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="1c826-135">Благодаря интеграции новейшие hello теперь можно включить CDN для вашей учетной записи, не выходя из портала модуля хранилища.</span><span class="sxs-lookup"><span data-stu-id="1c826-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="1c826-136">Выберите учетную запись хранения hello, поиск «CDN» или прокрутки вниз от hello левом меню навигации, а затем нажмите кнопку «Azure CDN».</span><span class="sxs-lookup"><span data-stu-id="1c826-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="1c826-137">Hello **Azure CDN** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="1c826-137">hello **Azure CDN** blade appears.</span></span>

    ![Навигация для включения CDN][cdn-enable-navigation]
    
2. <span data-ttu-id="1c826-139">Создайте новую конечную точку, введя hello необходимые сведения</span><span class="sxs-lookup"><span data-stu-id="1c826-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="1c826-140">**Профиль CDN**. Вы можете создать новый профиль или использовать существующий.</span><span class="sxs-lookup"><span data-stu-id="1c826-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="1c826-141">**Ценовая категория**: достаточно tooselect ценовую категорию, если создается новый профиль CDN.</span><span class="sxs-lookup"><span data-stu-id="1c826-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="1c826-142">**Имя конечной точки CDN**. Введите имя конечной точки.</span><span class="sxs-lookup"><span data-stu-id="1c826-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="1c826-143">Конечная точка CDN Hello создан использует имя узла hello учетной записи как источник по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1c826-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="1c826-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="1c826-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="1c826-145">После создания новой конечной точки hello будут отображаться в список конечных точек hello выше.</span><span class="sxs-lookup"><span data-stu-id="1c826-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![Новая конечная точка хранилища CDN][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="1c826-147">Вы можете перейти tooAzure CDN расширения tooenable CDN. [Учебника](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="1c826-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="1c826-148">Шаг 3. Включение дополнительных функций CDN</span><span class="sxs-lookup"><span data-stu-id="1c826-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="1c826-149">Из колонки «Azure CDN» учетной записи хранилища щелкните конечную точку CDN hello из hello список tooopen CDN конфигурации колонки.</span><span class="sxs-lookup"><span data-stu-id="1c826-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="1c826-150">Можно включить дополнительные функции CDN, например сжатие, строку запроса, геофильтрацию.</span><span class="sxs-lookup"><span data-stu-id="1c826-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="1c826-151">Кроме того, можно также добавить конечную точку CDN tooyour сопоставления пользовательского домена и включить пользовательский домен HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1c826-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![Конфигурация CDN хранилища CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="1c826-153">Шаг 4. Доступ к содержимому CDN</span><span class="sxs-lookup"><span data-stu-id="1c826-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="1c826-154">tooaccess кэшированного содержимого на hello CDN, hello используйте URL-адрес CDN указано на портале hello.</span><span class="sxs-lookup"><span data-stu-id="1c826-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="1c826-155">Hello адрес кэшированного BLOB-объекта будет примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="1c826-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="1c826-156">http://<*имя_конечной_точки*\>.azureedge.net/<*общедоступный_контейнер*\>/<*имя_большого_двоичного_объекта*\></span><span class="sxs-lookup"><span data-stu-id="1c826-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="1c826-157">После включения учетной записи хранилища CDN доступ tooa все общедоступные объекты могут быть кэшированы пограничное кэширование CDN.</span><span class="sxs-lookup"><span data-stu-id="1c826-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="1c826-158">Если изменить объект, который в настоящее время кэшированных в hello CDN hello новое содержимое будет недоступен через hello CDN пока hello CDN обновляет его содержимое по окончании периода содержимого time-to-live hello в кэше.</span><span class="sxs-lookup"><span data-stu-id="1c826-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="1c826-159">Шаг 5: Удаление содержимого из CDN hello</span><span class="sxs-lookup"><span data-stu-id="1c826-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="1c826-160">Если вы больше не хотите toocache объекта в hello Azure доставки содержимого сети (CDN), можно выполнить одно из hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="1c826-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="1c826-161">Можно сделать hello контейнер закрытым, а не открытым.</span><span class="sxs-lookup"><span data-stu-id="1c826-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="1c826-162">В разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](../storage/blobs/storage-manage-access-to-resources.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="1c826-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="1c826-163">Можно отключить или удалить конечную точку CDN hello, с помощью портала управления hello.</span><span class="sxs-lookup"><span data-stu-id="1c826-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="1c826-164">Вы можете изменить вашей размещенной службы toono дольше ответ toorequests для hello объекта.</span><span class="sxs-lookup"><span data-stu-id="1c826-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="1c826-165">Объект, уже кэшированный в hello CDN будет остаются в кэше до истечения периода времени жизни hello объекта hello, или пока не будет очищено hello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="1c826-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="1c826-166">По истечении периода времени существования hello hello CDN проверяет toosee ли конечная точка CDN hello все еще действительна, hello объекта применимым для анонимного доступа.</span><span class="sxs-lookup"><span data-stu-id="1c826-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="1c826-167">Если это не так, затем hello объекта больше не кэшируются.</span><span class="sxs-lookup"><span data-stu-id="1c826-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c826-168">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1c826-168">Additional resources</span></span>
* [<span data-ttu-id="1c826-169">Как tooMap содержимого CDN tooa пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="1c826-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="1c826-170">Включение протокола HTTPS для личного домена Azure CDN</span><span class="sxs-lookup"><span data-stu-id="1c826-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
