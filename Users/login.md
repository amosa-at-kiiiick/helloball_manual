# [`/users/login`](../users/login.md) 會員登入
- Reserve URI 預定路徑：	 [`/users/login`](../users/login.md)
- Premission 權限： `All groups`
- System版本號：`v1.0.0+`

## 敘述
只要為已啟動的會員帳號，於登入表單中輸入註冊時所填寫的`Email`帳號與`密碼`，即可完成登入動作。一旦完成登入後，系統將會自動記憶使用者資訊，在同一台電腦使用同樣的瀏覽器拜訪網站情況下，系統將會自動幫使用者切換至登入狀態，直到使用者自行登出帳號。



## 流程圖
![流程示意圖](http://placehold.it/740x300)

### 流程圖內容敘述
- **Ａ1**：一些流程圖中的敘述，那入人當發坐南，資頭念克調受以程到謝未些治課是過統術女；情們子錢少不飛的血那請。
	- Ａ1-Y：一些流程圖中的敘述，情們子錢少不飛的血那請。
	- Ａ1-N：一些流程圖中的敘述，那入人當發坐南。



## 表單欄位
以下欄位為使用者在流程中，將可能會需要填寫的資料欄位:


| `欄位名稱` | `鍵詞` | `敘述` | `必填` | `唯一` | `備註` |      
| :---: | :---: | --- | :---: | :---: | --- |
| 信箱 | email | 會員的帳號 | Y | Y | 基本Email邏輯字串驗證 |
| 密碼 | password | 會員的密碼 | Y |  | 必須與該帳號所對應的內容相符合 |
 
 
## 事件內容
### 當 帳號登入成功 
*觸發條件*：當使用者輸入了正確的`帳號`與`密碼`

*觸發內容*：系統將顯示登入成功的提示訊息[`(lang:user:logged_in)`](../users/language/english.md#user:logged_in)，如無設定強制轉向頁面位置(`redirect_to`)，系統將自動導回至使用者連結至登入頁面之前的所在頁面(`previous_page`)，如果系統找不到`previous_page`的話，將會導向網站的首頁([`home`](../home.md))。

*觸發外掛事件*： [`Events::trigger('post_user_login')`](../events.md#post_user_login)

### 當 帳號登入失敗
*觸發條件*：當使用者輸入了錯誤的`帳號`或`密碼`

*觸發內容*：系統將顯示登入錯誤的提示訊息[`(lang:user:login_incorrect)`](../users/language/english.md#user:login_incorrect)，並導向登入頁([`/users/login`](../users/login.md))。

### 當 登入帳號未啟動
*觸發條件*：當使用者輸入了的`帳號` 尚未啟動

*觸發內容*：系統將顯示帳號尚未啟動的提示訊息[`(lang:user:inactive)`](../users/language/english.md#user:inactive)，並導向登入頁([`/users/login`](../users/login.md))。

## 相關參照文件
- [`/users/register`](../users/register.md) 會員註冊
- [`/users/activate`](../users/activate.md) 會員啟動
- [`/users/reset_pass`](../users/reset_pass.md) 忘記與重設密碼
- [`/users/reset_complete`](../users/reset_complete.md) 忘記與重設密碼
