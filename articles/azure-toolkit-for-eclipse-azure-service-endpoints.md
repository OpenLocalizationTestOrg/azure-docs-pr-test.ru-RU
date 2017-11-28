---
title: "Конечные точки службы Azure"
description: "Описываются параметры конечных точек службы Azure в наборе средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="b1c7d-103">Конечные точки службы Azure</span><span class="sxs-lookup"><span data-stu-id="b1c7d-103">Azure Service Endpoints</span></span>
<span data-ttu-id="b1c7d-104">Конечные точки службы определяют, где будет развернуто приложение и где будет управляться: на глобальной платформе Azure, на Azure под управлением 21Vianet в Китае или на частной платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="b1c7d-105">Диалоговое окно **Конечные точки службы** позволяет указать, какие конечные точки службы вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="b1c7d-106">Чтобы открыть диалоговое окно **Конечные точки службы** в Eclipse, щелкните **Окно**, **Настройки**, разверните **Azure** и выберите **Конечные точки службы**.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="b1c7d-107">Указав значение в поле **Active Set** (Активный набор), можно определить, какие конечные точки службы Azure будут использоваться для проектов Azure в текущей рабочей области.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="b1c7d-108">Ниже приведено диалоговое окно **Конечные точки службы** .</span><span class="sxs-lookup"><span data-stu-id="b1c7d-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="b1c7d-109">Задание конечных точек службы</span><span class="sxs-lookup"><span data-stu-id="b1c7d-109">To set the service endpoints</span></span>
<span data-ttu-id="b1c7d-110">В диалоговом окне **Конечные точки службы** выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="b1c7d-111">Если вы хотите использовать глобальную платформу Azure, в раскрывающемся списке **Active Set** (Активный набор) выберите **windowsazure.com** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="b1c7d-112">Если вы хотите использовать платформу Azure под управлением 21Vianet в Китае, в раскрывающемся списке **Active Set** (Активный набор) выберите **windowsazure.cn (China)** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="b1c7d-113">Если вы хотите использовать частную платформу Azure:</span><span class="sxs-lookup"><span data-stu-id="b1c7d-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="b1c7d-114">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="b1c7d-115">Открывается диалоговое окно с информацией о том, что диалоговое окно **Конечные точки службы** будет закрыто и будет открыт файл наборов настроек.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="b1c7d-116">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-116">Click **OK**.</span></span>

  3. <span data-ttu-id="b1c7d-117">В файле preferencesets.xml создайте новый элемент `preferenceset`.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="b1c7d-118">Для этого нового элемента создайте атрибуты `name`, `blob`, `management`, `portalURL` и `publishsettings` и добавьте для них значения, соответствующие вашей частной платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="b1c7d-119">Вы можете использовать значения, предоставленные для существующих элементов `preferenceset`, в качестве шаблона.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="b1c7d-120">**Примечание.** Используемое для атрибута `blob` значение должно содержать текст blob в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="b1c7d-121">Сохраните и закройте файл preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="b1c7d-122">Снова откройте диалоговое окно **Конечные точки службы** .</span><span class="sxs-lookup"><span data-stu-id="b1c7d-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="b1c7d-123">В раскрывающемся списке **Active Set** (Активный набор) выберите созданный активный набор и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="b1c7d-124">После создания элемента `preferenceset` частной платформы Azure можно изменить назначенные ему значения, нажав кнопку **Изменить** в диалоговом окне **Конечные точки службы**.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="b1c7d-125">Кроме того, при необходимости вы можете создать несколько элементов `preferenceset` частной платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c7d-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="b1c7d-126">См. также</span><span class="sxs-lookup"><span data-stu-id="b1c7d-126">See Also</span></span>
<span data-ttu-id="b1c7d-127">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b1c7d-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="b1c7d-128">[Установка набора средств Azure для Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b1c7d-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="b1c7d-129">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b1c7d-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="b1c7d-130">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="b1c7d-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
