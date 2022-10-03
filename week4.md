# Web Applications

## Learning Objectives
- Explain how HTTP requests and responses work at a high level
- Write integration tests for a web application
- Implement web routes using a lightweight web framework
- Follow a debugging process for a web application
- Deploy a web application using a light cloud service such as Heroku


 ┌──────────────┐        ┌──────────────────────────────┐
 │ Browser      │        │                              │
 │              │        │  ┌──────────┐   ┌──────────┐ │
 │ Mobile apps  │        │  │  Program │   │PostgreSQL│ │
 │              │  HTTP  │  │          │SQL│          │ │
 │ Curl         ├───────►│  │          ├──►│          │ │
 │              │        │  │          │   │          │ │
 │ Postman      │        │  │          │   │          │ │
 │              │        │  └──────────┘   └──────────┘ │
 │              │        │                              │
 └──────────────┘        └──────────────────────────────┘
      Client                          Server
      
      
## Sinatra

- Ruby library

**Routing**
- Web server receives HTTP requests => executes the code depending on request => returns a response
- Sintra has a 'routing' table
  - Associates given request method and path to a block of Ruby code

|Method|Path|Ruby code|
|-|-|-|
|GET|/|`# some code to execute`
|POST|/|`# some different code to execute`

```ruby
get '/' do
    # The code here is executed when a request is received,
    # and need to send a response. 

    # We can simply return a string which
    # will be used as the response content.
    # Unless specified, the response status code
    # will be 200 (OK).
    return 'Some response data'
```
- This block is called 'route block' 
- Executes only if the received request matches the method and path
  - Executes the first one that was matched

```ruby
# Request:
# GET /?name=David

get '/' do
  name = params[:name] # The value is 'David'

  # Do something with `name`...

  return "Hello #{name}"
end
```
- params hash used to access the request query parameters

```ruby
# Request:
# POST /hello
#   With body parameter: name=Alice

post '/hello' do
  name = params[:name] # The value is 'Alice'

  # Do something with `name`...

  return "Hello #{name}"
end
```
- can also be used to retrieve body parameters sent with POST request

