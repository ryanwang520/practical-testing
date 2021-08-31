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

## Why bother writing tests?

- Ship new features confidently
- Detect regression when features change
- Refactor code without fear
- Thinking in tests helps you write better code. Code is easy to test means that it's likely easy to be understood

Last but most important:

We don't want to ship bugs to production, which make our product lose users, lose money, and lose our reputation.

<style>


</style>

---
layout: two-cols
---

# What to Test

<br>

The Testing Pyramid?

<img src="https://martinfowler.com/bliki/images/testPyramid/test-pyramid.png" width="300">

::right::

The Testing Trophy!

<br>
<br>

<img src="https://pbs.twimg.com/media/DVUoM94VQAAzuws?format=jpg&name=900x900" width="300">

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

It's often better to use some other GUI tools like [Postman](https://www.getpostman.com/) or [Apifox](https://www.apifox.cn/) to create test suites.

---
layout: two-cols
---

# Static analysis tools.

<br>

- Code Linter

  ```python
  def f(a: int, b: int) -> int:
     return a + b
  # C0103: Function name "f" doesn't conform to snake_case naming style (invalid-name)
  # C0103: Argument name "a" doesn't conform to snake_case naming style (invalid-name)
  # C0103: Argument name "b" doesn't conform to snake_case naming style (invalid-name)
  # C0116: Missing function or method docstring (missing-function-docstring)
  ```

- Type Check

  ```python
  def f(a: int, b: int) -> int:
    return a + b

  f(1, 'str')   # Argument 2 to "f" has incompatible type "str"; expected "int"
  ```

::right::

<div class="mt-22 ml-10">

- Security Check

  ```python
  password = '123456'
  """
  Issue: [B105:hardcoded_password_string] Possible hardcoded password: '123'
   Severity: Low   Confidence: Medium
   More Info: https://bandit.readthedocs.io/en/latest/plugins/b105_hardcoded_password_string.html
  """
  ```

- Complexity Check

  <img src="https://wily.readthedocs.io/en/latest/_images/wily_report.png" class="object-cover h-38" style="object-position: top left;" width="400">

</div>

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

  - avoid global state as much as possible
  - fixtures for each test case should be isolated
  - fixtures should not rely on implementation details

- Test double

  - mocks(same api, only check if function or method is called as expected)
  - stubs(fixed result)
  - fake(mimic actual behavior, think of using inmemory database for testing)

---

# When to test

- commit-hook
- ci
- whenever

---

# Final Thoughts

<br>

- Tests result should be consistant, no surprising result each time
- Tests should be understandable
- Tests shouldn't depend on the execution order
- Tests should be easy to maintain
- Tests should be quickly to run
- 100% test coverage is a lie.
- Whenever a bug is reported, write some tests to reappear it.

<br>
<div class="text-center">
<h2 class="text-blue-500">Be practical!</h2>
</div>

<p> <span class="text-red-400">Don't be obessed by the concepts,</span> no one cares whether it's a unit test or integration test as long as it's a good test.</p>

<p><span class="text-red-400">Don't test too much!</span> You don't have to write tests for every single piece of code.</P>

<p>You write tests because you want to <span class="text-red-400">ship your code more confidently.</span></p>
