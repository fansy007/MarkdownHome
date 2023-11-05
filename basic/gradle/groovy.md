#basic #java 
[[Gradle 2023#Groovy]]
# MOP

class A {
    int a
    void printA() {
        println a
    }
}
new A(a:1).printA()   // [a:1]的缩写

MOP调用,groovy用的是动态调用
def a = new A(a:1)
invokeMethod(a,'printA',[])

map式调用
a\['printA'\]()

---
