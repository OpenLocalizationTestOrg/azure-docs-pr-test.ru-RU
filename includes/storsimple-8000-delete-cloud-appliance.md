#### <a name="to-delete-a-cloud-appliance"></a><span data-ttu-id="8cd95-101">Удаление облачного устройства</span><span class="sxs-lookup"><span data-stu-id="8cd95-101">To delete a cloud appliance</span></span>

1. <span data-ttu-id="8cd95-102">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8cd95-102">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="8cd95-103">Вы можете удалить только то деактивированное устройство, которое не содержит данных.</span><span class="sxs-lookup"><span data-stu-id="8cd95-103">You can only delete a deactivated device that does not contain data.</span></span> <span data-ttu-id="8cd95-104">Сначала удалите данные на устройстве, или же вы можете [выполнить отработку отказа данных](../articles/storsimple/storsimple-8000-device-failover-cloud-appliance.md) в контейнерах томов на другое устройство.</span><span class="sxs-lookup"><span data-stu-id="8cd95-104">Delete the data on the device first or you can [fail over the data](../articles/storsimple/storsimple-8000-device-failover-cloud-appliance.md) in volume containers to another device.</span></span> <span data-ttu-id="8cd95-105">После удаления данных вы будете готовы отключить устройство.</span><span class="sxs-lookup"><span data-stu-id="8cd95-105">Once the data is deleted, you are ready to deactivate the device.</span></span>
3. <span data-ttu-id="8cd95-106">На странице службы диспетчера устройств StorSimple щелкните **Устройства**, а затем выберите устройство.</span><span class="sxs-lookup"><span data-stu-id="8cd95-106">In your StorSimple Devide Manager service page, click **Devices** and then select the device.</span></span> <span data-ttu-id="8cd95-107">Щелкните его правой кнопкой мыши и выберите **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="8cd95-107">Right-click and select **Deactivate**.</span></span>
4. <span data-ttu-id="8cd95-108">После деактивации устройства щелкните его правой кнопкой мыши и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="8cd95-108">Once the device is deactivated, right-click the device and select **Delete**.</span></span>

    ![Выбор деактивированного устройства и его удаление щелчком](./media/storsimple-8000-delete-cloud-appliance/delete-cloud-appliance1.png)

5. <span data-ttu-id="8cd95-110">Введите имя устройства, чтобы подтвердить его удаление.</span><span class="sxs-lookup"><span data-stu-id="8cd95-110">Type the device name to confirm the deletion.</span></span> <span data-ttu-id="8cd95-111">После удаления устройства список устройств обновится.</span><span class="sxs-lookup"><span data-stu-id="8cd95-111">After the device is deleted, the device list updates.</span></span>

    ![Подтверждение удаления](./media/storsimple-8000-delete-cloud-appliance/delete-cloud-appliance2.png)

6. <span data-ttu-id="8cd95-113">После удаления устройства вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="8cd95-113">You are notified after the device is deleted.</span></span>

    ![Уведомление об успешном удалении устройства](./media/storsimple-8000-delete-cloud-appliance/delete-cloud-appliance4.png)

7. <span data-ttu-id="8cd95-115">Список устройств обновляется, чтобы указать удаленное устройство.</span><span class="sxs-lookup"><span data-stu-id="8cd95-115">The list of devices updates to indicate the deleted device.</span></span>

    ![Обновленный список устройств](./media/storsimple-8000-delete-cloud-appliance/delete-cloud-appliance5.png)
