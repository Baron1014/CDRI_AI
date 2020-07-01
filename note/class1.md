# AI深度學習實戰 (07/01)

###### 上課筆記
## Numpy
### Indexing & Slicing
![](./img/Numpy1.jpg)

### Boolean index(Mask)
- Find the elements of a that are bigger than 2：
```javascript=0
a = np.array([[1,2], [3, 4], [5, 6]])
bool_idx = (a > 2)
print(bool_idx)
print(a[bool_idx]) 
```
[[False False]
 [ True  True]
 [ True  True]]
 
[3 4 5 6]

- array & as array
```javascript=4
arr1 = np.ones((3,3))
arr2 = np.array(arr1)
arr3 = np.asarray(arr1)
arr1[1] = 2
```
> arr1 = [[1,1,1],[1,1,1],[1,1,1]]
>
> arr2 = [[1,1,1],[2,2,2],[1,1,1]]
>
> arr3 = [[1,1,1],[1,1,1],[1,1,1]]

==array為copy，而asarray則為View的型態==

### Fancy index
```javascript=8
a = np.arange(10,20)
b = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
print(a)
print(a[[1,5,8]])
print(b)  
print(b[:,[1,3]])
```
> a = [10 11 12 13 14 15 16 17 18 19]
> 
> a[[1,5,8]] = [11 15 18]
> 
> b=[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
>
> b[:,[1,3]] = [[ 2  4][ 6  8][10 12]]


### [Broadcasting](https://jakevdp.github.io/PythonDataScienceHandbook/02.05-computation-on-arrays-broadcasting.html)
- newaxis
```javascript=14
a = np.arange(3)
b = np.arange(3)[:, np.newaxis]

print(a)
print(b)
print(a+b)
```
>a = [0 1 2]
>
>b = [[0][1][2]]
>
>a+b = [[0 1 2]
 [1 2 3]
 [2 3 4]]

==np.newaxis為新增維度的功能，用途等同於reshape==

- ndim & matrix_rank 
```javascript=20
a = np.array([1,2,3])
print(a.shape, a.ndim, np.linalg.matrix_rank(a))
b = np.array([[1,2,3],[4,5,6]])
print(b.shape, b.ndim, np.linalg.matrix_rank(b))
```
>(3,) 1 1
>
>(2, 3) 2 2

==ndim功能為判斷維度；linalg.matrix_rank能計算有幾個線性獨立==
> 若b為[[1,2,3],[4,5,6]]經過linalg.matrix_rank則會為2
> 
> 若b為[[1,2,3],[2,4,6]]經過linalg.matrix_rank則會因為`共線性`而為1

- 多維度的運算需注意事項
> ==將對應的兩個array維度對應只能為相同值 or 0 or 1==
> 
> 以下有兩個皆為五個維度的物件
> 
>- [x] (4,2,7,3,2)
> (1,2,7,3,0)
> 
>- [ ] (4,2,7,3,2)
>(1,3,7,3,0) 
>*{- 第二個元素中為2及3，維度不符合規格，因此會報錯 -}*

###### 以下為Demo 範例
> This note is yours, feel free to play around.  :video_game: 
> Type on the left :arrow_left: and see the rendered result on the right. :arrow_right: 

## :memo: Where do I start?

### Step 1: Change the title and add a tag

- [x] Create my first HackMD note (this one!)
- [ ] Change its title
- [ ] Add a tag

:rocket: 

### Step 2: Write something in Markdown

Let's try it out!
Apply different styling to this paragraph:
**HackMD gets everyone on the same page with Markdown.** ==Real-time collaborate on any documentation in markdown.== Capture fleeting ideas and formalize tribal knowledge.

- [x] **Bold**
- [ ] *Italic*
- [ ] Super^script^
- [ ] Sub~script~
- [ ] ~~Crossed~~
- [x] ==Highlight==

:::info
:bulb: **Hint:** You can also apply styling from the toolbar at the top :arrow_upper_left: of the editing area.

![](https://i.imgur.com/Cnle9f9.png)
:::

> Drag-n-drop image from your file system to the editor to paste it!

### Step 3: Invite your team to collaborate!

Click on the <i class="fa fa-share-alt"></i> **Sharing** menu :arrow_upper_right: and invite your team to collaborate on this note!

![permalink setting demo](https://i.imgur.com/PjUhQBB.gif)

- [ ] Register and sign-in to HackMD (to use advanced features :tada: ) 
- [ ] Set Permalink for this note
- [ ] Copy and share the link with your team

:::info
:pushpin: Want to learn more? ➜ [HackMD Tutorials](https://hackmd.io/c/tutorials) 
:::

---

## BONUS: More cool ways to HackMD!

- Table

| Features          | Tutorials               |
| ----------------- |:----------------------- |
| GitHub Sync       | [:link:][GitHub-Sync]   |
| Browser Extension | [:link:][HackMD-it]     |
| Book Mode         | [:link:][Book-mode]     |
| Slide Mode        | [:link:][Slide-mode]    | 
| Share & Publish   | [:link:][Share-Publish] |

[GitHub-Sync]: https://hackmd.io/c/tutorials/%2Fs%2Flink-with-github
[HackMD-it]: https://hackmd.io/c/tutorials/%2Fs%2Fhackmd-it
[Book-mode]: https://hackmd.io/c/tutorials/%2Fs%2Fhow-to-create-book
[Slide-mode]: https://hackmd.io/c/tutorials/%2Fs%2Fhow-to-create-slide-deck
[Share-Publish]: https://hackmd.io/c/tutorials/%2Fs%2Fhow-to-publish-note

- LaTeX for formulas

$$
x = {-b \pm \sqrt{b^2-4ac} \over 2a}
$$

- Code block with color and line numbers：
```javascript=16
var s = "JavaScript syntax highlighting";
alert(s);
```

- UML diagrams
```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
Note left of Alice: Alice responds
Alice->Bob: Where have you been?
```
- Auto-generated Table of Content
[ToC]

> Leave in-line comments! [color=#3b75c6]

- Embed YouTube Videos

{%youtube PJuNmlE74BQ %}

> Put your cursor right behind an empty bracket {} :arrow_left: and see all your choices.

- And MORE ➜ [HackMD Tutorials](https://hackmd.io/c/tutorials)
