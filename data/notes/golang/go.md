# GOLANG

* 函数
  > func function_name( [parameter list] ) [return_types] { 函数体 }

  ```  
  func max(num1, num2 int) int { }
  func swap(x, y string) (string, string) {}
  ```

* 数组

  > var variable_name [SIZE] variable_type

  ```
  var variable_name [SIZE] variable_type
  ```

* 指针

  > var var_name *var-type
  ```
  var ip *int        /* 指向整型*/
  var fp *float32    /* 指向浮点型 */
  ```

* 结构体定义
  > type struct_variable_type struct {
  > member definition
  > member definition
  > ...
  > member definition
  > }

* 结构体声明

  > variable_name := structure_variable_type {value1, value2...valuen}   
  > variable_name := structure_variable_type { key1: value1, key2: value2..., keyn: valuen}

  ```
  package main
  import "fmt"
  type Books struct { title string author string subject string book_id int }
  func main() {
      // 创建一个新的结构体
      fmt.Println(Books{"Go 语言", "www.runoob.com", "Go 语言教程", 6495407})
      // 也可以使用 key => value 格式
      fmt.Println(Books{title: "Go 语言", author: "www.runoob.com", subject: "Go 语言教程", book_id: 6495407})
      // 忽略的字段为 0 或 空
  fmt.Println(Books{title: "Go 语言", author: "www.runoob.com"})
  }

  ```