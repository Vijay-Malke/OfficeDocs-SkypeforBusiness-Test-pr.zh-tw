﻿---
title: Lync Server 2013：管理 SIP 主幹服務提供者的位置
TOCTitle: 管理 SIP 主幹服務提供者的位置
ms:assetid: d9b33b56-66c2-4dee-b056-faaf98925bf2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398959(v=OCS.15)
ms:contentKeyID: 49292506
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理 SIP 主幹服務提供者的位置

 

_**上次修改主題的時間：** 2012-10-02_

若要設定讓 Lync Server 自動在網路內尋找用戶端，您需要在 位置資訊服務資料庫內填入網路接線圖並發佈位置，或者連至已包含正確對應的外部資料庫。您必須在此程序中向 E9-1-1 服務提供者驗證位置的市民地址。如需詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中設定位置資料庫](lync-server-2013-configure-the-location-database.md)＞。

您可在位置資訊服務資料庫填入緊急回應位置 (ERL)，其中包含市民地址與建築物內的特定地址。有建築物內特定位置的 位置資訊服務**Location** 欄位長度上限為 20 個字元 (包括空格)。

  - 簡單易懂且可識別 119 致電者位置的名稱，確保緊急救護員到達市民地址時能迅速找到該特定位置。此位置名稱可包含建築物編號、樓層編號、側廳指示項、房號等。避免使用只有員工才知道的暱稱，其可能會讓緊急救護員前往錯誤的位置。

  - 位置識別碼，幫助使用者輕鬆看出其 Lync 用戶端已取得正確的位置。Lync 用戶端會在其標頭自動串連和顯示找到的 **Location** 與 **City** 欄位。建議您在每個位置識別碼加上建築物的街道地址 (例如 \<街道編號\> 1 樓)。不加上街道地址，一般位置識別碼 (例如 1 樓) 可泛指城市中的任何建築物。

  - 如果是由無線存取點決定的概略位置，您可能想要加上 Near 的字詞 (例如 1234 號 1 樓附近)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在使用 Lync Server 管理命令介面命令發佈位置，並複寫到集區的本機存放區之前，用戶端無法使用新增到中央位置資料庫的位置。如需詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-publish-the-location-database.md">在 Lync Server 2013 中發佈位置資料庫</a>＞。</td>
</tr>
</tbody>
</table>


以下各節討論填入和維護位置資料庫時需考量的事項。

## 填入位置資料庫

下列問題可協助您決定如何填入位置資料庫。

  - **您將使用何種程序填入位置資料庫？**  
    資料會出現在何處，以及需要執行哪些步驟將資料轉換成位置資料庫所需的格式？您將個別加入位置，或是使用 CSV 檔大量加入位置？

<!-- end list -->

  - **您是否有已包含位置對應的協力廠商資料庫？**  
    使用 Lync Server 的次要 位置資訊服務選項連線至協力廠商資料庫，就能使用離線平台將位置分組並進行管理。此方法的好處在於，除了將位置與網路識別碼產生關聯之外，您還可以將位置與使用者產生關聯。這表示， 位置資訊服務可以將多個自次要 位置資訊服務產生的位址傳回 Lync Server 用戶端。然後使用者可以選擇最適合的位置。
    
    若要與 位置資訊服務整合，協力廠商資料庫必須遵循 Lync Server 位置要求/回應結構描述。如需詳細資訊，請參閱《\[MS-E911WS\]：E911 支援通訊協定規格的 Web 服務》，網址為 [http://go.microsoft.com/fwlink/?linkid=213819\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=213819%26clcid=0x404) (英文)。如需部署次要 位置資訊服務的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中設定次要位置資訊服務](lync-server-2013-configure-a-secondary-location-information-service.md)＞。

如需填入位置資料庫的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中設定位置資料庫](lync-server-2013-configure-the-location-database.md)＞。

## 維護位置資料庫

填入位置資料庫之後，您必須發展可隨著網路組態變更而更新資料庫的策略。下列問題將協助您決定如何維護位置資料庫。

  - **您要如何更新位置資料庫？**  
    有數種情況需要更新位置資料庫，包括新增 WAP、辦公室重新佈線 (造成指派不同的交換器) 以及擴充子網路。您將直接更新每個個別位置，或是使用 CSV 檔大量更新所有位置？

<!-- end list -->

  - **您要使用 SNMP 應用程式將 Lync 用戶端的 MAC 位址來與連接埠和交換器識別碼比對嗎？**  
    如果您使用 SNMP 應用程式，就必須發展可讓 SNMP 應用程式與位置資料庫之間的交換器底座與連接埠資訊保持一致的手動程序。如果 SNMP 應用程式傳回資料庫中沒有的底座 IP 位址或連接埠識別碼， 位置資訊服務即無法將位置傳回用戶端。

