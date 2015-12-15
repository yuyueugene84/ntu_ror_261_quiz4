1. 請說明 ```rails g scaffold xxx``` 功能的壞處為何？
  
  **Answer:**
  a. 很難透過自動化產出完全符合需求的程式碼，尤其當的 model 很複雜時
  b. 會產生不必要的檔案或資料夾，像是 .coffee 檔和 spec 資料夾


2. 若今天需要為 ```Project``` 和 ```Issue``` 這兩個 Model 建立一對多的關係，請寫出實作上所需要的 migratiion 和 model 檔案 
  
  **Answer:** 

  ```ruby
  class AddProjectAndIssueTables < ActiveRecord::Migration
  	def change
	  	create_table :projects do |t|
	      t.string :name
	    end

	  	create_table :issues do |t|
	      t.string :name
	      t.integer :project_id
	    end
  	end
  end


  class Project < ActiveRecord::Base
  	has_many :issues
  end

  class Issue < ActiveRecord::Base
  	belongs_to :project
  end
  ```

3. 若今天我有以下 model 檔：

  ```ruby
  class User < ActiveRecord::Base
    has_many :groups_users
    has_many :groups, through: :groups_users 
  end
  ```

  請寫出和這個 model 檔相關連的 model 檔，以及這些 model 檔所需要的資料庫欄位

  **Answer:** 

  ```ruby
  class Group < ActiveRecord::Base
	has_many :groups_users
	has_many :users, through: :groups_users
  end

  class Groups_User < ActiveRecord::Base
	belongs_to :group
	belongs_to :user
  end
  ```

4. 延續第3題，如果需要讓一個叫 "Bob" 的使用者產生一個名字叫做 "Rails is Fun" 的社團，應該如何在 rails console 裡實作出來？
  
  **Answer:**

  ```ruby
  bob = User.create(name: "Bob")
  group = Group.create(title: "Rails is Fun")
  bob.groups << group 
  ```
  或是
  ```ruby
  bob = User.create(name: "Bob")
  group = Group.create(name: "Rails is Fun")
  group.users << bob
  ```



5. 延續第4題，請寫一段程式碼確保使用者在建立新社團時社團名字不可以是空白，而且不能超過50個字
  
  **Answer:**

  ```ruby
  class Group < ActiveRecord::Base
	has_many :groups_users
	has_many :users, through: :groups_users

	validates :title, presence: true, length: {maximum: 50}
  end
  ```


6. 請列出兩種方法檢查在 routes.rb 裡面設定的路由

  **Answer:**

  a. 打開瀏覽器，在 rails server 運作的情況下輸入 ```/rails/info/routes```
  b. 在 terminal 裡，輸入 ```rake routes``` 指令


7. 請列出在一個 rails 專案裡使用 bootstrap 套件的步驟

  **Answer:**

  **step1:**  
  GemFile裡輸入
  ```ruby
  gem 'bootstrap-sass'
  ```
  **step2:** 
  在 terminal 執行：
  ```
  $bundle install
  ```
  **step3:**  
  /app/assets/javescripts/application.js  
  ```ruby
  //= require bootstrap
  ```
  **step4:**  
  /app/assets/sheetstyles/application.scss
  ```css
  @import 'bootstrap'
  ```


8. 請說明在 .erb 檔案裡 ```<%= %>``` 與 ```<% %>``` 這兩種 tag 的差別

  **Answer:** 
  ```<%= %>``` 會顯示裡面被執行的 ruby 程式碼的結果，適用於顯示資訊 ex. ```<%= post.title %>```、```<%= user.name %>```，而```<% %>``` 則不會顯示裡面被執行的 ruby 程式碼的結果，適用於判斷式或迴圈關鍵字 ex. ```<% arr.each do |x| %>```、```<% if else end %>```
