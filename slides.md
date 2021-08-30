---
# try also 'default' to start simple
theme: apple-basic
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
---

# Practical Testing

<br>
<br>

## Why writing test?

- Ship new features confidently
- Detect regression when features change
- Refactor code without fear
- Thinking in test helps you write better code. Code is easy to test means that it's likely easy to be understood

<style>

h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}
</style>

---

# What to Test

<br>

The classic test pyramid

<br>
<br>

<img src="https://automationpanda.files.wordpress.com/2017/10/the-testing-pyramid.png" width="300">

---

# Unit Tests

<br>

Focus on some distinct units of code in a relatively isolated manner.

<br>

```python
def fib(n):
  return 1 if n <= 1 else fib(n - 1) + fib(n - 2)

def test_fib():
  assert fib(0) == 1
  assert fib(1) == 1
  assert fib(2) == 1
  assert fib(3) == 2
  assert fib(4) == 3
  assert fib(5) == 5
  # fib(-1) ?

```

---

# Integration Tests

<br>

A system is usually built up of multiple components, modules, or subsystems. Integration tests are tests that verify that the system is working as expected.

<br>

```python
def signup():
  create_user()
  create_user_profile()
  send_activation_link()
  generate_auth_token()

def test_signup():
  signup()
  assert_user_created()
  assert_profile_created()
  assert_activate_link_sent()
  assert_auth_token_generated_correct()
```

---

# End2end Tests

<br>

End2end Tets These test typical journeythrough a whole software system from start to finish.

```python
def test_make_order_flow():
  client = TestClient()
  client.post('/signup', data={'username': 'test', 'password': 'test'})
  client.post('/activate', data={'token': 'test'})
  client.post('/login', data={'username': 'test', 'password': 'test'})
  client.get('/products')
  client.get('/product/<product_id>')
  client.post('/checkout')
  client.post('/make_order')
  client.get('/order/<order_id>')
```

It's often better to use some other GUI tools like [Postman](https://www.getpostman.com/) and [Apifox](https://www.apifox.cn/) to create test suites.

---

<div class="text-center mt-24">
<h1>But that's not the whole story.</h1>
</div>

---

<br>
<br>

## Introducing static analysis tools.

<br>

- Code Formatter

- Code linter

- Type Check

- Security Check

- Complexity check

---

# How to write a test case?

<br>

## Arrange

Set up the application state.

## Act

Call the function or methods you'd like to test.

## Assert

Ensure the behavior is just what you expect.

---

# Test Setup

- Fixtures

- Test double

  - mocks(same api, only check if function or method is called as expected)
  - stubs(fixed result)
  - fake(mimic actual behavior, think of using inmemory database for testing)

---

# When to test

- commit-hook
- ci
- before release

---

# Final Thoughts

<br>

- Tests result should be consistant, no surprising result each time
- Tests should be understandable
- Tests shouldni't depend on the execution order
- Tests should be easy to maintain
- Tests should be automated
- Tests should be quickly to run
