# JinxLori.github.io
wsh Blog



切换分支命令

git checkout 分支名



资源文件分支 blog_source

blog静态网页资源文件分支 master



上传资源更新到git

先切换到blog_source分支下

git add .

git commit -m '提交注释'

git push origin blog_source



更新blog静态资源

hexo g

hexo s  (本地部署)

hexo d