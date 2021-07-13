

https://r4ds.had.co.nz/data-visualisation.html

https://jrnold.github.io/r4ds-exercise-solutions/data-visualisation.html

# **1 Introduction**

![img](ReadingNotes.assets/data-science-explore.png)

**Tidying**和**Transforming**合称**Wrangling**。

数据分析完成之后的**Communication**意味着分析结果不能仅仅被自己理解，更需要让他人理解。

本书所提供的内容是你在各种数据科学项目中会用的工具，大概占80%的比例，但各个项目中可能总有20%的工具是在本书之外的。



本书先从作图开始，这样子会更有趣；然后是处理数据的部分；接着是更高阶的编程部分。



本书不会处理大数据、Python/Julia、非矩形数据、假设检验等问题。



本书需要的工具是`R`、`RStuidio`、`tidyverse`以及额外的一些`R`包。

此外本书还会用到如下数据集：

```R
install.packages(c("nycflights13", "gapminder", "Lahman"))
```

> 其实整本书都是以`RStudio`、`tidyverse`生态为基础的。不过，书中也会在一些地方给出与`baseR`的对比，在对比中可以看到其相应的操作方式。



在网络上提问时，应该给他人提供最小可复现样例（**reprex**）：

1. 你使用的`Packages`；
2. 使用`dput()`函数输出一个**数据**样例；
3. 尽量保证你的**代码**具有较高的可读性。



# **Explore**

# **3 Data Visualization**

用`ggplot2::mpg`这个数据集来展示一些基本操作。

```R
ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))
```

`ggplot2`的图是由层构成的,`+`号就是层的一种叠加。



同一张点图，信息也可以逐步丰富的。画图，信息要浓缩在其中。
![img](ReadingNotes.assets/unnamed-chunk-3-1.png)
```R
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class))
```
![img](ReadingNotes.assets/unnamed-chunk-7-1.png)

这个过程叫做**scaling**。当然scaling的方法多种多样。



`ggplot2`的帮助：https://ggplot2.tidyverse.org/

`ggplot2`的扩展：https://exts.ggplot2.tidyverse.org/gallery/

`ggplot2`的cheatsheet：https://www.rstudio.com/resources/cheatsheets/



关于数据 **mapping**，你既可以写在`ggplot()`里面，这代表着是**全局**的，也可以写在`geom_function()`里面，这表示是**局部**的。



`ggplot2`里提供了大约20种统计值（参见`?stat_bin`）。



`group`需要多多注意：https://ggplot2.tidyverse.org/reference/aes_group_order.html

hist、bar、line之类的图中经常用到，如果不加该参数可能会使图像出错。

![img](ReadingNotes.assets/visualization-stat-bar.png)

`position` 有三个值：`"identity"`, `"dodge"` or `"fill"`。而关于位置调整的参数，可见下述：`?position_dodge`, `?position_fill`, `?position_identity`, `?position_jitter`, and `?position_stack`。



坐标系是较为复杂的部分，`coord_flip()` 可以调换x轴和y轴；`coord_polar()` 可以调用极坐标系；`coord_quickmap()` 则针对地图



总的来说，作图的图层如下：

```R
ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(
     mapping = aes(<MAPPINGS>),
     stat = <STAT>, 
     position = <POSITION>
  ) +
  <COORDINATE_FUNCTION> +
  <FACET_FUNCTION>
```

除了data、geom_function、mapping之外，其他都带有默认值。





在作图中，需要注意的方面包括：

1. `ggplot()`构造出画布
2. Aesthetic mapping，`aes(<MAPPINGS>)`添加对象和colour、size、shape属性
3. `facets`，安排图像的呈现
4. `geom_XXX()`构造不同对象的几何图形
5. 有些图其实在绘制的过程进行了一些**统计**（stat），例如`bar`；**stat** 和 **geom**有一定的对应的关系，两者可以呼唤，例如`stat_count()`和`geom_bar()`
6. Position的调整会改变出图的形式，比如是堆叠在一起，还是分别呈现
7. 坐标系，一般都是使用笛卡尔坐标系，但涉及到地图类型的就会更复杂



![img](ReadingNotes.assets/visualization-grammar-1.png)

![img](ReadingNotes.assets/visualization-grammar-2.png)![img](ReadingNotes.assets/visualization-grammar-3.png)



# **4 Workflow: basics**

