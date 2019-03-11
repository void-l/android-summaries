# Android Animations
android 常用动画总结，应用场景介绍
## Tween Animation
完全由属性动画代替

## Frame Animation
序列帧动画， 一些特殊的页面加载状态提示可以考虑序列帧动画。由设计师提供固定的序列帧图片，开发通过AnimationDrawable定义动画帧即可。

[Lottie](https://airbnb.design/lottie/) is an iOS, Android, and React Native library that renders After Effects animations in real time, allowing apps to use animations as easily as they use static images.

## Property Animation
动画的组成要素：view target、property、interpolater、duration、listener
- view target: 动画控制的目标view，动画的呈现的对象
- property: 动画控制的属性，变化量，一个或者多个
- interpolater: 差值器
- duration:  动画时长
- listener: 动画执行回调，onStart/ onUpdating/ onEnd/ onRepeat/ onCancle

常用的属性动画：ValueAnimator、ObjectAnimator、AnimatorSet

常见的动画场景：
- 简单动画： 控制对象的单一属性
    - ValueAnimator， 由红色动画渐变为白色
    - ObjectAnimator, 简单的平移、透明度、缩放动画
```java
ObjectAnimator.ofFloat(myView, "rotation", 0f, 360f);
```
- 多属性动画： 控制对象的多个属性
    - PropertyValueHolder + ObjectAnimator
```java
PropertyValuesHolder pvhX = PropertyValuesHolder.ofFloat("x", 50f);
PropertyValuesHolder pvhY = PropertyValuesHolder.ofFloat("y", 100f);
ObjectAnimator.ofPropertyValuesHolder(myView, pvhX, pvhY).start();
```
- 动画组：控制对个对象同时进行动画
    - AnimatorSet， 上述两类动画的组合，可以设置并行或者串行执行
- 关键帧动画
    - KeyFrame + PropertyValueHodler + ObjectAnimator
```java
Keyframe kf0 = Keyframe.ofFloat(0f, 0f);
Keyframe kf1 = Keyframe.ofFloat(.5f, 360f);
Keyframe kf2 = Keyframe.ofFloat(1f, 0f);
PropertyValuesHolder pvhRotation = PropertyValuesHolder.ofKeyframe("rotation", kf0, kf1, kf2);
ObjectAnimator rotationAnim = ObjectAnimator.ofPropertyValuesHolder(target, pvhRotation);
rotationAnim.setDuration(5000);
```


## Physics-based motion
基于物理引擎的动画，更符合现实中的自然效果

- Spring Animation

- Fling Animation


## Pixel Animation(Using OpenGL)
- 坐标系转换: 世界坐标系与屏幕坐标系的转换，在投影视图下，如何将特定z值平面转化为屏幕坐标
- CPU vs GPU 之工作方式的不同
- 渲染管线： vertex shader & fragment shader