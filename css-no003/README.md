# ✏ **CSS切版筆記 - 『金魚切版系列: 人員介紹卡片 NO003  』**

![]()



## **切版知識點與技巧補充:**
* [三角形製作方式](https://youtu.be/Dn75bi1OG6k)
* [區塊尺寸怎麼算](https://youtu.be/MV9_P6klL-Q)
* [CSS absolute 絕對定位](https://www.youtube.com/watch?v=JOdZdHnuGmM)
* [CSS relative 相對定位](https://www.youtube.com/watch?v=Rukgrh1HlZg)
* [transition 動畫的做法](https://www.youtube.com/watch?v=kR6JpIGJDBQ)
* [flex-direction 的原理](https://www.youtube.com/watch?v=_nCBQ6AIzDU&t=1702s)



## **HTML 架構**
首先先建構三欄式的卡片架構內容
```html
   <div class="wrap">
        <div class="card">
            <img class="card-img" src="https://i.imgur.com/sFDjzmC.jpg" alt="picture"></img>
            <div class="card-body">
                <h2 class="card-title">Amos</h2>
                <p class="card-text">現任 Youtube CSScoke 頻道直播主，不定時更新影片和分享業界實務技巧與經驗，趕快斗內支持一下吧!</p>
            </div>
        </div>
        <div class="card">
            <img class="card-img" src="https://i.imgur.com/nnuSogX.jpg" alt="picture"></img>
            <div class="card-body">
                <h2 class="card-title">css可樂</h2>
                <p class="card-text">一個優質的技術型Youtube 頻道，宗旨在讓更多網路新手跳坑學習網站開發技術，運用淺顯易懂的教學方式讓新手跨進網業領域。</p>
            </div>
        </div>
        <div class="card">
            <img class="card-img" src="https://i.imgur.com/79lYMBf.jpg" alt="picture"></img>
            <div class="card-body">
                <h2 class="card-title">推坑大魔王</h2>
                <p class="card-text">不是路不平，而是坑太多，閒暇看到好東西時就會推坑給周遭朋友，不管是好物或好書，看似抽傭抽很大卻是一毛不取唷!!</p>
            </div>
        </div>
    </div>
```



## **SCSS 樣式**

* 基本卡片架構樣式製作
  >先建構排版架構及基本樣式設定

![](https://i.imgur.com/B0fXFaV.jpg)

```scss
.wrap {
    width: 1200px;
    display: flex;
    margin: 0 auto;
}

.card {
    width: 374px;
    margin: 0 12px;
    text-align: center;
    background: #fff;
    border: 1px solid #fff;
    .card-img {
        width: 100%; // 圖片滿寬於父層 .card
        vertical-align: middle; // 清除圖片下方多餘空間
    }

    .card-title {
        border-bottom: 1px solid gray;
        padding-bottom: 4px;
        margin-bottom: 4px;
        font-weight: 900;
    }

   .card-text {
      line-height: 1.5;
      font-weight: 300;
   }

  // .card-body 文字內容區塊
  .card-body {
      padding: 20px;
    }
}
```
* 製作三角形遮罩
  練習重點是使用利用`偽元素::before`的做法製作三角形遮罩
  - 三角形遮罩先在`card-body`內呈現，所以要`card-body`使用`偽元素::before`設定`相對定位，並在父層`card-body`設定`絕對定位`。
  - 設定寬度及高度為0，並固定在左上方當起點，利用`border-top`先把三角形頂點用高度撐開，再製作三角形兩邊斜角長度，設定斜角長度為`card-body`寬度的一半，並要扣掉兩邊邊框1px。
  - 在 `card-body` 中背景是白色，所以左右邊線條也給白色，因為要做成三角形的缺角，故頂點的線條顏色使用無色(transparent)。
  - 最後使三角形頂點其對齊圖片下方，使用位移 transform: translateY(-100%);
  
```scss
 .card-body {
      padding: 20px;
      position: relative;
    //   三角形蓋板製作
      &::before {
          content: '';
          //設定絕對定位後會自動轉型成區塊元素
          position: absolute; 
          width: 0;
          height: 0;
          left: 0;
          top: 0;
          // 將 border-top 改成 50px高度 的透明三角形
          border-top: 50px solid  transparent;
          // 兩側 三角形斜邊長改成 `card` 寬度 374px 的一半 再扣掉兩邊 1公分實線寬
          border-left: 186px solid #fff;
          border-right: 186px solid #fff;
          // 向上位移 -100% 的位置
          transform: translateY(-100%);
      }
    }
```

* hover 互動效果
  >添加互動效果樣式，讓網頁更加生動活潑
```scss
   .card {
    width: 374px;
    margin: 0 12px;
    text-align: center;
    background: #fff;
    border: 1px solid #fff;
    // 卡片位移設定
    transform: translateY(0px);
    transition: 0.5s;
    cursor: pointer;
    //  卡片位移效果
    &:hover {
        transform: translateY(-50px);

         // 換色效果，卡片(父層)被hover，子層(.card-body::after)做動作(換色)
         //漸層從下到上
        .card-body {
          background-image: linear-gradient(0deg,lightsalmon,orange);
        }

        .card-body::before {
            border-left: 186px solid orange;
            border-right: 186px solid orange;
        }
    }
     
    .card-body {
        padding: 20px;
        position: relative;
        //   三角形蓋板製作
        &::before {
            content: "";
            //設定絕對定位後會自動轉型成區塊元素
            position: absolute;
            width: 0;
            height: 0;
            left: 0;
            top: 0;
            // 將 border-top 改成 50px高度 的透明三角形
            border-top: 50px solid transparent;
            // 兩側 三角形斜邊長改成 `card` 寬度 374px 的一半 再扣掉兩邊 1公分實線寬
            border-left: 186px solid #fff;
            border-right: 186px solid #fff;
            // 向上位移 -100% 的位置
            transform: translateY(-100%);
        }
    }

    .card-img {
        width: 100%; // 圖片滿寬於父層 .card
        vertical-align: middle; // 清除圖片下方多餘空間
    }

    .card-title {
        border-bottom: 1px solid gray;
        padding-bottom: 4px;
        margin-bottom: 4px;
        font-weight: 900;
    }

    .card-text {
        line-height: 1.5;
        font-weight: 300;
    }
}
```



## **練習程式碼**
  * [codepen](https://codepen.io/pohxiqqo/full/MWOMeNp)

  

## **參考資料出處**:
---
* [金魚都能懂的這個網頁畫面怎麼切 : 人員介紹卡片](https://ithelp.ithome.com.tw/articles/10217278)
* [金魚都能懂的網頁切版 : 人員介紹卡片 NO003 | 切版教學 | HTML教學 | 網頁教學 | 網頁切版](https://www.youtube.com/watch?v=2Qs0EuqJIYA&t=1s)

