# rails中自定义请求头

~~~~
 class AssetHeaders
   def initialize(app)
    @app = app 
   end
   
   def call(env)
      request = Rack::Request.new(env)
      response = @app.call(env)
      if request.path =~ /^\/assets\//
        response[1]["Access-Control-Allow"] = "*"
      end
      response
    end 
 end
 
  Railscasts::Application.configure do
    config.middleware.use "AssetHeaders"
  end
~~~~

