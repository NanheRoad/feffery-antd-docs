# AntdCalendar

## 简介源码：`views/AntdCalendar/intro.py`
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
                {'title': translator.t('数据录入')},
                {'title': translator.t('AntdCalendar 日历')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCalendar 日历'), level=2),
        fac.AntdParagraph(translator.t('用于渲染可交互的日历。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 回调监听

- 说明：用于监听日历的点击事件。

#### 代码
```python
[
    fac.AntdSpace(
        [
            fac.AntdCalendar(
                id='calendar-demo',
                defaultValue='2024-01-01',
                style={'width': '300px'},
            ),
            fac.AntdParagraph(id='calendar-demo-output'),
        ]
    ),
    fac.AntdSpace(
        [
            fac.AntdCalendar(
                id='calendar-format-demo',
                defaultValue='2024年01月01日',
                format='YYYY年MM月DD日',
                style={'width': '300px'},
            ),
            fac.AntdParagraph(id='calendar-format-demo-output'),
        ]
    ),
]

...

@app.callback(
    Output('calendar-demo-output', 'children'),
    Input('calendar-demo', 'value')
)
def calendar_demo(value):

    return f'value: {value}'


@app.callback(
    Output('calendar-format-demo-output', 'children'),
    Input('calendar-format-demo', 'value')
)
def calendar_format_demo(value):

    return f'value: {value}'
```

### 基础使用

- 说明：最基础的日历。

#### 代码
```python
fac.AntdCalendar()
```

### 不同的尺寸规格

- 说明：设置参数`size`调整日历的尺寸规格。

#### 代码
```python
fac.AntdCalendar(size='large')
```

### 监听日期单元格点击事件

- 说明：通过监听属性`cellClickEvent`变化来获取日期单元格的点击事件。

#### 代码
```python
[
    fac.AntdCalendar(
        id='calendar-cell-click-event-demo',
    ),
    html.Pre(id='calendar-cell-click-event-demo-output'),
]

...

@app.callback(
    Output('calendar-cell-click-event-demo-output', 'children'),
    Input('calendar-cell-click-event-demo', 'cellClickEvent'),
    prevent_initial_call=True,
)
def calendar_cell_click_event_demo(cellClickEvent):
    return json.dumps(cellClickEvent, indent=4, ensure_ascii=False)
```

### 自定义单元格内容

- 说明：通过参数`customCells`为指定模式下的指定日期单元格添加自定义内容，未填写条件的部分将视作通配规则。

#### 代码
```python
fac.AntdCalendar(
    size='large',
    customCells=[
        {
            'type': 'date',
            'month': 8,
            'date': 1,
            'content': fac.AntdTag(content='建军节', color='red'),
        },
        {
            'type': 'date',
            'month': 8,
            'date': 7,
            'content': fac.AntdTag(content='立秋', color='gold'),
        },
        {
            'type': 'date',
            'month': 8,
            'date': 12,
            'content': fac.AntdSpace(
                ['0.3.0发布', '🎉🎉🎉'],
                direction='vertical',
                align='center',
                size=0,
                style={'width': '100%', 'fontSize': 16},
            ),
        },
        {
            'type': 'date',
            'month': 8,
            'date': 22,
            'content': fac.AntdTag(content='处暑', color='volcano'),
        },
        {
            'type': 'month',
            'month': 7,
            'content': fac.AntdTag(content='暑假', color='volcano'),
        },
        {
            'type': 'month',
            'month': 8,
            'content': fac.AntdTag(content='暑假', color='volcano'),
        },
        {
            'type': 'date',
            'date': 6,
            'content': fac.AntdTag(content='每月6号', color='red'),
        },
    ],
    value='2024-08-12',
)
```

## API 参数说明

- id (string; optional):
    The unique id of the component.

- aria-* (string; optional):
    Wildcard for attributes in the `aria-*` format.

- cellClickEvent (dict; optional):
    Listen for the click event on the date cell.

    `cellClickEvent` is a dictionary with keys:

    - timestamp (number; optional):
        The timestamp of the event.

    - type (string; optional):
        The type of the panel being recorded.

- className (string | dict; optional):
    The current component's CSS class name, supports [dynamic CSS](/advanced-classname).

- customCells (list of dicts; optional):
    Custom display content for the corresponding month and date.

    `customCells` is a list of dictionaries with keys:

    - content (a list of or a singular dash component, string or number; optional):
        Custom content.

    - date (number; optional):
        The date value that the current item matches.

    - month (number; optional):
        The month value that the current item matches.

    - type (a value equal to: 'month', 'date'; required):
        Required, the type corresponding to the current item, options include `'month'`, `'date'`.

    - year (number; optional):
        The year value that the current item matches.

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- defaultValue (string; optional):
    The initial selected date value.

- format (string; default 'YYYY-MM-DD'):
    The format for displaying dates, [reference material](https://day.js.org/docs/en/display/format) 
    Default value: `'YYYY-MM-DD'`.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the component.

- loading_state (dict; optional)

    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de'; default 'zh-cn'):
    The language of the component's text, options include `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German)
    Default value: `'zh-cn'`.

- name (string; optional):
    Used in conjunction with the `AntdForm` form batch value collection/control feature, serving as the field name for the current form item, with `id` as the default value.

- persisted_props (list of a value equal to: 'value's; default ['value']):
    The names of several properties that enable attribute persistence, with the option of `'value'`. Default value: `['value']`.

- persistence (boolean | string | number; optional):
    Whether to enable [property persistence](/prop-persistence).

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    The storage type for property persistence, options include `'local'` (local persistence), `'session'` (session persistence), `'memory'` (memory persistence)
    Default value: `'local'`.

- size (a value equal to: 'default', 'large'; default 'default'):
    The calendar size specification, options include `'default'`, `'large'`. Default value: `'default'`.

- style (dict; optional):
    The current component's CSS styles.

- value (string; optional):
    Listen for or set the current selected date value.
