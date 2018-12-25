# Rails and Devise
Devise is a useful authentication library. This repository follow the [GoRails tutorial](#resource).

# installation
```
gem install devise
bundle install
```
# setup
after run this below command, follow the suggestion 5 steps in console
```
rails generate devise:install
```

generate **User** tables by devise helper
```
rails generate devise user
rake db:migrate
```
# Routes
on file routes.rb we will get this line
```
devise_for :users
```

check routes by `rails routes`.

- `new_user_registration_path register` new user
- `new_user_session_path` login user
- `destroy_user_session_path` log out user

# Custom Devise's Views
- `rails generate devise:views`
- go to `app/views/devise/`
# Helper
## View
- `<%= notice %>` notice message from devise such as 'login success'
- `<%= alert %>` alert or error message from devise such as 'need to login`
- `<% if user_signed_in? %>`
- `<%= current_user %>` such as `<%= current_user.email %>`

## Controller
### check user session before access
```ruby
class BooksController < ApplicationController
before_action :authenticate_user!, except: [:index, :show]
```
### create Book with current user
```ruby
# app/models/user.rb
class User < ApplicationRecord
...
  has_many :books
...
```
```ruby
# app/models/book.rb
class Book < ApplicationRecord
...
  belongs_to :books
...
```
```ruby
class BooksController < ApplicationController
...
  def create
    # @book = Book.new(book_params) # original
    @book = current_user.books.new(book_params) # can use current_user for create books
  ...
  end
...
```

# Resource
- [User Authentication in Rails with Devise](https://www.youtube.com/watch?v=ef11ToOE4N0)

