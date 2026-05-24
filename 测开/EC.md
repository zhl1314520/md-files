| 场景         | EC 方法                                |
| ------------ | -------------------------------------- |
| 元素是否存在 | presence_of_element_located            |
| 元素是否可见 | visibility_of_element_located          |
| 点击按钮     | element_to_be_clickable                |
| 判断文本     | text_to_be_present_in_element          |
| iframe       | frame_to_be_available_and_switch_to_it |
| loading消失  | invisibility_of_element_located        |

```python
WebDriverWait(self.driver, 10).until(
    EC.url_contains("/login")
)
```

```python
WebDriverWait(self.driver, 5).until(
    EC.presence_of_element_located((By.ID, "username"))
)
```