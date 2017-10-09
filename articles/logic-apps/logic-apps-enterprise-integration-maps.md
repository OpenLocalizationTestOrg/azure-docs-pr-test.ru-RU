---
title: "aaaTransform XML с картами XSLT - приложения логики Azure | Документы Microsoft"
description: "Добавление XSLT карты tootransform XML-данных с помощью приложения логики Azure и hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="8342d-103">Добавление карт для преобразования данных XML</span><span class="sxs-lookup"><span data-stu-id="8342d-103">Add maps for XML data transform</span></span>

<span data-ttu-id="8342d-104">Enterprise интеграции использует сопоставляет XML-данные tootransform между форматами.</span><span class="sxs-lookup"><span data-stu-id="8342d-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="8342d-105">Карта представляет XML-документ, который определяет hello данные в документе, который необходимо преобразовать в другой формат.</span><span class="sxs-lookup"><span data-stu-id="8342d-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="8342d-106">Для чего используются карты?</span><span class="sxs-lookup"><span data-stu-id="8342d-106">Why use maps?</span></span>

<span data-ttu-id="8342d-107">Предположим, что регулярно появление B2B заказов или счетов из клиента, который использует формат YYYMMDD hello для дат.</span><span class="sxs-lookup"><span data-stu-id="8342d-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="8342d-108">Однако в вашей организации хранить даты в формате MMDDYYY hello.</span><span class="sxs-lookup"><span data-stu-id="8342d-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="8342d-109">Также можно использовать карту*преобразования* формат даты YYYMMDD hello в hello MMDDYYY перед сохранением в базе данных активности клиентов hello подробности заказа или счета.</span><span class="sxs-lookup"><span data-stu-id="8342d-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="8342d-110">Как создать карту?</span><span class="sxs-lookup"><span data-stu-id="8342d-110">How do I create a map?</span></span>

<span data-ttu-id="8342d-111">Вы можете создавать проекты интеграции BizTalk с hello [пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции enterprise hello") для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8342d-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="8342d-112">Затем создайте файл карты интеграции, чтобы визуально сопоставить элементы между двумя XML-файлами схем.</span><span class="sxs-lookup"><span data-stu-id="8342d-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="8342d-113">После создания этого проекта вы получите документ XSLT.</span><span class="sxs-lookup"><span data-stu-id="8342d-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="8342d-114">Добавление карты</span><span class="sxs-lookup"><span data-stu-id="8342d-114">How do I add a map?</span></span>

1. <span data-ttu-id="8342d-115">В hello портал Azure, выберите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="8342d-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="8342d-116">Введите в поле поиска фильтра hello, **интеграции**, а затем выберите **учетные записи службы интеграции** из списка результатов hello.</span><span class="sxs-lookup"><span data-stu-id="8342d-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="8342d-117">Выберите счет интеграции hello место tooadd hello карты.</span><span class="sxs-lookup"><span data-stu-id="8342d-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="8342d-118">Выберите hello **Maps** плитки.</span><span class="sxs-lookup"><span data-stu-id="8342d-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="8342d-119">После открытия колонке hello карты, выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="8342d-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="8342d-120">Введите **имя** карты.</span><span class="sxs-lookup"><span data-stu-id="8342d-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="8342d-121">карта hello tooupload файла, выберите значок папки hello hello правой части hello **карты** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="8342d-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="8342d-122">После завершения процесса передачи hello выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8342d-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="8342d-123">После Azure добавляет учетной записи интеграции tooyour карты hello, выдается сообщение на экране, показывающий, добавлен ли файл карты.</span><span class="sxs-lookup"><span data-stu-id="8342d-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="8342d-124">После получения этого сообщения, выберите hello **Maps** плитку, чтобы можно было просматривать hello вновь добавить карты.</span><span class="sxs-lookup"><span data-stu-id="8342d-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="8342d-125">Изменение карты</span><span class="sxs-lookup"><span data-stu-id="8342d-125">How do I edit a map?</span></span>

<span data-ttu-id="8342d-126">Новый файл карты с hello изменений, которые необходимо передать.</span><span class="sxs-lookup"><span data-stu-id="8342d-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="8342d-127">Можно сначала загрузить hello карты для редактирования.</span><span class="sxs-lookup"><span data-stu-id="8342d-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="8342d-128">tooupload новую карту, которая заменяет существующую карту hello, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8342d-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="8342d-129">Выберите hello **Maps** плитки.</span><span class="sxs-lookup"><span data-stu-id="8342d-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="8342d-130">После открытия колонке hello карты, выберите hello карты, которые должны tooedit.</span><span class="sxs-lookup"><span data-stu-id="8342d-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="8342d-131">На hello **Maps** колонке выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="8342d-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="8342d-132">В средства выбора файлов hello, выберите файл карты hello требуется tooupload, затем выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="8342d-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="8342d-133">Как toodelete карты?</span><span class="sxs-lookup"><span data-stu-id="8342d-133">How toodelete a map?</span></span>

1. <span data-ttu-id="8342d-134">Выберите hello **Maps** плитки.</span><span class="sxs-lookup"><span data-stu-id="8342d-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="8342d-135">После открытия колонке hello карты, выберите требуется toodelete карты hello.</span><span class="sxs-lookup"><span data-stu-id="8342d-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="8342d-136">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="8342d-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="8342d-137">Подтвердите toodelete hello карты.</span><span class="sxs-lookup"><span data-stu-id="8342d-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="8342d-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8342d-138">Next Steps</span></span>
* [<span data-ttu-id="8342d-139">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="8342d-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")  
* [<span data-ttu-id="8342d-140">Узнайте о соглашениях и Пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="8342d-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  
* [<span data-ttu-id="8342d-141">Интеграция Enterprise с преобразованием данных XML</span><span class="sxs-lookup"><span data-stu-id="8342d-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Интеграция Enterprise с преобразованием данных XML")  

