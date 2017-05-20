---
layout: post
title: jekyll-now に Google Analytics のトラッキングコード入れる時に勘違いしていたこと
---
GA ( Google Analytics )の勉強も兼ねて、本ブログにトラッキングコードを設定しようと思ったんだが、ちょっと間違えてしまったので、備忘録としてメモ。

<!-- more -->
### _includes/analytics.html をいじらず _config.yml をいじろう  
GA を設定しようとしてまず目に飛び込んできたのが、```_includes/analytics.html```  
ソースの中はこんな感じ。  
```  
<!-- Google Analytics -->
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', '{{ site.google_analytics }}', 'auto');
  ga('send', 'pageview', {
    'page': '{{ site.baseurl }}{{ page.url }}',
    'title': '{{ page.title | replace: "'", "\\'" }}'
  });
</script>
<!-- End Google Analytics -->  
```  
なんとまぁ、ここに「トラッキングコードを入れなさいよ」と言わんばかりの内容。初見だとまず間違える。  
実際、ここにトラッキングコード設定して更新しても、実際のページにはトラッキングコードが出てこない。はて？？

#### _config.yml を見てみる  
で、なんでやろと思っていたら
```   
# Enter your Google Analytics web tracking code (e.g. UA-2110908-2) to activate tracking
google_analytics:
```  
こんなところに、なんともご丁寧に用意して待っていてくれていたではないか。  

ということで、ここにトラッキングコード設定して反映したら、ちゃんと設定できてましたとさ。  

_includesディレクトリ内のファイルはあまりユーザーに触らせずに、configで完結するようにしてくれているのでしょう。  
なんにせよ、これにて一件落着でした。
