# Scara RL 教學文件 1

* * *

## 大綱

1. 基礎指令解釋
2. 基礎程式邏輯教學
3. 實例程式
    1. 快速ㄇ字往返
    2. DMV 四點定位取物

* * *

# 基礎指令解釋

## 基本設定

[Image: https://quip.com/-/blob/TMZAAA8imWo/Dz0Rgua8yg7Aai8i9zMiOw]
```lua
-- 影響 MovP, MovJ 的動作指令
AccJ(100) -- 加速度百分比,可輸入範圍為 1~100,不可輸入浮點數
DecJ(100) -- 減速度百分比,可輸入範圍為 1~100,不可輸入浮點數
SpdJ(100) -- 最高速百分比,可輸入範圍為 1~100,不可輸入浮點數

-- 影響 MovL、 MArchL、MArc、MCircle 的動作指令
AccL(25000) -- 實際速度毫米/秒平方(mm/s2),可輸入範圍為 1~25000
DecL(25000) -- 實際速度毫米/秒平方(mm/s2),可輸入範圍為 1~25000
SpdL(25000) -- 實際速度毫米/秒平方(mm/s2),可輸入範圍為 1~25000

-- 「HIGH」到位精度最高;
-- 「STANDARD」到位精度標準;
-- 「MEDIUM」到位精度一般;
-- 「ROUGH」到位精度較低;
Accur("HIGH")

```

### Ex. 今天要先設定速度、加速度、減速度再去做動作

```
-- MovP 版本
AccJ(90)
DecJ(80)
SpdJ(100)
MovP("MyFirstPoint")
```

### Ex. 今天要先設定速度、加速度、減速度再去做動作

```
-- MovL 版本
AccL(25000)
DecL(20000)
SpdL(10000)
MovL("MyFirstPoint")
```

## 點位指令

```
-- ReadPoint 讀取點位
PostionX=ReadPoint(1001,"X") -- 讀取 Index 1001 點位的 X 座標值
PostionY=ReadPoint(1001,"Y") -- 讀取 Index 1001 點位的 Y 座標值
PostionZ=ReadPoint(1001,"Z") -- 讀取 Index 1001 點位的 Z 座標值
PostionRZ=ReadPoint(1001,"RZ") -- 讀取 Index 1001 點位的 RZ 座標值
PostionH=ReadPoint(1001,"H") -- 讀取 Index 1001 點位的手系資訊
PostionX1=ReadPoint("P1","X") -- 讀取 P1 點位的 X 座標值
PostionY1=ReadPoint("P1","Y") -- 讀取 P1 點位的 Y 座標值
PostionZ1=ReadPoint("P1","Z") -- 讀取 P1 點位的 Z 座標值
PostionRZ=ReadPoint("P1","RZ") -- 讀取 P1 點位的 RZ 座標值
PostionH1=ReadPoint("P1","H") -- 讀取 P1 點位的手系資訊
```

```
-- WritePoint 寫入點位
WritePoint(1001,"X",300) -- 對 Index 1001 點位的 X 座標值輸入 300毫米(mm)
WritePoint(1001,"Y",50) -- 對 Index 1001 點位的 Y 座標值輸入 50毫米(mm)
WritePoint(1001,"Z",-50) -- 對 Index 1001 點位的 Z 座標值輸入 -50毫米(mm)
WritePoint(1001,"RZ",30) -- 對 Index 1001 點位的 RZ 座標值輸入 30 度
WritePoint(1001,"H",0) -- 對 Index 1001 點位的手系寫入 0
WritePoint("P1","X",250) -- 對 P1 點位的 X 座標值輸入 250毫米(mm)
WritePoint("P1","Y",50) -- 對 P1 點位的 Y 座標值輸入 50毫米(mm)
WritePoint("P1","Z",-100) -- 對 P1 點位的 Z 座標值輸入 -100毫米(mm)
WritePoint("P1","RZ",30) -- 對 P1 點位的 RZ 座標值輸入 30度
WritePoint("P1","H",1) -- 對 P1 點位的手系寫入 1
WritePoint(1002,"X",300.223) -- 對 Index 1002 點位的 X 座標值輸入 300.223毫米(mm)
WritePoint(1002,"Y",50.671) -- 對 Index 1002 點位的 Y 座標值輸入 50.671毫米(mm)
WritePoint(1002,"Z",-50.111) -- 對 Index 1002 點位的 Z 座標值輸入 -50.111毫米(mm)
WritePoint(1002,"RZ",30.456) -- 對 Index 1002 點位的 RZ 座標值輸入 30.456度
WritePoint(1002,"H",0) -- 對 Index 1002 點位的手系寫入 0
WritePoint("P2","X",250.232) -- 對 P2 點位的 X 座標值輸入 250.232毫米(mm)
WritePoint("P2","Y",50.761) -- 對 P2 點位的 Y 座標值輸入 50.761毫米(mm)
WritePoint("P2","Z",-100.105) -- 對 P2 點位的 Z 座標值輸入 -100.105毫米(mm)
WritePoint("P2","RZ",30.222) -- 對 P2 點位的 RZ 座標值輸入 30.222 度
WritePoint("P2","H",1) -- 對 P2 點位的手系寫入 1
```

### ex. Read 點位 跟 write 點位的綜合應用範例

```
-- 假設 FirstPoint 的 X,Y,Z 分別是 100, 50, 80
-- 假設 SecondPoint 的 X,Y,Z 分別是 0, 0, 0

PostionX1 = ReadPoint("FirstPoint","X") -- 讀取 FirstPoint 點位的 X 座標值
PostionY1 = ReadPoint("FirstPoint","Y") -- 讀取 FirstPoint 點位的 Y 座標值
PostionZ1 = ReadPoint("FirstPoint","Z") -- 讀取 FirstPoint 點位的 Z 座標值

PostionX2 = PostionX1 + 100 -- 第二個點位 X 的值是前一個點位的 X 多 100
PostionY2 = PostionY1 + 50 -- 第二個點位 Y 的值是前一個點位的 Y 多 50
PostionZ2 = PostionZ1 - 80  -- 第二個點位 Z 的值是前一個點位的 Z 少 80

WritePoint("SecondPoint", "X", PostionX2) -- 對 SecondPoint 點位的 X 座標值輸入 PostionX2
WritePoint("SecondPoint", "Y", PostionY2) -- 對 SecondPoint 點位的 Y 座標值輸入 PostionY2
WritePoint("SecondPoint", "Z", PostionZ2) -- 對 SecondPoint 點位的 Z 座標值輸入 PostionZ2

-- 這時 SecondPoint 的 X,Y,Z 分別會是 200, 100, 0
```



### EX. MODBUS 跟 read / write point 的綜合應用

```
-- 模擬 MS 從 DMV 讀取目標物座標
-- 使用 DO 夾取目標物
-- 移動到目標座標放置目標物

Flag = False
while Flag == False then  -- 如果 Flag 一直是 False 的話就一直讀取直到 Flag 為 True 為止
  XTemp = ReadModbus(0x1010,"DW")
  YTemp = ReadModbus(0x1012,"DW")
  ZTemp = ReadModbus(0x1014,"DW")
  Flag = ReadModbus(0x1100,"DW") -- 讀取資料傳送 Flag，如果 Flag 回傳 True 代表資料傳送完成
  DELAY (0.1)
end

WritePoint("MyPoint", "X", XTemp)
WritePoint("MyPoint", "Y", YTemp)
WritePoint("MyPoint", "Z", ZTemp)
MovP("MyPoint")
MovPR(-100, "Z")
DO(1, "ON")
MovPR(100, "Z")
MovP("MyTargetPoint")
DO(1, "OFF")
```

### EX. 判斷 IO 之後去繞圈切割

```
-- 判斷 IO 之後去繞圈切割
while true then
  if DI(1) == "ON" then
    MovP("ReadyPoint")
    for i = 1 , 10 do
      MCircle("StartPoint","EndPoint", "BORDER", "PASS")
    end
    MovP("EndPoint")
  end
end

```





## 運動指令

```
-- MovJ 軸移動
MovJ(4,180)
MovJ(4,180,50) -- 第四軸以 50% 的速度移動到正 180 度的位置
MovJ(4,-180,100,10,10) -- 第四軸以加速度為 10%,減速度為 10%,100% 的速度移動到 負 180 度的位置
MovJ(4,18000,”PUU”) --第四軸移動到18000 PUU的位置
MovJ(1,2000,”PUU”,50) --第一軸以50%的速度移動到2000 PUU的位置 MovJ(2,200,”PUU”,30,10,10) --第二軸以加速度為10%,減速度為10%,30%的速度移動到 200 PUU的位置

-- MovP 點對點移動
MovP(1) --- 以點對點方式移動到第一個點位的位置
MovP(2,“PASS”) --- 以點對點連續移動方式移動到第二個點位的位置
MovP(3,100,50,50) --- 以點對點且速度設為 100%,加減速度設為 50% 方式移動到第三個點位
MovP("P1", "PASS",100,50,50) --- 以點對點且連續移動方式,速度設為 100%,加減速度設為50%方式移動,到點位名稱為 1 的位置

-- MovPR 點對點相對移動
MovPR(10,"X") --- 以 PtP 方式相對移動往正 X 方向,移動 10 毫米
MovPR(-10,"X") --- 以 PtP 方式相對移動往負 X 方向,移動 10毫米
MovPR(10,"Y") --- 以 PtP 方式相對移動往正 Y 方向,移動 10毫米
MovPR(10,"Z") --- 以 PtP 方式相對移動往正 Z 方向,移動 10毫米
MovPR(-10,"Z") --- 以 PtP 方式相對移動往負 Z 方向,移動 10毫米
MovPR(10,"RZ") --- 以 PtP 方式相對移動往正 RZ 方向,移動 10 度
MovPR(-10,"RZ") --- 以 PtP 方式相對移動往負 RZ 方向,移動 10 度

-- MovL 絕對座標直線移動
MovL("P1") --- 以 Line 方式移動到第一個點位的位置
MovL(1, "PASS") --- 以 Line 連續移動方式移動到第一個點位的位置
MovL(1,1000,500,500) --- 以 Line 且速度設為 1000毫米/ 秒(mm/s),加減速度設為 500毫米/秒平方(mm/s2) 方式移動, 到點位名稱為 1 的位置
MovL("P1", "PASS",1000,500,500) --- 以 Line 且連續移動方式,速度設為 1000毫米/秒(mm/s),加減速度設為 500毫米/ 秒平方(mm/s2) 方式移動,到點位名稱為 1 的位置

-- MovLR 以相對方式進行直線移動
MovLR(10,"X") --- 以直線方式相對移動往正 X 方向,移動 10 毫米
MovLR(-10,"X") --- 以直線方式相對移動往負 X 方向,移動 10 毫米
MovLR(10,"Y") --- 以直線方式相對移動往正 Y 方向,移動 10 毫米
MovLR(10,"Z") --- 以直線方式相對移動往正 Z 方向,移動 10 毫米
MovLR(-10,"Z") --- 以直線 P 方式相對移動往負 Z 方向,移動 10 毫米 6. MovLR (10,"RZ") --- 以直線方式相對移動往正 RZ 方向,移動 10 度
MovLR(-10,"RZ") --- 以直線方式相對移動往負 RZ 方向,移動 10 度

-- 以絕對座標方式進行弧線運動
MArc("P1","P2",”BORDER”) -- P1 點為經過點,P2 點為目標點
MArc("P1","P2",”BORDER”,"PASS") -- P1 點為經過點,P2 點為目標點,以連續方式移動
MArc("P1","P2",”BORDER”,100) -- P1 點為經過點,P2 點為目標點,速度為 100毫米/ 秒(mm/s)
MArc("P1","P2",”BORDER”,"PASS",100) -- P1 點為經過點,P2 點為目標點,速度為 100毫米/ 秒 (mm/s) 且以連續方式移動
MArc("P1","P2",”BORDER”,”PASS”,100,100,100) -- P1 點為經過點,P2 點為目標點,速度為100 毫米/ 秒(mm/s) ,加速度為 100毫米/ 秒平方(mm/s2) ,減速度 100毫米/秒平方(mm/s2) ,且以連續 方式移動

-- 以絕對座標方式進行圓形運動,三點成圓
MCircle("P1","P2",”BORDER”) --P1 點為經過點,P2 點為目標點
MCircle("P1","P2",”BORDER”,"PASS") --P1 點為經過點,P2 點為目標點,以連續方式移動
MCircle("P1","P2",”BORDER”,100) --P1 點為經過點,P2 點為目標點,速度為 100毫米/ 秒
MCircle("P1","P2",”BORDER”,"PASS",100) --P1 點為經過點,P2 點為目標點,速度為毫米/秒(mm/s) (mm/s) 且以連續 方式移動
MCircle("P1","P2",”BORDER”,"PASS",100,100,100) --P1 點為經過點,P2 點為目標點,速 度為 100毫米/ 秒(mm/s) ,加速度為 100毫米/ 秒(mm/s2) ,減速度 100毫米/ 秒(mm/s2),且 以連續方式移動

-- Lift
Lift("P0",45,10,90) –以P0點為參考點,移動到以該參考點位置上升角度45度,上升高度10公釐,上升 方向90度的位置
```



## IO 通訊

```
-- 輸入
DI(n)
-- 輸出
DO(n,s,t)

if DO(1) == "ON" then
  DO(1,"OFF") --Let first DO Off
end

if DO(1) == "OFF" then
  DO (1,"ON") --Let first DO On
end

DO (1,"ON",1) --Let first DO On for one second
```



## Modbus 通訊

```
-- ReadModbus 此為與外部構通指令,用於讀取記憶體位置的值,可讀取的記憶位址為 0x1000~0x1FFF,總共 4096 個 word 可使用,以 Double word 的長度來做讀取資料時,欲讀取的記憶體位址須為雙數,才可以做讀 取的 動作
-- WriteModbus 此為與外部構通指令,用於寫入記憶體位置的值,可寫入的記憶位址為 0x1000~0x1FFF,總共 4096 個 word 可使用,以 Double word 的長度來做寫入資料時,欲寫入的記憶體位址須為雙數,才可以做寫 入的 動作

readModbus_0x1000=ReadModbus(0x1000,"W")

if readModbus_0x1000 == 1 then
  WriteModbus(0x1F00,"DW",2)
  DELAY (0.1)
end

readModbus_0x1F00=ReadModbus(0x1F00,"DW")

```


* * *

# 基礎程式邏輯教學

## 註解

```
-- 這些程式都不會執行，只是給人看的
-- 這些程式都不會執行，只是給人看的

MovP(1001) -- MovP 會執行，但是這段文字不會被執行
-- MovP(1002) 這邊 MovP 不會被執行

```

## IF...ELSE

```
if DI(1) == "ON" then
  -- 如果 DI1 是 ON 的話做這些事
else
  -- 如果 DI1 不是 ON 的話做這些事
end
```

## IF..ELSEIF..ELSE

```
-- 一般邏輯判斷
if DI(1) == "ON" then
  -- 如果 DI1 是 ON 的話做這些事
elseif DI(2) == "ON" then
  -- 如果 DI1 不是 ON 但是 DO2 是 ON 的話做這些事
else
  -- 如果都不是的話做這些事
end



-- Modbus 交握
command = ReadModbus(0x1000,"W")
if command == 1 then
  -- 如果 command 是 1 的話做這些事
elseif command == 2 then
  -- 如果 command 是 2 的話做這些事
elseif command == 3 then
  -- 如果 command 是 3 的話做這些事
elseif command == 4 then
  -- 如果 command 是 4 的話做這些事
else
  -- 如果都不是的話做這些事
end
```

## While 迴圈

```
a=10
while( a < 20 ) do -- 當 a 小於 20 時執行
   MovPR(30, "X")
   DELAY(2)
   a = a + 1
end
-- 控制 Scara 逐次往正Ｘ方向移動，每次移動 30 mm ，共移動 10 次

while true do -- 永遠執行
   MovPR(30, "X")
   DELAY(2)
end
-- 控制 Scara 一直無限的往正 X 方向移動到跳出極限錯誤為止
```

## For 迴圈

[http://www2.kimicat.com/lua%E6%95%99%E5%AD%B8—%E8%BF%B4%E5%9C%88](http://www2.kimicat.com/lua%E6%95%99%E5%AD%B8%E2%80%94%E8%BF%B4%E5%9C%88)

```
-- for i = 1, 10 的意思是說，建立一個暫時性的變數 i，
-- 它的值從 1 開始，一直加 1 直到 10，重覆執行 do 和 end 之間的程式。
-- 所以，一開始 i 的值是 1，執行 print(i)，接著 i 的值變成 2，再執行 print(i)，
-- 依此類推直到 i 的值是 10 為止。因此，上面的程式，會印出 1 至 10 之間的數字。
for i = 1, 10 do
  print(i)
end


-- 以下程式 i 會從 2 執行到 5
-- 每次執行時會執行裡面的程式
-- 宣告一個變數 distance 為 20 乘上 i 然後控制機器人往正 X 方向移動該距離
-- 所以總共每次會分別移動 40, 60, 80, 100 mm 的距離
for i = 2, 5 do
  distance = 20*i
  MovPR(distance, "X")
  DELAY(2)
end
```

## 補充：更多 LUA 程式語言

http://www.runoob.com/lua/lua-tutorial.html
* * *

# 實例程式

## 1.快速ㄇ字往返

```
-- 要先在點位配置配置四個點位: 1001, 1002, 1003, 1004
-- 以此案例：
-- 1001(50, -100, -100)
-- 1002(50, -100, -50)
-- 1003(50, 100, -50)
-- 1004(50, 100, -100)

RobotServoOff()
RobotServoOn()

-- 設定速度、加速度、減速度，我們這邊要用 MovP 的
AccJ(100)
DecJ(100)
SpdJ(100)

MovP(1001) -- 都先到第一個點
while true do -- 無限循環ㄇ字型往返
  MovP(1002)
  MovP(1003)
  MovP(1004)
  MovP(1003)
  MovP(1002)
  MovP(1001)
end
```

## 2.DMV 四點定位取物

```
RobotServoOff()
RobotServoOn()

SpdJ(30.0)
AccJ(30.0)
DecJ(30.0)

-- 初始化讓 Robot 到原點，讓 DMV 照得到可視範圍
MovP("Origin")

-- 透過 IO 去觸發 DMV 拍照，取得圖片資料並且執行四點定位
DO(1, "OFF")
DO(1, "ON")

-- 將 DMV 透過 Modbus 傳過來的 X, Y 位置存到變數中
ComFlag = ReadModbus (0x1100, "DW") -- DMV 完成旗標
TmpFlag = 0
while TmpFlag == 0 do -- 在 TmpFlag 完成前不斷執行交握
    if ComFlag == 1 then  --當 DMV 完成旗標為 1 時執行交握
        X1 = ReadModbus(0x1000, "DW")/1000
        Y1 = ReadModbus(0x1002, "DW")/1000
        X2 = ReadModbus(0x1004, "DW")/1000
        Y2 = ReadModbus(0x1006, "DW")/1000
        TmpFlag = 1 -- 交握完將 TmpFlag 設定成 1 後，下次迴圈就不再執行
    end
end
-- 將 X1, Y1 寫入 P1 點位中
WritePoint("P1", "X", X1)
WritePoint("P1", "Y", Y1)
WritePoint("P1", "Z", -120)
WritePoint("P1", "RZ", 0)
WritePoint("P1", "H", 0) --*to confirm specific difference between right vs. left

-- 將 X2, Y2 寫入 P2 點位中
WritePoint("P2", "X", X2)
WritePoint("P2", "Y", Y2)
WritePoint("P2", "Z", -120)
WritePoint("P2", "RZ", 0)
WritePoint("P2", "H", 0) --*to confirm specific difference between right vs. left

-- 試著前往點位1跟點位2
if X1 ~= 0 then
    MovP("P1")
    MovP("Origin")
end
if X2 ~= 0 then
    MovP("P2")
    MovP("Origin")
end


```

## 3.DMV 四點定位取物 ( SMAC USB )

[Image: https://quip.com/-/blob/TMZAAA8imWo/7k_wsu-4hBeiapIt0PG75A]
```
SpdJ(95.0)
AccJ(95.0)
DecJ(95.0)
tempX1 = -10000
tempY1 = -10000
tempRz = -10000

while true do
  --Initialize Origin to free camera FoV
  MovP("Origin")

  --Write DMV X & Y coordinate data into SCARA memory
  ComFlag = ReadModbus(0x1100, "DW")
  TmpFlag = 0
  while TmpFlag == 0 do
   if ComFlag == 1 then
    X1 = ReadModbus(0x1000, "DW")/1000
    Y1 = ReadModbus(0x1002, "DW")/1000
    Rz = ReadModbus(0x1004, "DW")/-1000
    TmpFlag = 1
   end
  end



  if( ABS((X1 - tempX1)) <= 10) and(  ABS((Y1 - tempY1))<= 10 ) and (ABS((Rz - tempRz)) <= 10 ) then

  else
    tempX1 = X1
    tempY1 = Y1
    tempRz = Rz
    --Write coordinate data into individual point e.g. P1
    WritePoint("P1", "X", X1)
    WritePoint("P1", "Y", Y1)
    WritePoint("P1", "Z", -150)
    WritePoint("P1", "RZ", Rz)
    WritePoint("P1", "H", 0) --*to confirm specific difference between right vs. left

    WritePoint("P2", "X", X1)
    WritePoint("P2", "Y", Y1)
    WritePoint("P2", "Z", -190)
    WritePoint("P2", "RZ", Rz)
    WritePoint("P2", "H", 0) --*to confirm specific difference between right vs. left

    --Move to Object 1 initial location
    MovP("P1","PASS")
    MovP("P2")
    DO(2, "ON")
    --DELAY(0.1)
    MovP("P1","PASS")
    MovP("TargetUp","PASS")
    MovP("Target","PASS")
    DELAY(0.1)
    DO(2, "OFF")
    DO(3, "ON")

    DELAY(0.05)
    MovP("TargetUp","PASS")
    DO(3, "OFF")
    MovP("Origin")
 end

 DELAY(1)

end
```






