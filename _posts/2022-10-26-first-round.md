---
layout: post
title: "first round"
subtitle: ""
date: 2022-10-26
author: "夜雨声烦"
header-img: "img/bg2.png"
header-mask: 0.2
catalog: true
tags: []
---

## One Step at a Time: Long-Horizon Vision-and-Language Navigation with Milestones

### 摘要

我们研究开发可以遵循人类指令来推断和执行一系列动作以完成基础任务的自主代理的问题。近年来取得了重大进展，特别是在短期任务方面。然而，当涉及到具有扩展动作序列的长期任务时，代理很容易忽略一些指令或卡在长指令的中间并最终导致任务失败。为了应对这一挑战，我们提出了一个模型无关的基于里程碑的任务跟踪器（M-TRACK）来指导代理并监控其进度。具体来说，我们提出了一个里程碑构建器，它使用代理需要逐步完成的导航和交互里程碑来标记指令，以及一个里程碑检查器，它系统地检查代理在其当前里程碑中的进度并确定何时进行下一个里程碑。在具有挑战性的 ALFRED 数据集上，我们的 M-TRACK 导致与两个竞争基础模型相比，看不见的成功率显着提高了 33% 和 52%。