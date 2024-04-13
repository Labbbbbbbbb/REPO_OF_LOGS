消息内容[定义于与之关联的xml 文件中](https://mavlink.io/zh/messages/)。 每个xml文件对应一个特定的MAVLink系统，并为该系统定义了专属的消息集（亦被称之为“语支dialect”）。 *大部分* 地面站和自动驾驶仪所采用的“通用消息集”定义于 [common.xml](https://mavlink.io/zh/messages/common.html)中 (大多数“语支”均是基于“通用消息集“*构建* 的：即，大多数“语支”所对应的xml文件里，均包含了common.xml) 。

参考：

[MAVLink XML Schema · MAVLink Developer Guide](https://mavlink.io/zh/guide/xml_schema.html)

common.xml文件：[mavlink/message_definitions/v1.0/common.xml at master · mavlink/mavlink (github.com)](https://github.com/mavlink/mavlink/blob/master/message_definitions/v1.0/common.xml) （同路径下还有很多示例.xml文件）


### 文件结构

```
<?xml version="1.0"?>
<mavlink>

    <include>common.xml</include>
    <include>other_dialect.xml</include>

    <!-- NOTE: If the included file already contains a version tag, remove the version tag here, else uncomment to enable. -->
    <!-- <version>6</version> -->

    <dialect>8</dialect>

    <enums>
        <!-- Enums are defined here (optional) -->
    </enums>

    <messages>
        <!-- Messages are defined here (optional) -->
    </messages>

</mavlink>
```

以上示例结构中含有几个主要标签（所有标签都是可选的）

`include` : 指定所包含的其他xml文件，通常会包含 `common.xml`

`version`: 版本的次要版本号

`dialect` : 这个数字是该语支的版本号

`enums` : 枚举类型的定义，若用不上可以删除该块

`messages` : 可以在此块中定义特定于语支的消息，若用不上可以删除该块

> `<?xml version="1.0"?>` 是 XML 文件的声明，它表明这是一个 XML 文档，并指定了 XML 的版本。在这个声明中，`version="1.0"` 表示使用的是 XML 1.0 版本规范。这个声明通常出现在 XML 文件的开头，用于告诉解析器如何解析 XML 文档。
>
> 而 `<version>` 标签是在 MAVLink XML 文件中用来指定所描述的 MAVLink 协议的版本号。这个版本号用于确定 XML 文件所描述的协议规范的版本，以及定义了该协议版本的特性和规范。
>
> 两者的区别在于，`<?xml version="1.0"?>` 是 XML 文件的声明，用于指定 XML 版本，而 `<version>` 标签是在 XML 文件中用来指定描述的 MAVLink 协议的版本。它们都是用于标识文件或协议的版本信息，但它们所代表的范围和意义不同。

实际编写mavlink的xml文件时的常用模板：

```
<?xml version="1.0"?>
<mavlink>
  <version>3</version>
  <messages>
    <message id="1" name="SPEED">
      <description>机器人的速度</description>
      <field type="double" name="vx">x 方向速度</field>
      <field type="double" name="vy">y 方向速度</field>
      <field type="double" name="rot">z 方向角速度</field>
    </message>
    <message id="2" name="GYRO">
      <description>陀螺仪数据</description>
      <field type="int16_t" name="gx">x 方向角速度</field>
      <field type="int16_t" name="gy">y 方向角速度</field>
      <field type="int16_t" name="gz">z 方向角速度</field>
      <field type="int16_t" name="ax">x 方向加速度</field>
      <field type="int16_t" name="ay">y 方向加速度</field>
      <field type="int16_t" name="az">z 方向加速度</field>
    </message>
  </messages>
</mavlink>
```
