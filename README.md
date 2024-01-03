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
*** 請加強說明程式邏輯 <br>

#### Demo video: (請將影片放到雲端空間)

<a href="https://drive.google.com/drive/u/1/my-drive" title="Demo Video"><img src="https://github.com/Kliver0910/logic/blob/main/%E5%B0%88%E9%A1%8C%E5%9C%96%E7%89%87/S__10985510.jpg?raw=true" alt="Demo Video" width="500"/></a>
