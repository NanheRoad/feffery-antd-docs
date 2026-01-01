# AntdMentions

## 简介源码：`views/AntdMentions/intro.py`
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
                {'title': 'AntdMentions 提及'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdMentions 提及', level=2),
        fac.AntdParagraph(
            '用于实现在输入内容中对不同角色进行提及的功能，常用于构建论坛、协同办公等平台中的评论功能。'
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### auto_size

- 说明：演示 auto_size 的用法。

#### 代码
```python
fac.AntdDivider(
    'autoSize=False（默认）',
    innerTextOrientation='left'
),
fac.AntdMentions(
    defaultValue='示例内容'*20,
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    style={
        'width': 300
    }
),

fac.AntdDivider(
    'autoSize=True',
    innerTextOrientation='left'
),
fac.AntdMentions(
    defaultValue='示例内容'*20,
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    autoSize=True,
    style={
        'width': 300
    }
),

fac.AntdDivider(
    '配置minRows、maxRows参数',
    innerTextOrientation='left'
),
fac.AntdMentions(
    defaultValue='示例内容'*20,
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    autoSize={
        'minRows': 2,
        'maxRows': 6
    },
    style={
        'width': 300
    }
)
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdMentions(
    id='mentions-demo',
    autoSize={
        'minRows': 2,
        'maxRows': 4
    },
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    style={
        'width': 300
    }
),

html.Br(),

fac.AntdSpace(
    id='mentions-demo-output',
    direction='vertical'
)

...

@app.callback(
    Output('mentions-demo-output', 'children'),
    [Input('mentions-demo', 'value'),
     Input('mentions-demo', 'selectedOptions')]
)
def mentions_demo(value, selectedOptions):

    return [
        fac.AntdText(
            f'value: {value}'
        ),
        fac.AntdText(
            f'selectedOptions: {selectedOptions}'
        )
    ]
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdMentions(
    placeholder='请输入@',
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    style={
        'width': 200
    }
)
```

### different_placement

- 说明：演示 different_placement 的用法。

#### 代码
```python
fac.AntdMentions(
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    placement='top',
    style={
        'width': 200
    }
)
```

### disabled_status

- 说明：演示 disabled_status 的用法。

#### 代码
```python
fac.AntdMentions(
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    disabled=True,
    style={
        'width': 200
    }
)
```

### render_status

- 说明：演示 render_status 的用法。

#### 代码
```python
fac.AntdDivider(
    'status="warning"',
    innerTextOrientation='left'
),
fac.AntdMentions(
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    status='warning',
    style={
        'width': 200
    }
),

fac.AntdDivider(
    'status="error"',
    innerTextOrientation='left'
),
fac.AntdMentions(
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    status='error',
    style={
        'width': 200
    }
)
```

### trigger_keyword

- 说明：演示 trigger_keyword 的用法。

#### 代码
```python
fac.AntdMentions(
    placeholder='请输入#',
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    prefix='#',
    style={
        'width': 200
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

- popupClassName (string; optional):
    展开菜单css类名.

- name (string; optional):
    配合`AntdForm`表单批量值搜集/控制功能使用，充当当前表单项的字段名，以`id`作为缺省值.

- enableBatchControl (boolean; default True):
    控制当前组件是否参与有效的`AntdForm`表单批量值搜集/控制功能  默认值：`True`.

- autoSize (dict; default False):
    配置输入框高度自适应相关功能  默认值：`False`.

    `autoSize` is a boolean | dict with keys:

    - minRows (number; optional):
        输入框最小行数.

    - maxRows (number; optional):
        输入框最大行数.

- prefix (string; default '@'):
    触发选择菜单展开的关键字  默认值：`'@'`.

- value (string; optional):
    监听或设置已输入值.

- defaultValue (string; optional):
    初始化已输入值.

- options (list of dicts; required):
    必填，配置选择菜单子项.

    `options` is a list of dicts with keys:

    - label (a list of or a singular dash component, string or number; optional):
        组件型，当前选项标签内容.

    - value (string; optional):
        当前选项值.

- selectedOptions (list of strings; optional):
    监听输入内容中对应的已选子项值.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- placement (a value equal to: 'top', 'bottom'; default 'bottom'):
    选择菜单弹出方向，可选项有`'top'`、`'bottom'`  默认值：`'bottom'`.

- bordered (boolean; default True):
    是否显示边框，设置为`True`时等价于`variant='outlined'`  默认值：`True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):
    形态变体类型，可选项有`'outlined'`、`'borderless'`、`'filled'`、`'underlined'`，其中`'outlined'`等价于`bordered=True`，但优先级更高.

- placeholder (string; optional):
    输入框占位文字内容.

- status (a value equal to: 'error', 'warning'; optional):
    控制校验状态，可选项有`'error'`、`'warning'`.

- autoFocus (boolean; default False):
    是否自动获取焦点  默认值：`False`.

- popupContainer (a value equal to: 'parent', 'body'; optional):
    相关展开层锚定策略，可选项有`'parent'`、`'body'`  默认值：`'body'`.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
