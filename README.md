SwipeBackLayout
===
本库Fork自[SwipeBackLayout](https://github.com/ikew0ng/SwipeBackLayout),主要增加了两个功能：
 1. 全局滑动的支持，参照[博客](http://blog.csdn.net/u013003052/article/details/50448617)中的提示，但实现更加简洁，但是在选择All时无法全局滑动。
 2. 实现从顶部下拉滑动功能。参照[UltimateSwipeTool](https://github.com/CameloeAnthony/UltimateSwipeTool)中的`SwipeBackLayout`，适当做了修改，确保效果和功能正常。

实现下拉滑动功能时最大的难点是在释放的时候：
```
...
@Override
public void onViewReleased(View releasedChild, float xvel, float yvel) {
		final int childWidth = releasedChild.getWidth();
		final int childHeight = releasedChild.getHeight();

		int left = 0, top = 0;
		if ((mTrackingEdge & EDGE_LEFT) != 0) {
				left = xvel > 0 || xvel == 0 && mScrollPercent > mScrollThreshold ? childWidth
								+ mShadowLeft.getIntrinsicWidth() + OVERSCROLL_DISTANCE : 0;
		} else if ((mTrackingEdge & EDGE_RIGHT) != 0) {
				left = xvel < 0 || xvel == 0 && mScrollPercent > mScrollThreshold ? -(childWidth
								+ mShadowLeft.getIntrinsicWidth() + OVERSCROLL_DISTANCE) : 0;
		} else if ((mTrackingEdge & EDGE_TOP) != 0) {
				top = yvel > 0 || yvel == 0 && mScrollPercent > mScrollThreshold ? (childHeight
								+ mShadowTop.getIntrinsicHeight() + OVERSCROLL_DISTANCE) : 0;
		} else if ((mTrackingEdge & EDGE_BOTTOM) != 0) {
				top = yvel < 0 || yvel == 0 && mScrollPercent > mScrollThreshold ? -(childHeight
								+ mShadowBottom.getIntrinsicHeight() + OVERSCROLL_DISTANCE) : 0;
		}

		mDragHelper.settleCapturedViewAt(left, top);
		invalidate();
}
...
```

对于新功能的使用：
```
mSwipeBackLayout.setEnableAllEdge(true);
```
即可实现全局滑动手势。

新增的`EDGE_TOP`与其他的功能相似，使用相同的api`setEdgeTrackingEnabled`即可。

其他介绍参见原库[README](https://github.com/ikew0ng/SwipeBackLayout/blob/master/README.md)
