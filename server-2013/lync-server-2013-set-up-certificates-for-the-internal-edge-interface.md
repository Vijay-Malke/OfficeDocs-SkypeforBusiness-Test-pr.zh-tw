﻿---
title: Lync Server 2013：設定內部邊緣介面的憑證
TOCTitle: 設定內部邊緣介面的憑證
ms:assetid: a1963cc9-87c5-4935-86c0-6bedc6afd0ac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412750(v=OCS.15)
ms:contentKeyID: 49291870
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定內部邊緣介面的憑證

 

_**上次修改主題的時間：** 2013-11-07_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您執行 [憑證精靈] 時，請確定您用來登入的帳戶，是具有您要使用之憑證範本類型適當權限的群組成員。根據預設， Lync Server 2013 憑證要求會使用 Web 伺服器憑證範本。如果您要以 RTCUniversalServerAdmins 群組成員的帳戶使用此範本來要求憑證，請確定群組具有使用該範本所需的註冊權限。</td>
</tr>
</tbody>
</table>


每部 Edge Server 的內部介面均需要單一憑證。該內部介面的憑證既可以由內部企業憑證授權單位 (CA) 核發，又可以由公用 CA 核發。若在您的組織內部署了一個內部 CA，則透過使用該內部 CA 為內部介面核發憑證，可以省去使用公用憑證的費用。您可以使用內部 Windows Server 2008 CA 或 Windows Server 2008 R2 CA 建立這些憑證。

如需有關此憑證與其他憑證需求的詳細資訊，請參閱＜ [Lync Server 2013 中的外部使用者存取的憑證需求](lync-server-2013-certificate-requirements-for-external-user-access.md)＞。

若要在某個網站設定內部邊緣介面的憑證，請使用本節中的程序執行下列動作：

1.  將內部介面的 CA 憑證鏈結下載到每部 Edge Server。

2.  在每部 Edge Server 上匯入內部介面的 CA 憑證鏈結。

3.  在一部 Edge Server (在此稱為第一部 Edge Server) 上，為內部介面建立憑證要求。

4.  在第一部 Edge Server 上匯入內部介面的憑證。

5.  在此網站 (或部署在此負載平衡器之後) 的其他 Edge Server 上匯入憑證。

6.  為每一部 Edge Server 的內部介面指派憑證。

如果使用 Edge Server 的網站超過一個 (也就是多重網站邊緣拓撲)，或者在不同的負載平衡器後方部署了不同組的 Edge Server，就需要針對具有 Edge Server 的每個網站以及部署在不同的負載平衡器後方的每組 Edge Server 執行這些步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本節程序的步驟使用 Windows Server 2008 CA、 Windows Server 2008 R2 CA、 Windows Server 2012 CA，或 Windows Server 2012 R2 CA，來為每部 Edge Server 建立憑證。如需任何其他 CA 的逐步指引，請參閱該 CA 的相關文件。根據預設，所有通過驗證的使用者皆有適當的使用者權限來要求憑證。<br />
本節中的程序會將在 Edge Server 上建立憑證要求作為 Edge Server 部署程序的一部分。可以使用前端伺服器建立憑證要求。這樣做之後，您可以及早在計劃和部署程序期間完成憑證要求，然後再開始部署 Edge Server。為此，您必須確保您要求的憑證已使用可匯?的私密金鑰來定義。<br />
本節中的程序描述了對憑證使用 .cer 和 .p7b 檔案。若您使用的是其他類型的檔案，請根據需要修改這些程序。</td>
</tr>
</tbody>
</table>


## 使用 certsrv 網站為內部介面下載 CA 憑證鏈結

1.  以 **Administrators** 群組成員的身分登入內部網路中的 Lync Server 2013 伺服器 (也就是說，不是 Edge Server)。

2.  若要在命令提示字元下執行下列命令，只需依序按一下 **\[開始\]** 、 **\[執行\]** ，然後再鍵入下列內容：
    
        https://<name of your Issuing CA Server>/certsrv
    
    例如：
    
        https://ca01.contoso.net/certsrv
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您使用的是 Windows Server 2008 或 Windows Server 2008 R2 企業 CA，則必須使用 https，而非 http。</td>
    </tr>
    </tbody>
    </table>


3.  在發行 CA 的 certsrv 網頁上，在 \[選取工作\] 下方，按一下 \[下載 CA 憑證、憑證鏈結或 CRL\] 。

4.  在 **\[下載 CA 憑證、憑證鏈結或 CRL\]** 底下，按一下 **\[下載 CA 憑證鏈結\]** 。

5.  在 **\[檔案下載\]** 對話方塊中，按一下 **\[儲存\]** 。

6.  將 .p7b 檔案儲存到伺服器的硬碟機上，然後將它複製到每一部 Edge Server 上的資料夾。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>.p7b 檔案包含憑證路徑中的所有憑證。如果要檢視憑證路徑，請開啟伺服器憑證，然後按一下憑證路徑。</td>
    </tr>
    </tbody>
    </table>


## 使用 MMC 為內部介面匯出 CA 憑證鏈結

1.  您可以使用 Microsoft Management Console (MMC) 從任何已加入網域的電腦匯出 CA 根憑證。依序按一下 \[開始\] 、\[執行\] ，然後輸入 **MMC**。

2.  在 MMC 主控台中按一下 \[檔案\] ，然後按一下 \[新增/移除\] 。

3.  在 \[新增或移除嵌入式管理單元\] 對話清單中，選取 \[憑證\] ，然後按一下 \[新增\] 。在提示出現時，選取 \[電腦帳戶\] 。在 \[選取電腦\] 對話方塊中，選取 \[本機電腦\] 。按一下 \[完成\] 。按一下 \[確定\] 。

4.  展開 \[憑證 (本機電腦)\] 。展開 \[信任的根憑證授權\] ，選取 \[憑證\] 。

5.  按一下您的 CA 發行的根憑證。用滑鼠右鍵按一下此憑證，依序選取 \[所有工作\] 、\[匯出\] 。\[憑證匯出精靈\] 將會開啟。

6.  在 \[憑證匯出精靈\] 中，按 \[下一步\] 。

7.  在 \[匯出檔案格式\] 對話方塊中，選取要匯出的目標格式。建議使用 \[密碼編譯訊息語法標準 – PKCS \#7 憑證 (.P7B)\]。如果您選取 \[密碼編譯訊息語法標準 – PKCS \#7 憑證 (.P7B)\]，請選取 \[如果可能的話，包含憑證路徑中的所有憑證\] 核取方塊以匯出憑證鏈結，包含根 CA 憑證和任何中繼 CA 憑證。按 \[下一步\] 。

8.  在檔案名稱輸入的 \[要匯出的檔案\] 對話方塊中，輸入所匯出憑證的路徑和檔案名稱 (預設副檔名為 .p7b)。選擇性按一下 \[瀏覽\] ，找出要放入所匯出憑證的目錄，並提供所匯出憑證的名稱。按一下 \[儲存\] ，再按 \[下一步\] 。

9.  檢閱動作摘要，然後按一下 \[完成\] 便完成憑證匯出。按一下 \[確定\] 確認匯出成功。

## 若要匯入內部介面的 CA 憑證鏈結

1.  依序按一下 **\[開始\]** 、 **\[執行\]** ，然後在 **\[開啟\]** 方塊中輸入 **mmc** ，然後按一下 **\[確定\]** ，在每一部 Edge Server 上開啟 Microsoft Management Console (MMC)。

2.  在 **\[檔案\]** 功能表中，按一下 **\[新增/移除嵌入式管理單元\]** ，然後按一下 \[新增\] 。

3.  在 **\[新增獨立嵌入式管理單元\]** 方塊中，按一下 **\[憑證\]** ，然後按一下 \[新增\] 。

4.  在 **\[憑證嵌入式管理單元\]** 對話方塊中，按一下 **\[電腦帳戶\]** ，然後按 **\[下一步\]** 。

5.  在 **\[選擇電腦\]** 對話方塊中，確定 **\[本機電腦: (執行這個主控台的電腦)\]** 核取方塊已經選取，然後按一下 \[完成\] 。

6.  按一下 **\[關閉\]** ，然後按一下 \[確定\] 。

7.  在主控台樹狀目錄中，依序展開 **\[憑證 (本機電腦)\]** ，以滑鼠右鍵按一下 **\[信任的根憑證授權\]** ，指向 **\[所有工作\]** ，然後按一下 **\[匯入\]** 。

8.  在精靈的 **\[要匯入的檔案\]** 中，指定憑證的檔案名稱 (即在上述程序中為內部介面下載 CA 憑證鏈結時所指定的名稱)。

9.  在每一部 Edge Server 上重複這個程序。

## 若要為內部介面建立憑證要求

1.  在一部 Edge Server 上，開始 \[部署精靈\]，然後前往 **\[步驟 3：要求、安裝或指派憑證\]** ，再按一下 **\[執行\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您在集區中的單一位置有多部 Edge Server，則可以在任何一部 Edge Server 上執行「憑證精靈」。<br />
    首次執行步驟 3 之後，按鈕將變更為 <strong>[再執行一次]</strong> ，要求、安裝並指派了所有的必要憑證之後，才會顯示一個綠色核取記號，表示成功完成工作。</td>
    </tr>
    </tbody>
    </table>


2.  在 \[可用憑證工作\] 頁面上，按一下 \[建立新憑證要求\] 。

3.  在「憑證要求」 頁面上，按 \[下一步\] 。

4.  在「延遲或立即要求」 頁面上，按一下 **\[立即準備此要求，但稍後再傳送\]** 。

5.  在「憑證要求檔案」 頁面上，輸入用來儲存此要求的檔案完整路徑和名稱，(例如， **c:\\cert\_internal\_edge.cer** )。

6.  若要使用預設 WebServer 範本之外的其他範本，在 **\[指定其他憑證範本\]** 頁面上，選取 **\[針對選取的憑證授權單位使用其他憑證範本\]** 核取方塊。

7.  在 \[名稱和安全性設定\] 頁面上，執行下列動作：
    
      - 在 **\[易記名稱\]** 中，鍵入憑證的顯示名稱 (例如 \[內部邊緣\])。
    
      - 在 **\[位元長度\]** 中，指定位元長度 (預設值通常是 **2048** )。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>位元長度越長越安全，但是可能會對速度造成負面影響。</td>
        </tr>
        </tbody>
        </table>
    
      - 如果憑證需要是可匯?的憑證，則請選取 **\[將憑證私密金鑰標示為可匯出\]** 核取方塊。

8.  在 **\[組織資訊\]** 頁面上，輸入組織的名稱和組織單位 (OU)，例如部門。

9.  在 \[地理資訊\] 頁面上，指定位置資訊。

10. 在 \[主體名稱/主體別名\] 頁面上，會顯示精靈將自動填入的資訊。

11. 在 \[設定其他主體別名\] 頁面上，指定任何需要的其他主體別名。

12. 在 **\[要求摘要\]** 頁面上，檢閱要用於產生要求的憑證資訊。

13. 命令完成之後，請執行下列動作：
    
      - 若要檢視憑證要求記錄檔，按一下 **\[檢視記錄檔\]** 。
    
      - 若要完成憑證要求，按 **\[下一步\]** 。

14. 在 **\[憑證要求檔案\]** 頁面上，執行下列步驟：
    
      - 若要檢視產生的憑證簽署要求 (CSR) 檔案，按一下 **\[檢視\]** 。
    
      - 按一下 **\[完成\]** ，關閉精靈。

15. 將這個檔案送出給 CA (透過電子郵件或是您的組織對企業 CA 支援的其他方法)，然後當您收到回應檔案時，將新的憑證複製到這部電腦上，讓它可供匯入。

## 若要為內部介面匯入憑證

1.  以 Administrators 群組成員的身分登入建立憑證要求的 Edge Server。

2.  在 \[部署精靈\] 中的 **\[步驟 3：要求、安裝或指派憑證\]** 旁邊的 **\[再執行一次\]** 。
    
    首次執行步驟 3 之後，按鈕將變更為 **\[再執行一次\]** ，要求、安裝並指派了所有的必要憑證之後，才會顯示一個綠色核取記號，表示成功完成工作。

3.  在 **\[可用憑證工作\]** 頁面上，按一下 **\[從 .P7b, .pfx 或 .cer 檔案匯入憑證\]** 。

4.  在 **\[匯入憑證\]** 頁面上，鍵入此 Edge Server 內部介面要求或收到的憑證的完整路徑名稱和檔案名稱 (或是按一下 **\[瀏覽\]** 找出並選取該檔案)。

5.  如果要將某個包含私密金鑰的憑證匯入集區中其他成員的憑證中，請選取 **\[憑證檔案包含憑證的私密金鑰\]** 核取方塊，然後指定密碼。

## 為集區中的 Edge Server 匯出包含私密金鑰的憑證

1.  以 Administrators 群組成員身分登入剛才用來匯入憑證的同一部 Edge Server。

2.  依序按一下 \[開始\] 、\[執行\] ，然後輸入 **MMC** 。

3.  在 MMC 主控台按一下 \[檔案\] ，按一下 \[新增/移除嵌入式管理單元\] 。

4.  在 \[新增或移除嵌入式管理單元 \] 頁面中，按一下 \[憑證\] ，按一下 \[新增\] 。

5.  在 \[憑證嵌入式管理單元\] 對話方塊中，選取 \[電腦帳戶\] 。按 \[下一步\] 。在 \[選取電腦\] 中選取 \[本機電腦 (執行這個主控台的電腦)\] 。按一下 \[完成\] 。按一下 \[確定\] 以完成 MMC 主控台的設定。

6.  按兩下 \[憑證 (本機電腦)\] 以展開憑證存放區。按兩下 \[個人\] ，然後按兩下 \[憑證\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果本機電腦的憑證個人存放區中沒有憑證，則匯入的憑證就沒有關聯的私密金鑰。請檢閱要求和匯入步驟。如果問題仍持續存在，請與您的憑證授權單位管理員或提供者連絡。</td>
    </tr>
    </tbody>
    </table>


7.  在本機電腦的憑證個人存放區中，用滑鼠右鍵按一下您要匯出的憑證。按一下 \[所有工作\] ，按一下 \[匯出\] 。

8.  在 \[憑證匯出精靈\] 中，按 \[下一步\] 。選取 \[是，匯出私密金鑰\] 。按 \[下一步\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 [是，匯出私密金鑰] 選項無法使用，則與該憑證關聯的私密金鑰就不會標示為可匯出。您需要重新申請憑證，確定憑證標示為允許匯出私密金鑰，才能繼續匯出。請與您的憑證授權單位管理員或提供者連絡。</td>
    </tr>
    </tbody>
    </table>


9.  在 \[匯出檔案格式\] 對話方塊中，選取 \[個人資訊交換 – PKCS\#12 (.PFX)\]，然後選取下列項目：
    
      - 盡可能在憑證路徑中包含所有憑證
    
      - 匯出所有延伸內容
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>從 Edge Server 匯出憑證時，不要選取 [如果匯出成功即刪除私密金鑰] 。選取這個選項時，必須將憑證和私密金鑰匯入這個 Edge Server。</td>
        </tr>
        </tbody>
        </table>
    
    按 \[下一步\] 繼續。

10. 如果您要指派密碼來保護私密金鑰，請輸入私密金鑰的密碼。再次輸入密碼進行確認。按 \[下一步\] 。

11. 輸入匯出憑證的路徑和檔案名稱，使用 .pfx 副檔名。路徑必須可供集區中的所有其他 Edge Server 存取，或是可透過卸除式媒體進行傳輸，例如 USB 快閃磁碟機。按 \[下一步\] 。

12. 檢視 \[完成憑證匯出精靈\] 對話方塊上的摘要。按一下 \[完成\] 。

13. 在匯出成功的對話方塊中按一下 \[確定\] 。

14. 遵循＜ [針對 Lync Server 2013 設定外部 Edge 介面的憑證](lync-server-2013-set-up-certificates-for-the-external-edge-interface.md)＞中所述的步驟，將匯出的憑證檔案匯入其他 Edge Server。

## 若要在 Edge Server 上指派內部憑證

1.  在每部 Edge Server 上，於 \[部署精靈\] 中的 **\[步驟 3：要求、安裝或指派憑證\]** 旁邊的 **\[再執行一次\]** 。

2.  在 **\[可用憑證工作\]** 頁面上，按一下 **\[指派現有的憑證\]** 。

3.  在 **\[憑證指派\]** 頁面上，選取清單中的 **\[Edge 內部\]** 。

4.  在 **\[憑證儲存\]** 頁面上，選取在上述程序中為內部邊緣匯入的憑證。

5.  在 **\[憑證指派摘要\]** 頁面上，檢閱您的設定，然後按 **\[下一步\]** 指派憑證。

6.  在精靈完成頁面中，按一下 \[完成\] 。

7.  使用本程序指派內部邊緣憑證之後，開啟每部伺服器上的「憑證」嵌入式管理單元，依序展開 **\[憑證 (本機電腦)\]** 、 **\[個人\]** ，按一下 **\[憑證\]** ，然後確認在詳細資料窗格中有列出的內部邊緣憑證。

8.  如果您的部署範圍包括多部 Edge Server，請為每部 Edge Server 重複這個程序。
