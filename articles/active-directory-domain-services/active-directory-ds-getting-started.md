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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Включение Azure доменных служб Active Directory с помощью hello портал Azure (Предварительная версия)
В этой статье показано, как tooenable Active Directory домена служб Azure (Azure AD DS) с помощью hello портал Azure.


toolaunch hello **включить доменные службы Azure AD** мастера, завершенной hello, следующие шаги:

1. Go toohello [портал Azure](https://portal.azure.com).
2. В левой области hello, нажмите кнопку **New**.
3. В hello **New** колонки, тип **доменных служб** в строку поиска hello.

    ![Поиск доменных служб](./media/getting-started/search-domain-services.png)

4. Нажмите кнопку tooselect **доменные службы Azure AD** hello списке вариантов поиска. На hello **доменные службы Azure AD** колонка, щелкните hello **создать** кнопки.

    ![Колонка "Доменные службы"](./media/getting-started/domain-services-blade.png)

5. Hello **включить доменные службы Azure AD** запустить мастер.


## <a name="task-1-configure-basic-settings"></a>Задача 1. Настройка основных параметров
В hello **основы** страница приветствия мастера, можно указать hello DNS-имя домена для домена управляемого hello. Можно также выбрать группу ресурсов hello и расположение Azure toowhich hello управляемого домена следует развернуть.

![Настройка основных сведений](./media/getting-started/domain-services-blade-basics.png)

1. Выберите hello **DNS-имя домена** управляемого домена.

   * имя домена по умолчанию Hello hello каталога (с **. onmicrosoft.com** суффикс) по умолчанию.

   * Можно также ввести пользовательское доменное имя. В этом примере — hello пользовательское имя домена *contoso100.com*.

     > [!WARNING]
     > Hello префикс к имени домена (например, *contoso100* в hello *contoso100.com* доменное имя) должно содержать не более 15 символов. Невозможно создать управляемый домен с префиксом длиннее 15 символов.
     >
     >

2. Убедитесь, что hello DNS-имя домена, выбранный для hello управляемого домена еще не существует в виртуальной сети hello. В частности, убедитесь в следующем:

   * Уже имеется домен с hello же DNS-имя домена в виртуальной сети hello.

   * Hello виртуальной сети, где планируется tooenable hello управляемый домен имеет VPN-подключение к локальной сети. В этом случае убедитесь, не нужно, чтобы домен с hello же DNS-имя домена в локальной сети.

   * У вас есть существующей облачной службы с таким именем hello виртуальной сети.

3. Выберите hello **тип виртуальной сети**. По умолчанию hello **диспетчера ресурсов** выбран тип виртуальной сети. Мы рекомендуем использовать этот тип виртуальной сети для всех создаваемых управляемых доменов.

4. Выберите hello Azure **подписки** хотите toocreate hello управляемый домен.

5. Выберите hello **группы ресурсов** должны принадлежать к управляемому домену toowhich hello. Вы можете либо hello **создать новый** или **использовать существующие** группы ресурсов hello tooselect параметры.

6. Выберите hello Azure **расположение** в какой hello следует создать управляемый домен. На hello **сети** страница приветствия мастера вы видите только виртуальные сети, которые принадлежат toohello расположение выбора.

7. Закончив, нажмите кнопку **ОК** toomove на toohello **сети** на странице приветствия мастера.


## <a name="next-step"></a>Дальнейшие действия
[Задача 2. Настройка сетевых параметров](active-directory-ds-getting-started-network.md)
