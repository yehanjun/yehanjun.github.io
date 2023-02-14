Git迁移新仓库并保存历史提交记录
第一步，从远程仓库克隆到本地

git clone https://gitee.com/oldxxx/oldxxx.git

第二步，删除需要迁移的本地项目所关联的远程仓库地址

git remote remove origin

第三步，关联新仓库的地址

git remote add origin https://gitee.com/newxxx/newxxx.git

第四步，把项目推送到新的远程仓库

git push --set-upstream origin master

第五步，从原仓库地址克隆一份裸版本库

git clone --bare https://gitee.com/oldxxx/oldxxx.git

第六步，原仓库所有分支同步新仓库

git push --mirro https://gitee.com/newxxx/newxxx.git



