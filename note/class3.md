# AI 深度學習實戰(07/08)

## 上周複習
- Optimizer為將loss function最小化
- tf.argmax 得出最大預測的索引值
- tf.equal 得出預測的boolean
- tf.cast  
True→1  
False→0
- tf.reduce_mean 按照資料長度取平均


## 梯度消失
- sigmoid在做backpropagation，會導致前面Dense的權重會越來越小

## 正則化
- 不等於normolize
- 要將W最小化
- L1/L2為正則項  
L1 為取絕對值  
L2 為取平方根號
- 新的loss = loss(MSE、Cross Entropy) + 正則項
- 做完正則化，收斂會比較快

## Feature Scaling
- FC = Input * Weight
- FC→batch normalize→激活函數→FC→batch normalize→激活函數

## CNN
- 上一層有幾個feature kernel，下一層深度就為多少
- [CNN概念](https://cs231n.github.io/convolutional-networks/)
- 長:寬公式 Output = ((W-k+2p)/s) +1
- 若padding = same 公式則改為W/S
- 若CNN不準，可以試以下方法
1. 把Maxpooling拿掉
2. 增加Epoch，讓機器多看幾次
3. 取消正則化(regularization)，因為正則化是防止模型overfitting

## Maxpooling 
- 進行資料壓縮
- 若電腦較好，可以不用使用，效果會比有加還好
- strides為步伐(1,水平移動步數,垂直移動步數,1)

## AlexNet
- 將神經網路疊了8層
- 使用reluru激活函數而非sigmoid
- 使用dropout
- 使用maxpooling而非meanpooling
- 使用資料增強技巧(翻轉、隨機裁切)

## VGG
- 神經網路越深越準
- 1X1的捲機運算是有用的

## ResNet
- 神經網路152層
- 會有 Degradation Problem  
若層數疊到一定深度，準確率會開始下降 

## YOLO
- onestage  
將兩者合再一起
- twostage  
一部分物件選取，一部分物件辨識
- 將照片分為一格一格的格子
- 針對每個格子要給一組標籤
- [搞懂YOLO看這篇就夠了!](https://www.twblogs.net/a/5c94fb50bd9eee35fc1602f6)
- [Labeling tool](https://github.com/tzutalin/labelImg)
- 