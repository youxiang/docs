Skeleton effect可以认为是一种加载指示器，目前的方案主要有：

- Shimmer

- Skeleton（Deprecated）

# Shimmer

Shimmer是Facebook对外发布的一个Android工具库，利用该库可以给任意的View添加Shimmer效果（Skeleton effect）。

<img src="http://facebook.github.io/shimmer-android/images/shimmer-small.gif" alt="img" style="zoom:50%;" />

## 如何使用

1. 在app的build.gradle文件里添加依赖

   ```groovy
   dependencies {
     implementation 'com.facebook.shimmer:shimmer:0.5.0'
   }
   ```



2. 使用ShimmerFrameLayout

   ```xml
   <com.facebook.shimmer.ShimmerFrameLayout
        android:id="@+id/shimmer_view_container"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
   >
        ...(your complex view here)...
   </com.facebook.shimmer.ShimmerFrameLayout>
   ```



## 参考链接

http://facebook.github.io/shimmer-android/ 

https://github.com/facebook/shimmer-android



# Skeleton

同样是一个Android库，提供了显示skeleton加载效果的方法。其本质也是基于Shimmer（非facebook版本）二次开发，适配了RecyclerView，可以很容易的对列表和方格类的页面处理skeleton效果。

<img src="https://github.com/ethanhua/Skeleton/raw/master/screenshots/01.gif" alt="img" style="zoom: 50%;" />

## 如何使用

1. 在app的build.gradle文件里添加依赖

   ```groovy
   dependencies {
          implementation 'com.ethanhua:skeleton:1.1.2'
          implementation 'io.supercharge:shimmerlayout:2.1.0'
       }
   ```

   

2. For RecyclerView

   ```java
   skeletonScreen = Skeleton.bind(recyclerView)
                                 .adapter(adapter)
                                 .load(R.layout.item_skeleton_news)
                                 .show();
   ```

   

3. For View

   ```java
   skeletonScreen = Skeleton.bind(rootView)
                                 .load(R.layout.layout_img_skeleton)
                                 .show();
   ```

   

4. More Config

   ```java
   .shimmer(true)      // whether show shimmer animation.                      default is true
   .count(10)          // the recycler view item count.                        default is 10
   .color(color)       // the shimmer color.                                   default is #a2878787
   .angle(20)          // the shimmer angle.                                   default is 20;
   .duration(1000)     // the shimmer animation duration.                      default is 1000;
   .frozen(false)      // whether frozen recyclerView during skeleton showing  default is true; 
   ```

   

5. when data return you can call the method to hide skeleton loading view

   ```java
   skeletonScreen.hide()
   ```

   

## 参考链接

https://github.com/ethanhua/Skeleton

https://github.com/team-supercharge/ShimmerLayout

# Shimmer VS Skeleton

|                 | Shimmer                                                      | Skeleton                                                     |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 包大小          | 小                                                           | 小，比Shimmer稍大                                            |
| 原理            | 在View上面添加一个ShimmerDrawable；<br />需要显示shimmer效果时通过属性动画刷新并绘制该drawable；<br />需要显示内容时停止属性动画 | 基本原理与Shimmer类似，基于Shimmer功能增加了对RecyclerView的支持 |
| 使用难度        | 简单                                                         | 简单                                                         |
| 实现方案&工作量 | 增加额外的shimmer layout；<br />处理动画的开始和停止；<br />处理列表界面需要固定编写相应的shimmer layout | 同理，在列表界面的处理上可能更符合编码规范                   |
| 最新版本        | 0.5.0                                                        | 1.1.2，但项目处于Deprecated状态                              |

由于原理相同，可考虑使用简单的Shimmer作为skeleton effect的方案