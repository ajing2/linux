
以下每个指令的设定值都与 PHP-5.2.0 内建的默认值相同。
也就是说，如果''php.ini''不存在，或者你删掉了某些行，默认值与之相同。


[Apache]

仅在将PHP作为Apache模块时才有效。

　　
engine = On

是否启用PHP解析引擎。
可以在httpd.conf中基于目录或者虚拟主机来打开或者关闭PHP解析引擎。


last_modified = Off

是否在Last-Modified应答头中放置该PHP脚本的最后修改时间。


xbithack = Off


　　是否不管文件结尾是什么，都作为PHP可执行位组来解析。
　　
　　
child_terminate = Off


　　PHP脚本在请求结束后是否允许使用apache_child_terminate()函数终止子进程。该指令仅在UNIX平台上将PHP安装为Apache1.3的模块时可用。其他情况下皆不存在。
　　
　　


## PHP核心



[PHP-Core-DateTime]


前四个配置选项目前仅用于date_sunrise()和date_sunset()函数。


date.default_latitude = 31.7667

默认纬度

date.default_longitude = 35.2333

默认经度

date.sunrise_zenith = 90.583333

默认日出天顶

date.sunset_zenith = 90.583333

默认日落天顶

date.timezone =

未设定TZ环境变量时用于所有日期和时间函数的默认时区。
中国大陆应当使用"PRC"
应用时区的优先顺序为：
1. 用date_default_timezone_set()函数设定的时区(如果设定了的话)
2. TZ 环境变量(如果非空的话)
3. 该指令的值(如果设定了的话)
4. PHP自己推测(如果操作系统支持)
5. 如果以上都不成功，则使用 UTC

[PHP-Core-Assert]

assert.active = On


是否启用assert()断言评估

assert.bail = Off

是否在发生失败断言时中止脚本的执行

assert.callback =


发生失败断言时执行的回调函数

assert.quiet_eval = Off

是否使用安静评估(不显示任何错误信息，相当于error_reporting=0)。
若关闭则在评估断言表达式的时候使用当前的error_reporting指令值。

assert.warning = On

是否对每个失败断言都发出警告

[PHP-Core-SafeMode]

安全模式是为了解决共享服务器的安全问题而设立的。
但试图在PHP层解决这个问题在结构上是不合理的，
正确的做法应当是修改web服务器层和操作系统层。
因此在PHP6中废除了安全模式，并打算使用open_basedir指令取代之。

safe_mode = Off

SYS
是否启用安全模式。
打开时，PHP将检查当前脚本的拥有者是否和被操作的文件的拥有者相同，
相同则允许操作，不同则拒绝操作。

safe_mode_gid = Off

SYS
在安全模式下，默认在访问文件时会做UID比较检查。
但有些情况下严格的UID检查反而是不适合的，宽松的GID检查已经足够。
如果你想将其放宽到仅做GID比较，可以打开这个参数。

safe_mode_allowed_env_vars = "PHP_"

　 SYS
在安全模式下，用户仅可以更改的环境变量的前缀列表(逗号分隔)。
允许用户设置某些环境变量，可能会导致潜在的安全漏洞。
注意: 如果这一参数值为空，PHP将允许用户更改任意环境变量！

safe_mode_protected_env_vars = "LD_LIBRARY_PATH"

　　SYS
在安全模式下，用户不能更改的环境变量列表(逗号分隔)。
这些变量即使在safe_mode_allowed_env_vars指令设置为允许的情况下也会得到保护。

safe_mode_exec_dir = "/usr/local/php/bin"

SYS
在安全模式下，只有该目录下的可执行程序才允许被执行系统程序的函数执行。
这些函数是：system, escapeshellarg, escapeshellcmd, exec, passthru,proc_close, proc_get_status, proc_nice, proc_open, proc_terminate, shell_exec

safe_mode_include_dir =

　　SYS
在安全模式下，该组目录和其子目录下的文件被包含时，将跳过UID/GID检查。换句话说，如果此处的值为空，任何UID/GID不符合的文件都不允许被包含。这里设置的目录必须已经存在于include_path指令中或者用完整路径来包含。
多个目录之间用冒号(Win下为分号)隔开。指定的限制实际上是一个前缀，而非一个目录名，也就是说"/dir/incl"将允许访问"/dir/include"和"/dir/incls"如果您希望将访问控制在一个指定的目录，那么请在结尾加上斜线。

sql.safe_mode = Off

SYS
是否使用SQL安全模式。
如果打开，指定默认值的数据库连接函数将会使用这些默认值代替支持的参数。对于每个不同数据库的连接函数，其默认值请参考相应的手册页面。

[PHP-Core-Safe]

allow_url_fopen = On

　　ini
是否允许打开远程文件

allow_url_include = Off

　　SYS
是否允许include/require远程文件。

disable_classes =

　　ini
该指令接受一个用逗号分隔的类名列表，以禁用特定的类。

disable_functions =

ini
该指令接受一个用逗号分隔的函数名列表，以禁用特定的函数。

enable_dl = On

　　SYS
是否允许使用dl()函数。dl()函数仅在将PHP作为apache模块安装时才有效。
禁用dl()函数主要是出于安全考虑，因为它可以绕过open_basedir指令的限制。
在安全模式下始终禁用dl()函数，而不管此处如何设置。

expose_php = On

ini
是否暴露PHP被安装在服务器上的事实(在http头中加上其签名)。
它不会有安全上的直接威胁，但它使得客户端知道服务器上安装了PHP。

open_basedir =

SYS
将PHP允许操作的所有文件(包括文件自身)都限制在此组目录列表下。
当一个脚本试图打开一个指定目录树之外的文件时，将遭到拒绝。
所有的符号连接都会被解析，所以不可能通过符号连接来避开此限制。
特殊值''.''指定了存放该脚本的目录将被当做基准目录。
但这有些危险，因为脚本的工作目录可以轻易被chdir()改变。
对于共享服务器，在httpd.conf中灵活设置该指令将变得非常有用。
在Windows中用分号分隔目录，UNIX系统中用冒号分隔目录。
作为Apache模块时，父目录中的open_basedir路径将自动被继承。
指定的限制实际上是一个前缀，而非一个目录名，
也就是说"/dir/incl"将允许访问"/dir/include"和"/dir/incls"，
如果您希望将访问控制在一个指定的目录，那么请在结尾加上一个斜线。
默认是允许打开所有文件。

[PHP-Core-Error]

error_reporting = E_ALL & ~E_NOTICE

错误报告级别是位字段的叠加，推荐使用 E_ALL | E_STRICT

1　E_ERROR　　　　　　 致命的运行时错误

2　E_WARNING　　　　　 运行时警告(非致命性错误)

4　E_PARSE　　　　　　 编译时解析错误

8　E_NOTICE　　　　　　运行时提醒(经常是bug，也可能是有意的)

16　E_CORE_ERROR　　　　PHP启动时初始化过程中的致命错误

32　E_CORE_WARNING　　　PHP启动时初始化过程中的警告(非致命性错)

64　E_COMPILE_ERROR　　 编译时致命性错

128　E_COMPILE_WARNING　 编译时警告(非致命性错)

256　E_USER_ERROR　　　　用户自定义的致命错误

512　E_USER_WARNING　　　用户自定义的警告(非致命性错误)

1024　E_USER_NOTICE　　　 用户自定义的提醒(经常是bug，也可能是有意的)

2048　E_STRICT　　　　　　编码标准化警告(建议如何修改以向前兼容)

4096　E_RECOVERABLE_ERROR 接近致命的运行时错误，若未被捕获则视同E_ERROR

6143　E_ALL　　　　　　　 除E_STRICT外的所有错误(PHP6中为8191,即包含所有)

track_errors = Off

是否在变量$php_errormsg中保存最近一个错误或警告消息。

display_errors = On
是否将错误信息作为输出的一部分显示。
在最终发布的web站点上，强烈建议你关掉这个特性，并使用错误日志代替(参看下面)。
在最终发布的web站点打开这个特性可能暴露一些安全信息，
例如你的web服务上的文件路径、数据库规划或别的信息。

display_startup_errors = Off

　　是否显示PHP启动时的错误。
即使display_errors指令被打开，关闭此参数也将不显示PHP启动时的错误。
建议你关掉这个特性，除非你必须要用于调试中。

report_memleaks = On

　　是否报告内存泄漏。这个参数只在以调试方式编译的PHP中起作用，
并且必须在error_reporting指令中包含 E_WARNING

　report_zend_debug = On
　
尚无说明文档

html_errors = On

　　是否在出错信息中使用HTML标记。
注意: 不要在发布的站点上使用这个特性！

docref_root =　;"http://localhost/phpmanual/"

docref_ext =　 ;".html"

　　如果打开了html_errors指令，PHP将会在出错信息上显示超连接，
直接链接到一个说明这个错误或者导致这个错误的函数的页面。
你可以从http://www.php.net/docs.php下载php手册，
并将docref_root指令指向你本地的手册所在的URL目录。
你还必须设置docref_ext指令来指定文件的扩展名(必须含有''.'')。
注意: 不要在发布的站点上使用这个特性。

error_prepend_string =　;"<font color=#f00>"

　　用于错误信息前输出的字符串
　　
error_append_string =　 ;"</font>"

　　用于错误信息后输出的字符串
　　
xmlrpc_errors = Off

xmlrpc_error_number = 0

尚无文档

[PHP-Core-Logging]

define_syslog_variables = Off

　　是否定义各种系统日志变量，如：$LOG_PID, $LOG_CRON 等等。
关掉它以提高效率的好主意。
你可以在运行时调用define_syslog_variables()函数来定义这些变量。

error_log =

将错误日志记录到哪个文件中。该文件必须对Web服务器用户可写。
syslog 表示记录到系统日志中(NT下的事件日志, Unix下的syslog(3))
如果此处未设置任何值，则错误将被记录到Web服务器的错误日志中。

log_errors = Off

　　是否在日志文件里记录错误，具体在哪里记录取决于error_log指令。
强烈建议你在最终发布的web站点时使用日志记录错误而不是直接输出，
这样可以让你既知道那里出了问题，又不会暴露敏感信息。

log_errors_max_len = 1024

　　设置错误日志中附加的与错误信息相关联的错误源的最大长度。
这里设置的值对显示的和记录的错误以及$php_errormsg都有效。
设为 0 可以允许无限长度。

ignore_repeated_errors = Off

　　记录错误日志时是否忽略重复的错误信息。
错误信息必须出现在同一文件的同一行才被被视为重复。

ignore_repeated_source = Off

是否在忽略重复的错误信息时忽略重复的错误源。

[PHP-Core-Mail]

　　要使邮件函数可用，PHP必须在编译时能够访问sendmail程序。
如果使用其它的邮件程序，如qmail或postfix，确保使用了相应的sendmail包装。PHP首先会在系统的PATH环境变量中搜索 sendmail，接着按以下顺序搜索：/usr/bin:/usr/sbin:/usr/etc:/etc:/usr/ucblib:/usr/lib
强烈建议在PATH中能够找到sendmail。
另外，编译PHP的用户必须能够访问sendmail程序。

SMTP = "localhost"

　　mail()函数中用来发送邮件的SMTP服务器的主机名称或者IP地址。仅用于win32。
　　
smtp_port = 25

　　SMTP服务器的端口号。仅用于win32。
　　
sendmail_from =

发送邮件时使用的"From:"头中的邮件地址。仅用于win32
该选项还同时设置了"Return-Path:"头。

sendmail_path = "-t -i"

　　SYS
仅用于unix，也可支持参数(默认的是''sendmail -t -i'')
sendmail程序的路径，通常为"/usr/sbin/sendmail或/usr/lib/sendmail"。
configure脚本会尝试找到该程序并设定为默认值，但是如果失败的话，可以在这里设定。
不使用sendmail的系统应将此指令设定为sendmail替代程序(如果有的话)。
例如，Qmail用户通常可以设为"/var/qmail/bin/sendmail"或"/var/qmail/bin/qmail-inject"。
qmail-inject 不需要任何选项就能正确处理邮件。

mail.force_extra_parameters =

作为额外的参数传递给sendmail库的强制指定的参数附加值。
这些参数总是会替换掉mail()的第5个参数，即使在安全模式下也是如此。

[PHP-Core-ResourceLimit]

default_socket_timeout = 60

默认socket超时(秒)

max_execution_time = 30

每个脚本最大允许执行时间(秒)，0 表示没有限制。
这个参数有助于阻止劣质脚本无休止的占用服务器资源。
该指令仅影响脚本本身的运行时间，任何其它花费在脚本运行之外的时间，
如用system()/sleep()函数的使用、数据库查询、文件上传等，都不包括在内。
在安全模式下，你不能用ini_set()在运行时改变这个设置。

memory_limit = 16M

一个脚本所能够申请到的最大内存字节数(可以使用K和M作为单位)。
这有助于防止劣质脚本消耗完服务器上的所有内存。
要能够使用该指令必须在编译时使用"--enable-memory-limit"配置选项。
如果要取消内存限制，则必须将其设为 -1 。
设置了该指令后，memory_get_usage()函数将变为可用。

max_input_time = -1

每个脚本解析输入数据(POST, GET, upload)的最大允许时间(秒)。
-1 表示不限制。

post_max_size = 8M

允许的POST数据最大字节长度。此设定也影响到文件上传。
如果POST数据超出限制，那么$_POST和$_FILES将会为空。
要上传大文件，该值必须大于upload_max_filesize指令的值。
如果启用了内存限制，那么该值应当小于memory_limit指令的值。

realpath_cache_size = 16K

SYS
指定PHP使用的realpath(规范化的绝对路径名)缓冲区大小。
在PHP打开大量文件的系统上应当增大该值以提高性能。

realpath_cache_ttl = 120

　　SYS
realpath缓冲区中信息的有效期(秒)。
对文件很少变动的系统，可以增大该值以提高性能。

[PHP-Core-FileUpLoad]

file_uploads = On

SYS
是否允许HTTP文件上传。
参见upload_max_filesize, upload_tmp_dir, post_max_size指令

upload_max_filesize = 2M

　　允许上传的文件的最大尺寸。
　　
upload_tmp_dir =

　　SYS
文件上传时存放文件的临时目录(必须是PHP进程用户可写的目录)。
如果未指定则PHP使用系统默认的临时目录。

[PHP-Core-MagicQuotes]

　　PHP6将取消魔术引号，相当于下列指令全部为 Off
　　
magic_quotes_gpc = On

　　是否对输入的GET/POST/Cookie数据使用自动字符串转义( ''　"　　NULL )。
这里的设置将自动影响 $_GEST $_POST $_COOKIE 数组的值。
若将本指令与magic_quotes_sybase指令同时打开，则仅将单引号('')转义为('''')，
其它特殊字符将不被转义，即( "　　NULL )将保持原样！！
建议关闭此特性，并使用自定义的过滤函数。

magic_quotes_runtime = Off

是否对运行时从外部资源产生的数据使用自动字符串转义( ''　"　　NULL )。
若打开本指令，则大多数函数从外部资源(数据库,文本文件等)返回数据都将被转义。
例如：用SQL查询得到的数据，用exec()函数得到的数据，等等---www.bianceng.cn
若将本指令与magic_quotes_sybase指令同时打开，则仅将单引号('')转义为('''')，
其它特殊字符将不被转义，即( "　　NULL )将保持原样！！
建议关闭此特性，并视具体情况使用自定义的过滤函数。

magic_quotes_sybase = Off

　　是否采用Sybase形式的自动字符串转义(用 '''' 表示 '')
　　
[PHP-Core-HighLight]

highlight.bg = "#FFFFFF"

highlight.comment = "#FF8000"

highlight.default = "#0000BB"

highlight.html = "#000000"

highlight.keyword = "#007700"

highlight.string = "#DD0000"

　　语法高亮模式的色彩(通常用于显示 .phps 文件)。
只要能被接受的东西就能正常工作。

[PHP-Core-Langue]

short_open_tag = On

　　是否允许使用""短标识。否则必须使用""长标识。
除非你的php程序仅在受控环境下运行，且只供自己使用，否则请不要使用短标记。
如果要和XML结合使用PHP，可以选择关闭此选项以方便直接嵌入""，不然你必须用PHP来输出：
本指令也会影响到缩写形式"asp_tags = Off
　　是否允许ASP风格的标记""，这也会影响到缩写形式"PHP6中将删除此指令
arg_separator.output = "&"
PHP所产生的URL中用来分隔参数的分隔符。
另外还可以用"&"或","等等。

arg_separator.input = "&"

　　PHP解析URL中的变量时使用的分隔符列表。
字符串中的每一个字符都会被当作分割符。
另外还可以用",&"等等。

allow_call_time_pass_reference = On

　　是否强迫在函数调用时按引用传递参数(每次使用此特性都会收到一条警告)。
php反对这种做法，并在将来的版本里不再支持，因为它影响到了代码的整洁。
鼓励的方法是在函数声明里明确指定哪些参数按引用传递。
我们鼓励你关闭这一选项，以保证你的脚本在将来版本的语言里仍能正常工作。

auto_globals_jit = On

是否仅在使用到$_SERVER和$_ENV变量时才创建(而不是在脚本一启动时就自动创建)。
如果并未在脚本中使用这两个数组，打开该指令将会获得性能上的提升。
要想该指令生效，必须关闭register_globals和register_long_arrays指令。

auto_prepend_file =

auto_append_file　=

指定在主文件之前/后自动解析的文件名。为空表示禁用该特性。
该文件就像调用了include()函数被包含进来一样，因此会使用include_path指令的值。
注意：如果脚本通过exit()终止，那么自动后缀将不会发生。---www.bianceng.cn
variables_order = "EGPCS"
　　PHP注册 Environment, GET, POST, Cookie, Server 变量的顺序。
分别用 E, G, P, C, S 表示，按从左到右注册，新值覆盖旧值。
举例说，设为"GP"将会导致用POST变量覆盖同名的GET变量，
并完全忽略 Environment, Cookie, Server 变量。
推荐使用"GPC"或"GPCS"，并使用getenv()函数访问环境变量。

register_globals = Off

是否将 E, G, P, C, S 变量注册为全局变量。
打开该指令可能会导致严重的安全问题，除非你的脚本经过非常仔细的检查。
推荐使用预定义的超全局变量：$_ENV, $_GET, $_POST, $_COOKIE, $_SERVER
该指令受variables_order指令的影响。
PHP6中已经删除此指令。

register_argc_argv = On

是否声明$argv和$argc全局变量(包含用GET方法的信息)。
建议不要使用这两个变量，并关掉该指令以提高性能。

register_long_arrays = On

是否启用旧式的长式数组(HTTP_*_VARS)。
鼓励使用短式的预定义超全局数组，并关闭该特性以获得更好的性能。
PHP6中已经删除此指令。

always_populate_raw_post_data = Off

是否总是生成$HTTP_RAW_POST_DATA变量(原始POST数据)。
否则，此变量仅在遇到不能识别的MIME类型的数据时才产生。
不过，访问原始POST数据的更好方法是 php://input 。
$HTTP_RAW_POST_DATA对于enctype="multipart/form-data"的表单数据不可用。

unserialize_callback_func =

　　如果解序列化处理器需要实例化一个未定义的类，
这里指定的回调函数将以该未定义类的名字作为参数被unserialize()调用，
以免得到不完整的"__PHP_Incomplete_Class"对象。
如果这里没有指定函数，或指定的函数不包含(或实现)那个未定义的类，将会显示警告信息。
所以仅在确实需要实现这样的回调函数时才设置该指令。
若要禁止这个特性，只需置空即可。

y2k_compliance = On

　　是否强制打开2000年适应(可能在非Y2K适应的浏览器中导致问题)。
　　
zend.ze1_compatibility_mode = Off

是否使用兼容Zend引擎I(PHP 4.x)的模式。
这将影响对象的复制、构造(无属性的对象会产生FALSE或0)、比较。
兼容模式下，对象将按值传递，而不是默认的按引用传递。

precision = 14

浮点型数据显示的有效位数。

serialize_precision = 100

　　将浮点型和双精度型数据序列化存储时的精度(有效位数)。
默认值能够确保浮点型数据被解序列化程序解码时不会丢失数据。

[PHP-Core-OutputControl]

　　输出控制函数很有用，特别是在已经输出了信息之后再发送HTTP头的情况下。
输出控制函数不会作用于header()或setcookie()等函数发送的HTTP头，
而只会影响类似于echo()函数输出的信息和嵌入在PHP代码之间的信息。

implicit_flush = Off

　　是否要求PHP输出层在每个输出块之后自动刷新数据。
这等效于在每个 print()、echo()、HTML块 之后自动调用flush()函数。
打开这个选项对程序执行的性能有严重的影响，通常只推荐在调试时使用。
在CLI SAPI的执行模式下，该指令默认为 On 。

output_buffering = 0

　　输出缓冲区大小(字节)。建议值为4096~8192。
输出缓冲允许你甚至在输出正文内容之后再发送HTTP头(包括cookies)。
其代价是输出层减慢一点点速度。
设置输出缓冲可以减少写入，有时还能减少网络数据包的发送。
这个参数的实际收益很大程度上取决于你使用的是什么Web服务器以及什么样的脚本。

output_handler =

　　将所有脚本的输出重定向到一个输出处理函数。
比如，重定向到mb_output_handler()函数时，字符编码将被透明地转换为指定的编码。
一旦你在这里指定了输出处理程序，输出缓冲将被自动打开(output_buffering=4096)。
注意0: 此处仅能使用PHP内置的函数，自定义函数应在脚本中使用ob_start()指定。
注意1: 可移植脚本不能依赖该指令，而应使用ob_start()函数明确指定输出处理函数。
使用这个指令可能会导致某些你不熟悉的脚本出错。
注意2: 你不能同时使用"mb_output_handler"和"ob_iconv_handler"两个输出处理函数。
你也不能同时使用"ob_gzhandler"输出处理函数和zlib.output_compression指令。
注意3: 如果使用zlib.output_handler指令开启zlib输出压缩，该指令必须为空。

[PHP-Core-Directory]

doc_root =

　　SYS
PHP的"根目录"。仅在非空时有效。
如果safe_mode=On，则此目录之外的文件一概被拒绝。
如果编译PHP时没有指定FORCE_REDIRECT，并且在非IIS服务器上以CGI方式运行，则必须设置此指令(参见手册中的安全部分)。
替代方案是使用的cgi.force_redirect指令。

include_path = ".:/path/to/php/pear"

　　指定一组目录用于require(), include(), fopen_with_path()函数寻找文件。
格式和系统的PATH环境变量类似(UNIX下用冒号分隔，Windows下用分号分隔)：
UNIX: "/path1:/path2"
Windows: "path1;path2"
在包含路径中使用''.''可以允许相对路径，它代表当前目录。

user_dir =

　　SYS
告诉php在使用 /~username 打开脚本时到哪个目录下去找，仅在非空时有效。
也就是在用户目录之下使用PHP文件的基本目录名，例如："public_html"

extension_dir = "/path/to/php"

　　SYS
存放扩展库(模块)的目录，也就是PHP用来寻找动态扩展模块的目录。
Windows下默认为"C:/php5"

[PHP-Core-HTTP]

default_mimetype = "text/html"

default_charset =　;"gb2312"

　　PHP默认会自动输出"Content-Type: text/html" HTTP头。
如果将default_charset指令设为"gb2312"，
那么将会自动输出"Content-Type: text/html; charset=gb2312"。

[PHP-Core-Unicode]

detect_unicode = On

　　尚无文档
　　
[PHP-Core-Misc]

auto_detect_line_endings = Off

　　是否让PHP自动侦测行结束符(EOL)。
如果的你脚本必须处理Macintosh文件，
或者你运行在Macintosh上，同时又要处理unix或win32文件，
打开这个指令可以让PHP自动侦测EOL，以便fgets()和file()函数可以正常工作。
但同时也会导致在Unix系统下使用回车符(CR)作为项目分隔符的人遭遇不兼容行为。

cgi.rfc2616_headers = 0

　　指定PHP在发送HTTP响应代码时使用何种报头。
0 表示发送一个"Status: "报头，Apache和其它web服务器都支持。
若设为1，则PHP使用RFC2616标准的头。
除非你知道自己在做什么，否则保持其默认值 0

cgi.nph = Off

在CGI模式下是否强制对所有请求都发送"Status: 200"状态码。

fastcgi.impersonate = Off

IIS中的FastCGI支持模仿客户端安全令牌的能力。
这使得IIS能够定义运行时所基于的请求的安全上下文。
Apache中的mod_fastcgi不支持此特性(03/17/2002)
如果在IIS中运行则设为On，默认为Off。

fastcgi.logging = On

是否记录通过FastCGI进行的连接。

[PHP-Core-Weirdy]

　　这些选项仅存在于文档中，却不存在于phpinfo()函数的输出中
　　
async_send = Off

　　是否异步发送。
　　
from =　;"john@doe.com"

　　定义匿名ftp的密码(一个email地址)
　　
　　
## 近核心模块　;;
[Pcre]

Perl兼容正则表达式模块

pcre.backtrack_limit = 100000

　PCRE的最大回溯(backtracking)步数。
　
pcre.recursion_limit = 100000

PCRE的最大递归(recursion)深度。
如果你将该值设的非常高，将可能耗尽进程的栈空间，导致PHP崩溃。

[Session]

　　除非使用session_register()或$_SESSION注册了一个变量。
否则不管是否使用了session_start()，都不会自动添加任何session记录。
包括resource变量或有循环引用的对象包含指向自身的引用的对象，不能保存在会话中。
register_globals指令会影响到会话变量的存储和恢复。

session.save_handler = "files"

　　存储和检索与会话关联的数据的处理器名字。默认为文件("files")。
如果想要使用自定义的处理器(如基于数据库的处理器)，可用"user"。
有一个使用PostgreSQL的处理器：http://sourceforge.net/projects/phpform-ext/

session.save_path = "/tmp"

传递给存储处理器的参数。对于files处理器，此值是创建会话数据文件的路径。
Windows下默认为临时文件夹路径。
你可以使用"N;[MODE;]/path"这样模式定义该路径(N是一个整数)。
N表示使用N层深度的子目录，而不是将所有数据文件都保存在一个目录下。

[MODE;]可选，必须使用8进制数，默认600(=384)，表示每个目录下最多保存的会话文件数量。
这是一个提高大量会话性能的好主意。

