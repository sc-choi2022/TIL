### Quiz

```html
<p>1</p>
<p class="blue">2</p>
<p class="blue green">3</p>
<p class="green blue">4</p>
<p id="red" class="blue">5</p>
<h2 id="red" class="blue">6</h2>
<p id="red" class="blue" style="color: yellow;">7</p>
<h2 id="red" class="blue" style="color: yellow;">8</h2>
```

```css
h2 {
  color: darkviolet !important;
}

p {
  color: orange;
}

.blue {
  color: blue;
}

.green {
  color: green;
}

#red {
  color: red;
}
```



**상속**

02_inheritance.html

```html
<body>
  <p>안녕하세요<span>김싸피</span>입니다.</p>
</body>
```

```html
<style>
  p {
    /* 상속됨 */
    color: red;
    /* 상속 안됨*/
    border: 1px solid black;
}
  span{
    border: 1px solid blue;
}
</style>
```

