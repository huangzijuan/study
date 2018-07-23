1. ../../src/main/java/com/android/inputmethod/latin/ad/ADPanelController.java:110: Do not place Android context classes in static fields (static reference to OrionNativeAd which has field Q pointing to View); this is a memory leak (and also breaks Instant Run)

2. ../../src/main/java/panda/keyboard/emoji/commercial/lottery/ui/widget/LotteryStepView.java:468: Avoid object allocations during draw/layout operations (preallocate and reuse instead)

3. 用SparseArray代替Map，Map中的containsKey方法如何处理

4. Node can be replaced by a TextView with compound drawables 有些会改变点击范围

5. ../../src/main/java/com/android/inputmethod/latin/settings/feedback/FeedbackLayout.java:433: This Handler class should be static or leaks might occur (anonymous android.os.Handler) onDestroy中有removeMsg


Drawable drawable = this.getResources().getDrawable(R.drawable.icon_news_fullarticle_arrows).mutate();
drawable.setColorFilter(new GLPorterDuffColorFilter(mTheme.titleColor, PorterDuff.Mode.SRC_IN));
mBottomADText.setCompoundDrawables(null, null, drawable, null);


android:drawablePadding="4.67dp"

http://api.c.avazunativeads.com/anative/nativeads?rinfo=OTcxMzQ2Qbgraxm81Gkes%2F9shEkBK%2Bi4tgMly2dBuTYmj8Rwy3ONumPrTkIPxFDGXh%2Bo6zDc&slotstyle=3&market=google&deviceid=863863038894264&sdkversion=3.0.1.012616&pkg=com.cmcm.keyboard.themeapk&ua=Mozilla%2F5.0+%28Linux%3B+Android+6.0.1%3B+M2+E+Build%2FMMB29U%3B+wv%29+AppleWebKit%2F537.36+%28KHTML%2C+like+Gecko%29+Version%2F4.0+Chrome%2F44.0.2403.144+Mobile+Safari%2F537.36&os=android&language=zh-CN&reqId=938c308f-ecae-4688-9a6d-2cf27305d169&maid=a9c92e3a13c079ee&gpid=f9490f15-d5e1-4c1b-acfc-6381e69b0023

http:\/\/cdn.avazutracking.net\/images\/201806\/110\/8cb595ef2b9c97eb8bbdd2070342d006_1200x627.png
