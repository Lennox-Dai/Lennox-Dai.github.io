---
title: RUST整理2--基本类型
description: 基本类型
published: 2024-05-22
tags: 课内学习
comments: true
image: "img/slt14.jpg"
category: RUST程序设计
draft: false
---



# RUST整理2--基本类型



1. **数据表示方法：**

   > - `1_024`：十进制数字，下划线是Rust的一个特性，用于增加数字的可读性。这与`1024`是等价的。
   > - `0xff`：十六进制表示的数字，等于十进制的`255`。
   > - `0o77`：八进制表示的数字，等于十进制的`63`。
   > - `0b1111_1111`：二进制表示的数字，等于十进制的`255`。
   >
   > ```rust
   > // 修改 `assert!` 让代码工作
   > fn main() {
   >     let v = 1_024 + 0xff + 0o77 + 0b1111_1111;
   >     assert!(v == 1597);
   > }
   > ```



2. **默认浮点数推断是f64**



3. **Range用法：**

   > - **Range:**
   >
   >   `Range`表示一个半开区间，包括起始值但不包括结束值。
   >
   > - **RangeInclusive:**
   >
   >   `RangeInclusive`表示一个闭区间，即包括起始值和结束值。
   >
   >   ```rust
   >   use std::ops::{Range, RangeInclusive};
   >   fn main() {
   >       assert_eq!((1..5), Range{ start: 1, end: 5 });
   >       assert_eq!((1..=5), RangeInclusive::new(1, 5));
   >   }
   >   ```



4. **返回空元组**

   ```rust
   fn implicitly_ret_unit() {
       println!("I will return a ()")
   }
   
   fn main() {
       implicitly_ret_unit();
   }
   ```

   > 这里implicitly_ret_unit()的返回值是一个空元组==（）==



5. **大括号赋值**

   ```rust
   fn main() {
       let v = {
           let x = 3;
           x
       };
   
       assert!(v == 3);
   }
   ```

   > 如果都是语句，那么返回（），不然返回表达式的值



6. **！返回类型**

   ```rust
   fn never_return() -> ! {
       loop {
           // 无限循环，永远不会返回
       }
   }
   ```

   > 无限循环

   ```rust
   fn never_return() -> ! {
       panic!("This function never returns!");
   }
   ```

   > 调用panic！宏

   ```rust
   fn another_never_return() -> ! {
       loop {
           // 无限循环，永远不会返回
       }
   }
   
   fn never_return() -> ! {
       another_never_return();
   }
   ```

   > 调用另一个永远不会返回的函数



7. **发散函数**

   ```rust
   fn never_return_fn() -> ! {
       unimplemented!()
   }
   ```

   ```rust
   fn never_return_fn() -> ! {
       panic!()
   }
   ```

   ```rust
   fn never_return_fn() -> ! {
       todo!();
   }
   ```

   ```rust
   fn never_return_fn() -> ! {
       loop {
           std::thread::sleep(std::time::Duration::from_secs(1))
       }
   }
   ```

   
