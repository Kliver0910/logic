# 此為 NCNU FPGA 期末專案 github readme 檔案

# FPGA-project-1
### Authors: 111321030 吳冠德 111321028 莊財瑋

#### Input/Output unit:<br>
* 8x8 LED 矩陣，用來顯示遊戲畫面。下圖為按下 clear 的初始畫面。<br>
<img src="https://github.com/Kliver0910/logic/blob/main/%E5%B0%88%E9%A1%8C%E5%9C%96%E7%89%87/S__10985508.jpg?raw=true" width="300"/><br>
* 七段顯示器，用來顯示分數。<br>
<img src="https://github.com/Kliver0910/logic/blob/main/%E5%B0%88%E9%A1%8C%E5%9C%96%E7%89%87/S__10985511.jpg?raw=true" width="300"/><br>
* LED 陣列，用來計生命值。<br>
<img src="https://github.com/Kliver0910/logic/blob/main/%E5%B0%88%E9%A1%8C%E5%9C%96%E7%89%87/S__10985512.jpg?raw=true" width="300"/><br>

#### 功能說明:<br>
2位玩家輪流對戰，得分較高者獲勝<br>

#### 程式模組說明:<br>
module dodgetgame(output reg [7:0]position_R, position_B, position_G, //8*8 LED,output reg [2:0]S,//LED的腳位,output reg touch, //是否有碰撞,input CLK, Clear, right, left, // 清除，左右，時脈output reg A,B,C,D,E,F,G, // 七段顯示分數,output reg [2:0]b,//life,output reg COM1,COM2//腳位 <br><br>
 left, rigjt -> 4-bit SW.b,touch->16LED. A,B,C,D,E,F,G ->七段顯示器<br>
 Clear ->  8-bit DIPSW.position_R, position_B, position_G ,S-> 8X8LED<br>
1.主要模塊 dodgetgame <br>
 輸出信號：<br>
  position_R、position_B 和 position_G 是顯示在顯示屏上的物體的位置，它們都是 8 位元的。<br>
  S 是一個 3 位元的信號，可能表示某種狀態。<br>
  A、B、C、D、E、F、G 是用於顯示數字的 7 個 LED 燈。<br>
  b 是一個 8 位元的信號，可能表示某種狀態。<br>
  COM1 和 COM2 可能用於多路復用（multiplexing）顯示 7 段顯示器。<br>
 輸入信號：<br>
  CLK 是時鐘信號。<br>
  Clear 用於清零或重置遊戲。<br>
  right 和 left 分別表示向右和向左的移動。<br>
2.移動物邏輯簡化：<br>
  使用 position_R 變量來表示移動物的位置。<br>
  當 left 和 right 標誌觸發時，移動物會向左或向右移動。<br>
  簡化了邊界檢查，防止超出範圍。<br>
3.計分邏輯簡化：<br>
  使用 A_count 和 B_count 變量分別記錄計分。<br>
  使用條件語句進行計分邏輯，使代碼更清晰易讀。<br>
  減少不必要的條件判斷。<br>
#### Demo video: (請將影片放到雲端空間)

<a href="https://drive.google.com/drive/u/1/my-drive" title="Demo Video"><img src="https://github.com/Kliver0910/logic/blob/main/%E5%B0%88%E9%A1%8C%E5%9C%96%E7%89%87/S__10985510.jpg?raw=true" alt="Demo Video" width="500"/></a>
