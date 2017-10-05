---
title: "Схемы для проверки XML — Azure Logic Apps | Документация Майкрософт"
description: "Проверка XML-документов с помощью схем для Azure Logic Apps и пакета интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4f58a587c1f10aea1cee89e46fa9ec340e0d21c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="06da3-103">Проверка XML с помощью схем для Azure Logic Apps и пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="06da3-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="06da3-104">Схемы используются для подтверждения того, что получаемые документы XML являются допустимыми и содержат ожидаемые данные в предопределенном формате.</span><span class="sxs-lookup"><span data-stu-id="06da3-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="06da3-105">С помощью схем также можно проверить сообщения, которыми стороны обмениваются в сценарии B2B.</span><span class="sxs-lookup"><span data-stu-id="06da3-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="06da3-106">Добавление схемы</span><span class="sxs-lookup"><span data-stu-id="06da3-106">Add a schema</span></span>

1. <span data-ttu-id="06da3-107">На портале Azure щелкните **Другие службы**.</span><span class="sxs-lookup"><span data-stu-id="06da3-107">In the Azure portal, select **More services**.</span></span>

    ![Портал Azure, "Другие службы"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="06da3-109">Введите **интеграции** в поле фильтра поиска и выберите **Учетные записи интеграции** в списке результатов.</span><span class="sxs-lookup"><span data-stu-id="06da3-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![Поле фильтра поиска](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="06da3-111">Выберите **учетную запись интеграции**, в которую необходимо добавить схему.</span><span class="sxs-lookup"><span data-stu-id="06da3-111">Select the **integration account** where you want to add the schema.</span></span>

    ![Список учетных записей интеграции](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="06da3-113">Выберите плитку **Схемы**.</span><span class="sxs-lookup"><span data-stu-id="06da3-113">Choose the **Schemas** tile.</span></span>

    ![Пример учетной записи интеграции, "Схемы"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="06da3-115">Добавление файла схемы, размер которого меньше 2 МБ</span><span class="sxs-lookup"><span data-stu-id="06da3-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="06da3-116">В открывшейся колонке **Схемы** (см. выше) нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="06da3-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![Колонка "Схемы", "Добавить"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="06da3-118">Введите имя для схемы.</span><span class="sxs-lookup"><span data-stu-id="06da3-118">Enter a name for your schema.</span></span> <span data-ttu-id="06da3-119">Чтобы передать файл схемы, выберите значок папки рядом с текстовым полем **Схемы**.</span><span class="sxs-lookup"><span data-stu-id="06da3-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="06da3-120">После завершения передачи нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="06da3-120">After the upload process completes, select **OK**.</span></span>

    ![Снимок экрана: колонка "Добавление схемы" с выделенным элементом "Мелкий файл"](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="06da3-122">Добавление файла схемы, размер которого больше 2 МБ (максимум 8 МБ)</span><span class="sxs-lookup"><span data-stu-id="06da3-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="06da3-123">Эта процедура зависит от уровня доступа к контейнеру больших двоичных объектов: **Общедоступный** или **Без анонимного доступа**.</span><span class="sxs-lookup"><span data-stu-id="06da3-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="06da3-124">**Определение уровня доступа**</span><span class="sxs-lookup"><span data-stu-id="06da3-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="06da3-125">Откройте **обозреватель хранилищ Azure**.</span><span class="sxs-lookup"><span data-stu-id="06da3-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="06da3-126">В разделе **Контейнеры BLOB-объектов** выберите нужный контейнер двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="06da3-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="06da3-127">Выберите последовательно **Безопасность**, **Уровень доступа**.</span><span class="sxs-lookup"><span data-stu-id="06da3-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="06da3-128">Если для контейнера больших двоичных объектов определен уровень доступа **Общедоступный**, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="06da3-128">If the blob security access level is **Public**, follow these steps.</span></span>

![Обозреватель хранилищ Azure с выделенными элементами "Контейнеры больших двоичных объектов", "Безопасность" и "Общедоступный"](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="06da3-130">Передайте схему в учетную запись хранения и скопируйте универсальный код ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="06da3-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![Учетная запись хранения с выделенным URI](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="06da3-132">В колонке **Добавление схемы** выберите **Большой файл** и укажите универсальный код ресурса (URI) в текстовом поле **URI контента**.</span><span class="sxs-lookup"><span data-stu-id="06da3-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    ![Страница "Схемы", на которой выделены кнопка "Добавить" и параметр "Большой файл"](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="06da3-134">Если для контейнера больших двоичных объектов определен уровень доступа **Без анонимного доступа**, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="06da3-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

![Обозреватель хранилищ Azure с выделенными элементами "Контейнеры больших двоичных объектов", "Безопасность" и "Без анонимного доступа"](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="06da3-136">Передайте схему в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="06da3-136">Upload the schema to your storage account.</span></span>

    ![Учетная запись хранения](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="06da3-138">Создайте подписанный URL-адрес для схемы.</span><span class="sxs-lookup"><span data-stu-id="06da3-138">Generate a shared access signature for the schema.</span></span>

    ![Учетная запись хранения с выделенной вкладкой подписанных URL-адресов](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="06da3-140">В колонке **Добавление схемы** выберите **Большой файл** и укажите URI подписанного URL-адреса в текстовом поле **URI содержимого**.</span><span class="sxs-lookup"><span data-stu-id="06da3-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    ![Страница "Схемы", на которой выделены кнопка "Добавить" и параметр "Большой файл"](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="06da3-142">В колонке **Схемы** учетной записи интеграции теперь должна быть видна добавленная схема.</span><span class="sxs-lookup"><span data-stu-id="06da3-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Учетная запись интеграции с выделенными плиткой "Схемы" и новой схемой](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="06da3-144">Изменение схем</span><span class="sxs-lookup"><span data-stu-id="06da3-144">Edit schemas</span></span>

1. <span data-ttu-id="06da3-145">Выберите плитку **Схемы**.</span><span class="sxs-lookup"><span data-stu-id="06da3-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="06da3-146">В открывшейся колонке **Схемы** выберите схему, которую вы хотите изменить.</span><span class="sxs-lookup"><span data-stu-id="06da3-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="06da3-147">В колонке **Схемы** нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="06da3-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![Колонка "Схемы"](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="06da3-149">Выберите файл схемы, который требуется изменить, а затем нажмите кнопку **открыть**.</span><span class="sxs-lookup"><span data-stu-id="06da3-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![Открытие файла схемы для редактирования](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="06da3-151">Azure отображает сообщение, что схема успешно отправлена.</span><span class="sxs-lookup"><span data-stu-id="06da3-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="06da3-152">Удаление схем</span><span class="sxs-lookup"><span data-stu-id="06da3-152">Delete schemas</span></span>

1. <span data-ttu-id="06da3-153">Выберите плитку **Схемы**.</span><span class="sxs-lookup"><span data-stu-id="06da3-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="06da3-154">В открывшейся колонке **Схемы** выберите схему, которую вы хотите удалить.</span><span class="sxs-lookup"><span data-stu-id="06da3-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="06da3-155">В колонке **Схемы** нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="06da3-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![Колонка "Схемы"](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="06da3-157">Нажмите кнопку **Да**, чтобы подтвердить удаление выбранной схемы.</span><span class="sxs-lookup"><span data-stu-id="06da3-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    ![Сообщение с подтверждением "Удаление схемы"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="06da3-159">В колонке **Схемы** список схем обновляется, и удаленная схема больше не отображается.</span><span class="sxs-lookup"><span data-stu-id="06da3-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    ![Учетная запись интеграции с выделенной плиткой "Схемы"](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="06da3-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06da3-161">Next steps</span></span>
* <span data-ttu-id="06da3-162">[Узнайте больше о пакете интеграции Enterprise.](logic-apps-enterprise-integration-overview.md "Узнайте о пакете интеграции Enterprise").</span><span class="sxs-lookup"><span data-stu-id="06da3-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  

