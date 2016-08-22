# TI SensorTag CC2541 評估

評估目標：

1.  可以實作瞭解 BLE Subscribe/Notify 的運作
2.  測試與 HTML5/PhoneGap 可以整合的程度
3.  Pilot for IoT

參考資料：

*   CC2541 的首頁： [](http://processors.wiki.ti.com/index.php/Category:BluetoothLE)http://processors.wiki.ti.com/index.php/Category:BluetoothLE

問題：

1.  只能scan 一次的問題(若不 stopScan 就可以持續 scan)
2.  phonegap 的 bluetooth 的元件，同時只能  scan 到一個設備
3.  CC2541 若要變成 iBeacon 需要 Apple 的 MFI 認證，也許到市場上買 iBeacon 比較快

待處理：

*   瞭解CC2541回傳值如何解析, (從 SensorTag App 裡，有每個 censor 的資料，至於資料如何解析，要用 app 把資訊傳出來比較可行)

**   Temperature Data
*   {"0":191,"1":254,"2":8,"3":15,"length":4,"byteOffset":0,"buffer":{"byteLength":4},"byteLength":4}
*    {"0":55,"1":255,"2":8,"3":15,"length":4,"byteOffset":0,"buffer":{"byteLength":4},"byteLength":4}
*   {"0":40,"1":255,"2":12,"3":15,"length":4,"byteOffset":0,"buffer":{"byteLength":4},"byteLength":4}
*   {"0":53,"1":255,"2":12,"3":15,"length":4,"byteOffset":0,"buffer":{"byteLength":4},"byteLength":4}
*   {"0":21,"1":255,"2":12,"3":15,"length":4,"byteOffset":0,"buffer":{"byteLength":4},"byteLength":4}
*   191, 254, 8, 15
*   55, 255, 8, 15
*   40, 255, 12, 15
*   53, 255, 12, 15
*   218, 254, 16, 15
*

*   美化呈現
*   取得更多資訊

心得：

1.  BLE 的 Life-cycle － scan, stop scan, connect, write, subscribe, read, disconnect
2.  iBeacon 與 BLE 的差異

        1.  BLE 使用 GATT 進行溝通，但 iBeacon 只使用 Advertisment Data
    2.  BLE 只有連結時進行 advertisment, iBeacon 持續 Advertisment
    3.  BLE 與 iBeacon 的 advertisment data 完全不同。 iBeacon 有標準的格式，已經有 Phonegap Plugin 寫好的可以讀取
    4.  iBeacon 只能單獨作為 iBeacon 不能與 BLE 其他功能共用

3.  CC2541 Tag 的內容
4.  SubScribe/Notify 的機制，若使用HTML5 的 Brocasting 機制比較容易進行