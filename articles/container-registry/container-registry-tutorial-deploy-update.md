---
title: "Руководство по реестру контейнеров Azure. Отправка обновленного образа в региональные развертывания"
description: "Отправьте измененный образ Docker в геореплицируемый реестр контейнеров Azure, а затем просмотрите изменения, развернутые автоматически в веб-приложения, выполняемые в нескольких регионах. Это третья часть руководства из трех частей."
services: container-registry
author: mmacy
manager: timlt
ms.service: container-registry
ms.topic: tutorial
ms.date: 10/24/2017
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 359fdcabd579d277e40f02eba2d4603ebd9f5f1f
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2017
---
# <a name="push-an-updated-image-to-regional-deployments"></a>Отправка обновленного образа в региональные развертывания

Это третья часть руководства из трех частей. В [предыдущем руководстве](container-registry-tutorial-deploy-app.md) была настроена георепликация для двух различных развертываний веб-приложений. В этом руководстве сначала изменяется приложение, а затем создается новый образ контейнера, который принудительно отправляется в геореплицированный реестр, и наконец, просматриваются изменения, развернутые автоматически веб-перехватчиками реестра контейнеров Azure в обоих экземплярах веб-приложений.

В этом руководстве (последняя часть в серии) вы выполните такие задачи:

> [!div class="checklist"]
> * Изменение веб-приложения HTML.
> * Создание и маркировка образа Docker.
> * Отправка изменений в реестр контейнеров Azure.
> * Просмотр обновленного приложения в двух разных регионах.

Если вы еще не настроили два региональных развертывания службы *Веб-приложение для контейнеров*, см. предыдущее руководство в серии [Развертывание веб-приложения из реестра контейнеров Azure](container-registry-tutorial-deploy-app.md).

## <a name="modify-the-web-application"></a>Изменение веб-приложения

На этом шаге внесите изменения в веб-приложение, которое будет отображаться после принудительной отправки обновленного образа контейнера в реестр контейнеров Azure.

Найдите файл `AcrHelloworld/Views/Home/Index.cshtml` в источнике приложения, [клонированного из GitHub](container-registry-tutorial-prepare-registry.md#get-application-code) в предыдущем руководстве, и откройте его в предпочитаемом текстовом редакторе. Добавьте следующую строку под существующей строкой `<h1>`:

```html
<h1>MODIFIED</h1>
```

Измененный файл `Index.cshtml` должен выглядеть так:

```html
@{
    ViewData["Title"] = "Azure Container Registry :: Geo-replication";
}
<style>
    body {
        background-image: url('images/azure-regions.png');
        background-size: cover;
    }
    .footer {
        position: fixed;
        bottom: 0px;
        width: 100%;
    }
</style>

<h1 style="text-align:center;color:blue">Hello World from:  @ViewData["REGION"]</h1>
<h1>MODIFIED</h1>
<div class="footer">
    <ul>
        <li>Registry URL: @ViewData["REGISTRYURL"]</li>
        <li>Registry IP: @ViewData["REGISTRYIP"]</li>
        <li>Registry Region: @ViewData["REGION"]</li>
    </ul>
</div>
```

## <a name="rebuild-the-image"></a>Перестройка образа

Теперь, после обновления веб-приложения, перестройте его образ контейнера. Как и раньше используйте полное имя образа, включая URL-адрес сервера входа для тега:

```bash
docker build . -f ./AcrHelloworld/Dockerfile -t <acrName>.azurecr.io/acr-helloworld:v1
```

## <a name="push-image-to-azure-container-registry"></a>Передача образа в реестр контейнеров Azure

Теперь отправьте обновленный образ контейнера *acr helloworld* в геореплицированный реестр. Выполните одну команду `docker push`, чтобы развернуть обновленный образ в репликах реестра в регионах *Западная часть США* и *Восточная часть США*.

```bash
docker push <acrName>.azurecr.io/acr-helloworld:v1
```

Выходные данные должны иметь следующий вид.

```bash
The push refers to a repository [uniqueregistryname.azurecr.io/acr-helloworld]
5b9454e91555: Pushed
d6803756744a: Layer already exists
b7b1f3a15779: Layer already exists
a89567dff12d: Layer already exists
59c7b561ff56: Layer already exists
9a2f9413d9e4: Layer already exists
a75caa09eb1f: Layer already exists
v1: digest: sha256:4c3f2211569346fbe2d1006c18cbea2a4a9dcc1eb3a078608cef70d3a186ec7a size: 1792
```

## <a name="view-the-webhook-logs"></a>Просмотр журналов веб-перехватчика

В ходе репликации образа можно увидеть, что веб-перехватчики реестра контейнеров Azure были активированы.

Для просмотра региональных веб-перехватчиков, созданных при развертывании контейнера в службе *Веб-приложения для контейнеров* в предыдущем руководстве, перейдите в реестр контейнеров на портале Azure, а затем выберите **Веб-перехватчик** в разделе **Службы**.

![Веб-перехватчики реестра контейнеров на портале Azure][tutorial-portal-01]

Выберите каждый веб-перехватчик, чтобы просмотреть его журнал вызовов и ответов. Строка для действия **отправки** отобразится в журналах обоих веб-перехватчиков. В этом журнале для веб-перехватчика, расположенного в регионе *Западная часть США*, видно действие **отправки**, активированное с помощью команды `docker push` на предыдущем шаге:

![Журнал веб-перехватчика реестра контейнеров на портале Azure (западная часть США)][tutorial-portal-02]

## <a name="view-the-updated-web-app"></a>Просмотр обновленных веб-приложений

Веб-перехватчики уведомляют веб-приложения о передаче в реестр нового образа, который автоматически развертывает обновленные контейнеры в два региональных веб-приложения.

Убедитесь, что приложение обновлено в обоих развертываниях, перейдя к обоим региональным развертываниям веб-приложений в веб-браузере. Напоминаем, что URL-адрес развернутых веб-приложений можно найти в верхней правой части каждой вкладки обзора службы приложений.

![Обзор службы приложений на портале Azure][tutorial-portal-03]

Чтобы просмотреть обновленное приложение, выберите эту ссылку в обзоре службы приложений. Ниже приведен пример представления приложения, выполняемого в регионе *Западная часть США*:

![Представление измененного веб-приложения в регионе "Западная часть США" в браузере][deployed-app-westus-modified]

Убедитесь, что обновленный образ контейнера также развернут в развертывании *Восточная часть США*, просмотрев его в браузере.

![Представление измененного веб-приложения в регионе "Восточная часть США" в браузере][deployed-app-eastus-modified]

Выполнив одну команду `docker push`, вы обновили оба региональных развертывания веб-приложений, а реестр контейнеров Azure обработал образы контейнеров в сетевых репозиториях.

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы обновили и отправили новую версию контейнера веб-приложения в геореплицированный реестр. Веб-перехватчики в реестре контейнеров Azure уведомили службу "Веб-приложение для контейнеров" об обновлении, что активировало локальное извлечение из реплик реестра.

В этом руководстве (последняя часть в серии) вы выполнили следующие задачи:

> [!div class="checklist"]
> * Обновление веб-приложения HTML.
> * Создание и маркировка образа Docker.
> * Отправка изменений в реестр контейнеров Azure.
> * Просмотр обновленного приложения в двух разных регионах.

<!-- IMAGES -->
[deployed-app-eastus-modified]: ./media/container-registry-tutorial-deploy-update/deployed-app-eastus-modified.png
[deployed-app-westus-modified]: ./media/container-registry-tutorial-deploy-update/deployed-app-westus-modified.png
[local-container-01]: ./media/container-registry-tutorial-deploy-update/local-container-01.png
[tutorial-portal-01]: ./media/container-registry-tutorial-deploy-update/tutorial-portal-01.png
[tutorial-portal-02]: ./media/container-registry-tutorial-deploy-update/tutorial-portal-02.png
[tutorial-portal-03]: ./media/container-registry-tutorial-deploy-update/tutorial-portal-03.png