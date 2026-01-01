# AntdSteps

## 简介源码：`views/AntdSteps/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

# 国际化
from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('导航')},
                {'title': translator.t('AntdSteps 步骤条')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdSteps 步骤条'), level=2),
        fac.AntdParagraph(
            translator.t('用于引导用户按照流程完成一系列连贯的步骤。')
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### 回调监听

- 说明：通过回调函数监听并控制步骤条功能。

#### 代码
```python
[
    fac.AntdSteps(
        id='steps-demo',
        steps=[{'title': f'步骤{i}'} for i in range(5)],
        direction='horizontal',
        type='navigation',
        allowClick=True,
    ),
    fac.AntdDivider(isDashed=True),
    fac.AntdButton('下一步', id='steps-demo-go-next', type='primary'),
    fac.AntdDivider(direction='vertical'),
    fac.AntdButton('上一步', id='steps-demo-go-last', type='primary'),
    fac.AntdDivider(direction='vertical'),
    fac.AntdButton('重置', id='steps-demo-restart', type='primary'),
    fac.AntdDivider(isDashed=True),
    fac.AntdText(id='steps-demo-current'),
]

...

@app.callback(
    Output('steps-demo', 'current'),
    [
        Input('steps-demo-go-next', 'nClicks'),
        Input('steps-demo-go-last', 'nClicks'),
        Input('steps-demo-restart', 'nClicks'),
    ],
    State('steps-demo', 'current'),
    prevent_initial_call=True,
)
def steps_callback_demo_part1(go_next, go_last, restart, current):
    ctx = dash.callback_context

    if ctx.triggered[0]['prop_id'].startswith('steps-demo-go-next'):
        return current + 1

    elif ctx.triggered[0]['prop_id'].startswith('steps-demo-go-last'):
        return max(current - 1, 0)

    else:
        return 0


@app.callback(
    Output('steps-demo-current', 'children'),
    Input('steps-demo', 'current'),
    prevent_initial_call=True,
)
def steps_callback_demo_part2(current):
    return f'当前步骤为：步骤{current}'
```

### 基础使用

- 说明：基础的静态步骤条。

#### 代码
```python
fac.AntdSteps(
    steps=[{'title': f'步骤{i + 1}'} for i in range(3)]
)
```

### 允许点击切换步骤

- 说明：设置参数`allowClick=True`后可直接点击步骤进行步骤切换。

#### 代码
```python
fac.AntdSteps(
    steps=[{'title': f'步骤{i + 1}'} for i in range(3)], allowClick=True
)
```

### 控制当前步骤状态

- 说明：None

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSteps(
            steps=[
                {
                    'title': f'步骤{i + 1}的title',
                    'subTitle': f'步骤{i + 1}的subTitle',
                    'description': f'步骤{i + 1}的description',
                }
                for i in range(3)
            ],
            current=2,
            status=status,
        )
        for status in ['process', 'wait', 'finish', 'error']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 自定义图标

- 说明：步骤图标可传入任意组件型内容。

#### 代码
```python
fac.AntdSteps(
    steps=[
        {
            'title': 'Login',
            'status': 'finish',
            'icon': fac.AntdIcon(icon='antd-user'),
        },
        {
            'title': 'Verification',
            'status': 'finish',
            'icon': fac.AntdIcon(icon='antd-file-protect'),
        },
        {
            'title': 'Pay',
            'status': 'process',
            'icon': fac.AntdIcon(icon='antd-loading'),
        },
        {
            'title': 'Done',
            'status': 'wait',
            'icon': fac.AntdIcon(icon='antd-smile'),
        },
    ]
)
```

### 点状步骤条

- 说明：简洁风格的点状步骤条。

#### 代码
```python
fac.AntdSteps(
    steps=[
        {
            'title': f'步骤{i + 1}的title',
            'subTitle': f'步骤{i + 1}的subTitle',
            'description': f'步骤{i + 1}的description',
        }
        for i in range(3)
    ],
    progressDot=True,
)
```

### 内联风格步骤条

- 说明：None

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdFlex(
            [
                fac.AntdTitle('计算任务xxx', level=4),
                fac.AntdText(
                    '这是计算任务xxx的描述信息balabalabala',
                    type='secondary',
                ),
            ],
            vertical=True,
        ),
        fac.AntdSteps(
            steps=[
                {
                    'title': f'步骤{i + 1}',
                    'description': f'这是步骤{i + 1}的描述',
                }
                for i in range(3)
            ],
            type='inline',
            style={'height': 50},
        ),
    ],
    justify='space-between',
    align='flex-end',
)
```

### 导航风格步骤条

- 说明：None

#### 代码
```python
fac.AntdSteps(
    steps=[
        {
            'title': f'步骤{i + 1}的title',
            'subTitle': f'步骤{i + 1}的subTitle',
            'description': f'步骤{i + 1}的description',
        }
        for i in range(3)
    ],
    type='navigation',
    current=2,
)
```

### 当前步骤环状进度

- 说明：通过设置参数`percent`控制当前步骤的环状进度显示效果。

#### 代码
```python
fac.AntdSteps(
    steps=[{'title': f'步骤{i + 1}'} for i in range(3)],
    current=1,
    percent=66,
)
```

### 设置当前所在步骤

- 说明：通过参数`current`可控制当前步骤条所在步骤。

#### 代码
```python
fac.AntdSteps(
    steps=[
        {
            'title': f'步骤{i + 1}的title',
            'subTitle': f'步骤{i + 1}的subTitle',
            'description': f'步骤{i + 1}的description',
        }
        for i in range(3)
    ],
    current=2,
)
```

### 尺寸规格

- 说明：不同尺寸的步骤条。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSteps(
            steps=[
                {
                    'title': f'步骤{i + 1}的title',
                    'subTitle': f'步骤{i + 1}的subTitle',
                    'description': f'步骤{i + 1}的description',
                }
                for i in range(3)
            ]
        ),
        fac.AntdSteps(
            steps=[
                {
                    'title': f'步骤{i + 1}的title',
                    'subTitle': f'步骤{i + 1}的subTitle',
                    'description': f'步骤{i + 1}的description',
                }
                for i in range(3)
            ],
            size='small',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 垂直步骤条

- 说明：从上往下垂直展示步骤条信息。

#### 代码
```python
fac.AntdSteps(
    steps=[
        {
            'title': f'步骤{i + 1}的title',
            'subTitle': f'步骤{i + 1}的subTitle',
            'description': f'步骤{i + 1}的description',
        }
        for i in range(3)
    ],
    direction='vertical',
)
```

### 垂直展示步骤条信息

- 说明：通过参数`labelPlacement`可控制步骤条额外信息的展示形式。

#### 代码
```python
fac.AntdSteps(
    steps=[
        {
            'title': f'步骤{i + 1}的title',
            'subTitle': f'步骤{i + 1}的subTitle',
            'description': f'步骤{i + 1}的description',
        }
        for i in range(3)
    ],
    labelPlacement='vertical',
)
```

### 带说明信息的步骤条

- 说明：步骤条节点可额外设置副标题及描述信息。

#### 代码
```python
fac.AntdSteps(
    steps=[
        {
            'title': f'步骤{i + 1}的title',
            'subTitle': f'步骤{i + 1}的subTitle',
            'description': f'步骤{i + 1}的description',
        }
        for i in range(3)
    ]
)
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- allowClick (boolean; default False):
    Whether the step can be switched by clicking. Default value: `False`.

- aria-* (string; optional):
    Wildcard for `aria-*` formatted attributes.

- className (string | dict; optional):
    The current component's CSS class name, supports [dynamic CSS class names](/advanced-classname).

- current (number; default 0):
    The current step number. Default value: `0`.

- data-* (string; optional):
    Wildcard for `data-*` formatted attributes.

- direction (a value equal to: 'horizontal', 'vertical'; default 'horizontal'):
    The display direction of the step bar, options include `'horizontal'`, `'vertical'`. Default value: `'horizontal'`.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the component.

- labelPlacement (a value equal to: 'horizontal', 'vertical'; optional):
    The display direction of the label content, options include `'horizontal'`, `'vertical'`.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- percent (number; optional):
    The current step progress, the value should be between 0 and 100, suitable for a regular step bar.

- progressDot (boolean; default False):
    Whether to render as a dotted step bar. Default value: `False`.

- responsive (boolean; default True):
    Whether to automatically force vertical display when the page width is less than 532px. Default value: `True`.

- size (a value equal to: 'default', 'small'; default 'default'):
    The size specification of the step bar, options include `'default'`, `'small'`. Default value: `'default'`.

- status (a value equal to: 'wait', 'process', 'finish', 'error'; default 'process'):
    The status of the step bar, options include `'wait'`, `'process'`, `'finish'`, `'error'`.
    Default value: `'process'`.

- steps (list of dicts; required):
    Required, defines the data structure of the step content.

    `steps` is a list of dictionaries with keys:

    - description (a list of or a singular dash component, string or number; optional):
        The description content of the step.

    - disabled (boolean; optional):
        Whether the current step is disabled.

    - icon (a list of or a singular dash component, string or number; optional):
        Custom icon for the step.

    - status (a value equal to: 'wait', 'process', 'finish', 'error'; optional):
        Force the status of the current step, same as the status parameter.

    - subTitle (a list of or a singular dash component, string or number; optional):
        The sub-title of the step.

    - title (a list of or a singular dash component, string or number; required):
        The title of the step.

- style (dict; optional):
    The current component's CSS styles.

- type (a value equal to: 'default', 'navigation', 'inline'; default 'default'):
    The type of the step bar, options include `'default'`, `'navigation'`, `'inline'`. Default value: `'default'`.
