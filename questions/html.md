# HTML and Semantics

How you can improve the following markup?

```html
<div>My Favorite Colors</div>
<div>
  <div>Red</div>
  <div>Green</div>
  <div>Blue</div>
</div>
```

***

What's the problem with this code?

```html
<div>
A quam enim <h1>This text needs to be big</h1> omnis et. Consequatur recusandae accusantium illum corporis ea necessitatibus molestiae enim amet. Non voluptatem quasi illum consequatur quibusdam. Consequatur magni aut. Dignissimos quam et.
</div>
```

***

Which version is better? Why?

```html
<article class="tweet">
  <header class="header">
    <img class="avatar" alt="...">
    …
  </header>
  <div class="body-text">
    …
  </div>
</article>
```

```html
<article class="Tweet">
  <header class="Tweet-header">
    <img class="Tweet-avatar" alt="...">
    …
  </header>
  <div class="Tweet-bodyText">
    …
  </div>
</article>
```

***

Which version is better for screen readers? Why?

```html
Click <span onclick="register()">register</span> to learn more
```

```html
Click <button onclick="register()">register</button> to learn more
```
