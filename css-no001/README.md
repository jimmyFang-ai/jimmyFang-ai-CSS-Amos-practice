# ✏ **CSS切版筆記 - 『金魚切版系列:  圖文滿版區塊 NO001 』**

![](https://i.imgur.com/LnNnfxt.jpg)

<<<<<<< HEAD
=======
 ![](https://i.imgur.com/LnNnfxt.jpg)
>>>>>>> 20c103952f577ca543099edfacd0bcb8279fa1a4



## **切版知識點與技巧補充:**
* [為何需要reset](https://www.youtube.com/watch?v=WtjXBIyxhw8)
* [inline & block 的作用](https://www.youtube.com/watch?v=TtvQsVjt9t8)
* [flex-direction 的原理](https://www.youtube.com/watch?v=_nCBQ6AIzDU&t=1702s)
* [好想工作室-漸層色彩與多重背景撰寫方式](https://ithelp.ithome.com.tw/articles/10197136)
* vh 單位介紹


## **HTML 架構**
>先建立正確架構，再來撰寫CSS樣式
```html
 <div class="banner">
        <div class="container">
            <div class="bannerText">
                <h1 class="heroTitle">金魚都能懂的
                    <small>跟著AMOS老師學切版</small>
                </h1>
                <h2 class="subTitle">圖文滿版區塊</h2>
                <p>這畫面實在常見，在各種樣版網站可說是設計常客
                    <br>金魚切不出來實在說不過去阿
                </p>
            </div>
        </div>
    </div>
```



## **SCSS 樣式**

  * ###  CSS reset
    > Amos 老師使用這個方式，完成CSS reset，保留原本預設 HTML 標籤的樣式與彈性運用
    >因為實際開發環境上如果使用 reset.css 與 normalize.css，可以針對需求擇一使用即可
     ``` scss
     * {
    margin: 0;
    padding: 0;
    list-style: none;
    };
     ```

  * ### .container
    >設定 container  (RWD)響應式設計，可隨著視窗縮放
    ```scss
    .container {
    width: 100%;
    height: 100%;
    max-width: 1280px;  //RWD(容器最大寬度)偷懶方式
    margin: 0 auto;
    }
     ```
   
  * ### .banner-text
    > 先處理文字內容區塊排版
    ```scss     
    .bannerText {
    height: 100%;
    display: flex;
    flex-direction: column; // 主軸
    justify-content: center; // 與主軸垂直居中
    align-items: flex-start; // 交錯軸設定: 往交錯軸起始點對齊
    .heroTitle {
        font-size: 50px;
        border-bottom: 1px solid #333;
        font-weight: 900;
        color: red;
        small {
            display: block;
            font-size: 40;
            font-weight: 700;
            color: #333;
        };
    };
    .subTitle {
        font-size: 30px;
        font-weight: 700;
        color: red;
    }

    p {
        font-size: 20px;
        font-weight: 300;
        color: #333;
    };
    };
    ```
  * ### .banner
    > 使用漸層色彩與多重背景撰寫方式
     ```scss
    .banner {
    width: 100%;
    height: 100vh; // 螢幕視窗滿版高
    background: #ccc;
     //背景縮寫技巧  漸層：(角度，色碼1 位置1 ,色碼2 位置2 / background-position 漸層寬高;
    background: linear-gradient(115deg,#7bf 50%, transparent 50%) center center / 100% 100%,//多重背景寫法  url(背景連結) background-position /圖片寬高;
    url("https://images.unsplash.com/photo-1431057259500-78dd318a0a75?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80")right center / auto 100%;
    };
    ```


<<<<<<< HEAD
## **練習程式碼**
  * [codepen](https://codepen.io/pohxiqqo/pen/abVQxvN)
=======
## 練習程式碼
   * [codepen](https://codepen.io/pohxiqqo/pen/abVQxvN)
>>>>>>> 20c103952f577ca543099edfacd0bcb8279fa1a4
  

## **參考資料出處**:
---
* [金魚都能懂的這個網頁畫面怎麼切 : 圖文滿版區塊](https://ithelp.ithome.com.tw/articles/10215601)
* [金魚都能懂的網頁切版 : 圖文滿版區塊 NO001 | 切版教學 | HTML教學 | 網頁教學 | 網頁切版](https://www.youtube.com/watch?v=rwTMBmnIHcY&list=PLqivELodHt3hxeuLX8PYaI8u1GcDaBoJo)
* [好想工作室-漸層色彩與多重背景撰寫方式](https://ithelp.ithome.com.tw/articles/10197136)
