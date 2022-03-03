# ✏ **CSS切版筆記 - 『金魚切版系列: 互動圖文卡片 NO002  』**

![](https://i.imgur.com/q1wa9b1.jpg)



## **切版知識點與技巧補充:**
* [CSS absolute 絕對定位](https://www.youtube.com/watch?v=JOdZdHnuGmM)
* [CSS relative 相對定位](https://www.youtube.com/watch?v=Rukgrh1HlZg)
* [transition 動畫的做法](https://www.youtube.com/watch?v=kR6JpIGJDBQ)
* [flex-direction 的原理](https://www.youtube.com/watch?v=_nCBQ6AIzDU&t=1702s)



## **HTML 架構**
> .warp 為外容器，裡面包覆 4 個 .card 物件內含圖片及文字，建立正確的架構後，在撰寫css 樣式
```html
 <div class="wrap">
        <div class="card">
            <img class="card-img" src="https://i.imgur.com/s4k9olk.jpg" alt="picture">
            <div class="card-body">
                <h2 class="card-title">金魚切版系列教學 : 製作一個互動圖文卡片</h2>
                <p class="card-text">互動卡片都是我在網頁中常見的範列，讓我們來跟AMOS一起學起來吧!</p>
            </div>
        </div>
        <div class="card">
            <img class="card-img" src="https://i.imgur.com/TDEQUeq.jpg" alt="picture">
            <div class="card-body">
                <h2 class="card-title">金魚切版系列教學 : 製作一個互動圖文卡片</h2>
                <p class="card-text">互動卡片都是我在網頁中常見的範列，讓我們來跟AMOS一起學起來吧!</p>
            </div>
        </div>
        <div class="card">
            <img class="card-img" src="https://i.imgur.com/DtavzLv.jpg" alt="picture">
            <div class="card-body">
                <h2 class="card-title">金魚切版系列教學 : 製作一個互動圖文卡片</h2>
                <p class="card-text">互動卡片都是我在網頁中常見的範列，讓我們來跟AMOS一起學起來吧!</p>
            </div>
        </div>
        <div class="card">
            <img class="card-img" src="https://i.imgur.com/a0Mo6HZ.jpg" alt="picture">
            <div class="card-body">
                <h2 class="card-title">金魚切版系列教學 : 製作一個互動圖文卡片</h2>
                <p class="card-text">互動卡片都是我在網頁中常見的範列，讓我們來跟AMOS一起學起來吧!</p>
            </div>
        </div>
    </div>
```



## **SCSS 樣式**
  * ###  **.wrap (外容器)**
    >將 .warp 設定網頁滿寬的容器，使用 flex 將 .card 的四個物件水平排列置中
     ``` scss
    .wrap {
    width: 100%;
    display: flex;
    margin:  0 auto;
    };
     ```

   * ### **.card (容器內的物件)**
       1. .card 將四個物件分別設定佔據 .wrap 容器內25%(約四分之一的寬度) 因為 .card-body 使用絕對定位要定位.card(父層)，所以要使用相對定位。
       2. .card-img 設定為與 .card(父層滿寬)， 並加入vertical-align: middle樣式，清除圖片下方多餘空間使其對齊。
       3. .card-body (子層)使用絕對定位，做成圖片遮罩，定位位置為 .card(父層)且完整覆蓋
       4. .card-body 內的文字樣式調整
   
      ```scss
      .card {
      width: 25%;
      position: relative;

      // 互動效果製作: 父層下指令，子層執行動作
      // &:hover {
      //     .card-body {
      //         opacity: 1;
      //     };

      //     .card-title::after {
      //         width: 100%;
      //     }
      // }
      .card-img {
        width: 100%;
        //清除圖片下方多餘空間
        vertical-align: middle;
      }
      .card-body {
        //使用絕對定位，定位在父層 .card 做成圖片遮罩
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        padding: 20px;
        background: rgba(0, 0, 0, 0.6);
        // 使用 flex 將 .card-body 內容垂直居中排列
        display: flex;
        flex-direction: column;
        justify-content: center;
        // 互動效果製作 - 隱藏文字 , Transition 網頁動畫: 屬性 轉換時間 延遲執行時間 速度
        // opacity: 0;
        // transition: opacity 0.5s;
        // cursor: pointer;
     }

      // 4. .card-body 內的文字樣式調整
      .card-title {
        font-size: 32px;
        color: red;
        font-weight: 500;
        // 使用 偽元素 :after 製作 跑馬燈效果線條
        // &::after {
        //     content: "";
        //     display: block;
        //     width: 0%; //一開始線條為 0
        //     height: 2px;
        //     margin: 10px 0;
        //     background-color: red;
        //     transition: width 0.5s 0.3s;
        // }
     }
     .card-text {
        font-size: 16px;
        color: #fff;
        font-weight: 100;
      }
      }
      ```

   * ### **hover 效果**
  
     > 建立 hover 效果習慣，父層下指令，子層執行動作
     * 所以當.card (父層):hover時，.card-body(子層) 的透明效果變為顯示  opacity:1。
     * 在.card-body(子層)加上 transition 效果，讓 opacity 的時間為 0.5s，就會有漸變效果，視覺上也較自然。
     ```scss
      .card {
      width: 25%;
      position: relative;

      // 互動效果製作: 父層下指令，子層執行動作
      &:hover {
          .card-body {
              opacity: 1;
         };

        .card-title::after {
            width: 100%;
         };
      };
      .card-img {
        width: 100%;
        //清除圖片下方多餘空間
        vertical-align: middle;
      }
      .card-body {
        //使用絕對定位，定位在父層 .card 做成圖片遮罩
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        padding: 20px;
        background: rgba(0, 0, 0, 0.6);
        // 使用 flex 將 .card-body 內容垂直居中排列
        display: flex;
        flex-direction: column;
        justify-content: center;
        // 互動效果製作 - 隱藏文字 , Transition 網頁動畫: 屬性 轉換時間 延遲執行時間 速度
         opacity: 0;
         transition: opacity 0.5s;
         cursor: pointer;
       }

      // 4. .card-body 內的文字樣式調整
      .card-title {
        font-size: 32px;
        color: red;
        font-weight: 500;
        // 使用 偽元素 :after 製作 跑馬燈效果線條
        // &::after {
        //     content: "";
        //     display: block;
        //     width: 0%; //一開始線條為 0
        //     height: 2px;
        //     margin: 10px 0;
        //     background-color: red;
        //     transition: width 0.5s 0.3s;
        // }
     }
     .card-text {
        font-size: 16px;
        color: #fff;
        font-weight: 100;
      } 
     } 
     ```

  *  ##  **使用偽元素增加網頁互動效果 ::after**

     >使用偽元素製作在 .card-title 下製作跑馬燈線，能讓網頁與使用者互動時，更加生動有趣
     * 要在 .card-title 下方加上一條橫線產生互動，並且 transition 後面指定的值可 以單獨指定，與應用  在前面指定 opacity 相同。
     * 並且指定在 hover 後的效果占滿 .card 內的寬度 100%。
     * 使 .card-title底線用 transition 指定寬度時間漸變 0.5s，delay(延遲) 0.3s。

     ```scss
     .card {
     width: 25%;
     position: relative;

     // 互動效果製作: 父層下指令，子層執行動作
     &:hover {
        // 被 hover 後 , 文字內容區塊出現
        .card-body {
            opacity: 1;
        };
        
        // 被 hover 後 ，底線寬度占滿 .card 內的寬度 100%。
        .card-title::after {
            width: 100%;
        }
     }
     .card-img {
        width: 100%;
        //清除圖片下方多餘空間
        vertical-align: middle;
     }
     .card-body {
        //使用絕對定位，定位在父層 .card 做成圖片遮罩
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        padding: 20px;
        background: rgba(0, 0, 0, 0.6);
        // 使用 flex 將 .card-body 內容垂直居中排列
        display: flex;
        flex-direction: column;
        justify-content: center;
        // 互動效果製作 - 隱藏文字 , Transition 網頁動畫: 屬性 轉換時間 延遲執行時間 速度
        opacity: 0;
        transition: opacity 0.5s;
        cursor: pointer;
     }

     // 4. .card-body 內的文字樣式調整
     .card-title {
        font-size: 32px;
        color: red;
        font-weight: 500;
        // 使用 偽元素 :after 製作 跑馬燈效果線條
        &::after {
            content: "";
            display: block;
            width: 0%; //一開始線條為 0
            height: 2px;
            margin: 10px 0;
            background-color: red;
            transition: width 0.5s 0.3s;
        }
      }
     .card-text {
        font-size: 16px;
        color: #fff;
        font-weight: 100;
     }
      }
     ```
## **練習程式碼**
  * [codepen](https://codepen.io/pohxiqqo/pen/YzEdjZX)

  

## **參考資料出處**:
---
* [金魚都能懂的這個網頁畫面怎麼切 : 製作一個互動圖文卡片](https://ithelp.ithome.com.tw/articles/10216684)
* [金魚都能懂的網頁切版 : 互動圖文卡片 NO002 | 切版教學 | HTML教學 | 網頁教學 | 網頁切版](https://www.youtube.com/watch?v=IocyLERRdko&t=17s)

