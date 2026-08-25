
---
title: "rust学习第10章"
description: "rust学习第10章"
date: 2026-08-14
lastmod: 2024-08-14
cover: "/hero/background/15.jpg"
categories:
  - 学习
  - rust
tags:
  - 学习
  - rust
tocStartLevel: 3
tocEndLevel: 4
---





#### 测试
##### #[cfg(test)]标注
```rust
#[cfg(test)]
mod tests{
  #[test]
  fn it_works()
  {
    assert_eq!(4,2 + 2);
  }
  fn nothing()
  {

  }
}
```
##### 测试私有函数
```rust
pub fn add_two(a:i32)->i32
{
  internal_adder(a,2)
}
fn internal_adder(a:i32,b:i32)->i32
{
  a + b
}
#[cfg(test)]
mod tests{
  use super::*;
  #[test]
  fn it_works()
  {
    assert_eq!(4,internal_adder(2,2));
  }
}
```
#### 集成测试
一个test目录和src文件夹同级
在test目录下的每个测试文件都是单独的crate
在test目录下不需要特殊处理
也就是说只需要引用然后#[test]就可以了
对于上面的例子在test文件里就是这样
```rust
use temp1;//项目名
#[test]
fn it_works()
{
  assert_eq!(4,internal_adder(2,2));
}
```
**特别强调！**

当src/里只有一个main.rs时tests/里的用不了，原因如下
- Cargo 只在存在 src/lib.rs（或 Cargo.toml 里声明了 [lib]）时才会生成一个名为 temp1 的库 crate，别的文件（包括 tests/）才能 use temp1;。
- 只有 src/main.rs 时，temp1 是一个二进制 crate，它不能被任何其他 crate 导入。于是 use temp1; 报 E0432: no external crate temp1。
**办法**
. 直接在main.rs里进行测试写#[cfg(test)]
. 写一个lib.rs就可以了



. 运行一个特定的集成测试：cargo test 函数名
. 运行某个测试文件内的所有测试：cargo test --test 文件名

11章内容结束！
