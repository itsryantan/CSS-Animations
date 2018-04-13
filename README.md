# _Just some research n study_

### [Dots-Opacity](https://github.com/itsryantan/CSS-Animations/tree/master/Dots-Opacity)
* Effect

![Dots Opaciity](https://upload-images.jianshu.io/upload_images/5830070-714683f9e2003929.gif?imageMogr2/auto-orient/strip)
* Principle

    Use `animation` like this ⬇️ to control the status(time/position/opacity) of animation.
  <pre><code>-webkit-animation: opacity 1s ease 0s infinite forwards;
  </code></pre>

    By using `keyframes` `opacity` like this ⬇️ to control the keyframes of the animation.
  <pre><code>@-webkit-keyframes opacity {
    0% {
        opacity: 0;
    }
    50% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
  }
  </code></pre>


----------

### [Dots-Wave](https://github.com/itsryantan/CSS-Animations/tree/master/Dots-Wave)
* Effect

![Dots Wave](https://upload-images.jianshu.io/upload_images/5830070-920b920baadae14d.gif?imageMogr2/auto-orient/strip)
* Principle

    Use `animation` like this ⬇️ to control the status(time/position/opacity) of animation.
  <pre><code>-webkit-animation:move 1s ease 0s infinite forwards;
  </code></pre>

    By using `keyframes` `opacity` like this ⬇️ to control the keyframes where the dots should change direction and position of the animation.
  <pre><code>@-webkit-keyframes move {
    0% {
        transform: translateY(5px);
        animation-timing-function: ease;
    }
    50% {
        transform: translateY(-5px);
        animation-timing-function: ease;
    }
    100% {
        transform: translateY(5px);
        animation-timing-function: ease;
    }
  }
  </code></pre>

----------

### [Circle-Wave](https://github.com/itsryantan/CSS-Animations/tree/master/Circle-Wave)
* Effect

![Circle Wave](https://upload-images.jianshu.io/upload_images/5830070-aa828b96938d228b.gif?imageMogr2/auto-orient/strip)
* Principle

    Obviously, it's a hard one. I tried to use `animation` as usual but somehow found that they kept zooming from the corner rather than the center. So I tried to use `scale`, yeah it zoomed as I wish but the border zoomed at the same time. 

    Finally! (Thank god I did it.) I thought maybe I can use `radial-gradient` to simulate the border like:
  <pre><code>background: radial-gradient(circle, #fff 69%, #333 69%);
  </code></pre>

    AND！Use my favorite `keyframes` `opacity` `transform：scale` at the same time like magic.

    Btw the `opacity` here is for the "fade in" effect during zooming so it can become REALLY gentle.BP
  <pre><code>@-webkit-keyframes opacity {
    0% {
        opacity: 0;
    }
    50% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
  }
  @-webkit-keyframes zoom {
    0% {
        -webkit-transform: scale(0);
    }
    100% {
        -webkit-transform: scale(3);
    }
  }</code></pre>

----------

### [Dots-Move-Regular](https://github.com/itsryantan/CSS-Animations/tree/master/Dots-Moving-Regular)
* Effect

![Dots-Move-Regular](https://upload-images.jianshu.io/upload_images/5830070-42e15e77b174403c.gif?imageMogr2/auto-orient/strip)
* Principle

    Using position property to control the path of dots moving like a rectangle.

    Locate the positions of dots in axes and adjust the angle at first. Then input the position data in the `transform: translate(X,Y)`. And it should contain 5 `keyframes` which was divided into 5 equal parts from 0% to 100% like 0%/25%/50%/75%/100%. The 0% and 100% should be totally same so the dots can always back to the beginning after they finished a round.

    You might find the size of the path would be reduced. It's because 4 dots were moving at the same time, they actually formed a smaller rectangle when they were moving to the middle of the single path. You can find out why in this picture⬇️.

    ![Axes of Regular](https://upload-images.jianshu.io/upload_images/5830070-793cf9570cfe9ffb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    About how to set the position, you can get your answer in the code here⬇️.
 
  <pre><code>@-webkit-keyframes move {
    0% {
        transform: translate(40px,-20px);
        animation-timing-function: ease;
    }
    25% {
        transform: translate(-20px,-40px);
        animation-timing-function: ease;
    }
    50% {
        transform: translate(-40px,20px);
        animation-timing-function: ease;
    }
    75% {
        transform: translate(20px,40px);
        animation-timing-function: ease;
    }
    100% {
        transform: translate(40px,-20px);
        animation-timing-function: ease;
    }
  }
  </code></pre>

----------

### [Dots-Move-Perspective](https://github.com/itsryantan/CSS-Animations/tree/master/Dots-Moving-Perspective)
* Effect

![Dots-Move-Perspective](https://upload-images.jianshu.io/upload_images/5830070-619a74b794c32096.gif?imageMogr2/auto-orient/strip)
* Principle

    Adjust the size of the dots while changing the position property.

    It won't work if you add another animation code to the existing code, it will only cover your original code and to perform by sorting. So we need to add `width` and `height` properties to `transform` of the existing code. 

    Sort the size from the smallest to the biggest and add to 25% at first. Why? Because our animation is starting from 0% and the smallest dot is located at the position of 25% if we are going to draw a perspective path. 

    Also, we need to change the position at the same time. Just repeat 
    > Locate the positions of dots in axes and adjust the angle at first. Then input the position data in the `transform: translate(X,Y)`.

    So the final effect should be like this⬇️.

    ![Axes of Perspective](https://upload-images.jianshu.io/upload_images/5830070-4b3dd9910ad3948d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    To set the `width`,`height` and `border-radius`(to ensure your dots will be a circular all the time) properties, just follow the `transform` of every `keyframes`⬇️.
 
  <pre><code>@-webkit-keyframes move {
    0% {
        transform: translate(35px,-30px);
        width: 20px;
        height: 20px;
        border-radius: 15px;
    }
    25% {
        transform: translate(-20px,-20px);
        width: 15px;
        height: 15px;
        border-radius: 15px;
    }
    50% {
        transform: translate(-35px,20px);
        width: 20px;
        height: 20px;
        border-radius: 15px;
    }
    75% {
        transform: translate(40px,40px);
        width: 25px;
        height: 25px;
        border-radius: 15px;
        animation-timing-function: ease;
    }
    100% {
        transform: translate(35px,-30px);
        width: 20px;
        height: 20px;
        border-radius: 15px;
        animation-timing-function: ease;
    }
  }
  </code></pre>

----------
