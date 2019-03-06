自定义view一般会涉及六个步骤：


1. 继承View或者ViewGroup
2. 复三个构造方法，构造方法一般用来解析自定义view的属性还有一些初始化工作
3. 复写onMeasure方法来测量，并确定自身的宽高
4. 复写onLayout方法来确定子类的布局位置
5. 复写onDraw方法来绘制内容
6. 复写onTouchEvent方法实现view的触摸效果



# 认识 MeasureSpec #
MeasureSpec类，它封装了父布局传递给子布局的布局要求，每个MeasureSpec代表了一组宽度和高度的要求  MeasureSpec由size和mode组成。
specMode一共有三种类型，如下所示： 
1. EXACTLY 
表示父视图希望子视图的大小应该是由specSize的值来决定的，系统默认会按照这个规则来设置子视图的大小，简单的说（当设置width或height为match_parent时，模式为EXACTLY，因为子view会占据剩余容器的空间，所以它大小是确定的） 
2. AT_MOST 
表示子视图最多只能是specSize中指定的大小。（当设置为wrap_content时，模式为AT_MOST, 表示子view的大小最多是多少，这样子view会根据这个上限来设置自己的尺寸）
3. UNSPECIFIED 
表示开发人员可以将视图按照自己的意愿设置成任意的大小，没有任何限制。这种情况比较少见，不太会用到。 


# onMeasure(int widthMeasureSpec, int heightMeasureSpec) #
这个方法有两个方法参数，是ViewGroup传递给子View的，子View可以根据这两个参数来得到父类建议的宽高
		常用方法

		//宽度Mode
        int specWidthMode = MeasureSpec.getMode(widthMeasureSpec);
        //父类建议的宽度
        int specWidthSize = MeasureSpec.getSize(widthMeasureSpec);

		//设置自身的宽高
		setMeasuredDimension(int measuredWidth, int measuredHeight)

		//ViewGroup的方法，自定义ViewGroup时,用于测量子View的宽高
		measureChildren(widthMeasureSpec,heightMeasureSpec);

# onDraw(Canvas) #