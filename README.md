# WPCreatePostRestAPI
Create post base on rest api

```HTML
  <div id="admin-quick-add">
    <h3> Quick Add Post </h3>
    <input type="text" name="title" placeholder="Title">
    <textarea name="content" placeholder="Content"></textarea>
    <button id="quick-add-button"> Create Post </button>
  </div>
```

```PHP
 // function file
 function rest_api_fetch_register() {
  wp_enqueue_script('Handlebar-JS','https://cdn.jsdelivr.net/npm/handlebars@latest/dist/handlebars.js', NULL , NULL , true );
  wp_enqueue_script('app-fetch-rest-api-JS', get_template_directory_uri() . '/js/app-fetch-rest-api.js', NULL , 1.0 , true );
  
  wp_localize_script('app-fetch-rest-api-JS', 'magicalData', array('nonce' => wp_create_nonce('wp_rest')));
 }
 add_action( 'wp_enqueue_scripts', 'rest_api_fetch_register' );
```

```JS
var btnQuickAddButton = document.querySelector("#quick-add-button");
if( btnQuickAddButton ) {
   
    btnQuickAddButton.addEventListener('click', function() {
        var ourPostData = {
            'title'   : document.querySelector('#admin-quick-add [name="title"]').value,
            'content' : document.querySelector('#admin-quick-add [name="content"]').value,
            'status'  : 'publish'
        }
        var createPost  = new XMLHttpRequest();
        createPost.open("POST", 'http://localhost/wpdev/wp-json/wp/v2/posts');
        createPost.setRequestHeader("X-WP-Nonce", magicalData.nonce);
        createPost.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
        createPost.send(JSON.stringify(ourPostData));
    });
    console.log(ourPostData);
 }
```
