if (fragments.size() > 1) { //多于1，才会循环跳转
    if (mIndex < 1) { //首位之前，跳转到末尾（N）
        mIndex = 3;
        mViewPager.setCurrentItem(mIndex,false);
    } else if (mIndex > 3) { //末位之后，跳转到首位（1）
        mViewPager.setCurrentItem(1,false); //false:不显示跳转过程的动画
        mIndex = 1;
    }
}
