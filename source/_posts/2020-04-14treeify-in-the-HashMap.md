---
title: 为什么在HashMap中树化的阈值为8
date: 2020-04-14 15:14:06
tags: HashMap
categories: Java
---

具体原因在源码上的注释有讲到一些。

1. 树化后，每个节点基本上会变为原来的`2倍`，主要是因为树中的节点还需要保留更多其他节点的信息，比如原本只需要`hash, key, value, next`，树化的节点继承了原本的节点，还需要`parent, left, right, pre, red`等信息，所以最好的情况是不要树化。而且一般情况下的hash不会冲突成这个样子。
2. 不失一般性，采用随机hash进行实验，发现链长度服从强度为0.5的泊松分布，及`exp(-0.5)*pow(0.5, k)/k!`，当`k=8`时，其概率已经到`0.00000006`了，在往后就小于千万分之一了，因此这里树化的阈值选择为8.