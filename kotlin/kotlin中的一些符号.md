## ? 表示这个对象可能为空
 b?.length //如果 b非空，就返回 b.length ，否则返回 null，这个表达式的类型是 Int?

### 如果 ?: 左侧表达式非空，elvis操作符就返回其左侧表达式，否则返回右侧表达式。
 请注意，当且仅当左侧为空时，才会对右侧表达式求值。
 val l = b?.length ?: -1

## !! 会返回一个非空的 b 值 或者如果 b 为空，就会抛出一个 NPE 异常
## $ 在字符串中引用一个变量
 print("this is my $str")
## ==判断值是否相等
## ===判断值及引用是否完全相等
## ..
if (i in 1..10) { // 等同于 1 <= i && i <= 10
  println(i)
}
//使用until函数,创建一个不包括其结束元素的区间
for (i in 1 until 10) {   // i in [1, 10) 排除了 10
   println(i)
}

## _
Book声明了 id，name两个变量。解构时如果只需要id这一个变量时，可以这么做：

val book = Book(1, "英语")
val (id, _ ) = book

## ::
//得到类的Class对象
startActivity(Intent(this@KotlinActivity, MainActivity::class.java))

//内联函数和reified后续介绍
inline  fun <reified T> Gson.fromJson(json:String):T
{
   return fromJson(json, T::class.java)
}

var setBook = setOf<String>("hello", "hi", "你好")
//    setBook.forEach { print(it)}
    setBook.forEach(::print)

## @
1、限定this的类型
class User {
    inner class State{
        fun getUser(): User{
            //返回User
            return this@User
        }
        fun getState(): State{
            //返回State
            return this@State
        }
    }
}

2、作为标签

跳出双层for
loop@ for (itemA in arraysA) {
     var i : Int = 0
      for (itemB in arraysB) {
         i++
         if (itemB > 2) {
             break@loop
         }

         println("itemB:$itemB")
     }

}
命名函数自动定义标签：
fun fun_run(){
    run {
        println("lambda")
    }
    var i: Int = run {
        return@run 1
    }
    println("$i")
    //匿名函数可以通过自定义标签进行跳转和返回
    i = run (outer@{
        return@outer 2
    })
    println(i)
}

从forEach函数跳出
fun forEach_label(ints: List<Int>)
{
    var i =2
    ints.forEach {
        //forEach中无法使用continue和break;
      //  if (it == 0) continue //编译错误
      //   if (it == 2) break  //编译错误
        print(it)
    }
     run outer@{
         ints.forEach {
             if (it == 0) return@forEach //相当于在forEach函数中continue,实际上是从匿名函数返回
             if (it == 2) return@outer //相当于在forEach函数中使用break,实际上是跳转到outer之外
         }
     }

    if (i == 3)
    {
        //每个函数的名字代表一个函数地址，所以函数自动成为标签
        return@forEach_label //等同于return
    }
}

## {}
  // 一个参数
var callback: ((str: String) -> Unit)? = null
callback = { println(it)}
// 判断并使用
callback?.invoke("hello")

//两个参数
var callback2: ((name: String, age: Int) -> Unit)? = null
callback2 = { hello: String, world: Int -> println("$hello's age is $world") }
callback2?.invoke("Tom", 22)

var callback3 :((num1:Int, num2: Int)->String)? = null
//类型可以推断
callback3 = { num1, num2 ->
    var res:Int = num1 + num2
    res.toString()
}

println(callback3?.invoke(1, 2))
