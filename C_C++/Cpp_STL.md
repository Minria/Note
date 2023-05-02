# String
|构造函数|解释|
|---|---|
|string()|构造一个空的string对象|
|string(const char*s)|使用C语言的字符串来构造string对象|
|string(size_t n, char c)|string对象包含n个c|
|string(const string&s)|拷贝函数构造|


|常见api|解释|
|---|---|
|size|返回有效长度|
|length|返回有效长度|
|capacity|返回空间长度|
|empty|判空|
|clear|清空有效长度|
|reserve|为字符串预留多少空间|
|resize|将有效字符增加，多的用c填空|