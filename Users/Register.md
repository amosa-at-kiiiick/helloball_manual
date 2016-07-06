# [`/users/register`](../users/register.md) 會員註冊
- Reserve URI 預定路徑：	 [`/users/register`](../users/register.md)
- Premission 權限： `All groups`
- System版本號：`v1.0.0+`

## 敘述
會員註冊主要使用為Email當為每個使用者的帳號，並且一旦註冊後將不能更改帳號Email內容。

當帳號註冊完成，帳號將會是`未啟動`的狀態，`未啟動`的帳號等同於無效的會員帳號，使用者必須透過由系統發送的`啟動信件`來完成第二階段的會員認證步驟([`/users/activate`](../users/activate.md))，才算是完整有效的會員帳號。

## 流程圖
![流程示意圖](http://placehold.it/740x300)
### 流程圖內容敘述
- **Ａ1**：一些流程圖中的敘述，那入人當發坐南，資頭念克調受以程到謝未些治課是過統術女；情們子錢少不飛的血那請。
	- Ａ1-Y：一些流程圖中的敘述，情們子錢少不飛的血那請。
	- Ａ1-N：一些流程圖中的敘述，那入人當發坐南。

- **Ａ2**：一些流程圖中的敘述。參照 [`/users/activate`](../users/activate.md)

- **Ａ2**：一些流程圖中的敘述，那入人當發坐南


## 表單欄位
以下欄位為使用者資料在註冊中，將可能會需要填寫的資料欄位:


| `欄位名稱` | `鍵詞` | `敘述` | `必填` | `唯一` | `備註` |      
| :---: | :---: | --- | :---: | :---: | --- |
| 信箱 | email | 電子信箱位置，也代表為會員的登入帳號 | Y | Y | 基本Email邏輯字串驗證 |
| 密碼 | password | 會員的登入密碼 | Y |  | 密碼字元允許為英數字半形組合，長度為6-20字元，註冊畫面中將會對應一組確認密碼(password conf)欄位用來核對密碼是否輸入正確 |
系統帳號 | username | 此為系統內部操作用的會員代號ID | Y | Y |隱藏的欄位，將會使用會員註冊Email帳號的@前字串當作內容，如與系統已存的username有相同者，會自動在尾碼加上流水號數字作為區別|
| 電話 | phone | 聯絡電話號碼 | | | |
| 同意條款 | agree | 同意網站隱私權/使用條款 | Y | | 使用者必須完全同意使用者條款，才能送出註冊表單，否則將無法送出。 |
 
## 事件內容
### 已登入偵測 
*觸發條件*：當使用者在已登入的身份，拜訪 [`/users/register`](../users/register.md)

*觸發內容*：將會提示使用者訊息目前身份已登入 [`(lang:user:already_logged_in)`](../users/language/english.md#user:already_logged_in)  ，並將使用者導向首頁 [`/home`](../home.md)。


### 偵測機器人註冊 
*觸發條件*：當使用者送出註冊表單時，檢查隱藏碼以判斷是操作者是否為機器人

*觸發內容*：如判斷為機器人，則告知目前操作者 操作錯誤 [`(lang:user:register_error)`](../users/language/english.md#user:register_error)  ，並將使用者導向首頁 [`/users/login`](../users/login.md)。


### 當註冊資料成功 
*觸發條件*：當使用者送出註冊表單時，表單驗證皆完成

*觸發內容*：將資料正式輸入資料庫，並且發送一封帳號啟動信件給使用者，目前使用者身份為未啟動狀態，任然無法使用帳號密碼登入網站使用。

*信件主旨*：[`lang:subject_activation`](../users/language/english.md#subject_activation)

*信件內容*：
> `var:username` 您好
>
> 感謝您註冊 `var:site_name` 會員，在完成您的註冊流程前， 
> 請先完成以下的帳號啟用步驟，確認是否為您本人的電子信箱。 
>
> > `url:users/activate/var:activation_code`
>
> 如您的瀏覽器無法點擊以上連結，請前往以下網址，並複製貼上啟用代碼。 
>
> > `url:users/activate`
> 
> 啟用碼：`var:activation_code`


### 當註冊資料有誤
*觸發條件*： 當使用者送出註冊表單，表單驗證發生錯誤時。

*觸發內容*： 將會導回至前頁表單註冊頁面([`/users/register`](../users/register.md))，並留存前次輸入資料且提示填寫錯誤的欄位與原因。


## 相關參照文件
- [`/users/activate`](../users/activate.md) 會員啟動
- [`/users/login`](../users/login.md) 會員登入
- [`/users/reset_pass`](../users/reset_pass.md) 忘記與重設密碼
- [`/users/reset_complete`](../users/reset_complete.md) 忘記與重設密碼
