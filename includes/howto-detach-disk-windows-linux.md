---
writer: kathydav
editor: tysonn
manager: timlt

{}

---
當不再需要某個連接至虛擬機器的資料磁碟時，卸離此資料磁碟很簡單。這會將磁碟從虛擬機器中卸離，但這不會將它從儲存體中移除。

如果您想要再次使用磁碟上現有的資料，您可以將磁碟重新連接至相同或其他虛擬機器。

> [!NOTE]
> 若要卸離作業系統磁碟，您必須先刪除虛擬機器。
> 
> 

## 尋找磁碟
如果您不知道磁碟的名稱，或想要先驗證它再卸離，請遵循下列步驟。

1. 登入 [Azure 傳統入口網站](http://manage.windowsazure.com)。
2. 按一下 [**虛擬機器**]，按一下虛擬機器的名稱，然後按一下 [**儀表板**]。
3. 在 [磁碟] 下，資料表會列出所有連接磁碟的名稱和類型。例如，此畫面會顯示虛擬機器及一個作業系統 (OS) 磁碟和一個資料磁碟：
   
    ![尋找資料磁碟](./media/howto-detach-disk-windows-linux/FindDataDisks.png)

## 卸離磁碟
1. 按一下 [**虛擬機器**]，按一下您想要卸離的資料磁碟所屬的虛擬機器名稱，然後按一下 [**儀表板**]。
2. 從命令列中按一下 [**卸離磁碟**]。
3. 選取資料磁碟，然後按一下核取記號即可卸離。
   
    ![卸離磁碟詳細資料](./media/howto-detach-disk-windows-linux/DetachDiskDetails.png)

磁碟仍留在儲存體中，但不再連接至虛擬機器。

