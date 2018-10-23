### Kaminari
---

https://github.com/kaminari/kaminari

```
gem 'kaminari'
bundle

rails g kaminari:config

rails g kaminari:views default
rails g kaminari:views default --views-prefix admin

rails g kaminari:views THEME
rails g kaminari:views

rails g kaminari:views default (skip if you have existing kaminari views)
cd app/views/kaminari
mkdir my_custom_theme
cp _*.html.* my_custom_theme/

bundle install
rake test:all

rake test:active_record_50

BUNDLE_GEMFILE='gemfiles/active_record_50.gemfile' bundle install
BUNDLE_GEMFILE='gemfiles/active_record_50.gemfile' TEST=kaminari-core/test/requests/navigation_test.rb bundle exec rake test

```

```ruby
User.page(7)

User.count
User.page(1).limit_value
User.page(1).total_pages
User.page(1).current_page
User.page(1).next_page
User.page(2).prev_page
User.page(1).frist_page?
User.page(50).last_page?
User.page(100).out_of_range?

User.page(7).per(50)

User.count
a = User.limit(5); a.count
a.page(1).per(20).size
a.page(1).per(20).total_count

User.page(7).per(50).padding(3)

users = User.page(7).per(50)
unpaged_users = users.except(:limit, :offset)

default_per_page
max_per_page
max_pages
window
outer_window
left
right
page_method_name
param_name
params_on_first_page


class User < ActiveRecord::Base
  paginates_per 50
end

class User < ActiveRecord::Base
  max_paginates_per 100
end

@users = User.order(:name).page params[:page]


User.page(3).without_count

@paginatable_array = Kaminari.paginate_array(my_array_object).page(params[:page]).per(10)

@paginatable_array = Kaminari.paginate_array([], total_count: 145).page(params[:page]).per(10)

resources :my_resources do
  get 'page/:page', action: :index, on: :collection
end

concern :paginatable do
  get '(page/:page)', action: :index, on: :collection, as: ''
end
resources :my_resources, concerns: :paginable

kaminari-core: the core pagination logic
kaminari-activerecord: Active Record adapter
kaminari-actionview: Action View adapter

gem 'kaminari-activerecord'
gem 'kaminari-actionview'

gem 'kaminari-mongoid'
gem 'kaminari-actionview'

gem 'kaminari-activerecord'
gem 'kaminari-sinatra'

```

```html
<%= paginate @users %>

<%= paginate @users %>

<%= paginate @users, window: 2 %>

<%= paginate @users, outer_window: 3 %>

<%= paginate @users, left: 1, right: 3 %>

<%= paginate @users, param_name: :pagina %>

<%= paginate @users, params: {controller: 'foo', action: 'bar'} %>

<%= paginate @users, remote: true %>

<%= paginate @users, views_prefix: 'templlates' %>

<%= link_to_next_page @items, 'Next Page' %>

<%= page_entries_info @posts %>

<%= page_entries_info @posts, entry_name: 'item' %>

<%= rel_next_prev_link_tags @users %>

<%= path_to_next_page @users %>

<%= path_to_prev_page @users %>

<%= paginate @users, theme: 'my_custom_theme' %>

<%= link_to_prev_page @users, 'Previous Page' %>
<%= link_to_next_page @uses, 'Next Page' %>

```

```yml
en:
  views:
    pagination:
      first: "&laquo; First"
      last: "Last &raquo;"
      previous: "&lsaquo; Prev"
      next: "Next &rsaquo;"
      truncate: "&hellip;"
  helpers:
    page_entries_info:
      one_page:
        display_entries:
          zero: "Displaying <b>1</b> %{entry_name}"
          one: "Displaying <b>all %{count}</b> %{entry_name}"
          other: "Displaying <b>all %{count}</b> %{entry_name}"
      more_pages:
        display_entries: "Displaying %{entry_name} <b>%{first}&nbsp;-&nbsp;%{last}</b> of <b>%{total}</b> in total "

```



