# Docker

标签（空格分隔）： SummerCamp2018 Docker

---

[toc]

## 1. 概述

## 1.1. 什么是Docker?

早在Docker出现之前，虚拟化技术就被用在虚拟机和杀毒软件上。其中虚拟机是用软件模拟操作系统所需要的整个硬件环境，如比较知名的VM Ware和VirtualBox软件，从而达到在操作系统中运行另一个操作系统的效果，但其非常地消耗系统资源。而一些杀毒软件使用沙箱技术模拟出木马运行的环境，从而可以研究木马病毒的行为而不对用户系统造成破坏。Docker在容器的基础上，进行了进一步的封装，从文件系统、网络互联到进程隔离等等，极大的简化了容器的创建和维护。使得 Docker 技术比虚拟机技术更为轻便、快捷。
近几年伴随着云计算的发展，Docker容器技术由于其突出的性能和资源利用率，得到了飞速地发展。

## 1.2. 为什么要用Docker?
对比传统虚拟机总结


|   特性     |   容器    |   虚拟机   |
| --------   | --------  | ---------- |
| 启动       | 秒级      | 分钟级     |
| 硬盘使用   | 一般为 MB | 一般为 GB  |
| 性能       | 接近原生  | 弱于       |
| 系统支持量 | 单机支持上千个容器 | 一般几十个 |

下面这些Docker的使用场景，为你展示了如何借助Docker的强力，在非常低的额外开销的情况下，打造一个一致性的环境。

**1. 简化配置。**这是Docker公司宣传的Docker的主要使用场景。虚拟机的最大好处是能在你的硬件设施上运行各种配置不一样的平台（软件、系统），Docker在降低额外开销的情况下提供了同样的功能。它能让你将运行环境和配置放在代码中然后部署，同一个Docker的配置可以在不同的环境中使用，这样就降低了硬件要求和应用环境之间耦合度。
**2. 代码流水线（Code Pipeline）。**管理前一个场景对于管理代码的流水线起到了很大的帮助。代码从开发者的机器到最终在生产环境上的部署，需要经过很多的中间环境。而每一个中间环境都有自己微小的差别，Docker给应用提供了一个从开发到上线均一致的环境，让代码的流水线变得简单不少。
**3. 提高开发效率。**这就带来了一些额外的好处：Docker能提升开发者的开发效率。如果你想看一个详细一点的例子，可以参考Aater在DevOpsDays Austin 2014 大会或者是DockerCon上的演讲。不同的开发环境中，我们都想把两件事做好。一是我们想让开发环境尽量贴近生产环境，二是我们想快速搭建开发环境。理想状态中，要达到第一个目标，我们需要将每一个服务都跑在独立的虚拟机中以便监控生产环境中服务的运行状态。然而，我们却不想每次都需要网络连接，每次重新编译的时候远程连接上去特别麻烦。这就是Docker做的特别好的地方，开发环境的机器通常内存比较小，之前使用虚拟的时候，我们经常需要为开发环境的机器加内存，而现在Docker可以轻易的让几十个服务在Docker中跑起来。
**4. 隔离应用。**有很多种原因会让你选择在一个机器上运行不同的应用，比如之前提到的提高开发效率的场景等。我们经常需要考虑两点，一是因为要降低成本而进行服务器整合，二是将一个整体式的应用拆分成松耦合的单个服务（译者注：微服务架构）。如果你想了解为什么松耦合的应用这么重要，请参考Steve Yege的这篇论文，文中将Google和亚马逊做了比较。
**5. 整合服务器。**正如通过虚拟机来整合多个应用，Docker隔离应用的能力使得Docker可以整合多个服务器以降低成本。由于没有多个操作系统的内存占用，以及能在多个实例之间共享没有使用的内存，Docker可以比虚拟机提供更好的服务器整合解决方案。
**6. 调试能力。** Docker提供了很多的工具，这些工具不一定只是针对容器，但是却适用于容器。它们提供了很多的功能，包括可以为容器设置检查点、设置版本和查看两个容器之间的差别，这些特性可以帮助调试Bug。你可以在《Docker拯救世界》的文章中找到这一点的例证。
**7. 多租户环境。**另外一个Docker有意思的使用场景是在多租户的应用中，它可以避免关键应用的重写。我们一个特别的关于这个场景的例子是为IoT（译者注：物联网）的应用开发一个快速、易用的多租户环境。这种多租户的基本代码非常复杂，很难处理，重新规划这样一个应用不但消耗时间，也浪费金钱。使用Docker，可以为每一个租户的应用层的多个实例创建隔离的环境，这不仅简单而且成本低廉，当然这一切得益于Docker环境的启动速度和其高效的diff命令。你可以在这里了解关于此场景的更多信息。
**8. 快速部署。**在虚拟机之前，引入新的硬件资源需要消耗几天的时间。Docker的虚拟化技术将这个时间降到了几分钟，Docker只是创建一个容器进程而无需启动操作系统，这个过程只需要秒级的时间。这正是Google和Facebook都看重的特性。你可以在数据中心创建销毁资源而无需担心重新启动带来的开销。通常数据中心的资源利用率只有30%，通过使用Docker并进行有效的资源分配可以提高资源的利用率。

---

## 2. 学习目标与学习方法
### 2.1. 目标
　　掌握Docker的基本用法，

### 2.2. 方法
　　推荐读者根据本教程内容的步骤进行操作，同时浏览推荐的学习资料，如有任何不清楚的地方可参考推荐的学习资料或者自行搜索答案和找他人解答。
　　
### 2.3. 推荐学习资料

[Docker — 从入门到实践]( https://yeasy.gitbooks.io/docker_practice)

[自己学Docker](http://blog.csdn.net/Mungo/article/category/6183705)

[Container Hacks and Fun Images](https://pan.baidu.com/s/1bn0hdpH)


---

## 3. 课程内容
* [安装Docker](content/install.md)
* [安装后的准备工作](content/prepare.md)
* [获取镜像](content/pull.md)
* [操作容器](content/container.md)
* [使用Dockerfile](content/dockerfile.md)
* [操作仓库](content/push.md)

---

## 4.　课程作业

**目标：** 使用Dockerfile构建镜像编译[GSLAM](https://github.com/zdzhaoyong/GSLAM)，并使用docker run命令运行gslam, 导出镜像到文件gslam_<yourname>.tar, 并将Dockerfile文件和镜像文件提交到Report/tool/docker/<yourname>目录中。

