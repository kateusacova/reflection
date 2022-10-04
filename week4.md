# Web Applications

## Learning Objectives
- Explain how HTTP requests and responses work at a high level
- Write integration tests for a web application
- Implement web routes using a lightweight web framework
- Follow a debugging process for a web application
- Deploy a web application using a light cloud service such as Heroku

```
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
 ```     

## HTTP

- **Server**
  - Central machine where the program runs
  - e.g. Ruby program
- **Client** 
  - machine and software used by users to interact with the program 
  - e.g. Postman, web browser
- HTTP request defined by:
  - method (e.g. get, post, delete, update)
  - path (e.g. /news)
  - parameters (request data)
- HTTP responnse defined by:
  - status code (e.g. 200, 404)
  - body (content)
- 

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


## CRUD Routes

```
  ┌────────┐HTTP┌────────┐Meth┌────────┐SQL ┌────────┐
  │        ├───►│        ├───►│        ├───►│        │
  │Client  │req │Sinatra │call│Repo    │q.  │Database│
  │        │    │app     │    │Class   │    │        │
  │GET     │    │        │    │        │    │        │
  │/albums │HTTP│AlbumRep│Ret │        │Res │        │
  │        │◄───┤@all    │◄───┤        │◄───┤        │
  └────────┘resp└────────┘val └────────┘set └────────┘
```

- HTTP routes designes to map to CRUD operations on the database
- e.g.

```
# Albums resource: 

# List all the albums
Request: GET /albums
Response: list of albums

# Read a single album
Request: GET /albums/1
Response: of a single album

# Create a new album
Request: POST /albums
  With body parameters: "title=OK Computer"
Response: None (just creates the resource on the server)

# Update a single album
Request: PATCH /albums/1
  With body parameters: "title=OK Computer"
Response: None (just updates the resource on the server)

# Delete an album
Request: DELETE /albums/1
Response: None (just deletes the resource on the server)
```

- This patter of routing is called **REST** 
  - maps HTTP request to CRUD operations

### Path parameters

```ruby
# GET /albums/1   -> get album with ID 1
# GET /albums/5   -> get album with ID 5
# GET /albums/12   -> get album with ID 12

get '/albums/:id' do
  album_id = params[:id] # Path parameter
end
```

## HTML Responses

```
app.rb
lib/
  ...
views/
  index.erb
```

We should separate the two 
- program logic (Ruby files)
- response content (HTML code)
  - so we write it in a ***view file*** in views/ dir

```ruby
context "GET to /" do
  it 'contains a h1 title' do
    response = get('/')

    expect(response.body).to include('<h1>Hello</h1>')
  end
  
  it 'contains a div' do
    response = get('/')

    expect(response.body).to include('<div>')
  end
end
```

## ERB

**ERB file**
- Uses Ruby variables to generate a meaningful HTML page
  - NO! new variables/call methods that change the program
- YES to:
  - display values of variables
  - loop through an array of values (to display some HTML for each item)
  - use conditions to display different bits of HTMl

```erb

# Interpolating variables
<p>
  <%= @name %=> 
</p>

# Conditions

<div>
  <% if @posts.length > 0 %> 
    <p>There are <%= @posts.length %> posts on this website.</p>
  <% else %>
    <p>No posts yet!</p>
  <% end %>
</div>

# Loops

<div>
  <% @posts.each do |post| %>
    <p>
      <%= post.title %>
      <%= post.author_name %>
    </p>
  <% end %>
</div>
```





