# DOM 是什么？

------

# ✅ 一句话解释（面试直接用）

👉
 **DOM（Document Object Model）是浏览器把网页解析后形成的一棵“树形结构”，程序可以通过它来读取和操作页面内容。**

 **DOM 是浏览器将 HTML 解析成的树形对象结构，UI 自动化正是通过操作 DOM 来定位元素、获取数据并执行操作。**

------

# 🧠 通俗理解（更容易记）

你可以把网页想象成：

👉 HTML 是“源码”
 👉 DOM 是“浏览器理解后的结构”

比如一个网页：

```
<html>
  <body>
    <button id="login">登录</button>
  </body>
</html>
```

浏览器会把它变成一棵树：

```
html
 └── body
      └── button (id=login)
```

👉 这棵树，就是 DOM

------

# 🔥 UI 自动化为什么离不开 DOM？

像你用 Selenium：

```
driver.find_element(By.ID, "login").click()
```

👉 实际上就是：

- 在 DOM 树里找到 id=login 的节点
- 然后操作它

------

# 📌 DOM 的核心能力

### 1️⃣ 查找元素

- id
- class
- xpath
- css

------

### 2️⃣ 获取信息

```
element.text
element.get_attribute("value")
```

------

### 3️⃣ 修改页面（JS 层面）

```
document.getElementById("login").innerText = "已登录"
```

------

# ⚠️ 面试常见追问

### ❓ DOM 和 HTML 有什么区别？

👉 标准回答：

| HTML          | DOM            |
| ------------- | -------------- |
| 静态文本      | 动态对象       |
| 写给人/浏览器 | 给程序操作     |
| 不会变        | 可以被 JS 修改 |

------

### ❓ 为什么 Selenium 定位不到元素？

👉 常见原因：

- 元素还没加载（DOM 未生成）
- 在 iframe 里
- 被 JS 动态修改
- XPath 写错

------

# 💡 再给你一个高级理解（加分）

👉
 **DOM 本质是浏览器提供的一套 API，让程序可以像操作对象一样操作网页结构**