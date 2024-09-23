# Thymeleaf

Thymeleaf is a modern server-side Java template engine for both web and standalone environments,
capable of processing HTML, XML, JavaScript, CSS and even plain text.

Unlike other templating languages, Thyleleaf is a **valid HTML**, meaning its' templates
can be displayed in the browsers unrendered.

[Link to the docs](https://www.thymeleaf.org/documentation.html)

---

### Getting Started

To get started create an HTML file with `th` namespace.


```html
<!DOCTYPE html>
<html lang="en" xmlns:th="https://www.thymeleaf.org">
<head>
  <meta content="text/html; charset=UTF-8" http-equiv="Content-Type"/>
  <title>Thyleleaf template example</title>
</head>
<body>
  <span th:text="${today}">13 february 2011</span>
</body>
</html>
```

### Expression Syntax

[Link to the docs](https://www.thymeleaf.org/doc/tutorials/3.1/usingthymeleaf.html#standard-expression-syntax)

* **Simple expressions:**
  * Variable Expressions: `${...}` [*docs*](https://www.thymeleaf.org/doc/tutorials/3.1/usingthymeleaf.html#variables)
  * Selection Variable Expressions: `*{...}`
  * Message Expressions: `#{...}` [*docs*](https://www.thymeleaf.org/doc/tutorials/3.1/usingthymeleaf.html#messages)
  * Link URL Expressions: `@{...}` [*docs*](https://www.thymeleaf.org/doc/tutorials/3.1/usingthymeleaf.html#link-urls)
  * Fragment Expressions: `~{...}`
* **Literals:**
  * Text literals: `'one text'`, `'Another one!'`,…
  * Number literals: `0`, `34`, `3.0`, `12.3`,…
  * Boolean literals: `true`, `false`
  * Null literal: `null`
  * Literal tokens: `one`, `sometext`, `main`,…
* **Text operations:**
  * String concatenation: `+`
  * Literal substitutions: `|The name is ${name}|`
* **Arithmetic operations:**
  * Binary operators: `+`, `-`, `*`, `/`, `%`
  * Minus sign (unary operator): `-`
* **Boolean operations:**
  * Binary operators: `and`, `or`
  * Boolean negation (unary operator): `!`, `not`
* **Comparisons and equality:**
  * Comparators: `>`, `<`, `>=`, `<=` (`gt`, `lt`, `ge`, `le`)
  * Equality operators: `==`, `!=` (`eq`, `ne`)
* **Conditional operators:**
  * If-then: `(if) ? (then)`
  * If-then-else: `(if) ? (then) : (else)`
  * Default: `(value) ?: (defaultvalue)`
* **Special tokens:**
  * No-Operation: `_`

All these features can be combined and nested:

```
'User is of type ' + (${user.isAdmin()} ? 'Administrator' : (${user.type} ?: 'Unknown'))
```

### Common usage examples

#### Replace text contents

```html
<!--Unascaped text-->
<p th:utext="#{home.welcome}"></p>

<!--Text with substitution-->
<p th:text="|state = ${state.name()}|"></p>

<!--Text with a placeholder value-->
<p th:text="${product.details()}">A placeholder</p>
```

#### Insert a fragment

```html
<!--Declare a fragment 'my-fragment' that accepts a 'fragId' parameter.-->
<div th:fragment="my-fragment (fragId)" th:text="|fragment = ${fragId}|"></div>

<!--Option 1: Insert a 'my-fragment' fragment into div.-->
<div th:insert="~{::my-fragment (fragId=1)}">...</div>

<!--Option 2: Replace a div by 'my-fragment' fragment.-->
<div th:replace="~{::my-fragment} (fragId=2)">...</div>

<!--The options above ^^^ show how to insert a fragment that is declared
in a single html file.
In order to use fragment from another file it's required to specify
the file name (without .html extension).-->
<div th:insert="~{my-file::my-fragment (fragId=3)}">...</div>
```
