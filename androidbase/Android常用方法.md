## 一、 View提供的获取坐标的方法
getTop()获取到的是view自身的顶边到其父布局顶边的距离
getLeft()获取到的是view自身的左边到其父布局左边的距离
getRight()获取到的是view自身的右边到父布局右边的距离
getBottom()获取到的是view自身底边到其父布局地边的距离

## 二、MotionEvent提供的获取坐标的方法
getX()获取点击事件距离控件左边的距离，即试图坐标
getY()获取点击事件距离控件顶边的距离，即试图坐标
getRawX()获取点击事件距离整个屏幕左边的距离，即绝对坐标
getRawY()获取点击事件距离整个屏幕顶边的距离，即绝对坐标
