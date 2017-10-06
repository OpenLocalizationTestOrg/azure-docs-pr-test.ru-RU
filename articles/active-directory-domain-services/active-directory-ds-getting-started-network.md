---
title: "Доменные службы Azure Active Directory: начало работы | Документы Майкрософт"
description: "Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)


## <a name="before-you-begin"></a>Перед началом работы
См. слишком[сетевые аспекты для доменных служб Active Directory Azure](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Задача 2. Настройка сетевых параметров
Следующая задача конфигурации Hello является toocreate виртуальной сети Azure и выделенная подсеть внутри него. Вам потребуется включить доменные службы Azure Active Directory в этой подсети. Можно также выбрать существующую виртуальную сеть и создать подсеть hello выделенных в нем.

1. Нажмите кнопку **виртуальная сеть** tooselect виртуальной сети.
2. На hello **виртуальной сети выберите** колонку, вы видите все существующие виртуальные сети. Вы видите только hello виртуальных сетей, принадлежащих toohello группы ресурсов и расположение Azure, выбранные на hello **основы** страницу мастера.

3. Выберите hello виртуальную сеть, в которой следует использовать доменные службы Azure AD. Нажмите кнопку **создать новый**, если вы предпочитаете toocreate новую виртуальную сеть. Для доменных служб Azure Active Directory настоятельно рекомендуется использовать выделенную подсеть. Если вы выберете существующей виртуальной сети, [Создание выделенной подсети с помощью расширения виртуальных сетей hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) , затем выберите этой подсети. 

    ![Выбор виртуальной сети](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Нажмите кнопку **подсети** toopick hello выделенной подсети в этой виртуальной сети, в течение которого tooenable нового управляемого домена. В hello **создать подсеть** , укажите имя для подсети hello и, при необходимости щелкните **ОК** после завершения работы. Например можно создайте подсеть с именем hello «DomainServices», упрощая для других администраторов toounderstand что развернута в подсети hello.

    ![Выберите подсеть внутри виртуальной сети hello](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Рекомендации по выбору подсети**
  > 1. Используйте выделенную подсеть для доменных служб Azure Active Directory. Не развертывайте какой-либо подсети toothis виртуальных машин. Эта конфигурация позволяет tooconfigure сетевой группы безопасности (Nsg) для рабочих нагрузок и виртуальных машин без нарушения управляемого домена. Дополнительные сведения см. в статье [Рекомендации по сетям для доменных служб Azure AD](active-directory-ds-networking.md).
  2. Не устанавливайте hello подсеть шлюза для развертывания доменные службы Azure AD, так как он не является поддерживаемой конфигурацией.
  3. Убедитесь, что достаточно доступное адресное пространство — по крайней мере 3-5 доступных IP-адресов этой подсети hello, которые вы выбрали.
  >

5. Закончив, нажмите кнопку **ОК** toomove на toohello **группу администраторов** на странице приветствия мастера.


## <a name="next-step"></a>Дальнейшие действия
[Задача 3. Настройка административной группы и включение доменных служб Azure AD](active-directory-ds-getting-started-admingroup.md)
