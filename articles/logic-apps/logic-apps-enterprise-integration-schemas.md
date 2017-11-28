---
title: "aaaSchemas для проверки XML - приложения логики Azure | Документы Microsoft"
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
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="45675-103">Проверка XML с помощью схем для приложения логики Azure и hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="45675-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="45675-104">Схемы убедитесь, что hello XML-документов, полученный являются допустимыми и hello ожиданиям данных в стандартных форматов.</span><span class="sxs-lookup"><span data-stu-id="45675-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="45675-105">С помощью схем также можно проверить сообщения, которыми стороны обмениваются в сценарии B2B.</span><span class="sxs-lookup"><span data-stu-id="45675-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="45675-106">Добавление схемы</span><span class="sxs-lookup"><span data-stu-id="45675-106">Add a schema</span></span>

1. <span data-ttu-id="45675-107">В hello портал Azure, выберите **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="45675-107">In hello Azure portal, select **More services**.</span></span>

    ![Портал Azure, "Другие службы"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="45675-109">Введите в поле поиска фильтра hello, **интеграции**и выберите **учетные записи службы интеграции** из списка результатов hello.</span><span class="sxs-lookup"><span data-stu-id="45675-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![Поле фильтра поиска](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="45675-111">Выберите hello **учетной записи интеграции** место tooadd hello схемы.</span><span class="sxs-lookup"><span data-stu-id="45675-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![Список учетных записей интеграции](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="45675-113">Выберите hello **схемы** плитки.</span><span class="sxs-lookup"><span data-stu-id="45675-113">Choose hello **Schemas** tile.</span></span>

    ![Пример учетной записи интеграции, "Схемы"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="45675-115">Добавление файла схемы, размер которого меньше 2 МБ</span><span class="sxs-lookup"><span data-stu-id="45675-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="45675-116">В hello **схемы** колонку, которая открывает (из hello предыдущих шагах), выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="45675-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![Колонка "Схемы", "Добавить"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="45675-118">Введите имя для схемы.</span><span class="sxs-lookup"><span data-stu-id="45675-118">Enter a name for your schema.</span></span> <span data-ttu-id="45675-119">Загрузить файл схемы hello, выбрав toohello Далее значок папки hello **схемы** поле.</span><span class="sxs-lookup"><span data-stu-id="45675-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="45675-120">После завершения процесса отправки hello **ОК**.</span><span class="sxs-lookup"><span data-stu-id="45675-120">After hello upload process completes, select **OK**.</span></span>

    ![Снимок экрана: колонка "Добавление схемы" с выделенным элементом "Мелкий файл"](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="45675-122">Добавьте файл схемы, размер которых превышает 2 МБ (вверх максимум too8 МБ)</span><span class="sxs-lookup"><span data-stu-id="45675-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="45675-123">Эти действия различаются в зависимости от уровня доступа для контейнера большого двоичного объекта hello: **открытый** или **отсутствие анонимного доступа**.</span><span class="sxs-lookup"><span data-stu-id="45675-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="45675-124">**toodetermine этот уровень доступа**</span><span class="sxs-lookup"><span data-stu-id="45675-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="45675-125">Откройте **обозреватель хранилищ Azure**.</span><span class="sxs-lookup"><span data-stu-id="45675-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="45675-126">В разделе **контейнеров больших двоичных объектов**, выберите контейнер больших двоичных объектов hello требуется.</span><span class="sxs-lookup"><span data-stu-id="45675-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="45675-127">Выберите последовательно **Безопасность**, **Уровень доступа**.</span><span class="sxs-lookup"><span data-stu-id="45675-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="45675-128">Если уровень доступа hello большого двоичного объекта безопасности **открытый**, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="45675-128">If hello blob security access level is **Public**, follow these steps.</span></span>

![Обозреватель хранилищ Azure с выделенными элементами "Контейнеры больших двоичных объектов", "Безопасность" и "Общедоступный"](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="45675-130">Передайте учетной записи хранилища tooyour схемы hello и скопируйте hello URI.</span><span class="sxs-lookup"><span data-stu-id="45675-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![Учетная запись хранения с выделенным URI](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="45675-132">В **добавить схему**выберите **большого файла**и укажите hello URI в hello **URI содержимого** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="45675-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    ![Страница "Схемы", на которой выделены кнопка "Добавить" и параметр "Большой файл"](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="45675-134">Если уровень доступа hello большого двоичного объекта безопасности **отсутствие анонимного доступа**, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="45675-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

![Обозреватель хранилищ Azure с выделенными элементами "Контейнеры больших двоичных объектов", "Безопасность" и "Без анонимного доступа"](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="45675-136">Передача схемы для hello tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="45675-136">Upload hello schema tooyour storage account.</span></span>

    ![Учетная запись хранения](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="45675-138">Создать подпись общего доступа для схемы hello.</span><span class="sxs-lookup"><span data-stu-id="45675-138">Generate a shared access signature for hello schema.</span></span>

    ![Учетная запись хранения с выделенной вкладкой подписанных URL-адресов](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="45675-140">В **добавить схему**выберите **большого файла**и укажите URI подписи коллективного доступа hello в hello **URI содержимого** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="45675-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    ![Страница "Схемы", на которой выделены кнопка "Добавить" и параметр "Большой файл"](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="45675-142">В hello **схемы** колонке учетной записи интеграции должны появиться добавленный схему.</span><span class="sxs-lookup"><span data-stu-id="45675-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Вашей учетной записи интеграции с «Схемы» и новой схемы hello выделен](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="45675-144">Изменение схем</span><span class="sxs-lookup"><span data-stu-id="45675-144">Edit schemas</span></span>

1. <span data-ttu-id="45675-145">Выберите hello **схемы** плитки.</span><span class="sxs-lookup"><span data-stu-id="45675-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="45675-146">После hello **схемы** открывает колонку hello выберите схемы, которые должны tooedit.</span><span class="sxs-lookup"><span data-stu-id="45675-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="45675-147">На hello **схемы** колонке выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="45675-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![Колонка "Схемы"](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="45675-149">Файл схемы выберите hello требуется tooedit, затем выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="45675-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![Открытие схемы файла tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="45675-151">Azure отображает сообщение, hello схемы успешно отправлены.</span><span class="sxs-lookup"><span data-stu-id="45675-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="45675-152">Удаление схем</span><span class="sxs-lookup"><span data-stu-id="45675-152">Delete schemas</span></span>

1. <span data-ttu-id="45675-153">Выберите hello **схемы** плитки.</span><span class="sxs-lookup"><span data-stu-id="45675-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="45675-154">После hello **схемы** открывает колонку, требуется toodelete схемы выберите hello.</span><span class="sxs-lookup"><span data-stu-id="45675-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="45675-155">На hello **схемы** колонке выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="45675-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![Колонка "Схемы"](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="45675-157">tooconfirm, что требуется toodelete hello выбора схемы, выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="45675-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    ![Сообщение с подтверждением "Удаление схемы"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="45675-159">В hello **схемы** колонке hello схемы список обновляется и больше не включает схему hello удаленного.</span><span class="sxs-lookup"><span data-stu-id="45675-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![Учетная запись интеграции с выделенной плиткой "Схемы"](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="45675-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45675-161">Next steps</span></span>
* <span data-ttu-id="45675-162">[Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции enterprise hello").</span><span class="sxs-lookup"><span data-stu-id="45675-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

