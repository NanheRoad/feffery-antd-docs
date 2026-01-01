# AntdSlider

## 简介源码：`views/AntdSlider/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': 'AntdSlider 滑动输入条'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSlider 滑动输入条', level=2),
        fac.AntdParagraph('用于为用户提供基于滑动交互的单值或范围设置功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSlider(
    id='slider-demo',
    min=0,
    max=100,
    defaultValue=33,
    style={
        'width': 300
    }
),
fac.AntdText(
    id='slider-demo-output'
),

fac.AntdSlider(
    id='slider-range-demo',
    range=True,
    min=0,
    max=100,
    defaultValue=[10, 90],
    style={
        'width': 300
    }
),
fac.AntdText(
    id='slider-range-demo-output'
)

...

@app.callback(
    Output('slider-demo-output', 'children'),
    Input('slider-demo', 'value')
)
def slider_demo(value):

    return f'value: {value}'


@app.callback(
    Output('slider-range-demo-output', 'children'),
    Input('slider-range-demo', 'value')
)
def slider_range_demo(value):

    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSlider(min=0, max=100, defaultValue=33, style={'width': 300}),
fac.AntdSlider(
    range=True,
    min=0,
    max=100,
    defaultValue=[10, 90],
    style={'width': 300},
)
```

### custom_marks

- 说明：演示 custom_marks 的用法。

#### 代码
```python
fac.AntdSlider(
    min=0,
    max=100,
    defaultValue=50,
    marks={i * 10: f'{i*10}%' for i in range(0, 11)},
    style={'width': 300},
)
```

### custom_step

- 说明：演示 custom_step 的用法。

#### 代码
```python
fac.AntdSlider(
    min=0,
    max=100,
    defaultValue=50,
    step=10,
    style={
        'width': 300
    }
)
```

### disabled_status

- 说明：演示 disabled_status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSlider(
            min=0,
            max=100,
            defaultValue=33,
            disabled=True,
            style={'width': 300},
        ),
        fac.AntdSlider(
            range=True,
            min=0,
            max=100,
            defaultValue=[10, 90],
            disabled=True,
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### editable

- 说明：演示 editable 的用法。

#### 代码
```python
fac.AntdSlider(
    min=0,
    max=100,
    defaultValue=[20, 30, 40, 50],
    range={
        'editable': True,
        'minCount': 3,
        'maxCount': 8,
    },
    style={'width': 300},
)
```

### rail_style

- 说明：演示 rail_style 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSlider(
            min=0,
            max=100,
            defaultValue=33,
            style={'width': 300},
            styles={'rail': {'background': '#37d67a'}},
        ),
        fac.AntdSlider(
            range=True,
            min=0,
            max=100,
            defaultValue=[10, 90],
            style={'width': 300},
            styles={'rail': {'background': '#37d67a'}},
        ),
    ],
    direction='vertical',
)
```

### read_only_status

- 说明：演示 read_only_status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSlider(
            min=0,
            max=100,
            defaultValue=33,
            readOnly=True,
            style={'width': 300},
        ),
        fac.AntdSlider(
            range=True,
            min=0,
            max=100,
            defaultValue=[10, 90],
            readOnly=True,
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### tooltip_prefix_suffix

- 说明：演示 tooltip_prefix_suffix 的用法。

#### 代码
```python
fac.AntdSlider(
    min=0,
    max=100,
    defaultValue=50,
    tooltipPrefix='当前值：',
    tooltipSuffix='%',
    style={
        'width': 300
    }
)
```

### tooltip_visible

- 说明：演示 tooltip_visible 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            fac.AntdText('tooltipVisible=True', code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSlider(
            min=0,
            max=100,
            defaultValue=50,
            tooltipVisible=True,
            style={'width': 300},
        ),
        fac.AntdDivider(
            fac.AntdText('tooltipVisible=False', code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSlider(
            min=0,
            max=100,
            defaultValue=50,
            tooltipVisible=False,
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### vertical_mode

- 说明：演示 vertical_mode 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSlider(
            vertical=True,
            min=0,
            max=100,
            defaultValue=33,
            style={'height': 200},
        ),
        fac.AntdSlider(
            vertical=True,
            range=True,
            min=0,
            max=100,
            defaultValue=[10, 90],
            style={'height': 200},
        ),
    ]
)
```
