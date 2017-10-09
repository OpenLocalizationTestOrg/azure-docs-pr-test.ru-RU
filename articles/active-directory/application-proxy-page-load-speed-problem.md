---
title: "aaaAn приложения прокси приложения занимает слишком длинный tooload | Документы Microsoft"
description: "Устранение неполадок производительности загрузки страницы с помощью hello прокси приложения Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>Слишком длинный tooload принимает приложения прокси приложения

В этой статье помогут toounderstand, почему приложение прокси приложения Azure AD может потребоваться tooload много времени и что можно сделать tooresolve эту проблему.

## <a name="overview"></a>Обзор
При работе приложения, но вы видите большие задержки, может возникнуть некоторые небольшие настройки топологии сети, можно учитывать скорость tooimprove hello. Для оценки различных топологий, в разделе hello [сети вопросы документа](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Если эти рекомендации не помогают, других советов по настройке производительности у нас, к сожалению, пока нет. Как службы прокси приложения hello разворачивается toomore центрах обработки данных, которые могут быть более подробно tooyou, можно запустить toosee улучшена задержки напрямую. Центрирует toosee hello полный список данных Azure, вы увидите hello [задержки тестовой страницы](http://www.azurespeed.com/Azure/Latency). 

Hello центрах обработки данных с помощью службы прокси приложения hello можно найти с помощью hello [средство тестирования порты соединитель](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Отзывы о расположениях центров обработки данных для прокси приложения 
Может быть центрах обработки данных Azure, которые еще не включайте прокси приложения, но улучшение значительные задержки tooa привели бы. расположение центра обработки данных Hello < aadapfeedback@microsoft.com > , мы планируем можно использовать tooplan ваш отзыв.

Мы работаем над некоторые дополнительные возможности, повышающие hello задержку для клиентов, которые в настоящее время доступны long задержки и быть убедиться, что документация tooshare после доступных.

## <a name="next-steps"></a>Дальнейшие действия
[Работа с имеющимися локальными прокси-серверами](application-proxy-working-with-proxy-servers.md)
