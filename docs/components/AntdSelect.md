# AntdSelect

## 简介源码：`views/AntdSelect/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {"title": translator.t("组件介绍")},
                {"title": translator.t("数据录入")},
                {"title": translator.t("AntdSelect 下拉选择")},
            ],
            style={"marginBottom": 8},
        ),
        fac.AntdTitle(translator.t("AntdSelect 下拉选择"), level=2),
        fac.AntdParagraph(translator.t("用于为用户提供一组选项进行选择。")),
    ]

```

## 示例源码（demos）

### `views/AntdSelect/demos/addon.py`
```python
import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, State

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("基础示例", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 6)],
                    dropdownBefore=fac.AntdInput(placeholder="输入关键字搜索"),
                    dropdownAfter=fac.AntdButton(type="primary", children="新增选项"),
                    style={"width": "100%"},
                ),
                fac.AntdDivider("添加选项示例", innerTextOrientation="left"),
                fac.AntdSelect(
                    id="select-add-option-demo",
                    options=[f"选项{i}" for i in range(1, 6)],
                    dropdownAfter=fac.AntdInput(
                        id="select-add-option-input-demo",
                        placeholder="输入新增选项",
                        suffix=fac.AntdButton(
                            id="select-add-option-button-demo",
                            icon=fac.AntdIcon(icon="antd-plus"),
                            type="primary",
                        ),
                    ),
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("Basic example", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    dropdownBefore=fac.AntdInput(placeholder="Type keywords to search"),
                    dropdownAfter=fac.AntdButton(type="primary", children="Add option"),
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider("Add option example", innerTextOrientation="left"),
                fac.AntdSelect(
                    id="select-add-option-demo",
                    options=[f"Option {i}" for i in range(1, 6)],
                    dropdownAfter=fac.AntdInput(
                        id="select-add-option-input-demo",
                        placeholder="Enter a new option",
                        suffix=fac.AntdButton(
                            id="select-add-option-button-demo",
                            icon=fac.AntdIcon(icon="antd-plus"),
                            type="primary",
                        ),
                    ),
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


# 新增选项回调
@app.callback(
    [
        Output("select-add-option-demo", "options"),
        Output("select-add-option-input-demo", "value"),
    ],
    Input("select-add-option-button-demo", "nClicks"),
    [
        State("select-add-option-input-demo", "value"),
        State("select-add-option-demo", "options"),
    ],
    prevent_initial_call=True,
)
def add_option(nClicks, value, options):
    if nClicks and value:
        # 需注意，options写法如果是简写，应向列表追加 string|number 类型，非简写则应按options格式追加dict
        options.append(value)
        return options, None
    return dash.no_update


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('基础示例', innerTextOrientation='left'),
        fac.AntdSelect(
            options=[f'选项{i}' for i in range(1, 6)],
            dropdownBefore=fac.AntdInput(placeholder='输入关键字搜索'),
            dropdownAfter=fac.AntdButton(
                type='primary', children='新增选项'
            ),
            style={'width': '100%'},
        ),
        fac.AntdDivider('添加选项示例', innerTextOrientation='left'),
        fac.AntdSelect(
            id='select-add-option-demo',
            options=[f'选项{i}' for i in range(1, 6)],
            dropdownAfter=fac.AntdInput(
                id='select-add-option-input-demo',
                placeholder='输入新增选项',
                suffix=fac.AntdButton(
                    id='select-add-option-button-demo',
                    icon=fac.AntdIcon(icon='antd-plus'),
                    type='primary',
                ),
            ),
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
...
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('Basic example', innerTextOrientation='left'),
        fac.AntdSelect(
            options=[f'Option {i}' for i in range(1, 6)],
            dropdownBefore=fac.AntdInput(placeholder='Type keywords to search'),
            dropdownAfter=fac.AntdButton(
                type='primary', children='Add option'
            ),
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdDivider('Add option example', innerTextOrientation='left'),
        fac.AntdSelect(
            id='select-add-option-demo',
            options=[f'Option {i}' for i in range(1, 6)],
            dropdownAfter=fac.AntdInput(
                id='select-add-option-input-demo',
                placeholder='Enter a new option',
                suffix=fac.AntdButton(
                    id='select-add-option-button-demo',
                    icon=fac.AntdIcon(icon='antd-plus'),
                    type='primary',
                ),
            ),
            style={'width': '100%'},
            locale="en-us",
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
...
"""
            }
        ]

```

### `views/AntdSelect/demos/allow_clear.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider(
                    "allowClear=True（默认值）", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    placeholder='mode="default"（默认）',
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    allowClear=True,
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    placeholder='mode="multiple"',
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    allowClear=True,
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    placeholder='mode="tags"',
                    mode="tags",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=["选项1", "自由新增选项"],
                    allowClear=True,
                    style={"width": "100%"},
                ),
                fac.AntdDivider("allowClear=False", innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder='mode="default"（默认）',
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    allowClear=False,
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    placeholder='mode="multiple"',
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    allowClear=False,
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    placeholder='mode="tags"',
                    mode="tags",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=["选项1", "自由新增选项"],
                    allowClear=False,
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider(
                    "allowClear=True (default)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    placeholder='mode="default" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    allowClear=True,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    placeholder='mode="multiple"',
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    allowClear=True,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    placeholder='mode="tags"',
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=["Option 1", "Newly added option"],
                    allowClear=True,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider("allowClear=False", innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder='mode="default" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    allowClear=False,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    placeholder='mode="multiple"',
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    allowClear=False,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    placeholder='mode="tags"',
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=["Option 1", "Newly added option"],
                    allowClear=False,
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('allowClear=True（默认值）', innerTextOrientation='left'),
        fac.AntdSelect(
            placeholder='mode="default"（默认）',
            options=[f'选项{i}' for i in range(1, 6)],
            value='选项1',
            allowClear=True,
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            placeholder='mode="multiple"',
            mode='multiple',
            options=[f'选项{i}' for i in range(1, 6)],
            value=[f'选项{i}' for i in range(1, 3)],
            allowClear=True,
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            placeholder='mode="tags"',
            mode='tags',
            options=[f'选项{i}' for i in range(1, 6)],
            value=['选项1', '自由新增选项'],
            allowClear=True,
            style={'width': '100%'},
        ),
        fac.AntdDivider('allowClear=False', innerTextOrientation='left'),
        fac.AntdSelect(
            placeholder='mode="default"（默认）',
            options=[f'选项{i}' for i in range(1, 6)],
            value='选项1',
            allowClear=False,
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            placeholder='mode="multiple"',
            mode='multiple',
            options=[f'选项{i}' for i in range(1, 6)],
            value=[f'选项{i}' for i in range(1, 3)],
            allowClear=False,
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            placeholder='mode="tags"',
            mode='tags',
            options=[f'选项{i}' for i in range(1, 6)],
            value=['选项1', '自由新增选项'],
            allowClear=False,
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('allowClear=True (default)', innerTextOrientation='left'),
        fac.AntdSelect(
            placeholder='mode="default" (default)',
            options=[f'Option {i}' for i in range(1, 6)],
            value='Option 1',
            allowClear=True,
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdSelect(
            placeholder='mode="multiple"',
            mode='multiple',
            options=[f'Option {i}' for i in range(1, 6)],
            value=[f'Option {i}' for i in range(1, 3)],
            allowClear=True,
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdSelect(
            placeholder='mode="tags"',
            mode='tags',
            options=[f'Option {i}' for i in range(1, 6)],
            value=['Option 1', 'Newly added option'],
            allowClear=True,
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdDivider('allowClear=False', innerTextOrientation='left'),
        fac.AntdSelect(
            placeholder='mode="default" (default)',
            options=[f'Option {i}' for i in range(1, 6)],
            value='Option 1',
            allowClear=False,
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdSelect(
            placeholder='mode="multiple"',
            mode='multiple',
            options=[f'Option {i}' for i in range(1, 6)],
            value=[f'Option {i}' for i in range(1, 3)],
            allowClear=False,
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdSelect(
            placeholder='mode="tags"',
            mode='tags',
            options=[f'Option {i}' for i in range(1, 6)],
            value=['Option 1', 'Newly added option'],
            allowClear=False,
            style={'width': '100%'},
            locale="en-us",
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]

```

### `views/AntdSelect/demos/auto_clear_search_value.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider(
                    "autoClearSearchValue=True", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    placeholder="输入内容以搜索选项",
                    mode="multiple",
                    autoClearSearchValue=True,
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    placeholder="输入内容以搜索选项",
                    mode="tags",
                    autoClearSearchValue=True,
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdDivider(
                    "autoClearSearchValue=False", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    placeholder="输入内容以搜索选项",
                    mode="multiple",
                    autoClearSearchValue=False,
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    placeholder="输入内容以搜索选项",
                    mode="tags",
                    autoClearSearchValue=False,
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider(
                    "autoClearSearchValue=True", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    placeholder="Type to search options",
                    mode="multiple",
                    autoClearSearchValue=True,
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    placeholder="Type to search options",
                    mode="tags",
                    autoClearSearchValue=True,
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "autoClearSearchValue=False", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    placeholder="Type to search options",
                    mode="multiple",
                    autoClearSearchValue=False,
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    placeholder="Type to search options",
                    mode="tags",
                    autoClearSearchValue=False,
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('autoClearSearchValue=True', innerTextOrientation='left'),
        fac.AntdSelect(
            placeholder='输入内容以搜索选项',
            mode='multiple',
            autoClearSearchValue=True,
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            placeholder='输入内容以搜索选项',
            mode='tags',
            autoClearSearchValue=True,
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdDivider('autoClearSearchValue=False', innerTextOrientation='left'),
        fac.AntdSelect(
            placeholder='输入内容以搜索选项',
            mode='multiple',
            autoClearSearchValue=False,
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            placeholder='输入内容以搜索选项',
            mode='tags',
            autoClearSearchValue=False,
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('autoClearSearchValue=True', innerTextOrientation='left'),
        fac.AntdSelect(
            placeholder='Type to search options',
            mode='multiple',
            autoClearSearchValue=True,
            options=[f'Option {i}' for i in range(1, 6)],
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdSelect(
            placeholder='Type to search options',
            mode='tags',
            autoClearSearchValue=True,
            options=[f'Option {i}' for i in range(1, 6)],
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdDivider('autoClearSearchValue=False', innerTextOrientation='left'),
        fac.AntdSelect(
            placeholder='Type to search options',
            mode='multiple',
            autoClearSearchValue=False,
            options=[f'Option {i}' for i in range(1, 6)],
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdSelect(
            placeholder='Type to search options',
            mode='tags',
            autoClearSearchValue=False,
            options=[f'Option {i}' for i in range(1, 6)],
            style={'width': '100%'},
            locale="en-us",
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]

```

### `views/AntdSelect/demos/auto_spin.py`
```python
import time

import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider('基础使用', innerTextOrientation='left'),
                fac.AntdSelect(
                    id='select-auto-spin-remote-load-options',
                    placeholder='请输入要搜索的内容',
                    options=[],
                    autoSpin=True,
                    debounceWait=200,
                    style={'width': '100%'},
                ),
                fac.AntdDivider(
                    '自定义loading内容', innerTextOrientation='left'
                ),
                fac.AntdSelect(
                    id='select-auto-spin-remote-load-custom-empty-options',
                    placeholder='请输入要搜索的内容',
                    options=[],
                    autoSpin=True,
                    debounceWait=200,
                    loadingEmptyContent=fac.AntdCenter(
                        fac.AntdIcon(icon='antd-loading')
                    ),
                    style={'width': '100%'},
                ),
            ],
            direction='vertical',
            style={'width': 350},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider('Basic usage', innerTextOrientation='left'),
                fac.AntdSelect(
                    id='select-auto-spin-remote-load-options',
                    placeholder='Type to search',
                    options=[],
                    autoSpin=True,
                    debounceWait=200,
                    style={'width': '100%'},
                    locale='en-us',
                ),
                fac.AntdDivider(
                    'Custom loading content', innerTextOrientation='left'
                ),
                fac.AntdSelect(
                    id='select-auto-spin-remote-load-custom-empty-options',
                    placeholder='Type to search',
                    options=[],
                    autoSpin=True,
                    debounceWait=200,
                    loadingEmptyContent=fac.AntdCenter(
                        fac.AntdIcon(icon='antd-loading')
                    ),
                    style={'width': '100%'},
                    locale='en-us',
                ),
            ],
            direction='vertical',
            style={'width': 350},
        )

    return demo_contents


@app.callback(
    Output('select-auto-spin-remote-load-custom-empty-options', 'options'),
    Input(
        'select-auto-spin-remote-load-custom-empty-options',
        'debounceSearchValue',
    ),
)
def select_auto_spin_remote_load_options_demo(debounceSearchValue):
    if debounceSearchValue:
        time.sleep(1)
        return [
            {
                'label': f'{debounceSearchValue}模拟选项{i}',
                'value': f'{debounceSearchValue}模拟选项{i}',
            }
            for i in range(1, 6)
        ]
    return []


@app.callback(
    Output('select-auto-spin-remote-load-options', 'options'),
    Input('select-auto-spin-remote-load-options', 'debounceSearchValue'),
)
def select_auto_spin_remote_load_options_custom_content_demo(
    debounceSearchValue,
):
    if debounceSearchValue:
        time.sleep(1)
        return [
            {
                'label': f'{debounceSearchValue}模拟选项{i}',
                'value': f'{debounceSearchValue}模拟选项{i}',
            }
            for i in range(1, 6)
        ]
    return []


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()
    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdDivider("基础使用", innerTextOrientation="left"),
        fac.AntdSelect(
            id="select-auto-spin-remote-load-options",
            placeholder="请输入要搜索的内容",
            options=[],
            autoSpin=True,
            debounceWait=200,
            style={"width": "100%"},
        ),
        fac.AntdDivider("自定义loading内容", innerTextOrientation="left"),
        fac.AntdSelect(
            id="select-auto-spin-remote-load-custom-empty-options",
            placeholder="请输入要搜索的内容",
            options=[],
            autoSpin=True,
            debounceWait=200,
            loadingEmptyContent=fac.AntdCenter(
                fac.AntdIcon(icon="antd-loading")
            ),
            style={"width": "100%"},
        ),
    ],
    direction="vertical",
    style={"width": 350},
)

...

@app.callback(
    Output("select-auto-spin-remote-load-custom-empty-options", "options"),
    Input("select-auto-spin-remote-load-custom-empty-options", "debounceSearchValue"),
)
def select_auto_spin_remote_load_options_demo(debounceSearchValue):
    if debounceSearchValue:
        time.sleep(1)
        return [
            {
                "label": f"{debounceSearchValue}模拟选项{i}",
                "value": f"{debounceSearchValue}模拟选项{i}",
            }
            for i in range(1, 6)
        ]
    return []


@app.callback(
    Output("select-auto-spin-remote-load-options", "options"),
    Input("select-auto-spin-remote-load-options", "debounceSearchValue"),
)
def select_auto_spin_remote_load_options_custom_content_demo(debounceSearchValue):
    if debounceSearchValue:
        time.sleep(1)
        return [
            {
                "label": f"{debounceSearchValue}模拟选项{i}",
                "value": f"{debounceSearchValue}模拟选项{i}",
            }
            for i in range(1, 6)
        ]
    return []
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdDivider("Basic usage", innerTextOrientation="left"),
        fac.AntdSelect(
            id="select-auto-spin-remote-load-options",
            placeholder="Type to search",
            options=[],
            autoSpin=True,
            debounceWait=200,
            style={"width": "100%"},
            locale="en-us",
        ),
        fac.AntdDivider("Custom loading content", innerTextOrientation="left"),
        fac.AntdSelect(
            id="select-auto-spin-remote-load-custom-empty-options",
            placeholder="Type to search",
            options=[],
            autoSpin=True,
            debounceWait=200,
            loadingEmptyContent=fac.AntdCenter(
                fac.AntdIcon(icon="antd-loading")
            ),
            style={"width": "100%"},
            locale="en-us",
        ),
    ],
    direction="vertical",
    style={"width": 350},
)

...

@app.callback(
    Output("select-auto-spin-remote-load-custom-empty-options", "options"),
    Input("select-auto-spin-remote-load-custom-empty-options", "debounceSearchValue"),
)
def select_auto_spin_remote_load_options_demo(debounceSearchValue):
    if debounceSearchValue:
        time.sleep(1)
        return [
            {
                "label": f"{debounceSearchValue}模拟选项{i}",
                "value": f"{debounceSearchValue}模拟选项{i}",
            }
            for i in range(1, 6)
        ]
    return []


@app.callback(
    Output("select-auto-spin-remote-load-options", "options"),
    Input("select-auto-spin-remote-load-options", "debounceSearchValue"),
)
def select_auto_spin_remote_load_options_custom_content_demo(debounceSearchValue):
    if debounceSearchValue:
        time.sleep(1)
        return [
            {
                "label": f"{debounceSearchValue}模拟选项{i}",
                "value": f"{debounceSearchValue}模拟选项{i}",
            }
            for i in range(1, 6)
        ]
    return []
"""
            }
        ]

```

### `views/AntdSelect/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        demo_contents = [
            fac.AntdSelect(
                id="select-basic-callbacks-demo",
                options=[f"选项{i}" for i in range(1, 6)],
                style={"width": 350},
            ),
            fac.AntdParagraph(id="select-basic-callbacks-output"),
        ]
    elif current_locale == "en-us":
        demo_contents = [
            fac.AntdSelect(
                id="select-basic-callbacks-demo",
                options=[f"Option {i}" for i in range(1, 6)],
                style={"width": 350},
                locale="en-us",
            ),
            fac.AntdParagraph(id="select-basic-callbacks-output"),
        ]
    return demo_contents


@app.callback(
    Output("select-basic-callbacks-output", "children"),
    Input("select-basic-callbacks-demo", "value"),
)
def _show_value(value):
    return f"value: {value}"


def code_string() -> list:
    """返回当前语种对应的演示代码"""
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
[
    fac.AntdSelect(
        id='select-basic-callbacks-demo',
        options=[f'选项{i}' for i in range(1, 6)],
        style={'width': 350},
    ),
    fac.AntdParagraph(id='select-basic-callbacks-output'),
]
...
@app.callback(
    Output('select-basic-callbacks-output', 'children'),
    Input('select-basic-callbacks-demo', 'value'),
)
def _show_value(value):
    return f'value: {value}'
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
[
    fac.AntdSelect(
        id='select-basic-callbacks-demo',
        options=[f'Option {i}' for i in range(1, 6)],
        style={'width': 350},
        locale="en-us",
    ),
    fac.AntdParagraph(id='select-basic-callbacks-output'),
]
...
@app.callback(
    Output('select-basic-callbacks-output', 'children'),
    Input('select-basic-callbacks-demo', 'value'),
)
def _show_value(value):
    return f'value: {value}'
"""
            }
        ]

```

### `views/AntdSelect/demos/basic_search.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    placeholder="输入内容以搜索选项",
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    placeholder="Type to search options",
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSelect(
            placeholder='输入内容以搜索选项',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSelect(
            placeholder='Type to search options',
            options=[f'Option {i}' for i in range(1, 6)],
            style={'width': '100%'},
            locale="en-us",
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]

```

### `views/AntdSelect/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            options=[{"label": f"选项{i}", "value": f"选项{i}"} for i in range(1, 6)],
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            options=[
                {"label": f"Option {i}", "value": f"Option {i}"} for i in range(1, 6)
            ],
            style={"width": 350},
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[
        {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(1, 6)
    ],
    style={'width': 350},
)
"""
            }
        ]

    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[
        {'label': f'Option {i}', 'value': f'Option {i}'} for i in range(1, 6)
    ],
    style={'width': 350},
    locale="en-us",
)
"""
            }
        ]

```

### `views/AntdSelect/demos/border.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    bordered=True,
                    placeholder="bordered=True（默认）",
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    bordered=False,
                    placeholder="bordered=False",
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    bordered=True,
                    placeholder="bordered=True (default)",
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    bordered=False,
                    placeholder="bordered=False",
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSelect(
            bordered=True,
            placeholder='bordered=True（默认）',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            bordered=False,
            placeholder='bordered=False',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSelect(
            bordered=True,
            placeholder='bordered=True (default)',
            options=[f'Option {i}' for i in range(1, 6)],
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdSelect(
            bordered=False,
            placeholder='bordered=False',
            options=[f'Option {i}' for i in range(1, 6)],
            style={'width': '100%'},
            locale="en-us",
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]

```

### `views/AntdSelect/demos/color_select.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("连续型色带", innerTextOrientation="left"),
                fac.AntdSelect(
                    defaultValue="色系1",
                    options=[
                        {
                            "label": "色系1",
                            "value": "色系1",
                            "colors": ["#fff5f5", "#ff8787", "#c92a2a"],
                        },
                        {
                            "label": "色系2",
                            "value": "色系2",
                            "colors": ["#f8f0fc", "#da77f2", "#862e9c"],
                        },
                        {
                            "label": "色系3",
                            "value": "色系3",
                            "colors": ["#e7f5ff", "#4dabf7", "#1864ab"],
                        },
                    ],
                    colorsMode="sequential",
                    style={"width": "100%"},
                ),
                fac.AntdDivider("离散型色带", innerTextOrientation="left"),
                fac.AntdSelect(
                    defaultValue="色系1",
                    options=[
                        {
                            "label": "色系1",
                            "value": "色系1",
                            "colors": ["#fff5f5", "#ff8787", "#c92a2a"],
                        },
                        {
                            "label": "色系2",
                            "value": "色系2",
                            "colors": ["#f8f0fc", "#da77f2", "#862e9c"],
                        },
                        {
                            "label": "色系3",
                            "value": "色系3",
                            "colors": ["#e7f5ff", "#4dabf7", "#1864ab"],
                        },
                    ],
                    colorsMode="diverging",
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("Sequential colormap", innerTextOrientation="left"),
                fac.AntdSelect(
                    defaultValue="Palette 1",
                    options=[
                        {
                            "label": "Palette 1",
                            "value": "Palette 1",
                            "colors": ["#fff5f5", "#ff8787", "#c92a2a"],
                        },
                        {
                            "label": "Palette 2",
                            "value": "Palette 2",
                            "colors": ["#f8f0fc", "#da77f2", "#862e9c"],
                        },
                        {
                            "label": "Palette 3",
                            "value": "Palette 3",
                            "colors": ["#e7f5ff", "#4dabf7", "#1864ab"],
                        },
                    ],
                    colorsMode="sequential",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider("Diverging colormap", innerTextOrientation="left"),
                fac.AntdSelect(
                    defaultValue="Palette 1",
                    options=[
                        {
                            "label": "Palette 1",
                            "value": "Palette 1",
                            "colors": ["#fff5f5", "#ff8787", "#c92a2a"],
                        },
                        {
                            "label": "Palette 2",
                            "value": "Palette 2",
                            "colors": ["#f8f0fc", "#da77f2", "#862e9c"],
                        },
                        {
                            "label": "Palette 3",
                            "value": "Palette 3",
                            "colors": ["#e7f5ff", "#4dabf7", "#1864ab"],
                        },
                    ],
                    colorsMode="diverging",
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('连续型色带', innerTextOrientation='left'),
        fac.AntdSelect(
            defaultValue='色系1',
            options=[
                {'label': '色系1','value': '色系1','colors': ['#fff5f5','#ff8787','#c92a2a']},
                {'label': '色系2','value': '色系2','colors': ['#f8f0fc','#da77f2','#862e9c']},
                {'label': '色系3','value': '色系3','colors': ['#e7f5ff','#4dabf7','#1864ab']},
            ],
            colorsMode='sequential',
            style={'width': '100%'},
        ),
        fac.AntdDivider('离散型色带', innerTextOrientation='left'),
        fac.AntdSelect(
            defaultValue='色系1',
            options=[
                {'label': '色系1','value': '色系1','colors': ['#fff5f5','#ff8787','#c92a2a']},
                {'label': '色系2','value': '色系2','colors': ['#f8f0fc','#da77f2','#862e9c']},
                {'label': '色系3','value': '色系3','colors': ['#e7f5ff','#4dabf7','#1864ab']},
            ],
            colorsMode='diverging',
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('Sequential colormap', innerTextOrientation='left'),
        fac.AntdSelect(
            defaultValue='Palette 1',
            options=[
                {'label': 'Palette 1','value': 'Palette 1','colors': ['#fff5f5','#ff8787','#c92a2a']},
                {'label': 'Palette 2','value': 'Palette 2','colors': ['#f8f0fc','#da77f2','#862e9c']},
                {'label': 'Palette 3','value': 'Palette 3','colors': ['#e7f5ff','#4dabf7','#1864ab']},
            ],
            colorsMode='sequential',
            style={'width': '100%'},
            locale="en-us",
        ),
        fac.AntdDivider('Diverging colormap', innerTextOrientation='left'),
        fac.AntdSelect(
            defaultValue='Palette 1',
            options=[
                {'label': 'Palette 1','value': 'Palette 1','colors': ['#fff5f5','#ff8787','#c92a2a']},
                {'label': 'Palette 2','value': 'Palette 2','colors': ['#f8f0fc','#da77f2','#862e9c']},
                {'label': 'Palette 3','value': 'Palette 3','colors': ['#e7f5ff','#4dabf7','#1864ab']},
            ],
            colorsMode='diverging',
            style={'width': '100%'},
            locale="en-us",
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]

```

### `views/AntdSelect/demos/debounce_search_callbacks.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdText("当前debounceWait(单位：ms)："),
                        fac.AntdInputNumber(
                            id="select-debounce-wait-demo",
                            value=500,
                            min=0,
                            precision=0,
                        ),
                    ],
                    style={"justify-content": "space-between", "width": "100%"},
                ),
                fac.AntdSelect(
                    id="select-debounce-demo",
                    placeholder="请搜索内容",
                    placement="topLeft",
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdCard(
                    [
                        html.Div(id="select-not-debounce-demo-output"),
                        html.Div(id="select-debounce-demo-output"),
                    ],
                    styles={
                        "header": {"display": "none"},
                        "body": {"flexDirection": "column"},
                    },
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdText("Current debounceWait (ms):"),
                        fac.AntdInputNumber(
                            id="select-debounce-wait-demo",
                            value=500,
                            min=0,
                            precision=0,
                        ),
                    ],
                    style={"justify-content": "space-between", "width": "100%"},
                ),
                fac.AntdSelect(
                    id="select-debounce-demo",
                    placeholder="Please search",
                    placement="topLeft",
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdCard(
                    [
                        html.Div(id="select-not-debounce-demo-output"),
                        html.Div(id="select-debounce-demo-output"),
                    ],
                    styles={
                        "header": {"display": "none"},
                        "body": {"flexDirection": "column"},
                    },
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


# 通过AntdInputNumber回调设定select的debounceWait数值
@app.callback(
    Output("select-debounce-demo", "debounceWait"),
    Input("select-debounce-wait-demo", "value"),
)
def set_debounce_wait(value):
    return value


@app.callback(
    Output("select-not-debounce-demo-output", "children"),
    Input("select-debounce-demo", "searchValue"),
)
def select_demo(searchValue):
    return f"searchValue: {searchValue}"


@app.callback(
    Output("select-debounce-demo-output", "children"),
    Input("select-debounce-demo", "debounceSearchValue"),
)
def select_debounce_demo(debounceSearchValue):
    return f"debounceSearchValue: {debounceSearchValue}"


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdText('当前debounceWait(单位：ms)：'),
                fac.AntdInputNumber(
                    id='select-debounce-wait-demo',
                    value=500,
                    min=0,
                    precision=0,
                ),
            ],
            style={
                'justify-content': 'space-between',
                'width': '100%',
            },
        ),
        fac.AntdSelect(
            id='select-debounce-demo',
            placeholder='请搜索内容',
            placement='topLeft',
            options=[f'选项{i}' for i in range(1, 6)],
            style={
                'width': '100%',
            },
        ),
        fac.AntdCard(
            [
                html.Div(id='select-not-debounce-demo-output'),
                html.Div(id='select-debounce-demo-output'),
            ],
            styles={
                'header': {'display': 'none'},
                'body': {'flexDirection': 'column'},
            },
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
...
@app.callback(
    Output('select-debounce-demo', 'debounceWait'),
    Input('select-debounce-wait-demo', 'value'),
)
def set_debounce_wait(value):
    return value
...
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdText('Current debounceWait (ms):'),
                fac.AntdInputNumber(
                    id='select-debounce-wait-demo',
                    value=500,
                    min=0,
                    precision=0,
                ),
            ],
            style={
                'justify-content': 'space-between',
                'width': '100%',
            },
        ),
        fac.AntdSelect(
            id='select-debounce-demo',
            placeholder='Please search',
            placement='topLeft',
            options=[f'Option {i}' for i in range(1, 6)],
            style={
                'width': '100%',
            },
            locale="en-us",
        ),
        fac.AntdCard(
            [
                html.Div(id='select-not-debounce-demo-output'),
                html.Div(id='select-debounce-demo-output'),
            ],
            styles={
                'header': {'display': 'none'},
                'body': {'flexDirection': 'column'},
            },
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
...
@app.callback(
    Output('select-debounce-demo', 'debounceWait'),
    Input('select-debounce-wait-demo', 'value'),
)
def set_debounce_wait(value):
    return value
...
"""
            }
        ]

```

### `views/AntdSelect/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    disabled=True,
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    disabled=True,
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    disabled=True,
                    mode="tags",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=["选项1", "自由新增选项"],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    disabled=True,
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    disabled=True,
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    disabled=True,
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=["Option 1", "Newly added option"],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdSelect(
                    disabled=True,
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    disabled=True,
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    disabled=True,
                    mode="tags",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=["选项1", "自由新增选项"],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdSelect(
                    disabled=True,
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    disabled=True,
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    disabled=True,
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=["Option 1", "Newly added option"],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]

```

### `views/AntdSelect/demos/disabled_options.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("常规用法", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[
                        {
                            "label": f"选项{i}",
                            "value": f"选项{i}",
                            "disabled": True if i == 3 else False,
                        }
                        for i in range(1, 6)
                    ],
                    style={"width": "100%"},
                ),
                fac.AntdDivider("自定义label用法", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[
                        {
                            "label": fac.AntdFlex(
                                [
                                    fac.AntdFlex(
                                        [
                                            fac.AntdAvatar(
                                                text=f"{i}", mode="text", size="small"
                                            ),
                                            fac.AntdTag(
                                                content=f"选项{i}",
                                                color=[
                                                    "blue",
                                                    "green",
                                                    "purple",
                                                    "orange",
                                                    "cyan",
                                                ][i - 1],
                                            ),
                                        ],
                                        justify="flex-start",
                                        align="center",
                                        gap=5,
                                    ),
                                    (
                                        fac.AntdIcon(
                                            icon="antd-stop", style={"color": "gray"}
                                        )
                                        if i == 3
                                        else None
                                    ),
                                ],
                                justify="space-between",
                                align="center",
                                gap=5,
                            ),
                            "value": f"选项{i}",
                            "disabled": True if i == 3 else False,
                        }
                        for i in range(1, 6)
                    ],
                    size="large",
                    style={"width": 350},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("Basic usage", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[
                        {
                            "label": f"Option {i}",
                            "value": f"Option {i}",
                            "disabled": True if i == 3 else False,
                        }
                        for i in range(1, 6)
                    ],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider("Custom label usage", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[
                        {
                            "label": fac.AntdFlex(
                                [
                                    fac.AntdFlex(
                                        [
                                            fac.AntdAvatar(
                                                text=f"{i}", mode="text", size="small"
                                            ),
                                            fac.AntdTag(
                                                content=f"Option {i}",
                                                color=[
                                                    "blue",
                                                    "green",
                                                    "purple",
                                                    "orange",
                                                    "cyan",
                                                ][i - 1],
                                            ),
                                        ],
                                        justify="flex-start",
                                        align="center",
                                        gap=5,
                                    ),
                                    (
                                        fac.AntdIcon(
                                            icon="antd-stop", style={"color": "gray"}
                                        )
                                        if i == 3
                                        else None
                                    ),
                                ],
                                justify="space-between",
                                align="center",
                                gap=5,
                            ),
                            "value": f"Option {i}",
                            "disabled": True if i == 3 else False,
                        }
                        for i in range(1, 6)
                    ],
                    size="large",
                    style={"width": 350},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('常规用法', innerTextOrientation='left'),
        fac.AntdSelect(
            options=[
                {
                    'label': f'选项{i}',
                    'value': f'选项{i}',
                    'disabled': True if i == 3 else False,
                }
                for i in range(1, 6)
            ],
            style={'width': '100%'},
        ),
        fac.AntdDivider('自定义label用法', innerTextOrientation='left'),
        fac.AntdSelect(
            options=[
                {
                    'label': fac.AntdFlex(
                        [
                            fac.AntdFlex(
                                [
                                    fac.AntdAvatar(
                                        text=f'{i}',
                                        mode='text',
                                        size='small',
                                    ),
                                    fac.AntdTag(
                                        content=f'选项{i}',
                                        color=[
                                            'blue',
                                            'green',
                                            'purple',
                                            'orange',
                                            'cyan',
                                        ][i - 1],
                                    ),
                                ],
                                justify='flex-start',
                                align='center',
                                gap=5,
                            ),
                            # 可通过额外的元素来展示disabled的视觉效果
                            fac.AntdIcon(
                                icon='antd-stop',
                                style={
                                    'color': 'gray',
                                },
                            )
                            if i == 3
                            else None,
                        ],
                        justify='space-between',
                        align='center',
                        gap=5,
                    ),
                    'value': f'选项{i}',
                    'disabled': True if i == 3 else False,
                }
                for i in range(1, 6)
            ],
            size='large',
            style={'width': 350},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdDivider("Basic usage", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[
                        {
                            "label": f"Option {i}",
                            "value": f"Option {i}",
                            "disabled": True if i == 3 else False,
                        }
                        for i in range(1, 6)
                    ],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider("Custom label usage", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[
                        {
                            "label": fac.AntdFlex(
                                [
                                    fac.AntdFlex(
                                        [
                                            fac.AntdAvatar(
                                                text=f"{i}", mode="text", size="small"
                                            ),
                                            fac.AntdTag(
                                                content=f"Option {i}",
                                                color=[
                                                    "blue",
                                                    "green",
                                                    "purple",
                                                    "orange",
                                                    "cyan",
                                                ][i - 1],
                                            ),
                                        ],
                                        justify="flex-start",
                                        align="center",
                                        gap=5,
                                    ),
                                    (
                                        fac.AntdIcon(
                                            icon="antd-stop", style={"color": "gray"}
                                        )
                                        if i == 3
                                        else None
                                    ),
                                ],
                                justify="space-between",
                                align="center",
                                gap=5,
                            ),
                            "value": f"Option {i}",
                            "disabled": True if i == 3 else False,
                        }
                        for i in range(1, 6)
                    ],
                    size="large",
                    style={"width": 350},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]

```

### `views/AntdSelect/demos/empty_content.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            emptyContent=fac.AntdResult(status="warning", subTitle="暂无可选项"),
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            emptyContent=fac.AntdResult(
                status="warning", subTitle="No options available"
            ),
            style={"width": 350},
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSelect(
    emptyContent=fac.AntdResult(
        status='warning',
        subTitle='暂无可选项',
    ),
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSelect(
    emptyContent=fac.AntdResult(
        status='warning',
        subTitle='No options available',
    ),
    style={'width': 350},
    locale="en-us",
)
"""
            }
        ]

```

### `views/AntdSelect/demos/group.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            options=[
                {
                    "group": "分组1",
                    "options": [
                        {"label": f"选项1-{i}", "value": f"选项1-{i}"}
                        for i in range(1, 4)
                    ],
                },
                {
                    "group": "分组2",
                    "options": [
                        {"label": f"选项2-{i}", "value": f"选项2-{i}"}
                        for i in range(1, 4)
                    ],
                },
            ],
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            options=[
                {
                    "group": "Group 1",
                    "options": [
                        {"label": f"Option 1-{i}", "value": f"Option 1-{i}"}
                        for i in range(1, 4)
                    ],
                },
                {
                    "group": "Group 2",
                    "options": [
                        {"label": f"Option 2-{i}", "value": f"Option 2-{i}"}
                        for i in range(1, 4)
                    ],
                },
            ],
            style={"width": 350},
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSelect(
            options=[
                {
                    "group": "分组1",
                    "options": [
                        {"label": f"选项1-{i}", "value": f"选项1-{i}"}
                        for i in range(1, 4)
                    ],
                },
                {
                    "group": "分组2",
                    "options": [
                        {"label": f"选项2-{i}", "value": f"选项2-{i}"}
                        for i in range(1, 4)
                    ],
                },
            ],
            style={"width": 350},
        )
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSelect(
            options=[
                {
                    "group": "Group 1",
                    "options": [
                        {"label": f"Option 1-{i}", "value": f"Option 1-{i}"}
                        for i in range(1, 4)
                    ],
                },
                {
                    "group": "Group 2",
                    "options": [
                        {"label": f"Option 2-{i}", "value": f"Option 2-{i}"}
                        for i in range(1, 4)
                    ],
                },
            ],
            style={"width": 350},
            locale="en-us",
        )
"""
            }
        ]

```

### `views/AntdSelect/demos/list_height.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    placeholder="listHeight=400",
                    options=[f"选项{i}" for i in range(1, 26)],
                    listHeight=400,
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    placeholder="listHeight=100",
                    options=[f"选项{i}" for i in range(1, 26)],
                    listHeight=100,
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    placeholder="listHeight=400",
                    options=[f"Option {i}" for i in range(1, 26)],
                    listHeight=400,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    placeholder="listHeight=100",
                    options=[f"Option {i}" for i in range(1, 26)],
                    listHeight=100,
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdSelect(
                    placeholder="listHeight=400",
                    options=[f"选项{i}" for i in range(1, 26)],
                    listHeight=400,
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    placeholder="listHeight=100",
                    options=[f"选项{i}" for i in range(1, 26)],
                    listHeight=100,
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdSelect(
                    placeholder="listHeight=400",
                    options=[f"Option {i}" for i in range(1, 26)],
                    listHeight=400,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    placeholder="listHeight=100",
                    options=[f"Option {i}" for i in range(1, 26)],
                    listHeight=100,
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]

```

### `views/AntdSelect/demos/max_count.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            options=[f"选项{i}" for i in range(1, 6)],
            mode="multiple",
            maxCount=2,
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            options=[f"Option {i}" for i in range(1, 6)],
            mode="multiple",
            maxCount=2,
            style={"width": 350},
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'选项{i}' for i in range(1, 6)],
    mode='multiple',
    maxCount=2,
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'Option {i}' for i in range(1, 6)],
    mode='multiple',
    maxCount=2,
    style={'width': 350},
    locale="en-us",
)
"""
            }
        ]

```

### `views/AntdSelect/demos/max_tag_count.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("maxTagCount=5（默认）", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 26)],
                    mode="multiple",
                    value=[f"选项{i}" for i in range(1, 8)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 26)],
                    mode="tags",
                    value=[
                        "选项1",
                        "选项2",
                        "选项3",
                        "选项4",
                        "自由设置的较长选项",
                        "选项5",
                        "选项6",
                    ],
                    style={"width": "100%"},
                ),
                fac.AntdDivider("maxTagCount=3", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 26)],
                    mode="multiple",
                    maxTagCount=3,
                    value=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 26)],
                    mode="tags",
                    maxTagCount=3,
                    value=["选项1", "选项2", "自由设置的较长选项", "选项5", "选项6"],
                    style={"width": "100%"},
                ),
                fac.AntdDivider(
                    'maxTagCount="responsive"', innerTextOrientation="left"
                ),
                fac.AntdText("选择框宽度："),
                fac.AntdRadioGroup(
                    id="select-width-radio-group-demo",
                    options=[f"{i}00px" for i in range(1, 5)],
                    defaultValue="300px",
                    optionType="button",
                    buttonStyle="solid",
                ),
                fac.AntdSelect(
                    options=[f"{i}" for i in range(1, 26)],
                    id="select-multiple-responsive-demo",
                    mode="multiple",
                    value=[f"{i}" for i in range(1, 11)],
                    maxTagCount="responsive",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    options=[f"{i}" for i in range(1, 26)],
                    id="select-tags-responsive-demo",
                    mode="tags",
                    value=["自由设置的较长选项"] + [f"{i}" for i in range(1, 11)],
                    maxTagCount="responsive",
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("maxTagCount=5 (default)", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 26)],
                    mode="multiple",
                    value=[f"Option {i}" for i in range(1, 8)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 26)],
                    mode="tags",
                    value=[
                        "Option 1",
                        "Option 2",
                        "Option 3",
                        "Option 4",
                        "A longer custom option",
                        "Option 5",
                        "Option 6",
                    ],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider("maxTagCount=3", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 26)],
                    mode="multiple",
                    maxTagCount=3,
                    value=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 26)],
                    mode="tags",
                    maxTagCount=3,
                    value=[
                        "Option 1",
                        "Option 2",
                        "A longer custom option",
                        "Option 5",
                        "Option 6",
                    ],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    'maxTagCount="responsive"', innerTextOrientation="left"
                ),
                fac.AntdText("Select width:"),
                fac.AntdRadioGroup(
                    id="select-width-radio-group-demo",
                    options=[f"{i}00px" for i in range(1, 5)],
                    defaultValue="300px",
                    optionType="button",
                    buttonStyle="solid",
                ),
                fac.AntdSelect(
                    options=[f"{i}" for i in range(1, 26)],
                    id="select-multiple-responsive-demo",
                    mode="multiple",
                    value=[f"{i}" for i in range(1, 11)],
                    maxTagCount="responsive",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    options=[f"{i}" for i in range(1, 26)],
                    id="select-tags-responsive-demo",
                    mode="tags",
                    value=["A longer custom option"] + [f"{i}" for i in range(1, 11)],
                    maxTagCount="responsive",
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


@app.callback(
    [
        Output("select-multiple-responsive-demo", "style"),
        Output("select-tags-responsive-demo", "style"),
    ],
    Input("select-width-radio-group-demo", "value"),
    prevent_initial_call=True,
)
def select_width_radio_group_callback(value):
    return {"width": value}, {"width": value}


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdDivider("maxTagCount=5（默认）", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 26)],
                    mode="multiple",
                    value=[f"选项{i}" for i in range(1, 8)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 26)],
                    mode="tags",
                    value=[
                        "选项1",
                        "选项2",
                        "选项3",
                        "选项4",
                        "自由设置的较长选项",
                        "选项5",
                        "选项6",
                    ],
                    style={"width": "100%"},
                ),
                fac.AntdDivider("maxTagCount=3", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 26)],
                    mode="multiple",
                    maxTagCount=3,
                    value=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 26)],
                    mode="tags",
                    maxTagCount=3,
                    value=["选项1", "选项2", "自由设置的较长选项", "选项5", "选项6"],
                    style={"width": "100%"},
                ),
                fac.AntdDivider(
                    'maxTagCount="responsive"', innerTextOrientation="left"
                ),
                fac.AntdText("选择框宽度："),
                fac.AntdRadioGroup(
                    id="select-width-radio-group-demo",
                    options=[f"{i}00px" for i in range(1, 5)],
                    defaultValue="300px",
                    optionType="button",
                    buttonStyle="solid",
                ),
                fac.AntdSelect(
                    options=[f"{i}" for i in range(1, 26)],
                    id="select-multiple-responsive-demo",
                    mode="multiple",
                    value=[f"{i}" for i in range(1, 11)],
                    maxTagCount="responsive",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    options=[f"{i}" for i in range(1, 26)],
                    id="select-tags-responsive-demo",
                    mode="tags",
                    value=["自由设置的较长选项"] + [f"{i}" for i in range(1, 11)],
                    maxTagCount="responsive",
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdDivider("maxTagCount=5 (default)", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 26)],
                    mode="multiple",
                    value=[f"Option {i}" for i in range(1, 8)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 26)],
                    mode="tags",
                    value=[
                        "Option 1",
                        "Option 2",
                        "Option 3",
                        "Option 4",
                        "A longer custom option",
                        "Option 5",
                        "Option 6",
                    ],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider("maxTagCount=3", innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 26)],
                    mode="multiple",
                    maxTagCount=3,
                    value=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 26)],
                    mode="tags",
                    maxTagCount=3,
                    value=[
                        "Option 1",
                        "Option 2",
                        "A longer custom option",
                        "Option 5",
                        "Option 6",
                    ],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    'maxTagCount="responsive"', innerTextOrientation="left"
                ),
                fac.AntdText("Select width:"),
                fac.AntdRadioGroup(
                    id="select-width-radio-group-demo",
                    options=[f"{i}00px" for i in range(1, 5)],
                    defaultValue="300px",
                    optionType="button",
                    buttonStyle="solid",
                ),
                fac.AntdSelect(
                    options=[f"{i}" for i in range(1, 26)],
                    id="select-multiple-responsive-demo",
                    mode="multiple",
                    value=[f"{i}" for i in range(1, 11)],
                    maxTagCount="responsive",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    options=[f"{i}" for i in range(1, 26)],
                    id="select-tags-responsive-demo",
                    mode="tags",
                    value=["A longer custom option"] + [f"{i}" for i in range(1, 11)],
                    maxTagCount="responsive",
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]

```

### `views/AntdSelect/demos/multiple.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            options=[f"选项{i}" for i in range(1, 6)],
            mode="multiple",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            options=[f"Option {i}" for i in range(1, 6)],
            mode="multiple",
            style={"width": 350},
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'选项{i}' for i in range(1, 6)],
    mode='multiple',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'Option {i}' for i in range(1, 6)],
    mode='multiple',
    style={'width': 350},
    locale="en-us",
)
"""
            }
        ]

```

### `views/AntdSelect/demos/options_filter_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    current_locale = get_current_locale()

    letters = ["A", "a", "B", "b", "c", "D", "e"]

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("尝试搜索大小写字母", innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="case-insensitive",
                    optionFilterMode="case-insensitive",
                    options=[f"选项{i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                ),
                fac.AntdDivider("尝试搜索大小写字母", innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="case-sensitive",
                    optionFilterMode="case-sensitive",
                    options=[f"选项{i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                ),
                fac.AntdDivider(
                    "尝试搜索[a-z]、[a-z]|[A-Z]、[0-9]等", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    placeholder="regex",
                    optionFilterMode="regex",
                    options=[f"选项{i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider(
                    "Try searching uppercase/lowercase letters",
                    innerTextOrientation="left",
                ),
                fac.AntdSelect(
                    placeholder="case-insensitive",
                    optionFilterMode="case-insensitive",
                    options=[f"Option {i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "Try searching uppercase/lowercase letters",
                    innerTextOrientation="left",
                ),
                fac.AntdSelect(
                    placeholder="case-sensitive",
                    optionFilterMode="case-sensitive",
                    options=[f"Option {i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "Try searching [a-z], [a-z]|[A-Z], [0-9], etc.",
                    innerTextOrientation="left",
                ),
                fac.AntdSelect(
                    placeholder="regex",
                    optionFilterMode="regex",
                    options=[f"Option {i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdDivider("尝试搜索大小写字母", innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="case-insensitive",
                    optionFilterMode="case-insensitive",
                    options=[f"选项{i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                ),
                fac.AntdDivider("尝试搜索大小写字母", innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="case-sensitive",
                    optionFilterMode="case-sensitive",
                    options=[f"选项{i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                ),
                fac.AntdDivider(
                    "尝试搜索[a-z]、[a-z]|[A-Z]、[0-9]等", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    placeholder="regex",
                    optionFilterMode="regex",
                    options=[f"选项{i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdDivider(
                    "Try searching uppercase/lowercase letters",
                    innerTextOrientation="left",
                ),
                fac.AntdSelect(
                    placeholder="case-insensitive",
                    optionFilterMode="case-insensitive",
                    options=[f"Option {i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "Try searching uppercase/lowercase letters",
                    innerTextOrientation="left",
                ),
                fac.AntdSelect(
                    placeholder="case-sensitive",
                    optionFilterMode="case-sensitive",
                    options=[f"Option {i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "Try searching [a-z], [a-z]|[A-Z], [0-9], etc.",
                    innerTextOrientation="left",
                ),
                fac.AntdSelect(
                    placeholder="regex",
                    optionFilterMode="regex",
                    options=[f"Option {i}-{index}" for index, i in enumerate(letters)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]

```

### `views/AntdSelect/demos/options_filter_prop.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        fruits = [
            {"label": "香蕉", "value": "banana"},
            {"label": "苹果", "value": "apple"},
            {"label": "西瓜", "value": "watermelon"},
            {"label": "草莓", "value": "strawberry"},
            {"label": "葡萄", "value": "grape"},
        ]
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider('尝试搜索"香蕉"', innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="search label",
                    optionFilterProp="label",
                    options=fruits,
                    style={"width": "100%"},
                ),
                fac.AntdDivider('尝试搜索"banana"', innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="search value",
                    optionFilterProp="value",
                    options=fruits,
                    style={"width": "100%"},
                ),
                fac.AntdDivider(
                    '针对组件型label，只可搜索"value"', innerTextOrientation="left"
                ),
                fac.AntdText("针对组件型label，只可搜索value"),
                fac.AntdSelect(
                    placeholder="search value in component label options",
                    optionFilterProp="value",
                    options=[
                        {"label": fac.AntdText("香蕉", strong=True), "value": "banana"},
                        {"label": fac.AntdText("苹果", strong=True), "value": "apple"},
                        {
                            "label": fac.AntdText("西瓜", strong=True),
                            "value": "watermelon",
                        },
                        {
                            "label": fac.AntdText("草莓", strong=True),
                            "value": "strawberry",
                        },
                        {"label": fac.AntdText("葡萄", strong=True), "value": "grape"},
                    ],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        fruits_en = [
            {"label": "Banana", "value": "banana"},
            {"label": "Apple", "value": "apple"},
            {"label": "Watermelon", "value": "watermelon"},
            {"label": "Strawberry", "value": "strawberry"},
            {"label": "Grape", "value": "grape"},
        ]
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider('Try searching "banana"', innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="Search label",
                    optionFilterProp="label",
                    options=fruits_en,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider('Try searching "banana"', innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="Search value",
                    optionFilterProp="value",
                    options=fruits_en,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    'For component labels, only "value" is searchable',
                    innerTextOrientation="left",
                ),
                fac.AntdText("For component labels, only value is searchable"),
                fac.AntdSelect(
                    placeholder="Search value in component label options",
                    optionFilterProp="value",
                    options=[
                        {
                            "label": fac.AntdText("Banana", strong=True),
                            "value": "banana",
                        },
                        {"label": fac.AntdText("Apple", strong=True), "value": "apple"},
                        {
                            "label": fac.AntdText("Watermelon", strong=True),
                            "value": "watermelon",
                        },
                        {
                            "label": fac.AntdText("Strawberry", strong=True),
                            "value": "strawberry",
                        },
                        {"label": fac.AntdText("Grape", strong=True), "value": "grape"},
                    ],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdDivider('尝试搜索"香蕉"', innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="search label",
                    optionFilterProp="label",
                    options=fruits,
                    style={"width": "100%"},
                ),
                fac.AntdDivider('尝试搜索"banana"', innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="search value",
                    optionFilterProp="value",
                    options=fruits,
                    style={"width": "100%"},
                ),
                fac.AntdDivider(
                    '针对组件型label，只可搜索"value"', innerTextOrientation="left"
                ),
                fac.AntdText("针对组件型label，只可搜索value"),
                fac.AntdSelect(
                    placeholder="search value in component label options",
                    optionFilterProp="value",
                    options=[
                        {"label": fac.AntdText("香蕉", strong=True), "value": "banana"},
                        {"label": fac.AntdText("苹果", strong=True), "value": "apple"},
                        {
                            "label": fac.AntdText("西瓜", strong=True),
                            "value": "watermelon",
                        },
                        {
                            "label": fac.AntdText("草莓", strong=True),
                            "value": "strawberry",
                        },
                        {"label": fac.AntdText("葡萄", strong=True), "value": "grape"},
                    ],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
            [
                fac.AntdDivider('Try searching "banana"', innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="Search label",
                    optionFilterProp="label",
                    options=fruits_en,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider('Try searching "banana"', innerTextOrientation="left"),
                fac.AntdSelect(
                    placeholder="Search value",
                    optionFilterProp="value",
                    options=fruits_en,
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    'For component labels, only "value" is searchable',
                    innerTextOrientation="left",
                ),
                fac.AntdText("For component labels, only value is searchable"),
                fac.AntdSelect(
                    placeholder="Search value in component label options",
                    optionFilterProp="value",
                    options=[
                        {
                            "label": fac.AntdText("Banana", strong=True),
                            "value": "banana",
                        },
                        {"label": fac.AntdText("Apple", strong=True), "value": "apple"},
                        {
                            "label": fac.AntdText("Watermelon", strong=True),
                            "value": "watermelon",
                        },
                        {
                            "label": fac.AntdText("Strawberry", strong=True),
                            "value": "strawberry",
                        },
                        {"label": fac.AntdText("Grape", strong=True), "value": "grape"},
                    ],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
"""
            }
        ]

```

### `views/AntdSelect/demos/options_label.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            options=[
                {
                    "label": fac.AntdFlex(
                        [
                            fac.AntdAvatar(text=f"{i}", mode="text", size="small"),
                            fac.AntdTag(
                                content=f"选项{i}",
                                color=["blue", "green", "purple", "orange", "cyan"][
                                    i - 1
                                ],
                            ),
                        ],
                        justify="flex-start",
                        align="center",
                        gap=5,
                    ),
                    "value": f"选项{i}",
                }
                for i in range(1, 6)
            ],
            size="large",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            options=[
                {
                    "label": fac.AntdFlex(
                        [
                            fac.AntdAvatar(text=f"{i}", mode="text", size="small"),
                            fac.AntdTag(
                                content=f"Option {i}",
                                color=["blue", "green", "purple", "orange", "cyan"][
                                    i - 1
                                ],
                            ),
                        ],
                        justify="flex-start",
                        align="center",
                        gap=5,
                    ),
                    "value": f"Option {i}",
                }
                for i in range(1, 6)
            ],
            size="large",
            style={"width": 350},
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """fac.AntdSelect(
            options=[
                {
                    "label": fac.AntdFlex(
                        [
                            fac.AntdAvatar(text=f"{i}", mode="text", size="small"),
                            fac.AntdTag(
                                content=f"选项{i}",
                                color=["blue", "green", "purple", "orange", "cyan"][
                                    i - 1
                                ],
                            ),
                        ],
                        justify="flex-start",
                        align="center",
                        gap=5,
                    ),
                    "value": f"选项{i}",
                }
                for i in range(1, 6)
            ],
            size="large",
            style={"width": 350},
        )"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSelect(
            options=[
                {
                    "label": fac.AntdFlex(
                        [
                            fac.AntdAvatar(text=f"{i}", mode="text", size="small"),
                            fac.AntdTag(
                                content=f"Option {i}",
                                color=["blue", "green", "purple", "orange", "cyan"][
                                    i - 1
                                ],
                            ),
                        ],
                        justify="flex-start",
                        align="center",
                        gap=5,
                    ),
                    "value": f"Option {i}",
                }
                for i in range(1, 6)
            ],
            size="large",
            style={"width": 350},
            locale="en-us",
        )"""
            }
        ]

```

### `views/AntdSelect/demos/options_share.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    id="select-options-share-1-demo",
                    placeholder="选择选项后查看其他下拉选择框的options",
                    options=[{"label": f"选项{i}", "value": i} for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    id="select-options-share-2-demo",
                    placeholder="选择选项后查看其他下拉选择框的options",
                    options=[{"label": f"选项{i}", "value": i} for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    id="select-options-share-3-demo",
                    placeholder="选择选项后查看其他下拉选择框的options",
                    options=[{"label": f"选项{i}", "value": i} for i in range(1, 6)],
                    mode="multiple",
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    id="select-options-share-1-demo",
                    placeholder="After selecting, check options of the other selects",
                    options=[{"label": f"Option {i}", "value": i} for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    id="select-options-share-2-demo",
                    placeholder="After selecting, check options of the other selects",
                    options=[{"label": f"Option {i}", "value": i} for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    id="select-options-share-3-demo",
                    placeholder="After selecting, check options of the other selects",
                    options=[{"label": f"Option {i}", "value": i} for i in range(1, 6)],
                    mode="multiple",
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


@app.callback(
    [
        Output("select-options-share-1-demo", "options"),
        Output("select-options-share-2-demo", "options"),
        Output("select-options-share-3-demo", "options"),
    ],
    [
        Input("select-options-share-1-demo", "value"),
        Input("select-options-share-2-demo", "value"),
        Input("select-options-share-3-demo", "value"),
    ],
)
def share_options(value1, value2, value3):
    if not value3:
        value3 = []
    options_1 = [
        {
            "label": f"选项{i}",
            "value": i,
            "disabled": True if i in [value2] + value3 else False,
        }
        for i in range(1, 6)
    ]
    options_2 = [
        {
            "label": f"选项{i}",
            "value": i,
            "disabled": True if i in [value1] + value3 else False,
        }
        for i in range(1, 6)
    ]
    options_3 = [
        {
            "label": f"选项{i}",
            "value": i,
            "disabled": True if i in [value2, value1] else False,
        }
        for i in range(1, 6)
    ]
    return options_1, options_2, options_3


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """fac.AntdSpace(
    [
        fac.AntdSelect(
            id='select-options-share-1-demo',
            placeholder='选择选项后查看其他下拉选择框的options',
            options=[
                {'label': f'选项{i}', 'value': i} for i in range(1, 6)
            ],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            id='select-options-share-2-demo',
            placeholder='选择选项后查看其他下拉选择框的options',
            options=[
                {'label': f'选项{i}', 'value': i} for i in range(1, 6)
            ],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            id='select-options-share-3-demo',
            placeholder='选择选项后查看其他下拉选择框的options',
            options=[
                {'label': f'选项{i}', 'value': i} for i in range(1, 6)
            ],
            mode='multiple',
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)

    
@app.callback(
    [
        Output('select-options-share-1-demo', 'options'),
        Output('select-options-share-2-demo', 'options'),
        Output('select-options-share-3-demo', 'options'),
    ],
    [
        Input('select-options-share-1-demo', 'value'),
        Input('select-options-share-2-demo', 'value'),
        Input('select-options-share-3-demo', 'value'),
    ],
)
def share_options(value1, value2, value3):
    # 避免value3 is None的情况
    if not value3:
        value3 = []
    options_1 = [
        {
            'label': f'选项{i}',
            'value': i,
            'disabled': True if i in [value2] + value3 else False,
        }
        for i in range(1, 6)
    ]
    options_2 = [
        {
            'label': f'选项{i}',
            'value': i,
            'disabled': True if i in [value1] + value3 else False,
        }
        for i in range(1, 6)
    ]
    options_3 = [
        {
            'label': f'选项{i}',
            'value': i,
            'disabled': True if i in [value2, value1] else False,
        }
        for i in range(1, 6)
    ]
    return options_1, options_2, options_3"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdSelect(
                    id="select-options-share-1-demo",
                    placeholder="After selecting, check options of the other selects",
                    options=[{"label": f"Option {i}", "value": i} for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    id="select-options-share-2-demo",
                    placeholder="After selecting, check options of the other selects",
                    options=[{"label": f"Option {i}", "value": i} for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    id="select-options-share-3-demo",
                    placeholder="After selecting, check options of the other selects",
                    options=[{"label": f"Option {i}", "value": i} for i in range(1, 6)],
                    mode="multiple",
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
        
        @app.callback(
    [
        Output("select-options-share-1-demo", "options"),
        Output("select-options-share-2-demo", "options"),
        Output("select-options-share-3-demo", "options"),
    ],
    [
        Input("select-options-share-1-demo", "value"),
        Input("select-options-share-2-demo", "value"),
        Input("select-options-share-3-demo", "value"),
    ],
)
def share_options(value1, value2, value3):
    if not value3:
        value3 = []
    options_1 = [
        {
            "label": f"选项{i}",
            "value": i,
            "disabled": True if i in [value2] + value3 else False,
        }
        for i in range(1, 6)
    ]
    options_2 = [
        {
            "label": f"选项{i}",
            "value": i,
            "disabled": True if i in [value1] + value3 else False,
        }
        for i in range(1, 6)
    ]
    options_3 = [
        {
            "label": f"选项{i}",
            "value": i,
            "disabled": True if i in [value2, value1] else False,
        }
        for i in range(1, 6)
    ]
    return options_1, options_2, options_3"""
            }
        ]

```

### `views/AntdSelect/demos/placement.py`
```python
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash import html
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = html.Div(
            [
                fuc.FefferyStyle(
                    rawStyle=".popup-custom-style {min-width: 100px!important;}"
                ),
                fac.AntdSpace(
                    [
                        fac.AntdSelect(
                            options=[f"选项{i}" for i in range(1, 6)],
                            placeholder=f'placement="{placement}"',
                            placement=placement,
                            popupMatchSelectWidth=False,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                        )
                        for placement in [
                            "bottomLeft",
                            "bottomRight",
                            "topLeft",
                            "topRight",
                        ]
                    ],
                    direction="vertical",
                    style={"width": 350},
                ),
            ]
        )

    elif current_locale == "en-us":
        demo_contents = html.Div(
            [
                fuc.FefferyStyle(
                    rawStyle=".popup-custom-style {min-width: 100px!important;}"
                ),
                fac.AntdSpace(
                    [
                        fac.AntdSelect(
                            options=[f"Option {i}" for i in range(1, 6)],
                            placeholder=f'placement="{placement}"',
                            placement=placement,
                            popupMatchSelectWidth=False,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                            locale="en-us",
                        )
                        for placement in [
                            "bottomLeft",
                            "bottomRight",
                            "topLeft",
                            "topRight",
                        ]
                    ],
                    direction="vertical",
                    style={"width": 350},
                ),
            ]
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """html.Div(
            [
                fuc.FefferyStyle(
                    rawStyle=".popup-custom-style {min-width: 100px!important;}"
                ),
                fac.AntdSpace(
                    [
                        fac.AntdSelect(
                            options=[f"选项{i}" for i in range(1, 6)],
                            placeholder=f'placement="{placement}"',
                            placement=placement,
                            popupMatchSelectWidth=False,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                        )
                        for placement in [
                            "bottomLeft",
                            "bottomRight",
                            "topLeft",
                            "topRight",
                        ]
                    ],
                    direction="vertical",
                    style={"width": 350},
                ),
            ]
        )"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """html.Div(
            [
                fuc.FefferyStyle(
                    rawStyle=".popup-custom-style {min-width: 100px!important;}"
                ),
                fac.AntdSpace(
                    [
                        fac.AntdSelect(
                            options=[f"Option {i}" for i in range(1, 6)],
                            placeholder=f'placement="{placement}"',
                            placement=placement,
                            popupMatchSelectWidth=False,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                            locale="en-us",
                        )
                        for placement in [
                            "bottomLeft",
                            "bottomRight",
                            "topLeft",
                            "topRight",
                        ]
                    ],
                    direction="vertical",
                    style={"width": 350},
                ),
            ]
        )"""
            }
        ]

```

### `views/AntdSelect/demos/popup_container.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 6)],
                    placeholder='popupContainer="body"',
                    popupContainer="body",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 6)],
                    placeholder='popupContainer="parent"',
                    popupContainer="parent",
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    placeholder='popupContainer="body"',
                    popupContainer="body",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    placeholder='popupContainer="parent"',
                    popupContainer="parent",
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 6)],
                    placeholder='popupContainer="body"',
                    popupContainer="body",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 6)],
                    placeholder='popupContainer="parent"',
                    popupContainer="parent",
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    placeholder='popupContainer="body"',
                    popupContainer="body",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    placeholder='popupContainer="parent"',
                    popupContainer="parent",
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )"""
            }
        ]

```

### `views/AntdSelect/demos/popup_match_select_width.py`
```python
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash import html
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = html.Div(
            [
                fuc.FefferyStyle(
                    rawStyle=".popup-custom-style {min-width: 100px!important;}"
                ),
                fac.AntdSpace(
                    [
                        fac.AntdSelect(
                            options=[f"选项{i}" for i in range(1, 26)],
                            placeholder="popupMatchSelectWidth=True",
                            popupMatchSelectWidth=True,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                        ),
                        fac.AntdSelect(
                            options=[f"选项{i}" for i in range(1, 26)],
                            placeholder="popupMatchSelectWidth=False",
                            popupMatchSelectWidth=False,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                        ),
                    ],
                    direction="vertical",
                    style={"width": 350, "marginBottom": 5},
                ),
                fac.AntdParagraph(
                    [
                        "可以看到，即使设置了自定义的下拉选择菜单宽度，在",
                        fac.AntdText("popupMatchSelectWidth=True", code=True),
                        "时，弹出框的宽度仍与选择框的宽度一致，只有在",
                        fac.AntdText("popupMatchSelectWidth=False", code=True),
                        "时，下拉选择菜单的自定义宽度才能生效。同时不再使用虚拟滚动。",
                    ]
                ),
            ]
        )

    elif current_locale == "en-us":
        demo_contents = html.Div(
            [
                fuc.FefferyStyle(
                    rawStyle=".popup-custom-style {min-width: 100px!important;}"
                ),
                fac.AntdSpace(
                    [
                        fac.AntdSelect(
                            options=[f"Option {i}" for i in range(1, 26)],
                            placeholder="popupMatchSelectWidth=True",
                            popupMatchSelectWidth=True,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                            locale="en-us",
                        ),
                        fac.AntdSelect(
                            options=[f"Option {i}" for i in range(1, 26)],
                            placeholder="popupMatchSelectWidth=False",
                            popupMatchSelectWidth=False,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                            locale="en-us",
                        ),
                    ],
                    direction="vertical",
                    style={"width": 350, "marginBottom": 5},
                ),
                fac.AntdParagraph(
                    [
                        "As you can see, even with a custom dropdown width, when ",
                        fac.AntdText("popupMatchSelectWidth=True", code=True),
                        " the popup matches the select width. Only when ",
                        fac.AntdText("popupMatchSelectWidth=False", code=True),
                        " does the custom width take effect, and virtual scrolling is disabled.",
                    ]
                ),
            ]
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """html.Div(
            [
                fuc.FefferyStyle(
                    rawStyle=".popup-custom-style {min-width: 100px!important;}"
                ),
                fac.AntdSpace(
                    [
                        fac.AntdSelect(
                            options=[f"选项{i}" for i in range(1, 26)],
                            placeholder="popupMatchSelectWidth=True",
                            popupMatchSelectWidth=True,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                        ),
                        fac.AntdSelect(
                            options=[f"选项{i}" for i in range(1, 26)],
                            placeholder="popupMatchSelectWidth=False",
                            popupMatchSelectWidth=False,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                        ),
                    ],
                    direction="vertical",
                    style={"width": 350, "marginBottom": 5},
                ),
                fac.AntdParagraph(
                    [
                        "可以看到，即使设置了自定义的下拉选择菜单宽度，在",
                        fac.AntdText("popupMatchSelectWidth=True", code=True),
                        "时，弹出框的宽度仍与选择框的宽度一致，只有在",
                        fac.AntdText("popupMatchSelectWidth=False", code=True),
                        "时，下拉选择菜单的自定义宽度才能生效。同时不再使用虚拟滚动。",
                    ]
                ),
            ]
        )"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """html.Div(
            [
                fuc.FefferyStyle(
                    rawStyle=".popup-custom-style {min-width: 100px!important;}"
                ),
                fac.AntdSpace(
                    [
                        fac.AntdSelect(
                            options=[f"Option {i}" for i in range(1, 26)],
                            placeholder="popupMatchSelectWidth=True",
                            popupMatchSelectWidth=True,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                            locale="en-us",
                        ),
                        fac.AntdSelect(
                            options=[f"Option {i}" for i in range(1, 26)],
                            placeholder="popupMatchSelectWidth=False",
                            popupMatchSelectWidth=False,
                            popupClassName="popup-custom-style",
                            style={"width": "100%"},
                            locale="en-us",
                        ),
                    ],
                    direction="vertical",
                    style={"width": 350, "marginBottom": 5},
                ),
                fac.AntdParagraph(
                    [
                        "As you can see, even with a custom dropdown width, when ",
                        fac.AntdText("popupMatchSelectWidth=True", code=True),
                        " the popup matches the select width. Only when ",
                        fac.AntdText("popupMatchSelectWidth=False", code=True),
                        " does the custom width take effect, and virtual scrolling is disabled.",
                    ]
                ),
            ]
        )"""
            }
        ]

```

### `views/AntdSelect/demos/prefix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            options=[f"选项{i}" for i in range(1, 6)],
            value="选项1",
            prefix=fac.AntdIcon(icon="antd-user"),
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            options=[f"Option {i}" for i in range(1, 6)],
            value="Option 1",
            prefix=fac.AntdIcon(icon="antd-user"),
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'选项{i}' for i in range(1, 6)],
    value='选项1',
    prefix=fac.AntdIcon(icon='antd-user'),
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'Option {i}' for i in range(1, 6)],
    value='Option 1',
    prefix=fac.AntdIcon(icon='antd-user'),
    locale="en-us",
)
"""
            }
        ]

```

### `views/AntdSelect/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    readOnly=True,
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    readOnly=True,
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    readOnly=True,
                    mode="tags",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=["选项1", "自由新增选项"],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    readOnly=True,
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    readOnly=True,
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    readOnly=True,
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=["Option 1", "Newly added option"],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdSelect(
                    readOnly=True,
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    readOnly=True,
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    readOnly=True,
                    mode="tags",
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=["选项1", "自由新增选项"],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdSelect(
                    readOnly=True,
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    readOnly=True,
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    readOnly=True,
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=["Option 1", "Newly added option"],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )"""
            }
        ]

```

### `views/AntdSelect/demos/search_value_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    id="select-search-value-demo",
                    placeholder="basic search",
                    options=[f"选项{i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    id="select-search-value-multiple-demo",
                    placeholder="multiple mode search",
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    id="select-search-value-auto-clear-false-demo",
                    placeholder="autoClearSearchValue=False",
                    mode="multiple",
                    autoClearSearchValue=False,
                    options=[f"选项{i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                ),
                fac.AntdCard(
                    id="select-search-value-demo-output",
                    styles={"header": {"display": "none"}},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSelect(
                    id="select-search-value-demo",
                    placeholder="basic search",
                    options=[f"Option {i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    id="select-search-value-multiple-demo",
                    placeholder="multiple mode search",
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    id="select-search-value-auto-clear-false-demo",
                    placeholder="autoClearSearchValue=False",
                    mode="multiple",
                    autoClearSearchValue=False,
                    options=[f"Option {i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdCard(
                    id="select-search-value-demo-output",
                    styles={"header": {"display": "none"}},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


@app.callback(
    Output("select-search-value-demo-output", "children"),
    [
        Input("select-search-value-demo", "searchValue"),
        Input("select-search-value-multiple-demo", "searchValue"),
        Input("select-search-value-auto-clear-false-demo", "searchValue"),
    ],
)
def select_search_value_demo(searchValue1, searchValue2, searchValue3):
    return fac.AntdSpace(
        [
            fac.AntdParagraph(f"searchValue：{searchValue1}", style={"margin": 0}),
            fac.AntdParagraph(
                f"multiple searchValue：{searchValue2}", style={"margin": 0}
            ),
            fac.AntdParagraph(
                f"autoClearSearchValue=False：{searchValue3}", style={"margin": 0}
            ),
        ],
        direction="vertical",
        size=5,
    )


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """fac.AntdSpace(
    [
        fac.AntdSelect(
            id='select-search-value-demo',
            placeholder='basic search',
            options=[f'选项{i}' for i in range(1, 6)],
            placement='topLeft',
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            id='select-search-value-multiple-demo',
            placeholder='multiple mode search',
            mode='multiple',
            options=[f'选项{i}' for i in range(1, 6)],
            placement='topLeft',
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            id='select-search-value-auto-clear-false-demo',
            placeholder='autoClearSearchValue=False',
            mode='multiple',
            autoClearSearchValue=False,
            options=[f'选项{i}' for i in range(1, 6)],
            placement='topLeft',
            style={'width': '100%'},
        ),
        fac.AntdCard(
            id='select-search-value-demo-output',
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)


@app.callback(
    Output('select-search-value-demo-output', 'children'),
    [
        Input('select-search-value-demo', 'searchValue'),
        Input('select-search-value-multiple-demo', 'searchValue'),
        Input('select-search-value-auto-clear-false-demo', 'searchValue'),
    ],
)
def select_search_value_demo(searchValue1, searchValue2, searchValue3):
    return fac.AntdSpace(
        [
            fac.AntdParagraph(
                f'searchValue：{searchValue1}', style={'margin': 0}
            ),
            fac.AntdParagraph(
                f'multiple searchValue：{searchValue2}', style={'margin': 0}
            ),
            fac.AntdParagraph(
                f'autoClearSearchValue=False：{searchValue3}',
                style={'margin': 0},
            ),
        ],
        direction='vertical',
        size=5,
    )"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdSelect(
                    id="select-search-value-demo",
                    placeholder="basic search",
                    options=[f"Option {i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    id="select-search-value-multiple-demo",
                    placeholder="multiple mode search",
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    id="select-search-value-auto-clear-false-demo",
                    placeholder="autoClearSearchValue=False",
                    mode="multiple",
                    autoClearSearchValue=False,
                    options=[f"Option {i}" for i in range(1, 6)],
                    placement="topLeft",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdCard(
                    id="select-search-value-demo-output",
                    styles={"header": {"display": "none"}},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )
        
        @app.callback(
    Output('select-search-value-demo-output', 'children'),
    [
        Input('select-search-value-demo', 'searchValue'),
        Input('select-search-value-multiple-demo', 'searchValue'),
        Input('select-search-value-auto-clear-false-demo', 'searchValue'),
    ],
)
def select_search_value_demo(searchValue1, searchValue2, searchValue3):
    return fac.AntdSpace(
        [
            fac.AntdParagraph(
                f'searchValue：{searchValue1}', style={'margin': 0}
            ),
            fac.AntdParagraph(
                f'multiple searchValue：{searchValue2}', style={'margin': 0}
            ),
            fac.AntdParagraph(
                f'autoClearSearchValue=False：{searchValue3}',
                style={'margin': 0},
            ),
        ],
        direction='vertical',
        size=5,
    )"""
            }
        ]

```

### `views/AntdSelect/demos/short_options.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, State

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdText("options_type："),
                        fac.AntdRadioGroup(
                            id="select-short-options-type-demo",
                            options=["list of string", "list of number"],
                            value="list of string",
                            optionType="button",
                            buttonStyle="solid",
                        ),
                    ]
                ),
                fac.AntdSelect(
                    id="select-short-options-demo",
                    options=[i for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdCard(
                    id="select-short-options-output-demo",
                    styles={"header": {"display": "none"}},
                ),
            ],
            direction="vertical",
            style={"width": 350, "gap": 5},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdText("options_type:"),
                        fac.AntdRadioGroup(
                            id="select-short-options-type-demo",
                            options=["list of string", "list of number"],
                            value="list of string",
                            optionType="button",
                            buttonStyle="solid",
                        ),
                    ]
                ),
                fac.AntdSelect(
                    id="select-short-options-demo",
                    options=[i for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdCard(
                    id="select-short-options-output-demo",
                    styles={"header": {"display": "none"}},
                ),
            ],
            direction="vertical",
            style={"width": 350, "gap": 5},
        )

    return demo_contents


@app.callback(
    [
        Output("select-short-options-demo", "options"),
        Output("select-short-options-demo", "value"),
    ],
    Input("select-short-options-type-demo", "value"),
)
def select_short_options_type_demo_callback(value):
    if value == "list of string":
        return [f"{i}" for i in range(1, 6)], "1"
    elif value == "list of number":
        return [i for i in range(1, 6)], 1


@app.callback(
    Output("select-short-options-output-demo", "children"),
    [
        Input("select-short-options-demo", "value"),
        State("select-short-options-demo", "options"),
    ],
)
def select_short_options_demo_callback(value, options):
    return fac.AntdSpace(
        [
            fac.AntdParagraph(f"options：{options}", style={"margin": 0}),
            fac.AntdParagraph(f"value：{value}", style={"margin": 0}),
            fac.AntdParagraph(f"value_type：{type(value)}", style={"margin": 0}),
        ],
        direction="vertical",
    )


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdText('options_type：'),
                fac.AntdRadioGroup(
                    id='select-short-options-type-demo',
                    options=[
                        'list of string',
                        'list of number',
                    ],
                    value='list of string',
                    optionType='button',
                    buttonStyle='solid',
                ),
            ]
        ),
        fac.AntdSelect(
            id='select-short-options-demo',
            options=[i for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdCard(
            id='select-short-options-output-demo',
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': 350, 'gap': 5},
)


# radioGroup回调设置select的options
@app.callback(
    [
        Output('select-short-options-demo', 'options'),
        Output('select-short-options-demo', 'value'),
    ],
    Input('select-short-options-type-demo', 'value'),
)
def select_short_options_type_demo_callback(value):
    if value == 'list of string':
        return [f'{i}' for i in range(1, 6)], '1'
    elif value == 'list of number':
        return [i for i in range(1, 6)], 1


# 回调数据展示
@app.callback(
    Output('select-short-options-output-demo', 'children'),
    [
        Input('select-short-options-demo', 'value'),
        State('select-short-options-demo', 'options'),
    ],
)
def select_short_options_demo_callback(value, options):
    return fac.AntdSpace(
        [
            fac.AntdParagraph(f'options：{options}', style={'margin': 0}),
            fac.AntdParagraph(f'value：{value}', style={'margin': 0}),
            fac.AntdParagraph(
                f'value_type：{type(value)}', style={'margin': 0}
            ),
        ],
        direction='vertical',
    )"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSpace(
                    [
                        fac.AntdText("options_type:"),
                        fac.AntdRadioGroup(
                            id="select-short-options-type-demo",
                            options=["list of string", "list of number"],
                            value="list of string",
                            optionType="button",
                            buttonStyle="solid",
                        ),
                    ]
                ),
                fac.AntdSelect(
                    id="select-short-options-demo",
                    options=[i for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdCard(
                    id="select-short-options-output-demo",
                    styles={"header": {"display": "none"}},
                ),
            ],
            direction="vertical",
            style={"width": 350, "gap": 5},
        )

        # radioGroup回调设置select的options
@app.callback(
    [
        Output('select-short-options-demo', 'options'),
        Output('select-short-options-demo', 'value'),
    ],
    Input('select-short-options-type-demo', 'value'),
)
def select_short_options_type_demo_callback(value):
    if value == 'list of string':
        return [f'{i}' for i in range(1, 6)], '1'
    elif value == 'list of number':
        return [i for i in range(1, 6)], 1


# 回调数据展示
@app.callback(
    Output('select-short-options-output-demo', 'children'),
    [
        Input('select-short-options-demo', 'value'),
        State('select-short-options-demo', 'options'),
    ],
)
def select_short_options_demo_callback(value, options):
    return fac.AntdSpace(
        [
            fac.AntdParagraph(f'options：{options}', style={'margin': 0}),
            fac.AntdParagraph(f'value：{value}', style={'margin': 0}),
            fac.AntdParagraph(
                f'value_type：{type(value)}', style={'margin': 0}
            ),
        ],
        direction='vertical',
    )
        """
            }
        ]

```

### `views/AntdSelect/demos/show_count.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdInput(mode="text-area", showCount=True, style={"width": 350}),
                fac.AntdInput(
                    mode="text-area",
                    maxLength=10,
                    showCount=True,
                    placeholder="设置maxLength后，字符数将显示上限",
                    style={"width": 350},
                ),
            ],
            direction="vertical",
            size="large",
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdInput(mode="text-area", showCount=True, style={"width": 350}),
                fac.AntdInput(
                    mode="text-area",
                    maxLength=10,
                    showCount=True,
                    placeholder="When maxLength is set, the counter shows the limit",
                    style={"width": 350},
                ),
            ],
            direction="vertical",
            size="large",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """fac.AntdSpace(
    [
        fac.AntdInput(
            mode='text-area',
            showCount=True,
            style={'width': 350},
        ),
        fac.AntdInput(
            mode='text-area',
            maxLength=10,
            showCount=True,
            placeholder='设置maxLength后，字符数将显示上限',
            style={'width': 350},
        ),
    ],
    direction='vertical',
    size='large',
)"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdInput(mode="text-area", showCount=True, style={"width": 350}),
                fac.AntdInput(
                    mode="text-area",
                    maxLength=10,
                    showCount=True,
                    placeholder="When maxLength is set, the counter shows the limit",
                    style={"width": 350},
                ),
            ],
            direction="vertical",
            size="large",
        )"""
            }
        ]

```

### `views/AntdSelect/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("默认模式不同尺寸示例", innerTextOrientation="left"),
                fac.AntdSelect(
                    size="small",
                    placeholder='size="small"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    size="middle",
                    placeholder='size="middle"（默认）',
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    size="large",
                    placeholder='size="large"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdDivider("多选模式不同尺寸示例", innerTextOrientation="left"),
                fac.AntdSelect(
                    size="small",
                    mode="multiple",
                    placeholder='size="small"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    size="middle",
                    mode="multiple",
                    placeholder='size="middle"（默认）',
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    size="large",
                    mode="multiple",
                    placeholder='size="large"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider(
                    "Size examples (single select)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    size="small",
                    placeholder='size="small"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    size="middle",
                    placeholder='size="middle" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    size="large",
                    placeholder='size="large"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "Size examples (multiple select)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    size="small",
                    mode="multiple",
                    placeholder='size="small"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    size="middle",
                    mode="multiple",
                    placeholder='size="middle" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    size="large",
                    mode="multiple",
                    placeholder='size="large"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """"fac.AntdSpace(
    [
        fac.AntdDivider(
            '默认模式不同尺寸示例', innerTextOrientation='left'
        ),
        fac.AntdSelect(
            size='small',
            placeholder='size="small"',
            options=[f'选项{i}' for i in range(1, 6)],
            value='选项1',
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            size='middle',
            placeholder='size="middle"（默认）',
            options=[f'选项{i}' for i in range(1, 6)],
            value='选项1',
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            size='large',
            placeholder='size="large"',
            options=[f'选项{i}' for i in range(1, 6)],
            value='选项1',
            style={'width': '100%'},
        ),
        fac.AntdDivider(
            '多选模式不同尺寸示例', innerTextOrientation='left'
        ),
        fac.AntdSelect(
            size='small',
            mode='multiple',
            placeholder='size="small"',
            options=[f'选项{i}' for i in range(1, 6)],
            value=[f'选项{i}' for i in range(1, 3)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            size='middle',
            mode='multiple',
            placeholder='size="middle"（默认）',
            options=[f'选项{i}' for i in range(1, 6)],
            value=[f'选项{i}' for i in range(1, 3)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            size='large',
            mode='multiple',
            placeholder='size="large"',
            options=[f'选项{i}' for i in range(1, 6)],
            value=[f'选项{i}' for i in range(1, 3)],
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdDivider(
                    "Size examples (single select)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    size="small",
                    placeholder='size="small"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    size="middle",
                    placeholder='size="middle" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    size="large",
                    placeholder='size="large"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "Size examples (multiple select)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    size="small",
                    mode="multiple",
                    placeholder='size="small"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    size="middle",
                    mode="multiple",
                    placeholder='size="middle" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    size="large",
                    mode="multiple",
                    placeholder='size="large"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )"""
            }
        ]

```

### `views/AntdSelect/demos/status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider('status="warning"', innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 6)],
                    status="warning",
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    status="warning",
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    mode="tags",
                    options=[f"选项{i}" for i in range(1, 6)],
                    status="warning",
                    value=["选项1", "自由新增选项"],
                    style={"width": "100%"},
                ),
                fac.AntdDivider('status="error"', innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"选项{i}" for i in range(1, 6)],
                    status="error",
                    value="选项1",
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    mode="multiple",
                    options=[f"选项{i}" for i in range(1, 6)],
                    status="error",
                    value=[f"选项{i}" for i in range(1, 3)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    mode="tags",
                    options=[f"选项{i}" for i in range(1, 6)],
                    status="error",
                    value=["选项1", "自由新增选项"],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider('status="warning"', innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="warning",
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="warning",
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="warning",
                    value=["Option 1", "Newly added option"],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider('status="error"', innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="error",
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="error",
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="error",
                    value=["Option 1", "Newly added option"],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """fac.AntdSpace(
    [
        fac.AntdDivider('status="warning"', innerTextOrientation='left'),
        fac.AntdSelect(
            options=[f'选项{i}' for i in range(1, 6)],
            status='warning',
            value='选项1',
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            mode='multiple',
            options=[f'选项{i}' for i in range(1, 6)],
            status='warning',
            value=[f'选项{i}' for i in range(1, 3)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            mode='tags',
            options=[f'选项{i}' for i in range(1, 6)],
            status='warning',
            value=['选项1', '自由新增选项'],
            style={'width': '100%'},
        ),
        fac.AntdDivider('status="error"', innerTextOrientation='left'),
        fac.AntdSelect(
            options=[f'选项{i}' for i in range(1, 6)],
            status='error',
            value='选项1',
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            mode='multiple',
            options=[f'选项{i}' for i in range(1, 6)],
            status='error',
            value=[f'选项{i}' for i in range(1, 3)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            mode='tags',
            options=[f'选项{i}' for i in range(1, 6)],
            status='error',
            value=['选项1', '自由新增选项'],
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """fac.AntdSpace(
            [
                fac.AntdDivider('status="warning"', innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="warning",
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="warning",
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="warning",
                    value=["Option 1", "Newly added option"],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider('status="error"', innerTextOrientation="left"),
                fac.AntdSelect(
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="error",
                    value="Option 1",
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    mode="multiple",
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="error",
                    value=[f"Option {i}" for i in range(1, 3)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    mode="tags",
                    options=[f"Option {i}" for i in range(1, 6)],
                    status="error",
                    value=["Option 1", "Newly added option"],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )"""
            }
        ]

```

### `views/AntdSelect/demos/suffix_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            options=[f"选项{i}" for i in range(1, 6)],
            value="选项1",
            suffixIcon=fac.AntdIcon(icon="antd-user"),
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            options=[f"Option {i}" for i in range(1, 6)],
            value="Option 1",
            suffixIcon=fac.AntdIcon(icon="antd-user"),
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'选项{i}' for i in range(1, 6)],
    value='选项1',
    suffixIcon=fac.AntdIcon(icon='antd-user'),
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'Option {i}' for i in range(1, 6)],
    value='Option 1',
    suffixIcon=fac.AntdIcon(icon='antd-user'),
    locale="en-us",
)
"""
            }
        ]

```

### `views/AntdSelect/demos/tags.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSelect(
            options=[f"选项{i}" for i in range(1, 6)],
            mode="tags",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSelect(
            options=[f"Option {i}" for i in range(1, 6)],
            mode="tags",
            style={"width": 350},
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'选项{i}' for i in range(1, 6)],
    mode='tags',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSelect(
    options=[f'Option {i}' for i in range(1, 6)],
    mode='tags',
    style={'width': 350},
    locale="en-us",
)
"""
            }
        ]

```

### `views/AntdSelect/demos/variant.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider("默认模式不同变体示例", innerTextOrientation="left"),
                fac.AntdSelect(
                    variant="outlined",
                    placeholder='variant="outlined"（默认）',
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    variant="filled",
                    placeholder='variant="filled"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    variant="underlined",
                    placeholder='variant="underlined"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    variant="borderless",
                    placeholder='variant="borderless"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdDivider("多选模式不同变体示例", innerTextOrientation="left"),
                fac.AntdSelect(
                    variant="outlined",
                    mode="multiple",
                    placeholder='variant="outlined"（默认）',
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    variant="filled",
                    mode="multiple",
                    placeholder='variant="filled"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    variant="borderless",
                    mode="multiple",
                    placeholder='variant="borderless"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
                fac.AntdSelect(
                    variant="underlined",
                    mode="multiple",
                    placeholder='variant="underlined"',
                    options=[f"选项{i}" for i in range(1, 6)],
                    style={"width": "100%"},
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDivider(
                    "Variant examples (single select)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    variant="outlined",
                    placeholder='variant="outlined" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="filled",
                    placeholder='variant="filled"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="underlined",
                    placeholder='variant="underlined"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="borderless",
                    placeholder='variant="borderless"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "Variant examples (multiple select)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    variant="outlined",
                    mode="multiple",
                    placeholder='variant="outlined" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="filled",
                    mode="multiple",
                    placeholder='variant="filled"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="borderless",
                    mode="multiple",
                    placeholder='variant="borderless"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="underlined",
                    mode="multiple",
                    placeholder='variant="underlined"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": 350},
        )

    return demo_contents


def code_string() -> list:
    current_locale = get_current_locale()
    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider(
            '默认模式不同变体示例', innerTextOrientation='left'
        ),
        fac.AntdSelect(
            variant='outlined',
            placeholder='variant="outlined"（默认）',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            variant='filled',
            placeholder='variant="filled"',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            variant='underlined',
            placeholder='variant="underlined"',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            variant='borderless',
            placeholder='variant="borderless"',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdDivider(
            '多选模式不同变体示例', innerTextOrientation='left'
        ),
        fac.AntdSelect(
            variant='outlined',
            mode='multiple',
            placeholder='variant="outlined"（默认）',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            variant='filled',
            mode='multiple',
            placeholder='variant="filled"',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            variant='borderless',
            mode='multiple',
            placeholder='variant="borderless"',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
        fac.AntdSelect(
            variant='underlined',
            mode='multiple',
            placeholder='variant="underlined"',
            options=[f'选项{i}' for i in range(1, 6)],
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdDivider(
                    "Variant examples (single select)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    variant="outlined",
                    placeholder='variant="outlined" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="filled",
                    placeholder='variant="filled"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="underlined",
                    placeholder='variant="underlined"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="borderless",
                    placeholder='variant="borderless"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdDivider(
                    "Variant examples (multiple select)", innerTextOrientation="left"
                ),
                fac.AntdSelect(
                    variant="outlined",
                    mode="multiple",
                    placeholder='variant="outlined" (default)',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="filled",
                    mode="multiple",
                    placeholder='variant="filled"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="borderless",
                    mode="multiple",
                    placeholder='variant="borderless"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
                fac.AntdSelect(
                    variant="underlined",
                    mode="multiple",
                    placeholder='variant="underlined"',
                    options=[f"Option {i}" for i in range(1, 6)],
                    style={"width": "100%"},
                    locale="en-us",
                ),
)
"""
            }
        ]

```

## API 文档

- id (string; optional):
  Component unique id.

- key (string; optional):
  Update the `key` value of the current component to force re-rendering of the current component F.

- className (string | dict; optional):
  CSS class name of the current component, supports [dynamic css](/advanced-classname).

- popupClassName (string; optional):
  CSS class name for the expanded menu.

- name (string; optional):
  Used with `AntdForm` for batch value collection/control, serving as the field name of the current form item, with `id` as the default value.

- enableBatchControl (boolean; default True):
  Controls whether the current component participates in the effective `AntdForm` batch value collection/control feature. Default: `True`.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
  Component text locale. Options are `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German), `'ru-ru'` (Russian)
  Default: `'zh-cn'`.

- options (list of dicts; optional):
  Configure dropdown options.

  `options` is a list of string | number | dict with keys:

  - label (a list of or a singular dash component, string or number; required):
    Component type, the label content of the current option.

  - value (string

    Or number; required):
    The value of the current option.

  - disabled (boolean; optional):
    Whether to disable the current option. Default: `False`.

  - colors (list of strings; optional):
    For the color ramp special rendering mode, set the array of color values required to generate the gradient color ramp. | dict with keys:

  - group (a list of or a singular dash component, string or number; optional):
    Component type, the label content of the current group.

  - options (list of dicts; optional):
    Configure options within the current group.

    `options` is a list of dicts with keys:

    - label (a list of or a singular dash component, string or number; required):

      Component type, the label content of the current option.

    - value (string | number; required):

      The value of the current option.

    - disabled (boolean; optional):

      Whether to disable the current option. Default: `False`.

    - colors (list of strings; optional):

      For the color ramp special rendering mode, set the array of color values required to generate the gradient color ramp.s

- listHeight (number; default 256):
  Maximum pixel height of the dropdown menu.

- colorsMode (a value equal to: 'sequential', 'diverging'; default 'sequential'):
  In the color ramp special rendering mode, set the rendering form. Options are `'sequential'`, `'diverging'`.

- colorsNameWidth (number; default 40):
  In the color ramp special rendering mode, set the pixel width of the name part for each option. Default: `40`.

- mode (a value equal to: 'multiple', 'tags'; optional):
  Selection mode. Options are `'multiple'` (multi-select), `'tags'` (free add).

- disabled (boolean; optional):
  Whether to disable the current component. Default: `False`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
  Current component size specification. Options are `'small'`, `'middle'`, `'large'`. Default: `'middle'`.

- bordered (boolean; default True):
  Whether to show the border. When set to `True`, it is equivalent to `variant='outlined'`. Default: `True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):
  Variant type. Options are `'outlined'`, `'borderless'`, `'filled'`, `'underlined'`. Among them, `'outlined'` is equivalent to `bordered=True`, but with higher priority.

- placeholder (string; optional):
  Placeholder text content for the input box.

- placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; default 'bottomLeft'):
  Direction in which the selection panel expands. Options are `'bottomLeft'`, `'bottomRight'`, `'topLeft'`, `'topRight'`
  Default: `'bottomLeft'`.

- value (string | number | list of string | numbers; optional):
  Listen to or set the selected value(s).

- defaultValue (string | number | list of string | numbers; optional):
  Initial selected value(s).

- maxTagCount (number | a value equal to: 'responsive'; default 5):
  When `multiple=True`, the maximum number of selected values to display. Default: `5`.

- status (a value equal to: 'error', 'warning'; optional):
  Control the validation state. Options are `'error'`, `'warning'`.

- optionFilterProp (a value equal to: 'value', 'label'; default 'value'):
  The target field for searching based on the input in the search box. Options are `'value'`, `'label'`. Default: `'value'`.

- searchValue (string; optional):
  Listen to the content already entered in the search box.

- optionFilterMode (a value equal to: 'case-insensitive', 'case-sensitive', 'regex', 'remote-match'; default 'case-insensitive'):
  Search matching mode. Options are `'case-insensitive'` (case insensitive), `'case-sensitive'` (case sensitive), `'regex'` (regular expression), `'remote-match'` (remote matching mode)
  Default: `'case-insensitive'`.

- debounceSearchValue (string; optional):
  Listen to the content already entered in the search box using a debounced delay.

- debounceWait (number; default 0):
  Debounce delay duration, in milliseconds. Default: `0`.

- autoSpin (boolean; default False):
  Whether to render in a loading state while the current component-related properties are being updated by callbacks. Default: `False`.

- autoClearSearchValue (boolean; default True):
  When `mode` is `'multiple'` or `'tags'`, set whether to automatically clear the content in the search box after selecting an item. Default: `True`.

- emptyContent (a list of or a singular dash component, string or number; optional):
  Component type, custom empty-data state prompt content.

- loadingEmptyContent (a list of or a singular dash component, string or number; optional):
  Component type, custom empty-data state prompt content in the loading state.

- dropdownBefore (a list of or a singular dash component, string or number; optional):
  Component type, prefix content of the selection menu.

- dropdownAfter (a list of or a singular dash component, string or number; optional):
  Component type, suffix content of the selection menu.

- prefix (a list of or a singular dash component, string or number; optional):
  Component type, embedded prefix content.

- suffixIcon (a list of or a singular dash component, string or number; optional):
  Custom suffix icon content for the selection box.

- allowClear (boolean; default True):
  Whether to allow one-click clearing of selected values. Default: `True`.

- autoFocus (boolean; default False):
  Whether to automatically gain focus. Default: `False`.

- popupMatchSelectWidth (boolean; default True):
  Whether the selection menu has the same width as the selection box. When set to `False`, virtual scrolling will be disabled. Default: `True`.

- readOnly (boolean; optional):
  Whether to render as read-only. Default: `False`.

- maxCount (number; optional):
  Effective in `'multiple'` and `'tags'` modes, limits the upper bound of the number of selected items.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
  Anchoring strategy for the related popup layer. Options are `'parent'`, `'body'`. Default: `'body'`.

- batchPropsNames (list of strings; optional):
  Several property names that need to be included in [batch property listening](/batch-props-values).

- batchPropsValues (dict; optional):
  Listen to several property values specified in `batchPropsNames`.

- data-_ (string; optional):
  Wildcard attributes in `data-_` format.

- aria-_ (string; optional):
  Wildcard attributes in `aria-_` format.

- persistence (boolean | string | number; optional):
  Whether to enable [prop persistence](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; optional):
  Several property names for which the persistence feature is enabled. Options are `'value'`. Default: `['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
  Type of persistent storage for properties. Options are `'local'` (local persistence), `'session'` (session persistence), `'memory'` (in-memory persistence)
  Default: `'local'`.
