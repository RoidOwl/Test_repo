require 'sinatra'
require 'sinatra/reloader' if development?

get '/testupload' do
  slim :index
end

__END__

@@layout
doctype html
html
  head
    title Sinatra & Slim Example
  body
    == yield

@@index
h1 Hello from Sinatra and Slim!
p This is a simple example combining Sinatra's routing with Slim's templating.