# rails-references
some useful rails commands

# Index
1. [Rails Generate](#Rails-Generate)
2. [Restful Routes](#Restful-Routes)
3. [Partial Form](#_form)
4. [Tag Helpers](#Tag-Helpers)
5. [Validate](#Validate)
6. [Strong Params](#Strong-Params)
---
### Rails Generate
### rails g model
```rails g model Author name:string genre:string bio:text --no-test-framework```
  1. migration
  2. model
### rails g migration 
```rails g migration add_more_statistics_to_authors copies_sold:integer last_novel_written:string --no-test-framework```
  * add_column :authors, :copies_sold, :integer
  * add_reference :products, :user, foreign_key: true
  * remove_column :authors, :last_novel_written, :string
  * create_table :products do |t|
    t.integer :shop_id, :creator_id
    t.references :creator_id
    t.string  :item_number, index: true
    t.string  :name, :value, default: "Untitled"
  * end
### rails g resource
  ``` rails g resource Book title:string author_id:integer --no-test-framework ```
  * migration: create_table
  * model with associations if defined
  * routes resources fullset
  * controller blank
  * empty view folder
  * TESTS if done without --no-test-framework
  [Back to top](#Index)
---
### Restful Routes
```get '/patients/:id', to: 'patients#show', as: 'patient'```
```resources :pro_players```
![alt text](https://i.stack.imgur.com/64uf4.png)
---
### _form
```
<% if @employee.errors %>
 <ul>
   <% @employee.errors.full_messages.each do |msg| %>
     <li style="color: red;"><%= msg %></li>
   <% end %>
 </ul>
<% end %>
<%= form_for(@employee) do |f| %>
    <%= f.label "first_name" %>
    <%= f.text_field :first_name %> <br>
    <%= f.label "last_name"%>
    <%= f.text_field :last_name %><br>
    <%= f.label "alias"%>
    <%= f.text_field :alias %><br>
    <%= f.label "title"%>
    <%= f.text_field :title %><br>
    <%= f.label "office"%>
    <%= f.text_field :office %><br>
    <%= f.label "image link"%>
    <%= f.text_field :img_url %><br>
    <%= f.label "doge_name" %>
    <%= f.collection_select(:dog_id, Dog.all, :id, :name)%> <br>
    <%= f.submit %>
<% end %>
```
* create, edit
```<%= render("form") %>```
---

### Tag Helpers

* delete with link_to
```<%= link_to('Delete Employee', employee_path(@employee), method: :delete, data: {confirm: "Are you sure?"}) %>```

* image with style
```<%= image_tag @employee.img_url, style: 'width:300px;height:auto' %>```

* good old form_tag
```
<%= form_tag posts_path do %>
  <label>Post title:</label><br>
  <%= text_field_tag :'post[title]' %><br>

  <label>Post description:</label><br>
  <%= text_area_tag :'post[description]' %><br>

  <%= submit_tag "Submit Post" %>
<% end %>
```
---
### Validate
```validates :email, uniqueness: true ```
```validates :title, presence: true ```
```validates :content, length: {minimum: 101} ```
```validates :age, numericality: {greater_than: 0} ```
---
### Strong Params
```private
 def sea_params
   params.require(:sea).permit(:name, :temperature, :bio, :mood, :image_url, :favoriate_color, :scariest_creature, :has_mermaids)
 end```
