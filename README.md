# Chirp Twitter

To start your Phoenix server:

  * Install dependencies with `mix deps.get`
  * Create and migrate your database with `mix ecto.setup`
  * Install Node.js dependencies with `npm install` inside the `assets` directory
  * Start Phoenix endpoint with `mix phx.server`

Now you can visit [`localhost:4000`](http://localhost:4000) from your browser.

Ready to run in production? Please [check our deployment guides](https://hexdocs.pm/phoenix/deployment.html).  

------------------------------
## Purpose
As one of my first steps of learning phoenix liveview, I followed [`Build a real-time Twitter clone in 15 minutes with LiveView and Phoenix 1.5`](https://www.youtube.com/watch?v=MZvmYaFkNJI) step by step, but found the following issues:
1) Icons do not show on page. 
2) "Prepand update" crashes which can be see after enabling liveSocket debug by:
```javascript
liveSocket.enableDebug()
```  
To address these issues and make the result the same as the tutorial video, I studied and improved the project.
<p>&nbsp;</p>

## Problem solving
1. Add fontawesome into phoenix assets:  
1.1 Install fontawesome  
    ```console
    cd assets
    npm i --save @fortawesome/fontawesome-free
    ```  
    1.2 Install mini-css-extract-plugin  
    ```console
    npm i -D mini-css-extract-plugin
    ```  
    1.3 Import fontawesome paths into assets/css/app.scss  
    1.4 Assign fa font path in assets/css/_custom.scss  
    1.5 Install file-loader  
    ```console
    npm i -D file-loader
    ```  
    1.6 Configure file-loader in webpack.config.js  

2. "Prepand update" crashes:  
* Phenomenon:  
  Serve's debug info shows 'dupilcate id' when updating twitts.  
* Root cause:  
  The tutorial just adds the updated post into the list of post in socket.assigns.posts, in which its old version already exists. The updated post and its old version in socket.assigns.posts are duplicate.  
* Solution:  
  Created a function to replace the post in socket.assigns.posts with the updated one (lib/chirp_web/live/post_live/index.ex).
------------------------------
## Learn more
  * Liveview twitter tutorial: https://www.youtube.com/watch?v=MZvmYaFkNJI
  * How to include FontAwesome in Phoenix app: https://elixirforum.com/t/how-to-include-fontawesome-in-phoenix-app/21749/9
