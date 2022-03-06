#### 注:本笔记是学习《Head First Ruby》一书的笔记。

#### 第一章(编写你想要的代码)

- 使用irb shell

  在控制台输入命令:irb(Interactive Ruby) shell 即可启动交互式Ruby解释器。输入:exit即可返回控制台窗口。

- 运行脚本

  新建一个名为hello.rb的脚本，输入以下内容:

  ```ruby
  puts "What's your name?"
  input = gets # 输入内容保存在input变量中
  puts "your name is #{input}"
  ```

  打开终端，使用命令执行这段脚本:

  ```ruby
  ruby hello.rb 
  ```

  即可执行脚本

  **puts**: 标准输出函数，后面可以跟多个参数，参数之间使用","分割，输出内容会分行显示。

  ```ruby
  puts "first","second","third"
  ```

  **gets**:从标准输入读入一行用户输入内容。

- 字符串内插(只在双引号字符串中应用)

  ```ruby
  puts "your name is #{input}"
  ```

  使用#{...}来内插替换字符串。#{}不只是使用变量，还可以是ruby的表达式

  ```ruby
  puts "result equal #{6 * 7}"
  ```

- chomp

  ```ruby
  puts "your name?"
  input = gets
  puts "your name is #{input}!"  # 如果是从gets命令中获取的，会自动换行
  
  # 结果
  your name?
  huang
  your name is huang
  ! # 换行了
  ```

  如果一个字符串的最后一个字符是换行，*chomp*方法会删除这个字符。

  ```ruby
  puts "your name?"
  input = gets
  name = input.chomp
  puts "your name is #{name}!"  # 如果是从gets命令中获取的，会自动换行
  
  # 结果
  your name?
  huang
  your name is huang!
  ```

  查看一个对象能调用的方法

  ```ruby
  puts "hello".methods  # 结果是一个列表，列表中存储的是这个字符串对象能调用的方法
  ```

- 条件语句

  ```ruby
  if/elsif/else ...end
  ```

  *if* 语句中的代码只在条件为*true*时才执行，不过*unless*语句中的代码只在条件为*false*时才执行。

  ```ruby
  a = 30
  b = 20
  if a > b
     puts "a 大于b"
  elsif
     puts "a 小于b"
  end
  
  a = 30
  b = 40
  unless a > b
     puts "a 小于b"
  else
     puts "a 大于b"
  end
  
  # 下面的更容易理解
  if !(lights == "red")
    puts "go"
  end
  ==> 
  unless lights == "red"
    puts "go" 
  end
  ```

- 循环 

  **while循环**

  ```ruby
  number = 1
  while number <= 5
    puts number
    number += 1
  end
  
  # until 和 while 刚好相反
  number = 1
  until number > 5
    puts number
    number += 1
  end
  ```

#### 第二章(方法与类)

**方法的定义**

```ruby
def 方法名(参数列表)
end
```

注意: 如果一个方法没有参数，可以省略"()"。方法名采用""小驼峰"原则，即"_"分隔。

- 可选参数

  ```ruby
  def order_soda(flavor, size = "medium", quantity = 1)
      if quantity == 1
          plural = "soda" # 多元的 
      else
          plural = "sodas"
      end
      puts "#{quantity} #{size} #{flavor} #{plural}"
  end
  ```

  *注意: 不能把可选参数放在必要参数的前面!*

Vehicle： 交通工具，车辆；（实现目的的）工具，媒介；

- 返回值

  一个方法中最后计算的表达式的值会自动作为这个方法的返回值。

  ```ruby
  def mileage(miles_driven, gas_used)
      if gas_used == 0
          return 0.0 # 提前终止
      end
      miles_driven / gas_used  # 自动返回，不需要显示的书写 return 关键字 
  end 
  ```

- **类**

  ```ruby
  # 类的模板
  # class 类名 (采用大驼峰原则)
  #   定义方法和变量
  # end  类定义结束
  class Dog
   def talk
      puts "hello"
   end
  end
  
  # 初始化一个类
  dog = Dog.new
  ```

- 实例变量

  ```ruby
  class Dog
      def make_up_name(name)
          @name = name # @name表示一个实例变量
      end
      
      def talk
          puts "Animal's name is #{@name}"
      end
  end
  
  dog = Dog.new
  dog.make_up_name("Yard")
  dog.talk
  ```

- 存取方法

  Ruby不允许直接访问一个类的实例，比如下面是错误的示范
  ```ruby
  dog = Dog.new
  dog.@name = "xx"  # 错误的语法
  ```

  正确示范:

  ```ruby
  class Dog
      def name= name_value  # "="为方法名的一部分了 
          @name = name_value
      end
  
      def name
          @name
      end
  end
  
  dog = Dog.new
  dog.name = "petter"  # "=" 之间可以有空格
  puts "#{dog.name}"
  ```

- 属性书写器和阅读器

  Ruby提供了一些快捷的方法，用于实例属性的访问

  ```ruby
  attr_writer :name  # 有空格  setter方法
  # 等同于下面的方法
  def name= (new_value)
    @name = new_value
  end
  
  attr_reader :name # getter方法
  # 等同于下面的方法
  def name
    @name
  end
  
  
  class Dog
      # setter和getter方法 可以多个实例变量
      attr_accessor :name, :age
  end
  
  dog = Dog.new
  dog.name = "huang"
  dog.age = 20
  puts "#{dog.name}---#{dog.age}"
  
  ```

  

  



