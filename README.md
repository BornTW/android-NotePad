# 基于NotePad应用的功能扩展

## 基本功能
### NotesList中显示条目增时间戳显示<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/time.PNG)<br>
找到列表中item的布局：noteslist_item.xml，在这个布局文件中，能看到一个TextView，在标题的TextView下再加一个时间的TextView
```xml
<?xml version="1.0" encoding="utf-8"?>
<!--添加一个垂直的线性布局-->
<LinearLayout  xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <!--原标题TextView-->
    <TextView xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@android:id/text1"
        android:layout_width="match_parent"
        android:layout_height="?android:attr/listPreferredItemHeight"
        android:textAppearance="?android:attr/textAppearanceLarge"
        android:gravity="center_vertical"
        android:paddingLeft="5dip"
        android:textColor="@color/colorBlack"
        android:singleLine="true"
        />
    <!--添加显示时间的TextView-->
    <TextView
        android:id="@+id/text1_time"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textAppearance="?android:attr/textAppearanceSmall"
        android:paddingLeft="5dip"
        android:textColor="@color/colorBlack"/>
</LinearLayout>
```
<br>


### 笔记查询（按标题查询）<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/search1.PNG)<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/search2.PNG)<br>



### 背景更换<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/background1.PNG)<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/background2.PNG)<br>

### 笔记排序(按创建时间)<br>
### 排序前<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/timesort-before.PNG)<br>
### 排序后(由高到低)<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/time-after.PNG)<br>


### 笔记排序(按颜色排序)<br>
### 排序前<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/timesort.PNG)<br>
### 排序后<br>

![](https://github.com/BornTW/android-NotePad/blob/master/Images/timesort-before.PNG)<br>
