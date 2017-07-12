# 动画框架的使用

* [引用](#引用)
* [使用](#使用)
* [动画](#动画)
* [参考地址](#参考地址)


## 引用
```
dependencies {
    compile 'com.android.support:support-compat:25.1.1'
    compile 'com.daimajia.easing:library:2.0@aar'
    compile 'com.daimajia.androidanimations:library:2.2@aar'
}
```

## 使用
```
public class MainActivity extends AppCompatActivity {
    private View viewAnimate;
    private ListView mListView;
    private AnimateAdapter mAdapter;

    private YoYo.YoYoString rope;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        viewAnimate = findViewById(R.id.tv_animate);
        mListView = (ListView) findViewById(R.id.list_view);
        mAdapter = new AnimateAdapter(this);
        mListView.setAdapter(mAdapter);
        viewAnimate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (rope != null) {
                    rope.stop(true);
                }
            }
        });
        mListView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                if (rope != null) {
                    rope.stop(true);
                }
                Techniques technique = (Techniques) view.getTag();
                rope = YoYo.with(technique)
                        .duration(1200)
                        .repeat(YoYo.INFINITE)
                        .pivot(YoYo.CENTER_PIVOT, YoYo.CENTER_PIVOT)
                        .interpolate(new AccelerateDecelerateInterpolator())
                        .withListener(new Animator.AnimatorListener() {
                            @Override
                            public void onAnimationStart(Animator animation) {

                            }

                            @Override
                            public void onAnimationEnd(Animator animation) {
                            }

                            @Override
                            public void onAnimationCancel(Animator animation) {
                            }

                            @Override
                            public void onAnimationRepeat(Animator animation) {

                            }
                        })
                        .playOn(viewAnimate);
            }
        });
    }
    @Override
    public void onWindowFocusChanged(boolean hasFocus) {
        if (hasFocus) {
            rope = YoYo.with(Techniques.FadeIn).duration(1000).playOn(viewAnimate);// after start,just click mTarget view, rope is not init
        }
    }
}
```


## 动画
* Attention 

    Flash, Pulse, RubberBand, Shake, Swing, Wobble, Bounce, Tada, StandUp, Wave
    
* Special

    Hinge, RollIn, RollOut,Landing,TakingOff,DropOut
    
* Bounce

    BounceIn, BounceInDown, BounceInLeft, BounceInRight, BounceInUp
    
* Fade

    FadeIn, FadeInUp, FadeInDown, FadeInLeft, FadeInRight  
    FadeOut, FadeOutDown, FadeOutLeft, FadeOutRight, FadeOutUp
    
* Flip

    FlipInX, FlipOutX, FlipOutY
    
* Rotate

    RotateIn, RotateInDownLeft, RotateInDownRight, RotateInUpLeft, RotateInUpRight  
    RotateOut, RotateOutDownLeft, RotateOutDownRight, RotateOutUpLeft, RotateOutUpRight
    
* Slide

    SlideInLeft, SlideInRight, SlideInUp, SlideInDown  
    SlideOutLeft, SlideOutRight, SlideOutUp, SlideOutDown
    
* Zoom

    ZoomIn, ZoomInDown, ZoomInLeft, ZoomInRight, ZoomInUp  
    ZoomOut, ZoomOutDown, ZoomOutLeft, ZoomOutRight, ZoomOutUp


## 参考地址

[https://github.com/daimajia/AndroidViewAnimations](https://github.com/daimajia/AndroidViewAnimations "参考地址")