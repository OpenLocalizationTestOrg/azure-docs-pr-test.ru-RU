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
# <a name="azure-service-endpoints"></a>Конечные точки службы Azure
Конечные точки службы Azure определяют, является ли приложение развернутой tooand управляется hello глобальной платформе Azure, Azure обслуживается 21Vianet в Китае или на частной платформе Azure. Hello **конечных точек службы** диалоговом окне можно toospecify, которого вы хотите toouse конечных точек службы. tooopen hello **конечных точек службы** диалоговое окно, в Eclipse, щелкните **окна**, нажмите кнопку **предпочтения**, разверните **Azure**и нажмите кнопку **Конечных точек службы**. Параметр hello **активный набор** поле определяет, какие службы Azure, конечные точки, которые будут использоваться для hello Azure проектов в текущей рабочей области.

Hello ниже показан hello **конечных точек службы** диалогового окна.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>конечные точки службы tooset hello
В hello **конечных точек службы** диалоговое окно, выполните одно из hello, следующие действия:

* Если необходимо, чтобы toouse hello глобальную платформу Azure, из hello **активный набор** раскрывающегося списка выберите **windowsazure.com** и нажмите кнопку **ОК**.

* Если требуется работать Azure, обслуживаемой 21Vianet в Китае, из hello toouse **активный набор** раскрывающегося списка выберите **windowsazure.cn (China)** и нажмите кнопку **ОК**.

* Если нужно toouse частной платформы Azure:

  1. Нажмите кнопку **Изменить**.

  2. Откроется диалоговое окно, информирующее, что hello **конечных точек службы** диалоговое окно будет закрыто и будет открыт файл наборов настроек hello. Нажмите кнопку **ОК**.

  3. В файле preferencesets.xml hello, создайте новый `preferenceset` элемента. Для этого нового элемента создайте `name`, `blob`, `management`, `portalURL` и `publishsettings` атрибуты и добавить значения для них, которые соответствуют tooyour частной платформы Azure. Можно использовать hello значения, предоставленные для существующих hello `preferenceset` элементы как шаблоны. **Примечание**: hello значение, используемое для hello `blob` атрибут должен содержать текст hello «BLOB-объект» в URL-АДРЕСЕ hello.

  4. Сохраните и закройте файл preferencesets.xml.

  5. Снова откройте hello **конечных точек службы** диалогового окна.

  6. Из hello **активный набор** раскрывающегося списка выберите hello активный набор создан и нажмите кнопку **ОК**.

  7. После создания вашей частной платформе Azure `preferenceset` элемента, можно изменить значения, назначенные tooit hello, щелкнув hello **изменить** кнопку в hello **конечной точки службы** диалогового окна. Кроме того, при необходимости вы можете создать несколько элементов `preferenceset` частной платформы Azure.

## <a name="see-also"></a>См. также
[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]

[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
