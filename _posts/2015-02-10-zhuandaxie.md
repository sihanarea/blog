---
layout: post
title: js金额转大写
category : js
tagline: "js"
tags : [js, 金额转大写]
---
{% include JB/setup %}

##js金额转大写
####这个东西之前在朗特威做后台合同的时候有，那时不会弄，网上找的都不知道怎么弄。现在知道了，弄了一个下来。放在这里做demo，以后要用的话直接拿来用了。
<pre><code class="prettyprint linenums">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head lang="en"&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;input type="text" placeholder="请输入正整数"/&gt;
&lt;p&gt;&lt;/p&gt;
&lt;/body&gt;
&lt;script&gt;
    function digit_uppercase(n) {

        var digit = [

            '零', '壹', '贰', '叁', '肆',

            '伍', '陆', '柒', '捌', '玖'

        ];

        var unit = [

            ['元', '万', '亿'],

            ['', '拾', '佰', '仟']

        ];
        var s = '';

        for (var i = 0; i &lt; unit[0].length &amp;&amp; n &gt; 0; i++) {

            var p = '';

            for (var j = 0; j &lt; unit[1].length &amp;&amp; n &gt; 0; j++) {

                p = digit[n % 10] + unit[1][j] + p;

                n = Math.floor(n / 10);

            }

            s = p.replace(/(零.)*零$/, '')

                    .replace(/^$/, '零')

            + unit[0][i] + s;

        }

        return s.replace(/(零.)*零元/, '元')

                        .replace(/(零.)+/g, '零')

                        .replace(/^$/, '零元') + '整';

    }

    var oInput =  document.getElementsByTagName("input")[0];
    var oP =  document.getElementsByTagName("p")[0];

    oInput.onkeyup = function(){
        oP.innerHTML = digit_uppercase(oInput.value);
    }

&lt;/script&gt;
&lt;/html&gt;</code></pre>

