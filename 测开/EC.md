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

## pre