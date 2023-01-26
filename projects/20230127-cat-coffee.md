---
title: CatCoffee 貓咖啡
description: 貓咖啡電商咖啡店 專案介紹
slug: cat-coffee
date: 2023-01-27
type: Post
socialImage: /images/projects/coffeeShop.jpg
---

<img alt="截圖 2022-04-21 下午8 40 42" src="https://user-images.githubusercontent.com/93901409/164461164-22a052d0-5d9f-4ce1-ae66-5ce6ec68f478.png">

# **貓咖啡 電商咖啡店**
> 貓咖啡 提供來自全世界的精品咖啡豆，即使生活在疫情時代，也能透過網站購買各式咖啡，除了基本咖啡豆以外，還有、冷萃咖啡、掛耳包、精品禮盒等等，讓你自己喝、一起喝、送別人喝都不成問題！

網站 : [貓咖啡](https://cofcat456.github.io/coffeeShop)

---

## **創店理念**
咖啡一直都是工作者們必備的良藥，尤其對工程師而言，在平常生活中，我喜歡帶上筆電，到咖啡廳中點一杯拿鐵，聽著店內的lofi音樂，不僅環境舒適，咖啡也帶給我源源不絕的能量，大幅提升我的學習品質。

而近兩年，隨著疫情不斷變得嚴重，許多公司開始宣布遠端工作，而且可能長達數月以上。
剛開始，工程師們可能會選擇到咖啡廳工作，不但保留人與人接觸的時間，也能喝到一杯絕佳的咖啡，保持工作品質，但伴隨著確診人數的增加，漸漸的，到咖啡廳工作，也變成是一種奢侈，

為了廣大工作者們著想，貓咖啡推出電商網站，雖不能與各位見面，但我們將精心挑選的咖啡豆，送至家中，讓您即使在家工作，也彷彿在咖啡廳般享受！

---

## **專案說明**
> * 使用 ` Vue.js ` 和 ` Vue CLI ` 進行開發
> * 使用 ` Vue Router ` 路由設定
> * 使用 ` Vue Axios ` 串接後台 API 資料
> * 使用 ` props ` ` emit ` ` Mitt ` 進行元件間資料的傳遞
> * 使用 ` Bootstrap 5 ` Css框架完成版面
> * 使用 ` ESlint Standard ` 控管程式碼品質
> * 使用 ` Git ` 版本控制

### **使用技術**
* Vue 2
* Vue Cli
* Vue Single-File Components
* Vue Router
* Vue Axios
* VeeValidate
* Vue-loading-overlay
* Vue-sweetalert2
* mitt
* Bootstrap5
* Bootstrap5 Icons
* FontAwesome
* Swiper
* Animate
* AOS
* LocalStorage

---

### **前台**
* 商品展示：首頁、商品列表、商品介紹等
* 收藏清單：新增、編輯、刪除收藏商品
* 購物車：新增、刪除及編輯商品數量
* 優惠卷：使用優惠卷可享全館8折
* 訂單：表單驗證顧客資料

### **後台**
* 管理者登入驗證
* 商品管理：新增、編輯、刪除
* 訂單管理：編輯部分訂單資訊、刪除
* 優惠卷管理：新增、修改、刪除

---

## 前台頁面介紹

### **首頁** 
<img width="80%" alt="首頁" src="https://user-images.githubusercontent.com/93901409/164472984-b24ec430-cbcf-451d-ab41-c5721304455f.png">

### **商品列表**
<img width="80%" alt="商品列表-1" src="https://user-images.githubusercontent.com/93901409/164473643-2c3efcaf-b983-4795-9694-869b5ddd3a10.png">
<img width="80%" alt="商品列表-2" src="https://user-images.githubusercontent.com/93901409/164473703-c402f6d1-eec7-44d2-8a64-94ad5e878564.png">
<img width="80%" alt="商品列表-3" src="https://user-images.githubusercontent.com/93901409/164473716-340e0490-6886-4aff-8787-5557c8b2cc34.png">

### **收藏清單**
* 利用 ` LocalStorage ` 儲存使用者收藏紀錄

<img width="80%" alt="收藏清單" src="https://user-images.githubusercontent.com/93901409/164474042-a0c95f5d-2526-4c5f-988e-85bcad27f2eb.png">

### **購物車**
* 可任意修改購買的商品數量（不得為負值）
* 可套用優惠卷

<img width="80%" alt="購物車" src="https://user-images.githubusercontent.com/93901409/164474819-097cfb24-60a1-451a-a496-64accf8e364f.png">

### **訂單填寫**
<img width="80%" alt="訂單填寫" src="https://user-images.githubusercontent.com/93901409/164475904-4a4fb95b-c68e-4bcd-a3d4-d8a46131fe4d.png">

* 紅色星號為必填項目
* 每個欄位皆有格式驗證

### **訂單建立**
<img width="80%" alt="訂單建立" src="https://user-images.githubusercontent.com/93901409/164476506-c20fb3f0-8eb8-4428-9030-99abdf746adb.png">

## 後台頁面介紹

### **商品管理頁面**
<img width="80%" alt="商品管理頁面" src="https://user-images.githubusercontent.com/93901409/164477455-5b799d00-6d11-4fb0-a91c-7aac72a043de.png">
<img width="80%" alt="商品編輯頁面" src="https://user-images.githubusercontent.com/93901409/164477524-426d61aa-bbfb-4f0a-9bd5-e7980680865c.png">

### **訂單管理**
<img width="80%" alt="訂單管理頁面" src="https://user-images.githubusercontent.com/93901409/164477839-0727af3a-cfe2-4d86-afb9-d41408565c00.png">
<img width="80%" alt="訂單編輯頁面" src="https://user-images.githubusercontent.com/93901409/164477939-3ae0e8db-4bdd-4593-bf9a-8ffd737e61c1.png">

### **優惠卷管理**
<img width="1440" alt="優惠卷管理頁面" src="https://user-images.githubusercontent.com/93901409/164478123-84e56677-62fe-4cf8-9931-d7d80c1776d1.png">

---

- 程式碼（Github) : [CofCat456/CoffeeShop](https://github.com/CofCat456/coffeeShop)
- 官網 : [貓咖啡](https://cofcat456.github.io/coffeeShop/#/)