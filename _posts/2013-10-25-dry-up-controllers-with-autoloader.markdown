---
layout: post
title:  "DRY up controllers with autoloader"
date:   2013-10-25 21:21:21
---

Have you ever had the feeling that you were repeating yourself when writing controller code for your Rails app? You were right, because you actually did!  

See this example of a basic posts controller in a blog application  

    PostsController < ActionController::Base
      def index
        @posts = Post.all
      end
      
      def show
        @post = Post.find(params[:id])
      end
      
      def new
        @post = Post.new
      end
      
      def create
        Post.create(params[:post])
      end
      
      def destroy
        post = Post.find(params[:id])
        post.destroy
      end
    end

Every controller that is tied to an ActiveRecord-model has more or less this structure. But why bother with this boilerplate database interaction? You can do better things with your time.  

#Autoloader to the rescue!

_Autoloader_ puts the 'Action' into ActionController and makes the boring things for you. This is what the above controller looks like when it has been supercharged with _Autoloader_:  

    PostsController < ActionController::Base
      autoload_resource :post
      def index
      end
      
      def show
      end
      
      def new
      end
      
      def create
        @post.save
      end
      
      def destroy
        @post.destroy
      end
    end

Yes, the only things you have to do are the writing operations on the database! Concentrate on the critical parts of your app. And if you don't like how autloader does its job, you can configure it with some powerful configuration options. But beware: some of the options are that badass you'd better ask for your parents' permission.  

_Autoloader is still alpha software. We have no automatic tests yet. When we first tried it, Justin Bieber released a new album. Please take care._  

# Where can I get it?
You can find all important information concerning installation, usage and other goodies in the projects [README](https://bitbucket.org/musicspot/autoloader/overview). Please report any issues you encounter in the [issue tracker](https://bitbucket.org/musicspot/autoloader/issues).  

# Everything is falling apart!
If you have tried everything to fix your problem by yourself and still have had no luck, you can contact us either using the [issue tracker](https://bitbucket.org/musicspot/autoloader/issues) or on Twitter ([@LukasSkywalker](https://twitter.com/LukasSkywalker)).