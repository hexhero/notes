# Eel

<https://github.com/ChrisKnott/Eel>

pip install eel

```python
import eel
eel.init('web')
eel.start('main.html')
```

```html
<script type="text/javascript" src="/eel.js"></script>
```

## js 调用 python

python
```py
@eel.expose
def my_python_function(a, b):
    print(a, b, a + b)
```

js
```js
eel.my_python_function(1, 2);
```

## python 调用 js

js
```js
eel.expose(my_javascript_function);
function my_javascript_function(a, b, c, d) {
  if (a < b) {
    console.log(c * d);
  }
}
```

python
```py
eel.my_javascript_function(1, 2, 3, 4)
```




