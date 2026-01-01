# AntdStatistic

## 简介源码：`views/AntdStatistic/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdStatistic 统计数值'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdStatistic 统计数值', level=2),
        fac.AntdParagraph('用于构建漂亮的统计数值展示。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdStatistic(
    id='statistic-demo',
    precision=2,
    title='XX股份实时股价',
    value=675.32,
    valueStyle={'color': '#cf1322'},
    prefix=fac.AntdIcon(icon='antd-rise'),
),
dcc.Interval(id='statistic-interval-demo', n_intervals=0),

...

@app.callback(
    [
        Output('statistic-demo', 'value'),
        Output('statistic-demo', 'prefix'),
        Output('statistic-demo', 'valueStyle'),
    ],
    Input('statistic-interval-demo', 'n_intervals'),
    State('statistic-demo', 'value'),
)
def statistic_demo_callback(n_intervals, value):
    new_value = value + np.random.randn()

    if new_value >= value:
        return [new_value, fac.AntdIcon(icon='antd-rise'), {'color': '#cf1322'}]

    else:
        return [new_value, fac.AntdIcon(icon='antd-fall'), {'color': '#3f8600'}]
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdStatistic(title='数值型统计数值示例', value=1321321.3213),
        fac.AntdStatistic(title='字符型统计数值示例', value='99.65%'),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)
```

### countup

- 说明：演示 countup 的用法。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdStatistic(
                title='Active Users',
                value=fuc.FefferyCountUp(end=112893, duration=3),
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdStatistic(
                title='Account Balance (CNY)',
                value=fuc.FefferyCountUp(end=112893, duration=3),
            ),
            span=12,
        ),
    ],
    gutter=16,
)
```

### group_separator

- 说明：演示 group_separator 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdDivider(
            fac.AntdText('showGroupSeparator=True', code=True),
            innerTextOrientation='left',
        ),
        fac.AntdStatistic(
            title='数值型统计数值示例',
            value=1321321.3213,
            showGroupSeparator=True,
        ),
        fac.AntdDivider(
            fac.AntdText('showGroupSeparator=False', code=True),
            innerTextOrientation='left',
        ),
        fac.AntdStatistic(
            title='数值型统计数值示例',
            value=1321321.3213,
            showGroupSeparator=False,
        ),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)
```

### precision

- 说明：演示 precision 的用法。

#### 代码
```python
fac.AntdStatistic(
    title='数值型统计数值示例', value=1321321.3213, precision=2
)
```

### title_tooltip

- 说明：演示 title_tooltip 的用法。

#### 代码
```python
fac.AntdStatistic(
    title='数值统计示例', value=98.67, titleTooltip='这是信息提示示例'
)
```

### unit

- 说明：演示 unit 的用法。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdStatistic(
                title='Feedback',
                value=1128,
                prefix=fac.AntdIcon(icon='antd-like'),
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdStatistic(title='Unmerged', value=93, suffix='/ 100'),
            span=12,
        ),
    ],
    gutter=16,
)
```

### used_in_card

- 说明：演示 used_in_card 的用法。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdCard(
                fac.AntdStatistic(
                    title='Active',
                    value=11.28,
                    precision=2,
                    valueStyle={
                        'color': '#3f8600',
                    },
                    prefix=fac.AntdIcon(icon='antd-arrow-up'),
                    suffix='%',
                ),
                title='Card One',
                variant='borderless',
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdCard(
                fac.AntdStatistic(
                    title='Idle',
                    value=9.3,
                    precision=2,
                    valueStyle={
                        'color': '#cf1322',
                    },
                    prefix=fac.AntdIcon(icon='antd-arrow-down'),
                    suffix='%',
                ),
                title='Card Two',
                variant='borderless',
            ),
            span=12,
        ),
    ],
    gutter=16,
    style={
        'backgroundColor': '#f0f2f5',
        'padding': '16px'
    }
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- value (number | string | a list of or a singular dash component, string or number; optional):
    支持组件型，要展示的数值.

- showGroupSeparator (boolean; default True):
    是否为数值型`value`添加千分位符  默认值：`True`.

- precision (number; optional):
    针对数值型`value`，设置数值精度.

- prefix (a list of or a singular dash component, string or number; optional):
    组件型，数值前缀内容.

- suffix (a list of or a singular dash component, string or number; optional):
    组件型，数值后缀内容.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- titleTooltip (string; optional):
    为标题内容添加额外鼠标悬停提示信息.

- valueStyle (dict; optional):
    数值内容css样式.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.
