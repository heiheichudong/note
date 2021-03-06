## 配置信息：git config 命令
```
git config [<options>]

Config file location
    --global              use global config file
    --system              use system config file
    --local               use repository config file
    -f, --file <file>     use given config file
    --blob <blob-id>      read config from given blob object

Action
    --get                 get value: name [value-regex]
    --get-all             get all values: key [value-regex]
    --get-regexp          get values for regexp: name-regex [value-regex]
    --get-urlmatch        get value specific for the URL: section[.var] URL
    --replace-all         replace all matching variables: name value [value_regex]
    --add                 add a new variable: name value
    --unset               remove a variable: name [value-regex]
    --unset-all           remove all matches: name [value-regex]
    --rename-section      rename section: old-name new-name
    --remove-section      remove a section: name
    -l, --list            list all
    -e, --edit            open an editor
    --get-color           find the color configured: slot [default]
    --get-colorbool       find the color setting: slot [stdout-is-tty]

Type
    --bool                value is "true" or "false"
    --int                 value is decimal number
    --bool-or-int         value is --bool or --int
    --path                value is a path (file or directory name)

Other
    -z, --null            terminate values with NUL byte
    --name-only           show variable names only
    --includes            respect include directives on lookup
    --show-origin         show origin of config (file, standard input, blob, command line)
```
## 配置名字和邮箱：-- global 全局的设置
```
git config --global user.name "zl"
git config --global user.email "wlbz2014@163.com"
```
## git仓库的创建：
```
mkdir <filename> 	//创建文件夹
cd <filename> 		//切换到文件夹
pwd			//查看当前文件夹
git init		//初始化git
```

## 添加远程库：
> 在服务器上创建git仓库
> 添加远程仓库：

```
git remote add origin https://github.com/heiheichudong/gitnote.git 	//添加远程库地址
git push -u origin master 						//第一次把内容推到远程库
git push origin master 							//之后就可以这样
git push origin dev							//推到指定分支
git remote -v 								//查看远程库
```

## 修改远程仓库:
#### 方法一：修改命令
```
git remote set-url origin [url]
```

#### 方法二：先删后加
```
git remote rm origin 
git remote add origin [url]
```

#### 方法三：直接修改config文件
```
config 位置待续
```

## 创建与合并分支
```
git checkout -b '分支名字' 	    //创建并切换的分支
git branch 分支名字		        //创建分支
git branch -a  			        //查看所有分支
git checkout 分支名字 		    //切换到分支
git branch 			            //查看分支
git merge 分支名字		        //合并到当前分支
git branch -d dev		        //删除分支
git log --graph --pretty=oneline --abbrev-commit 
//用带参数的 git log也可以看到分支的合并情况：合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
git branch -D <name> 强行删除
git push --set-upstream origin 分支名		//推送本地分支到远程仓库
git checkout -b 本地分支名 origin/远程分支名		//将远程git仓库里的指定分支拉取到本地（本地不存在的分支）拉取不成功 我们先执行 git fetch
```
## 保存现场
```
git stash		//保存当前的状态
git stash apply		//恢复保存的状态
git stash drop		//删除保存的状态
git stash pop		//恢复和删除保存的状态
```