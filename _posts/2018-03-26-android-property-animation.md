---
layout: default
title: Android 属性动画
---

# Android 属性动画

## ValueAnimator

```java
// 平滑过渡
ValueAnimator anim = ValueAnimator.ofFloat(0f, 1f);
anim.setDuration(300);
anim.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
    @Override
    public void onAnimationUpdate(ValueAnimator animation) {
        float currentValue = (float) animation.getAnimatedValue();
        Log.d("TAG", "cuurent value is " + currentValue);
    }
});
anim.start();
```
```java
// 多段过渡
ValueAnimator anim = ValueAnimator.ofFloat(0f, 5f, 3f, 10f);
anim.setDuration(5000);
anim.start();

// ValueAnimator 也有 ofInt ofObject 等值的类型操作
// 还可以调用 setStartDelay() setRepeatCount() setRepeatMode() 等相关 API
```

## ObjectAnimator

```java
// API: public static ObjectAnimator ofInt(Object target, String propertyName, int... values)
// ObjectAnimator内部的工作机制并不是直接对我们传入的属性名进行操作的，而是会去寻找这个属性名对应的get和set方法
ObjectAnimator.ofFloat(textview, "alpha", 1f, 0f);
// 示例
ObjectAnimator animator = ObjectAnimator.ofFloat(textview, "alpha", 1f, 0f, 1f);
animator.setDuration(5000);
animator.start();
ObjectAnimator animator = ObjectAnimator.ofFloat(textview, "rotation", 0f, 360f);
animator.setDuration(5000);
animator.start();
float curTranslationX = textview.getTranslationX();
ObjectAnimator animator = ObjectAnimator.ofFloat(textview, "translationX", curTranslationX, -500f, curTranslationX);
animator.setDuration(5000);
animator.start();
ObjectAnimator animator = ObjectAnimator.ofFloat(textview, "scaleY", 1f, 3f, 1f);
animator.setDuration(5000);
animator.start();

// API 示例
ValueAnimator valueAnimator = ValueAnimator.ofArgb(0xffff0000, 0xff00ff00, 0xff0000ff, 0xffff0000)
        .setDuration(4000);
valueAnimator.setRepeatCount(1);
valueAnimator.setRepeatMode(ValueAnimator.RESTART);
valueAnimator.setStartDelay(200);
valueAnimator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
    @Override
    public void onAnimationUpdate(ValueAnimator animation) {
        tv.setBackgroundColor((Integer) animation.getAnimatedValue());
        Log.d("animationValue", animation.getAnimatedValue().toString());
    }
});
// AnimatorListenerAdapter 继承自 AnimatorListener 和 AnimatorPauseListener 接口，空实现
valueAnimator.addListener(new AnimatorListenerAdapter() {
    @Override
    public void onAnimationEnd(Animator animation) {
        // ObjectAnimator inherit from ValueAnimation.
        ObjectAnimator.ofFloat(tv, "textSize", textSize, 36f, textSize)
                .setDuration(5000)
                .start();
    }
});
valueAnimator.start();
```

## 组合动画

实现组合动画功能主要需要借助AnimatorSet这个类，这个类提供了一个play()方法，如果我们向这个方法中传入一个Animator对象(ValueAnimator或ObjectAnimator)将会返回一个AnimatorSet.Builder的实例，AnimatorSet.Builder中包括以下四个方法：

- after(Animator anim)   将现有动画插入到传入的动画之后执行
- after(long delay)   将现有动画延迟指定毫秒后执行
- before(Animator anim)   将现有动画插入到传入的动画之前执行
- with(Animator anim)   将现有动画和传入的动画同时执行

```java
ObjectAnimator moveIn = ObjectAnimator.ofFloat(textview, "translationX", -500f, 0f);
ObjectAnimator rotate = ObjectAnimator.ofFloat(textview, "rotation", 0f, 360f);
ObjectAnimator fadeInOut = ObjectAnimator.ofFloat(textview, "alpha", 1f, 0f, 1f);
AnimatorSet animSet = new AnimatorSet();
animSet.play(rotate).with(fadeInOut).after(moveIn);
animSet.setDuration(5000);
animSet.start();
```

## 使用XML编写动画

通过XML来编写动画可能会比通过代码来编写动画要慢一些，但是在重用方面将会变得非常轻松，比如某个将通用的动画编写到XML里面，我们就可以在各个界面当中轻松去重用它。

- `<animator>`对应代码中的`ValueAnimator`
```xml
<animator xmlns:android="http://schemas.android.com/apk/res/android"
    android:valueFrom="0"
    android:valueTo="100"
    android:valueType="intType"/>
```
- `<objectAnimator>`对应代码中的`ObjectAnimator`
```xml
<objectAnimator xmlns:android="http://schemas.android.com/apk/res/android"
    android:valueFrom="1"
    android:valueTo="0"
    android:valueType="floatType"
    android:propertyName="alpha"/>
```
- `<set>`对应代码中的`AnimatorSet`
```xml
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:ordering="sequentially" >

    <objectAnimator
        android:duration="2000"
        android:propertyName="translationX"
        android:valueFrom="-500"
        android:valueTo="0"
        android:valueType="floatType" >
    </objectAnimator>

    <set android:ordering="together" >
        <objectAnimator
            android:duration="3000"
            android:propertyName="rotation"
            android:valueFrom="0"
            android:valueTo="360"
            android:valueType="floatType" >
        </objectAnimator>

        <set android:ordering="sequentially" >
            <objectAnimator
                android:duration="1500"
                android:propertyName="alpha"
                android:valueFrom="1"
                android:valueTo="0"
                android:valueType="floatType" >
            </objectAnimator>
            <objectAnimator
                android:duration="1500"
                android:propertyName="alpha"
                android:valueFrom="0"
                android:valueTo="1"
                android:valueType="floatType" >
            </objectAnimator>
        </set>
    </set>
</set>
```

调用如下代码来启动动画：
```java
Animator animator = AnimatorInflater.loadAnimator(context, R.animator.anim_file);
animator.setTarget(view);
animator.start();
```

## ViewPropertyAnimator的用法

```java
textview.animate().alpha(0f);
textview.animate().x(500).y(500);
textview.animate().x(500).y(500).setDuration(5000);
textview.animate().x(500).y(500).setDuration(5000)
		.setInterpolator(new BounceInterpolator());
```
