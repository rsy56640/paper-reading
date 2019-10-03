# [The anatomy of a large-scale hypertextual Web search engine](http://snap.stanford.edu/class/cs224w-readings/Brin98Anatomy.pdf) 论文学习笔记

倒排索引：word -> docs (附带 score)

搜索时做 multiway-sort-merge-join，并计算 pagerank

相关度：hyperlink + NLP

crawl 的时候可以通过 mapreduce 做倒排索引，并计算一些元数据。query 时做 join，计算 pagerank。

PageRank：入边的累积，自己的 rank 平分给出边（马氏链？）；另外还要考虑 doc 的质量，真实性，等等


## Reference

- [Paper Review: The Anatomy of a Large-Scale Hypertextual Web Search Engine](https://sookocheff.com/post/databases/google/)
- [The Original Google Algorithm & Research Papers](https://www.diamondpillar.com/blog/original-google-algorithm-research-papers)
- [A REVIEW OF “THE ANATOMY OF A LARGE-SCALE HYPERTEXTUAL WEB SEARCH ENGINE” BY SERGEY BRIN AND LAWRENCE PAGE](https://leesynkowski.wordpress.com/2014/02/14/a-review-of-the-anatomy-of-a-large-scale-hypertextual-web-search-engine-by-sergey-brin-and-lawrence-page/)
- [How Google Went From School Project to Global Phenomenon](https://www.inc.com/walter-isaacson/how-google-got-its-start.html)
- [student summary: The Anatomy of a Large-Scale Hypertextual Web Search Engine](https://www.cc.gatech.edu/projects/disl/courses/cs8803/summary/Week2_1.1.pdf)