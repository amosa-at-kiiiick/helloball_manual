# [`/users/activate`](../users/activate.md) 會員帳號啟動
- Reserve URI 預定路徑：	 [`/users/activate`](../users/activate.md)
- Premission 權限： `All groups`
- System版本號：`v1.0.0+`

## 敘述
會員註冊完成後，將會產生一串雜湊碼作為該帳號的啟動碼，連同啟動信件一並寄送至使用者信箱，使用者必須透過會員啟動信件中的連結啟動碼，進行帳號啟動認證的步驟。藉此步驟可驗證使用者信箱的正確性，及確認使用者信箱可正常收取由網站系統發送的電子信件。

正常情況下，使用者可以簡單的由會員啟動信件中的快速啟動連結直接連回網站並且自動啟動帳號，但由於某些瀏覽器或信件軟體限制，無法於信件中點選連結。因此，信件中也直接提供一段約32字元的`啟動碼`，使用者可自行回到網站[`/users/activate`](../users/activate.md)頁面，貼上這串`啟動碼`進行手動驗證的啟動帳號程序。

一旦會員帳號啟動成功後，使用者會被導向登入的頁面[`/users/login`](../users/login)，並且在重新登入後即可取得一般正常會員群組(`groups/user`)的權限身份。

## 流程圖
![流程示意圖](http://placehold.it/740x300)

### 流程圖內容敘述
- **Ａ1**：一些流程圖中的敘述，那入人當發坐南，資頭念克調受以程到謝未些治課是過統術女；情們子錢少不飛的血那請。
	- Ａ1-Y：一些流程圖中的敘述，情們子錢少不飛的血那請。
	- Ａ1-N：一些流程圖中的敘述，那入人當發坐南。

- **Ａ2**：一些流程圖中的敘述。參照 [`/users/activate`](../users/activate.md)

- **Ａ2**：一些流程圖中的敘述，那入人當發坐南


## 表單欄位
以下欄位為使用者在流程中，將可能會需要填寫的資料欄位:


| `欄位名稱` | `鍵詞` | `敘述` | `必填` | `唯一` | `備註` |      
| :---: | :---: | --- | :---: | :---: | --- |
| 信箱 | email | 會員的註冊帳號 | Y | Y | 基本Email邏輯字串驗證 |
| 啟動碼 | activation_code | 會員註冊時系統自動產生給予的啟動碼 | Y |  | 必須與系統內儲存的啟動碼內容相符合 |
 
 
## 事件內容
### 當 帳號啟動成功 
*觸發條件*：當使用者輸入或透過啟動連結輸入了正確的`帳號啟動碼`

*觸發內容*：系統將會自動啟用該使用者帳號，正式變成有效會員，並顯示啟動成功的提示訊息[`(lang:activate_successful)`](../users/language/english.md#activate_successful)  ，並將使用者導向登入頁面 [`/users/login`](../users/login.md)。

*觸發外掛事件*： [`Events::trigger('post_user_activation')`](../events.md#post_user_activation)

### 當 帳號啟動失敗
*觸發條件*：當使用者輸入或透過啟動連結輸入了錯誤的`帳號啟動碼`

*觸發內容*：系統將會顯示啟動錯誤的提示訊息[`(lang:activate_unsuccessful)`](../users/language/english.md#activate_unsuccessful)  ，並將使用者導向登入頁面 [`/users/login`](../users/login.md)。


## 相關參照文件
- [`/users/register`](../users/register.md) 會員註冊
- [`/users/login`](../users/login.md) 會員登入
- [`/users/reset_pass`](../users/reset_pass.md) 忘記與重設密碼
- [`/users/reset_complete`](../users/reset_complete.md) 忘記與重設密碼
