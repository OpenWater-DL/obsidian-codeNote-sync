终端自动补全的配置

打开终端，输入 :

nano .inputrc

在文件里面写上：

set completion-ignore-case on  
set show-all-if-ambiguous on  
TAB: menu-complete

ctrl + o ,回车，重启终端，自动补全按tab键就ok。

  