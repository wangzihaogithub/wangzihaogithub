---
layout: post
title:  "大数据_Spark"
tags: 自我反思
---

###  目录
    
   1.引言
    
   2.IK-Analyzer是什么?
    
   3.实现的原理
    
   4.实现的逻辑
    
   5.附1 : 官方文档
    
   6.附2 : 项目中使用的字典


### 1.引言

全文搜索是一场 查准率 与 查全率 之间的较量   (引用百度百科: 两者关系为互逆的关系 )

   查准率即尽量返回较少的无关文档，而查全率则尽量返回较多的相关文档。 

尽管能够精准匹配用户查询的单词，但这仍然不够，我们会错过很多被用户认为是相关的文档。 因此，我们需要把网撒得更广一些，去搜索那些和原文不是完全匹配但却相关的单词。



难道你不期待在搜索“quick brown fox“时匹配到包含“fast brown foxed“的文档，或是搜索“Johnny Walker“时匹配到“Johnnie Walker“， 又或是搜索“Arnolt Schwarzenneger“时匹配到“Arnold Schwarzenegger“吗？

如果文档 确实 包含用户查询的内容，那么这些文档应当出现在返回结果的最前面，而匹配程度较低的文档将会排在靠后的位置。

如果没有任何完全匹配的文档，我们至少可以给用户展示一些潜在的匹配结果；它们甚至可能就是用户最初想要的结果。



### 2.IK-Analyzer是什么?
       IK Analyzer 是一个开源的，基于 java 语言开发的轻量级的中文分词工具包。IK 实现了简单的分词歧义排除算法，标志着 IK 分词器从单纯
的词典分词向模拟语义分词衍化。

它采用了特有的“正向迭代最细粒度切分算法“，支持细粒度和智能分词两种切分模式；


 目前是放在项目中的Elastic-search中使用.



### 3.实现的原理


分词过程 = 输入一段**文本**,  程序从某处获取**词库数据**,  运行时使用某种**数据结构**, 去执行某种**算法**, 最终获得多个**词元**



### 3.实现的逻辑

  <table class="relative-table wrapped confluenceTable" style="width: 100.0%;" data-mce-style="width: 100.0%;">
   <colgroup>
    <col style="width: 3.62776%;" data-mce-style="width: 3.62776%;" />
    <col style="width: 7.49211%;" data-mce-style="width: 7.49211%;" />
    <col style="width: 20.347%;" data-mce-style="width: 20.347%;" />
    <col style="width: 55.9937%;" data-mce-style="width: 55.9937%;" />
    <col style="width: 12.5394%;" data-mce-style="width: 12.5394%;" />
   </colgroup>
   <tbody>
    <tr>
     <th class="confluenceTh"><br /></th>
     <th class="confluenceTh">纬度</th>
     <th class="confluenceTh">说明</th>
     <th class="confluenceTh" colspan="1">示例</th>
     <th class="confluenceTh">项目中使用</th>
    </tr>
    <tr>
     <td class="confluenceTd">1</td>
     <td class="confluenceTd">词库数据</td>
     <td class="confluenceTd">扩展词字典</td>
     <td class="confluenceTd" colspan="1"><p>3W咖啡</p><p>5G卡</p><p>Python开发</p><p>新浪微博</p></td>
     <td class="confluenceTd"><span>远程存储</span></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1">停用词字典</td>
     <td class="confluenceTd" colspan="1"><p>工程师</p><p>开发</p><p>q</p><p>w</p><p>e</p></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1">同义词字典</td>
     <td class="confluenceTd" colspan="1"><p>月薪,薪资,年薪,薪酬,工资,薪水</p><p>hr,招聘,人事,人力资源,人力</p></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd">2</td>
     <td class="confluenceTd">数据结构</td>
     <td class="confluenceTd">Tire(字典树)</td>
     <td class="confluenceTd" colspan="1">
      <div class="content-wrapper">
       <p><img class="confluence-embedded-image confluence-thumbnail" title="ig-research &gt; Elastic/IK-Analyzer(介绍) &gt; 字典树.jpg" height="250" src="/images/postimg/tiretree.jpg" data-image-src="/images/postimg/tiretree.jpg" data-unresolved-comment-count="0" data-linked-resource-id="5079828" data-linked-resource-version="1" data-linked-resource-type="attachment" data-linked-resource-default-alias="字典树.jpg" data-linked-resource-content-type="image/jpeg" data-linked-resource-container-id="5079789" data-linked-resource-container-version="23" data-location="ig-research &gt; Elastic/IK-Analyzer(介绍) &gt; 字典树.jpg" data-image-height="325" data-image-width="388" /></p>
      </div></td>
     <td class="confluenceTd"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd">3</td>
     <td class="confluenceTd">算法</td>
     <td class="confluenceTd"><p>正向迭代最细粒度切分算法</p><p>算法1: 中日韩处理</p><p>算法2: 中文数字处理</p><p>算法3: 英文字符阿拉伯数字处理[步奏1英文,步奏2阿拉伯数字, 步奏3.混合字母]</p><p><br /></p><p><br /></p><p><br /></p></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span><span>处理逻辑: 普通</span>切词</span></td>
     <td class="confluenceTd" colspan="1">
      <div class="content-wrapper">
       <p><strong>假设文本为:</strong></p>
       <p>张柏芝士蛋糕旗舰店11房 fsdZ H22好</p>
       <p><br /></p>
       <p><strong>假设词库数据为:</strong></p>
       <p>扩展词:[张柏芝,张柏,芝士,蛋糕]</p>
       <p>停<span>用</span>词:[<span>旗舰店</span>]</p>
       <p><br /></p>
       <p><strong>那么数据结构则为:</strong></p>
       <p>张→ 柏(是否是词=true,默认=false)→ 芝</p>
       <p>芝→ 士</p>
       <p>蛋→ 糕</p>
       <p><br /></p>
       <p><strong>算法流程则为:</strong></p>
       <p><img class="confluence-embedded-image" title="ig-research &gt; Elastic/IK-Analyzer(介绍) &gt; image2019-6-23_16-21-11.png" height="400" src="/download/attachments/5079789/image2019-6-23_16-21-11.png?version=1&amp;modificationDate=1561278217000&amp;api=v2" data-image-src="/download/attachments/5079789/image2019-6-23_16-21-11.png?version=1&amp;modificationDate=1561278217000&amp;api=v2" data-unresolved-comment-count="0" data-linked-resource-id="5079824" data-linked-resource-version="1" data-linked-resource-type="attachment" data-linked-resource-default-alias="image2019-6-23_16-21-11.png" data-base-url="http://wiki.iterget.com" data-linked-resource-content-type="image/png" data-linked-resource-container-id="5079789" data-linked-resource-container-version="23" data-location="ig-research &gt; Elastic/IK-Analyzer(介绍) &gt; image2019-6-23_16-21-11.png" data-image-height="457" data-image-width="396" data-mce-src="http://wiki.iterget.com/download/attachments/5079789/image2019-6-23_16-21-11.png?version=1&amp;modificationDate=1561278217000&amp;api=v2" /></p>
       <p><br /></p>
       <p><strong>获得的词元为:</strong></p>
       <p>张柏芝</p>
       <p>张柏</p>
       <p>芝士</p>
       <p>蛋糕</p>
       <p>1</p>
       <p>房</p>
       <p>fsdz</p>
       <p>h</p>
       <p>好</p>
       <p><br /></p>
       <p><strong>停用词为:</strong></p>
       <p>旗舰店(输出结果时会检查是否在停用词库, 是的话不输出)</p>
       <p><br /></p>
      </div></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>处理逻辑: 歧义切词</span></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd">4</td>
     <td class="confluenceTd">词元-<span>分类</span></td>
     <td class="confluenceTd"><p>UNKNOWN=未知</p></td>
     <td class="confluenceTd" colspan="1">其他字符</td>
     <td class="confluenceTd"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd"><br /></td>
     <td class="confluenceTd"><br /></td>
     <td class="confluenceTd"><span>ENGLISH=英文</span></td>
     <td class="confluenceTd" colspan="1"><span>ascII码中的英文</span></td>
     <td class="confluenceTd"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>ARABIC=数字</span></td>
     <td class="confluenceTd" colspan="1">ascII码中的数字</td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>LETTER=英文数字混合</span></td>
     <td class="confluenceTd" colspan="1"><span>ascII码中的英文 + <span>ascII码中的数字</span></span></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>CNWORD=中文词元</span></td>
     <td class="confluenceTd" colspan="1"><p><span>UTF-8Unicode的中文词汇</span></p><p>文章末尾有下载链接</p></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>CNCHAR=中文单字</span></td>
     <td class="confluenceTd" colspan="1"><span>UTF-8Unicode的中文单字</span></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>OTHER_CJK=日韩文字</span></td>
     <td class="confluenceTd" colspan="1"><span>UTF-8Unicode的日韩文字</span></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>CNUM=中文数字 </span></td>
     <td class="confluenceTd" colspan="1"><p>[</p><p>一二两三四五六七八九十零壹贰叁肆伍陆柒捌玖拾百千万亿拾佰仟萬億兆卅廿</p><p>]</p></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>COUNT=中文量词</span></td>
     <td class="confluenceTd" colspan="1"><p>纯中文量词</p><p><a class="confluence-link" href="/download/attachments/5079789/quantifier.dic?version=1&amp;modificationDate=1561273630000&amp;api=v2" data-linked-resource-container-id="5079789" data-linked-resource-container-version="23" data-linked-resource-content-type="application/octet-stream" data-linked-resource-id="5079816" data-linked-resource-version="1" data-linked-resource-type="attachment" data-linked-resource-default-alias="quantifier.dic" data-base-url="http://wiki.iterget.com" data-mce-href="http://wiki.iterget.com/download/attachments/5079789/quantifier.dic?version=1&amp;modificationDate=1561273630000&amp;api=v2">点击下载量词词库quantifier.dic</a></p></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><span>CQUAN=中文数量词</span></td>
     <td class="confluenceTd" colspan="1">
      <div class="content-wrapper">
       <p>英文数词+中文量词</p>
       <p>2世纪</p>
       <p><a class="confluence-link" href="/download/attachments/5079789/quantifier.dic?version=1&amp;modificationDate=1561273630000&amp;api=v2" data-linked-resource-container-id="5079789" data-linked-resource-container-version="23" data-linked-resource-content-type="application/octet-stream" data-linked-resource-id="5079816" data-linked-resource-version="1" data-linked-resource-type="attachment" data-linked-resource-default-alias="quantifier.dic" data-base-url="http://wiki.iterget.com" data-mce-href="http://wiki.iterget.com/download/attachments/5079789/quantifier.dic?version=1&amp;modificationDate=1561273630000&amp;api=v2">点击下载量词词库quantifier.dic</a></p>
      </div></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
    <tr>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
     <td class="confluenceTd" colspan="1"><br /></td>
    </tr>
   </tbody>
  </table> 


| 纬度 | 说明 | 示例 | 项目中使用 | 
| :- | :- | :- | 
			
|1  |词库数据	|扩展词字典	|3W咖啡, 5G卡, Python开发, 新浪微博 | 远程存储 |
|  |	        |停用词字典	|工程师, 开发, q, w, e             |  |
|  |	        |同义词字典	|月薪,薪资,年薪,薪酬,工资,薪水  .hr,招聘,人事,人力资源,人力 |  |
|2  |数据结构	|Tire(字典树) | |  |
|3  |算法        |停用词字典	|工程师, 开发, q, w, e             |  |
|  |	        |同义词字典	|月薪,薪资,年薪,薪酬,工资,薪水  .hr,招聘,人事,人力资源,人力 |  |







		
正向迭代最细粒度切分算法

算法1: 中日韩处理

算法2: 中文数字处理

算法3: 英文字符阿拉伯数字处理[步奏1英文,步奏2阿拉伯数字, 步奏3.混合字母]






处理逻辑: 普通切词	
假设文本为:

张柏芝士蛋糕旗舰店11房 fsdZ H22好



假设词库数据为:

扩展词:[张柏芝,张柏,芝士,蛋糕]

停用词:[旗舰店]



那么数据结构则为:

张→ 柏(是否是词=true,默认=false)→ 芝

芝→ 士

蛋→ 糕



算法流程则为:

ig-research > Elastic/IK-Analyzer(介绍) > image2019-6-23_16-21-11.png



获得的词元为:

张柏芝

张柏

芝士

蛋糕

1

房

fsdz

h

好



停用词为:

旗舰店(输出结果时会检查是否在停用词库, 是的话不输出)






处理逻辑: 歧义切词	

4	词元-分类	
UNKNOWN=未知

其他字符	


ENGLISH=英文	ascII码中的英文	


ARABIC=数字	ascII码中的数字	


LETTER=英文数字混合	ascII码中的英文 + ascII码中的数字	


CNWORD=中文词元	
UTF-8Unicode的中文词汇

文章末尾有下载链接




CNCHAR=中文单字	UTF-8Unicode的中文单字	


OTHER_CJK=日韩文字	UTF-8Unicode的日韩文字	


CNUM=中文数字 	
[

一二两三四五六七八九十零壹贰叁肆伍陆柒捌玖拾百千万亿拾佰仟萬億兆卅廿

]




COUNT=中文量词	
纯中文量词

点击下载量词词库quantifier.dic




CQUAN=中文数量词	
英文数词+中文量词

2世纪

点击下载量词词库quantifier.dic












附1:官方文档

[(点我下载)IKAnalyzer中文分词器V3.0使用手册.pdf](../files/IKAnalyzer中文分词器V3.0使用手册.pdf "(点我下载)IKAnalyzer中文分词器V3.0使用手册.pdf"). 

[((点我下载)IKAnalyzer中文分词器V2012使用手册.pdf](../files/IKAnalyzer中文分词器V2012使用手册.pdf "(点我下载)IKAnalyzer中文分词器V2012使用手册.pdf"). 


附2:项目中使用的字典

扩展词字典

http://common.iterget.com/es/dict/ext_company.dic;

http://common.iterget.com/es/dict/ext_position.dic;

http://common.iterget.com/es/dict/rs_anti_company.dic;

http://common.iterget.com/es/dict/mydict.dic

http://common.iterget.com/es/dict/iterget.dic

(目前ig的新词都放在iterget.dic里)



量词字典

点击下载量词词库quantifier.dic


停用词字典

http://common.iterget.com/es/stopwords/stop_word.dic



同义词字典

http://common.iterget.com/es/synonym/company.dic

http://common.iterget.com/es/synonym/project.dic

http://common.iterget.com/es/synonym/position.dic