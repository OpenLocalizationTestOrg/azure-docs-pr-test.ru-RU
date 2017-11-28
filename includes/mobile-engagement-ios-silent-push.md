> [!IMPORTANT]
> <span data-ttu-id="8c51d-101">Чтобы получать push-уведомления от Mobile Engagement, необходимо включить в приложении `Silent Remote Notifications`.</span><span class="sxs-lookup"><span data-stu-id="8c51d-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="8c51d-102">Для этого требуется добавить значение remote-notification в массив UIBackgroundModes в файле info.plist.</span><span class="sxs-lookup"><span data-stu-id="8c51d-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="8c51d-103">Откройте файл `info.plist` в проекте.</span><span class="sxs-lookup"><span data-stu-id="8c51d-103">Open `info.plist` file in the project</span></span>
2. <span data-ttu-id="8c51d-104">Щелкните правой кнопкой мыши верхний элемент в списке (`Information Property List`) и добавьте новую строку.</span><span class="sxs-lookup"><span data-stu-id="8c51d-104">Right click on the top item in the list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="8c51d-105">В новой строке введите: `Required background modes`</span><span class="sxs-lookup"><span data-stu-id="8c51d-105">In the new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="8c51d-106">Щелкните стрелку влево, чтобы развернуть строку.</span><span class="sxs-lookup"><span data-stu-id="8c51d-106">Click on the left arrow to expand the row</span></span>
5. <span data-ttu-id="8c51d-107">Добавьте следующее значение в элемент 0 `App downloads content in response to push notifications`</span><span class="sxs-lookup"><span data-stu-id="8c51d-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="8c51d-108">После внесения изменений XML-файл info.plist должен содержать следующий ключ и значение:</span><span class="sxs-lookup"><span data-stu-id="8c51d-108">Once you make the change, the info.plist XML should contain the following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="8c51d-109">Если вы используете **Xcode 7+** и **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="8c51d-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="8c51d-110">Включите **push-уведомления** в разделе Targets (Конечные объекты) > Your Target Name (Имя вашего конечного объекта) > Capabilities (Возможности).</span><span class="sxs-lookup"><span data-stu-id="8c51d-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

