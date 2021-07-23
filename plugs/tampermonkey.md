# 油猴插件开发

Thief Book的小功能

快捷键说明: 

➡ 下一页
⬅ 上一页
空格 老板键
~ 续航键

5秒钟如果没有按续航见，自动返回原页面

[Thief-book.js](thief-book.js)
```js
// ==UserScript==
// @name         Thief Book
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       yang bin
// @match        https://jira.mspbots.ai/**
// @Resource     https://
// @grant GM_setValue
// @grant GM_getValue
// ==/UserScript==
var book = null;
var source = null;
var flag = 1;
(function($) {
    'use strict';
    function init(){
        $('#page_line').val(GM_getValue('line'))
        $('#book_url').val(GM_getValue('bookname'))
        source = $('.user-content-block').html();
        book = GM_getValue(GM_getValue('bookname'),null)
        if (book == null){
            $.get(GM_getValue('bookname'),function(data){
                handlerData(data)
                GM_setValue(GM_getValue('bookname'),book);
            })
        }

    }
    function show(text){
        var aux = '<br/><a>https://teams.microsoft.com/l/message/19:3df5eb4ce7d04613adc50f3fd5e337a9@thread.skype/1623871505352?tenantId=a2af9d71-95f1-4236-be2c-c105ab9b7ee9&groupId=1ce5732c-8bbb-4314-b09e-833dce72554b&parentMessageId=1623871505352&teamName=MSPbots.ai&channelName=Bug%20Report%20and%20Feature%20Requests&createdTime=1623871505352</a>'
        $('.user-content-block').html(text)
    }

    function handlerData(data){
        book = data.split('\n')
    }

    function handle(){
        show(book[GM_getValue('line')])
    }

    function turnPage(num){
        var line = GM_getValue('line')
        $('#page_line').val(line)
        if( line>= book.length || line < 0){
            return;
        }
        var page = GM_getValue('line',0)
        GM_setValue('line',Number(page)+Number(num));
    }

    unsafeWindow.jump = function(){
        GM_setValue('line',Number($('#page_line').val()));
        handle();
    }
    unsafeWindow.loadbook = function(){
        var bookname = $('#book_url').val()
        console.log(bookname)
        GM_setValue('bookname',bookname)
        init()
    }
    document.onkeydown = function(e) {
        var k = e.keyCode;
        console.log(k)
        switch(k) {
            case 37:
                turnPage(-1)
                handle()
                flag=2
                break;
            case 39:
                turnPage(1)
                handle()
                flag=2
                break;
            case 32:
                show(source)
                break
            case 192:
                flag=3
        }
    }

    function checkTask(){
        if(flag == 2){
          show(source)
          flag=1
        }else if(flag == 3){
           flag = 2
        }
    }

    //$(document.body).append("<div id='ctrl-box' style='position:fixed;bottom:0;right:0'> <input id='page_line' style='width:35px' type='number'/> <input type='button' value='跳转' onclick='window.jump()'/> </div>");
    $(document.body).append('<div class="tool" draggable="true" style="background-color: #add;border: solid 1px #c3c3c3;position: fixed;top: 200px;right: 0;display: flex;justify-content: flex-end;align-items: center;"><div id="flip" style="writing-mode:vertical-lr;padding: 5px;text-align: center;cursor:pointer;">Book</div><div id="panel" style="padding: 5px;display: none;text-align: left;"> <div>书籍链接: <input type="text" name="" id="book_url"> <button onclick="loadbook()">加载</button></div> <div>跳转行数: <input id="page_line" type="number"/> <input type="button" value="跳转" onclick="window.jump()"/></div></div><script>$(document).ready(function () {$("#flip").click(function () {$("#panel").toggle();});});movetool = function (e){$(".tool").css("top",e.clientY + "px")};document.ondragend = movetool;</script></div>');

    window.onload=init();
    setInterval(function(){ checkTask() }, 4000);

})(jQuery);

```