# Creating Routes and Views: Understand how routes and views work in Pyramid.

## 1. What is a Route?

A **route** means a URL pattern.

Example:

```text
/home
/about
/contact
/students/10
```

In Pyramid, a route tells the framework:

```text
“When the user visits this URL, prepare to call a specific view.”
```

Pyramid’s official documentation says URL dispatch maps URLs to view code using pattern matching, and routes are checked one by one in order. ([Pylons Project][1])

Simple idea:

```text
URL = /about
Route = about
Meaning = this URL belongs to the about page
```

---

## 2. What is a View?

A **view** is the Python function or class that handles the request.

The view does the main work, such as:

```text
Receive request
Process logic
Get data
Return response
```

Officially, Pyramid describes a view callable as code that receives the request and returns a response object. ([Pylons Project][1])

Simple idea:

```text
Route = URL path
View = Python logic for that URL
```

---

## 3. Route and View Relationship

Think like this:

```text
User visits URL
      ↓
Pyramid checks route
      ↓
Route matches URL
      ↓
Pyramid calls connected view
      ↓
View returns response
      ↓
User sees result
```

Example concept:

```text
URL: /hello
Route name: hello
View: hello_view()
Response: Hello, World!
```

So the route is not the final output.
The route only finds **which view should run**.

---

## 4. Simple Flow Chart

```text
Browser Request
      ↓
URL: /about
      ↓
Pyramid Router
      ↓
Route Match: "about"
      ↓
View Function: about_view()
      ↓
Response Created
      ↓
Browser Shows Page
```

---

## 5. Small Example

```python
config.add_route('home', '/')
```

Meaning:

```text
Create a route named home
URL pattern is /
```

Then:

```python
config.add_view(home_view, route_name='home')
```

Meaning:

```text
Connect the home_view function with the home route
```

Together:

```text
/  →  home route  →  home_view()  →  response
```

The Pyramid docs explain that `add_route()` creates routes, while views can be connected to those route names using view configuration such as `add_view()` or `@view_config(route_name=...)`. ([Pylons Project][2])

---

## 6. Real-Life Analogy

Imagine a university office:

```text
Student asks: “Where is the accounts office?”
      ↓
Reception checks the direction list
      ↓
Reception says: “Go to Room 205”
      ↓
Room 205 solves the problem
```

In Pyramid:

```text
Student request = browser request
Direction list = routes
Room 205 = view
Solution = response
```

---

## 7. Static Route vs Dynamic Route

### Static Route

A static route is fixed.

```text
/about
/contact
/login
```

Example meaning:

```text
/about always opens the about page
```

---

### Dynamic Route

A dynamic route accepts changing values.

```text
/students/10
/students/25
/products/5
```

Here, `10`, `25`, and `5` are dynamic values.

Example:

```text
/students/10
```

Means:

```text
Show student whose ID is 10
```

In Pyramid, route patterns can include variables, and those values are taken from the URL and used inside the view. ([Pylons Project][1])

---

## 8. Important Pyramid Route Concept

Route order matters.

For example:

```text
/products/new
/products/{id}
```

If Pyramid checks `/products/{id}` first, it may think `new` is an ID.

So better order:

```text
/products/new
/products/{id}
```

Pyramid documentation notes that route declarations are matched in the order they are registered. ([Pylons Project][2])

---

## 9. Main Summary

```text
Route = URL pattern
View = function/class that handles the URL
route_name = bridge between route and view
Request = user action
Response = output sent back to browser
```

Super simple:

```text
URL comes in
Route catches it
View handles it
Response goes back
```

For your learning, just remember this line:

```text
In Pyramid, routes decide WHERE the request goes, and views decide WHAT response comes back.
```

[1]: https://docs.pylonsproject.org/projects/pyramid/en/latest/narr/urldispatch.html?utm_source=chatgpt.com "URL Dispatch — The Pyramid Web Framework v2.1"
[2]: https://docs.pylonsproject.org/projects/pyramid/en/latest/tutorials/wiki2/definingviews.html?utm_source=chatgpt.com "Defining Views — The Pyramid Web Framework v2.1"
