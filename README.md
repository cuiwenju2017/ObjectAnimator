## Android自带属性动画之ObjectAnimator

详情：[https://blog.csdn.net/juer2017/article/details/116061736?spm=1001.2014.3001.5501](https://blog.csdn.net/juer2017/article/details/116061736?spm=1001.2014.3001.5501)

```
btn_ObjectAnimator.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        /**属性动画ObjectAnimator
         * • translationX和translationY：用来沿着X轴或者Y轴进行平移。
         * • rotation、rotationX、rotationY：用来围绕View的支点进行旋转。
         * • scaleX、scaleY:横向拉伸和纵向拉伸
         * • alpha：透明度，默认是1（不透明），0代表完全透明。
         * • x和y：描述View对象在其容器中的最终位置。
         */
        objectAnimator = ObjectAnimator.ofFloat(iv, "alpha", 0f, 1f).setDuration(1000);
        objectAnimator.addListener(new AnimatorListenerAdapter() {
            @Override
            public void onAnimationEnd(Animator animation) {
                super.onAnimationEnd(animation);
                ObjectAnimator.ofFloat(iv, "translationX", 0f, 500f, -500f, 0f).setDuration(3000).start();
            }
        });
        objectAnimator.start();
    }
});

btn_AnimatorSet.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        /**组合动画AnimatorSet
         * • after（Animator anim）：将现有动画插入到传入的动画之后执行。
         * • after（long delay）：将现有动画延迟指定毫秒后执行。
         * • before（Animator anim）：将现有动画插入到传入的动画之前执行。
         * • with（Animator anim）：将现有动画和传入的动画同时执行。
         */
        ObjectAnimator animator1 = ObjectAnimator.ofFloat(iv, "alpha", 0f, 1f).setDuration(3000);
        ObjectAnimator animator2 = ObjectAnimator.ofFloat(iv, "rotation", 0f, 720f).setDuration(3000);
        ObjectAnimator animator3 = ObjectAnimator.ofFloat(iv, "translationX", -500f, 0f).setDuration(3000);
        AnimatorSet set = new AnimatorSet();
        set.play(animator1).with(animator2).with(animator3);
        set.start();
    }
});

btn_PropertyValuesHolder.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        /**组合动画PropertyValuesHolder
         *使用PropertyValuesHolder类只能是多个动画一起执行
         */
        PropertyValuesHolder valuesHolder1 = PropertyValuesHolder.ofFloat("scaleX", 1.0f, 2.0f, 1.0f);
        PropertyValuesHolder valuesHolder2 = PropertyValuesHolder.ofFloat("rotationX", 0.0f, 360.0f);
        PropertyValuesHolder valuesHolder3 = PropertyValuesHolder.ofFloat("alpha", 1.0f, 0.3f, 1.0f);
        PropertyValuesHolder valuesHolder4 = PropertyValuesHolder.ofFloat("scaleY", 1.0f, 2.0f, 1.0f);
        objectAnimator = ObjectAnimator.ofPropertyValuesHolder(iv, valuesHolder1, valuesHolder2, valuesHolder3, valuesHolder4);
        objectAnimator.setDuration(3000).start();
    }
});
```