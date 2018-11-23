---
title: "SublimeText3编辑器+Python3.7的DIY"
header:
  image: /assets/images/2018-11-22-EditorDIY/20181122200118-PJSON.png
  caption: PJSON
categories:
  - 工具
tags:
  - editor
  - SublimeText3
  - Python3
---

## WHY

编辑器，像linux自带的vim（当然也可以DIY，我没接触过），mg，nano，gedit，windows下常见的notedpad++，ultraedit，等等，一些IDE也会自带编辑器，比如matlab，VS还有Python最火的集成方案Anaconda+Spyder，是码农日常必备的工具。既然有了这些集成方案，为什么我们会费力去折腾editor。

我DIY的起因可以追溯到看C++ Primer这本书的时候，Stanley B. Lippman写到：
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/2018-11-23-213717-CPP_GCC.jpg" alt="placeholder image" caption="" %}
当时只接触过像VS2013这样的IDE，完全没有用过GCC和linux，更不要提后来令人无法自拔的autotools这些工具。后来接触了bash之后，真正认同了，hacker lives only in linux这种理念，无限崇尚自由和个人能力。

第一次接触强大的editor还是起源于[这篇博客](https://blog.csdn.net/redguardtoo/article/details/7222501/)，好奇心害死猫，就跳进了[steve purcell](https://github.com/purcell/emacs.d) + Emacs的深坑，"Emacs :loves: you"这几个字出来的一瞬间，完全被惊艳到：
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/2018-11-23-214819-EmacsFinal.jpg" alt="placeholder image" caption="" %}

后来偶然发现，linux的terminal/bash中，光标移动的shortcuts和emacs中的完全一样，ipython中也是，MacOS更狠，全系统都是！！！从此就像练了乾坤大挪移以后的张无忌，码字速度飞起，并彻底嫌弃了windows。分屏，语法高亮，build集成，自动补全，目录树，连接ssh，上网，发邮件，真是只有想不到没有emacs不能的！！！

到现在在自己的pro和有sudo权限的linux上还是emacs，vim一样好，只是我先跳了Richard Stallman的阵营而已。之所以会用SublimeText3，也是拜GFW所赐，同时也有Corey Schafer的功劳。 因为GFW的原因，有一些emacs包下载很慢，而且，emacs本身的配置是要比sublime复杂的。同时Corey在油管上有很好的视频教程，配置sublimetext3环境（btw，Corey的英语非常好听，语速也不快，大家不用字幕也没什么压力，日常煲耳），简直是傻瓜教程。Sublime最吸引人的功能就是多行同时编辑，还有Emmet这个反人类的插件！！！简直是HTML/CSS/JS的救星。最终效果：
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/2018-11-23-212620-FinalResult.png" alt="placeholder image" caption="" %}

总结一下，为什么要DIY：
- 好看+好玩！！！
- 效率的提升：弱化对鼠标的依赖[emacs做的最好]，双手不离开主键盘区域就可以掌控整个电脑；
- 代码支持强大：语法高亮，自动补全，自动缩进，complier/intepretor集成，分屏，目录树...
- 灵活性强，自适应啊！！！


## 整体方案
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/SublimeText3.png" alt="placeholder image" caption="" %}


## 推荐的plug-in
- Package Control: 管理插件的插件，sublimetext2之前是需要添加一段代码到debug terminal中去下载的，现在不用了，直接集成到Sublime3中；快捷键是`CTRL+SHIFT+P`，输入install可以进行安装(以下不在重复这个步骤)，根据网速，页面加载的速度也不一样。
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/20181123221846-packagecontrol-install.png" alt="placeholder image" caption="" %}
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/20181123221948-pacakagecontrol-loading.png" alt="placeholder image" caption="" %}
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/20181123221948-pacakagecontrol-result.png" alt="placeholder image" caption="" %}
- Daylee Rees Color Schemes: 配色方案库，只修改配色，不更改界面布局。这个作用就相当于CSS，喜欢什么样的配色，就到packagecontrol里边相应的配色就行，推荐EarthSong，非常平和的颜色。
```
ctrl+shift+p进入package control；
输入install进入安装页面；
输入daylee rees color schemes；
```
- Material Theme：修改editor主题的插件，不仅会改配色还会改图标；安装同上，需要注意的是，安装结束后，要根据Pacakge message的消息显示，在user配置里边添加相应代码激活，<b>不要在default中添加</b>
```
1. 同上一样安装
2. 在preference setting中添加相应的激活代码
```
- Code Block Heighlighter: <b>brackethighlighter</b>代码段起止block标记，对于长循环尤其有帮助
- Sidebar options enhancement：<b>SideBarEnhancement</b>原始的目录树鼠标右键得到的功能不强，这是一个补充
- 代码自动补全：<b>SublimeCodeIntel</b>
- 代码自动扩展：<b>Emmet</b>。这是个神器，还没有完全掌握。html、css一些长tag，可以键入几个字然后用emmt的快捷键补全，典型的像`ctrl+e`
- 语法检查：<b>SublimeLinter</b>，这个是支持不同编程语言的语法检查的工具，也是安装起来最麻烦的。不同语言对应不用插件，像JavaScript对应jlint，python对应sublimelinter-pylint，需要自己去package control里边输入sublimelinter之后浏览，同时还需要使用pip/conda/pipenv(python)，npm(java，node.js)去安装相应的应用插件。
- Python build system：这个需要在`Tools->Build System->New Build System`中添加相应的配置文件即可，将下边python解释器的路径修改掉就行
```
{
    "cmd": ["C:/Software/Programming/Anaconda3/python.exe", "-u", "$file"],
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
}
```
使用方法是，在相应的代码页面，`ctrl+b`就是了

## 我的配置
- user settings
```
{
    "bold_folder_labels": true,
    "caret_extra_width": 1,
    "caret_style": "phase",
    "close_windows_when_empty": false,
    "color_scheme": "Packages/Dayle Rees Color Schemes/legacy/Earthsong.tmTheme",
    "copy_with_empty_selection": false,
    "drag_text": false,
    "draw_minimap_border": true,
    "enable_tab_scrolling": false,
    "ensure_newline_at_eof_on_save": true,
    "file_exclude_patterns":
    [
        "*.pyc",
        "*.pyo",
        "*.exe",
        "*.dll",
        "*.obj",
        "*.o",
        "*.a",
        "*.lib",
        "*.so",
        "*.dylib",
        "*.ncb",
        "*.sdf",
        "*.suo",
        "*.pdb",
        "*.idb",
        ".DS_Store",
        "*.class",
        "*.psd",
        "*.sublime-workspace"
    ],
    "font_face": "Source Code Pro",
    "font_options":
    [
        "no_round"
    ],
    "font_size": 12,
    "highlight_line": true,
    "highlight_modified_tabs": true,
    "ignored_packages":
    [
        "Markdown",
        "Vintage"
    ],
    "line_padding_bottom": 1,
    "line_padding_top": 1,
    "match_brackets_content": false,
    "match_selection": false,
    "match_tags": false,
    "material_theme_accent_graphite": true,
    "material_theme_compact_sidebar": true,
    "open_files_in_new_window": false,
    "overlay_scroll_bars": "enabled",
    "preview_on_click": false,
    "scroll_past_end": true,
    "scroll_speed": 5.0,
    "show_definitions": true,
    "show_encoding": true,
    "show_errors_inline": false,
    "show_full_path": false,
    "sidebar_default": true,
    "theme": "Material-Theme-Darker.sublime-theme",
    "translate_tabs_to_spaces": true,
    "trim_trailing_white_space_on_save": true,
    "use_simple_full_screen": true,
    "word_wrap": true
}
```
- anaconda

```
{
    "auto_formatting": true,
    "autoformat_ignore":
    [
        "E309",
        "E501"
    ],
    "pep8_ignore":
    [
        "E309",
        "E501"
    ],
    "anaconda_linter_underlines": false,
    "anaconda_linter_mark_style": "none",
    "display_signatures": false,
    "disable_anaconda_completion": true
}
```

## 一些坑
有的时候，网速非常慢，package control经常下载失败，这个时候是可以手动到package control官方网页下载，然后解压缩到package的位置。pacakge的位置通过preference->pacakge browser->User的方式查看。
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/20181123224541-pacakgebrowser.png" alt="placeholder image" caption="" %}
{% include figure image_path="/assets/images/2018-11-22-EditorDIY/20181123224541-pacakgebrowser-User.png" alt="placeholder image" caption="" %}

## 常用快捷键整理
- <b>Ctrl + shift + p</b>: open command palette
- <b>Ctrl + P</b>: search files in project
- <b>Ctrl + G</b>: jump to lines
- <b>Ctrl + W</b>: close current file
- <b>Ctrl + [mouse_click]</b>: multi-cursors setting for synchronous editing
- <b>Ctrl + F</b>: search
- <b>Ctrl + H</b>: replace
- <b>Ctrl + L</b>: select line
- <b>Ctrl + shift + arrow</b>: select parts of block with [left/right], and move it with [up/down]
- <b>[Ctrl + mouse_click]+[Ctrl + shift + arrow]+[Ctrl + D]</b>: multi copy-paste
- <b>[Ctrl + L] + [Ctrl + shift + arrow]</b>: move selected line
- <b>Ctrl + /</b>: commit / uncommit lines
- <b>Ctrl + D</b>: <b><em>Ctrl</em></b> and repeated <b><em>D</em></b>, select same texts in different position for synchronous changes
- <b>Alt + F3<b>: select all same thing in the article
- <b>[Ctrl + tab] or [Ctrl + shift + tab]</b>: move between windows [normal OS shortcuts]
- <b>[Ctrl + W] or [Ctrl + shift + T]</b>: close tab / reopen recent closed tab [normal OS shortcuts]
- <b>[Alt + shift + 1/2/3/4/8/9]</b>: split windows for multi-view. <em>But i think Emacs-style is a lot better than this</em>
- <b>Ctrl + B<b>: build code with selected build system
- <b>Ctrl + K + Ctrl + B</b>: collapse/reopen the sidebar <em>hold on Ctrl key</em>
- <b>Ctrl + shift + p</b>: open command palette, for install/remove/choose package
- <b>Ctrl + k + Ctrl + C</b>: move to the selected line
- <b>HOME / END</b>: move to the begin / end of the word in the line


## 参考资料
- CoreySchafer：该blog是对Corey Schafer视频的一个粗陋整理，详细见原video。

<iframe width="640" height="360" src="https://www.youtube.com/embed/zVLJfrIwEP8?list=PL-osiE80TeTtHH8BZngXEsLPGotQxZa6z" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<iframe width="640" height="360" src="https://www.youtube.com/embed/xFciV6Ew5r4?list=PL-osiE80TeTt66h8cVpmbayBKlMTuS55y" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<iframe width="640" height="360" src="https://www.youtube.com/embed/xqcTfplzr7c?list=PL-osiE80TeTt66h8cVpmbayBKlMTuS55y" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


- Official doc
