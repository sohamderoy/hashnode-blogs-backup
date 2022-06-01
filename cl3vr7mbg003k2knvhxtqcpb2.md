## 8 ways to Center a Div like a pro 😎

As a web developer, sometimes **centring a div** feels like it is one of the toughest jobs on planet Earth. Well, not anymore. The following article lists down **8 different ways for centring a `div`**. We will explore how to centre divs using CSS **positions property, flexbox and grid**. After reading this whole article, I am sure that you will start **centring divs like a pro**.

![giphy.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1653570941669/jfm0gE2bu.gif align="left")

For this blog, I will be using the same HTML for all the 8 methods which are given below. It just contains a parent `div` and a child `div` inside it. The main aim of this article is to centre the inner `div` with respect to its parent. I will only be changing the CSS files for all the 8 different methods to take effect.

The common HTML file goes like this

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Centering divs</title>
    <link rel="stylesheet" href="./basicStyle.css" />
    <!-- Change the link of CSS file here -->
    <link rel="stylesheet" href="" />
    <style>
      * {
        box-sizing: border-box;
        margin: 0px;
        padding: 0px;
      }
    </style>
  </head>
  <body>
    <div id="parentContainer">
      <div id="childContainer"></div>
    </div>
  </body>
</html>
```

With just the basic styling as given in the following lines

```
#parentContainer {
  width: 400px;
  height: 400px;
  background-color: #f55353;
}
#childContainer {
  width: 100px;
  height: 100px;
  background-color: #feb139;
}
```

we will get something like this


![Screenshot 2022-05-27 at 15.02.59.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653644083895/XWCVoBQG6.png align="left")

We just make a parent `div` and give it a `width` and `height` of `400px`, and a `color` of `#f55353`. Similarly we create a child `div` inside it and give it a `width` and `height` of `100px` and give it a `color` of `#feb139`.
The final goal of this article will be to make this transformation


![Group 23.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653578471160/GDMSEOy5G.png align="left")

## Using CSS `position` property

### 1. Using position: relative, absolute and top, left offset values

```
#parentContainer {
  position: relative;
}
#childContainer {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
``` 

### 2. Using position: relative and absolute, top, left, right and bottom offset values and margin: auto

```
#parentContainer {
  position: relative;
}
#childContainer {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
}
```

## Using CSS Flexbox

### 3. Using flexbox, justify-content and align-item

```
#parentContainer {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### 4. Using flexbox, justify-content and align-self

```
#parentContainer {
  display: flex;
  justify-content: center;
}
#childContainer {
  align-self: center;
}
```

### 5. Using flexbox and margin: auto

```
#parentContainer {
  display: flex;
}
#childContainer {
  margin: auto;
}
```

## Using CSS Grid

### 6. Using grid and place-items

```
#parentContainer {
  display: grid;
  place-items: center;
}
```

### 7. Using grid, justify-content and align-items

```
#parentContainer {
  display: grid;
  justify-content: center;
  align-items: center;
}
```

### 8. Using grid, align-self and justify-self
```
#parentContainer {
  display: grid;
}
#childContainer {
  align-self: center;
  justify-self: center;
}
```

## The Result

Well as expected, following any of the above methods will result in this

![Screenshot 2022-05-27 at 15.02.39.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653644104196/cUlZ2WwiW.png align="left")

## Summary

In this article, we saw how to centre a div using 8 different methods viz.

1. Using **position: relative**, **absolute** and **top**, **left** offset values
2. Using **position**: **relative** and **absolute**, **top**, **left**, **right** and **bottom** offset values and **margin: auto**
3. Using **flexbox**, **justify-content** and **align-item**
4. Using **flexbox**, **justify-content** and **align-self**
5. Using **flexbox** and **margin: auto**
6. Using **grid** and **place-items**
7. Using **grid**, **justify-content** and **align-items**
8. Using **grid**, **align-self** and **justify-self**

## Github link

Github link for all the files for all the methods mentioned above can be found here: [Github Link](https://github.com/sohamderoy/blog-setup-centring-divs)

## Wrapup

Thanks for reading! I hope you liked this short and quick article on different methods to centre a `div`. Do consider hitting the like button and sharing it with your friends, I'd really appreciate that. Stay tuned for more amazing content! Peace out! 🖖

## Social Links

- [LinkedIn](linkedin.com/in/sohamderoy)
- [Website](www.sohamderoy.dev)
- [Blog site](blog.sohamderoy.dev)

 



