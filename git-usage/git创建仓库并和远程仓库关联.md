在需要创建仓库的文件夹打开git-bash打开git-bash

1. 新建一个远程仓库
2. 本地初始化
```
git init
```
3. 关联远程仓库
```
git remote add origin git@github.com:xiaoxiaocc/Learning-notes.git
```
4. 如果我们在创建远程仓库的时候添加了README和.ignore等文件,我们在后面关联仓库后,需要先执行pull操作
```
git pull origin master
```
5. 添加需要的文件
```
git add 文件
```
6. 提交
```
git commit -m '注释内容'
```
7. push到远程仓库(第一次使用加上了-u参数，是推送内容并关联分支)
```
git push -u origin master
```
