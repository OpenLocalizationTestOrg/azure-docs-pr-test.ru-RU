> [!IMPORTANT]
> Чтобы получать push-уведомления от Mobile Engagement, необходимо включить в приложении `Silent Remote Notifications`. Для этого требуется добавить значение remote-notification в массив UIBackgroundModes в файле info.plist.
> 
> 

1. Откройте файл `info.plist` в проекте.
2. Щелкните правой кнопкой мыши верхний элемент в списке (`Information Property List`) и добавьте новую строку.
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. В новой строке введите: `Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Щелкните стрелку влево, чтобы развернуть строку.
5. Добавьте следующее значение в элемент 0 `App downloads content in response to push notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. После внесения изменений XML-файл info.plist должен содержать следующий ключ и значение:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Если вы используете **Xcode 7+** и **iOS 9+**:
   
   * Включите **push-уведомления** в разделе Targets (Конечные объекты) > Your Target Name (Имя вашего конечного объекта) > Capabilities (Возможности).

