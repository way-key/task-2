# task-2 修正箇所  
	※Rspecテストが行えなくて断念(2020/4/17)  
  
---  
1. Gemfileに[gem 'bootstrap-sass']を追加  
2. routes.rbに以下の内容を追加
	- 末尾にendを追記  
	- 4段目のdevise_for :usersを2段目に移動
---  
3. application_controller.ebの9,14行目の記載内容を交換  
4. users_controller.ebに以下の内容を追加  
	- 5段目: @newbook = Book.new  
	- 12段目: end  
	- 27行目: render "**edit**"  
5. books_controller.ebに以下の内容を追加  
	- 6行目: @user = @book.user  
	- 10行目: @book = Book.new
	- 16行目: @book.user_id =current_user.id
	- 17行目: redirect_to **book_path(@book.id)**…  
	- 21行目: flash[:notice] = "error"  
	- 28~30行目: if @book.user != …end  
	- 36~38行目: **@**を削除  
  	- 53行目: params.require(:book).permit(:title, **:body**)  
---  
6. model >conserns 内の、book.rbとuser.rbについて、記載内容を修正  
	- book.rb：has_many :user → belongs_to :user  
	- book.rb：validates :introduction, length: {maximum: 50}  
	- user.rb：belongs_to :books → has_many :books, dependent: :destroy  
7. model >Userにprofile_image_idを追加  
---  
7. view > sessions > new.html.erb の14,19行目にあるタグの記述を修正  
	- <% … **-**%> → <% … %>  
8. view > registrations > new.html.erb の9行目を以下の通り修正  
	- <%= f.name_field :name,… → <%= f.text_field :name,…  
9. view > layouts > application.html.erbの43~44行目の間に[<%= yield %>]を追加  
10. view > users > show.html.erbに下記の通り追記  
	- 6行目: <%= render 'users/profile'**, user: @user** %>
	- 9行目: <%= render 'books/newform'**, book: @book** %>
	- 21行目: <% **@**books.each do |book| %>  
	- 全体をグリットシステムの ".row" で囲む  
	- User_infoとNewBookの部分はグリッドシステムの ".col-xs-3"で、Books以降を".col-xs-9"で囲む  
11. view > users > index.html.erbに下記の通り追記  
	- 6行目：<%= render '**books/**newform', book: @book %>
	- 全体をグリットシステムの ".row" で囲む  
	- User_infoとNewBookの部分はグリッドシステムの ".col-xs-3"で、Books以降を".col-xs-9"で囲む  
12. view > users > edit.html.erbに以下の通り追記  
	- <%= f.text_field :**name**, class: "name" %>
13. view > books > show.html.erbに以下の通り追記  
	- 6行目: <%= render 'users/profile'**, user: @user** %>  
	- 9行目: <%= render 'books/newform'**, book: @newbook** %>  
	- 26,29行目: <% if @user == current_user %>,<% end %>  
14. view > users > profile.html.erbを以下の通り修正  
	- <%= attachment…をtableタグの真下に  
	- name,introductionをtbodyで囲む  
15. view >home >top.html.erbを以下の通り修正  
	- 11行目: …new_user_session_path…  
	- 14行目: …new_user_registration_path…  
