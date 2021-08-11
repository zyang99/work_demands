## TypeScript

### TypeScript介绍

+ JS中的变量是动态类型---带来了一些隐患（比如加减法的时候 1+true 这是不报错的 就很难受 容易留下隐患）
+ TypeScript到底是什么？
  + 微软---以JavaScript为基础构建的语言--一个JavaScript的超集(扩展)---Type加了类型--从动态变为了静态
  + 可以在任何支持JavaScript的平台中执行。扩展了JavaScript，并添加了类型
  + TS不能被JS解析器直接执行---**需要先编译成JS** 
+ TypeScript增加了什么？
  + 类型
  + 支持ES的新特性（JS代码可以）
  + 添加了ES不具备的新特性
  + 丰富的配置选项--可以配置编译成什么版本的JS代码 
  + 强大的开发工具

### 基本类型

+ 类型声明

  + 类型声明是TS一个非常重要的点

  + 通过类型声明可以指定TS中变量（参数、形参）的类型

  + 指定类型后，当为变量赋值时，TS编译器会自动检查值是否符合类型声明，符合则赋值，否则报错

  + 简而言之，类型声明给变量设置了类型，使得变量只能存储某种类型的值

  + 语法

    ```typescript
    let 变量: 类型;
    let 变量: 类型 = 值;
    function fn(参数: 类型, 参数: 类型): 类型{
        ...
    }
    ```

+ 自动类型判断

  + TS拥有自动的类型判断机制
  + 当对变量的声明和赋值是同时进行的，TS编译器会自动判断变量的类型
  + 所以如果你的变量的声明和赋值是同时进行的，可以省略掉类型声明

+ 类型

  |   类型   |           例子           |                             描述                             |
  | :------: | :----------------------: | :----------------------------------------------------------: |
  |  number  |       1，-35，2.5        |                           任意数字                           |
  |  string  |       'hi',"hi",hi       |                          任意字符串                          |
  | boolean  |       true、false        |                      布尔值true或false                       |
  |  字面量  |          其本身          | 限制变量的值就是该字面量的值<br />let a: 10   那么a只能是10  |
  |   any    |            *             | 任意类型。<br />一个变量设置类型为any相当于该变量关闭了TS的类型检测----> 使用TS时，不建议使用any类型(显示any)<br />声明变量不指定类型，TS解析器会自动判断变量的类型为any(隐式any)<br />any类型的变量可以赋值给任意变量（祸害了其他变量） |
  | unknown  |            *             | 类型安全的any<br />unknowm类型的变量不能直接赋值给其他变量（1先判断一下类型再赋值 2使用类型断言） |
  |   void   |     空值(undefined)      |                     没有值(或undefined)                      |
  |  never   |          没有值          |                         不能是任何值                         |
  |  object  |    { name:'孙悟空' }     | 任意JS对象<br />不太实用，在JS中对象太多了<br />实际使用中，是限制对象中有什么些性质的属性。必须有且仅有这些属性<br />语法：{属性名1:属性值，属性名2?:属性值} 2可选 |
  |  array   |         [1,2,3]          |                          任意JS数组                          |
  |  tuple   |          [4,5]           |              元组：TS新增类型，**固定长度数组**              |
  |   enum   |        enum{A,B}         |                       枚举：TS新增类型                       |
  | 联合类型 | let a: boolean \| string |             可以使用 \|来连接多个类型(联合类型)              |

  + 对象类型 object

    + ```typescript
      // JS中对象很多
      let a: object
      a = {}
      a = function
      
      //{} 用来指定对象中包含哪些属性
      //语法： {属性名：属性值， 属性名：属性值}
      //在属性后边加上？表示属性是可选的
      let b: { name: string, age?: number }
      b = { name: '孙悟空', age: 18}
      
      //[propName: string]: any  表示任意类型属性
      let c = { name: string, [propName: string]: any }
      c = { name: '孙悟空', age: '18', gender: '男' }
      
      // 设置函数结构的类型声明：
      // 语法： （形参：类型， 形参：类型...）=>返回值类型
      let d: (a: number, b: number)=>number
      d = function(n1, n2): number{
          return n1+n2
      }
      ```

  + 数组类型 

    + ```typescript
      //string[] 表示字符串数组
      let a: string[]
      a = ['1','a','b']
      //Array<string>
      let b: Array<string>
      b = ['a','b','c']    
      ```

  + 元组

    + ```typescript
      //元组： 固定长度的数组
      let a: [string, string]
      a = ['a','b']
      ```

  + 枚举

    + ```typescript
      //枚举: 将所有可能的情况值写出来
      enum Gender{
          Male = 1,
          Female = 2,
          // 可写=1 也可不写  
          // 默认 =0  =1  =2 .....
      }
      let a: {name: string, gender: Gender}
      a = {
          name: '孙悟空',
          gender: Gender.Male
      }
      ```

      ```typescript
      // | 表示或   &表示且 与 同时
      // & 使用场景： 可能两个类型分开使用，在某个地方又是需要同时满足。 & 可以连接动态的类型
      let a: {name: string} & {age: string}
      a = {name:'122', age:'12'}
      
      // 类型别名
      type myType = 1 | 2 | 4 | string
      let b: myType
      let c: myType
      ```

  + 类型断言： 可以用来告诉解析器变量的实际类型（让解析器相信使用者的判断）

    ```typescript
    /*
    语法：
    	变量 as 类型
    	<类型>变量
    */
    e = a as string;
    e = <string>a;
    ```

### 编译选项



