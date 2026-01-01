# AntdRadioGroup

## 简介源码：`views/AntdRadioGroup/intro.py`
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
                {'title': 'AntdRadioGroup 单选框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdRadioGroup 单选框', level=2),
        fac.AntdParagraph('用于供用户在一组选项中进行唯一项选择。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdRadioGroup(
    id='radio-group-demo',
    options=[
        {
            'label': f'选项{c}',
            'value': c
        }
        for c in list('abcdef')
    ],
    defaultValue='a'
),

fac.AntdParagraph(
    id='radio-group-demo-output'
)

...

@app.callback(
    Output('radio-group-demo-output', 'children'),
    Input('radio-group-demo', 'value')
)
def radio_group_demo(value):

    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdRadioGroup(
    options=[
        {
            'label': f'选项{c}',
            'value': c
        }
        for c in list('abcdef')
    ],
    defaultValue='a'
)
```

### block

- 说明：演示 block 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            block=True,
        ),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            block=True,
        ),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            buttonStyle='solid',
            block=True,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### button_mode

- 说明：演示 button_mode 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            [fac.AntdText("'outline'", code=True), '风格'],
            innerTextOrientation='left',
        ),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
        ),
        fac.AntdDivider(
            [fac.AntdText("'solid'", code=True), '风格'],
            innerTextOrientation='left',
        ),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            buttonStyle='solid',
        ),
    ],
    direction='vertical',
)
```

### component_label

- 说明：演示 component_label 的用法。

#### 代码
```python
fac.AntdRadioGroup(
    options=[
        {
            'label': fac.AntdText([fac.AntdIcon(icon=icon), f'选项{i}']),
            'value': f'选项{i}',
        }
        for i, icon in enumerate(
            ['antd-carry-out', 'antd-car', 'antd-bulb', 'antd-build']
        )
    ],
    defaultValue='选项1',
)
```

### direction

- 说明：演示 direction 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('水平排列', innerTextOrientation='left'),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
        ),
        fac.AntdDivider('竖直排列', innerTextOrientation='left'),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            direction='vertical',
        ),
    ],
    direction='vertical',
)
```

### disabled_status

- 说明：演示 disabled_status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='a',
            disabled=True
        ),

        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            disabled=True
        )
    ],
    direction='vertical'
)
```

### fast_options

- 说明：演示 fast_options 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(options=list(range(10))),
        fac.AntdRadioGroup(options=[f'选项{i}' for i in range(10)]),
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
        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='c',
            readOnly=True
        ),

        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='c',
            optionType='button',
            readOnly=True
        )
    ],
    direction='vertical'
)
```

### sizes

- 说明：演示 sizes 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            size=size
        )
        for size in [
            'small', 'middle', 'large'
        ]
    ],
    direction='vertical'
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- name (string; optional):
    配合`AntdForm`表单批量值搜集/控制功能使用，充当当前表单项的字段名，以`id`作为缺省值.

- enableBatchControl (boolean; default True):
    控制当前组件是否参与有效的`AntdForm`表单批量值搜集/控制功能  默认值：`True`.

- direction (a value equal to: 'horizontal', 'vertical'; default 'horizontal'):
    单选框排列方向，可选项有`'horizontal'`、`'vertical'`  默认值：`'horizontal'`.

- options (list of dicts; optional):
    配置选项.

    `options` is a list of string | number | dict with keys:

    - label (a list of or a singular dash component, string or number; optional):
        组件型，当前选项标签内容.

    - value (string | number; optional):
        当前选项值.

    - disabled (boolean; optional):
        是否禁用当前选项  默认值：`False`.s

- block (boolean; default False):
    是否撑满父容器  默认值：`False`.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    当`optionType='button'`时，控制各选项按钮尺寸规格，可选项有`'small'`、`'middle'`、`'large'`
    默认值：`'middle'`.

- value (string | number; optional):
    监听或设置已选值，与`format`格式对应.

- defaultValue (string | number; optional):
    初始化已选值，与`format`格式对应.

- optionType (a value equal to: 'default', 'button'; default 'default'):
    选项形式，可选项有`'default'`、`'button'`  默认值：`'default'`.

- buttonStyle (a value equal to: 'outline', 'solid'; default 'outline'):
    当`optionType='button'`时，设置按钮风格，可选项有`'outline'`、`'solid'`
    默认值：`'outline'`.

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
