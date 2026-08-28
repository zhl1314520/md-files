| 场景         | EC 方法                                |
| ------------ | -------------------------------------- |
| 元素是否存在 | presence_of_element_located            |
| 元素是否可见 | visibility_of_element_located          |
| 点击按钮     | element_to_be_clickable                |
| 判断文本     | text_to_be_present_in_element          |
| iframe       | frame_to_be_available_and_switch_to_it |
| loading消失  | invisibility_of_element_located        |
| url 地址包含 | url_contains()                         |

## url_contains()

> ```python
> WebDriverWait(self.driver, 10).until(
>     EC.url_contains("/login")
> )
> ```

## text_to_be_present_in_element()

```python
is_display_Success = (By.XPATH, "//div[contains(@role, 'alert')]")

WebDriverWait(self.driver, 10).until(
EC.text_to_be_present_in_element(self.is_display_Success, "Success! Account created successfully for")		# 可以写部分文本，只要包含即可
    )
```

## presence_of_element_located()

> ```python
> WebDriverWait(self.driver, 5).until(
>     EC.presence_of_element_located((By.ID, "username"))
> )
> ```

## 显示等待 & 隐式等待

- ### 显式等待

  > ```python
  > WebDriverWait(self.driver, 5).until(
  >  EC.presence_of_element_located((By.ID, "username"))
  > )
  > ```

- ### 隐式等待

  > ```python
  > driver.implicitly_wait(5)
  > 
  > element = driver.find_element(By.ID, "login")
  > ```

- ### 共同点

  > 找到后立即继续，不会等满设置的时间，即：假如设置等待时间为 10s，在 2s 就找到了元素，那么直接继续下面的代码，不会等待到 10s

- ### 核心区别

  > 1. 显式等待：指定具体条件是否满足，例如：EC.presence_of_element_located()，常与 EC 一起使用
  > 2. 隐式等待：只能判定元素能不能找到，最典型的就是联合 find_element()、find_elements() 使用