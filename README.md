# Snort源码分析
因为前一段时间接触到了snort这个东西，为了能够更好的理解和使用它，这里写一点儿简单的源码分析。为了避免陷入代码细节导致无法自拔的情况，分析的过程中的代码片段会省略一部分或者直接用文字描述代替。

笔者个人的水平有限，如果发现有什么不对的地方或者是一些问题，欢迎提交pr或者是issue进行交流和沟通。文章本身是通过之前分析的笔记整理后编写的，目前仅完成五章，后续会继续更新。

[0x00_snort基础知识介绍](https://github.com/EggUncle/SnortSourceCodeAnalyze/blob/master/0x00_snort%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86%E4%BB%8B%E7%BB%8D.md)

[0x01_启动与运行](https://github.com/EggUncle/SnortSourceCodeAnalyze/blob/master/0x01_%E5%90%AF%E5%8A%A8%E4%B8%8E%E8%BF%90%E8%A1%8C.md)

[0x02_插件加载](https://github.com/EggUncle/SnortSourceCodeAnalyze/blob/master/0x02_%E6%8F%92%E4%BB%B6%E5%8A%A0%E8%BD%BD.md)

[0x03_规则解析](https://github.com/EggUncle/SnortSourceCodeAnalyze/blob/master/0x03_%E8%A7%84%E5%88%99%E8%A7%A3%E6%9E%90.md)

[0x04_数据包捕获](https://github.com/EggUncle/SnortSourceCodeAnalyze/blob/master/0x04_%E6%95%B0%E6%8D%AE%E5%8C%85%E6%8D%95%E8%8E%B7.md)
