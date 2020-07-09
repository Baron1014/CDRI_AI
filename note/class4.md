# AI 深度學習實戰(07/09)
###### tags: `AI深度學習實戰`
---

## Module
- 若要將資料夾視為模組，要在資料夾下加上`__init__.py`

## [YOLOv3](https://github.com/wizyoung/YOLOv3_TensorFlow)
- parse_anchors 把輸入物件轉成numpy array

## NLP 常被提及的領域
- 自然語言理解(NLU)，即讓AI了解語文的意思
- 自然語言生成(NLG)，即讓AI能自動產生自然語言

## Bag of Words
- 讀完語料庫，並將字詞轉為向量
- label encoding → one hot encoding
- 需將輸入中文改為以空白連接  
EX: "我 想 打籃球"
- vect.vocabulary_ 與料庫總共有幾個單字

## Bag of Words問題
- 雖然可以把文字很快轉成向量，但對電腦來說無法理解文字的意思
- 浪費儲存空間
- 字詞之間的向量沒有關係

## Word2vec 常見應用
- 文章分類
- 文章關鍵字抓取
- 聊天機器人

## skip-gram
- 是基於神經網路的Word2vec模型
- 核心思想是給定目標字的情況下，去預測上下的字
- 換句話說，某些字如果常出現相同的上下字，那麼這些字可能是相似的
- skip-gram 的作法主要是先建立一個只有一個隱藏層的神經網路
- 隱藏層沒有激活函數  
這樣設計是為了讓模型學到的字向量之間，擁有線性關係
- 需先決定window大小  
若window為2，輸入[I am a tall boy]則會生成  
[I a]  
[am a]  
[tall a]  
[boy a]  

## skip-gram 實作上的問題
- 如果損失函數選擇為cross-entropy，會遇到前面的softmax層計算量非常大
- 需改為sample softmax  
假設輸出有10000輸出元，sample softmax會透過label找到答案，並在隨機挑幾個輸出元做softmax，以降低計算量

## Collection.Counter(words).most_common()
- 計算words裡總共出現的次數

## generate_batch(batch_size, num_skips, skip_window)
- batch_size 一次幾個字
- num_skips widow挑出來後，隨機挑幾個看  
EX: widow=2, skip最多只能為4，因為widow為2最多只有四種組合，若skip為3則在widow四個組合挑出3個
- skip_window 對目標文字，往前及往後的字元，形成組合

## RNN文字產生器
- 字元模型  
一個字元一個字元將小說輸入到網路裏面去學習字源之間的機率分部

## [Stack & UnStack](https://blog.csdn.net/weixin_35718886/article/details/79013372)

## RNN 網路種類應用
- many to one  
EX: 電影影評分類
- many to many  
EX: 語言翻譯

## [Python arbitrary argument (不定常引數)](https://beginnersbook.com/2019/06/python-function-arguments-default-keyword-and-arbitrary/)
- zip(*exmaple)

## np.rnadom.permutation
- shuffled(洗牌概念)
目的讓每次的batch內容，盡量均勻
- 使用後，輸入的list元素將會隨機重新置換  
EX: np.rnadom.permutation([2,0,1]) = [1,2,0]

## Evaluation
- 測試時，不能使用dropout，不然訓練資料會變少

## LSTM 
- 主要多了RNN三種閘門Input-gate、output-gate、forget-gate

## 正規表示式
- [^] 不包含
- '([^\s\w]|_|[0-9]+)' 不包含空白、文字或_及數字

## RNN進階應用
- 機器翻譯原理
Encoder → Decoder
- 圖像生成描述
- 語音辨識