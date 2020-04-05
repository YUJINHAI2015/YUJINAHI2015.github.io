---
title: ruby学习第一课
date: 2020-03-30 23:34:07
tags:
categories: ruby
---

## 输出`helloworld`
- 文件保存 `puts "Hello, Ruby!";`  # put相当于print
- 命令行输入：`$ ruby test.rb`

## 多字符

>  EOC只是随便写的，可以用其他字符，只需保证首尾一样就行

- 普通字符输出

```
print <<EOF
    这是第一种方式创建here document 。
    多行字符串。
EOF

```

- 执行命令

```
print <<`EOC`                 # 执行命令
    echo hi there
    echo lo there
    ls -al
EOC

```

## BEGIN语句
- 输入

```
puts "这是主 Ruby 程序"
 
END {
   puts "停止 Ruby 程序"
}
BEGIN {
   puts "初始化 Ruby 程序"
}
```

- 输出

```
初始化 Ruby 程序
这是主 Ruby 程序
停止 Ruby 程序
```

## 值表示为字符串#{}

- 相当于`swift`里面的"\()", `OC` 里面的`[NSString StringWithFormat....];`
- 输入 `puts "相乘 : #{24*60*60}";`
- 输出 `相乘 : 86400`
- 输入 `name="ruby"
puts "#{name}" + "ok"
- 输出 `rubyok`

## 类和实例

- 类中变量规范

> 局部变量：小写字母或_开头
> 
> 实例变量：@开头
> 
> 类变量：@@开头
> 
> 全局变量：$开头
> 
> 类名一定是大写开头

- 输入

```
class Customer
   @@no_of_customers=0
   def initialize(id, name, addr)
      @cust_id=id
      @cust_name=name
      @cust_addr=addr
   end
   def display_details()
      puts "Customer id #@cust_id"
      puts "Customer name #@cust_name"
      puts "Customer address #@cust_addr"
    end
    def total_no_of_customers()
       @@no_of_customers += 1
       puts "Total number of customers: #@@no_of_customers"
    end
end

```

- 使用

```
cust1=Customer.new("1", "John", "Wisdom Apartments, Ludhiya")
cust1.display_details()
cust1.total_no_of_customers()

```

## 变量
- 变量和类很相似

```
Ruby 支持五种类型的变量。
	一般小写字母、下划线开头：变量（Variable）。
	$开头：全局变量（Global variable）。
	@开头：实例变量（Instance variable）。
	@@开头：类变量（Class variable）类变量被共享在整个继承链中
	大写字母开头：常数（Constant）。
```






















