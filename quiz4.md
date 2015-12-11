1. 請說明 ```rails g scaffold xxx``` 功能的壞處為何？

2. 若今天需要為 ```Project``` 和 ```Issue``` 這兩個 Model 建立一對多的關係，請寫出實作上所需要的 migratiion 和 model 檔案 

3. 若今天我有以下 model 檔：

  ```ruby
  class User < ActiveRecord::Base
    has_many :groups_users
    has_many :groups, through: :groups_users 
  end
  ```

  請寫出和這個 model 檔相關連的 model 檔，以及這些 model 檔所需要的資料庫欄位

4. 延續第3題，如果需要讓一個叫 "Bob" 的使用者產生一個名字叫做 "Rails is Fun" 的社團，應該如何在 rails console 裡實作出來？

5. 延續第4題，請寫一段程式碼確保使用者在建立新社團時社團名字不可以是空白，而且不能超過50個字

6. 請列出兩種方法檢查在 routes.rb 裡面設定的路由

7. 請列出在一個 rails 專案裡使用 bootstrap 套件的步驟

8. 請說明在 .erb 檔案裡 ```<%= %>``` 與 ```<% %>``` 這兩種 tag 的差別