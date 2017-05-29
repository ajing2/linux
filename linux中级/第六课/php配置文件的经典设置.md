<html lang="en"><head>
    <meta charset="UTF-8">
    <title></title>
<style id="system" type="text/css">h1,h2,h3,h4,h5,h6,p,blockquote {    margin: 0;    padding: 0;}body {    font-family: "Helvetica Neue", Helvetica, "Hiragino Sans GB", Arial, sans-serif;    font-size: 13px;    line-height: 18px;    color: #737373;    margin: 10px 13px 10px 13px;}a {    color: #0069d6;}a:hover {    color: #0050a3;    text-decoration: none;}a img {    border: none;}p {    margin-bottom: 9px;}h1,h2,h3,h4,h5,h6 {    color: #404040;    line-height: 36px;}h1 {    margin-bottom: 18px;    font-size: 30px;}h2 {    font-size: 24px;}h3 {    font-size: 18px;}h4 {    font-size: 16px;}h5 {    font-size: 14px;}h6 {    font-size: 13px;}hr {    margin: 0 0 19px;    border: 0;    border-bottom: 1px solid #ccc;}blockquote {    padding: 13px 13px 21px 15px;    margin-bottom: 18px;    font-family:georgia,serif;    font-style: italic;}blockquote:before {    content:"C";    font-size:40px;    margin-left:-10px;    font-family:georgia,serif;    color:#eee;}blockquote p {    font-size: 14px;    font-weight: 300;    line-height: 18px;    margin-bottom: 0;    font-style: italic;}code, pre {    font-family: Monaco, Andale Mono, Courier New, monospace;}code {    background-color: #fee9cc;    color: rgba(0, 0, 0, 0.75);    padding: 1px 3px;    font-size: 12px;    -webkit-border-radius: 3px;    -moz-border-radius: 3px;    border-radius: 3px;}pre {    display: block;    padding: 14px;    margin: 0 0 18px;    line-height: 16px;    font-size: 11px;    border: 1px solid #d9d9d9;    white-space: pre-wrap;    word-wrap: break-word;}pre code {    background-color: #fff;    color:#737373;    font-size: 11px;    padding: 0;}@media screen and (min-width: 768px) {    body {        width: 748px;        margin:10px auto;    }}</style><style id="custom" type="text/css"></style></head>
<body marginheight="0"><h3>配置disable_function</h3>
<p>disable_functions = eval,assert,popen,passthru,escapeshellarg,escapeshellcmd,passthru,exec,system,chroot,scandir,chgrp,chown,escapeshellcmd,escapeshellarg,shell_exec,proc_get_status,ini_alter,ini_restore,dl,pfsockopen,openlog,syslog,readlink,symlink,leak,popepassthru,stream_socket_server,popen,proc_open,proc_close

</p>
<p><strong> 说明：php中有非常多的函数，我们可以禁止掉：exec, shell_exec都是可以执行linux shell命令的，很危险 </strong>

</p>
<h3>配置error_log</h3>
<p>display_errors=off<br>log_errors=on<br>error_log=/export/servers/php/logs/error.log<br>error_reporting = E_ALL | E_STRICT

</p>
<p><strong> php错误日志级别： </strong><br>; E_ALL             所有错误和警告（除E_STRICT外）<br>; E_ERROR           致命的错误。脚本的执行被暂停。<br>; E_RECOVERABLE_ERROR    大多数的致命错误。<br>; E_WARNING         非致命的运行时错误，只是警告，脚本的执行不会停止。<br>; E_PARSE            编译时解析错误，解析错误应该只由分析器生成。<br>; E_NOTICE          脚本运行时产生的提醒（往往是我们写的脚本里面的一些bug，比如某个变量没有定义），这个错误不会导致任务中断。<br>; E_STRICT          脚本运行时产生的提醒信息，会包含一些php抛出的让我们要如何修改的建议信息。<br>; E_CORE_ERROR      在php启动后发生的致命性错误<br>; E_CORE_WARNING    在php启动后发生的非致命性错误，也就是警告信息<br>; E_COMPILE_ERROR    php编译时产生的致命性错误<br>; E_COMPILE_WARNING  php编译时产生的警告信息<br>; E_USER_ERROR       用户生成的错误<br>; E_USER_WARNING    用户生成的警告<br>; E_USER_NOTICE      用户生成的提醒<br>&amp; 表示并且<br>~ 表示非<br>| 表示或者<br>比如： error_reporting  =  E_ALL &amp; ~E_NOTICE  表示错误级别为E_ALL 并且除了E_NOTICE   

</p>
<h3>配置open_basedir</h3>
<p>php.ini: open_basedir = /dir1/:/dir2<br>httpd.conf: php_admin_value open_basedir "/dir1/:/dir2/"<br>这两个都是针对的解析php文件的，写一个简单的html可不行
Edit By <a href="http://mahua.jser.me">MaHua</a></p>
</body></html>