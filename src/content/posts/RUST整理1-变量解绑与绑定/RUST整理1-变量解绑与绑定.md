---
title: RUST整理1--变量解绑与绑定
description:
published: 2024-05-22
tags: 课内学习
comments: true
image:
  - "img/slt10.jpg"
categories:
  - 专业选修
  - RUST程序设计
draft:
---



# RUST整理1--变量解绑与绑定



1. **生命周期的声明处：**

   > - **函数签名：**
   >
   >   ```rust
   >      fn borrow<'a>(x: &'a str) -> &'a str {
   >          x
   >      }
   >   ```
   >
   > - **结构体定义：**
   >
   >   ```rust
   >      struct ImportantExcerpt<'a> {
   >          part: &'a str,
   >      }
   >   ```
   >
   > - **实现块（impl blocks）：**
   >
   >   *这里后面一个<'a'>要和struct声明的生命周期一样*
   >
   >   ```rust
   >      impl<'a> ImportantExcerpt<'a> {
   >          fn announce_and_return_part(&self, announcement: &str) -> &'a str {
   >              self.part
   >          }
   >      }
   >   ```
   >
   >   *如果需要在impl里引入新的生命周期，应该这样：*
   >
   >   ```rust
   >   impl<'a, 'b> ImportantExcerpt<'b> {
   >       fn announce_and_return_part(&self, announcement: &'a str) -> &'b str {
   >           // 你的代码逻辑
   >           self.part
   >       }
   >   }
   >   ```
   >
   > - **泛型类型的约束中：**
   >
   >   *生命周期参数的名称通常以 `'` 符号开始，后面紧跟诸如 `'a`、`'b` 等的描述符。*
   >
   >   ```rust
   >      fn longest_with_an_announcement<'a, T>(x: &'a str, y: &'a str, ann: T) -> &'a str
   >      where
   >          T: std::fmt::Display,
   >      {
   >          println!("Announcement! {}", ann);
   >          if x.len() > y.len() { x } else { y }
   >      }
   >   ```
   >
   > 



2. **&'static：**

   在Rust中，`'static` 是唯一一个具有特殊含义的生命周期标识符，它指的是程序运行期间的整个生命周期。

   ```rust
   fn define_x() -> &'static str {
       let x = "hello";
       x
   }
   ```

   
