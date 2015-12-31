# 高性能JavaScript DOM编程以及重排与重绘

<http://developer.51cto.com/art/201508/488053.htm>

> 我们知道，DOM是用于操作XML 和HTML文档的应用程序接口，用脚本进行DOM操作的代价很昂贵。有个贴切的比喻，把DOM和JavaScript（这里指ECMScript）各自想 象为一个岛屿，它们之间用收费桥梁连接，ECMAScript每次访问DOM，都要途径这座桥，并交纳“过桥费”,访问DOM的次数越多，费用也就越高。 因此，推荐的做法是尽量减少过桥的次数，努力待在ECMAScript岛上。我们不可能不用DOM的接口，那么，怎样才能提高程序的效率？
