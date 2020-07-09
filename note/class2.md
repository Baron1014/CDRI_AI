---
tags: AI深度學習實戰
---

# AI深度學習實戰(07/02)

<!-- Put the link to this slide here so people can follow -->
slide: https://hackmd.io/p/template-Talk-slide

---

書籍推薦：人工智慧導論、選擇的能力

---

## 深度學習常見應用

- 自然語言處理
tf-idf 主要為找出輸入文章中，每篇文章重要的詞
- 圖片描述
YOLO V4 台灣之光
- 圖片風格遷移
GAN算法能夠將一個圖的風格，轉換至我們的Input上

---
## TensorFlow基礎應用
### tensorflow V1
- `placeholder` 等待東西輸入
```javascript=1
//tf.placeholder(指定入資料型態, 指定輸入資料形狀, 幫節點命名)
x = tf.placeholder(tf.float32, shape=(1, 2), name='x')
//以圖片便是為例，當shape為None時，則是待會接受輸入圖片張數
x = tf.placeholder(tf.float32, [None, 784])
```

- `constant` 定義常數節點
- `Variable` 定義變量節點(需賦予初始化值)
※若初始化值賦予不好，會影響最終輸出結果
- `add` 將節點進行相加
- `matmul` 將節點進行相乘
- `run`執行模型
> 開始前需先進行節點的初始化
> `inputarr`為輸入資料
> `feed_dict`為定義X及Y
> 需注意run(out)，`out變量`需與前面接收變量命名不同
```javascript=1
with tf.Session() as sess:
    sess.run(tf.global_variables_initializer())
    inputarr = [[0,0],[0,1],[1,0],[1,1]]
    for i,arr in enumerate(inputarr):
        out_ = sess.run(out, feed_dict={x:[arr]})
        print(f'No{i}',out_)
```
- `Save` 模型儲存
```javascript=1
saver = tf.train.Saver()
with tf.Session() as sess:
    sess.run(tf.global_variables_initializer())
    saver.save(sess, "Saved_model/model.ckpt")
    print(sess.run(result))
```
- `restore` 模型載入
```javascript=1
saver = tf.train.import_meta_graph("Saved_model/model.ckpt.meta")
with tf.Session() as sess:
    saver.restore(sess, "Saved_model/model.ckpt")
    print(sess.run("result:0"))
```
※若是模型沒有載入，則會往前去讀去節點變量，範例如下：
```javascript=1
tf.reset_default_graph()
v1 = tf.Variable(tf.constant(1.0, shape=[1]), name='v1')
v2 = tf.Variable(tf.constant(2.0, shape=[1]), name='v2')
result = v1 + v2
saver = tf.train.Saver()

with tf.Session() as sess:
    saver.restore(sess, "Saved_model/model.ckpt")
    print(sess.run(result))
```

### tensorflow計算符號

| 算法          | tensorflow method          |
| ----------------- |:----------------------- |
|相加|add()|
|相減|sub()|
|相乘|multiply()|
|相除|divide()|
|平方|pow()|
|求餘數|mod()|
|求商數|div()|

### Random Generate Function

| function name | distribution | main parameters | 
| :------: | :------: | :------: | 
| tf.random_normal | normal distribution | mean, std, data type|
| tf.truncated_normal | normal distribution within two std | mean, std, data type|
| tf.random_uniform | uniform distribution | min value, max value, data type|
| tf.random_gamma | gamma distribution | alpha, beta, data type|

### Constant Generate Function

| function name | function | example 
| :------: | :------: | :------: |
| tf.zeros | produce all zeros | tf.zeros([2,1], int32)|
| tf.ones | produce all ones | tf.ones([2,3], int32)|
| tf.fill | produce specific number | tf.fill([2,1], 9)|
| tf.constant | prodcuce a given constant | tf.constant([2.0,1.0])|



### Tensotflow V2
- 與tf1的差別為包的比較完整
- 可以使用`tf.keras`直接呼叫Keras

---

## 損失函數的定義
### 損失函數的種類很多
- Mean Square Error(MSE)→Regression
- Cross-Entropy→Classfication
- Hinge loss

---

#### Entropy
- `資訊含量`的期望值
- 數值越大代表越混亂，越不確定
- 本身機率分部內的比較

#### Cross-Entropy
- 衡量兩個機率分布是否相似
- 數值越大代表越不相似、越小代表越相似
- 兩個機率分部的比較
- `機率分佈1`對`機率分佈2`做Cross-Entropy最小值為`機率分佈1`的Entropy
- `機率分佈2`對`機率分佈1`做Cross-Entropy最小值為`機率分佈2`的Entropy

#### softmax
- 所有出來結果為機率分佈
- 所有值總合為1

==`softmax`→`Entropy`→`Cross-Entropy`==

---

## Optimizer 學習率優化器
### adagrad
- 會考慮之前的梯度值
- 學習率會`decay`(越來越小)

### RMSprop 動量梯度下降
- 考慮前一次的動量梯度
- 學習率為定值

### Adam

---
## [Backward propagation 反向傳播](http://ai-start.com/dl2017/html/lesson1-week2.html#header-n361)

吳恩達深度學習筆記

---