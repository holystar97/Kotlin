### Kotlin Tutorial -Basic

```kotlin
import java.lang.Integer.parseInt
import java.lang.NullPointerException
import java.lang.NumberFormatException as NFE

fun main(args: Array<String>){

    println("변수에 대해 알아봅시다.")

    val a: Int =10 // 변경 불가 변수
    var b: Int =12 // 변경 가능 변수
    b=13

    // 원시 타입과 wrapper type 를 구분하지 않는다 -> Integer vs int no! Int yes !
    val IntegerVal : Int=10 // 타입을 명시할 필요없음
    val stringVal : String ="a string" // 타입을 명시할 필요없음
    val typeInterface=10  // int
    val typeInterface2="a string" // string


    val i=10
    // UInt : an unsigned 32 -bit integer, ranges from 0 to 65535
    // U : 부호 없는 정수
    val i2 : UInt =10U
    val l2 : Long =i.toLong() // 서로 다른 타입의 값을 명시 변환 필요
    //val l : Long =i // type mismatch -compile error


    println("조건문과 변수 타입 체크/변환")

    val x =if (a>10) "big" else "small"
    println(x)

    //자바의 최상위 클래스 Object 클래스, 코틀린의 최상위 클래스 Any(Object의 슈퍼 클래스)
    fun conditional_val(obj : Any){
        // 변수 타입 체크 is
        if(obj is Int) println("obj is Int")
        if(obj is String) println("obj is String")
        // 변수 타입 변환 as - 타입 캐스팅시에 unsafe <- 캐스팅 불가시에는 exception 발생
        // as 의 unsafe 를 방지하기 위해 ? 를 사용 -> exception 대신 null 입력
        // $ : 변수 넣어주기
        // {} : Unit return
        // ?: --> elvis 연산자 (null 대신 사용할 디폴트 값을 지정할 때 쓰는 연산자, null 인경우 기본값 지정)
        println("print obj as string > ${(obj as? String  ?: "" )}")
    }

    //obj is int
    conditional_val(1)
    //obj is String
    conditional_val("strings")

    println("슈퍼 클래스 any")
    // 슈퍼 클래스 any
    val t :Any =10
    println((t is Int))

    println("문자열 string ")
    // 문자열 string
    fun string_test(){
        val version="1.3.50"
        val javaStyle="Hello,Kotlin" + version +"!"
        val kotlinStyle ="Hello,Kotlin ${version}!"
        println(javaStyle)
        println(kotlinStyle)

        val num=10
        println("val num is equal to 10 : ${num==10}.")

        println("""\$""") // \$
        println("\$") // $
        println("""
            |hello
            |my name is kotlin
        """.trimMargin())
        // removes the trim in margin
        // default : | / other also possible

        val withoutMargin2 ="""
            #hello
            #okdol
            #apeach
        """.trimMargin("#")
        println(withoutMargin2)


    }
    string_test()

    println("비교 연산자 이해하기")

    //data class = 클래스가 data를 보유하면서 아무것도 하지 않는 클래스
    //data class는 입력한 정보가 나오는 반면, 일반 class는 주소값이 나온다.

    data class MyClass(val a: Int, val b: String)

    fun compare_operation(){
        val str1="hello, kotlin"
        val str2="hello, kotlin"
        // data class 를 사용
        val class1=MyClass(10,"class1")
        val class2=MyClass(10,"class1")
        val class3=MyClass(20,"class2")

        // == : 객체 내용 비교 (java : equals()), 문자열 비교
        // === : 객체 레퍼런스 비교
        println(str1==str2)
        println(class1 == class2)
        println(class1 == class3)
        println(class1 === class2)

    }

    compare_operation()


    println("배열 ")

    fun array_test(){
        var array= arrayOf(1,2,3)
        var array2=Array(10,{0})
        var anyArray= arrayOf(1,100,"hi",true,100.13)
        var arrayInt = arrayOf<Int>(10,20,30)
        var arrayString = arrayOf<String>("one","two","three")
        // insert
        array.set(0,100) // array.set(index, value)
        array[2]=300
        //output
        array.get(0)
        array[2]

        val intArrays =arrayOf(1,2,3,4,5)
        // return given size array with null values
        val strArrays = arrayOfNulls<String>(5)
        // return empty array of type T
        val dbArrays = emptyArray<Double>()

        println(intArrays[0])
        intArrays[0]=10
        println(intArrays[0])

        for (s in strArrays){
            println("$s, ")
        }
        println("")

        println(dbArrays.size)

    }
    array_test()

    println("for and iteration")

    fun loop_ex(){
        val array= arrayOf("Hello","this","is","kotlin")
        for (a in array)
            print("$a")
        println("")

        // fun UIntArray.withIndex() : Iterable<IndexedValue<UInt>>
        // return indexedvalue containing the index of that element and the element itself
        for((idx, a) in array.withIndex())
            print("($idx,$a)")
        println("")

        for (i in 1..10)
            print("$i ")
        println("")

        for(i in 'a' ..'f')
            print("$i ")
        println("")

        for(i in 1..10 step 2)
            print("$i ")
        println("")

        // forEach : fun IntArray.forEach(action: (Int) ->Unit)
        // return this
        (10 downTo 1).forEach{
            print("$it ")
        }
        println("")

        var i=0
        while(i<10){
            i++
            print("$i ")
        }
        println("")



    }
    loop_ex()


    println("function")

    fun myFunc(arg1: Int, arg2: String ="default", arg3:Int=10){
        println("$arg1,$arg2,$arg3")
    }
    fun sumFunc(a: Int, b:Int)=a+b
    fun Func_test(){
        myFunc(1,"hello",5)
        myFunc(arg1=2)
        myFunc(2,arg3=5)

        fun localFunc(a:Int) :Int {
            return a+10
        }
        println(sumFunc(1,2))
        println(localFunc(10))
    }

    Func_test()

    println("collections")

    fun col_test(){
        val array= arrayOf(1,2,3)
        val arrayList=array.toMutableList()
        val list= listOf(1,2,3)
        val mutableList=list.toMutableList()
        val set=setOf(1,2,3,3)
        val mutableSet =set.toMutableSet()
        val map = mapOf("one" to 1,"two" to 2, "three" to 3)
        val mutableMap =map.toMutableMap()

        arrayList.add(4)
        arrayList[arrayList.lastIndex]++
        mutableList.add(4)
        mutableList[0]=0
        mutableSet.add(4)
        mutableMap["four"]=4

        println(arrayList)
        println(mutableList)
        println(mutableSet)
        println(mutableMap)
    }

    col_test()

    println("exception")

    fun exception_ex(){
        val x=try{
            parseInt("10")
        }catch(e :NFE){
            0
        }
    }
    exception_ex()

    println("null safety")

    fun testNUll(arg: String?){
        println(arg?.toUpperCase())
        println(arg?.toUpperCase() ?: "-")
    }

    fun testNULl2(){
        // type 에 ?를 붙임으로서 null 이 가능한 변수임을 명시적 표현
        var nullable:String? =null
        var nonNUllable:String="nonNUllable"

        testNUll(nonNUllable)
        testNUll(nullable)

        // type 에 ?를 붙임으로서 null 이 가능한 변수임을 명시적 표현
        // null 를 안전하게 처리하기 위해 --> if(s!=null) s.UpperCase() else null
        nullable?.toUpperCase()
        try{
            // 강제로 null 이 아님을 선언한다. not null 로 인식하여 처리하도록 함
            nullable!!.toUpperCase()
        }catch (e : NullPointerException){
            println("NUllpointerException")
        }

    }

    testNULl2()

    println("when")

    fun when_test(arg :Any){
        when(arg){
            10->println("10")
            in 0..9->println("0<=x<=9")
            is String ->println("Hello, $arg")
            !in 0..100 ->println("x<10 and x>100")
            else ->{
                println("unknown")
            }
        }
    }

    fun when_test2(arg :Int) :Int
    {
        return when(arg){
            in 0..9 ->10
            in 10..19 ->20
            in 20..29 ->30
            else ->40
        }
    }

    fun when_final(){
        when_test(10)
        when_test(5)
        when_test("String")
        when_test(200)
        when_test(50)

        println(when_test2(15))
        println(when_test2(50))
    }
    when_final()

    // lambda 식은 function에 function을 전달하고 , 이를 콜하게 하는 것을 말한다.

    fun lambdaTest(a :(Int) ->Int) : Int{
        return a(10)
    }

    fun lambda2(){
        val sum={x:Int,y:Int->x+y}
        println(sum(10,20))

        val array= arrayOf(MyClass(10,"class1"),MyClass(20,"class2"),MyClass(30,"class3"))
        println(array.filter({c:MyClass ->c.a<15}))
        array.filter(){c:MyClass ->c.a <15}
        array.filter{c:MyClass->c.a <15}
        array.filter{c->c.a<15}
        array.filter{it.a<15}
        print(lambdaTest { it+10 })

        val title="Num: "
        val list =listOf(1,2,3,4)
        list.forEach{println("$title $it")}
    }



}



```

