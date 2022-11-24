原文：

[wpf UniformGrid使用小计](https://www.cnblogs.com/Jeffrey-Chou/p/12284692.html)

# [WPF之UniformGrid使用小记 ](https://www.cnblogs.com/Jeffrey-Chou/p/12284692.html)

### 一. 小记

这边为了以后看的方便，对 UniformGrid 的使用做了一个简单的归纳。UniformGrid 是一种横向的网格分割、纵向的网格分割分别是均等的分割的布局类型，故称为 " 均分布局 "。

### 二. 一些使用上的特点

1. 各个单元格的大小完全相同，宽与高分别相同；

2. **默认情况下**，单元格的数量取决于放入的控件的数量，且单元格一定是行、列数相同，即 1X1、2X2 、3X3 等等的单元格分布；

测试代码如下：

```
<UniformGrid>
    <Rectangle Fill="Aqua"/>
    <Rectangle Fill="Red"/>
</UniformGrid>
```

测试结果如下，UniformGrid 中只有两个元素，但是显示成了 2X2 分布：

![img](E:\codes\c-sharp\WPF\前端\Imag\1421482-20200209205050880-1520810645.png)

★**（重要、常用）** 

3. UniformGrid 有两个属性，分别是：Columns 和 Rows ，它们是分别用来指定当前的最大列数和最大的行数，如果只设置了其中一个而不设置另外一个的话，那么没有设置的那个默认为 1；在设置的这两个属性的情况下，UniformGrid 不再会按照行、列数相同来分布，而是按照用户指定的 Columns 和 Rows 来分布；

测试代码，我们创建一个 2X3 的 UniformGrid：

```
<UniformGrid Columns="2" Rows="3">
    <Rectangle Fill="Aqua"/>
    <Rectangle Fill="Red"/>
    <Rectangle Fill="Red"/>
    <Rectangle Fill="Aqua"/>
    <Rectangle Fill="Aqua"/>
    <Rectangle Fill="Red"/>
</UniformGrid>
```

测试结果如下：

![img](E:\codes\c-sharp\WPF\前端\Imag\1421482-20200209205627079-1044146599.png)

\4. 对于 Grid 的属性 Grid.Row 、Grid.Column 和 Grid.RowSpan 、Grid.ColumnSpan 用在 UniformGrid 上会没有任何的效果（虽然可以写上去，因为是附加属性）；

测试代码如下：

```
<UniformGrid>
    <Rectangle Fill="Aqua" Grid.Column="2" Grid.Row="3"/>
    <Rectangle Fill="RoyalBlue"/>
    <Rectangle Fill="RoyalBlue" Grid.ColumnSpan="2"/>
</UniformGrid>
```

测试结果如下，对于 Grid.Row 、Grid.Column 和 Grid.ColumnSpan、Grid.RowSpan 是无效的：

![img](E:\codes\c-sharp\WPF\前端\Imag\1421482-20200209211154115-1734341027.png)

### 三. 测试代码下载

[代码下载](https://files.cnblogs.com/files/Jeffrey-Chou/WPF之UniformGrid使用小记.zip)