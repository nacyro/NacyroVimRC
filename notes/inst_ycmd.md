# 安装配置 YouCompleteMe 动作要领

## &sect;1 配置 Socks5 网络代理

* 在你的 `~/.bashrc` 中加入如下环境变量:
```bash
export http_proxy=socks5://127.0.0.1:10808
export https_proxy=socks5://127.0.0.1:10808
```
* 在 `~/.gitconfig` 中加入如下配置:
```ini
[http]
	proxy = socks5://127.0.0.1:10808
[https]
	proxy = socks5://127.0.0.1:10808
```

## &sect;2 安装 YouCompleteMe 源码

### &sect;2.1 查看 GitHub 仓库大小
访问 `https://api.github.com/repos/user/repo` 的 `size` 字段  
https://api.github.com/repos/ycm-core/YouCompleteMe 

### &sect;2.2 自动安装 YouCompleteMe
* 设置好代理后, Vundle 也能轻松下载 YouCompleteMe, 就是慢, 也许;

### &sect;2.3 手动安装 YouCompleteMe
* 使用 gh 而不是 git 克隆源码, 相同条件下 gh 比 git 快上十倍以上;
  Linux安装就用Linux克隆源码, Windows安装就用Windows克隆源码;
  否则易出现换行符格式不对的问题;
```bash
cd ~/.vim/bundle
gh auth login
gh repo clone ycm-core/YouCompleteMe
```

### &sect;2.4 下载好大型依赖并放到指定位置
* 版本可能已经过期, 按照报错提示下载;

```
https://github.com/OmniSharp/omnisharp-roslyn/releases/download/v1.35.4/omnisharp.http-linux-x64.tar.gz
https://dl.bintray.com/ycm-core/libclang/libclang-11.0.0-x86_64-unknown-linux-gnu.tar.bz2

/home/suse/.vim/bundle/YouCompleteMe/third_party/ycmd/clang_archives/
/home/suse/.vim/bundle/YouCompleteMe/third_party/ycmd/third_party/omnisharp-roslyn/v1.35.4/
```

## &sect;3 编译
* 注意配置 npm 国内源
```bash
npm config set registry http://registry.npm.taobao.org
```

* 按照官方 README 安装好依赖, 执行编译, 然后去睡觉或喝茶;
```bash
cd ~/.vim/bundle/YouCompleteMe
python3 install.py --all
```


## &sect;4 配置(待续)
```vimrc
" ========================= Vundle Settings =========================
filetype off                                     " 为Vundle关闭filetype
" set the runtime path to include Vundle and initialize
if has("win32")
    set rtp+=$VIM/vimfiles/bundle/Vundle.vim     " 设置Vundle运行时
    call vundle#begin('$VIM/vimfiles/bundle/')   " 初始化Vundle
else
    set rtp+=$HOME/.vim/bundle/Vundle.vim        " 设置Vundle运行时
    call vundle#begin('$HOME/.vim/bundle/')      " 初始化Vundle
endif
Plugin 'VundleVim/Vundle.vim'                    " 达成VundleVim自管理
Plugin 'Valloric/YouCompleteMe'
call vundle#end()
filetype plugin indent on                        " 启用文件类型识别

" ========================= Plugin Settings =========================
" ========== Plugin YouCompleteMe ==========
if has("win32")
	let g:ycm_server_python_interpreter='C:\Nacyro\opt\Python38\python.exe'
else
	let g:ycm_server_python_interpreter='/usr/bin/python'
endif
"let g:ycm_global_ycm_extra_conf='$VIM/.ycm_extra_conf.py'
let g:ycm_show_diagnostics_ui = 0                  " 关闭语法提示
let g:ycm_complete_in_comments = 1                 " 补全功能在注释中同样有效
let g:ycm_confirm_extra_conf = 0                   " 允许 vim 加载 .ycm_extra_conf.py 文件, 不再提示
let g:ycm_collect_identifiers_from_tags_files = 1  " 开启 YCM 标签补全引擎
let g:ycm_min_num_of_chars_for_completion = 1      " 从第一个键入字符就开始罗列匹配项
let g:ycm_cache_omnifunc = 0                       " 禁止缓存匹配项，每次都重新生成匹配项
let g:ycm_seed_identifiers_with_syntax = 1         " 语法关键字补全
let g:ycm_goto_buffer_command = 'horizontal-split' " 跳转打开上下分屏
map <F2> :YcmCompleter GoToDefinition<CR>
map <F3> :YcmCompleter GoToDeclaration<CR>
map <F4> :YcmCompleter GoToDefinitionElseDeclaration<CR>
```

