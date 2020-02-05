---
layout: post
title:  "bitcoin"
date:   2016-12-13 09:51:02
categories: bitcoin
---

[参考文章](http://www.michaelnielsen.org/ddi/how-the-bitcoin-protocol-actually-works/)

# 比特币

比特币的核心是加密，防止其他人非法窃取你的货币

尝试一阶一阶的构建这样的加密货币系统，以理解比特币的运作方式

# Infocoin


# P2P Network

[Link](https://bitcoin.org/en/developer-guide#peer-discovery)

这里介绍了比特币节点连接的一些核心技术，

## DNS seed
一个钱包内部会自带一些比特币节点地址，或查询比特币节点的[DNS列表地址](https://bitcoin.org/en/glossary/dns-seed)。

## 本地记录
当完成了第一次的seed以后，会记录到本地硬盘非常多的其他节点数据，也就是说，即使所有seed都奔溃了。
只要这些相互记录的节点还存在，这个p2p网络还是可以运作的。只是新增加的节点，需要额外的手段（比如导入一个节点库），才能正确的接入到原有p2p网络中。
