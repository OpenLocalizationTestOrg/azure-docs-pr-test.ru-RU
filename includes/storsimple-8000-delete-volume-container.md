<!--author=alkohli last changed: 01/13/17-->

<span data-ttu-id="91367-101">Если hello контейнер томов имеет связанные тома, отключите эти тома сначала.</span><span class="sxs-lookup"><span data-stu-id="91367-101">If hello volume container has associated volumes, take those volumes offline first.</span></span> <span data-ttu-id="91367-102">Следуйте указаниям hello [перевести том в автономный режим](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="91367-102">Follow hello steps in [Take a volume offline](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="91367-103">После hello тома находятся в автономном режиме, их можно удалить.</span><span class="sxs-lookup"><span data-stu-id="91367-103">After hello volumes are offline, you can delete them.</span></span> <span data-ttu-id="91367-104">Если контейнер томов hello не имеет связанных томов, удалите контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="91367-104">When hello volume container has no associated volumes, delete hello volume container.</span></span> <span data-ttu-id="91367-105">Выполните следующие процедуры toodelete контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="91367-105">Perform hello following procedure toodelete a volume container.</span></span>

#### <a name="toodelete-a-volume-container"></a><span data-ttu-id="91367-106">toodelete контейнер тома</span><span class="sxs-lookup"><span data-stu-id="91367-106">toodelete a volume container</span></span>
1. <span data-ttu-id="91367-107">Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**.</span><span class="sxs-lookup"><span data-stu-id="91367-107">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="91367-108">Выберите и щелкните устройство hello и перейдите слишком**параметры > Управление > контейнеры томов**.</span><span class="sxs-lookup"><span data-stu-id="91367-108">Select and click hello device and then go too**Settings > Manage > Volume containers**.</span></span>

    ![Колонка "Контейнеры томов"](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

2. <span data-ttu-id="91367-110">Из hello табличный список контейнеров томов, hello выберите контейнер томов, требуется toodelete, щелкните правой кнопкой мыши **...**  , а затем выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="91367-110">From hello tabular list of volume containers, select hello volume container you want toodelete, right click **...** and then select **Delete**.</span></span>

    ![Удаление контейнера томов](./media/storsimple-8000-delete-volume-container/deletevolumecontainer1.png)

3. <span data-ttu-id="91367-112">Удалить контейнер можно в том случае, если с ним не связаны тома.</span><span class="sxs-lookup"><span data-stu-id="91367-112">If a volume container has no associated volumes, then it can be deleted.</span></span> <span data-ttu-id="91367-113">При появлении запроса на подтверждение, просмотрите и установите флажок hello, о том, hello влияние удаления контейнера томов hello.</span><span class="sxs-lookup"><span data-stu-id="91367-113">When prompted for confirmation, review and select hello checkbox stating hello impact of deleting hello volume container.</span></span> <span data-ttu-id="91367-114">Нажмите кнопку **удаление** toothen удалить контейнер томов hello.</span><span class="sxs-lookup"><span data-stu-id="91367-114">Click **Delete** toothen delete hello volume container.</span></span>

    ![Подтверждение удаления](./media/storsimple-8000-delete-volume-container/deletevolumecontainer2.png)

<span data-ttu-id="91367-116">Hello список контейнеров томов — контейнер тома обновленные tooreflect hello удален.</span><span class="sxs-lookup"><span data-stu-id="91367-116">hello list of volume containers is updated tooreflect hello deleted volume container.</span></span>

![](./media/storsimple-8000-delete-volume-container/deletevolumecontainer5.png)


