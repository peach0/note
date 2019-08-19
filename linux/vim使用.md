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

- vim宏
  - 宏的使用分为录制和回放
  - 使用q来录制，同时也是q结束录制
  - 使用q{register}选择要保存的寄存器，把录制的命令保存到其中
  - 使用@{register}回放寄存器中保存的一些列命名
- 代码补全（三种补全类型）
  - 使用ctrl+n和ctrl+p补全单词
  - 使用ctrl+x ctrl+f补全文件名
  - 使用ctrl+x ctrl+o补全代码，需要开启文件类型检查，安装插件
- vim配色
  - :colorscheme显示当前的主题配色，默认default
  - :colorscheme <ctrl+d> 显示所有的配色
  - :colorscheme 配色名 更换配色



## vim配置

- vim映射（VIm映射就是把「一个操作」映射到「另一个操作」）
  - 基本映射指的是normal模式下的映射，
    - 使用map就可以实现映射，比如:map - x 然后就按一个 - 就会删除字符
    - :map <space> viw 告诉vim按下空格的时候选中整个单词
    - :map <c-d> dd 可以使用ctrl+d执行dd删除一行
  - Vim常用的normal/visual/insert都可以映射，用nmap/vmap/imap定义映射只在normal/visual/insert分别有效 
    - 现有的映射问题是当设置 : nmap - dd和:nmap \ - ，当使用-会进行递归映射，使用\就可以执行dd操作。
    - *map有递归的风险，如果安装了一个插件，插件映射到了同一个案件的不同行为。有冲突就会有一个失效
  - Vim提供非递归映射，使用*map对应的nnoremap/vnoremap/inoremap,「任何时候」都使用非递归映射，避免冲突



## 插件

VIm插件是使用vimscript或者其他语言编写的vim功能扩展

### 如何安装插件

- 目前Vim有很多插件管理器可供选择，选择一个顺手的
- 常用的有vim-plug，Vundle，Pathogen，Dein.vim，volt等
- 综合性能、简易型、文档等几个方面，这里推荐使用vim-plug



### 使用vim-plug安装插件

- https://github.com/junegunn/vim-plug
- 提供官方文档示例



### 如何搜寻插件

- 通过google/百度
- [https://vimawesome.com](https://vimawesome.com/)

### Vim美化插件

更改vim的外观

- 修改启动界面： https://github.com/mhinz/vim-startify
- 状态栏美化：https://github.com/vim-airline/vim-airline
- 增加代码缩进线条：https://github.com/yggdroot/indentline
- 配色
  - vim-hybird配色：https://github.com/w0ng/vim-hybrid
  - solarized配色：https://github.com/altercation/vim-colors-solarized
  - gruvbox配色：https://github.com/altercation/vim-colors-solarized

### 优化插件

- 文件管理器nerdtree
  - 使用nerdtree插件进行文件目录树管理
  - https://github.com/scrooloose/nerdtree
  - noremap tr :NERDTreeToggle<CR>  通过快捷键快速打开和关闭目录
  - noremap <leader>v :NERDTreeFind<CR>  查找文件位置
- 快速搜索器
  - 快速查找并打开文件可以用ctrlp插件
  - https://github.com/ctrlpvim/ctrlp.vim
  - let g:ctrlp_map = '<c-p>'
- Vim快速定位插件
  - vim自带移动命令w/e基于单词移动，gg/G文件首尾，0/$行首尾，f{char}查询字符
  - ctrl+f ctrl+u前后翻屏
  - 使用easymotion实现快速定位
  - https://github.com/easymotion/vim-easymotion
  - nmap ss <Plug>(easymotion-s2) 使用ss快速查询
- 成对编辑
  - https://github.com/tpope/vim-surround
  - normal模式下面增加，删除，修改成对内容
  - ds（delete a surrounding）、cs(change a surrounding)、ys(you  a surrounding)
- 模糊搜索fzf与fzf.vim
  - https://github.com/junegunn/fzf.vim
  - 使用Ag[PATTREN]模糊搜索字符串
  - 使用File[Path]模糊搜索目录
- 搜索替换插件far.vim
- Vim-go插件自动补全
  - https://github.com/fatih/vim-go
  - <c-x><c-o> 补全
  - <c-]> 查看函数内容你  <c-o> 回退 <c-i>前进
  - 使用:gofmt 实现代码格式化
  - :GoRename 实现重构  :GoImports自动导入
- Python-mode
  - 比较多的是jedi-vim和Python-mode
  - https://github.com/python-mode/python-mode
  - python-mode同样具有补全、跳转、重构、格式化功能
- tagbar
  - 需要安装Universal Ctags生成对应的tag文件
- vim-interestingword高亮感兴趣单词
- 补全插件 deoplete.nvim或者coc.nvim
- Vim-autoformat和Neoformat是两种使用较多的格式化插件
  - 需要安装对应的格式化库。Python autopep8/js的prettier等
- 静态检查Lint
  - neomake和ale是两种常用的lint
- 快速注释 vim-commentary
  - https://github.com/tpope/vim-commentary
- fugitive
  - 在vim里面使用git
  - Gedit，Gdiff，Gblame，Gcommit
- Vim-gitgutter在vim里面显示文件变动
  - 在修改文件之后可以显示当前文件的变动  
- gv.vim查看git历史变更记录

------

推荐书籍《笨方法学VimScript》 

《practical vim》