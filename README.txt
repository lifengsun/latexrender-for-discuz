1.用途

LaTeXRenderForDiscuz!是Crossday Discuz! Board[1]的插件，可以把Discuz!中输入的LaTeX公式转换成图片形式显示在文章中。
LaTeXRenderForDiscuz!-7.2适用于Discuz!-7.2版。

2.原理

用户在[tex][/tex]标签对之间输入LaTeX公式代码，提取此代码，查找之前是否已有此代码对应公式的图片文件生成。若没有，则将此代码按事先设定的LaTeX模板生成一个tex源文件，依次调用latex、dvips、convert，最终生成内容为代码对应公式的图片文件，返回此文件路径；若有，则直接返回图片文件路径。最后，将得到的图片文件嵌入网页中，替换原来的tex标签。

3.安装

(a) LaTeXRenderForDiscuz!依赖LaTeX[1]和ImageMagick[2]，在安装之前先确保服务器上以下四个命令可以正常运行：
latex, dvips, convert, identify

(b) 修改latexrender/class.latexrender.php的以下四行，以符合服务器的设定
var $_latex_path = '/usr/bin/latex';
var $_dvips_path = '/usr/bin/dvips';
var $_convert_path = '/usr/bin/convert';
var $_identify_path = '/usr/bin/identify';

以下假定Discuz!安装在服务器的DISCUZ目录下。

(c) 上传latexrender目录下的所有文件到服务器的DISCUZ/plugins/latexrender目录。

(d) 修改服务器端的文件DISCUZ/include/discuzcode.func.php，在第111行加入下面两行代码

require_once DISCUZ_ROOT.'plugins/latexrender/latex.php';
$message = latex_content($message);

(e) 在服务端建立目录DISCUZ/forumdata/latexrender，并在它下面建立pictures、tmp两个目录。在这三个目录下分别建立一个名为index.htm的空文件。把pictures、tmp目录的访问权限设为777。

(f) 安装完成。

4.使用说明

帖子正文中[tex]a^b[/tex]等同于一般TeX文件中输入$a^b$，[tex]$a^b$[/tex]则等同于$$a^b$$。

5.LaTeX模板的定制

见latexrender/class.latexrender.php的wrap_formula函数。

6.联系作者

Lifeng Sun <lifongsun@gmail.com>


2011.05.10



[1] http://www.discuz.net
[2] http://www.ctan.org/
[3] http://www.imagemagick.org

