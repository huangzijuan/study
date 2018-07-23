## setXfremode遮罩
Canvas canvas = new Canvas(bitmap1);
paint.setXfermode(new PorterDuffXfermode(Mode.SRC_IN));
canvas.drawBitmap(mask, 0f, 0f, paint);

canvas原有的图片 可以理解为背景 就是dst
新画上去的图片 可以理解为前景 就是src

PorterDuff.Mode.CLEAR 清除画布上图像
PorterDuff.Mode.SRC 显示上层图像
PorterDuff.Mode.DST 显示下层图像
PorterDuff.Mode.SRC_OVER上下层图像都显示，上层居上显示
PorterDuff.Mode.DST_OVER 上下层都显示,下层居上显示
PorterDuff.Mode.SRC_IN 取两层图像交集部门,只显示上层图像
PorterDuff.Mode.DST_IN 取两层图像交集部门,只显示下层图像
PorterDuff.Mode.SRC_OUT 取上层图像非交集部门
PorterDuff.Mode.DST_OUT 取下层图像非交集部门
PorterDuff.Mode.SRC_ATOP 取下层图像非交集部门与上层图像交集部门
PorterDuff.Mode.DST_ATOP 取上层图像非交集部门与下层图像交集部门
PorterDuff.Mode.XOR 取两层图像的非交集部门
