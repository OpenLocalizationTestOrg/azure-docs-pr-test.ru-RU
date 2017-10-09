---
title: "aaaDisplaying содержимого Javadoc в Eclipse для hello пакета библиотек Azure для Java"
description: "Как toodisplay hello содержимого Javadoc для библиотек Azure hello в Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>Отображение в Eclipse содержимого Javadoc для пакета библиотек Azure для Java hello
Hello содержимого Javadoc для библиотек Azure для Java hello можно просмотреть в среде Eclipse, связав toohello содержимого Javadoc hello библиотек Azure для Java. Hello следующие шаги показывают, как toouse эту возможность в Eclipse.

Подразумевается, что вы уже добавили hello библиотеки Azure для Java tooyour построения пути.

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay содержимого Javadoc в Eclipse для hello библиотек Azure для Java
* В обозревателе проектов Eclipse в hello **ссылки на библиотеки** Привет открыть контекстное меню для библиотеки Azure для Java JAR hello, раздела проекта. Например **microsoft windowsazure-api 0.1.0.jar** (номер версии hello могут быть различия, зависящие от версии установки).

* Щелкните **Свойства**.

* В рамках hello **свойства** диалоговом окне приветствия левой панели, нажмите кнопку **расположение Javadoc**. Hello **расположение Javadoc** отображается диалоговое окно.

* Вы можете указать **Javadoc URL** (URL-адрес Javadoc) или **Javadoc in archive** (Javadoc в архиве) в соответствующих полях.

   * При выборе toospecify **URL-адрес Javadoc**, используйте hello URL-адреса, такие как **http://dl.windowsazure.com/javadoc** или **http://dl.windowsazure.com/storage/javadoc**.

   * При выборе toouse **Javadoc в архиве**, можно указать внешний файл или файл рабочей области.

   Выберите нужный вариант и при необходимости выполните переход или проверку. Hello следующий пример связывает hello библиотек Azure для Java с hello, соответствующий JAR-ФАЙЛ Javadoc, был загружен локально tooa папку с именем **c:\MyAzureJARs**.

   ![][ic553487]

* *Необязательно*: щелкните **Проверить**. Здесь могут отображаться потенциальные проблемы с JAR-ФАЙЛ Javadoc hello.

* Нажмите кнопку **ОК**.

После связывания с библиотекой hello hello содержимое Javadoc должно отображаться в Eclipse IDE. Например если `blob` определяется типа `CloudBlockBlob` в вашем коде hello ниже приведен пример содержимого Javadoc, которое появляется при вводе `blob.acquireLease` в коде:

![][ic553488]

## <a name="see-also"></a>См. также
[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]

[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
