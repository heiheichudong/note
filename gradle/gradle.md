> 仓库：
```
https://mvnrepository.com/
```
- 保持最新：latest.release

[TOC]
> 问题  
- 多人开发时,会出现明明在gitignore中忽略了.idea文件夹,但是提交时仍旧会出现.idea内文件变动的情况     
> 原因  
- .idea已经被git跟踪，之后再加入.gitignore后是没有作用的
> 解决方案  
- 清除.idea的git缓存
```
git rm -r --cached .idea
```
- .gitignore中添加.idea