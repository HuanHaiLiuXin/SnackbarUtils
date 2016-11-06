# SnackbarUtils
Snackbar工具类

        功能:
            1:设置Snackbar显示时间长短
                1.1:Snackbar.LENGTH_SHORT       {@link SnackbarUtils#Short(View, String)}
                1.2:Snackbar.LENGTH_LONG        {@link SnackbarUtils#Long(View, String)}
                1.3:Snackbar.LENGTH_INDEFINITE  {@link SnackbarUtils#Indefinite(View, String)}
                1.4:CUSTOM                      {@link SnackbarUtils#Custom(View, String, int)}
            2:设置Snackbar背景颜色
                2.1:color_info      {@link SnackbarUtils#info()}
                2.2:color_confirm   {@link SnackbarUtils#confirm()}
                2.3:color_warning   {@link SnackbarUtils#warning()}
                2.4:color_danger    {@link SnackbarUtils#danger()}
                2.5:CUSTOM          {@link SnackbarUtils#backColor(int)}
            3:设置TextView(@+id/snackbar_text)的文字颜色
                {@link SnackbarUtils#messageColor(int)}
            4:设置Button(@+id/snackbar_action)的文字颜色
                {@link SnackbarUtils#actionColor(int)}
            5:设置Snackbar背景的透明度
                {@link SnackbarUtils#alpha(float)}
            6:设置Snackbar显示的位置
                {@link SnackbarUtils#gravityFrameLayout(int)}
                {@link SnackbarUtils#gravityCoordinatorLayout(int)}
                6.1:Gravity.TOP;
                6.2:Gravity.BOTTOM;
                6.3:Gravity.CENTER;
            7:设置Button(@+id/snackbar_action)文字内容 及 点击监听
                {@link SnackbarUtils#setAction(int, View.OnClickListener)}
                {@link SnackbarUtils#setAction(CharSequence, View.OnClickListener)}
            8:设置Snackbar展示完成 及 隐藏完成 的监听
                {@link SnackbarUtils#setCallback(Snackbar.Callback)}
            9:设置TextView(@+id/snackbar_text)左右两侧的图片
                {@link SnackbarUtils#leftAndRightDrawable(Drawable, Drawable)}
                {@link SnackbarUtils#leftAndRightDrawable(Integer, Integer)}
            10:设置TextView(@+id/snackbar_text)中文字的对齐方式
                默认效果就是居左对齐
                {@link SnackbarUtils#messageCenter()}   居中对齐
                {@link SnackbarUtils#messageRight()}    居右对齐
                注意:这两个方法要求SDK>=17.{@link View#setTextAlignment(int)}
                    本来想直接设置Gravity,经试验发现在 TextView(@+id/snackbar_text)上,design_layout_snackbar_include.xml
                    已经设置了android:textAlignment="viewStart",单纯设置Gravity是无效的.
                    TEXT_ALIGNMENT_GRAVITY:{@link View#TEXT_ALIGNMENT_GRAVITY}
            11:向Snackbar布局中添加View(Google不建议,复杂的布局应该使用DialogFragment进行展示)
                {@link SnackbarUtils#addView(int, int)}
                {@link SnackbarUtils#addView(View, int)}
                注意:使用addView方法的时候要注意新加布局的大小和Snackbar内文字长度，Snackbar过大或过于花哨了可不好看
            12:设置Snackbar布局的外边距
                {@link SnackbarUtils#margins(int)}
                {@link SnackbarUtils#margins(int, int, int, int)}
                注意:经试验发现,调用margins后再调用 gravityFrameLayout,则margins无效.
                    为保证margins有效,应该先调用 gravityFrameLayout,在 show() 之前调用 margins
                    SnackbarUtils.Long(bt9,"设置Margin值").backColor(0XFF330066).gravityFrameLayout(Gravity.TOP).margins(20,40,60,80).show();
            13:设置Snackbar布局的圆角半径值
                {@link SnackbarUtils#radius(float)}
            14:设置Snackbar布局的圆角半径值及边框颜色及边框宽度
                {@link SnackbarUtils#radius(int, int, int)}
            15:设置Snackbar显示在指定View的上方
                {@link SnackbarUtils#above(View, int, int, int)}
                注意:
                    1:此方法实际上是 {@link SnackbarUtils#gravityFrameLayout(int)}和{@link SnackbarUtils#margins(int, int, int, int)}的结合.
                        不可与 {@link SnackbarUtils#margins(int, int, int, int)} 混用.
                    2:暂时仅仅支持单行Snackbar,因为方法中涉及的{@link SnackbarUtils#calculateSnackBarHeight()}暂时仅支持单行Snackbar高度计算.
            16:设置Snackbar显示在指定View的下方
                {@link SnackbarUtils#bellow(View, int, int, int)}
                注意:同15
        参考:
            //写的很好的Snackbar源码分析
            http://blog.csdn.net/wuyuxing24/article/details/51220415
            //借鉴了作者部分写法,自定义显示时间 及 向Snackbar中添加View
            http://www.jianshu.com/p/cd1e80e64311
            //借鉴了作者部分写法,4种类型的背景色 及 方法调用的便捷性
            http://www.jianshu.com/p/e3c82b98f151
            //大神'工匠若水'的文章'Android应用坐标系统全面详解',用于计算Snackbar显示的精确位置
            http://blog.csdn.net/yanbober/article/details/50419117
        示例:
            在Activity中:
            int total = 0;
            int[] locations = new int[2];
            getWindow().findViewById(android.R.id.content).getLocationInWindow(locations);
            total = locations[1];
            SnackbarUtils.Custom(bt_multimethods,"10s+左右drawable+背景色+圆角带边框+指定View下方",1000*10)
                .leftAndRightDrawable(R.mipmap.i10,R.mipmap.i11)
                .backColor(0XFF668899)
                .radius(16,1,Color.BLUE)
                .bellow(bt_margins,total,16,16)
                .show();
