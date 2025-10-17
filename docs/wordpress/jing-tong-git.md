---
layout: default
title: 精通git
parent: wordpress
---

# 1113-11-10-《精通git》读书笔记

## 目录

- [3.5 远程分支](#35-远程分支)
- [ch04](#ch04)
  - [4.1 协议](#41-协议)
    - [4.1.1 本地协议](#411-本地协议)
    - [4.1.2 HTTP协议](#412-HTTP协议)
    - [4.1.3 SSH协议](#413-SSH协议)
    - [4.1.4 git协议](#414-git协议)
  - [4.2 在服务器上搭建git](#42-在服务器上搭建git)
    - [4.2.1 将裸仓库放置在服务器上](#421-将裸仓库放置在服务器上)
    - [4.2.2 小型团队配置](#422-小型团队配置)
  - [4.3 生成个人的ssh公钥](#43-生成个人的ssh公钥)
  - [4.4 设置服务器](#44-设置服务器)
  - [4.5 git守护进程](#45-git守护进程)
  - [4.6 智能HTTP](#46-智能HTTP)
  - [4.7 GitWeb](#47-GitWeb)
  - [4.8 GitLab](#48-GitLab)
- [ch05](#ch05)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-1-%E5%88%86%E5%B8%83%E5%BC%8F%E5%B7%A5%E4%BD%9C%E6%B5%81 "5.1 分布式工作流")5.1 分布式工作流](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git5-1-E58886E5B883E5BC8FE5B7A5E4BD9CE6B581-51-分布式工作流51-分布式工作流)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-1-1-%E9%9B%86%E4%B8%AD%E5%BC%8F%E5%B7%A5%E4%BD%9C%E6%B5%81 "5.1.1 集中式工作流")5.1.1 集中式工作流](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git5-1-1-E99B86E4B8ADE5BC8FE5B7A5E4BD9CE6B581-511-集中式工作流511-集中式工作流)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-1-2-%E9%9B%86%E6%88%90%E7%AE%A1%E7%90%86%E8%80%85%E5%B7%A5%E4%BD%9C%E6%B5%81 "5.1.2 集成管理者工作流")5.1.2 集成管理者工作流](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git5-1-2-E99B86E68890E7AEA1E79086E88085E5B7A5E4BD9CE6B581-512-集成管理者工作流512-集成管理者工作流)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-1-3-%E5%8F%B8%E4%BB%A4%E5%AE%98%E4%B8%8E%E5%89%AF%E5%AE%98%E5%B7%A5%E4%BD%9C%E6%B5%81 "5.1.3 司令官与副官工作流")5.1.3 司令官与副官工作流](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git5-1-3-E58FB8E4BBA4E5AE98E4B88EE589AFE5AE98E5B7A5E4BD9CE6B581-513-司令官与副官工作流513-司令官与副官工作流)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-2-%E4%B8%BA%E9%A1%B9%E7%9B%AE%E5%81%9A%E8%B4%A1%E7%8C%AE "5.2 为项目做贡献")5.2 为项目做贡献](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git5-2-E4B8BAE9A1B9E79BAEE5819AE8B4A1E78CAE-52-为项目做贡献52-为项目做贡献)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-2-1-%E6%8F%90%E4%BA%A4%E5%87%86%E5%88%99 "5.2.1 提交准则")5.2.1 提交准则](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git5-2-1-E68F90E4BAA4E58786E58899-521-提交准则521-提交准则)
    - [5.2.4 用rebase -i将工作内容压缩成单个提交可能会方便维护人员评审补丁。](#524-用rebase--i将工作内容压缩成单个提交可能会方便维护人员评审补丁)
    - [5.2.5 用git format-patch来生成要通过电子邮件发送的mbox格式的文件](#525-用git-format-patch来生成要通过电子邮件发送的mbox格式的文件)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E7%A1%AE%E5%AE%9A%E5%BC%95%E5%85%A5%E5%86%85%E5%AE%B9 "确定引入内容")确定引入内容](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE7A1AEE5AE9AE5BC95E585A5E58685E5AEB9-确定引入内容确定引入内容)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-3-5-%E5%A4%A7%E5%9E%8B%E5%90%88%E5%B9%B6%E5%B7%A5%E4%BD%9C%E6%B5%81 "5.3.5 大型合并工作流")5.3.5 大型合并工作流](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git5-3-5-E5A4A7E59E8BE59088E5B9B6E5B7A5E4BD9CE6B581-535-大型合并工作流535-大型合并工作流)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-3-9-%E6%B1%87%E6%80%BB%E8%87%AAv1-1-1%E4%B9%8B%E5%90%8E%E6%89%80%E6%9C%89%E6%8F%90%E4%BA%A4 "5.3.9 汇总自v1.1.1之后所有提交")5.3.9 汇总自v1.1.1之后所有提交](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git5-3-9-E6B187E680BBE887AAv1-1-1E4B98BE5908EE68980E69C89E68F90E4BAA4-539-汇总自v111之后所有提交539-汇总自v111之后所有提交)
- [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch06 "ch06")ch06](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitch06-ch06ch06)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#6-3-2-%E6%B7%BB%E5%8A%A0%E5%8D%8F%E4%BD%9C%E4%BA%BA%E5%91%98%EF%BC%9ACollaborators "6.3.2 添加协作人员：Collaborators")6.3.2 添加协作人员：Collaborators](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git6-3-2-E6B7BBE58AA0E58D8FE4BD9CE4BABAE59198EFBC9ACollaborators-632-添加协作人员Collaborators632-添加协作人员Collaborators)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#6-5-GitHub%E8%84%9A%E6%9C%AC%E5%8C%96 "6.5 GitHub脚本化")6.5 GitHub脚本化](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git6-5-GitHubE8849AE69CACE58C96-65-GitHub脚本化65-GitHub脚本化)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#6-5-1-%E9%92%A9%E5%AD%90%E7%B3%BB%E7%BB%9F "6.5.1 钩子系统")6.5.1 钩子系统](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git6-5-1-E992A9E5AD90E7B3BBE7BB9F-651-钩子系统651-钩子系统)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#6-5-2-GitHub-API "6.5.2 GitHub API")6.5.2 GitHub API](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git6-5-2-GitHub-API-652-GitHub-API652-GitHub-API)
- [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch07 "ch07")ch07](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitch07-ch07ch07)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E9%80%89%E6%8B%A9%E4%BF%AE%E8%AE%A2%E7%89%88%E6%9C%AC "选择修订版本")选择修订版本](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE98089E68BA9E4BFAEE8AEA2E78988E69CAC-选择修订版本选择修订版本)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%98%BE%E7%A4%BA%E5%87%BA%E6%8F%90%E4%BA%A4%E5%B1%9E%E4%BA%8E%E5%93%AA%E4%B8%80%E4%BE%A7%E7%9A%84%E5%88%86%E6%94%AF "显示出提交属于哪一侧的分支")显示出提交属于哪一侧的分支](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE698BEE7A4BAE587BAE68F90E4BAA4E5B19EE4BA8EE593AAE4B880E4BEA7E79A84E58886E694AF-显示出提交属于哪一侧的分支显示出提交属于哪一侧的分支)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-3-%E5%82%A8%E8%97%8F "7.3 储藏")7.3 储藏](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-3-E582A8E8978F-73-储藏73-储藏)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-3-3-%E4%BB%8E%E5%82%A8%E8%97%8F%E4%B8%AD%E5%88%9B%E5%BB%BA%E5%88%86%E6%94%AF "7.3.3 从储藏中创建分支")7.3.3 从储藏中创建分支](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-3-3-E4BB8EE582A8E8978FE4B8ADE5889BE5BBBAE58886E694AF-733-从储藏中创建分支733-从储藏中创建分支)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%B8%85%E7%90%86%E5%B7%A5%E4%BD%9C%E7%9B%AE%E5%BD%95 "清理工作目录")清理工作目录](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE6B885E79086E5B7A5E4BD9CE79BAEE5BD95-清理工作目录清理工作目录)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-5-%E6%90%9C%E7%B4%A2 "7.5 搜索")7.5 搜索](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-5-E6909CE7B4A2-75-搜索75-搜索)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-5-1-%E5%B7%A5%E4%BD%9C%E7%9B%AE%E5%BD%95%E6%90%9C%E7%B4%A2 "7.5.1 工作目录搜索")7.5.1 工作目录搜索](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-5-1-E5B7A5E4BD9CE79BAEE5BD95E6909CE7B4A2-751-工作目录搜索751-工作目录搜索)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-5-2-%E6%97%A5%E5%BF%97%E6%90%9C%E7%B4%A2 "7.5.2 日志搜索")7.5.2 日志搜索](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-5-2-E697A5E5BF97E6909CE7B4A2-752-日志搜索752-日志搜索)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E9%87%8D%E5%86%99%E5%8E%86%E5%8F%B2 "重写历史")重写历史](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE9878DE58699E58E86E58FB2-重写历史重写历史)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-6-3-%E9%87%8D%E6%8E%92%E6%8F%90%E4%BA%A4%EF%BC%9A%E5%9C%A8%E4%BA%A4%E4%BA%92%E5%BC%8F%E5%8F%98%E5%9F%BA%E4%B8%AD%E6%94%B9%E5%8F%98%E8%A1%8C%E7%9A%84%E9%A1%BA%E5%BA%8F "7.6.3 重排提交：在交互式变基中改变行的顺序")7.6.3 重排提交：在交互式变基中改变行的顺序](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-6-3-E9878DE68E92E68F90E4BAA4EFBC9AE59CA8E4BAA4E4BA92E5BC8FE58F98E59FBAE4B8ADE694B9E58F98E8A18CE79A84E9A1BAE5BA8F-763-重排提交在交互式变基中改变行的顺序763-重排提交在交互式变基中改变行的顺序)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-6-4-%E5%8E%8B%E7%BC%A9%E6%8F%90%E4%BA%A4%EF%BC%9A%E5%9C%A8%E4%BA%A4%E4%BA%92%E5%BC%8F%E5%8F%98%E5%9F%BA%E4%B8%AD%E7%94%A8squash "7.6.4 压缩提交：在交互式变基中用squash")7.6.4 压缩提交：在交互式变基中用squash](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-6-4-E58E8BE7BCA9E68F90E4BAA4EFBC9AE59CA8E4BAA4E4BA92E5BC8FE58F98E59FBAE4B8ADE794A8squash-764-压缩提交在交互式变基中用squash764-压缩提交在交互式变基中用squash)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-6-5-%E6%8B%86%E5%88%86%E6%8F%90%E4%BA%A4%EF%BC%9A%E5%9C%A8%E4%BA%A4%E4%BA%92%E5%BC%8F%E5%8F%98%E5%9F%BA%E4%B8%AD%E7%94%A8edit "7.6.5 拆分提交：在交互式变基中用edit")7.6.5 拆分提交：在交互式变基中用edit](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-6-5-E68B86E58886E68F90E4BAA4EFBC9AE59CA8E4BAA4E4BA92E5BC8FE58F98E59FBAE4B8ADE794A8edit-765-拆分提交在交互式变基中用edit765-拆分提交在交互式变基中用edit)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-6-6-%E8%B6%85%E5%BC%BA%E5%91%BD%E4%BB%A4%EF%BC%9Afilter-branch "7.6.6 超强命令：filter-branch")7.6.6 超强命令：filter-branch](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-6-6-E8B685E5BCBAE591BDE4BBA4EFBC9Afilter-branch-766-超强命令filter-branch766-超强命令filter-branch)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E7%A7%98%EF%BC%9Areset%E5%92%8Ccheckout "7.7 重置揭秘：reset和checkout")7.7 重置揭秘：reset和checkout](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-7-E9878DE7BDAEE68FADE7A798EFBC9AresetE5928Ccheckout-77-重置揭秘reset和checkout77-重置揭秘reset和checkout)
    - [7.7.5 要压缩最新的几个提交，只需git reset --soft 旧提交然后commit](#775-要压缩最新的几个提交只需git-reset---soft-旧提交然后commit)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-7-7-%E6%96%87%E4%BB%B6%E7%BA%A7%E5%88%AB%E4%B8%8E%E6%8F%90%E4%BA%A4%E7%BA%A7%E5%88%AB "7.7.7 文件级别与提交级别")7.7.7 文件级别与提交级别](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-7-7-E69687E4BBB6E7BAA7E588ABE4B88EE68F90E4BAA4E7BAA7E588AB-777-文件级别与提交级别777-文件级别与提交级别)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-8-1-%E5%90%88%E5%B9%B6%E5%86%B2%E7%AA%81 "7.8.1 合并冲突")7.8.1 合并冲突](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-8-1-E59088E5B9B6E586B2E7AA81-781-合并冲突781-合并冲突)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-8-2-%E8%BF%98%E5%8E%9F%E6%8F%90%E4%BA%A4 "7.8.2 还原提交")7.8.2 还原提交](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-8-2-E8BF98E58E9FE68F90E4BAA4-782-还原提交782-还原提交)
    - [7.8.3 -Xours与-s ours](#783--Xours与-s-ours)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E5%AD%90%E6%A0%91%E5%90%88%E5%B9%B6 "子树合并")子树合并](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE5AD90E6A091E59088E5B9B6-子树合并子树合并)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-9-rerere "7.9 rerere")7.9 rerere](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-9-rerere-79-rerere79-rerere)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-10-%E4%BD%BF%E7%94%A8git%E8%B0%83%E8%AF%95 "7.10 使用git调试")7.10 使用git调试](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-10-E4BDBFE794A8gitE8B083E8AF95-710-使用git调试710-使用git调试)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-10-1-%E6%96%87%E4%BB%B6%E6%A0%87%E6%B3%A8 "7.10.1  文件标注")7.10.1 文件标注](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-10-1-E69687E4BBB6E6A087E6B3A8-7101--文件标注7101-文件标注)
    - [7.10.2 git bisect帮助尽快确定问题是由那、哪一次提交引发的](#7102-git-bisect帮助尽快确定问题是由那哪一次提交引发的)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-%E5%AD%90%E6%A8%A1%E5%9D%97 "7.11 子模块")7.11 子模块](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-11-E5AD90E6A8A1E59D97-711-子模块711-子模块)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-1-%E5%BC%80%E5%A7%8B%E4%BD%BF%E7%94%A8%E5%AD%90%E6%A8%A1%E5%9D%97 "7.11.1 开始使用子模块")7.11.1 开始使用子模块](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-11-1-E5BC80E5A78BE4BDBFE794A8E5AD90E6A8A1E59D97-7111-开始使用子模块7111-开始使用子模块)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-2-%E5%85%8B%E9%9A%86%E5%90%AB%E6%9C%89%E5%AD%90%E6%A8%A1%E5%9D%97%E7%9A%84%E9%A1%B9%E7%9B%AE "7.11.2 克隆含有子模块的项目")7.11.2 克隆含有子模块的项目](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-11-2-E5858BE99A86E590ABE69C89E5AD90E6A8A1E59D97E79A84E9A1B9E79BAE-7112-克隆含有子模块的项目7112-克隆含有子模块的项目)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-3-%E5%BC%80%E5%8F%91%E5%90%AB%E6%9C%89%E5%AD%90%E6%A8%A1%E5%9D%97%E7%9A%84%E9%A1%B9%E7%9B%AE "7.11.3 开发含有子模块的项目")7.11.3 开发含有子模块的项目](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-11-3-E5BC80E58F91E590ABE69C89E5AD90E6A8A1E59D97E79A84E9A1B9E79BAE-7113-开发含有子模块的项目7113-开发含有子模块的项目)
      - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%8B%89%E5%8F%96%E4%B8%8A%E6%B8%B8%E5%8F%98%E6%9B%B4 "拉取上游变更")拉取上游变更](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE68B89E58F96E4B88AE6B8B8E58F98E69BB4-拉取上游变更拉取上游变更)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-4-foreach%E4%B8%8E%E5%88%AB%E5%90%8D "7.11.4 foreach与别名")7.11.4 foreach与别名](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-11-4-foreachE4B88EE588ABE5908D-7114-foreach与别名7114-foreach与别名)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-5-%E5%AD%90%E6%A8%A1%E5%9D%97%E7%9A%84%E9%97%AE%E9%A2%98 "7.11.5 子模块的问题")7.11.5 子模块的问题](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-11-5-E5AD90E6A8A1E59D97E79A84E997AEE9A298-7115-子模块的问题7115-子模块的问题)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-12-%E6%89%93%E5%8C%85 "7.12 打包")7.12 打包](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-12-E68993E58C85-712-打包712-打包)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-13-%E6%9B%BF%E6%8D%A2 "7.13 替换")7.13 替换](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-13-E69BBFE68DA2-713-替换713-替换)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E5%87%AD%E6%8D%AE%E5%AD%98%E5%82%A8 "凭据存储")凭据存储](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE587ADE68DAEE5AD98E582A8-凭据存储凭据存储)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-14-1-%E5%BA%95%E5%B1%82%E5%AE%9E%E7%8E%B0 "7.14.1 底层实现")7.14.1 底层实现](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-14-1-E5BA95E5B182E5AE9EE78EB0-7141-底层实现7141-底层实现)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-14-2-%E8%87%AA%E5%AE%9A%E4%B9%89%E5%87%AD%E6%8D%AE%E7%BC%93%E5%AD%98 "7.14.2 自定义凭据缓存")7.14.2 自定义凭据缓存](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git7-14-2-E887AAE5AE9AE4B989E587ADE68DAEE7BC93E5AD98-7142-自定义凭据缓存7142-自定义凭据缓存)
- [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch08-%E8%87%AA%E5%AE%9A%E4%B9%89git "ch08 自定义git")ch08 自定义git](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitch08-E887AAE5AE9AE4B989git-ch08-自定义gitch08-自定义git)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-%E9%85%8D%E7%BD%AEgit "8.1 配置git")8.1 配置git](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-1-E9858DE7BDAEgit-81-配置git81-配置git)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-1-%E5%9F%BA%E6%9C%AC%E9%85%8D%E7%BD%AE "8.1.1 基本配置")8.1.1 基本配置](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-1-1-E59FBAE69CACE9858DE7BDAE-811-基本配置811-基本配置)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-2-%E8%87%AA%E5%AE%9A%E4%B9%89%E9%85%8D%E8%89%B2 "8.1.2 自定义配色")8.1.2 自定义配色](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-1-2-E887AAE5AE9AE4B989E9858DE889B2-812-自定义配色812-自定义配色)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-3-%E5%A4%96%E9%83%A8%E7%9A%84%E5%90%88%E5%B9%B6%E4%B8%8Ediff%E5%B7%A5%E5%85%B7 "8.1.3 外部的合并与diff工具")8.1.3 外部的合并与diff工具](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-1-3-E5A496E983A8E79A84E59088E5B9B6E4B88EdiffE5B7A5E585B7-813-外部的合并与diff工具813-外部的合并与diff工具)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-4-%E6%A0%BC%E5%BC%8F%E5%8C%96%E4%B8%8E%E7%A9%BA%E7%99%BD%E5%AD%97%E7%AC%A6 "8.1.4 格式化与空白字符")8.1.4 格式化与空白字符](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-1-4-E6A0BCE5BC8FE58C96E4B88EE7A9BAE799BDE5AD97E7ACA6-814-格式化与空白字符814-格式化与空白字符)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-5-%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%85%8D%E7%BD%AE "8.1.5 服务器配置")8.1.5 服务器配置](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-1-5-E69C8DE58AA1E599A8E9858DE7BDAE-815-服务器配置815-服务器配置)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-git%E5%B1%9E%E6%80%A7 "8.2 git属性")8.2 git属性](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-2-gitE5B19EE680A7-82-git属性82-git属性)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-1-%E4%BA%8C%E8%BF%9B%E5%88%B6%E6%96%87%E4%BB%B6 "8.2.1 二进制文件")8.2.1 二进制文件](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-2-1-E4BA8CE8BF9BE588B6E69687E4BBB6-821-二进制文件821-二进制文件)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-2-%E5%85%B3%E9%94%AE%E5%AD%97%E6%89%A9%E5%B1%95 "8.2.2 关键字扩展")8.2.2 关键字扩展](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-2-2-E585B3E994AEE5AD97E689A9E5B195-822-关键字扩展822-关键字扩展)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-3-%E6%9C%892%E4%B8%AA%E5%B1%9E%E6%80%A7%E7%94%A8%E4%BA%8Egit-archive "8.2.3 有2个属性用于git archive")8.2.3 有2个属性用于git archive](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-2-3-E69C892E4B8AAE5B19EE680A7E794A8E4BA8Egit-archive-823-有2个属性用于git-archive823-有2个属性用于git-archive)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-4-%E5%90%88%E5%B9%B6%E6%97%B6%E5%BF%BD%E7%95%A5%E7%89%B9%E6%80%A7%E5%88%86%E6%94%AF%E7%9A%84%E5%8F%98%E6%9B%B4 "8.2.4 合并时忽略特性分支的变更")8.2.4 合并时忽略特性分支的变更](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-2-4-E59088E5B9B6E697B6E5BFBDE795A5E789B9E680A7E58886E694AFE79A84E58F98E69BB4-824-合并时忽略特性分支的变更824-合并时忽略特性分支的变更)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-3-%E9%92%A9%E5%AD%90 "8.3 钩子")8.3 钩子](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-3-E992A9E5AD90-83-钩子83-钩子)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-3-1-%E5%AE%89%E8%A3%85%E9%92%A9%E5%AD%90 "8.3.1 安装钩子")8.3.1 安装钩子](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-3-1-E5AE89E8A385E992A9E5AD90-831-安装钩子831-安装钩子)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-3-2-%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%92%A9%E5%AD%90 "8.3.2 客户端钩子")8.3.2 客户端钩子](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-3-2-E5AEA2E688B7E7ABAFE992A9E5AD90-832-客户端钩子832-客户端钩子)
      - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%8F%90%E4%BA%A4%E5%B7%A5%E4%BD%9C%E6%B5%81%E9%92%A9%E5%AD%90 "提交工作流钩子")提交工作流钩子](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE68F90E4BAA4E5B7A5E4BD9CE6B581E992A9E5AD90-提交工作流钩子提交工作流钩子)
      - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E5%9F%BA%E4%BA%8E%E7%94%B5%E5%AD%90%E9%82%AE%E4%BB%B6%E7%9A%843%E4%B8%AA%E9%92%A9%E5%AD%90%E9%83%BD%E6%98%AF%E7%94%B1git-am%E8%B0%83%E7%94%A8%E7%9A%84 "基于电子邮件的3个钩子都是由git am调用的")基于电子邮件的3个钩子都是由git am调用的](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE59FBAE4BA8EE794B5E5AD90E982AEE4BBB6E79A843E4B8AAE992A9E5AD90E983BDE698AFE794B1git-amE8B083E794A8E79A84-基于电子邮件的3个钩子都是由git-am调用的基于电子邮件的3个钩子都是由git-am调用的)
      - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E5%85%B6%E4%BB%96%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%92%A9%E5%AD%90 "其他客户端钩子")其他客户端钩子](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE585B6E4BB96E5AEA2E688B7E7ABAFE992A9E5AD90-其他客户端钩子其他客户端钩子)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-3-3-%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E9%92%A9%E5%AD%90 "8.3.3 服务器端钩子")8.3.3 服务器端钩子](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git8-3-3-E69C8DE58AA1E599A8E7ABAFE992A9E5AD90-833-服务器端钩子833-服务器端钩子)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#git%E5%BC%BA%E5%88%B6%E7%AD%96%E7%95%A5%E7%A4%BA%E4%BE%8B "git强制策略示例")git强制策略示例](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitgitE5BCBAE588B6E7AD96E795A5E7A4BAE4BE8B-git强制策略示例git强制策略示例)
- [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch09-git%E4%B8%8E%E5%85%B6%E4%BB%96%E7%B3%BB%E7%BB%9F "ch09 git与其他系统")ch09 git与其他系统](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitch09-gitE4B88EE585B6E4BB96E7B3BBE7BB9F-ch09-git与其他系统ch09-git与其他系统)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#9-1-1-git-svn%E4%B8%8ESubversion%E5%8F%8C%E5%90%91%E6%A1%A5%E6%8E%A5 "9.1.1 git svn与Subversion双向桥接")9.1.1 git svn与Subversion双向桥接](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git9-1-1-git-svnE4B88ESubversionE58F8CE59091E6A1A5E68EA5-911-git-svn与Subversion双向桥接911-git-svn与Subversion双向桥接)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#9-2-5-%E8%87%AA%E5%AE%9A%E4%B9%89%E5%AF%BC%E5%85%A5%E5%B7%A5%E5%85%B7 "9.2.5 自定义导入工具")9.2.5 自定义导入工具](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git9-2-5-E887AAE5AE9AE4B989E5AFBCE585A5E5B7A5E585B7-925-自定义导入工具925-自定义导入工具)
- [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch10-git%E5%86%85%E5%B9%95 "ch10 git内幕")ch10 git内幕](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitch10-gitE58685E5B995-ch10-git内幕ch10-git内幕)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-1-%E5%BA%95%E5%B1%82%E5%91%BD%E4%BB%A4%E5%92%8C%E9%AB%98%E5%B1%82%E5%91%BD%E4%BB%A4 "10.1 底层命令和高层命令")10.1 底层命令和高层命令](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-1-E5BA95E5B182E591BDE4BBA4E5928CE9AB98E5B182E591BDE4BBA4-101-底层命令和高层命令101-底层命令和高层命令)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-2-git%E5%AF%B9%E8%B1%A1 "10.2 git对象")10.2 git对象](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-2-gitE5AFB9E8B1A1-102-git对象102-git对象)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-2-1-%E6%A0%91%E5%AF%B9%E8%B1%A1 "10.2.1 树对象")10.2.1 树对象](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-2-1-E6A091E5AFB9E8B1A1-1021-树对象1021-树对象)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-2-2-%E6%8F%90%E4%BA%A4%E5%AF%B9%E8%B1%A1 "10.2.2 提交对象")10.2.2 提交对象](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-2-2-E68F90E4BAA4E5AFB9E8B1A1-1022-提交对象1022-提交对象)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-2-3-%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8 "10.2.3 对象存储")10.2.3 对象存储](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-2-3-E5AFB9E8B1A1E5AD98E582A8-1023-对象存储1023-对象存储)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-3-git%E5%BC%95%E7%94%A8 "10.3 git引用")10.3 git引用](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-3-gitE5BC95E794A8-103-git引用103-git引用)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E5%8C%85%E6%96%87%E4%BB%B6 "包文件")包文件](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE58C85E69687E4BBB6-包文件包文件)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-5-%E5%BC%95%E7%94%A8%E8%A7%84%E6%A0%BC "10.5 引用规格")10.5 引用规格](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-5-E5BC95E794A8E8A784E6A0BC-105-引用规格105-引用规格)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-6-git%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE "10.6 git传输协议")10.6 git传输协议](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-6-gitE4BCA0E8BE93E58D8FE8AEAE-106-git传输协议106-git传输协议)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-6-1-%E5%93%91%E5%8D%8F%E8%AE%AE "10.6.1 哑协议")10.6.1 哑协议](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-6-1-E59391E58D8FE8AEAE-1061-哑协议1061-哑协议)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-6-2-%E6%99%BA%E8%83%BD%E5%8D%8F%E8%AE%AE "10.6.2 智能协议")10.6.2 智能协议](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-6-2-E699BAE883BDE58D8FE8AEAE-1062-智能协议1062-智能协议)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-7-%E7%BB%B4%E6%8A%A4%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D "10.7 维护与数据恢复")10.7 维护与数据恢复](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-7-E7BBB4E68AA4E4B88EE695B0E68DAEE681A2E5A48D-107-维护与数据恢复107-维护与数据恢复)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E7%BB%B4%E6%8A%A4 "维护")维护](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE7BBB4E68AA4-维护维护)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-7-2-%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D "10.7.2 数据恢复")10.7.2 数据恢复](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-7-2-E695B0E68DAEE681A2E5A48D-1072-数据恢复1072-数据恢复)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E7%A7%BB%E9%99%A4%E5%A4%A7%E5%AF%B9%E8%B1%A1 "移除大对象")移除大对象](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE7A7BBE999A4E5A4A7E5AFB9E8B1A1-移除大对象移除大对象)
      - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E9%A6%96%E5%85%88%E6%89%BE%E5%88%B0%E5%93%AA%E4%BA%9B%E6%96%87%E4%BB%B6%E8%BE%83%E5%A4%A7 "首先找到哪些文件较大")首先找到哪些文件较大](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE9A696E58588E689BEE588B0E593AAE4BA9BE69687E4BBB6E8BE83E5A4A7-首先找到哪些文件较大首先找到哪些文件较大)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%9F%A5%E7%9C%8B%E5%93%AA%E4%BA%9B%E6%8F%90%E4%BA%A4%E4%BF%AE%E6%94%B9%E4%BA%86%E8%AF%A5%E5%A4%A7%E6%96%87%E4%BB%B6 "查看哪些提交修改了该大文件")查看哪些提交修改了该大文件](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE69FA5E79C8BE593AAE4BA9BE68F90E4BAA4E4BFAEE694B9E4BA86E8AFA5E5A4A7E69687E4BBB6-查看哪些提交修改了该大文件查看哪些提交修改了该大文件)
      - [\[\](http://bj.apso.cn/2022/06/14/2022-06-14-jing-tong-git/#%E7%A7%BB%E9%99%A4 "移除")移除](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitE7A7BBE999A4-移除移除)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-8-%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F "10.8 环境变量")10.8 环境变量](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-8-E78EAFE5A283E58F98E9878F-108-环境变量108-环境变量)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-8-2-%E4%BB%93%E5%BA%93%E4%BD%8D%E7%BD%AE "10.8.2 仓库位置")10.8.2 仓库位置](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-8-2-E4BB93E5BA93E4BD8DE7BDAE-1082-仓库位置1082-仓库位置)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-8-5-%E7%BD%91%E7%BB%9C "10.8.5 网络")10.8.5 网络](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-8-5-E7BD91E7BB9C-1085-网络1085-网络)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-8-7-%E8%B0%83%E8%AF%95 "10.8.7 调试")10.8.7 调试](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-8-7-E8B083E8AF95-1087-调试1087-调试)
    - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-8-8-%E6%9D%82%E9%A1%B9 "10.8.8 杂项")10.8.8 杂项](#httpbjapsonic-motocn202206142022-06-14-jing-tong-git10-8-8-E69D82E9A1B9-1088-杂项1088-杂项)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#A-6-powershell "A.6 powershell")A.6 powershell](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitA-6-powershell-A6-powershellA6-powershell)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#B-%E5%9C%A8%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E4%B8%AD%E5%B5%8C%E5%85%A5git "B 在应用程序中嵌入git")B 在应用程序中嵌入git](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitB-E59CA8E5BA94E794A8E7A88BE5BA8FE4B8ADE5B58CE585A5git-B-在应用程序中嵌入gitB-在应用程序中嵌入git)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#C-2-2-clone "C.2.2 clone")C.2.2 clone](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitC-2-2-clone-C22-cloneC22-clone)
  - [\[\](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#C-3-3-diff "C.3.3 diff")C.3.3 diff](#httpbjapsonic-motocn202206142022-06-14-jing-tong-gitC-3-3-diff-C33-diffC33-diff)

## 3.5 远程分支

如果不想每次推送时都键入密码，可以设置一个凭据缓存（credential cache）。请参阅[7.14节](http://bj.apsonic-moto.cn/2022/06/16-14-jing-tong-git/#凭据存储 "7.14节")

`git branch -vv`列出每个分支的名字及其跟踪的远程分支信息，以及领先或落后的信息。要注意的是，这条命令和`git status`都不会与服务器通信以获取最新信息。

# ch04

如果你对自己运行git服务器不感兴趣，可以跳过本章的前面几节，直接阅读4.9节。

## 4.1 协议

### 4.1.1 本地协议

使用file://前缀的主要原因是希望取出仓库中的外部引用或多余对象。

### 4.1
智能HTTP协议最普遍。既支持匿名访问，也支持用户验证。

### 4.1.3 SSH协议

SSH不能实现匿名访问

### 4.1.4 git协议

git协议不提供任何身份验证方式

## 4.2 在服务器上搭建git

### 4.2.1 将裸仓库放置在服务器上

如果你只需要与几个人协作完成一个私有项目，那么只需要SSH服务器和裸仓库就够了

### 4.2.2 小型团队配置

配置git服务器时最麻烦的一个方面就是用户管理

## 4.3 生成个人的ssh公钥

让git服务器的管理员把公钥添加到git用户的`~/.ssh/authorized_keys`文件中即可访问

## 4.4 设置服务器

每次创建新项目时，都需要有人通过SSH方式登录该服务器并创建一个新的裸仓库

如果该服务器搭建在内网，并且已经配置好DNS，使得gitserver指向该服务器，那么你就可以直接克隆`git@gitserver:/srv/git/project.git`

## 4.5 git守护进程

无需授权，提供公开项目的访问

## 4.6 智能HTTP

git自带一个叫做git-http-backend的CGI脚本，你可以调用它来实现通过HTTP协议发送和接收数据

## 4.7 GitWeb

在Linux上lighttpd一般都已经装好，可以直接在项目目录下执行`git instaweb`来通过web展示git项目和数据

## 4.8 GitLab

每个项目都归属于单个命名空间

1. 用户命名空间
2. 组命名空间

钩子会触发HTTP POST操作，其中携带的描述性信息采用的是JSON格式。以便自动化

# ch05

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14/#5-1-%E5%88%86%E5%B8%83%E5%BC%8F%E5%B7%A5%E4%BD%9C%E6%B5%81> "5.1 分布式工作流")5.1 分布式工作流

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-1-1-%E9%9B%86%E4%B8%AD%E5%BC%8F%E5%B7%A5%E4%BD%9C%E6%B5%81> "5.1.1 集中式工作流")5.1.1 集中式工作流

中枢接受代码，所有人以此同步各自的工作

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-1-2-%E9%9B%86%E6%88%90%E7%AE%A1%E7%90%86%E8%80%85%E5%B7%A5%E4%BD%9C%E6%B5%81> "集成管理者工作流")5.1.2 集成管理者工作流

开发人员fork，集成管理者处理pull request

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-1-3-%E5%8F%B8%E4%BB%A4%E5%AE%98%E4%B8%8E%E5%89%AF%E5%AE%98%E5%B7%A5%E4%BD%9C%E6%B5%81> "5.1.3 司令官与副官工作流")5.1.3 司令官与副官工作流

用于Linux内核等等超大型项目或高度层次化环境。

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-2-%E4%B8%BA%E9%A1%B9%E7%9BE5%81%9A%E8%B4%A1%E7%8C%AE> "5.2 为项目做贡献")5.2 为项目做贡献

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-2-1-%E6%8F%90%E4%BA%A4%E5%87%86%E5%88%99> "5.2.1 提交准则")5.2.1 提交准则

提交之前执行`git diff --check`列出可能存在的空白字符错误

提交消息的第一行不应该超过50个字符

### 5.2.4 用`rebase -i`将工作内容压缩成单个提交可能会方便维护人员评审补丁。

CF：[7.6节](http://bj.apsonic-moto.cn/2022022-06-14-jing-tong-git/#重写历史 "7.6节")会对交互式变基做更详尽的介绍。

### 5.2.5 用`git format-patch`来生成要通过电子邮件发送的mbox格式的文件

用`git send-email`之前需要配置

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E7%A1%AE%E5%AE%9A%E5%BC%95%E5%85%A5%E5%86%85%E5%AE%B9> "确定引入内容")确定引入内容

CF：[7.1 选择修订版本](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#选择修订版本 "7.1 é log master..contrib`显示在contrib中但不在master中的提交三点语法：`git diff master...contrib`显示contrib与master分岔后的diff

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-3-5-%E5%A4%A7%E5%9E%8B%E5%90%88%E5%B9%B6%E5%B7%A5%E4%BD%9C%E6%B5%81> "5.3.5 大型合并工作流")5.3.5 大型合并工作流

将主题分支合并到next并推送共享，如果主题分支仍需改进则合并到pu分支，稳定下来后重新和并入master。这意味着masterå偶尔变基，pu频繁变基。maint用于提供向后移植补丁。

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#5-3-9-%E6%B1%87%E6%80%BB%E8%87%AAv1-1-1%E4%B9%8B%E5%90%8E%E6%89%80%E6%9C%89%E6%8F%90%E4%BA%A4> "5.3.9 汇总自v1.1.1之后所有提交")5.3.9 汇总自v1.1.1之后所有提交

`git shortlog --no-merges master --not v1.1.1`

# \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch06> "ch06")ch06

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/202ong-git/#6-3-2-%E6%B7%BB%E5%8A%A0%E5%8D%8F%E4%BD%9C%E4%BA%BA%E5%91%98%EF%BC%9ACollaborators> "6.3.2 添加协作人员：Collaborators")6.3.2 添加协作人员：Collaborators

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#6-5-GitHub%E8%84%9A%E6%9C%AC%E5%8C%96> "6.5 GitHub脚本化")6.5 GitHub脚本化

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#6-5-1-%E9%92%A9%E5%AD%90%E7%B3%BB%E7%BB%9F> "6.5.1 钩子系统")6.5.1 钩子系统

### \[]\(<http://bj.apto.cn/2022/06/14/2022-06-14-jing-tong-git/#6-5-2-GitHub-API> "6.5.2 GitHub API")6.5.2 GitHub API

# \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch07> "ch07")ch07

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E9%80%89%E6%8B%A9%E4%BF%AE%E8%AE%A2%E7%89%88%E6%9C%AC> "选择修订版本")选择修订版本

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%98%BE%E7%A4%BA%E5%87%BA%E6%8F%90%E4%BA%A4%E5%B1%9E%E4%BA%8E%E5%93%AA%E4%B8%80%%E7%9A%84%E5%88%86%E6%94%AF> "显示出提交属于哪一侧的分支")显示出提交属于哪一侧的分支

`git log --left-right master...experiment`。CF：[5.3.4 确定引入内容](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#确定引入内容 "5.3.4 确定引入内容")

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-3-%E5%82%A8%E8%97%8F> "7.3 储藏")7.3 储藏

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-3-3-%E4%BB%8E%E5A8%E8%97%8F%E4%B8%AD%E5%88%9B%E5%BB%BA%E5%88%86%E6%94%AF> "7.3.3 从储藏中创建分支")7.3.3 从储藏中创建分支

`git stash branch 新分支名`

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%B8%85%E7%90%86%E5%B7%A5%E4%BD%9C%E7%9B%AE%E5%BD%95> "清理工作目录")清理工作目录

- `git stash -all`以储藏形式保存全部内容
- `git clean -n`做一次删除的演习
- `git clean -f`进行实际删除

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-ng-tong-git/#7-5-%E6%90%9C%E7%B4%A2> "7.5 搜索")7.5 搜索

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-5-1-%E5%B7%A5%E4%BD%9C%E7%9B%AE%E5%BD%95%E6%90%9C%E7%B4%A2> "7.5.1 工作目录搜索")7.5.1 工作目录搜索

- `git grep 模式`默认只查找工作目录下的文件
- `git grep --count 模式`输出总结信息：每个匹配的文件中有多少处匹配
- `git grep -p 模式`显示所查找到的匹配属于哪个方法或函数

还可以使用–and选项来查æ### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-5-2-%E6%97%A5%E5%BF%97%E6%90%9C%E7%B4%A2> "7.5.2 日志搜索")7.5.2 日志搜索

- `git log -S 字符串`显示出添加过或删除过该字符串的那些提交
- `git log -G 模式`等同于-S但使用正则表达式进行模式匹配
- `git log -L 模式:文件`显示所有匹配的改动记录

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E9%87%8D%E5%86%99%E5%8E%86%E5%8F%B2> "重写历史")重写åttp://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-6-3-%E9%87%8D%E6%8E%92%E6%8F%90%E4%BA%A4%EF%BC%9A%E5%9C%A8%E4%BA%A4%E4%BA%92%E5%BC%8F%E5%8F%98%E5%9F%BA%E4%B8%AD%E6%94%B9%E5%8F%98%E8%A1%8C%E7%9A%84%E9%A1%BA%E5%BA%8F> "7.6.3 重排提交：在交互式变基中改变行的顺序")7.6.3 重排提交：在交互式变基中改变行的顺序

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-6-4-%E5%8E%8B%E7%BC%A9%E6%8F%90%E4%BA%A4%EF%BC%9A%E5%9C%A8%E4%BA%A4%E4%BA%92%EE5%8F%98%E5%9F%BA%E4%B8%AD%E7%94%A8squash> "7.6.4 压缩提交：在交互式变基中用squash")7.6.4 压缩提交：在交互式变基中用squash

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-6-5-%E6%8B%86%E5%88%86%E6%8F%90%E4%BA%A4%EF%BC%9A%E5%9C%A8%E4%BA%A4%E4%BA%92%E5%BC%8F%E5%8F%98%E5%9F%BA%E4%B8%AD%E7%94%A8edit> "7.6.5 拆分提交：在交互式变基中用edit")7.6.5 拆分提交：在交互式变基中用edit

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14ng-git/#7-6-6-%E8%B6%85%E5%BC%BA%E5%91%BD%E4%BB%A4%EF%BC%9Afilter-branch> "7.6.6 超强命令：filter-branch")7.6.6 超强命令：filter-branch

1. 从所有提交中删除某个文件：`git filter-branch --tree-filter 'rm -f 文件' HEAD`。要想在所有分支上执行filter-branch，可以传入–all选项
2. 将子目录设置为新的根目录：`git filter-branch --subdirectory-filter 目录 HEAD`
3. 全面修改邮件地址：利用shell中的if语句配合GIT\_AUTHOR环境变量

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E7%A7%98%EF%BC%9Areset%E5%92%8Ccheckout> "7.7 重置揭秘：reset和checkout")7.7 重置揭秘：reset和checkout

### 7.7.5 要压缩最新的几个提交，只需`git reset --soft 旧提交`然后commit

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-7-7-%E6%96%87%E4%BB%B6%E7%BA%A7%E5%88%AB%E4%B8%8E%E6%8F%90%E4%BA%A4%E7%BA%A7%E5%88%AB> "7.7.7 文件级别与提交级别")7.7.7 文件级å
|                      | 索引 | 工作目录 | 覆盖是否安全 |
| -------------------- | -- | ---- | ------ |
| 提交级别                 |    |      |        |
| reset –soft COMMIT   |    |      |        |
| reset –mixed COMMIT  |    |      |        |
| reset –hard COMMIT   |    |      |        |
| checkout COMMIT      |    |      |        |
| 文件级别                 |    |      |        |
| reset COMMIT FILE    |    |      |        |
| checkout COMMIT FILE |    |      |        |

###bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-8-1-%E5%90%88%E5%B9%B6%E5%86%B2%E7%AA%81> "7.8.1 合并冲突")7.8.1 合并冲突

- `git merge -Xignore-all-space`忽略空白字符的变更
- `git checkout --conflict=diff3 冲突文件名`在冲突标记中提供内嵌的base版本
- `git checkout`还可以接受–ours和–theirs作为选项，这是一种只选择其中一侧的快速方法。

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-8-2-%E8%BF%98%E5%8E%9F%E6F%90%E4%BA%A4> "7.8.2 还原提交")7.8.2 还原提交

对合并提交执行`git revert`需要用-m选项指明要还原哪个父节点引入的变更

如果使用`git revert -m 1 HEAD`来抵消合并，会影响这两个分支以后的合并基础

### 7.8.3 `-Xours`与`-s ours`

给merge传入-Xours或-Xtheirs选项就不再添加冲突标记。任何能够合并的差异，git会选择合并。任何有冲突的差异，git会简单地选择你所指定的那一侧。

更严格的策略是`-s ours`。一次假合并。它会记录一个

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E5%AD%90%E6%A0%91%E5%90%88%E5%B9%B6> "子树合并")子树合并

git能够聪明地发现一个子目录是另一个的子树

这给我们提供了一种方法，可以在不使用子模块的情况下拥有一种类似于子模块流程的工作方式。其不足之处在于略有些复杂，容易出现操作错误

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-9-reere")7.9 rerere

在有些情况下，重用冲突解决方案相当方便。例如：

- 想确保一个长期的topic分支能够干净地合并，但又不想要一堆用于**中间阶段**的合并提交。你可以启动rerere功能，偶尔进行合并、解决冲突、**然后退出合并**。如果你一直这么做，那么最终的合并应该会很容易。变基也同理
- 选用一个已合并的分支，修复了一堆冲突后决定对其进行变基操作，这样你可能就不必再去解å偶尔将多个尚在改进的topic分支合并到一个可测试的头部。如果测试失败，你可以返回合并之前，不使用导致失败的topic分支，然后再次合并，无需再次重新解决冲突。

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-10-%E4%BD%BF%E7%94%A8git%E8%B0%83%E8%AF%95> "7.10 使用git调试")7.10 使用git调试

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-10-1-%E6%96%87%E4%BB%B6%E6%A0%87%E6%B3%A8> "7.10.1.1 文件标注

`git blame -L 起始行,结束行 文件`查看每一行的最后一次修改者和修改时间

加入-C参数要求git找出代码移动的原始出处

### 7.10.2 `git bisect`帮助尽快确定问题是由那、哪一次提交引发的

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-%E5%AD%90%E6%A8%A1%E5%9D%97> "7.11 子模块")7.11 子模块

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-1-%E5%BC%80%E5%A7%8B%E4%BD%BF%E7%94%A85%AD%90%E6%A8%A1%E5%9D%97> "7.11.1 开始使用子模块")7.11.1 开始使用子模块

在已有的git仓库中执行`git submodule add https://github.com/chaconinc/DbConnector`会将子项目放入DbConnector文件夹中；还会自动在.gitmodules保存url与路径的映射关系

因为其他用户会首先尝试从.gitmodules文件中的url处进行克隆/获取，所以要确保大家都能访问到该url。如果你用来推送的url和别人拉取时用的url不一样，那么换一个别人能够è§行`git config submodule.DbConnector.url PRIVATE_URL`来覆盖这个值，以供自己使用。如果可以，采用相对路径是一个不错的选择

执行`git diff --cached DbConnector`会发现git并不会跟踪其中的内容，而是把它看作仓库中的一次特殊的提交。

如果你希望diff的输出美观一些，可以给`git diff`传入`--submodule`选项。如果不想在每次执行`git diff`时都键入`--submodule`，可以设置`git config --global diff.submodule log`

在提äode 160000 DbConnector`。模式为160000的rack条目表示你将一次提交作为一个目录项（而非子目录或文件）进行记录

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-2-%E5%85%8B%E9%9A%86%E5%90%AB%E6%9C%89%E5%AD%90%E6%A8%A1%E5%9D%97%E7%9A%84%E9%A1%B9%E7%9B%AE> "7.11.2 克隆含有子模块的项目")7.11.2 克隆含有子模块的项目

克隆时，默认会得到含有子模块的目录，但是目录中并没有文件。你必须分别执行两条命odule init 用于初始化本地配置文件
2. git submodule update 用于从项目中获取所有数据并检出父项目中适合的提交

更简单的做法是在clone时传入`--recursive`选项

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-3-%E5%BC%80%E5%8F%91%E5%90%AB%E6%9C%89%E5%AD%90%E6%A8%A1%E5%9D%97%E7%9A%84%E9%A1%B9%E7%9B%AE> "7.11.3 开发含有子模块的项目")7.11.3 开发含有子模块的项目

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-g-git/#%E6%8B%89%E5%8F%96%E4%B8%8A%E6%B8%B8%E5%8F%98%E6%9B%B4> "拉取上游变更")拉取上游变更

进入DbConnector目录执行fetch和merge

返回主项目执行`git diff --submodule`就会看到子模块已经得到了更新

更简单的做法是执行`git submodule update --remote`自动更新所有子模块。该命令默认会假定你要将检出更新为子模块仓库的master分支。可以在两个地方修改

1. `git config -f .gitmodules submodule.DbConnector.branch stable`修改.gitmod以跟踪到）
2. 去掉选项`-f .gitmodules`将只修改本地的`.git/config`，只对你有效

**跳过复杂操作**

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-4-foreach%E4%B8%8E%E5%88%AB%E5%90%8D> "7.11.4 foreach与别名")7.11.4 foreach与别名

`git submodule foreach 'git diff'`

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-11-5-%E5%AD%90%E6%A8%A1%E5%9D%97%E7%9A%84%E9%97%AE%E9%A2%98> "7.11.5 子模块的问题")7.11.5 子模块的é 入子模块后切换回没有子模块的分支B，会留下一个未被跟踪的子模块目录。

如果删除该目录，然后切换回分支A，需要执行`submodule update --init`来重新填充

另一个要重点注意的地方涉及从子目录到子模块的切换

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-12-%E6%89%93%E5%8C%85> "7.12 打包")7.12 打包

`git bundle create repo.bundle HEAD master`创建的repo.bundle文件包含了重建仓库master分支所éone repo.bundle repo`可以从二进制文件克隆到一个目录中。如果在create时没有在引用中包含HEAD，那还得指定`-b master`或者其他被引入的分支

也可以只打包部分提交，与format-patch的区别在于只生成一个文件

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-13-%E6%9B%BF%E6%8D%A2> "7.13 替换")7.13 替换

历史记录拆分后可用replace重新嫁接

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%8D%AE%E5%AD%98%E5%82%A8> "凭据存储")凭据存储

git凭据系统提供的选项

1. 默认不缓存任何内容。所有连接都会提醒你输入输入用户名和密码
2. cache模式会将凭据保存在内存15分钟，绝不会将密码存储在磁盘上。
3. store模式将凭据保存在磁盘上的纯文本文件中，且永不过期。
4. Mac还有osxkeychain模式，会把凭据以加密形式存放在磁盘上
5. Win可以安装`Git Credential Manager for Windows`使用`Windows Credential S敏感信息

`git config --global credential.helper cache --timeout 30000`设置将凭据保存在内存中约8小时

`git config --global credential.helper store --file 路径`设置将凭据保存在硬盘

如果你的凭据文件保存在u盘上，希望在没有插入u盘的时候使用内存缓存来保存凭据。那么.gitconfig看起来如下所示

|                   |                                                                                                                   |
| --------- | ----------------------------------------------------------------------------------------------------------------- |
| 1  
2  
3 | \[credential]  
 helper = store --file /mnt/thumbdrive/.git-credentials  
 helper = cache --timeout 30000 |

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-14-1-%E5%BA%95%E5%B1%82%E5%AE%9E%E7%8E%B0> "7.14.1 底层实现")7.14.1 底层实现

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#7-14-2-%E8%87%AA%E5%AE%9A%E4%B9%89%E5%87%AD%E6%8D%AE%E7%BC%93%E5%AD%98> "7.14.2 自定义凭据缓存")7.14.2 自定义凭据缓存

# \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch08-%E8%87%AA%E5%AE%9A%E4%B9%89git> "ch08 自定义git")ch08 自定义git

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-%E9%85%8D%E7%BD%AEgit> "8.1 配置git")8.1 配置git

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-1-%E5%9F%BA%E6%9C%AC%E9%85%8D%E7%BD%AE> "8.1.1 基本配置")配置

`git config --global commit.template ~/.gitmessage.txt`设置默认的提交消息占位符

如果你要创建签署过的附注标签（在7.4节中讨论过），那么将你的GPG签署密钥作为配置项设置会更方便。进行下述设置以后再签署标签时只需`git tag -s <tag-name>`

`git config --global user.signingkey <gpg-key-id>`

core.excludesfile可用于设置系统级ignore

将help.autocorrect设置为1可以在输错命令时将git推测出的命令自动执行；将其è 正命令前给你留出5秒钟的考虑时间

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-2-%E8%87%AA%E5%AE%9A%E4%B9%89%E9%85%8D%E8%89%B2> "8.1.2 自定义配色")8.1.2 自定义配色

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-3-%E5%A4%96%E9%83%A8%E7%9A%84%E5%90%88%E5%B9%B6%E4%B8%8Ediff%E5%B7%A5%E5%85%B7> "8.1.3 外部的合并与diff工具")8.1.3 外部的合并与diff工具

`git config --global merge.tool kdiff3`

### \[]\(<http://psonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-4-%E6%A0%BC%E5%BC%8F%E5%8C%96%E4%B8%8E%E7%A9%BA%E7%99%BD%E5%AD%97%E7%AC%A6> "8.1.4 格式化与空白字符")8.1.4 格式化与空白字符

1. core.autocrlf 处理行终止符。win适合把它置为true，unix适合把它置为input。
2. core.whitespace 用于检测、修正与空白字符相关的问题

- （默认）blank-at-eol 会查找行尾的空格
- （默认）blank-at-eof 会查看文件末尾的空行
- （默认）space-before-tab 会æ
1. 如果提交了存在空白字符问题的文件，可以执行`git rebase --whitespace=fix`自动修复

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-1-5-%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%85%8D%E7%BD%AE> "8.1.5 服务器配置")8.1.5 服务器配置

设置`git config --system receive.fsckObjects true`能够确认在推送过程中接收到的每一个对象的有效性以及是否匹配其SHA-1校验和。但代价太高，有可能拖慢其他操作，尤其是在处理大。

设置`git config --system receive.denyNonFastForwards true`可以拒绝`push -f`。另一种实现方法是通过服务器端的接收钩子，能够让你完成一些更复杂的操作

有一种方法可以绕开denyNonFastForwards：先删除分支然后再推送。为了避免这种情况，可以将receive.denyDeletes设置为true禁止删除远程分支

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-git%E5%B1%9E%E6%80%A7> "8.2 git属性")8.2 git属性

针对路径ç你不希望将属性文件连同项目一起提交，也可以在.git/info/atttibutes文件中设置

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-1-%E4%BA%8C%E8%BF%9B%E5%88%B6%E6%96%87%E4%BB%B6> "8.2.1 二进制文件")8.2.1 二进制文件

1. `*.pbxproj binary`告诉git把后缀为.pbxproj的文件当做二进制文件来处理
2. 比较二进制文件

- `*.docx diff=word`配合`git config diff.word.textconv docx2txt`可比较word文件的文字改动
- `*.png diff=ext config diff.exif.textconv exiftool`可比较图像的元信息

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-2-%E5%85%B3%E9%94%AE%E5%AD%97%E6%89%A9%E5%B1%95> "8.2.2 关键字扩展")8.2.2 关键字扩展

`*.txt ident`让git在检出时将blob对象的SHA-1写入$Id$字段。用途有限

可以编写自己的smudge和clean后，在文件检出时会运行smudge过滤器，在文件暂存时会运行clean过滤器

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-3-%E6%9C%892%E4%B8%AA%E5%B1%9E%E6%80%A7%E7%94%A8%E4%BA%8Egit-archive> "8.2.3 有2个属性用于git archive")8.2.3 有2个属性用于git archive

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-2-4-%E5%90%88%E5%B9%B6%E6%97%B6%E5%BF%BD%E7%95%A5%E7%89%B9%E6%80%A7%E5%88%86%E6%94%AF%E7%9A%84%E5%8F%98%E6%9B%B4> "8.2.4 合并时忽略特性分支的变更")8.2.4 合并时忽略特性分支的变更

设置`git config --global merge.ours.driver true`并添加属性`db.rge=ours`可以让db.xml文件不受特性分支影响

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-3-%E9%92%A9%E5%AD%90> "8.3 钩子")8.3 钩子

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-3-1-%E5%AE%89%E8%A3%85%E9%92%A9%E5%AD%90> "8.3.1 安装钩子")8.3.1 安装钩子

想启用一个钩子脚本，需要将不含.sample后缀的可执行文件放入.git/hooks

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-3-2-%E5%2%E6%88%B7%E7%AB%AF%E9%92%A9%E5%AD%90> "8.3.2 客户端钩子")8.3.2 客户端钩子

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%8F%90%E4%BA%A4%E5%B7%A5%E4%BD%9C%E6%B5%81%E9%92%A9%E5%AD%90> "提交工作流钩子")提交工作流钩子

1. pre-commit钩子在键入提交消息前运行。如果以非零值退出，提交会被中止，但可以使用`git commit --no-verify`来绕过这个环节
2. prapare-commit-msg钩子的运行时机是在提交消息编辑器启动之å后。它接受一个路径参数，指向用户编写的提交信息。在8.4节有示例。一般用于 那些自动生成默认消息的提交。如

- 提交消息模板
- 合并提交
- 压缩提交
- 修正提交

1. commit-msg钩子用于在提交通过前验证项目状态或提交信息。在[8.4节](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#git强制策略示例 "8.4节")演示
2. post-commit钩子在提交结束后运行，通常用于通知

#### \[]\(<http://bj.apsonic-m06/14/2022-06-14-jing-tong-git/#%E5%9F%BA%E4%BA%8E%E7%94%B5%E5%AD%90%E9%82%AE%E4%BB%B6%E7%9A%843%E4%B8%AA%E9%92%A9%E5%AD%90%E9%83%BD%E6%98%AF%E7%94%B1git-am%E8%B0%83%E7%94%A8%E7%9A%84> "基于电子邮件的3个钩子都是由git am调用的")基于电子邮件的3个钩子都是由git am调用的

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E5%85%B6%E4%BB%96%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%92%A9%E5%AD%90> "其他客户端钩子")其他客户端钩子

1. pre-rebase钩子在变å果以非零值退出，那么变基过程就会被挂起
2. post-rewrite钩子由那些执行提交替换的命令调用，包括–amend和rebase，但不包括filter-branch。该脚本的唯一参数是触发重写的命令名称，它从stdin中接收一系列重写的提交。
3. post-checkout钩子在checkout成功执行后被调用，可用于移入不想纳入版本控制的大型文件
4. post-merge钩子会在merge成功执行后运行，可用于

- 恢复git无法跟踪的权限数据
- 验è¸受git控制的文件存在

1. pre-push钩子的调用时机是在远程引用被更新之后，尚未传输对象之前。如果以非零值退出，中止推送
2. pre-auto-gc钩子会在git gc开始前被调用

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#8-3-3-%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E9%92%A9%E5%AD%90> "8.3.3 服务器端钩子")8.3.3 服务器端钩子

在推送之前运行的服务器端钩子可以随时以非零值退出，拒绝推送操作，并在客提示

1. pre-receive在收到推送时首先运行，它会从stdin处接收一系列被推送的引用
2. update脚本类似于pre-receive，但它会为每一个要更新的分支都运行一次。它不会从stdin处读取内容，它接受3个参数：引用名称（分支）、推送之前的SHA-1、推送内容的SHA-1。如果以非零值退出，只有对应的引用会被拒绝，其他引用仍然会被更新
3. post-receive钩子无法阻止推送过程，但在推送结束之前会一直保持此进行一些耗时较长的操作需谨慎

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#git%E5%BC%BA%E5%88%B6%E7%AD%96%E7%95%A5%E7%A4%BA%E4%BE%8B> "git强制策略示例")git强制策略示例

用Ruby编写脚本实现：检查提交消息的格式，只允许特定的用户修改项目中特定的子目录

在钩子脚本中用`#!`指定脚本的解释器，如果是ruby脚本，用ARGV\[0]提取首个参数

# \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git%E4%B8%8E%E5%85%B6%E4%BB%96%E7%B3%BB%E7%BB%9F> "ch09 git与其他系统")ch09 git与其他系统

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#9-1-1-git-svn%E4%B8%8ESubversion%E5%8F%8C%E5%90%91%E6%A1%A5%E6%8E%A5> "9.1.1 git svn与Subversion双向桥接")9.1.1 git svn与Subversion双向桥接

建议保持线性：只变基不合并

不要向单独的git服务器推送任何不包含git-svn-id的内容

**跳过**

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jin9-2-5-%E8%87%AA%E5%AE%9A%E4%B9%89%E5%AF%BC%E5%85%A5%E5%B7%A5%E5%85%B7> "9.2.5 自定义导入工具")9.2.5 自定义导入工具

git fast-import从stdin中读取简单的指令来写入特定的git数据。比起执行原始的git命令或是编写原始对象要容易

# \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#ch10-git%E5%86%85%E5%B9%95> "ch10 git内幕")ch10 git内幕

git本质上是一个可按内容寻址的文件系统

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-014-jing-tong-git/#10-1-%E5%BA%95%E5%B1%82%E5%91%BD%E4%BB%A4%E5%92%8C%E9%AB%98%E5%B1%82%E5%91%BD%E4%BB%A4> "10.1 底层命令和高层命令")10.1 底层命令和高层命令

.git目录中，有4项很重要

1. objects存储了个人数据库的所有内容
2. refs存储指针，指向提交对象
3. HEAD指向当前检出的分支
4. index保存暂存区信息

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-2-git%E5%AF%B9%E8%B1%A1> "10.2 git对象")10.2 git对象

git的核心å¼”数据存储。

blob对象保存文件内容

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-2-1-%E6%A0%91%E5%AF%B9%E8%B1%A1> "10.2.1 树对象")10.2.1 树对象

树类型对象解决了存储文件名的问题

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-2-2-%E6%8F%90%E4%BA%A4%E5%AF%B9%E8%B1%A1> "10.2.2 提交对象")10.2.2 提交对象

提交对象指定单个树对象的SHA-1、父提交对象和提交信息

### \[]\(<http://bj.apsonin/2022/06/14/2022-06-14-jing-tong-git/#10-2-3-%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8> "10.2.3 对象存储")10.2.3 对象存储

git构造出以对象类型作为开头的头部信息，例如”blob #{content.length}\0”，将头部信息和原始内容拼接在一起，然后计算新内容的SHA-1；接着使用zlib压缩新内容；最后写道磁盘上的对象中

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-3-git%E5%BC%95%E7%94%A8> "10.3 git引用")10.3 git引用

1. `.giHEAD`包含指向当前所在分支的符号引用；
2. `.git/refs/heads/`存储分支；
3. `.git/refs/tags/`存储标签；
4. `.git/refs/remotes/`存储最后一次推送到远程仓库的每个分支的值。是只读的，无法用commit命令来更新

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E5%8C%85%E6%96%87%E4%BB%B6> "包文件")包文件

执行git gc会查找名称和大小相近的文件，只保存不同版本文件之间的差异。

包文件包含了删除的，索引文件包含了针对包文件内容的偏移（**博主注：这似乎说明在加密文件系统中使用大型包文件可能会让索引记录的偏移失去意义，因为某些加密模式需要解密整个包文件**CF：[10.7.1](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#维护 "10.7.1")）

- `.git/objects/info/packs`
- `.git/objects/pack/pack-*.idx`
- `.git/objects/pack/pack-*.pack`

底层命令`git verify-pack`可以用来查看打包的内容。CF：[10.7.3](http://.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#移除大对象 "10.7.3")

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-5-%E5%BC%95%E7%94%A8%E8%A7%84%E6%A0%BC> "10.5 引用规格")10.5 引用规格

`git remote add origin <url>`会在.git/config中添加3行

|                   |                                                                           |
| ----------------- | ------------------------------------------------------------------------- |
| 1  
2  
3 | \[remoigin"]url = \<url>fetch = +refs/heads/*:refs/remotes/origin/* |

其中的加号指示即便在不能快进的情况下也更新引用

可以通过添加一行`push = refs/heads/master:refs/remotes/qa/master`使得这成为`git push origin`的默认操作

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-6-git%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE> "10.6 git传输协议")10.6 git传输协议

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-6-1-%E5%93%91%E8D%8F%E8%AE%AE> "10.6.1 哑协议")10.6.1 哑协议

dumb协议的获取过程就是一系列的HTTP GET请求

替代仓库是让派生项目共享对象的好办法。`objects/info/http-alternates`记录替代仓库URL列表

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-6-2-%E6%99%BA%E8%83%BD%E5%8D%8F%E8%AE%AE> "10.6.2 智能协议")10.6.2 智能协议

用ssh协议push时会尝试以ssh的方式在远程服务器上执行命令，就像

`ssh -x git@server "git-receive-packsimplegit-progit.git'"`

收到服务器的状态后，send-pack进程就能够确定那些提交是自己拥有但服务器却没有的

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-7-%E7%BB%B4%E6%8A%A4%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D> "10.7 维护与数据恢复")10.7 维护与数据恢复

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E7%BB%B4%E6%8A%A4> "维护")维护

有7000个左右的松散对象或50个以上的包文件会触å和gc.autopacklimit配置设置来修改这些限制。CF：[10.4](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#包文件 "10.4")

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-7-2-%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D> "10.7.2 数据恢复")10.7.2 数据恢复

`git reflog`展示HEAD曾经指向的引用

`git log -g`会将引用日志按照正常的log格式输出

如果丢失了引用日志，例如误操作`rm -Rf .git/logs/`，可以使用`git fsck`检æ选项会显示出所有没被其他对象指向的对象

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E7%A7%BB%E9%99%A4%E5%A4%A7%E5%AF%B9%E8%B1%A1> "移除大对象")移除大对象

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E9%A6%96%E5%85%88%E6%89%BE%E5%88%B0%E5%93%AA%E4%BA%9B%E6%96%87%E4%BB%B6%E8%BE%83%E5%A4%A7> "首先找到哪些文件较大")首先找到哪些文件较大

先执行git gc把所有对象放到包文件中（博主注：包后用`git count-objects -v`查看是否只有1个包文件

接着用`git verify-pack -v .git/objects/pack/pack-*.idx | sort -k 3 -n | tail`列出最大体积的对象。要查出文件名，还要用`git rev-list --objects --all | grep <sha1>`

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E6%9F%A5%E7%9C%8B%E5%93%AA%E4%BA%9B%E6%8F%90%E4%BA%A4%E4%BF%AE%E6%94%B9%E4%BA%86%E8%AF%A5%E5%A4%A7%E6%96%87%E4%BB%B6> "查看哪些提交修改了该大文件")查看哪些提交修改了该
`git log --oneline --branches -- <path>`

#### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#%E7%A7%BB%E9%99%A4> "移除")移除

|           |                                                                                                        |
| --------- | ------------------------------------------------------------------------------------------------------ |
| 1  
2 | git filter-branch -index-filter \  
 'git rm --ignore-unmatch --cached \<path>' -- <引入大文件的最早æ¶中–index-filter选项与[7.6节](http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#重写历史 "7.6节")用过的–tree-filter类似，但它配合`git rm --cached`速度更快。–ignore-unmatch选项指明待删除文件不匹配时不显示错误

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-8-%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F> "10.8 环境变量")10.8 环境变量

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-8-2-%E4%BE4%BD%8D%E7%BD%AE> "10.8.2 仓库位置")10.8.2 仓库位置

GIT\_CEILING\_DIRECTORIES控制.git目录的查找行为。如果你访问到加载速度缓慢的目录（磁带或慢速网络），你可能会想要git趁早停止。

GIT\_ALTERNATE\_OBJECT\_DIRECTORIES是一个由冒号分隔的列表，用于告诉git，如果对象不再`.git/object`中，应该去哪里检查对象。用于大量项目中共享相同内容的大文件，避免存储过多的副本

### \[]\(<http://bj.apsonic-moto.cn/2022022-06-14-jing-tong-git/#10-8-5-%E7%BD%91%E7%BB%9C> "10.8.5 网络")10.8.5 网络

GIT\_SSL\_NO\_VERIFY告诉git不验证ssl证书。如果你使用自签名证书通过https搭建git服务器，还没有安装完整的证书，这个选项就很有必要了

如果http操作的数据速率低于GIT\_HTTP\_LOW\_SPEED\_LIMIT字节/秒、持续时间超过GIT\_HTTP\_LOW\_SPEED\_TIME秒，git将中止该操作。这些值会覆盖http.lowSpeedLimit和http.lowSpeedTime配置值

### \[]\(<http://bj.apsonic-mot022/06/14/2022-06-14-jing-tong-git/#10-8-7-%E8%B0%83%E8%AF%95> "10.8.7 调试")10.8.7 调试

### \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#10-8-8-%E6%9D%82%E9%A1%B9> "10.8.8 杂项")10.8.8 杂项

GIT\_FLUSH强制git在向stdout中增量写入的时候使用非缓冲I/O。取值为1会使得git更频繁地刷新，取值为0会缓冲所有的输出。默认不设置此变量会根据活动情况和输出模式来选择合适的缓冲方案

## \[]\(<http://bj.apsonic-moto.cn/20226/14/2022-06-14-jing-tong-git/#A-6-powershell> "A.6 powershell")A.6 powershell

Post-Git包为powershell中的git提供命令补全功能

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#B-%E5%9C%A8%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E4%B8%AD%E5%B5%8C%E5%85%A5git> "B 在应用程序中嵌入git")B 在应用程序中嵌入git

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#C-2-2-clone> "C.2.2 clone")C.2.2 clone

默认的`git clone`像是多条命令的包装器：创建新目录、进入该目录，init，remote add，fetch，checkout

## \[]\(<http://bj.apsonic-moto.cn/2022/06/14/2022-06-14-jing-tong-git/#C-3-3-diff> "C.3.3 diff")C.3.3 diff

使用-b选项来过滤掉空白字符造成的差异

