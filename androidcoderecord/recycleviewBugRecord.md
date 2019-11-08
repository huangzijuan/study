## Bug及解决方式
1. notifyItemChange(position) position错位问题
使用holder.getAdapterPosition()

2. 禁止recycleview默认动画
DefaultItemAnimator defaultItemAnimator = ((DefaultItemAnimator) recyclerViewItem.getItemAnimator());
if (defaultItemAnimator != null) {
    defaultItemAnimator.setSupportsChangeAnimations(false);
}
