---
layout: post
title: 浅谈Puppet、Chef、Ansible和SaltStack四大运维管理工具
date: 2018-01-04
categories: blog
tags: [标签一,标签二]
description: 文章金句。
---

   虚拟化技术日益普及，基于行业标准的服务器功能越来越强大，加上云计算的出现，这些因素共同导致了企业内外需要加以管理的服务器数量大幅增长。过去我们只要管理内部数据中心里面的物理服务器机架，而现在我们要管理多得多的服务器，它们有可能遍布全球各地。
	这时候，数据中心协调和配置管理工具就派得上用场。在许多情况下，我们管理大批同样的服务器，它们运行同样的应用程序和服务。这些服务器部署在企业内部的虚拟化框架上，或者作为云计算或托管实例在远程数据中心运行。在一些情况下，我们可能谈论的是完全为了支持超大应用系统而存在的大型环境，或者是支持无数小型服务的大型环境。不管怎么样，让它们都乖乖听从管理员的指挥这种能力不可小视。这是管理这些越来越庞大的基础设施的方式。
	Puppet、Chef、Ansible和Salt都是为了实现这个目标而开发的：让用户极容易配置和维护数十台、数百台、乃至数千台服务器。这倒不是说小公司就不会得益于这些工具，因为自动化和协调技术通常可以简化任何规模的基础设施的正常运行。
　　深入测评这四款工具中的每一款，探究各自的设计和功能，可以发现：虽然一些工具的得分更高，但每款工具都有一席之地，这取决于部署的目的。
  
Puppet
Puppet也许是四款工具中最深入人心的。就可用操作、模块和用户界面而言，它是最全面的。Puppet呈现了数据中心协调的全貌，几乎涵盖每一个运行系统，为各大操作系统提供了深入的工具。初始设置比较简单，只需要在需要加以管理的每个系统上安装主服务器和客户端代理软件。
　　命令行接口(CLI)简单直观，允许通过puppet命令下载和安装模块。然后，需要对配置文件进行更改，好让模块适合所需的任务;应接到指令的客户端与主服务器联系时，会更改配置文件，或者客户端通过立即触发更改配置文件的推送(push)来进行更改。
还有一些模块可以提供和配置云服务器实例和虚拟服务器实例。所有模块和配置都使用基于Ruby的Puppet专属语言或者Ruby本身构建而成，因而除了系统管理技能外，还需要编程专业知识。			
Puppet企业版拥有最全面的Web用户界面，允许使用主服务器上的预制模块和菜谱(cookbook)，实时控制被管理的节点。Web用户界面很适合用于管理，但是不允许对模块进行诸多配置。报告工具非常完善，提供了详细信息，以便了解代理软件运行如何、已做出什么样的变更。
Chef
　　Chef的总体概念类似Puppet，因为在被管理的节点上安装有主服务器和代理软件，但实际部署又不一样。除了主服务器外，安装的Chef环境还需要工作站来控制主服务器。代理软件可以借助使用SSH来部署的knife工具从工作站加以安装，减轻了安装负担。之后，被管理的节点通过使用证书，完成与主服务器之间的验证。
　　Chef的配置离不开Git，所以对Chef运作而言，了解Git如何工作是先决条件。与Puppet一样，Chef同样基于Ruby，所以还需要了解Ruby。与Puppet一样，模块可以下载，也可以从头开始编写，可以在所需配置之后部署到被管理的节点。
　　与Puppet不一样，Chef还没有一项完善的推送功能，不过提供了测试版代码。这意味着需要配置代理软件，以便与主服务器进行联系，实际上不可能立即应用变更的内容。
　　企业版Chef的Web用户界面很实用，但不提供更改配置的功能。这个Web用户界面不如Puppet企业版来得全面，缺少报告及其他功能，但允许库存控制和节点组织。
　　与Puppet一样，Chef得益于一大批的模块和配置菜谱，那些模块和配置菜谱又高度依赖Ruby。由于这个原因，Chef非常适合注重开发的基础设施。
　　Ansible
　　Ansible极其类似Salt，而不太类似Puppet或Chef。Ansible关注的重点是力求精简和快速，而且不需要在节点上安装代理软件。因此，Ansible通过SSH执行所有功能。Ansible基于Python;相比之下，Puppet和Chef基于Ruby。
　　Ansible可以通过Git软件库克隆，安装到Ansible主服务器上。安装完毕后，需要管理的节点被添加到Ansible配置环境，SSH授权密钥被附加到每个节点上，这与运行Ansible的用户有关。一旦完成了这步，Ansible主服务器可以通过SSH与节点进行通信，执行所有必要的任务。为了与默认情况下不允许根SSH访问的操作系统或发行版协同运行，Ansible接受sudo登录信息，以便在那些系统上以根用户的身份运行命令。
　　Ansible可以使用Paramiko(基于SSH2协议的Python实现)或标准SSH用于通信，不过还有一种加速模式，允许更快速、更大规模的通信。
　　针对确保服务在运行，或者触发更新和重新启动之类的简单任务，Ansible可以从命令行来运行，不需要使用配置文件。至于比较复杂的任务，Ansible配置通过名为Playbook的配置文件中的YAML语法来加以处理。Playbook还可以使用模板来扩展其功能。
　　Ansible有一大批模块，可用于管理各种系统以及亚马逊弹性计算云(EC2)和OpenStack等云计算基础设施。可以用几乎任何一种语言来编写自定义Ansible模块，只要模块输出是有效的JSON。
　　Ansible的Web用户界面以AnsibleWorks AWX的形式出现，但AWX与CLI并不直接联系在一起。这意味着，除非进行了同步过程，否则CLI里面的配置元素不会出现在Web用户界面中。你可以使用那个内置的同步工具，让两者保持一致，但需要按照预定计划运行同步工具。
　　SaltStack
　　Salt类似Ansible，因为它也是基于CLI的工具，采用了推送方法实现客户端通信。它可以通过Git或通过程序包管理系统安装到主服务器和客户端上。客户端会向主服务器提出请求，请求在主服务器上得到接受后，就可以控制该客户端了。
　　Salt可以通过普通的SSH与客户端进行通信，但如果使用名为minion的客户端代理软件，可以大大增强可扩展性。此外，Salt含有一个异步文件服务器，可以为客户端加快文件服务速度，这完全是Salt注重高扩展性的一个体现。
　　与Ansible一样，你可以直接通过CLI，向客户端发出命令，比如启动服务或安装程序包;你也可以使用名为state的YAML配置文件，处理比较复杂的任务。还有“pillar”，这些是放在集中地方的数据集，YAML配置文件可以在运行期间访问它们。
　　你可以直接通过CLI，向客户端请求配置信息，比如内核版本或网络接口方面的详细信息。只要使用名为“grain”的库存元素，就可以描述客户端;这样一来，管理员可以轻松向某一种类型的服务器发出命令，不需要依赖已配置群组。比如说，只要使用一个CLI命令，你就可以向运行某个内核版本的每个客户端发送命令。
　　与Puppet、Chef和Ansible一样，Salt也提供了大量的模块，以处理特定的软件、操作系统和云服务。自定义模块可以用Python或PyDSL来编写。除了Unix管理外，Salt的确提供Windows管理功能，但它还是更擅长管理Unix和Linux系统。
　　Salt的Web用户界面Halite非常新，功能不如其他系统的Web用户界面来得全面。它提供了事件日志和客户端状态的视图，能够在客户端上运行命令，但除此之外乏善可陈。
　　Salt的较大优点在于可扩展性和弹性。你可以有多个级别的主服务器。上游主服务器可以控制下游主服务器及其客户端。另一个优点在于对等系统，让客户端可以向主服务器提出问题，然后主服务器从其他服务器得到答案，提供全面信息。如果需要在实时数据库中查询数据，以便完成客户端的配置，这个优点就很方便。
选用Puppet、Chef、Ansible还是Salt?
   Puppet和Chef会吸引广大开发人员和注重开发的公司，而Salt和Ansible极其适合系统管理员的要求。Ansible的简洁界面和可用性非常迎合系统管理员的想法;而在拥有许多Linux和Unix系统的公司，Ansible运行起来一开始就快速又轻松。
　　Salt是四款工具中最漂亮最稳健的;与Ansible一样，它也会博得系统管理员的芳心。Salt拥有高扩展性和强大功能，的软肋就是Web用户界面。
　　Puppet是这四款工具中最成熟的，从可用性的角度来看恐怕也最容易上手，不过竭力建议你对Ruby要有深入了解。Puppet不如Ansible或Salt来得精简，配置起来有时会变得错综复杂。对异构环境来说，Puppet是最稳妥的选择，但是你可能会发觉Ansible或Salt比较适合更庞大或更一致的基础设施。
　　Chef拥有稳定的、精心设计的布局，虽然它在原始功能方面远未达到Puppet的水平，但这是款功能非常强大的解决方案。要是管理员缺乏丰富的编程经验，Chef学起来可能最困难，但它也许最适合注重开发的管理员和开发部门。











