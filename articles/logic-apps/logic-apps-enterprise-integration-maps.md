---
title: "Преобразование XML с помощью карт XSLT — Azure Logic Apps | Документация Майкрософт"
description: "Добавление карт XSLT для преобразования XML-данных с помощью Azure Logic Apps и пакета интеграции Enterprise"
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
ms.openlocfilehash: 4445a84a6c6425110e7d705019a28b5cc5447046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="42393-103">Добавление карт для преобразования данных XML</span><span class="sxs-lookup"><span data-stu-id="42393-103">Add maps for XML data transform</span></span>

<span data-ttu-id="42393-104">В интеграции Enterprise используются карты для преобразования данных XML из одного формата в другой.</span><span class="sxs-lookup"><span data-stu-id="42393-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="42393-105">Карта — это документ XML, который определяет, какие данные в документе должны быть преобразованы в другой формат.</span><span class="sxs-lookup"><span data-stu-id="42393-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="42393-106">Для чего используются карты?</span><span class="sxs-lookup"><span data-stu-id="42393-106">Why use maps?</span></span>

<span data-ttu-id="42393-107">Предположим, что вы регулярно получаете заказы или счета от клиентов "бизнес — бизнес", которые используют формат даты ГГГММДД.</span><span class="sxs-lookup"><span data-stu-id="42393-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="42393-108">Однако в вашей организации даты хранятся в формате ММДДГГГ.</span><span class="sxs-lookup"><span data-stu-id="42393-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="42393-109">Вы можете использовать карту, чтобы *преобразовать* формат даты ГГГММДД в ММДДГГГ перед сохранением сведений о заказе или счете в базе данных деловой активности клиента.</span><span class="sxs-lookup"><span data-stu-id="42393-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="42393-110">Как создать карту?</span><span class="sxs-lookup"><span data-stu-id="42393-110">How do I create a map?</span></span>

<span data-ttu-id="42393-111">Вы можете создать проекты интеграции BizTalk с помощью [пакета интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Узнайте о пакете интеграции Enterprise") для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="42393-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="42393-112">Затем создайте файл карты интеграции, чтобы визуально сопоставить элементы между двумя XML-файлами схем.</span><span class="sxs-lookup"><span data-stu-id="42393-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="42393-113">После создания этого проекта вы получите документ XSLT.</span><span class="sxs-lookup"><span data-stu-id="42393-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="42393-114">Добавление карты</span><span class="sxs-lookup"><span data-stu-id="42393-114">How do I add a map?</span></span>

1. <span data-ttu-id="42393-115">На портале Azure щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="42393-115">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="42393-116">Введите **интеграция** в поле фильтра поиска, затем выберите **Учетные записи интеграции** в списке результатов.</span><span class="sxs-lookup"><span data-stu-id="42393-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="42393-117">Выберите учетную запись интеграции, в которую необходимо добавить карту.</span><span class="sxs-lookup"><span data-stu-id="42393-117">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="42393-118">Выберите плитку **Карты** .</span><span class="sxs-lookup"><span data-stu-id="42393-118">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="42393-119">Когда откроется колонка карт, нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="42393-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="42393-120">Введите **имя** карты.</span><span class="sxs-lookup"><span data-stu-id="42393-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="42393-121">Чтобы передать файл карты, щелкните значок папки в правой части текстового поля **Карта**.</span><span class="sxs-lookup"><span data-stu-id="42393-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="42393-122">После завершения передачи нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="42393-122">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="42393-123">Когда Azure добавит карту в вашу учетную запись интеграции, вы увидите сообщение о том, что файл добавлен или не добавлен.</span><span class="sxs-lookup"><span data-stu-id="42393-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="42393-124">Получив это сообщение, выберите плитку **Карты**, чтобы просмотреть добавленную карту.</span><span class="sxs-lookup"><span data-stu-id="42393-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="42393-125">Изменение карты</span><span class="sxs-lookup"><span data-stu-id="42393-125">How do I edit a map?</span></span>

<span data-ttu-id="42393-126">Передайте новый файл карты с нужными изменениями.</span><span class="sxs-lookup"><span data-stu-id="42393-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="42393-127">Сначала можно загрузить карту и изменить ее.</span><span class="sxs-lookup"><span data-stu-id="42393-127">You can first download the map for editing.</span></span>

<span data-ttu-id="42393-128">Чтобы отправить новую карту, которая заменит существующую, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="42393-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="42393-129">Выберите плитку **Карты** .</span><span class="sxs-lookup"><span data-stu-id="42393-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="42393-130">В открывшейся колонке карт выберите карту, которую вы хотите изменить.</span><span class="sxs-lookup"><span data-stu-id="42393-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="42393-131">В колонке **Карты** нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="42393-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="42393-132">В окне выбора файлов выберите файл карты, который требуется отправить, а затем нажмите кнопу **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="42393-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="42393-133">Как удалить карту?</span><span class="sxs-lookup"><span data-stu-id="42393-133">How to delete a map?</span></span>

1. <span data-ttu-id="42393-134">Выберите плитку **Карты** .</span><span class="sxs-lookup"><span data-stu-id="42393-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="42393-135">В открывшейся колонке карт выберите карту, которую вы хотите удалить.</span><span class="sxs-lookup"><span data-stu-id="42393-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="42393-136">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="42393-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="42393-137">Подтвердите, что вы действительно хотите удалить карту.</span><span class="sxs-lookup"><span data-stu-id="42393-137">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="42393-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42393-138">Next Steps</span></span>
* [<span data-ttu-id="42393-139">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="42393-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise")  
* [<span data-ttu-id="42393-140">Узнайте о соглашениях и Пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="42393-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  
* [<span data-ttu-id="42393-141">Интеграция Enterprise с преобразованием данных XML</span><span class="sxs-lookup"><span data-stu-id="42393-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Интеграция Enterprise с преобразованием данных XML")  

