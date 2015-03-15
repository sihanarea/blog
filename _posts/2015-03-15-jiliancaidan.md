---
layout: post
title: js级联菜单
category : js
tagline: "js"
tags : [js, 级联菜单]
---
{% include JB/setup %}
<html lang="en"><head>
    <meta charset="UTF-8">
    <title></title>
<style id="system" type="text/css">h1,h2,h3,h4,h5,h6,p,blockquote {    margin: 0;    padding: 0;}body {    font-family: "Helvetica Neue", Helvetica, "Hiragino Sans GB", Arial, sans-serif;    font-size: 13px;    line-height: 18px;    color: #737373;    margin: 10px 13px 10px 13px;}a {    color: #0069d6;}a:hover {    color: #0050a3;    text-decoration: none;}a img {    border: none;}p {    margin-bottom: 9px;}h1,h2,h3,h4,h5,h6 {    color: #404040;    line-height: 36px;}h1 {    margin-bottom: 18px;    font-size: 30px;}h2 {    font-size: 24px;}h3 {    font-size: 18px;}h4 {    font-size: 16px;}h5 {    font-size: 14px;}h6 {    font-size: 13px;}hr {    margin: 0 0 19px;    border: 0;    border-bottom: 1px solid #ccc;}blockquote {    padding: 13px 13px 21px 15px;    margin-bottom: 18px;    font-family:georgia,serif;    font-style: italic;}blockquote:before {    content:"C";    font-size:40px;    margin-left:-10px;    font-family:georgia,serif;    color:#eee;}blockquote p {    font-size: 14px;    font-weight: 300;    line-height: 18px;    margin-bottom: 0;    font-style: italic;}code, pre {    font-family: Monaco, Andale Mono, Courier New, monospace;}code {    background-color: #fee9cc;    color: rgba(0, 0, 0, 0.75);    padding: 1px 3px;    font-size: 12px;    -webkit-border-radius: 3px;    -moz-border-radius: 3px;    border-radius: 3px;}pre {    display: block;    padding: 14px;    margin: 0 0 18px;    line-height: 16px;    font-size: 11px;    border: 1px solid #d9d9d9;    white-space: pre-wrap;    word-wrap: break-word;}pre code {    background-color: #fff;    color:#737373;    font-size: 11px;    padding: 0;}@media screen and (min-width: 768px) {    body {        width: 748px;        margin:10px auto;    }}</style><style id="custom" type="text/css"></style></head>
<body marginheight="0"><h2>js级联菜单</h2>
<h4>写个demo</h4>
<pre><code class="lang-javascript">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head lang="en"&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;script&gt;
   window.onload = function(){
        var s1 = new Sel('div1');
        s1.add('0',['1','2','3']);
        s1.add('0-1',['1-1','1-2','1-3']);

        s1.add('0-1-1',['1-1-1','1-1-2','1-1-3']);
        s1.add('0-1-2',['1-2-1','1-2-2','1-2-3']);
        s1.add('0-1-3',['1-3-1','1-3-2','1-3-3']);


        s1.add('0-2',['2-1','2-2','2-3']);

        s1.add('0-2-1',['2-1-1','2-1-2','2-1-3']);
        s1.add('0-2-2',['2-2-1','2-2-2','2-2-3']);
        s1.add('0-2-3',['2-3-1','2-3-2','2-3-3']);


        s1.add('0-3',['3-1','3-2','3-3']);

        s1.add('0-3-1',['3-1-1','3-1-2','3-1-3']);
        s1.add('0-3-2',['3-2-1','3-2-2','3-2-3']);
        s1.add('0-3-3',['3-3-1','3-3-2','3-3-3']);

        s1.init(3);
    };

    /*构造函数*/
    function Sel(id){
        this.oParent = document.getElementById(id);
        this.data = {};
        this.aSel = this.oParent.getElementsByTagName('select');
    }

    Sel.prototype = {
        /*初始化方法*/
        init:function(num){
            /*创建select*/
            var _this = this;
            for(var i=1;i&lt;=num;i++){
                var oSel = document.createElement('select');
                var oPt = document.createElement('option');
                oPt.innerHTML ='默认';
                oSel.appendChild(oPt);
                oSel.index = i;
                this.oParent.appendChild(oSel);

                oSel.onchange = function(){
                    _this.change(this.index);
                }
            }

            this.first();
        },

        /*添加数据*/
        add:function(key,value){
            this.data[key]  = value;
        },

        /*第一个下拉菜单*/
        first:function(){
            var arr = this.data['0'];
            for(var i = 0,len = arr.length;i&lt;len;i++){
                var oPt = document.createElement('option');
                oPt.innerHTML = arr[i];
                this.aSel[0].appendChild(oPt);
            }
        },

        /*改变后面的级联菜单*/
        change:function(iNow){
            var str = '0';
            for(var i = 0;i&lt;iNow;i++){
                  str +='-' + (this.aSel[i].selectedIndex);
            }
            if(this.data[str]) {
                var arr = this.data[str];
                this.aSel[iNow].options.length = 1;
                for (var i = 0; i &lt; arr.length; i++) {
                    var oPt = document.createElement('option');
                    oPt.innerHTML = arr[i];
                    this.aSel[iNow].appendChild(oPt);
                 }
                this.aSel[iNow].options[1].selected = true;
                iNow++;
                if(iNow &lt; this.aSel.length){
                    this.change(iNow);
                }
            }else{
                if(iNow &lt; this.aSel.length){
                    this.aSel[iNow].options.length = 1;
                }
            }
        }
    }
&lt;/script&gt;
&lt;body&gt;
&lt;div id="div1"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
</body></html>