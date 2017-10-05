---
title: "Управление учетными записями хранения с помощью Azure Explorer для Eclipse | Документы Майкрософт"
description: "Вы можете узнать, как управлять учетными записями хранения Azure с помощью Azure Explorer для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 5b3014b5aca368be8ea46863c83665abde10fed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a>Управление учетными записями хранения с помощью Azure Explorer для Eclipse

Azure Explorer, входящий в состав набора средств Azure для Eclipse, предоставляет разработчикам на Java удобное решение для управления учетными записями хранения в их учетной записи Azure из интегрированной среды разработки Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a>Создание учетной записи хранения в Eclipse

Чтобы создать учетную запись хранения с помощью Azure Explorer, сделайте следующее:

1. Войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для Eclipse].

2. В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши элемент **Учетные записи хранения** и выберите **Создать учетную запись хранения**.

   ![Команда "Создать учетную запись хранения"][CS01]

3. В диалоговом окне **Создание учетной записи хранения** укажите следующие параметры.

   ![Диалоговое окно "Создание учетной записи хранения"][CS02]

   * **Имя**: указывает имя для новой учетной записи хранения.

   * **Подписка**: указывает подписку Azure, которую нужно использовать для новой учетной записи хранения.

   * **Группа ресурсов**: указывает группу ресурсов для виртуальной машины. Выберите один из следующих вариантов:
      * **Создать**: указывает, что нужно создать группу ресурсов.
      * **Использовать существующий**: указывает, что вы выберете группу ресурсов, связанную с учетной записью Azure.

   * **Регион**: указывает расположение для создания учетной записи хранения, например "западная часть США".

   * **Тип учетной записи**: указывает тип создаваемой учетной записи хранения (например, "хранилище BLOB-объектов"). Дополнительные сведения см. в статье [Об учетных записях хранения Azure].

   * **Производительность**: определяет, какое предложение по учетной записи хранения выбранного издателя нужно использовать (например, "Премиум"). Дополнительные сведения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure].

   * **Репликация**: указывает репликацию для учетной записи хранения (например, "избыточная в пределах зоны"). Дополнительные сведения см. в статье [Репликация службы хранилища Azure].

4. Указав все перечисленные выше параметры, нажмите кнопку **Создать**.

## <a name="create-a-storage-container-in-eclipse"></a>Создание контейнера хранилища в Eclipse

Чтобы создать контейнер хранилища с помощью Azure Explorer, сделайте следующее:

1. В представлении **Azure Explorer** щелкните правой кнопкой мыши учетную запись хранения, для которой нужно создать контейнер, а затем нажмите кнопку **Создать контейнер BLOB-объектов**.

   ![Команда "Создать контейнер BLOB-объектов"][CC01]

2. В диалоговом окне **Создание контейнера BLOB-объектов** укажите имя для своего контейнера и нажмите кнопку **ОК**. Дополнительные сведения об именовании контейнеров хранилища см. в статье [Naming and Referencing Containers, Blobs, and Metadata] (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них).

   ![Диалоговое окно "Создание контейнера BLOB-объектов"][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a>Удаление контейнера хранилища в Eclipse

Чтобы удалить контейнер хранилища с помощью Azure Explorer, сделайте следующее:

1. В представлении **Azure Explorer** щелкните правой кнопкой мыши контейнер хранилища и выберите **Удалить**.

   ![Команда "Удалить контейнер хранилища"][DC01]

2. В диалоговом окне подтверждения нажмите кнопку **ОК**.

   ![Окно подтверждения удаления контейнера хранилища][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a>Удаление учетной записи хранения в Eclipse

Чтобы удалить учетную запись хранения с помощью Azure Explorer, сделайте следующее:

1. В представлении **Azure Explorer** щелкните правой кнопкой мыши учетную запись хранения и выберите пункт **Удалить**.

   ![Команда "Удалить учетную запись хранения"][DS01]

2. В диалоговом окне подтверждения нажмите кнопку **ОК**.

   ![Окно подтверждения удаления учетной записи хранения][DS02]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об учетных записях хранения, размерах и ценах см. в следующих ресурсах:

* [Введение в службу хранилища Microsoft Azure]
* [Об учетных записях хранения Azure]
* Размеры учетных записей хранения Azure
  * [Размеры учетных записей хранения Windows в Azure]
  * [Размеры учетных записей хранения Linux в Azure]
* Цены на учетные записи хранения Azure
  * [Windows storage-account pricing] (Цены на учетные записи хранения Windows)
  * [Linux storage-account pricing] (Цены на учетные записи хранения Linux)

Дополнительные сведения о наборах средств Azure для Java IDE см. в следующих ресурсах:

* [Набор средств Azure для Eclipse]
  * [Новые возможности набора средств Azure для Eclipse]
  * [Установка набора средств Azure для Eclipse]
  * [Инструкции по входу для набора средств Azure для Eclipse]
  * [Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]
* [Набор средств Azure для IntelliJ]
  * [Новые возможности набора средств Azure для IntelliJ]
  * [Установка набора средств Azure для IntelliJ]
  * [Инструкции по входу для набора средств Azure для IntelliJ]
  * [Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]

Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Установка набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции по входу для набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[Введение в службу хранилища Microsoft Azure]: /azure/storage/storage-introduction
[Об учетных записях хранения Azure]: /azure/storage/storage-create-storage-account
[Репликация службы хранилища Azure]: /azure/storage/storage-redundancy
[Целевые показатели масштабируемости и производительности службы хранилища Azure]: /azure/storage/storage-scalability-targets
[Naming and Referencing Containers, Blobs, and Metadata]: http://go.microsoft.com/fwlink/?LinkId=255555 (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них)

[Размеры учетных записей хранения Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры учетных записей хранения Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/ (Цены на учетные записи хранения Windows)
[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/ (Цены на учетные записи хранения Linux)

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
