# 音樂頻譜網頁效果

1. 使用createjs來進行聲音的處理跟畫面的效果
2. Easekjs + Soundjs
3. Soundjs 載入音樂，抓音頻
4. Easekjs 繪製線條圖

##### 範例 <https://mikecheng1208.github.io/MusicVisualization/index.html>
### 獲取音頻
```javascript
    var analyserNode;                                               //可視化音頻的節點
    var freqByteData;                                               //數組從analyserNode檢索數據
    
    var context = createjs.Sound.activePlugin.context;              //獲取聲音。
    analyserNode = context.createAnalyser();                        //抓取音頻節點
    analyserNode.fftSize = 2048;                                    //多少頻譜(2的次方)
    analyserNode.connect(context.destination);                      //連接到音頻節點，輸出音頻
                
    //壓縮節點(降低了信號的最響亮的部分，當多個播放聲音防止失真)
    var dynamicsNode = createjs.Sound.activePlugin.dynamicsCompressorNode;	
    dynamicsNode.disconnect();                                      //指定斷開連接
    dynamicsNode.connect(analyserNode);                             //連接節點
            
    freqByteData = new Uint8Array(analyserNode.frequencyBinCount);  //將音頻的每個節點數據丟入Uint8陣列
```

### 當更新畫面時
```javascript
    analyserNode.getByteFrequencyData(freqByteData);                //將當前的音頻資料複製到 Uint8Array
    console.log(freqByteData);                                      //輸出音頻節點
```


所有的程式都有下註解，可以直接看
