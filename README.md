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

要将时间显示，首先要在PROJECTION中定义显示的时间，原应用有两种时间，我选择修改时间作为显示的时间<br>
```java
 private static final String[] PROJECTION = new String[] {
            NotePad.Notes._ID, // 0
            NotePad.Notes.COLUMN_NAME_TITLE, // 1
            //扩展 显示时间 颜色
            NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE,
            NotePad.Notes.COLUMN_NAME_BACK_COLOR, 
    };
```

### 笔记查询（按标题查询）<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/search1.PNG)<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/search2.PNG)<br>

添加笔记查询功能，就要在应用中增加一个搜索的入口。找到菜单的xml文件，list_options_menu.xml，添加一个搜索的item<br>

```xml
<item
    android:id="@+id/menu_search"
    android:title="@string/menu_search"
    android:icon="@android:drawable/ic_search_category_default"
    android:showAsAction="always">
</item>
```
在NotesList中找到onOptionsItemSelected方法，在switch中添加搜索的case语句:<br>
```java
//添加搜素
    case R.id.menu_search:
    Intent intent = new Intent();
    intent.setClass(NotesList.this,NoteSearch.class);
    NotesList.this.startActivity(intent);
    return true;
```
在安卓中有个用于搜索控件：SearchView，可以把SearchView跟ListView相结合，动态地显示搜索结果。先布局搜索页面，在layout中新建布局文件note_search_list.xml：<br>
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
    <SearchView
        android:id="@+id/search_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:iconifiedByDefault="false"
        android:queryHint="输入搜索内容..."
        android:layout_alignParentTop="true">
    </SearchView>
    <ListView
        android:id="@android:id/list"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
    </ListView>
</LinearLayout>
```

### 背景更换<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/background1.PNG)<br>
![](https://github.com/BornTW/android-NotePad/blob/master/Images/background2.PNG)<br>
背景更换指的是编辑笔记时的背景色更换。编辑笔记的Activity为NoteEditor。同样的，在PROJECTION中添加颜色项：<br>
```java

  private static final String[] PROJECTION =
        new String[] {
            NotePad.Notes._ID,
            NotePad.Notes.COLUMN_NAME_TITLE,
            NotePad.Notes.COLUMN_NAME_NOTE,
            NotePad.Notes.COLUMN_NAME_BACK_COLOR
    };
 ```
 从数据库读取颜色并设置编辑界面背景色操作放入其中，好处除了从笔记列表点进来时可以被执行到，跳到改变颜色Activity回来时也会被执行到。<br>
 ```java
 //读取颜色数据
int x = mCursor.getInt(mCursor.getColumnIndex(NotePad.Notes.COLUMN_NAME_BACK_COLOR));
    /**
    * 白 255 255 255
    * 黄 247 216 133
    * 蓝 165 202 237
    * 绿 161 214 174
    * 红 244 149 133
    */
    switch (x){
        case NotePad.Notes.DEFAULT_COLOR:
            mText.setBackgroundColor(Color.rgb(255, 255, 255));
            break;
        case NotePad.Notes.YELLOW_COLOR:
            mText.setBackgroundColor(Color.rgb(247, 216, 133));
            break;
        case NotePad.Notes.BLUE_COLOR:
            mText.setBackgroundColor(Color.rgb(165, 202, 237));
            break;
        case NotePad.Notes.GREEN_COLOR:
            mText.setBackgroundColor(Color.rgb(161, 214, 174));
            break;
        case NotePad.Notes.RED_COLOR:
            mText.setBackgroundColor(Color.rgb(244, 149, 133));
            break;
        default:
            mText.setBackgroundColor(Color.rgb(255, 255, 255));
            break;
    }
 ```

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
