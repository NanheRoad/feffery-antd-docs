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

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - root (dict; optional):
        根元素css样式.

    - track (dict; optional):
        范围选择下，点和点之间单个选取条css样式.

    - tracks (dict; optional):
        范围选择下，整个范围选取条css样式.

    - rail (dict; optional):
        背景条css样式.

    - handle (dict; optional):
        抓取点元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - root (string; optional):
        根元素css类名.

    - track (string; optional):
        范围选择下，点和点之间单个选取条css类名.

    - tracks (string; optional):
        范围选择下，整个范围选取条css类名.

    - rail (string; optional):
        背景条css类名.

    - handle (string; optional):
        抓取点元素css类名.

- name (string; optional):
    配合`AntdForm`表单批量值搜集/控制功能使用，充当当前表单项的字段名，以`id`作为缺省值.

- enableBatchControl (boolean; default True):
    控制当前组件是否参与有效的`AntdForm`表单批量值搜集/控制功能  默认值：`True`.

- vertical (boolean; default False):
    是否以垂直模式显示  默认值：`False`.

- range (dict; default False):
    是否以范围模式显示.

    `range` is a boolean | dict with keys:

    - editable (boolean; optional):
        是否开启节点动态增减功能  默认值：`False`.

    - minCount (number; optional):
        开启节点动态增减功能后，允许的最小节点数量  默认值：`0`.

    - maxCount (number; optional):
        开启节点动态增减功能后，允许的最大节点数量.

- min (number; default 0):
    必填，可滑动范围下限.

- max (number; default 100):
    必填，可滑动范围上限.

- step (number; default 1):
    滑动步长.

- marks (dict with strings as keys and values of type a list of or a singular dash component, string or number; optional):
    为部分数值设置刻度信息.

- tooltipVisible (boolean; optional):
    滑动数值文字提示显示策略，`True`表示持续显示，`False`表示始终不显示.

- tooltipPrefix (string; default ''):
    滑动数值文字提示前缀信息.

- tooltipSuffix (string; default ''):
    滑动数值文字提示后缀信息.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- value (number | list of numbers; optional):
    监听或设置已选值.

- defaultValue (number | list of numbers; optional):
    初始化已选值.

- autoFocus (boolean; default False):
    是否允许一键清空已选值  默认值：`True`.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    相关展开层锚定策略，可选项有`'parent'`、`'body'`  默认值：`'body'`.

- readOnly (boolean; default False):
    是否渲染为只读状态  默认值：`False`.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; optional):
    开启属性持久化功能的若干属性名，可选项有`'value'`  默认值：`['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.
