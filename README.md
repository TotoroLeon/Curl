/**
在webbrowser的PHP-CGI模式下，至少需要2个PHP独立端口来完成任务。
一个的话，就是自己把自己阻塞死掉。

CURL HTTP: post/get

Todo:
1, cookie
2, session


TODO:
1, 判断POST是否是上传的 getPostData 方法，要增加 递归方式进行检查
2, 添加COOKIE变量


ChangeLog:
2014-01-26
   1) 自动判断POST变量，使其兼容 @ 性能更好。只有本地文件存在的情况下，才会post形式发送文件，否则仅仅发送变量
   2) 增加500之类的调试，需要开启 IS_DEBUG_CURL

Example 1: Force request the special ip, ignore local hosts file, dns server.
$target_ip = '1.111.211.110';
$url = 'http://p.klzxbf.com/so/acton.php?id=7923&pass=frame3232#fome232323';
$params = array('my' => '1st parameter', 'second' => '1');
$content = CurlCli::factory()->fake_ip('8.8.8.4')->force_ip($target_ip)->get($url, $params, 'http://www.baidu.com/?kw=chinaMobile');
Exmaple 2: Upload file

$target_ip = '127.0.0.1';
$url = 'http://localhost/upload.php';
$params = array(
    'gg' => " My is GG value&sdf=ynf%20%%20\r\nNew Line By system.",
    'save' => 'leap.php',
    'att' => "@test_dirlist.php"
);

// multiple attachment
$params = array(
    'pictures[0]' => "@cat.jpg",
    'pictures[1]' => "@dog.jpg"
);


$content = CurlCli::factory()->fake_ip('8.8.8.4')->force_ip($target_ip)->post($url, $params, 'http://www.baidu.com/?kw=chinaMobile');
print_r($content);

cookie file format:

Domain\tHttpOnly\tPath\tSecure\tExpire\tCookieName\tCookieValue\n

* @author redblade
*
*/
