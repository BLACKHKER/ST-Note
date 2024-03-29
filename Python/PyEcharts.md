## PyEcharts

> 第三方图标开发框架(百度)

##### 官网

```http
pyecharts.org
```



##### 画廊

```http
gallery.pyecharts.org
```







### 配置

#### 全局配置

> 针对整个图进行配置(标题、图例、工具箱)

##### set_global_opts

```python
from pyecharts.charts import Line
# 标题包
from pyecharts.options import TitleOpts

# 创建一个折线图对象
line = Line()
line.set_global_opts(
    # 标题配置(标题名，位置[横向]，高度[纵向])
    title_opts=TitleOpts(title="测试", pos_left="center", pos_bottom="1%"),
    # 图例配置(是否展示)
    legend_opts=LegendOpts(is_show=True),
    # 工具箱配置(是否展示)
    toolbox_opts=ToolboxOpts(is_show=True),
    # 视觉映射(是否展示)
    visualmap_opts=VisualMapOps(is_show=True),
    tooltip_opts=TooltipOpts(is_show=True)
)
```





#### 系列配置

> 轴数据配置









### 折线图

#### 基础折线图

> 运行后会在当前文件下生成一个html页面，打开就是生成的数据图

##### 导包

```python
from pyecharts.charts import Line
```



##### 示例

```python
# 创建一个折线图对象
line = Line()
# 给折线图添加X轴数据
line.add_xaxis(["中国", "美国", "英国"])
# 给折线图添加Y轴数据
line.add_yaxis("GDP", [30, 20, 10])
# 通过render()方法，将代码生成为图像
line.render()
```

