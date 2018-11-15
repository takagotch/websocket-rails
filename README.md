### websocket-rails
---
https://github.com/websocket-rails/websocket-rails

```ruby
WebsocketRails::EventMap.describe do
  namespace :tasks do
    subscribe :create, :to => TaskController, :with_method => :create
    subscribe :update, 'task#update'
    subscribe :create_admin, :to => Admin::TasksController, :with_method => :create
    subscribe :update_admin, 'admin/task#update'
  end
end


class TaskController < WebsocketRails::BaseController
  def create
    task = Taks.new
    if task.save
      send_message :create_success, task, :namespace => :tasks  
    else
      send_message :create_fail, task, :namespace => :tasks
    end
  end
end

def create
  task = Task.create message
  if task.save
    trigger_success task
  else
    trigger_failure task
  end
end

def create
  task = Task.create! message
  trigger_success task
end

channel = dispatcher.subscribe('posts');
channel.bind('new', funciton(post){
  console.log('a new post about '+post.title+' arribed!');
});

latest_post = Post.latest
WebsocketRails[:post].trigger 'new', latest_post

WebsocketRails::EventMap.describe do
  private_channel :secret_posts
  namespace :websocket_rails
    subscribe :subscribe_private, :to => AuthorizationController, :with_method => :authorize_channels
  end
end

WebsocketRails[:secret_posts].make_private
```

```js
var task = {
  name: 'Start taking advantage of WebSockets',
  completed: false
}
var dispatcher = new WebSocketRails();
dispatcher.trigger('tasks.create', task);

dispatcher.bind('tasks.create_success', function(task){
  console.log("Created:" + task.name);
});

var success = function(task){ console.log("Created: " + task.name); }
var failure = function(task){
  console.log("Failed to create Product: " + product.name)
}
dispatcher.trigger('products.create', task, success, failure);

var failureCallback = function(task){
  console.log( task.name );
  console.log( task.errors );
  console.log( "You have" + task.errors.length + " errors.");
}

dispatcher.unbind('tasks.create_success');
```

```
```


