
…or create a new repository on the command line
```
echo "# subtitleVideo" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:heiheichudong/subtitleVideo.git
git push -u origin master
```
…or push an existing repository from the command line
```
git remote add origin git@github.com:heiheichudong/subtitleVideo.git
git push -u origin master
```
…or import code from another repository
```
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.
```





简易的命令行入门教程:
Git 全局设置:
```
git config --global user.name "嘿嘿行动"
git config --global user.email "wlbz2014@163.com"
```
创建 git 仓库:
```
mkdir stock
cd stock
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin git@gitee.com:heiheixingdong/stock.git
git push -u origin master
```
已有仓库?
```
cd existing_git_repo
git remote add origin git@gitee.com:heiheixingdong/stock.git
git push -u origin maste
```
