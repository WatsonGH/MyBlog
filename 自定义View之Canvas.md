## 自定义View的三个构造函数 ##

## Canvas ##
**平移坐标系**
```
Canvas.translate(float dx, float dy) //相对于当前的坐标系，平移到指定原点坐标系，其中参数dx和dy为平移后的原点坐标

//举例：把坐标系平移到容器中间，然后平移回默认左上角位置
canvas.traslate(getWidth()/2,getHeight()/2);//平移到容器中间位置
canvas.traslate(-getWidth()/2,-getHeight()/2);//平移回默认的左上角位置
```

**旋转坐标系**
```
Canvas.rotate(float degrees) //degree>0?顺时针旋转坐标系：逆时针旋转坐标系；注意：旋转的是坐标系
```


**save画布和restore画布**
[https://blog.csdn.net/tiankongcheng6/article/details/83000247](https://blog.csdn.net/tiankongcheng6/article/details/83000247 "save方法和restore方法的理解")
```
Canvas.save() //保存画布save之前的状态
Canvas.restore()//恢复save之前的状态

//举例
//save之前先平移坐标系原点到容器中间
canvas.translate(getWidth()/2.0f,getHeight()/2.0f);
canvas.drawLine(0,0,100,100,paint);

//保存
canvas.save();
//把坐标系原点平移回容器左上角
canvas.translate(-getWidth()/2.0f,-getHeight()/2.0f);
paint.setColor(Color.RED);
canvas.drawLine(0,0,100,100,paint);

//恢复保存前的画布状态(坐标系的状态)，此时的坐标系原点在中间
canvas.restore();
paint.setColor(Color.GREEN);
//继续画一条直线，因为调用了restore恢复所以会在容器中间画一条长为100的垂直方向的直线
canvas.drawLine(0,0,0,100,paint);

```

## invalidate刷新绘制 ##
```
View.invalidate() //在UI主线程中使用，invalidate()本质是调用View的onDraw()绘制。
View.postInvalidate()//在子线程中使用（当然也可以在UI线程中调用），其内部也是通过Handler转换线程调用invalidate()，从重绘速率讲，invalidate()效率高。
```

## 画文字信息 ##
**canvas.drawText(String text,float x,float y,Paint mPaint)**


> 其中主要关心x和y这两个参数，x代表着开始绘制文字的水平位置，而y这代表着文字的baseline(基准线)
> 测量文字宽高的方法：
> **1.Paint.measureText测量宽度**
```
Paint paint = new Paint();
paint.setTextSize(size);
float strWidth = paint.measureText(str);
```
>**2.Paint.getTextBounds测量文字宽高**
```
Paint paint = new Paint();
Rect rect = new Rect();  
paint.getTextBounds(str, 0, str.length(), rect);  
int w = rect.width();  
int h = rect.height();
```
>**3.Paint.getFontMetrics获取精确高度**
```
Paint mPaint = new Paint();
mPaint.setTextSize(50);
Paint.FontMetrics fontMetrics = mPaint.getFontMetrics();
float ascent = fontMetrics.ascent;
float bottom = fontMetrics.bottom;
float descent = fontMetrics.descent;
float leading = fontMetrics.leading;
float top = fontMetrics.top;
//高度计算，从下图可知，height1计算的更精确，height2会有多余的空白，看产品需求决定
float height1 = fontMetrics.descent - fontMetrics.ascent;
float height2 = fontMetrics.bottom - fontMetrics.top;
```
>![](https://i.imgur.com/THWA3qO.png)
>**上述这些参数大小与具体是什么文字无关，只与字体大小和字体格式有关。并且，在Baseline上方的尺寸为负，下方为正。也就是top、ascent都是负数，bottom和descent为正数。在绘制文字时第三个参数y指定的就是文字baseLine的位置（也可以理解为指定所有字符里面最小字符的底部位置），举例：把文字显示到容器的中间位置**
```
baseLine(即y参数): getHeight()/2+(height1/2-descent)
```
>关于绘制文字的博客：https://hencoder.com/ui-1-3/