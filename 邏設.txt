module Dodgetgame(
output reg [7:0]position_R, position_B, position_G, 
output reg [2:0]S,
output reg touch,
output reg enable, 
input CLK, Clear, right, left, 
output reg A,B,C,D,E,F,G,
output reg [2:0]b,
output reg COM1,COM2
);
 wire [7:0]p1;
 wire [2:0]S1;
 wire [7:0]p2; 
 wire [2:0]S2;
 wire [7:0]p3; 
 wire [2:0]S3;
 wire [7:0]p4;
 wire [2:0]S4;
 reg [1:0] count;
 reg [3:0] count2;
   reg [3:0] ti;
   reg [3:0]s;
   reg COM;
 reg [0:3]a;
 reg x;
 reg [4:0] hp;
 reg [3:0]A_count,B_count;
 
 divfreq C1(CLK, CLK_div);
 divfreq2 C2(CLK, CLK_div2);
 divfreq3 C3(CLK, CLK_div3);
 divfreq4 C4(CLK, CLK_div4);
 divfreq5 C5(CLK, CLK_div5);
 divfreq6 C6(CLK, CLK_div6);
 divfreq7 C7(CLK, CLK_div7);
 divfreq8 C8(CLK, CLK_div8);
 divfreq10 C10(CLK, CLK_div10);
 divfreq11 C11(CLK, CLK_div11);
 moveobject M1(CLK_div, Clear, right, left, p1, S1); 
   fallingobject F1(CLK_div2, CLK_div5,Clear,touch, p2, S2,get1);
 fallingobject2 F2(CLK_div4, CLK_div6, Clear, p3, S3,get2);
 fallingobject3 F3(CLK_div7, CLK_div8, Clear, p4, S4,get3);
 
   initial 
 begin
  touch = 0;
  b = 3'b111;
  s=0;
  x=1;
  enable= 1;
 end
 
always @(posedge CLK_div11, posedge Clear)
  begin 
    if(Clear)  
  begin
   A_count <= 4'b0000;
   B_count <= 4'b0000;
  end
    else if(hp<3) 
  begin
    if(A_count<4'b1001)
      A_count <= A_count + 1'd1; 
  else
    begin
    A_count<=4'b0000;
    B_count<=B_count+1'd1;
        end
  end
 end
 
always@(posedge CLK_div3)
   begin
    COM<=~COM;
  if(COM)
   begin
    a[0:3]<=A_count;
    COM1<=0;
    COM2<=1;
   end
  else
   begin
    a[0:3]<=B_count;
    COM1<=1;
    COM2<=0;
   end
      A = ~(a[0]&~a[1]&~a[2] | ~a[0]&a[2] | ~a[1]&~a[2]&~a[3] | ~a[0]&a[1]&a[3]);
        B = ~(~a[0]&~a[1] | ~a[1]&~a[2] | ~a[0]&~a[2]&~a[3] | ~a[0]&a[2]&a[3]);
    C = ~(~a[0]&a[1] | ~a[1]&~a[2] | ~a[0]&a[3]);
    D = ~(a[0]&~a[1]&~a[2] | ~a[0]&~a[1]&a[2] | ~a[0]&a[2]&~a[3] | ~a[0]&a[1]&~a[2]&a[3] | ~a[1]&~a[2]&~a[3]);
    E = ~(~a[1]&~a[2]&~a[3] | ~a[0]&a[2]&~a[3]);
    F = ~(~a[0]&a[1]&~a[2] | ~a[0]&a[1]&~a[3] | a[0]&~a[1]&~a[2] | ~a[1]&~a[2]&~a[3]);
    G = ~(a[0]&~a[1]&~a[2] | ~a[0]&~a[1]&a[2] | ~a[0]&a[1]&~a[2] | ~a[0]&a[2]&~a[3]);
   end

 always@(posedge touch,posedge Clear)
  begin
     if(Clear)
    hp<=0;
   else if(hp<4)
      hp <= hp+1;
  end

 always@(posedge CLK_div3,posedge Clear)
 begin
    if(Clear)
  begin
   count <= count+1;
   b<=3'b111;
   if(count>3)
    count<=0;
   if(count==0)
    begin
     position_R<=p1;
     position_G<=8'b11111111;
     position_B<=8'b11111111;
     S<=S1;  
    end
   else if(count==1)
    begin
      position_R<=8'b11111111;
      position_G<=8'b11111111;
      position_B<=~p2;
      S<=S2;
      if(get1)
       s<= s+2;
    
    end
   else if(count==2)
      begin
      position_R<=8'b11111111;
      position_B<=8'b11111111;
      position_G<=~p3;
      S<=S3;
      if(get2)
       s<=s+2;
      end
    else if(count==3)
      begin
      position_R<=~p4;
      position_B<=8'b11111111;
      position_G<=~p4;
      S<=S4;
      if(get3)
       s<=s+2;
      end
   
   
  end
  else if(hp<3)
  begin
   count <= count+1;
   
   if(count>2)
    count<=0;
   if(count==0)
    begin
     position_R<=p1;
     position_G<=8'b11111111;
     position_B<=8'b11111111;
     S<=S1;  
    end
   else if(count==1)
    begin
      position_R<=8'b11111111;
      position_G<=8'b11111111;
      position_B<=~p2;
      S<=S2;
      if(get1)
       s<= s+2;
      
    end
   else if(count==2)
      begin
      position_R<=8'b11111111;
      position_B<=8'b11111111;
      position_G<=~p3;
      S<=S3;
      if(get2)
       s<=s+2;
      end
   else if(count==3)   //某某障礙物
      begin
      position_R<=8'b11111111;
      position_B<=~p4;
      position_G<=~p4;
      S<=S4;
      if(get3)
       s<=s+2;
      end
      
   if(((p1==((~p2)+2'b11))&&(S1==S2))||((p1==((~p3)-1'b1))&&(S1==S3)) ||((p1==((~p4)-1'b1))&&(S1==S4)))
    begin
     touch <=1;
    end 
   else
    touch<=0;
   if(hp==0)
     b<=3'b111;
   if(hp==1)
     b<=3'b110;
   if(hp==2)
     b<=3'b100;
   
  end
  else if(hp==3) //顯示OVER
   begin
    count2 <= count2+1;
    b<=3'b000;
    if(count2>7)
     count2<=0;
    if (count2 == 0)
             begin
          position_R <= 8'b01111110;  // Set position for "X"
            position_G <= 8'b11111111;
          position_B <= 8'b11111111;
           S <= 0;
           end
        else if (count2 == 1)
         begin
         position_R <= 8'b10111101;  // Set position for "X"
         position_G <= 8'b11111111;
         position_B <= 8'b11111111;
          S <=1;
         end
     else if(count2==2)
     begin
      position_R<=8'b11011011;
      position_G<=8'b11111111;
      position_B<=8'b11111111;
      S<=2;
     end
    else if(count2==3)
     begin
      position_R<=8'b11100111;
      position_G<=8'b11111111;
      position_B<=8'b11111111;
      S<=3;
     end
    else if(count2==4)
     begin
      position_R<=8'b11100111;
      position_G<=8'b11111111;
      position_B<=8'b11111111;
      S<=4;
     end
    else if(count2==5)
     begin
      position_R<=8'b11011011;
      position_G<=8'b11111111;
      position_B<=8'b11111111;
      S<=5;
     end
    else if(count2==6)
     begin
      position_R<=8'b10111101;
      position_G<=8'b11111111;
      position_B<=8'b11111111;
      S<=6;
     end
    else if(count2==7)
     begin
      position_R<=8'b01111110;
      position_G<=8'b11111111;
      position_B<=8'b11111111;
      S<=7;
          end
     end
      end
endmodule

//////移動物////////
module moveobject(input CLK_div, Clear, right, left, output reg [7:0]position, output reg [2:0]S); 
 always@(posedge CLK_div, posedge Clear)
  begin
   if(Clear) //reset
    begin
     S<=4;
     position<=~(8'b00000001);
    end
   else if(left)
    begin
     if(S==0) //邊
      begin
       S<=S;
       position<=~(8'b00000001);
      end
     else
      begin
       S<=S-1;
       position<=~(8'b00000001);
      end
    end
   else if(right)
    begin
     
     if(S==7) //邊
      begin
       S<=S;
       position<=~(8'b00000001);
      end
     else
      begin
       S<=S+1;
       position<=~(8'b00000001);
      end
    end
  end
endmodule

module fallingobject(input CLK_div2, CLK_div5,x,Clear, output reg [7:0]position_B, output reg [2:0]SS,output reg get);
 reg[24:0]cnt;
   reg restart;
   reg player_hit;
 
 always @(posedge CLK_div5) 
  begin
   if(cnt > 5000000)
    cnt <= 25'd0;   

   else
       cnt <= cnt + 1'b1;
         
  end
 initial
   begin
  position_B = 8'b10000000;
  SS =cnt%8;
      restart = 0;
  get=0;
  player_hit = 0; // 初始化碰撞檢測信號
   end 
 always @(posedge CLK_div2)
  begin
    if(restart)
     begin
      position_B <= 8'b10000000; 
      SS <=cnt%8;
      restart = 0;
      get=0;
              player_hit = 0; // 初始化碰撞檢測信號
     end
      else
     begin
      position_B = position_B >> 1;
      
                  if (position_B == SS) begin// 假設玩家碰到寶物的條件是玩家的位置等於寶物的位置
                     player_hit = 1; // 如果碰撞發生，設置碰撞檢測信號
                  end

      if (position_B == 8'b10000000) begin
                    restart = 1;
                     if (x==1) begin
                       get = 1; // 當寶物到達底部且碰撞發生時，設置生命值恢復信號
                     end
                   player_hit = 0; // 重置碰撞檢測信號
                  end
     end 
  end

endmodule

/////綠色掉落物/////
module fallingobject2(input CLK_div4, CLK_div6, Clear, output reg [7:0]position_G, output reg [2:0]SS,output reg get);
 reg[24:0]cnt;
 reg restart;
 always @(posedge CLK_div6) 
  begin
   if(cnt > 7500000)
    cnt <= 25'd0;   
   else
    cnt <= cnt + 1'b1;   
  end  
  
 initial
 begin
  position_G = 8'b10000000;
  SS =cnt%8;
      restart = 0;
  get=0;
 end  
 always @(posedge CLK_div4)
  begin
   if(restart)
    begin
     position_G <= 8'b10000000; 
     SS <=cnt%8;
     restart = 0;
    end
   else 
    begin
     position_G = position_G >> 1;
     if(position_G == 8'b00000000)
     begin 
      restart = 1;
      get = 1;
     end
    end
  end 
endmodule

/////黃色掉落物/////
module fallingobject3(input CLK_div7, CLK_div8, Clear, output reg [7:0]position_Y, output reg [2:0]SS,output reg get);
 reg[24:0]cnt;
 reg restart;
 always @(posedge CLK_div8) 
  begin
   if(cnt > 55000000)
    cnt <= 25'd0;   
   else
    cnt <= cnt + 1'b1;   
  end  
  
 initial
 begin
  position_Y = 8'b10000000;
  SS =cnt%8;
      restart = 0;
  
 end  
 always @(posedge CLK_div7)
  begin
   if(restart)
    begin
     position_Y <= 8'b10000000; 
     SS <=cnt%8;
     restart = 0;
    end
   else 
    begin
     position_Y = position_Y >> 1;
     if(position_Y == 8'b00000000)
      restart = 1;
      get =1;
    end
  end 
endmodule
///////移動物的除頻器//////
module divfreq(input CLK, output reg CLK_div); 
 reg [24:0] Count; 
 always @(posedge CLK) 
  begin 
   if(Count > 7500000) 
    begin 
     Count <= 25'b0; CLK_div <= ~CLK_div; 
    end 
   else 
    Count <= Count + 1'b1;  
  end 
endmodule 

/////藍色掉落物的除頻器/////
module divfreq2(input CLK, output reg CLK_div);
 reg [24:0] Count; 
 always @(posedge CLK) 
  begin 
   if(Count > 2500000) 
    begin 
     Count <= 25'b0; CLK_div <= ~CLK_div; 
    end 
   else 
    Count <= Count + 1'b1; 
  end 
endmodule 

//////移動物和掉落物交替的除頻器//////
module divfreq3(input CLK, output reg CLK_div); 
 reg [24:0] Count; 
 always @(posedge CLK) 
  begin 
   if(Count > 50000) 
    begin 
     Count <= 25'b0; CLK_div <= ~CLK_div; 
    end 
   else 
    Count <= Count + 1'b1; 
  end 
endmodule 

///////////綠色掉落物的除頻器//////////
module divfreq4(input CLK, output reg CLK_div); 
reg [24:0] Count; 
always @(posedge CLK) 
begin 
 if(Count > 2000000) 
 begin 
  Count <= 25'b0; CLK_div <= ~CLK_div; 
 end 
 else 
  Count <= Count + 1'b1; 
end 
endmodule 

////random////blue/////
module divfreq5(input CLK, output reg CLK_div); 
reg [24:0] Count; 
always @(posedge CLK) 
begin 
 if(Count > 123456) 
 begin 
  Count <= 25'b0; CLK_div <= ~CLK_div; 
 end 
 else 
  Count <= Count + 1'b1; 
end 
endmodule 

////random////green////
module divfreq6(input CLK, output reg CLK_div); 
reg [24:0] Count; 
always @(posedge CLK) 
begin 
 if(Count > 654321) 
 begin 
  Count <= 25'b0; CLK_div <= ~CLK_div; 
 end 
 else 
  Count <= Count + 1'b1; 
end 
endmodule 

///////////黃色掉落物的除頻器//////////
module divfreq7(input CLK, output reg CLK_div); 
reg [24:0] Count; 
always @(posedge CLK) 
begin 
 if(Count > 3000000) 
 begin 
  Count <= 25'b0; CLK_div <= ~CLK_div; 
 end 
 else 
  Count <= Count + 1'b1; 
end 
endmodule 

////random////yellow////
module divfreq8(input CLK, output reg CLK_div); 
reg [24:0] Count; 
always @(posedge CLK) 
begin 
 if(Count > 355555) 
 begin 
  Count <= 25'b0; CLK_div <= ~CLK_div; 
 end 
 else 
  Count <= Count + 1'b1; 
end 
endmodule 
/////倒數的除頻器//////
module divfreq10(input CLK, output reg CLK_div); 
 reg [24:0] Count; 
 always @(posedge CLK) 
  begin 
   if(Count > 10000000) 
    begin 
     Count <= 25'b0; CLK_div <= ~CLK_div; 
    end 
   else 
    Count <= Count + 1'b1;  
  end 
endmodule 


module divfreq11(input CLK, output reg CLK_div);
  reg [29:0] Count;
  always @(posedge CLK)
    begin
    if(Count > 75000000)
      begin
        Count <= 30'b0;
        CLK_div <= ~CLK_div;
      end
    else
      Count <= Count + 1'b1;
    end
endmodule
