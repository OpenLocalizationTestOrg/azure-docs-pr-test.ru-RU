---
title: "aaaAzure конечных точек службы"
description: "Описание параметров конечной точки службы Azure hello в hello средств Azure для Eclipse."
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
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="7fab8-103">Конечные точки службы Azure</span><span class="sxs-lookup"><span data-stu-id="7fab8-103">Azure Service Endpoints</span></span>
<span data-ttu-id="7fab8-104">Конечные точки службы Azure определяют, является ли приложение развернутой tooand управляется hello глобальной платформе Azure, Azure обслуживается 21Vianet в Китае или на частной платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="7fab8-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="7fab8-105">Hello **конечных точек службы** диалоговом окне можно toospecify, которого вы хотите toouse конечных точек службы.</span><span class="sxs-lookup"><span data-stu-id="7fab8-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="7fab8-106">tooopen hello **конечных точек службы** диалоговое окно, в Eclipse, щелкните **окна**, нажмите кнопку **предпочтения**, разверните **Azure**и нажмите кнопку **Конечных точек службы**.</span><span class="sxs-lookup"><span data-stu-id="7fab8-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="7fab8-107">Параметр hello **активный набор** поле определяет, какие службы Azure, конечные точки, которые будут использоваться для hello Azure проектов в текущей рабочей области.</span><span class="sxs-lookup"><span data-stu-id="7fab8-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="7fab8-108">Hello ниже показан hello **конечных точек службы** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7fab8-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="7fab8-109">конечные точки службы tooset hello</span><span class="sxs-lookup"><span data-stu-id="7fab8-109">tooset hello service endpoints</span></span>
<span data-ttu-id="7fab8-110">В hello **конечных точек службы** диалоговое окно, выполните одно из hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7fab8-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="7fab8-111">Если необходимо, чтобы toouse hello глобальную платформу Azure, из hello **активный набор** раскрывающегося списка выберите **windowsazure.com** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7fab8-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="7fab8-112">Если требуется работать Azure, обслуживаемой 21Vianet в Китае, из hello toouse **активный набор** раскрывающегося списка выберите **windowsazure.cn (China)** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7fab8-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="7fab8-113">Если нужно toouse частной платформы Azure:</span><span class="sxs-lookup"><span data-stu-id="7fab8-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="7fab8-114">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="7fab8-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="7fab8-115">Откроется диалоговое окно, информирующее, что hello **конечных точек службы** диалоговое окно будет закрыто и будет открыт файл наборов настроек hello.</span><span class="sxs-lookup"><span data-stu-id="7fab8-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="7fab8-116">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7fab8-116">Click **OK**.</span></span>

  3. <span data-ttu-id="7fab8-117">В файле preferencesets.xml hello, создайте новый `preferenceset` элемента.</span><span class="sxs-lookup"><span data-stu-id="7fab8-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="7fab8-118">Для этого нового элемента создайте `name`, `blob`, `management`, `portalURL` и `publishsettings` атрибуты и добавить значения для них, которые соответствуют tooyour частной платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="7fab8-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="7fab8-119">Можно использовать hello значения, предоставленные для существующих hello `preferenceset` элементы как шаблоны.</span><span class="sxs-lookup"><span data-stu-id="7fab8-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="7fab8-120">**Примечание**: hello значение, используемое для hello `blob` атрибут должен содержать текст hello «BLOB-объект» в URL-АДРЕСЕ hello.</span><span class="sxs-lookup"><span data-stu-id="7fab8-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="7fab8-121">Сохраните и закройте файл preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="7fab8-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="7fab8-122">Снова откройте hello **конечных точек службы** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7fab8-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="7fab8-123">Из hello **активный набор** раскрывающегося списка выберите hello активный набор создан и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7fab8-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="7fab8-124">После создания вашей частной платформе Azure `preferenceset` элемента, можно изменить значения, назначенные tooit hello, щелкнув hello **изменить** кнопку в hello **конечной точки службы** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7fab8-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="7fab8-125">Кроме того, при необходимости вы можете создать несколько элементов `preferenceset` частной платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="7fab8-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="7fab8-126">См. также</span><span class="sxs-lookup"><span data-stu-id="7fab8-126">See Also</span></span>
<span data-ttu-id="7fab8-127">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7fab8-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="7fab8-128">[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7fab8-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="7fab8-129">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7fab8-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="7fab8-130">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="7fab8-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
