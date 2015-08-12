<p>
Edit: I am not the author of the code. I probably won't maintain this project. I simply wanted to save the code from https://code.google.com/p/htmlcompressor/ for you guys :)

</p>
<p>HtmlCompressor is a small, fast and very easy to use Java library that minifies given HTML or XML source by removing extra whitespaces, comments and other unneeded characters without breaking the content structure. As a result pages become smaller in size and load faster. A command-line version of the compressor is also available. </p><p>Here is a few samples of HTML compression results with default settings: <table class="wikitable"><tr><td style="border: 1px solid #ccc; padding: 5px;"> <strong>Site Name</strong> </td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>Original</strong> </td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>Compressed</strong> </td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>Decrease</strong> </td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">BBC</td><td style="border: 1px solid #ccc; padding: 5px;">77,054b</td><td style="border: 1px solid #ccc; padding: 5px;">55,324b</td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>28.2%</strong> </td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">CNet</td><td style="border: 1px solid #ccc; padding: 5px;">86,492b</td><td style="border: 1px solid #ccc; padding: 5px;">61,896b</td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>28.4%</strong> </td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">FOX News</td><td style="border: 1px solid #ccc; padding: 5px;">75,266b</td><td style="border: 1px solid #ccc; padding: 5px;">64,221b</td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>14.7%</strong> </td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">GameTrailers </td><td style="border: 1px solid #ccc; padding: 5px;">112,199b</td><td style="border: 1px solid #ccc; padding: 5px;">92,851b</td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>17.2%</strong> </td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">Kotaku</td><td style="border: 1px solid #ccc; padding: 5px;">134,938b</td><td style="border: 1px solid #ccc; padding: 5px;">116,280b</td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>13.8%</strong> </td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">National Post</td><td style="border: 1px solid #ccc; padding: 5px;">75,006b</td><td style="border: 1px solid #ccc; padding: 5px;">55,628b</td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>25.8%</strong> </td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">SlashDot</td><td style="border: 1px solid #ccc; padding: 5px;">158,137b</td><td style="border: 1px solid #ccc; padding: 5px;">142,346b</td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>10.0%</strong> </td></tr> <tr><td style="border: 1px solid #ccc; padding: 5px;">StackOverflow</td><td style="border: 1px solid #ccc; padding: 5px;">116,032b</td><td style="border: 1px solid #ccc; padding: 5px;">100,478b</td><td style="border: 1px solid #ccc; padding: 5px;"> <strong>13.4%</strong> </td></tr> </table></p><h4><a name="Table_of_Contents"></a>Table of Contents<a href="#Table_of_Contents" class="section_anchor"></a></h4><p><ul><ul><li><a href="#How_it_Works">How it Works</a></li><li><a href="#How_to_Use">How to Use</a></li><ul><li><a href="#For_Java_Projects">For Java Projects</a></li><li><a href="#For_Non-Java_Projects">For Non-Java Projects</a></li><li><a href="#Bad_Practices">Bad Practices</a></li><li><a href="#Known_Issues">Known Issues</a></li></ul><li><a href="#Dependencies">Dependencies</a></li><li><a href="#Compressing_HTML_and_XML_files_from_a_command_line">Compressing HTML and XML files from a command line</a></li><ul><li><a href="#Defining_custom_preservation_rules">Defining custom preservation rules</a></li><li><a href="#Compressing_whole_directories_and_multiple_files_at_once">Compressing whole directories and multiple files at once</a></li><li><a href="#HTML_Analyzer">HTML Analyzer</a></li></ul><li><a href="#Using_HTML_Compressor_from_Java_API">Using HTML Compressor from Java API</a></li><ul><li><a href="#Creating_your_own_block_preservation_rules">Creating your own block preservation rules</a></li><li><a href="#Using_different_and_CSS_compressor_implementations">Using different and CSS compressor implementations</a></li><li><a href="#Retrieving_HTML_compression_statistics">Retrieving HTML compression statistics</a></li></ul><li><a href="#Using_XML_Compressor_from_Java_API">Using XML Compressor from Java API</a></li><li><a href="#Compressing_selective_content_in_JSP_pages">Compressing selective content in JSP pages</a></li><ul><li><a href="#Taglib_installation_procedure">Taglib installation procedure</a></li><li><a href="#Using_compressor_taglib">Using compressor taglib</a></li></ul><li><a href="#Compressing_selective_content_in_Velocity_templates">Compressing selective content in Velocity templates</a></li><ul><li><a href="#Compressor_directive_installation_procedure">Compressor directive installation procedure</a></li><li><a href="#Using_compressor_directives">Using compressor directives</a></li></ul><li><a href="#Setting_up_Ant_task_to_compress_files">Setting up Ant task to compress files</a></li><li><a href="#Maven_Integration">Maven Integration</a></li><ul><li><a href="#Maven_Artifact">Maven Artifact</a></li><li><a href="#Maven_Plugin">Maven Plugin</a></li></ul><li><a href="#Who_Uses_it">Who Uses it</a></li></ul></ul> </p><h2><a name="How_it_Works"></a>How it Works<a href="#How_it_Works" class="section_anchor"></a></h2><p>During HTML compression the following is applied to the page source: <ul><li>Any content within <tt>&lt;pre&gt;</tt>, <tt>&lt;textarea&gt;</tt>, <tt>&lt;script&gt;</tt> and <tt>&lt;style&gt;</tt> tags will be preserved and remain untouched (with the exception of <tt>&lt;script type=&quot;text/x-jquery-tmpl&quot;&gt;</tt> tags which are compressed as HTML). Inline javascript inside tags (<tt>onclick=&quot;test()&quot;</tt>) will be preserved as well. You can wrap any part of the page in <tt>&lt;!-- {{{ --&gt;...&lt;!-- }}} --&gt;</tt> comments to preserve it, or provide a set of your own preservation rules (out of the box <tt>&lt;?php...?&gt;</tt>, <tt>&lt;%...%&gt;</tt>, and <tt>&lt;!--#... --&gt;</tt> are also supported) </li><li>Comments are removed (except IE conditional comments). Could be disabled. </li><li>Multiple spaces are replaced with a single space. Could be disabled. </li><li>Unneeded spaces inside tags (around <tt>=</tt> and before <tt>/&gt;</tt>) are removed. </li><li>Quotes around tag attributes could be removed when safe (off by default). </li><li>All spaces between tags could be removed (off by default). </li><li>Spaces around selected tags could be removed (off by default). </li><li>Existing doctype declaration could be replaced with simple <tt>&lt;!DOCTYPE html&gt;</tt> declaration (off by default). </li><li>Default attributes from <tt>&lt;script&gt;</tt>, <tt>&lt;style&gt;</tt>, <tt>&lt;link&gt;</tt>, <tt>&lt;form&gt;</tt>, <tt>&lt;input&gt;</tt> tags could be removed (off by default). </li><li>Values from boolean tag attributes could be removed (off by default). </li><li><tt>javascript:</tt> pseudo-protocol could be removed from inline event handlers (off by default). </li><li><tt>http://</tt> and <tt>https://</tt> protocols could be replaced with <tt>//</tt> inside <tt>href</tt>, <tt>src</tt>, <tt>cite</tt>, and <tt>action</tt> tag attributes (tags marked with <tt>rel=&quot;external&quot;</tt> are skipped). </li><li>Content inside <tt>&lt;style&gt;</tt> tags could be optionally compressed using YUI compressor or your own compressor implementation.  </li><li>Content inside <tt>&lt;script&gt;</tt> could be optionally compressed using YUI compressor, Google Closure Compiler or your own compressor implementation.  </li></ul></p><p>With default settings your compressed HTML layout should be 100% identical to the original in all browsers (only characters that are completely safe to remove are removed). Optional settings (that should be safe in 99% cases) would give you extra savings. </p><p>You can optionally remove all unnecessary quotes from tag attributes (attributes that consist from a single word: <tt>&lt;div id=&quot;example&quot;&gt;</tt> would become <tt>&lt;div id=example&gt;</tt>). This usually gives around 3% pagesize decrease at no performance cost but might break strict HTML validation so this option is disabled by default. </p><p>About extra 3% pagesize can be saved by removing inter-tag spaces. It is fairly safe to turn this option on unless you rely on spaces for page formatting. Even if you do, you can always preserve required spaces with <tt>&amp;#20;</tt> or <tt>&amp;nbsp;</tt>. This option has no performance impact. </p><p>You can quickly test how each of the compressor settings would affect filesize of your page by running command line <a href="#HTML_Analyzer">HTML Analyzer</a>. </p><p>During XML compression: <ul><li>Any content inside <tt>&lt;![CDATA[...]]&gt;</tt> is preserved. </li><li>All comments are removed. Could be disabled. </li><li>All spaces between tags are removed. Could be disabled. </li><li>Unneeded spaces inside tags (multiple spaces, spaces around <tt>=</tt>, spaces before <tt>/&gt;</tt>) are removed. </li></ul></p><h2><a name="How_to_Use"></a>How to Use<a href="#How_to_Use" class="section_anchor"></a></h2><p>Before reading further, if you are not serving your HTML/XML content using GZip compression, you should really look into that first, as it would give you very significant compression ratio (sometimes up to 10 times) and usually very easy to implement. For further reading on GZip compression please see <a href="http://betterexplained.com/articles/how-to-optimize-your-site-with-gzip-compression/" rel="nofollow">this article</a> for example. </p><p>If you want to reach further size decrease, the next step would be removing insignificant, from browser&#x27;s perspective, characters from your pages, that&#x27;s where this library comes in handy.  </p><p>Juriy Zaytsev did an excellent detailed research on HTML minification techniques, which you can use as a guide to what HTML compression settings would work best for your project. Please see his <a href="http://perfectionkills.com/optimizing-html/" rel="nofollow">Optimizing HTML</a> and <a href="http://perfectionkills.com/experimenting-with-html-minifier/" rel="nofollow">Experimenting with html minifier</a> articles. </p><h3><a name="For_Java_Projects"></a>For Java Projects<a href="#For_Java_Projects" class="section_anchor"></a></h3><p>If you are generating static HTML files on the server, the most flexible solution would be calling html compression before writing output to the file. If you are generating HTML files once in a while and then uploading them to a production server, the easiest solution that doesn&#x27;t require any code modifications would be using ANT task that calls the command line version of the library and rewrites files with their compressed versions. </p><p>For dynamic sites that are using JSP, the best way of compressing the output would be using compressor taglib. </p><p>For dynamic sites using Velocity, you can either wrap your templates with compressor directives or call compressor manually after merging the template. </p><p>For other dynamic cases you will probably have to call compressors directly from the code before serving a page to the client. </p><p><tt>HtmlCompressor</tt> and <tt>XmlCompressor</tt> classes are considered thread safe<tt>*</tt> and can be used in multi-thread environment (the only unsafe part is setting compression options, so it would be a good idea to initialize a compressor with required settings once per application and then use it to compress different pages in parallel in multiple threads. Please note that enabling statistics generation makes compressor not safe). </p><p>For Maven projects HtmlCompressor library is available as a <a href="#Maven_Artifact">Maven artifact</a>. </p><h3><a name="For_Non-Java_Projects"></a>For Non-Java Projects<a href="#For_Non-Java_Projects" class="section_anchor"></a></h3><p>If you are generating HTML for your site (or have simple site in pure HTML) you can use a command line version of the library (Java still must be installed). For dynamic sites it other languages the only option would be programmatically executing shell command that runs command line compressor.  </p><h3><a name="Bad_Practices"></a>Bad Practices<a href="#Bad_Practices" class="section_anchor"></a></h3><ul><li>Don&#x27;t feed the compressor actual templates (php, jsp, etc). This most likely won&#x27;t work, even if it does it would be a bad idea anyway as you will lose their readability and further development will be very inconvenient. Instead of compressing templates you should consider compressing resulting html after a template is merged. If you absolutely have to compress templates, you need to set custom block preservation rules for HTML Compressor. </li><li>If your site is in pure HTML, always keep original files and only compress their copies that will be served to the client. If you compress your only sources, again your further development will be very hard and there is no easy way to decompress pages back. </li></ul><h3><a name="Known_Issues"></a>Known Issues<a href="#Known_Issues" class="section_anchor"></a></h3><ul><li>When <tt>&lt;script&gt;</tt> tag contains some custom preserved block (for example <tt>&lt;?php&gt;</tt>), enabling inline javascript compression will fail. Such <tt>&lt;script&gt;</tt> tags could be skipped by wrapping them with <tt>&lt;!-- {{{ --&gt;...&lt;!-- }}} --&gt;</tt> comments (skip blocks). </li><li>Removing intertag spaces might break text formatting, for example spaces between  words surrounded with <tt>&lt;b&gt;</tt> will be removed. Such spaces might be preserved by replacing them with <tt>&amp;#20;</tt> or <tt>&amp;nbsp;</tt>. </li></ul><h2><a name="Dependencies"></a>Dependencies<a href="#Dependencies" class="section_anchor"></a></h2><p>XML compressor doesn&#x27;t rely on any external libraries. </p><p>HTML compressor with default settings doesn&#x27;t require any dependencies.  </p><p>Inline CSS compression requires <a href="http://developer.yahoo.com/yui/compressor/" rel="nofollow">YUI compressor</a> library. </p><p>Inline JavaScript compression requires either <a href="http://developer.yahoo.com/yui/compressor/" rel="nofollow">YUI compressor</a> library (by default) or <a href="http://code.google.com/closure/compiler/" rel="nofollow">Google Closure Compiler</a> library. </p><p>All dependencies could be found in <tt>/lib/</tt> folder of the package. </p><p>Please note that if using command line compressor, there are strict restrictions on jar filenames for dependencies (more details in the command line compressor section below). </p><h2><a name="Compressing_HTML_and_XML_files_from_a_command_line"></a>Compressing HTML and XML files from a command line<a href="#Compressing_HTML_and_XML_files_from_a_command_line" class="section_anchor"></a></h2><p>If you have <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" rel="nofollow">Java</a> installed, you can run HTML and XML compressors from a command line.  </p><p>For inline JavaScript compression you can choose between YUI Compressor (default) and Google Closure Compiler. If YUI compressor is used, jar file <tt>yuicompressor-2.4.6.jar</tt> (or <tt>yuicompressor-2.4.*.jar</tt> or <tt>yuicompressor.jar</tt>) must be present at the same directory as HtmlCompressor jar. For Closure Compiler <tt>compiler.jar</tt> must be present. (Please note that jar filenames cannot be changed). </p><p>Usage: <tt>java -jar htmlcompressor.jar [options] [input]</tt> </p><pre class="prettyprint">[input]                        URL, filename, directory, or space separated list
                               of files and directories to compress.
                               If none provided reads from &lt;stdin&gt;

Global Options:
 -?, /?, -h, --help            Displays this help screen
 -t, --type &lt;html|xml&gt;         If not provided autodetects from file extension
 -r, --recursive               Process files inside subdirectories
 -c, --charset &lt;charset&gt;       Charset for reading files, UTF-8 by default
 -m, --mask &lt;filemask&gt;         Filter input files inside directories by mask
 -o, --output &lt;path&gt;           Filename or directory for compression results.
                               If none provided outputs result to &lt;stdout&gt;
 -a, --analyze                 Tries different settings and displays report.
                               All settings except --js-compressor are ignored

XML Compression Options:
 --preserve-comments           Preserve comments
 --preserve-intertag-spaces    Preserve intertag spaces

HTML Compression Options:
 --preserve-comments           Preserve comments
 --preserve-multi-spaces       Preserve multiple spaces
 --preserve-line-breaks        Preserve line breaks
 --remove-intertag-spaces      Remove intertag spaces
 --remove-quotes               Remove unneeded quotes
 --simple-doctype              Change doctype to &lt;!DOCTYPE html&gt;
 --remove-style-attr           Remove TYPE attribute from STYLE tags
 --remove-link-attr            Remove TYPE attribute from LINK tags
 --remove-script-attr          Remove TYPE and LANGUAGE from SCRIPT tags
 --remove-form-attr            Remove METHOD=&quot;GET&quot; from FORM tags
 --remove-input-attr           Remove TYPE=&quot;TEXT&quot; from INPUT tags
 --simple-bool-attr            Remove values from boolean tag attributes
 --remove-js-protocol          Remove &quot;javascript:&quot; from inline event handlers
 --remove-http-protocol        Remove &quot;http:&quot; from tag attributes
 --remove-https-protocol       Remove &quot;https:&quot; from tag attributes
 --remove-surrounding-spaces &lt;min|max|all|custom_list&gt;
                               Predefined or custom comma separated list of tags
 --compress-js                 Enable inline JavaScript compression
 --compress-css                Enable inline CSS compression using YUICompressor
 --js-compressor &lt;yui|closure&gt; Switch inline JavaScript compressor between
                               YUICompressor (default) and Closure Compiler

JavaScript Compression Options for YUI Compressor:
 --nomunge                     Minify only, do not obfuscate
 --preserve-semi               Preserve all semicolons
 --disable-optimizations       Disable all micro optimizations
 --line-break &lt;column num&gt;     Insert a line break after the specified column

JavaScript Compression Options for Google Closure Compiler:
 --closure-opt-level &lt;simple|advanced|whitespace&gt;
                               Sets level of optimization (simple by default)
 --closure-externs &lt;file&gt;      Sets custom externs file, repeat for each file
 --closure-custom-externs-only Disable default built-in externs

CSS Compression Options for YUI Compressor:
 --line-break &lt;column num&gt;     Insert a line break after the specified column

Custom Block Preservation Options:
 --preserve-php                Preserve &lt;?php ... ?&gt; tags
 --preserve-server-script      Preserve &lt;% ... %&gt; tags
 --preserve-ssi                Preserve &lt;!--# ... --&gt; tags
 -p, --preserve &lt;path&gt;         Read regular expressions that define
                               custom preservation rules from a file

Please note that if you enable CSS or JavaScript compression, additional
YUI Compressor or Google Closure Compiler jar files must be present
in the same directory as this jar.</pre><p>Input and output files could be the same, in this case a file will be overwritten with its compressed version. </p><p>If <tt>--type</tt> parameter is not set, the compressor would try to guess it based on a file extension. If a file extension is not recognized, it defaults to html compression. When compressing <a href="#Compressing_whole_directories_and_multiple_files_at_once">multiple files at once</a>, the type is not guessed and defaults to HTML compression if it wasn&#x27;t set manually. </p><p>If charset is not provided, <tt>UTF-8</tt> will be used by default. List of all supported charsets could be found  <a href="http://download.oracle.com/javase/1.5.0/docs/guide/intl/encoding.doc.html" rel="nofollow">here</a> (required name is specified in the first column, for example: <tt>ISO-8859-1</tt>, <tt>windows-1251</tt>). </p><p>Examples: </p><pre class="prettyprint">java -jar htmlcompressor.jar --preserve-comments --type html -o /path/compressed/test-compressed.html /path/original/test.html

java -jar htmlcompressor.jar --compress-js /path/original/test.html &gt; /path/compressed/test-compressed.html

java -jar htmlcompressor.jar --compress-js --js-compressor closure --closure-opt-level advanced --closure-externs /path/externs1.js --closure-externs /path/externs2.js original.html &gt; compressed.html</pre><h3><a name="Defining_custom_preservation_rules"></a>Defining custom preservation rules<a href="#Defining_custom_preservation_rules" class="section_anchor"></a></h3><p>If you need to set custom tag preservation rules, you can put regular expressions defining them into a text file (one expression per line) and pass path to this file as <tt>-p /path/to/regexps.txt</tt> parameter. Regular expressions in a file can have so called &quot;embedded flag expressions&quot; macro options that set options for a regular expression compiler.  </p><p>For example if you want to apply <tt>CASE_INSENSITIVE</tt> and <tt>DOTALL</tt> options to this expression that matches php blocks: </p><pre class="prettyprint">&lt;\?php.+?\?&gt;</pre><p>you need to use this syntax: </p><pre class="prettyprint">(?si)&lt;\?php.+?\?&gt;</pre><p>You can read more about regular expression compiler options and their corresponding embedded flags <a href="http://download.oracle.com/javase/6/docs/api/java/util/regex/Pattern.html" rel="nofollow">here</a> </p><p>Example: </p><pre class="prettyprint">java -jar htmlcompressor.jar --preserve-php -p /path/regexp.txt http://path/original/test.html &gt; /path/compressed/test-compressed.html</pre><h3><a name="Compressing_whole_directories_and_multiple_files_at_once"></a>Compressing whole directories and multiple files at once<a href="#Compressing_whole_directories_and_multiple_files_at_once" class="section_anchor"></a></h3><p>Command line compressor can take a whole directory as input. In this case output parameter should point to a directory as well. </p><p>For example: </p><pre class="prettyprint">java -jar htmlcompressor.jar --type html -o /to/ /from/</pre><p>In this mode all files from the input directory will be compressed and placed into the output directory (with the same filenames). Sub-directories are not included by default, use <tt>--recursive</tt> option to include sub-directories. </p><p>Please note that <tt>--type</tt> parameter in this case plays important role as it not only defines which compressor mode to use, but also which files to compress. For HTML type only <tt>*.html</tt> and <tt>*.htm</tt> files are processed, for XML - only <tt>*.xml</tt>. If type is not explicitly set, it defaults to HTML. </p><p>You can overwrite default file masks by setting <tt>--mask &lt;mask&gt;</tt> parameter. Mask is a semicolon (<tt>;</tt>) separated filename filter, with the following special characters: </p><ul><li>Star (<tt>*</tt>) - any character zero or more times </li><li>Question mark (<tt>?</tt>) - any character exactly one time </li></ul><p>For example to compress only <tt>.php</tt> files, files which names start with <tt>test-</tt>, and files with two letter extensions: </p><pre class="prettyprint">java -jar htmlcompressor.jar --type html --recursive --mask *.php;test-*;*.?? -o /to/ /from/</pre><p>(Please note that mask shouldn&#x27;t contain any spaces) </p><p>Another way to compress multiple files at once is providing a space separated list of files (or even directories) as input: </p><pre class="prettyprint">java -jar htmlcompressor.jar -o /to/ /source1/ /source2/ file1.html file2.html</pre><p>Please note that in this mode all files will be placed into the same output folder (<tt>/to/</tt>). If it is not a desired behavior, please compress each folder separately. </p><h3><a name="HTML_Analyzer"></a>HTML Analyzer<a href="#HTML_Analyzer" class="section_anchor"></a></h3><p>To run a command line compressor in analyzer mode you only need to specify input file or URL: </p><pre class="prettyprint">java -jar htmlcompressor.jar --js-compressor closure -a http://www.cnn.com/</pre><p>In this mode HTML compressor will try to compress provided page with all possible compression parameters and display result in a report: </p><pre class="prettyprint">================================================================================
         Setting          | Incremental Gain |    Total Gain    |  Page Size   |
================================================================================
Compression disabled      |         0 (0.0%) |         0 (0.0%) |      103,568 |
All settings disabled     |        27 (0.0%) |        27 (0.0%) |      103,541 |
Comments removed          |     5,517 (5.3%) |     5,544 (5.4%) |       98,024 |
Multiple spaces removed   |     4,234 (4.3%) |     9,778 (9.4%) |       93,790 |
No spaces between tags    |       838 (0.9%) |   10,616 (10.3%) |       92,952 |
No surround spaces (min)  |         4 (0.0%) |   10,620 (10.3%) |       92,948 |
No surround spaces (max)  |         0 (0.0%) |   10,620 (10.3%) |       92,948 |
No surround spaces (all)  |       116 (0.1%) |   10,736 (10.4%) |       92,832 |
Quotes removed from tags  |     2,072 (2.2%) |   12,808 (12.4%) |       90,760 |
&lt;link&gt; attr. removed      |       112 (0.1%) |   12,920 (12.5%) |       90,648 |
&lt;style&gt; attr. removed     |         0 (0.0%) |   12,920 (12.5%) |       90,648 |
&lt;script&gt; attr. removed    |     1,040 (1.1%) |   13,960 (13.5%) |       89,608 |
&lt;form&gt; attr. removed      |        22 (0.0%) |   13,982 (13.5%) |       89,586 |
&lt;input&gt; attr. removed     |        40 (0.0%) |   14,022 (13.5%) |       89,546 |
Simple boolean attributes |        36 (0.0%) |   14,058 (13.6%) |       89,510 |
Simple doctype            |        86 (0.1%) |   14,144 (13.7%) |       89,424 |
Remove js pseudo-protocol |         0 (0.0%) |   14,144 (13.7%) |       89,424 |
Remove http protocol      |     1,095 (1.2%) |   15,239 (14.7%) |       88,329 |
Remove https protocol     |         0 (0.0%) |   15,239 (14.7%) |       88,329 |
Compress inline CSS (YUI) |       354 (0.4%) |   15,593 (15.1%) |       87,975 |
Compress JS (Closure)     |     2,095 (2.4%) |   17,688 (17.1%) |       85,880 |
================================================================================

Each consecutive compressor setting is applied on top of previous ones.
In order to see JS and CSS compression results, YUI jar file must be present.
All sizes are in bytes.</pre><p>Having this information might help you decide which compression parameters to use. </p><h2><a name="Using_HTML_Compressor_from_Java_API"></a>Using HTML Compressor from Java API<a href="#Using_HTML_Compressor_from_Java_API" class="section_anchor"></a></h2><p>Create <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/HtmlCompressor.html" rel="nofollow">HtmlCompressor</a> instance and pass HTML content to <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/HtmlCompressor.html#compress(java.lang.String)" rel="nofollow">compress(String source)</a> method, which would return compressed result: </p><pre class="prettyprint">String html = getHtml(); //your external method to get html from memory, file, url etc.
HtmlCompressor compressor = new HtmlCompressor();
String compressedHtml = compressor.compress(html);</pre><p>By default it: <ul><li>Preserves any content within <tt>&lt;pre&gt;</tt>, <tt>&lt;textarea&gt;</tt>, <tt>&lt;script&gt;</tt> and <tt>&lt;style&gt;</tt> tags </li><li>Removes HTML comments </li><li>Replaces multiple whitespace characters and line breaks with spaces </li></ul></p><p>If you need to set additional compression parameters: </p><pre class="prettyprint">HtmlCompressor compressor = new HtmlCompressor();

compressor.setEnabled(true);                   //if false all compression is off (default is true)
compressor.setRemoveComments(true);            //if false keeps HTML comments (default is true)
compressor.setRemoveMultiSpaces(true);         //if false keeps multiple whitespace characters (default is true)
compressor.setRemoveIntertagSpaces(true);      //removes iter-tag whitespace characters
compressor.setRemoveQuotes(true);              //removes unnecessary tag attribute quotes
compressor.setSimpleDoctype(true);             //simplify existing doctype
compressor.setRemoveScriptAttributes(true);    //remove optional attributes from script tags
compressor.setRemoveStyleAttributes(true);     //remove optional attributes from style tags
compressor.setRemoveLinkAttributes(true);      //remove optional attributes from link tags
compressor.setRemoveFormAttributes(true);      //remove optional attributes from form tags
compressor.setRemoveInputAttributes(true);     //remove optional attributes from input tags
compressor.setSimpleBooleanAttributes(true);   //remove values from boolean tag attributes
compressor.setRemoveJavaScriptProtocol(true);  //remove &quot;javascript:&quot; from inline event handlers
compressor.setRemoveHttpProtocol(true);        //replace &quot;http://&quot; with &quot;//&quot; inside tag attributes
compressor.setRemoveHttpsProtocol(true);       //replace &quot;https://&quot; with &quot;//&quot; inside tag attributes
compressor.setPreserveLineBreaks(true);        //preserves original line breaks
compressor.setRemoveSurroundingSpaces(&quot;br,p&quot;); //remove spaces around provided tags

compressor.setCompressCss(true);               //compress inline css 
compressor.setCompressJavaScript(true);        //compress inline javascript
compressor.setYuiCssLineBreak(80);             //--line-break param for Yahoo YUI Compressor 
compressor.setYuiJsDisableOptimizations(true); //--disable-optimizations param for Yahoo YUI Compressor 
compressor.setYuiJsLineBreak(-1);              //--line-break param for Yahoo YUI Compressor 
compressor.setYuiJsNoMunge(true);              //--nomunge param for Yahoo YUI Compressor 
compressor.setYuiJsPreserveAllSemiColons(true);//--preserve-semi param for Yahoo YUI Compressor 

//use Google Closure Compiler for javascript compression
compressor.setJavaScriptCompressor(new ClosureJavaScriptCompressor(CompilationLevel.SIMPLE_OPTIMIZATIONS));

//use your own implementation of css comressor
compressor.setCssCompressor(new MyOwnCssCompressor());

String compressedHtml = compressor.compress(html);</pre><p>If JavaScript compression is enabled, corresponding compressor libraries should be included into project&#x27;s classpath. See <a href="#Dependencies">Dependencies</a> section for more details. </p><h3><a name="Creating_your_own_block_preservation_rules"></a>Creating your own block preservation rules<a href="#Creating_your_own_block_preservation_rules" class="section_anchor"></a></h3><p>If you are going to compress HTML mixed with some non-HTML tags (like PHP, JSP, etc), you most likely would want to keep those tags preserved. You can set custom preservation rules for HTML compressor by passing a list of regular expression <tt>Pattern</tt> objects. </p><p><a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/HtmlCompressor.html" rel="nofollow">HtmlCompressor</a> class currently has 3 predefined patterns for most often used custom preservation rules: <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/HtmlCompressor.html#PHP_TAG_PATTERN" rel="nofollow">PHP_TAG_PATTERN</a>, <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/HtmlCompressor.html#SERVER_SCRIPT_TAG_PATTERN" rel="nofollow">SERVER_SCRIPT_TAG_PATTERN</a> and <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/HtmlCompressor.html#SERVER_SIDE_INCLUDE_PATTERN" rel="nofollow">SERVER_SIDE_INCLUDE_PATTERN</a>. Other patterns could be created manually: </p><pre class="prettyprint">List&lt;Pattern&gt; preservePatterns = new ArrayList&lt;Pattern&gt;();
preservePatterns.add(HtmlCompressor.PHP_TAG_PATTERN); //&lt;?php ... ?&gt; blocks
preservePatterns.add(HtmlCompressor.SERVER_SCRIPT_TAG_PATTERN); //&lt;% ... %&gt; blocks
preservePatterns.add(HtmlCompressor.SERVER_SIDE_INCLUDE_PATTERN); //&lt;!--# ... --&gt; blocks
preservePatterns.add(Pattern.compile(&quot;&lt;jsp:.*?&gt;&quot;, Pattern.DOTALL | Pattern.CASE_INSENSITIVE)); //&lt;jsp: ... &gt; tags

HtmlCompressor compressor = new HtmlCompressor();
compressor.setPreservePatterns(preservePatterns);
compressor.compress(source);</pre><p>Custom preservation rules have the highest priority. </p><h3><a name="Using_different_and_CSS_compressor_implementations"></a>Using different JavaScript and CSS compressor implementations<a href="#Using_different_and_CSS_compressor_implementations" class="section_anchor"></a></h3><p>Out of the box HTML Compressor comes with two JavaScript implementations that use YUI and Google Closure compressors for compressing inline <tt>&lt;script&gt;</tt> tags, and one implementation that uses YUI compressor for compressing inline <tt>&lt;style&gt;</tt> tags. You can additionally create your own implementations using any third party library. </p><p>CSS compressor implementation based on YUI is called <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/YuiCssCompressor.html" rel="nofollow">YuiCssCompressor</a>. In most cases you won&#x27;t need to use this class directly as HTML compressor would initialize it behind the scenes for you if no other implementation is provided for CSS compression. </p><pre class="prettyprint">YuiCssCompressor cssCompressor = new YuiCssCompressor();
cssCompressor.setLineBreak(-1);
htmlCompressor.setCssCompressor(cssCompressor);</pre><p>This would be exactly the same as: </p><pre class="prettyprint">htmlCompressor.setYuiCssLineBreak(-1);</pre><p>JavaScript compressor implementation based on YUI is called <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/YuiJavaScriptCompressor.html" rel="nofollow">YuiJavaScriptCompressor</a>. You usually won&#x27;t need to use it directly either, as HTML Compressor will use it behind the scenes by default. </p><p>JavaScript compressor based on Google Closure Compiler implementation is called <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/ClosureJavaScriptCompressor.html" rel="nofollow">ClosureJavaScriptCompressor</a>: </p><pre class="prettyprint">//default settings
htmlCompressor.setJavaScriptCompressor(new ClosureJavaScriptCompressor());

//you can set different level of compilation in a constructor
htmlCompressor.setJavaScriptCompressor(new ClosureJavaScriptCompressor(CompilationLevel.WHITESPACE_ONLY));

//or fine tune all settings
ClosureJavaScriptCompressor jsCompressor = new ClosureJavaScriptCompressor();
jsCompressor.setCompilationLevel(CompilationLevel.SIMPLE_OPTIMIZATIONS);
jsCompressor.setCompilerOptions(new CompilerOptions());
jsCompressor.setExterns(new ArrayList&lt;JSSourceFile&gt;());
jsCompressor.setCustomExternsOnly(false);
jsCompressor.setLoggingLevel(Level.SEVERE);
jsCompressor.setWarningLevel(WarningLevel.DEFAULT);

htmlCompressor.setJavaScriptCompressor(jsCompressor);</pre><p>Please see <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/ClosureJavaScriptCompressor.html" rel="nofollow">javadocs</a> for details. </p><p>If you would like to create your own compressor, you need to create a class that  implements simple <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/Compressor.html" rel="nofollow">Compressor</a> interface: </p><pre class="prettyprint">public interface Compressor {
	public abstract String compress(String source);
}</pre><p>You can take current <a href="http://code.google.com/p/htmlcompressor/source/browse/trunk/src/com/googlecode/htmlcompressor/compressor/YuiJavaScriptCompressor.java" rel="nofollow">YuiJavaScriptCompressor</a> and <a href="http://code.google.com/p/htmlcompressor/source/browse/trunk/src/com/googlecode/htmlcompressor/compressor/ClosureJavaScriptCompressor.java" rel="nofollow">ClosureJavaScriptCompressor</a> implementations as examples. </p><h3><a name="Retrieving_HTML_compression_statistics"></a>Retrieving HTML compression statistics<a href="#Retrieving_HTML_compression_statistics" class="section_anchor"></a></h3><p>HTML Compressor can optionally collect compression statistics: </p><pre class="prettyprint">HtmlCompressor compressor = new HtmlCompressor();
compressor.setGenerateStatistics(true);
compressor.compress(html);

System.out.println(String.format(
	&quot;Compression time: %,d ms, Original size: %,d bytes, Compressed size: %,d bytes&quot;, 
	compressor.getStatistics().getTime(), 
	compressor.getStatistics().getOriginalMetrics().getFilesize(), 	
	compressor.getStatistics().getCompressedMetrics().getFilesize()
));</pre><p>Please note that enabling statistics generation makes HTML compressor not thread safe. </p><p>For a full list of all statistics parameters collected please see <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/HtmlCompressorStatistics.html" rel="nofollow">HtmlCompressorStatistics</a> javadocs. </p><h2><a name="Using_XML_Compressor_from_Java_API"></a>Using XML Compressor from Java API<a href="#Using_XML_Compressor_from_Java_API" class="section_anchor"></a></h2><p>Create <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/XmlCompressor.html" rel="nofollow">XmlCompressor</a> instance and pass XML content to <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/compressor/XmlCompressor.html#compress(java.lang.String)" rel="nofollow">compress(String source)</a> method, which would return a compressed source: </p><pre class="prettyprint">String xml = getXml(); //your external method to get xml from memory, file, url etc.
XmlCompressor compressor = new XmlCompressor();
String compressedXml = compressor.compress(xml);</pre><p>By default it: <ul><li>Preserves any content within tags and <tt>CDATA</tt> blocks. </li><li>Removes XML comments </li><li>Removes all whitespace characters outside of the tags </li></ul></p><p>If you need to set additional compression parameters: </p><pre class="prettyprint">XmlCompressor compressor = new XmlCompressor();

compressor.setEnabled(true);             //if false all compression is off (default is true)
compressor.setRemoveComments(true);      //if false keeps XML comments (default is true)
compressor.setRemoveIntertagSpaces(true);//removes iter-tag whitespace characters  (default is true)
String compressedXml = compressor.compress(xml);</pre><h2><a name="Compressing_selective_content_in_JSP_pages"></a>Compressing selective content in JSP pages<a href="#Compressing_selective_content_in_JSP_pages" class="section_anchor"></a></h2><p>If you install the compressor taglib, you will be able to use <tt>&lt;compress:html&gt;</tt>, <tt>&lt;compress:xml&gt;</tt>, <tt>&lt;compress:js&gt;</tt> and <tt>&lt;compress:css&gt;</tt> tags in your JSP pages to mark selective code blocks that need to be compressed.  </p><h3><a name="Taglib_installation_procedure"></a>Taglib installation procedure<a href="#Taglib_installation_procedure" class="section_anchor"></a></h3><ol><li>Download <tt>.jar</tt> file of the current release and put it into your lib directory </li><li>Add the following taglib directive to your JSP pages: </li><pre class="prettyprint">&lt;%@ taglib uri=&quot;http://htmlcompressor.googlecode.com/taglib/compressor&quot; prefix=&quot;compress&quot; %&gt;</pre></ol><p>Please note that JSP 2.0 or above is required. </p><h3><a name="Using_compressor_taglib"></a>Using compressor taglib<a href="#Using_compressor_taglib" class="section_anchor"></a></h3><p>Now you can wrap parts of JSP pages that need to be compressed with corresponding tags: </p><pre class="prettyprint">&lt;%@ taglib uri=&quot;http://htmlcompressor.googlecode.com/taglib/compressor&quot; prefix=&quot;compress&quot; %&gt;
&lt;html&gt;
	&lt;head&gt;&lt;title&gt;Compressor Example&lt;/title&gt;&lt;/head&gt;
	&lt;body&gt;
		&lt;compress:html enabled=&quot;${param.enabled != &#x27;false&#x27;}&quot; compressJavaScript=&quot;false&quot;&gt;
			&lt;h1&gt; Header &lt;/h1&gt;
			&lt;a href=&quot;/&quot;&gt; Link &lt;/a&gt;
			&lt;script&gt;
				alert(&quot;javascript&quot;); //comment
			&lt;/script&gt;
		&lt;/compress:html&gt;
		
		&lt;script&gt;
			&lt;compress:js jsCompressor=&quot;closure&quot;&gt;
				alert(&quot;javascript&quot;); //comment
			&lt;/compress:js&gt;
		&lt;/script&gt;
	&lt;/body&gt;
&lt;/html&gt;</pre><p>Each tag supports all attributes from corresponding compressors, so you have full control over their options, for example: </p><pre class="prettyprint">&lt;compress:html enabled=&quot;true&quot; removeComments=&quot;false&quot; compressJavaScript=&quot;true&quot; yuiJsDisableOptimizations=&quot;true&quot;&gt;&lt;/compress:html&gt;
&lt;compress:html compressJavaScript=&quot;true&quot; jsCompressor=&quot;closure&quot; closureOptLevel=&quot;simple&quot;&gt;&lt;/compress:html&gt;
&lt;compress:js enabled=&quot;true&quot; yuiJsLineBreak=&quot;80&quot; yuiJsPreserveAllSemiColons=&quot;true&quot;&gt;&lt;/compress:js&gt;</pre><p><tt>&lt;compress:js&gt;</tt> and <tt>&lt;compress:css&gt;</tt> tags call corresponding compressors directly bypassing HtmlCompressor, so they should be used only for actual JavaScript and Css content. If you need to wrap mixed content use <tt>&lt;compress:html&gt;</tt> with required attributes.  For the complete list of available attributes see taglib or <a href="http://htmlcompressor.googlecode.com/svn/trunk/doc/com/googlecode/htmlcompressor/taglib/package-summary.html" rel="nofollow">javadocs</a>. </p><h2><a name="Compressing_selective_content_in_Velocity_templates"></a>Compressing selective content in Velocity templates<a href="#Compressing_selective_content_in_Velocity_templates" class="section_anchor"></a></h2><p>After installing Velocity compressor directives you will be able to use <tt>#compressHtml</tt>, <tt>#compressXml</tt>, <tt>#compressJs</tt> and <tt>#compressCss</tt> directives in your Velocity templates to mark selective blocks that need to be compressed.  </p><h3><a name="Compressor_directive_installation_procedure"></a>Compressor directive installation procedure<a href="#Compressor_directive_installation_procedure" class="section_anchor"></a></h3><p>First you need to set <tt>userdirective</tt> Velocity property and provide a list of  directive classes. You can do this by either adding the following line into your <tt>velocity.properties</tt>: </p><pre class="prettyprint">userdirective=com.googlecode.htmlcompressor.velocity.HtmlCompressorDirective, \
    com.googlecode.htmlcompressor.velocity.XmlCompressorDirective, \ 
    com.googlecode.htmlcompressor.velocity.JavaScriptCompressorDirective, \
    com.googlecode.htmlcompressor.velocity.CssCompressorDirective</pre><p>Or using runtime configuration: </p><pre class="prettyprint">VelocityEngine velocity = new VelocityEngine();
velocity.setProperty(&quot;userdirective&quot;, &quot;com.googlecode.htmlcompressor.velocity.HtmlCompressorDirective,&quot; + 
    &quot;com.googlecode.htmlcompressor.velocity.XmlCompressorDirective,&quot; + 
    &quot;com.googlecode.htmlcompressor.velocity.JavaScriptCompressorDirective,&quot; + 
    &quot;com.googlecode.htmlcompressor.velocity.CssCompressorDirective&quot;);
velocity.init();</pre><p>You can include only compressors you would need. </p><p>All compressors are now ready to be used with default configurations. You can change configuration properties either in <tt>velocity.properties</tt> or using runtime configuration by setting <tt>userdirective.{directive}.{property_name}</tt> values. Here is a list of all supported parameters with their default values: </p><pre class="prettyprint">userdirective.compressHtml.enabled = true
userdirective.compressHtml.removeComments = true
userdirective.compressHtml.removeMultiSpaces = true
userdirective.compressHtml.removeIntertagSpaces = false
userdirective.compressHtml.removeQuotes = false
userdirective.compressHtml.preserveLineBreaks = false
userdirective.compressHtml.simpleDoctype = false
userdirective.compressHtml.removeScriptAttributes = false
userdirective.compressHtml.removeStyleAttributes = false
userdirective.compressHtml.removeLinkAttributes = false
userdirective.compressHtml.removeFormAttributes = false
userdirective.compressHtml.removeInputAttributes = false
userdirective.compressHtml.simpleBooleanAttributes = false
userdirective.compressHtml.removeJavaScriptProtocol = false
userdirective.compressHtml.removeHttpProtocol = false
userdirective.compressHtml.removeHttpsProtocol = false
userdirective.compressHtml.compressJavaScript = false
userdirective.compressHtml.compressCss = false
userdirective.compressHtml.jsCompressor = yui #(or &quot;closure&quot;)
userdirective.compressHtml.yuiJsNoMunge = false
userdirective.compressHtml.yuiJsPreserveAllSemiColons = false
userdirective.compressHtml.yuiJsLineBreak = -1
userdirective.compressHtml.yuiCssLineBreak = -1
userdirective.compressHtml.closureOptLevel = simple #(or &quot;advanced&quot;, &quot;whitespace&quot;)

userdirective.compressXml.enabled = true
userdirective.compressXml.removeComments = true
userdirective.compressXml.removeIntertagSpaces = true

userdirective.compressJs.enabled = true
userdirective.compressJs.jsCompressor = yui #(or &quot;closure&quot;)
userdirective.compressJs.yuiJsNoMunge = false
userdirective.compressJs.yuiJsPreserveAllSemiColons = false
userdirective.compressJs.yuiJsLineBreak = -1
userdirective.compressJs.closureOptLevel = simple #(or &quot;advanced&quot;, &quot;whitespace&quot;)

userdirective.compressCss.enabled = true
userdirective.compressCss.yuiCssLineBreak = -1</pre><h3><a name="Using_compressor_directives"></a>Using compressor directives<a href="#Using_compressor_directives" class="section_anchor"></a></h3><p>Now you can wrap parts of Velocity templates that need to be compressed with corresponding directives (please note that directives must end with empty parentheses): </p><pre class="prettyprint">&lt;html&gt;
	&lt;head&gt;&lt;title&gt;Compressor Example&lt;/title&gt;&lt;/head&gt;
	&lt;body&gt;
		#compressHtml()
			&lt;h1&gt; Header &lt;/h1&gt;
			&lt;a href=&quot;/&quot;&gt; Link &lt;/a&gt;
			&lt;script&gt;
				alert(&quot;javascript&quot;); //comment
			&lt;/script&gt;
		#end
		
		&lt;script&gt;
		#compressJs()
                      	alert(&quot;javascript&quot;); //comment
		#end
		&lt;/script&gt;

	&lt;/body&gt;
&lt;/html&gt;</pre><p><tt>#compressJs</tt> and <tt>#compressCss</tt> directives call corresponding YUI or Closure compressor classes directly bypassing HtmlCompressor, so they should be used only for actual JavaScript and CSS content. If you need to wrap mixed content use <tt>#compressHtml</tt> with required properties.   </p><h2><a name="Setting_up_Ant_task_to_compress_files"></a>Setting up Ant task to compress files<a href="#Setting_up_Ant_task_to_compress_files" class="section_anchor"></a></h2><p>If you are using Ant for project builds you can setup a task that will compress provided files automatically during a build. </p><p>For example: </p><pre class="prettyprint">    &lt;target name=&quot;compress&quot;&gt;
    	&lt;apply executable=&quot;java&quot; parallel=&quot;false&quot;&gt;
	        &lt;fileset dir=&quot;/test/&quot; includes=&quot;*.html&quot;&gt;
	        	&lt;exclude name=&quot;**/leave/**&quot; /&gt;
	        &lt;/fileset&gt;
	        &lt;arg value=&quot;-jar&quot;/&gt;
	        &lt;arg path=&quot;/path/to/htmlcompressor-0.8.jar&quot;/&gt;
	 	&lt;arg line=&quot;--type html&quot;/&gt;
	 	&lt;arg value=&quot;--preserve-comments&quot;/&gt;
	        &lt;srcfile/&gt;
	        &lt;arg value=&quot;-o&quot;/&gt;
	        &lt;mapper type=&quot;glob&quot; from=&quot;*&quot; to=&quot;/compressed/*&quot;/&gt;
	        &lt;targetfile/&gt;
	    &lt;/apply&gt;
    &lt;/target&gt;</pre><p>This will compress all html files from <tt>/test/</tt> excluding <tt>/leave/</tt> subfolders and put results to <tt>/compressed/</tt> folder using <tt>--preserve-comments</tt> and <tt>--type html</tt> compression parameters. </p><p>Another example: </p><pre class="prettyprint">    &lt;target name=&quot;compress&quot;&gt;
    	&lt;apply executable=&quot;java&quot; parallel=&quot;false&quot; force=&quot;true&quot; dest=&quot;/test/&quot;&gt;
	        &lt;fileset dir=&quot;/test/&quot; includes=&quot;*.xml&quot;/&gt;
	        &lt;arg value=&quot;-jar&quot;/&gt;
	        &lt;arg path=&quot;/path/to/htmlcompressor-0.8.jar&quot;/&gt;
	        &lt;srcfile/&gt;
	        &lt;arg value=&quot;-o&quot;/&gt;
	        &lt;mapper type=&quot;identity&quot;/&gt;
	        &lt;targetfile/&gt;
	    &lt;/apply&gt;
    &lt;/target&gt;</pre><p>This will overwrite all xml files within <tt>/test/</tt> folder with their compressed versions. </p><h2><a name="Maven_Integration"></a>Maven Integration<a href="#Maven_Integration" class="section_anchor"></a></h2><h3><a name="Maven_Artifact"></a>Maven Artifact<a href="#Maven_Artifact" class="section_anchor"></a></h3><p>HtmlCompressor is available as a maven artifact: </p><pre class="prettyprint">&lt;dependency&gt;
  &lt;groupId&gt;com.googlecode.htmlcompressor&lt;/groupId&gt;
  &lt;artifactId&gt;htmlcompressor&lt;/artifactId&gt;
  &lt;version&gt;1.4&lt;/version&gt;
&lt;/dependency&gt;</pre><p>Please note, that HtmlCompressor uses YUI Compressor and/or Google Closure libraries if inline javascript or css compression is enabled. These dependencies were marked as optional, so you would have to declare them explicitly in your project if corresponding functionality is required: </p><pre class="prettyprint">&lt;-- Optional dependencies if js/css compression is enabled --&gt;
&lt;dependency&gt;
  &lt;groupId&gt;com.google.javascript&lt;/groupId&gt;
  &lt;artifactId&gt;closure-compiler&lt;/artifactId&gt;
  &lt;version&gt;r1043&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
  &lt;groupId&gt;com.yahoo.platform.yui&lt;/groupId&gt;
  &lt;artifactId&gt;yuicompressor&lt;/artifactId&gt;
  &lt;version&gt;2.4.6&lt;/version&gt;
&lt;/dependency&gt;</pre><h3><a name="Maven_Plugin"></a>Maven Plugin<a href="#Maven_Plugin" class="section_anchor"></a></h3><p>For compressing HTML and XML files during the build process <a href="http://code.google.com/p/htmlcompressor-maven-plugin/" rel="nofollow">Maven HTMLCompressor Plugin</a> created by Alex Tunyk is available: </p><pre class="prettyprint">&lt;build&gt;
  &lt;plugins&gt;
    &lt;plugin&gt;
      &lt;groupId&gt;com.tunyk.mvn.plugins.htmlcompressor&lt;/groupId&gt;
      &lt;artifactId&gt;htmlcompressor-maven-plugin&lt;/artifactId&gt;
      &lt;version&gt;1.0&lt;/version&gt;
      &lt;configuration&gt;
        &lt;goalPrefix&gt;htmlcompressor&lt;/goalPrefix&gt;
      &lt;/configuration&gt;
    &lt;/plugin&gt;
  &lt;/plugins&gt;
&lt;/build&gt;</pre><p>For plugin configuration options and usage details please see the <a href="http://code.google.com/p/htmlcompressor-maven-plugin/" rel="nofollow">project homepage</a>. </p><h2><a name="Who_Uses_it"></a>Who Uses it<a href="#Who_Uses_it" class="section_anchor"></a></h2><ul><li><a href="http://html5boilerplate.com/" rel="nofollow">HTML5 Boilerplate</a> </li><li><a href="http://www.spafinder.com/" rel="nofollow">SpaFinder</a> </li><li><a href="http://erik.thauvin.net/blog/" rel="nofollow">Erik&#x27;s Weblog</a> </li><li><a href="http://cybermonitor.ru/" rel="nofollow">CyberMonitor.ru</a> </li><li><a href="http://smallerapp.com/" rel="nofollow">Smaller</a> </li></ul><p>   </p>
