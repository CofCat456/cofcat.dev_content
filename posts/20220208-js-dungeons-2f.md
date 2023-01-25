---
title: 新手 JS 地下城 2F — 時鐘
description: 六角學院 JS 地下城 - 2F 時鐘
slug: js-dungeons-2f
date: 2022-02-08
type: Post
socialImage: https://cdn-images-1.medium.com/max/800/1*l1hApnmk_ZTlJYuRLYAwhg.png
---

### 新手 JS 地下城 2F — 時鐘

![](https://cdn-images-1.medium.com/max/800/1*l1hApnmk_ZTlJYuRLYAwhg.png)

**2F — 時鐘**

> **這篇是六角學院的** [**_JavaScript 題目篇-_** 🐲 **_新手 JS 地下城_**](https://courses.hexschool.com/courses/enrolled/674121)**，**[**2F Boss 關卡「時鐘」**](https://courses.hexschool.com/courses/javascript-js/lectures/12019667)**攻略過程心得。**

順利攻略完第一關後，決定馬上來挑戰一下第二關，這一次還多了特定技術的考驗，既然都踏入地下城了，當然要來挑戰看看囉!

---

#### BOSS 弱點

1.  【特定技術】需使用 JS 原生語法的 `getDate()` 撈取時間，不可用套件
2.  【特定技術】需使用 JS 原生語法的 `setTimeout()` 或 `setInterval()`，持續讓秒針、分針、時針能夠以台北時區移動
3.  【特定技術】介面請全部用 CSS2、CSS3 手寫繪製，什麼…？你說太強人所難？？那..用圖片也不是不行辣， 點選一下元素，右側控制列會有個藍色按鈕，點選 [下載] 即可。

### 解題思路

-   使用 getDate() 來抓取現在時間
-   使用 setInterval() 來持續呼叫函式
-   利用 Vue 概念來加速完成關卡

這一次在挑戰前看了不少其他**同學的作品**，一部分是對這次的關卡沒甚麼掌握度，另一部分也就是那**邪惡的版面**...意外發現大多同學都推薦 **Alex 老師**先前的的 [**_CSS + JS Clock 的教學影片_**](https://www.youtube.com/watch?v=O1YsB3qxO4g)，不僅觀念講得很詳細，甚至可以直接完成這關的挑戰呢~

Alex 老師的頻道有好多 JS 和 Vue 的影片，看起來又發現了新大陸呢!

---

### 畫面處理

![](https://cdn-images-1.medium.com/max/800/1*-fVoz7A19nei7ieSZ1vOww.jpeg)

**2F — 時鐘 設計稿**

雖然這次有提供了設計稿可以直接使用，不過還是決定來挑戰一下自己!

![](https://cdn-images-1.medium.com/max/800/1*VHfU5GhD-0FkhbDTeIgh4w.jpeg)

**2F — 時鐘 BackGround**

首先需要處理的時鐘中的背景，最麻煩的也就是中間的刻度，這裡我使用元件的方式，將內外數字和點拆成三部分來完成。

```javascript
app.component('clock-text', {
	data() {
			return {
				textCss: {
				rotate: '',
				content: '',
				textRotate: '',
			},
		};
	},
	props: ['x'],
	template: `<div class="clock-text" :style="{ 'transform': rotate,
	'--textRotate': textRotate }" :data-text='text'></div>`,
	created() {
		this.rotate = `rotate(${this.x * 30}deg)`;
		this.text = this.x + 12 + '';
		this.textRotate = `rotate(${this.x * -30}deg)`;
	},
});
```

**2F — 時鐘刻度 Component**

```javascript
app.component('clock-stext', {
	data() {
		return {
			textCss: {
				rotate: '',
				stextRotate: '',
			},
		};
	},
	props: ['y'],
	template: `<div class="clock-stext" :style="{ 'transform': rotate,
	'--stextRotate': stextRotate }" :data-stext='y'></div>`,
	created() {
		this.rotate = `rotate(${this.y * 30}deg)`;
		this.stextRotate = `rotate(${this.y * -30}deg)`;
	},
});
```


**2F — 時鐘刻度 Component**

文字部分比較單純，可以直接用 **v-for** 快速處理，再將值用 **props** 傳入進行運算，這裡都是各印出 12 個，比較需要**注意**的有兩個地方。

-   **數字間橘線的部分需要處理**
-   **每個數字位置要計算清楚，以免對不上秒針**
-   **數字呈現時要調整角度讓數字擺正**

首先橘線的部分我是這樣完成的~

![](https://cdn-images-1.medium.com/max/800/1*eA35e3Z4tyNSNZzXMbF93g.jpeg)

**2F — 時鐘 BackGround CSS**

接著再使用偽元素來完成文字，一個圓有 **360 度**，而我們需要放上 12 個數字，所以每放上一個就要增加 **60** 度，如果不懂的話可以看 [**Alex 老師**](https://www.youtube.com/watch?v=O1YsB3qxO4g)講解的影片喔!

比較特別的是，這裡我使用了 attr() 的語法，由於橘線會重複 12 條，使用 v-for 後，將值 * 12 後加在標籤中。

![](https://cdn-images-1.medium.com/max/800/1*ruw6o4J0y16j3PAhvsVGaw.png)

**使用 v-bind 綁定 data-text 的值**

接著在 CSS 中用 **content: attr(data-text)** 來動態切換 **content** 的值!

```css
.clock-text::before {
	content: attr(data-text);
	position: absolute;
	transform: translate(-6px, -20px) var(--textRotate);
}
```

**只要將 data 值 放入 attr() 內就可以使用!**

attr()目前根據 MDN 文件記載，除了 content 以外，其他屬性的使用皆實驗階段。

[詳細請看 MDN 文件](https://developer.mozilla.org/zh-TW/docs/Web/CSS/attr%28%29)

這樣數字就會跑出來了~

![](https://cdn-images-1.medium.com/max/800/1*dw3IJUr0KLe8GxvQqAjA3Q.jpeg)

**2F — 時鐘 BackGround**

接下來要做的是將數字擺正，這裡我使用 CSS 變數來做動態更換。

![](https://cdn-images-1.medium.com/max/800/1*Xt46iW4r_2adNBmu-yJlww.png)

[**詳細可以看卡斯伯老師的文章**](https://w3c.hexschool.com/blog/21985acb)

一樣使用 **v-bind** 的方式來綁定 **style** 就可以達到效果。

而內層數字的方式跟外層不太一樣，我使用在裡投新增一個內圓的方式。

![](https://cdn-images-1.medium.com/max/800/1*Rr2yqDefrIUK4jqD90-FTg.jpeg)

**2F — 時鐘 BackGround**

這樣除了能將文字放到對應的地方，還可以調整**圓的背景色**來**抵銷多餘的橘線**!!!

至於其他部分都和外數字一樣處理就歐給了。

> _貼心提醒 : 裡頭一樣會新增 12 個數字，也就是 12 個內圓，而這每一個內圓會_**_不斷的蓋上前一個圓_**_，所以請另外使用_ **_CSS 選取器_**_來調整第_**_一個圓背景色_**_~如果直接加在_**_每一個圓的 CSS_** _裡面的話，_**_文字可是會被蓋掉的喔_**_!_

以上是卡在這個地方長達一個小時差點懷疑人生的過來人經驗。

點的部分就沒什麼問題了，只要注意**每一個點的角度**跟和**星星**與**數字的位置**，透過 **JS 判斷**就可以完成。

```javascript
app.component('clock-point', {

data() {

return {

textCss: {

pointRotate: '',

startRotate: '',

},

};

},

props: ['z'],

template: `<div v-if='(z % 3 !== 0)' class="clock-point" :style="{ 'transform': pointRotate }"></div>

<div v-else-if='(z % 6 !== 0)' class='star' :style="{ 'transform': pointRotate }">

<div class='star-top'></div>

<div class='star-bottom'></div>

</div>`,

created() {

this.pointRotate = `rotate(${this.z * 5}deg)`;

if (this.z === 1) {

this.startRotate = `rotate(${this.z * 15}deg)`;

} else {

this.startRotate = `rotate(${this.z * 30}deg)`;

}

console.log(this.pointRotate);

},

});
```

**2F — 時鐘刻度 Component**

> 針的部分按照設計稿，使用偽元素就可以了，秒針的部分比較困難，網上有很多大神同學的解法，弱弱的我表示看不懂@@，我是強行拼湊出來的，就不獻醜了~

---

### 時間處理

![](https://cdn-images-1.medium.com/max/800/1*k1f7jVxgBmBnpAZ_UGmQaQ.png)

**2F — 時鐘 Vue Code**

這裡我使用**兩個 _function_**，**抓取時間**後再呼叫另一個function **將時間換成角度**，最後在 **created** 的地方使用 **setInterval()** 設定間隔1秒不斷執行，就大功告成了~

這裡將 **setInterval()** 放在 **mounted()** 中是要確保程式是在元件掛載後再開始執行。

> _除了原本的計算度數以外，_**_額外再增加秒針、分針的執行程度，_**_來讓_**_分針_**_和_**_時針_**_慢慢移動，可以讓時鐘看起來更仿真。_

> _除了_ **_setTimeout()_** _和_ **_setInterval()_** _兩種方式以外，還可以使用這種方式_**_Window.requestAnimationFrame()_** _來完成，不需要設定時間，會隨著使用者硬體的支援頻率來更新畫面~詳細介紹可以參考 Alex 老師的講解和_ [_MDN文件_](https://developer.mozilla.org/zh-TW/docs/Web/API/window/requestAnimationFrame)

> 最後只要傳上 GigHub Page 就完成了挑戰了(灑花)

[完成品 Demo](https://cofcat456.github.io/JS-Dungeons/2F/)

---

### 心得

![](https://cdn-images-1.medium.com/max/800/1*2w8c9L9gYZ92bNlyjWYWCA.jpeg)

Photo by [Samantha Gades](https://unsplash.com/@srosinger3997?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

這次的版面比第一關難上許多，除了要使用 transform 來完成，還第一次用上了 **attr()** 和 **CSS變數** 來完成綁定，算是很實用且意外的收穫!

> 我絕對不會說，我今天才知道原來**偽元素的 content 屬性，原來是可以拿來插入內容**。