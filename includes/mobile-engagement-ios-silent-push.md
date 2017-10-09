> [!IMPORTANT]
> <span data-ttu-id="a834d-101">tooreceive Push-уведомления от мобильного охвата необходимо tooenable `Silent Remote Notifications` в приложении.</span><span class="sxs-lookup"><span data-stu-id="a834d-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="a834d-102">Необходимо tooadd hello уведомления удаленного toohello UIBackgroundModes массив значений в файле Info.plist.</span><span class="sxs-lookup"><span data-stu-id="a834d-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="a834d-103">Откройте `info.plist` файл в проекте hello</span><span class="sxs-lookup"><span data-stu-id="a834d-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="a834d-104">Щелкните правой кнопкой мыши hello верхний элемент в списке hello (`Information Property List`) и добавить новую строку</span><span class="sxs-lookup"><span data-stu-id="a834d-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="a834d-105">Введите в новую строку hello`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="a834d-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="a834d-106">Щелкните строку hello tooexpand стрелка влево hello</span><span class="sxs-lookup"><span data-stu-id="a834d-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="a834d-107">Добавьте следующий элемент toohello значение 0 hello`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="a834d-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="a834d-108">После внесения изменения hello info.plist hello XML должен содержать следующие hello ключ и значение:</span><span class="sxs-lookup"><span data-stu-id="a834d-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="a834d-109">Если вы используете **Xcode 7+** и **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="a834d-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="a834d-110">Включите **push-уведомления** в разделе Targets (Конечные объекты) > Your Target Name (Имя вашего конечного объекта) > Capabilities (Возможности).</span><span class="sxs-lookup"><span data-stu-id="a834d-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

