# vim使用

## 插入模式

+ ctrl+h 删除单词 ctrl+w删除单词  ctrl+u删除行
+ ctrl+c代替esc（可能会中断某些插件）使用ctrl+[

## normal模式

+ gi:快速跳转最后一次编辑的地方
+ 跳转
  - w/W移到下一个word/WORD开头，e/E移到下一个word/WORD结尾
  - b/B回到上一个word/WORD开头（word指的是以非空白符号分割的单词，WORD是以空白符分割的单词）
+ 行间搜索移动（同一行快速移动的方式其实是搜索一个字符并且移动到该字符）
  + 使用f{char} 可以移动到char字符上，t移动到char的前一个字符
  + 如果没搜到，可以使用分号（;）/逗号(,)继续搜索行下一个/上一个
  + 大写的F反过来搜索前面的字符
+ 水平移动（快速移动到一行的行首或行位）
  + 0移动到行首第一个字符，^移动到第一个非白字符
  + $移动到行尾，g_移动到行尾非空白字符j
+ 页面移动
  + gg/G 页首/页尾，ctrl+o 快速返回
  + H/M/L跳转到屏幕开头Header，中间Middle，结尾Lower
+ 快速删除
  + d删除行，x删除字符
  + daw（d around word）删除一个单词
  + 删除一个字符
+ 快速修改
  + r(replace), c(change),s(subtitute)
  + r替换单字符，s删除字符并插入，
  + c配合文本对象，进行快速修改。cw ct‘等等
+ 查询
  + / 或者 ？ 进行向前或者反向的搜索
  + n/N跳转下一个或上一个搜索
  + */#进行当前单词的向前匹配和向后匹配
+ 搜索替换
  + Substitute命令允许我们查找并且替换掉文本，并且支持正则
  + :[range]s[ubtitute]/{pattern}/{string}/[flag]
  + Range表示范围 比如:10,20 表示10-20行，%表示全部
  + pattern是要替换的模式，string是替换后的文本
  + Flag替换的标志 
    + g(gloabal)表示全局范围执行
    + c(confirm)表示确认，可以确认或者拒绝修改
    + n(number)报告比配到的次数而不替换，可以用来查看匹配次数
+ Buffer切换
  + :ls列举所有当前缓冲区  :b n跳转到第n个缓冲区
  + :bpre :bnext :bfirst :blast
  + 或者:b buffer_name 加上tab补全跳转
+ 窗口可视化分割
  + <ctrl+w>s水平分割 <ctrl+w>v垂直分割，或者:sp/:vs
  + <ctrl+w>hjkl进行跳转