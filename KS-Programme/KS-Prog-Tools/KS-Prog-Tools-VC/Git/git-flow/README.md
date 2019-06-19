# Git Flow
```md
是构建在Git之上的一个组织软件开发活动的模型，是在Git之上构建的一项软件开发最佳实践。
是一套使用Git进行源代码管理时的一套行为规范和简化部分Git操作的工具。
按 Vincent Driessen 的分支模型提供高层次的库操作。

Git Flow重点解决的是由于源代码在开发过程中的各种冲突导致开发活动混乱的问题。
利用Git创建和管理分支的能力，为每个分支设定具有特定的含义名称，
并将软件生命周期中的各类活动归并到不同的分支上。实现了软件开发过程不同操作的相互隔离。

Gitflow Workflow 是一个 Git工作流程设计。
Gitflow 工作流定义了围绕项目发布设计的严格分支模型。这为管理大型项目提供了一个强大的框架。
```

# Design
```md
核心思想 ：
主分支有master、develop两个组成，分别用于产品发布、功能开发。
余下的三个辅助分支—— hotfixes、release branches、feature branches，
分别用于已发版本的bug修复、新版QA发布、新功能开发。
```

## Usage
```md
brew install git-flow-avh
```

## Reference
* [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)

* [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
* [Git Flow工作流程](https://www.jianshu.com/p/9a76e9aa9534)
* [Git Flow精简模型](http://blog.gejiawen.com/2016/12/12/git-flow-compact-model/)
