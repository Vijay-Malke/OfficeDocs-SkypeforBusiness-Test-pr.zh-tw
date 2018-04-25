﻿---
title: Lync Server 2013：定義 E9-1-1 部署的範圍
TOCTitle: 定義 E9-1-1 部署的範圍
ms:assetid: 2c572dfd-e901-471d-b5a0-18bc8d1d5328
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425775(v=OCS.15)
ms:contentKeyID: 49290446
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義 E9-1-1 部署的範圍

 

_**上次修改主題的時間：** 2012-06-06_

在針對 E9-1-1 設定 Microsoft Lync Server 2013 前，您必須先規劃 E9-1-1 部署。應考量的問題包括：

  - **您組織對於 E9-1-1 的原則及法律義務為何？**  
    E9-1-1 對於 PBX (以 E9-1-1 的說法稱為多線電話系統，或 MLTS) 的法律要求會因為各州而有所不同。您應諮詢您的法律小組，了解可能要在相關地理區域的 Lync Server 部署中套用的義務。

<!-- end list -->

  - **您的企業中有哪些領域需要啟用 E9-1-1？**  
    您可以為整個企業或為選取的位置啟用 E9-1-1。例如，對於位於不同州的辦公室，您可能有不同的 E9-1-1 需求，或者您可能想要排除美國境外的網站。

<!-- end list -->

  - **您要如何將 E9-1-1 部署至分支網站？**  
    在分支網站部署 E9-1-1 時，語音恢復能力是必須要了解的重要概念。如果您有集中式 E-9-1-1 主幹，在 WAN 中斷時，登入的用戶端將可能無法連繫 位置資訊服務的位置，或是連線至緊急服務的服務提供者。 Lync Server 提供了幾項用以處理分公司語音恢復能力的策略，包括：佈建可恢復的資料網路、在每個分公司部署 SIP 主幹，或是在 WAN 中斷期間將電話向外發送至本機閘道。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中規劃分支網站語音彈性](lync-server-2013-planning-for-branch-site-voice-resiliency.md)＞。

<!-- end list -->

  - **您是否會為在網路以外工作的使用者啟用 E9-1-1？**  
    自動取得位置僅適用於位於組織網路內部的用戶端，因此您的組織必須決定是否要支援來自外部部署 Lync 用戶端發出的 E9-1-1 電話。例如，若使用者是在家裡工作，或是在客戶網站上，您是否要允許該使用者撥打緊急通話？若用戶端位於企業網路之外，可設定用戶端提示使用者告知其位置。不過根據主要街道地址指南 (MSAG)，這些使用者提供的位置無法預先加以驗證，緊急服務的服務提供者發送方需要以口頭與來電者確定此位置的有效性，才能將電話路由至公共安全勤務中心 (PSAP)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>使用 VPN 連線至您組織的使用者，其 Lync 用戶端可取得內部 IP 位址資訊，但由於這些位址無法用於識別使用者的實際位置，因此必須將 VPN 子網路排除在 位置資訊服務之外。</td>
    </tr>
    </tbody>
    </table>


<!-- end list -->

  - **您是否要提供路由至美國以外網站的緊急電話？**  
    您可以為公司中不受緊急服務的服務提供者所涵蓋的區域 (例如駐外地點) 提供緊急路由。若要這麼做，請建立新網站，然後為其指派語音原則，並讓此語音原則參照透過本機 PSTN 閘道路由電話的 PSTN 使用方式。
