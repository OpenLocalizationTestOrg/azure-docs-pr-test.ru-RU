---
title: "aaaManage виртуальных машин с помощью hello обозреватель Azure для IntelliJ | Документы Microsoft"
description: "Узнайте, как toomanage виртуальных машин Azure с помощью hello обозреватель Azure для IntelliJ."
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a>Управление виртуальными машинами с помощью hello обозреватель Azure для IntelliJ

Hello Explorer Azure, который является частью набора средств Azure для IntelliJ hello, предоставляет разработчикам Java с помощью решения для использования в управлении виртуальными машинами свою учетную запись в Azure из внутри hello IntelliJ интегрированной среды разработки (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Создание виртуальной машины в IntelliJ

toocreate виртуальной машины с помощью обозревателя Azure hello hello следующие: 

1. Войдите в tooyour учетная запись Azure с помощью действия hello в hello [входа в инструкции для hello Azure Toolkit для IntelliJ] статьи.

2. В hello **обозреватель Azure** , разверните узел hello **Azure** узел, щелкните правой кнопкой мыши **виртуальные машины**и нажмите кнопку **создания виртуальной Машины**. 

   ![Hello команда создания виртуальной Машины][CR01]  
    Hello **Создание новой виртуальной машины** откроется мастер.

3. В hello **выберите подписку** окно, выберите подписку и нажмите кнопку **Далее**. 

   ![Выберите окно подписки Hello][CR02]

4. В hello **выберите образ виртуальной машины** окно, введите hello следующую информацию:

   * **Расположение**: указывает расположение для создания виртуальной машины (например, *Западная часть США*). 

   * **Recommended Image** (Рекомендуемый образ): указывает, что вы выберете образ из сокращенного списка часто используемых образов.

   * **Пользовательский образ**: Указывает, будет выбрать пользовательский образ, предоставляя hello следующую информацию:

      * **Издатель**: указывает издателю hello hello образа, который будет использоваться для виртуальной машины (например, *Microsoft*).

      * **Предложить**: указывает hello виртуальной машины предложения toouse hello выбранного издателя (например, *JDK*).

      * **SKU**: указывает toouse единица складского учета hello из выбранного предложения hello (например, *JDK_8*).

      * **Версия #**: Указывает, какую версию выбранного hello SKU toouse.

   ![Hello выбора образа виртуальной машины окна][CR03]

5. Щелкните **Далее**. 

6. В hello **основные параметры виртуальной машины** окно, введите hello следующую информацию:

   * **Имя виртуальной машины**: Указывает имя hello для новой виртуальной машины, которой должно начинаться с буквы и содержать только буквы, цифры и дефисы.

   * **Размер**: указывает hello количество ядер и памяти tooallocate для виртуальной машины.

   * **Имя пользователя**: указывает hello toocreate учетной записи администратора для управления виртуальной машины.

   * **Пароль** и **Подтверждение**: указывает hello пароль для учетной записи администратора.

   ![окно Hello основные параметры виртуальной машины][CR04]

7. Щелкните **Далее**. 

8. В hello **связанные ресурсы** окно, введите hello следующую информацию:

   * **Группа ресурсов**: указывает hello группу ресурсов для виртуальной машины. Выберите один из следующих вариантов hello.
      * **Создать новый**: Указывает, что toocreate новую группу ресурсов.
      * **Использовать существующие**: Указывает, что tooselect из списка групп ресурсов, которые связаны с учетной записью Azure.

       ![окно Hello связанные ресурсы][CR07]

   * **Учетная запись хранения**: указывает hello toouse учетной записи хранилища для хранения виртуальной машины. Вы можете выбрать имеющуюся учетную запись хранения или создать ее. При выборе **создать новый**, появится следующая диалоговое окно приветствия:

      ![Создание учетной записи хранилища Hello-диалоговое окно][CR05]

   * **Виртуальная сеть** и **подсети**: задает hello виртуальной сети и подсети, в которой будут подключаться к виртуальной машине. Вы можете выбрать имеющуюся сеть и подсеть или создать их. При выборе **создать новый**, появится следующая диалоговое окно приветствия:

      ![Создание виртуальной сети Hello-диалоговое окно][CR06]

   * **Общедоступный IP-адрес**: указывает внешний IP-адрес для виртуальной машины. Вы можете toocreate новый IP-адрес или, если виртуальная машина не будет иметь общедоступный IP-адрес, можно выбрать **(нет)**. 

   * **Группа безопасности сети**: определяет необязательный брандмауэр для виртуальной машины. Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр. 

   * **Группа доступности**: определяет необязательную группу доступности, в которую может входить виртуальная машина. Можно выбрать существующий набор доступности, создать новую группу доступности или, если виртуальная машина не будет принадлежать tooan набора доступности, выберите **(нет)**.

9. Нажмите кнопку **Готово**  
    В окне инструментов обозревателя Azure hello появляется на новую виртуальную машину. 

   ![Новая виртуальная машина в Azure обозревателя hello][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Перезапуск виртуальной машины в IntelliJ

toorestart виртуальной машины с помощью обозревателя Azure hello в IntelliJ, hello следующие:

1. В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **перезапустите**.

   ![команды перезапуска виртуальной машины Hello][RE01]

2. В окне подтверждения hello, щелкните **Да**. 

   ![Hello перезагрузите окно подтверждения виртуальной машины][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Завершение работы виртуальной машины в IntelliJ

tooshut вниз работающей виртуальной машины с помощью обозревателя Azure hello в IntelliJ, hello следующие:

1. В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **завершение работы**.

   ![Здравствуйте, команда завершения работы виртуальной машины][SH01]

2. В окне подтверждения hello, щелкните **Да**. 

   ![Завершите работу виртуальной машины окно подтверждения Hello][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Удаление виртуальной машины в IntelliJ

toodelete виртуальной машины с помощью обозревателя Azure hello в IntelliJ, hello следующие:

1. В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **удалить**.

   ![команда удаления виртуальной машины Hello][DE01]

2. В окне подтверждения hello, щелкните **Да**. 

   ![Hello удалить окно подтверждения виртуальной машины][DE02]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об Azure размеры виртуальных машин и ценах см. в разделе hello следующие ресурсы:

* Размеры виртуальных машин Azure
  * [Размеры виртуальных машин Windows в Azure]
  * [Размеры виртуальных машин Linux в Azure]
* Цены на виртуальные машины Azure
  * [Цены на виртуальные машины Windows]
  * [Цены на виртуальные машины Linux]

Дополнительные сведения о hello наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:

* [Набор средств Azure для Eclipse]
  * [Новые возможности средств Azure для Eclipse hello]
  * [Установка средств Azure для Eclipse hello]
  * [Инструкции вход для hello средств Azure для Eclipse]
  * [Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]
* [Набор средств Azure для IntelliJ]
  * [Новые возможности средств Azure для IntelliJ hello]
  * [Установка hello Azure Toolkit для IntelliJ]
  * [входа в инструкции для hello Azure Toolkit для IntelliJ]
  * [Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]

Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции вход для hello средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[входа в инструкции для hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Цены на виртуальные машины Windows]: /pricing/details/virtual-machines/windows/
[Цены на виртуальные машины Linux]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
