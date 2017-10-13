---
title: "Публикация содержимого на портале Azure | Документация Майкрософт"
description: "В этом руководстве пошагово описано, как публиковать содержимое на портале Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 6759d3f49e15a3b01022df318a83563ad6bd859f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="publish-content-in-the-azure-portal"></a>Публикация содержимого на портале Azure
> [!div class="op_single_selector"]
> * [Портал](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Обзор
> [!NOTE]
> Для работы с этим учебником требуется учетная запись Azure. Дополнительные сведения см. на странице с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Чтобы предоставить пользователю URL-адрес, который можно использовать для потоковой передачи или загрузки содержимого, сначала опубликуйте ресурс, создав указатель. Указатели предоставляют доступ к файлам ресурсов. Службы мультимедиа Azure поддерживают два типа указателей: 

* **Указатели потоковой передачи OnDemandOrigin.** Такие указатели используются для потоковой передачи с переменной скоростью. Примеры потоковой передачи с переменной скоростью: Apple HTTP Live Streaming (HLS), Microsoft Smooth Streaming и динамическая потоковая передача с переменной скоростью по HTTP (DASH, также называется MPEG-DASH). Чтобы создать указатель потоковой передачи, в ресурсе должен быть ISM-файл. 
* **Последовательные указатели (подписанного URL-адреса).** Такие указатели используются для доставки видео при последовательном скачивании.

Чтобы создать URL-адрес потоковой передачи HLS, добавьте *(format=m3u8-aapl)* к URL-адресу:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{file name}.ism/Manifest(format=m3u8-aapl)

Чтобы создать URL-адрес потоковой передачи для воспроизведения ресурсов Smooth Streaming, используйте следующий формат:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{file name}.ism/Manifest

Чтобы создать URL-адрес для потоковой передачи в формате MPEG-DASH, добавьте к исходному адресу строку *(format=mpd-time-csf)*:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{file name}.ism/Manifest(format=mpd-time-csf)

Подписанный URL-адрес имеет следующий формат:

    {blob container name}/{asset name}/{file name}/{shared access signature}

Дополнительные сведения см. в статье [Доставка содержимого клиентам](media-services-deliver-content-overview.md).

> [!NOTE]
> Срок действия указателей, которые были созданы на портале Azure до марта 2015 г., — два года.  
> 
> 

Чтобы обновить для указателя конечную дату срока действия, вы можете использовать [REST API](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) или [.NET API](http://go.microsoft.com/fwlink/?LinkID=533259). 

> [!NOTE]
> Когда вы обновляете срок действия последовательного указателя, URL-адрес изменяется.

### <a name="to-use-the-portal-to-publish-an-asset"></a>Публикация ресурса с помощью портала
1. Создание учетной записи служб мультимедиа Azure с помощью [портала Azure](https://portal.azure.com/).
2. Установите флажок **Параметры** > **Ресурсы-контейнеры**. Выберите ресурс, который требуется опубликовать.
3. Нажмите кнопку **Опубликовать**.
4. Выберите тип указателя.
5. Выберите **Добавить**.
   
    ![Публикация видео](./media/media-services-portal-vod-get-started/media-services-publish1.png)

URL-адрес будет добавлен в список **опубликованных URL-адресов**.

## <a name="play-content-in-the-portal"></a>Воспроизведение содержимого на портале
На портале Azure можно проверить видео с помощью проигрывателя содержимого.

Выберите видео и нажмите кнопку **Воспроизвести**.

![Воспроизведение видео на портале Azure](./media/media-services-portal-vod-get-started/media-services-play.png)

Важные особенности

* Убедитесь, что видео опубликовано.
* Проигрыватель мультимедиа на портале Azure воспроизводит содержимое из конечной точки потоковой передачи по умолчанию. Если требуется воспроизвести содержимое из другой конечной точки потоковой передачи (не являющейся точкой по умолчанию), выберите URL-адрес, скопируйте его и вставьте другой проигрыватель. Например, можно проверить видео с помощью [проигрывателя мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* Конечная точка потоковой передачи, из которой осуществляется потоковая передача, должна быть запущена.  

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

