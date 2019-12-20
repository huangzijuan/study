## 步骤
1. 通过GlobalKey找到对应元素的BuildContext对象
2. 通过BuildContext对象的size属性获取大小，Sliver系列的Widget除外(Sliver系列Widget必须使用内部容器间接获取控件大小)
3. 通过findRender方法获取到渲染对象，然后使用paintBounds获取大小

```
RenderObject renderObject = _myKey.currentContext.findRenderObject();
print("semanticBounds:${renderObject.semanticBounds.size} paintBounds:${renderObject.paintBounds.size} size:${_myKey.currentContext.size}");

```

## 获取控件大小和位置
```
showSizes() {
    RenderBox renderBoxRed = fileListKey.currentContext.findRenderObject();
    print(renderBoxRed.size);
  }

showPositions() {
    RenderBox renderBoxRed = fileListKey.currentContext.findRenderObject();
    print(renderBoxRed.localToGlobal(Offset.zero));
  }
```
