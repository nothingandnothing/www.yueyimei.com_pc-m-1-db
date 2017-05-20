#说明
www.yueyimei.com和m.yueyimei.com使用dedecms系统,双后台，共用一个数据库。

##1、使用dede分别搭建www.yueyimei.com和m.yueyimei.com后台##
###m.yueyimei.com焦点图制作###
关于焦点图文件主要有:
*/dede/focus_add.php;
*/dede/focus_edit.php;
*/dede/focus_main.php;
*/dede/focus_type.php;
和
*/dede/templets/focus_add.htm;
*/dede/templets/focus_edit.htm;
*/dede/templets/focus_main.htm;
*/dede/templets/focus_type.htm;
在数据库中添加表：
focus和focustype;
将php文件指向的数据库名指向已经添加的focus和focustype表;
在/dede/inc/inc_menu_module.php 辅助插件中添加

$plusset

<m:item name='焦点图' link='focus_main.php' rank='10' target='main' />

添加焦点图并链接到focus_main.php;
在/include/extend.func.php文件中加入代码：
<pre><code>
function focuswz($id) {
global $dsql ;
if($id==0) {
$string ="无效参数";
} else {
$row1 = $dsql->GetOne("SELECT catid FROM #@__focus where id=$id");
}
return str_replace(',', '|', $row1['catid']);;
}//don
</code></pre>

###数据连接###
修改/data/common.inc.php配置参数：
$cfg_dbhost = '服务器名';
$cfg_dbname = '数据库名称';
$cfg_dbuser = '账号';
$cfg_dbpwd = '密码';
$cfg_dbprefix = '数据库前缀';
$cfg_db_language = 'utf8';

###在系统参数中添加移动端的全局参数###