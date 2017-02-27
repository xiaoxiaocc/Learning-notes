在需要创建仓库的文件夹打开git-bash

1. 配置用户名：
    ```
      git config --global user.name yourname
    ```
2. 配置邮箱：
    ```
      git config --global user.email youremail
    ```
3. 查看配置信息：
    ```
      git config --list
    ```
4. 添加ssh key：
    ```
     ssh-keygen -t rsa

     会提示在在某个目录生成的id_rsa和id_rsa_pub文件，其中后者为公钥。将公钥内容复制粘贴到github Profile Settings->SSH key-> add ssh keys。
    ```
5. 测试一下：
    ```
      ssh git@github.com
    ```
