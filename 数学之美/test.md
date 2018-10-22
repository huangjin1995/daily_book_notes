

如何验证模型的效果？(数据量太小，验证效果不可信？)  
1).   
2).   




https://github.com/observerss/textfilter/blob/master/keywords
https://github.com/dongxiexidian/Chinese/tree/master/%E6%95%8F%E6%84%9F%E8%AF%8D%E5%BA%93

过滤的几种方法：  
1). 布尔值过滤  
a). 字符逐一比较  
f = DFAFilter()
f.add("sexy")
f.filter("hello sexy baby")
'hello **** baby'
b). 整个字符是否在字符串中  
"hello sexy baby".replace('sexy','****') if 'sexy' in "hello sexy baby" else 'hello sexy baby'
'hello **** baby'

2). 先分词，再布尔值过滤
长脏字和短脏字  


