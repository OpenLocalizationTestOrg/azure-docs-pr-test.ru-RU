---
title: "aaaUnderstanding DNS-сервер в стек Azure | Документы Microsoft"
description: "Основные сведения о DNS функций и возможностей в стек Azure"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: f60128cf98af8e98ac2bc87172b54132ed06cd8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-idns-for-azure-stack"></a>Общие сведения о имена IDN для стек Azure
================================

имена IDN — это функция Azure стека, который позволяет вам tooresolve внешних DNS-имен (например, http://www.bing.com).
Она также позволяет имена tooregister внутреннюю виртуальную сеть. Таким образом, можно разрешить виртуальных машин на hello одной виртуальной сети по имени, а не IP-адресов, без необходимости tooprovide пользовательские записи DNS-сервера.

Это то, что всегда было существует в Azure, но она доступна в Windows Server 2016 и стек Azure слишком.

## <a name="what-does-idns-do"></a>Каково предназначение IDN.
Имена IDN в стек Azure позволяет получить hello следующие возможности, без необходимости toospecify пользовательские записи DNS-сервера.

* Общие службы разрешения имен DNS для рабочих нагрузок клиентов.
* Принудительное службы DNS для разрешения имен и регистрация DNS в виртуальную сеть клиента hello.
* Служба рекурсивный DNS для разрешения имен Интернета из виртуальных машин клиентов. Клиенты больше не нужна toospecify пользовательские DNS записи tooresolve имен Интернета (например, www.bing.com).

По-прежнему можно подключить собственный DNS-сервера и использовать пользовательские DNS-серверы, если необходимо. Но теперь только имена DNS Интернета могут tooresolve toobe и сможете Здравствуйте, tooconnect tooother виртуальных машин в одной виртуальной сети, не требуется toospecify ничего, и он будет работать.

## <a name="what-does-idns-not-do"></a>Что делает имена IDN не?
Какие имена IDN не позволит toodo является создание записи DNS для имени, которое можно привести вне hello в виртуальной сети.

В Azure у вас hello указания метка DNS-имени, которое может быть связано с общедоступный IP-адрес. Можно выбрать метки hello (префикс), но Azure выбирает hello суффикс, который основан на hello регион, в котором можно создавать hello общедоступный IP-адрес.

![Метка снимок экрана DNS-имени](media/azure-stack-understanding-dns-in-tp2/image3.png)

Hello рисунке выше Azure создаст» «запись в DNS для метка DNS-имени hello, указанные в разделе зоны hello **westus.cloudapp.azure.com**. Суффикс префикс и hello вместе образуют полное доменное имя (FQDN), можно разрешить в любом месте на hello общедоступный Интернет.

Azure стека только поддерживает имена IDN регистрация внутреннее имя, поэтому его нельзя hello следующие.

* Создание записи DNS в существующей размещенной зоны DNS (например, local.azurestack.external).
* Создайте зону DNS (например, Contoso.com).
* Создайте запись в создаваемую зону DNS.
* Поддерживает покупку hello доменных имен.

