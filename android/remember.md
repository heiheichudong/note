# android之好记性不如烂笔头

> icon 尺寸：

文件夹              |   尺寸
------              |:------:
mipmap-mdpi         |48x48
mipmap-hdpi         |72x72
mipmap-xhdpi        |96x96
mipmap-xxhdpi       |144x144
mipmap-xxxhdpi      |192x192

> Bitmap

```
public static int[] getImageWidthHeight(String path){
    BitmapFactory.Options options = new BitmapFactory.Options();

    /**
     * 最关键在此，把options.inJustDecodeBounds = true;
     * 这里再decodeFile()，返回的bitmap为空，但此时调用options.outHeight时，已经包含了图片的高了
     */
    options.inJustDecodeBounds = true;
    Bitmap bitmap = BitmapFactory.decodeFile(path, options); // 此时返回的bitmap为null
    /**
     *options.outHeight为原始图片的高
     */
    return new int[]{options.outWidth,options.outHeight};
}
```

addView()
在拖拽view1的时候，要重新对view1的布局参数进行设置，如下
```
RelativeLayout.LayoutParams layoutParams = (LayoutParams) view1.getLayoutParams();
  layoutParams.leftMargin = view1.getLeft();
  layoutParams.topMargin = view1.getTop();
  view1.setLayoutParams(layoutParams);
```

