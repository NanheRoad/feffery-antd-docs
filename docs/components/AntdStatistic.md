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
