[TOC]



# NotePad 扩展应用

NotePad 扩展应用是基于原始 Android NotePad 应用的改进版本，增加了多项新功能和用户界面的改进，以提升用户体验和应用的实用性。

## 安装

本应用需要 Android SDK 版本 21 或更高。要构建和运行应用，请遵循以下步骤：

1. 克隆仓库到本地：
   ```
   git clone https://github.com/your-repository/NotePad_new-master.git
   ```
2. 使用 Android Studio 打开项目文件夹。
3. 构建项目并运行在模拟器或实际设备上。

## 功能描述

### 基本功能

- **显示时间戳**：在 NoteList 界面中，每个笔记条目现在都会显示最后修改的时间戳。
   ```xml
   <!-- note_list_item.xml -->
   <TextView
       android:id="@+id/timestamp"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:textAppearance="?android:attr/textAppearanceSmall"
       android:textColor="#999"/>
   ```
- **笔记查询功能**：用户可以根据笔记的标题或内容进行搜索，快速找到相关笔记。
   ```java
   // NoteList.java
   public void searchNotes(String query) {
       Cursor noteSearch = getContentResolver().query(
           Notes.CONTENT_URI,
           new String[] { Notes.COLUMN_NAME_TITLE, Notes.COLUMN_NAME_NOTE },
           Notes.COLUMN_NAME_TITLE + " LIKE '%" + query + "%' OR " +
           Notes.COLUMN_NAME_NOTE + " LIKE '%" + query + "%'",
           null,
           null);
       adapter.changeCursor(noteSearch);
   }
   ```

### 扩展功能

- **UI 美化**：更新了笔记列表和编辑界面的 UI，使其更现代化，提供更好的用户体验。
   ```xml
   <!-- note_list_item.xml -->
   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:textSize="18sp"
       android:textColor="#333"
       android:padding="16dp"/>
   ```
- **笔记分类**：用户可以根据不同的类别对笔记进行分类，方便管理和查找。
   ```java
   // NoteList.java
   public void categorizeNote(int categoryId) {
       ContentValues values = new ContentValues();
       values.put(Notes.COLUMN_NAME_CATEGORY_ID, categoryId);
       getContentResolver().update(Notes.CONTENT_URI, values, null, null);
   }
   ```
- **更换背景**：用户可以自定义笔记编辑界面的背景，增加个性化体验。
   ```xml
   <!-- note_editor.xml -->
   <RelativeLayout
       android:background="@drawable/custom_background">
       ...
   </RelativeLayout>
   ```
- **笔记排序**：支持按照时间、标题等多种方式对笔记进行排序。
   ```java
   // NoteList.java
   public void sortNotes(String sortBy) {
       Cursor sortedNotes = getContentResolver().query(
           Notes.CONTENT_URI,
           new String[] { Notes.COLUMN_NAME_TITLE, Notes.COLUMN_NAME_MODIFICATION_DATE },
           null,
           null,
           sortBy);
       adapter.changeCursor(sortedNotes);
   }
   ```
- **笔记预览**：在笔记列表界面，用户可以快速预览笔记的部分内容。
   ```xml
   <!-- note_list_item.xml -->
   <TextView
       android:id="@+id/preview"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:textAppearance="?android:attr/textAppearanceSmall"
       android:textColor="#666"
       android:maxLines="2"/>
   ```

## 技术实现

## 页面截图

以下是应用的几个主要界面的截图，展示了新增功能的实际效果：

### 显示时间戳

在 `note_list_item.xml` 布局文件中，为每个笔记条目添加了一个新的 TextView 用于显示时间戳。

![Screenshot 2024-12-02 010726.png](Screenshot%202024-12-02%20010726.png)

### 笔记查询功能

在 `NoteList.java` 中添加了搜索框和相应的查询逻辑，使用 SQL LIKE 语句匹配标题或内容。

![Screenshot 2024-12-01 234033.png](Screenshot%202024-12-01%20234033.png)

### UI 美化

对 `note_list_item.xml` 和 `note_editor.xml` 布局文件进行了修改，包括字体大小、颜色和边距的调整。

![Screenshot 2024-12-02 170040.png](Screenshot%202024-12-02%20170040.png)

### 笔记排序

在 `NoteList.java` 中实现了排序功能，用户可以通过界面上的选项来选择排序方式。

![Screenshot 2024-12-02 170045.png](Screenshot%202024-12-02%20170045.png)
![Screenshot 2024-12-02 170049.png](Screenshot%202024-12-02%20170049.png)

### 更换背景

允许用户从预设的背景图库中选择或上传自定义图片作为编辑界面背景。

![Screenshot 2024-12-02 170109.png](Screenshot%202024-12-02%20170109.png)
![Screenshot 2024-12-02 170116.png](Screenshot%202024-12-02%20170116.png)
![Screenshot 2024-12-02 170134.png](Screenshot%202024-12-02%20170134.png)
![Screenshot 2024-12-02 170217.png](Screenshot%202024-12-02%20170217.png)

### 笔记分类
在数据库模型中添加了分类字段，并在 UI 中提供了分类选项。

![Screenshot 2024-12-02 172849.png](Screenshot%202024-12-02%20172849.png)

### 笔记预览
修改了笔记列表的 UI，使每个条目可以显示更多的内容预览。

![Screenshot 2024-12-02 172857.png](Screenshot%202024-12-02%20172857.png)
![Screenshot 2024-12-02 172916.png](Screenshot%202024-12-02%20172916.png)

