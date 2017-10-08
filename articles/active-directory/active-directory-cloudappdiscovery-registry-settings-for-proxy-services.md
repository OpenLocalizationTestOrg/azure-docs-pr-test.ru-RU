---
title: "Параметры реестра обнаружения приложения для службы прокси-сервера aaaCloud | Документы Microsoft"
description: "Hello цель этой статьи — tooprovide вам hello действия требуется порт hello необходимые tooset tooperform на компьютерах hello агентом hello Cloud App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Параметры реестра Cloud App Discovery для прокси-служб
По умолчанию агент hello Cloud App Discovery — настроенное toouse только hello порты 80 и 443. Если вы планируете установить Cloud App Discovery в среде с прокси-сервер, который использует другой номер порта (не 80 или 443), необходимо tooconfigure вашей toouse агентов этот порт. Настройка Hello основана на раздел реестра.

Hello цель этой статьи — tooprovide вам hello действия требуется порт hello необходимые tooset tooperform на компьютерах hello агентом hello Cloud App Discovery.

**toomodify hello порт, используемый hello компьютера под управлением агента Cloud App Discovery hello, выполните следующие шаги hello.**

1. Откройте редактор реестра hello. <br> ![Выполнить](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Перейдите tooor создать hello следующий раздел реестра: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Создайте новый **мультистроковый** параметр **Ports**. ![Создать](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. tooopen hello **Редактирование мультистроки** диалоговое окно, дважды щелкните значение Ports hello.
5. Hello значение данных в текстовое поле введите следующие значения hello и добавьте все настраиваемые порты, которые используются в вашей организации: <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![Редактирование мультистроки](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. Нажмите кнопку **ОК** tooclose hello **Редактирование мультистроки** диалогового окна.

**Дополнительные ресурсы**

* [Как обнаруживать несанкционированные облачные приложения, которые используются в моей организации](active-directory-cloudappdiscovery-whatis.md) 

