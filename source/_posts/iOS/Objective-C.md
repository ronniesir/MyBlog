---
title: Objective-C基础语法
date: 2013-10-24
updated: 2017-12-20	
tags:
- 移动开发
- iOS
- Objective-C
- C
categories:
- iOS
---

### Objective-C 的数据类型
### Objective-C 的数组（可变数组和不可变数组）
```Objective-c
    NSMutableArray* mutableArrary = [[NSMutableArray alloc]init];
    [mutableArrary addObject:@"first"];
    [mutableArrary addObject:@"second"];
    NSArray *array = [[NSArray alloc]initWithObjects:@"third",@"fouth",nil];
```
### Objective-C 字典（可变字典和不可变字典）
```iOS
    NSDictionary* dic = [[NSDictionary alloc]initWithObjectsAndKeys:@"value",@"key",@"value1",@"key2", nil];
    NSMutableDictionary* dicM = [[NSMutableDictionary alloc]init];
    [dicM setObject:@"value3" forKey:@"key3"];
    [dicM addEntriesFromDictionary:dic];
```
### Objective-C 的方法和接口定义
### Objective-C 的方法和接口定义

