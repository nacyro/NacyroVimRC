# &sect; VIM使用方法 #

<!-- TOC -->

![](images/vi-vim-cheat-sheet.gif 'vi-vim-cheat-sheet')

### &sect; Vim按键定义 ###
* 别用 ESC, 用 C-[ C-c 更快捷.
* 在编辑模式下移动:
```vim
inoremap <C-h> <Left>
inoremap <C-j> <Down>
inoremap <C-k> <Up>
inoremap <C-l> <Right>
```

### &sect; buffer操作 ###
```vim
:ls  查看已打开的buffer
:bN  切换到缓冲N
:bn  切换到列表中下一缓冲
:bp  切换到列表中上一缓冲
:b#  切换到之前所在的缓冲
```

### &sect; 多标签与多窗口 ###
##### 多窗口操作 #####
```vim
:sp  上下切分
:vs  左右切分
:[vertical] res[ize] [N]
CTRL-W =        使得所有窗口 (几乎) 等宽、等高，但当前窗口使用 'winheight' 和 'winwidth'。
:res[ize] -N
CTRL-W -        使得当前窗口高度减 N (默认值是 1)。如果在 'vertical' 之后使用，则使得宽度减 N
:res[ize] +N
CTRL-W +        使得当前窗口高度加 N (默认值是 1)。如果在 'vertical' 之后使用，则使得宽度加 N
:res[ize] [N]
CTRL-W CTRL-_
CTRL-W _        设置当前窗口的高度为 N (默认值为最大可能高度)
:vertical res[ize] [N]
CTRL-W |        设置当前窗口的宽度为 N (默认值为最大可能宽度)
z{nr}<CR>       设置当前窗口的高度为 {nr}  
CTRL-W <        使得当前窗口宽度减 N (默认值是 1)
CTRL-W >        使得当前窗口宽度加 N (默认值是 1)
<整个窗口的移动>
CTRL-W-H 将窗口移到最左边
CTRL-W-L 将窗口移到最右边
CTRL-W-J 将窗口移到底端
CTRL-W-K 将窗口移到顶端
" 定义调节窗口大小的快捷键
nmap w= :vertical resize +2<CR>
nmap w- :vertical resize -2<CR>
nmap w, :resize +2<CR>
nmap w. :resize -2<CR>
```
##### 多标签操作 #####
```vim
vim 只有一个标签时默认不显示标签栏,可用 `set showtabline=1` 设置
vim 默认只能打开10个标签页,需要使用 `set tabpagemax=${num}` 改变这个限制
$ vim -p ${FILE_NAMES} ## 以多标签形式打开文件
$ vim -p *             ## 以标签模式打开当前目录所有文件
:tabnew [file]         ## 新建标签中打开指定文件
:tabe [file]           ## 同上
:tab split             ## 在新标签页中打开当前缓冲
:tabf or :tabfind      ## 搜索并打开${PATH}中的文件
:tabs                  ## 标签列表
:tabc                  ## 关闭当前标签
:tabo                  ## 关闭所有其他标签
:tabp or gT            ## 查看前一标签
:tabn or gt            ## 查看后一标签
:tabfirst or :tabr     ## 移动到第一标签页
:tablast               ## 移动到最后标签页
:tabm [opnum]          ## 移动当前标签页到指定位置,从0开始计数,不指定计数移至最后
:tabdo [cmd]           ## 标签页域执行 `:tabdo %s/food/drink/g`
```

### &sect; Vim补全方案 ###
##### 内置`ins-completion`写C够用 #####
```vim
:help ins-completion         :help compl-omni
:help 'omnifunc'             :help i_CTRL-X_CTRL-O
:help ins-completion-menu    :help popupmenu-keys
:help 'completeopt'          :help compl-omni-filetypes
:help omnicppcomplete.txt

<C-x><C-l>                整行
<C-x><C-f>                文件名
<C-x><C-p> or <C-x><C-n>  文件域关键字
<C-n> or <C-p>            complete选项所指定范围中的关键字,范围更广,
                          不像<C-x><C-p> or <C-x><C-n>局限于文件域;
                          complete定义详见 :help E535
<C-x><C-k>                字典补全,指定字典文件,例如:
                          :set dictionary+=/path/to/es6.dict
<C-x><C-o>                OmniCompletion 语义补全
                          Vim 根据光标前的内容猜测光标后的内容
CTags初始化:
CTags刷新:
```

### &sect; Shell命令操作与实用命令 ###
```vim
:!wc %          ## 测量当前文本
:read !wc %     ## 添加命令输出为下一行
:2read !wc %    ## 输出添加到指定行后,$指定最后一行,0指定第一行前
:r !date        ## 读入时间到下一行
:r !echo "scale=3;2^7"| bc          ## bc计算器
:r!echo "scale=10000;4*a(1)"|bc -l  ## 计算PI前10000位,2MIN+
:w !sudo tee %  ## 提升权限并保存
:sh  :shell     ## 直接访问Shell,执行exit或<C-D>返回
```

### &sect; 设置工作路径 ###
```vim
:cd ${DIR}      改变Vim当前的工作路径
:lcd ${DIR}     改变当前窗口的工作路径
:pwd            打印工作路径
:set autochdir  自动设置当前文本所在目录为当前工作目录
```

### &sect; iconv编码转换 ###
```vim
----- 参数 -----
-f encoding, --from-code=encoding  ## 把字符从encoding编码开始转换
-t encoding, --to-code=encoding    ## 把字符转换到encoding编码
-l --list                          ## 列出已知的编码字符集合
-o file                            ## 指定输出文件
-c                                 ## 忽略输出的非法字符
-s                                 ## 安静处理
----- 用例 -----
iconv -f gbk -t utf-8 main.c
```

### &sect; 系统剪贴板 ###
* 复制Vim里面的内容至系统粘贴板 `"+y`
* 粘贴系统粘贴板里面的内容至Vim `"+p`

