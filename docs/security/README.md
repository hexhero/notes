# 安全

## XSS 注入

```html
<img src="xxx.jpg" alt="An xss injection vulnerability" onerror="(() => { alert('you are hacked'); })()">
```