﻿---
title: Lync Server 2013：建立撥號對應表
TOCTitle: 建立撥號對應表
ms:assetid: d2fef3d0-7e78-4591-b712-d62ac71d71a5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398909(v=OCS.15)
ms:contentKeyID: 49292407
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立撥號對應表

 

_**上次修改主題的時間：** 2013-10-24_

若要建立新的撥號對應表，請執行下列程序中的步驟。如果您要編輯撥號對應表，請參閱 [在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)。

## 若要建立撥號對應表

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[語音路由\]** 和 **\[撥號對應表\]** 。

4.  在 **\[撥號對應表\]** 頁面上按一下 **\[新增\]** ，然後選取撥號對應表的範圍：
    
      - **\[站台撥號對應表\]** 適用於整個網站，但指派給使用者對應表的任何使用者或群組除外。如果您選取 **\[站台\]** 做為撥號對應表的範圍，則必須從 **\[選取站台\]** 對話方塊選擇網站。如果已建立網站的撥號對應表，則該網站不會出現在 **\[選取站台\]** 對話方塊。
    
      - **\[集區撥號對應表\]** 可以套用至公用交換電話網路 (PSTN) 閘道或登錄器。如果您選取 **\[集區\]** 做為撥號對應表的範圍，請從 **\[選取服務\]** 對話方塊選擇 PSTN 閘道或登錄器。如果已建立服務 (PSTN 閘道或登錄器) 的撥號對應表，則該服務不會出現在清單中。
    
      - **\[使用者撥號對應表\]** 可套用至指定的使用者或群組。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>選取撥號對應表範圍之後，就無法更改。</td>
    </tr>
    </tbody>
    </table>


5.  如果您要建立使用者撥號對應表，請在 **\[新的撥號對應表\]** 對話方塊的 **\[名稱\]** 欄位中輸入描述性名稱。此名稱儲存之後，就無法更改。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若為網站撥號對應表， <strong>[名稱]</strong> 欄位會預先填入網站名稱，而且無法更改。<br />
    若為集區撥號對應表， <strong>[名稱]</strong> 欄位會預先填入 PSTN 閘道或登錄器名稱，而且無法更改。</td>
    </tr>
    </tbody>
    </table>


6.  **\[簡單名稱\]** 欄位會預先填入出現在 **\[名稱\]** 欄位中的相同名稱。您可以選擇性地編輯此欄位來指定更為描述性的名稱，以便反映套用撥號對應表的網站、服務或使用者。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>[簡單名稱] 在 Lync Server 部署內的所有撥號對應表之間必須是唯一的。此名稱不得超過 256 個 Unicode 字元，其中每個字元可以是字母或數字字元、連字號 (-)、句點 (.) 或底線 (_)。<br />
    「不支援」的字元 包括空格與在 RFC 3966 (http://www.ietf.org/rfc/rfc3966.txt) 中定義的保留字元。 [簡單名稱]中「不支援」的保留字元包括以下：<br />
    &quot;;&quot; &quot;/&quot; &quot;?&quot; &quot;:&quot; &quot;@&quot; &quot;&amp;&quot; &quot;=&quot; &quot;+&quot; &quot;$&quot; &quot;,&quot;</td>
    </tr>
    </tbody>
    </table>


7.  (選用) 在 **\[描述\]** 欄位中，可以輸入有關撥號對應表的其他描述性資訊。

8.  (選用) 如果要使用此撥號對應表作為電話撥入式會議存取號碼的地區，請指定 **\[電話撥入式會議地區\]** 。如果不想將此撥號對應表用於電話撥入式會議存取號碼，請將此欄位保留為空。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>需要使用電話撥入式會議地區，將電話撥入式會議存取號碼與一個或多個撥號對應表關聯。</td>
    </tr>
    </tbody>
    </table>


9.  (選用) 在 **\[外部存取首碼\]** 欄位中，指定只有在使用者需要撥打一個或多個額外的前置數字 (例如 9) 來撥打外線的值。您最多可以輸入四個字元的首碼值 (\#、\* 和 0-9)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果指定了外部存取首碼，則不需要建立新的正規化規則來容納首碼。</td>
    </tr>
    </tbody>
    </table>


10. 針對撥號對應表建立關聯及設定正規化規則，如下所述：
    
      - 若要從 企業語音 部署中可用的所有正規化規則清單中選擇一個或多個規則，請按一下 **\[選取\]** 。在 **\[選取正規化規則\]** 中，反白顯示要與撥號對應表產生關聯的規則，然後按一下 **\[確定\]** 。
    
      - 若要定義新的正規化規則並將其與撥號對應表關聯，請按一下 **\[新增\]** 。如需定義新規則的詳細資訊，請參閱 [在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)。
    
      - 若要編輯已與撥號對應表關聯的正規化規則，請反白顯示該規則名稱並按一下 **\[顯示詳細資訊\]** 。如需編輯規則的詳細資訊，請參閱 [在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)。
    
      - 若要複製現有正規化規則以用作定義新規則的起點，請反白顯示該規則名稱，然後依序按一下 **\[複製\]** 和 **\[貼上\]** 。如需編輯副本的詳細資訊，請參閱 [在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)。
    
      - 若要從撥號對應表移除正規化規則，請反白顯示該規則名稱並按一下 **\[移除\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>每個撥號對應表至少必須具有一個關聯的正規化規則。如需如何判斷撥號對應表需要的所有正規化規則的詳細資訊，請參閱規劃文件中的 <a href="lync-server-2013-dial-plans-and-normalization-rules.md">Lync Server 2013 中的撥號對應表和正規化規則</a>。</td>
    </tr>
    </tbody>
    </table>


11. 確認撥號對應表的正規化規則按照正確的順序排列。若要變更規則在清單中的位置，請反白規則名稱，然後按向上或向下箭頭。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 會由上而下周遊正規化規則清單，並使用符合撥打號碼的第一個規則。如果設定撥號對應表，以便撥打的號碼可以符合多個正規化規則，請確定較嚴格的規則排在較不嚴格的規則上面。<br />
    預設的 [全部保留] 正規化規則 <strong>^(\d{11})$</strong> 符合任何 11 位數號碼。例如，如果您加入符合 11 位數數字且開頭為 1425 的正規化規則，務必確定 [全部保留] 是依照較嚴格的 <strong>^(1425\d{7})$</strong> 規則排序。</td>
    </tr>
    </tbody>
    </table>


12. (選用) 輸入一個測試撥號對應表的號碼，然後按一下 **\[前往\]** 。測試結果將顯示在 **\[輸入測試號碼\]** 下。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以儲存尚未通過測試的撥號對應表，並於日後重新設定。如需詳細資訊，請參閱 <a href="lync-server-2013-test-voice-routing.md">在 Lync Server 2013 中測試語音路由</a>。</td>
    </tr>
    </tbody>
    </table>


13. 按一下 \[確定\] 。

14. 在 \[撥號對應表\] 頁面上，依序按一下 \[認可\] 和 \[全部認可\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>只要您建立撥號對應表，就必須執行 <strong>[全部認可]</strong> 命令發佈組態變更。如需詳細資訊，請參閱操作文件中的 <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### 其他資源

[在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)

