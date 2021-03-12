<div class="rich_media_content " id="js_content" style="visibility: visible;">

                    <section style="font-size: 16px;color: rgb(0, 0, 0);line-height: 2.2;letter-spacing: 1.5px;font-family: Optima-Regular, Optima, PingFangSC-light, PingFangTC-light, &quot;PingFang SC&quot;, Cambria, Cochin, Georgia, Times, &quot;Times New Roman&quot;, serif;">> 作者:L_先生
> 原文链接：https://tinyurl.com/yc2cuexe

#### <span style="font-size: inherit;color: inherit;line-height: inherit;">Mysql最常用的命令</span>

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1</span>、显示数据库列表：
    show&nbsp;databases;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">2</span>、显示库中的数据表：
    show&nbsp;tables;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">3</span>、显示数据表的结构：
    describe&nbsp;表名;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">4</span>、建库：
    <span style="font-size: inherit;line-height: inherit;color: rgb(224, 196, 108);overflow-wrap: inherit !important;word-break: inherit !important;">create</span>&nbsp;database&nbsp;库名;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">5</span>、建表：
    <span style="font-size: inherit;line-height: inherit;color: rgb(224, 196, 108);overflow-wrap: inherit !important;word-break: inherit !important;">create</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(224, 196, 108);overflow-wrap: inherit !important;word-break: inherit !important;">table</span>&nbsp;表名&nbsp;(字段设定列表);

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">6</span>、删库和删表:
    drop&nbsp;database&nbsp;库名;
    drop&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(224, 196, 108);overflow-wrap: inherit !important;word-break: inherit !important;">table</span>&nbsp;表名;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">7</span>、将表中记录清空：
    delete&nbsp;from&nbsp;表名;(内容清空，自增id不会被清掉，自增id会保留)
    mysql&gt;&nbsp;truncate&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(224, 196, 108);overflow-wrap: inherit !important;word-break: inherit !important;">table</span>&nbsp;users;
    数据库返回：“Query OK, <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">0</span>&nbsp;rows&nbsp;affected&nbsp;(<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">0.04</span>&nbsp;sec)”
    （成功返回<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">0</span>）（自增id也一同会被清掉）

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">8</span>、显示表中的记录：
    <span style="font-size: inherit;line-height: inherit;color: rgb(224, 196, 108);overflow-wrap: inherit !important;word-break: inherit !important;">select</span>&nbsp;*&nbsp;from&nbsp;表名
    `</pre>

    #### <span style="font-size: inherit;color: inherit;line-height: inherit;">库的基本操作</span>

    让我们一起开始学习吧
    <pre style="font-size: inherit;color: inherit;line-height: inherit;">`1.创建数据库：
    <span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">mysql&gt;</span><span style="font-size: inherit;color: inherit;line-height: inherit;overflow-wrap: inherit !important;word-break: inherit !important;">&nbsp;create&nbsp;database&nbsp;ceshi;</span>

    2.连接数据库
    <span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">mysql&gt;</span><span style="font-size: inherit;color: inherit;line-height: inherit;overflow-wrap: inherit !important;word-break: inherit !important;">&nbsp;use&nbsp;ceshi;</span>

    3.查看当前使用的数据库
    <span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">mysql&gt;</span><span style="font-size: inherit;color: inherit;line-height: inherit;overflow-wrap: inherit !important;word-break: inherit !important;">&nbsp;select&nbsp;database();</span>

    4.当前数据库包含的表信息
    <span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">mysql&gt;</span><span style="font-size: inherit;color: inherit;line-height: inherit;overflow-wrap: inherit !important;word-break: inherit !important;">&nbsp;show&nbsp;tables;&nbsp;</span>

    5.删除数据库
    <span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">mysql&gt;</span><span style="font-size: inherit;color: inherit;line-height: inherit;overflow-wrap: inherit !important;word-break: inherit !important;">&nbsp;drop&nbsp;database&nbsp;ceshi;</span>
    `</pre>

    #### <span style="font-size: inherit;color: inherit;line-height: inherit;">表的基本操作</span>
    <pre style="font-size: inherit;color: inherit;line-height: inherit;">`一、建表

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1.</span>命令:create&nbsp;table&nbsp;&lt;表名&gt;&nbsp;(&lt;字段名&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1</span>&gt;&nbsp;&lt;类型&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1</span>&gt;&nbsp;[,..&lt;字段名&nbsp;n&gt;&nbsp;&lt;类型&nbsp;n&gt;]);

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1.1</span>例子：
    mysql&gt;&nbsp;create&nbsp;table&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>(
    id&nbsp;int(<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">4</span>)&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">not</span>&nbsp;null(不能为空)&nbsp;primary&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">key</span>（主键）&nbsp;auto_increment（自增长）,&nbsp;
    name&nbsp;varchar(<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">25</span>)&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">not</span>&nbsp;null,&nbsp;
    age&nbsp;int&nbsp;(<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">4</span>)&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">not</span>&nbsp;null&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">default</span><span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">'0');&nbsp;&nbsp;&nbsp;&nbsp;（default'0'&nbsp;设置默认值为0）</span>

    二、获取表结构
    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">2</span>命令:&nbsp;desc&nbsp;表名，或者show&nbsp;columns&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">from</span>&nbsp;表名

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">2.1</span>例子：
    mysql&gt;&nbsp;desc&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>;
    mysql&gt;&nbsp;describe&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>;
    mysql&gt;&nbsp;show&nbsp;columns&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">from</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>;

    三、插入数据
    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">3.</span>命令:insert&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">into</span>&nbsp;&lt;表名&gt;&nbsp;[(&nbsp;&lt;字段名&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1</span>&gt;[,..&lt;字段名&nbsp;n&nbsp;&gt;&nbsp;])]&nbsp;values&nbsp;(&nbsp;值&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1</span>&nbsp;)[,&nbsp;(&nbsp;值&nbsp;n&nbsp;)]

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">3.1</span>例子：
    mysql&gt;&nbsp;insert&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">into</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;values(<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1</span>,<span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">'Wrry',26),(2,'ZJW',28);</span>

    四、查询表中的数据

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">4.</span>查询所有行

    mysql&gt;&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">select</span>&nbsp;*&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">from</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">4.1</span>查询前几行数据

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">4.1</span><span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">.1</span>例如:查看表&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;中前&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">3</span>&nbsp;行数据
    mysql&gt;&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">select</span>&nbsp;*&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">from</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;limit&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">0</span>,<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">3</span>;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">4.1</span><span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">.2</span>或者
    mysql&gt;&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">select</span>&nbsp;*&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">from</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">order</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">by</span>&nbsp;id&nbsp;limit&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">0</span>,<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">3</span>;&nbsp;&nbsp;&nbsp;&nbsp;（<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">order</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">by</span>&nbsp;id &nbsp;：以id排序）

    五、删除表中数据

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">5.1</span>命令:
    delete&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">from</span>&nbsp;表名&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">where</span>&nbsp;表达式

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">5.2</span>例如:删除表&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;中编号为&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">6</span>&nbsp;的记录
    mysql&gt;&nbsp;delete&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">from</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">MyClass</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">where</span>&nbsp;id=<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">1</span>;

    六、修改表中数据

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">6.</span>命令:
    update&nbsp;表名&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">set</span>&nbsp;字段=新值,...&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">where</span>&nbsp;条件
    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">6.1</span>例如:
    mysql&gt;&nbsp;update&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">set</span>&nbsp;name=<span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">'AI'&nbsp;where&nbsp;id=1;</span>

    七、在表中增加字段

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">7</span>命令:alter&nbsp;table&nbsp;表名&nbsp;add&nbsp;字段&nbsp;类型&nbsp;其他;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">7.1</span>例如:在表&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;中添加了一个字段&nbsp;sex,类型为&nbsp;varchar(<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">25</span>),默认值为&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">0</span>
    mysql&gt;&nbsp;alter&nbsp;table&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;add&nbsp;sex&nbsp;varchar(<span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">25</span>)&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">default</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(127, 127, 127);overflow-wrap: inherit !important;word-break: inherit !important;">'0'</span>

    八、更改表名

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">8.</span>命令:rename&nbsp;table&nbsp;原表名&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">to</span>&nbsp;新表名;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">8.1</span>例如:在表&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;名字更改为&nbsp;MClass
    mysql&gt;&nbsp;rename&nbsp;table&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">Class</span>&nbsp;<span style="font-size: inherit;line-height: inherit;color: rgb(203, 120, 50);overflow-wrap: inherit !important;word-break: inherit !important;">to</span>&nbsp;MClass;

    九、删除表

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">9.</span>命令:drop&nbsp;table&nbsp;&lt;表名&gt;

    <span style="font-size: inherit;line-height: inherit;color: rgb(104, 150, 186);overflow-wrap: inherit !important;word-break: inherit !important;">9.1</span>例如:删除表名为&nbsp;MClass&nbsp;的表

    mysql&gt;&nbsp;drop&nbsp;table&nbsp;MClass;
</section>

                </div>
