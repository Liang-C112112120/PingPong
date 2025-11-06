# PingPong
乒乓球遊戲
  
雙人對打，使用兩顆按鈕與八顆LED燈，LED燈移動至最末端，對應的玩家要按下按鈕打擊回去。  
提早按下按鈕或沒按下按鈕都會讓對方加一分，得分時會在得分的那方顯示四顆LED。  

狀態機設計，定義了四種狀態(MovingR, MovingL, Lwin, Rwin)  
S0(MovingR)：LED右移。  
S1(MovingL)：LED左移。  
S2(Lwin)：當右方玩家提早打或漏接時，左方玩家得分。  
S3(Rwin)：當左方玩家提早打或漏接時，右方玩家得分。  

將led_p process改成Mealy狀態機，並且使用除頻過的時脈。  
進入led_p時，會將state存進prev_state裡面，用來比對上一個狀態與目前的狀態LED要如何變化。  
如果全部都用最高速的系統時脈，會讓FSM更新太快導致LED移動有問題，而且LED在實體FPGA板上會全亮，無法觀察。  
  
設計情境：左方發球 -> 右方接球 -> 左方提早打，右方得分並發球 -> 左方接球 -> 右方提早打，左方得分並發球 -> 右方漏接，左方得分並發球 -> 右方接球 -> 左方漏接，右方得分，結束  
模擬結果：  
<img width="1366" height="539" alt="sim" src="https://github.com/user-attachments/assets/fd823e9e-3203-42ea-acd8-9f680e6d83ac" />

