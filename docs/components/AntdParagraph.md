# AntdParagraph

## 简介源码：`views/AntdParagraph/intro.py`
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
                {'title': translator.t('通用')},
                {'title': translator.t('排版相关')},
                {'title': translator.t('AntdParagraph 段落')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdParagraph 段落'), level=2),
        fac.AntdParagraph(
            translator.t('用于渲染具有丰富样式和功能的段落文字。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdParagraph/demos/content_ellipsis.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale

paragraph_demo = '　　君不见黄河之水天上来，奔流到海不复回。君不见高堂明镜悲白发，朝如青丝暮成雪。人生得意须尽欢，莫使金樽空对月。天生我材必有用，千金散尽还复来。烹羊宰牛且为乐，会须一饮三百杯。岑夫子，丹丘生，将进酒，杯莫停。与君歌一曲，请君为我倾耳听。钟鼓馔玉不足贵，但愿长醉不复醒。古来圣贤皆寂寞，惟有饮者留其名。陈王昔时宴平乐，斗酒十千恣欢谑。主人何为言少钱，径须沽取对君酌。五花马，千金裘，呼儿将出换美酒，与尔同销万古愁。'
paragraph_demo_en_us = """To be, or not to be, that is the question:
Whether 'tis nobler in the mind to suffer
The slings and arrows of outrageous fortune,
Or to take arms against a sea of troubles
And by opposing end them. To die—to sleep,
No more; and by a sleep to say we end
The heart-ache and the thousand natural shocks
That flesh is heir to: 'tis a consummation
Devoutly to be wish'd. To die, to sleep;
To sleep, perchance to dream—ay, there's the rub:
For in that sleep of death what dreams may come,
When we have shuffled off this mortal coil,
Must give us pause—there's the respect
That makes calamity of so long life.
"""


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdSpace(
            [
                fac.AntdParagraph(paragraph_demo, ellipsis=True),
                fac.AntdParagraph(
                    paragraph_demo, ellipsis={'expandable': True}
                ),
                fac.AntdParagraph(
                    paragraph_demo, ellipsis={'expandable': True, 'rows': 3}
                ),
                fac.AntdParagraph(paragraph_demo, ellipsis={'suffix': '👉'}),
                fac.AntdParagraph(
                    paragraph_demo,
                    ellipsis={
                        'expandable': True,
                        'rows': 3,
                        'symbol': fac.AntdText('点我展开', type='secondary'),
                    },
                ),
                fac.AntdParagraph(
                    paragraph_demo,
                    ellipsis={'expandable': 'collapsible', 'rows': 3},
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdParagraph(
                    paragraph_demo_en_us, ellipsis=True, locale='en-us'
                ),
                fac.AntdParagraph(
                    paragraph_demo_en_us,
                    ellipsis={'expandable': True},
                    locale='en-us',
                ),
                fac.AntdParagraph(
                    paragraph_demo_en_us,
                    ellipsis={'expandable': True, 'rows': 3},
                    locale='en-us',
                ),
                fac.AntdParagraph(
                    paragraph_demo_en_us,
                    ellipsis={'suffix': '👉'},
                    locale='en-us',
                ),
                fac.AntdParagraph(
                    paragraph_demo_en_us,
                    ellipsis={
                        'expandable': True,
                        'rows': 3,
                        'symbol': fac.AntdText('点我展开', type='secondary'),
                    },
                    locale='en-us',
                ),
                fac.AntdParagraph(
                    paragraph_demo_en_us,
                    ellipsis={'expandable': 'collapsible', 'rows': 3},
                    locale='en-us',
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
paragraph_demo = '　　君不见黄河之水天上来，奔流到海不复回。君不见高堂明镜悲白发，朝如青丝暮成雪。人生得意须尽欢，莫使金樽空对月。天生我材必有用，千金散尽还复来。烹羊宰牛且为乐，会须一饮三百杯。岑夫子，丹丘生，将进酒，杯莫停。与君歌一曲，请君为我倾耳听。钟鼓馔玉不足贵，但愿长醉不复醒。古来圣贤皆寂寞，惟有饮者留其名。陈王昔时宴平乐，斗酒十千恣欢谑。主人何为言少钱，径须沽取对君酌。五花马，千金裘，呼儿将出换美酒，与尔同销万古愁。'

...

fac.AntdSpace(
    [
        fac.AntdParagraph(paragraph_demo, ellipsis=True),
        fac.AntdParagraph(
            paragraph_demo, ellipsis={'expandable': True}
        ),
        fac.AntdParagraph(
            paragraph_demo, ellipsis={'expandable': True, 'rows': 3}
        ),
        fac.AntdParagraph(paragraph_demo, ellipsis={'suffix': '👉'}),
        fac.AntdParagraph(
            paragraph_demo,
            ellipsis={
                'expandable': True,
                'rows': 3,
                'symbol': fac.AntdText('点我展开', type='secondary'),
            },
        ),
        fac.AntdParagraph(
            paragraph_demo,
            ellipsis={'expandable': 'collapsible', 'rows': 3},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
paragraph_demo_en_us = """To be, or not to be, that is the question:
Whether 'tis nobler in the mind to suffer
The slings and arrows of outrageous fortune,
Or to take arms against a sea of troubles
And by opposing end them. To die—to sleep,
No more; and by a sleep to say we end
The heart-ache and the thousand natural shocks
That flesh is heir to: 'tis a consummation
Devoutly to be wish'd. To die, to sleep;
To sleep, perchance to dream—ay, there's the rub:
For in that sleep of death what dreams may come,
When we have shuffled off this mortal coil,
Must give us pause—there's the respect
That makes calamity of so long life.
"""
...

fac.AntdSpace(
    [
        fac.AntdParagraph(
            paragraph_demo_en_us, ellipsis=True, locale='en-us'
        ),
        fac.AntdParagraph(
            paragraph_demo_en_us,
            ellipsis={'expandable': True},
            locale='en-us',
        ),
        fac.AntdParagraph(
            paragraph_demo_en_us,
            ellipsis={'expandable': True, 'rows': 3},
            locale='en-us',
        ),
        fac.AntdParagraph(
            paragraph_demo_en_us,
            ellipsis={'suffix': '👉'},
            locale='en-us',
        ),
        fac.AntdParagraph(
            paragraph_demo_en_us,
            ellipsis={
                'expandable': True,
                'rows': 3,
                'symbol': fac.AntdText('点我展开', type='secondary'),
            },
            locale='en-us',
        ),
        fac.AntdParagraph(
            paragraph_demo_en_us,
            ellipsis={'expandable': 'collapsible', 'rows': 3},
            locale='en-us',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
'''
            }
        ]

```

### `views/AntdParagraph/demos/different_render_mode.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component

from i18n import get_current_locale

paragraph_demo = '　　君不见黄河之水天上来，奔流到海不复回。君不见高堂明镜悲白发，朝如青丝暮成雪。人生得意须尽欢，莫使金樽空对月。天生我材必有用，千金散尽还复来。烹羊宰牛且为乐，会须一饮三百杯。岑夫子，丹丘生，将进酒，杯莫停。与君歌一曲，请君为我倾耳听。钟鼓馔玉不足贵，但愿长醉不复醒。古来圣贤皆寂寞，惟有饮者留其名。陈王昔时宴平乐，斗酒十千恣欢谑。主人何为言少钱，径须沽取对君酌。五花马，千金裘，呼儿将出换美酒，与尔同销万古愁。'
paragraph_demo_en_us = """To be, or not to be, that is the question:
Whether 'tis nobler in the mind to suffer
The slings and arrows of outrageous fortune,
Or to take arms against a sea of troubles
And by opposing end them. To die—to sleep,
No more; and by a sleep to say we end
The heart-ache and the thousand natural shocks
That flesh is heir to: 'tis a consummation
Devoutly to be wish'd. To die, to sleep;
To sleep, perchance to dream—ay, there's the rub:
For in that sleep of death what dreams may come,
When we have shuffled off this mortal coil,
Must give us pause—there's the respect
That makes calamity of so long life.
"""


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = html.Div(
            [
                fac.AntdDivider('默认模式', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo),
                fac.AntdDivider('code=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, code=True),
                fac.AntdDivider('copyable=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, copyable=True),
                fac.AntdDivider(
                    'strikethrough=True', innerTextOrientation='left'
                ),
                fac.AntdParagraph(paragraph_demo, strikethrough=True),
                fac.AntdDivider('disabled=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, disabled=True),
                fac.AntdDivider('mark=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, mark=True),
                fac.AntdDivider('strong=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, strong=True),
                fac.AntdDivider('italic=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, italic=True),
                fac.AntdDivider('underline=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, underline=True),
                fac.AntdDivider(
                    'type="secondary"', innerTextOrientation='left'
                ),
                fac.AntdParagraph(paragraph_demo, type='secondary'),
                fac.AntdDivider('type="success"', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, type='success'),
                fac.AntdDivider('type="warning"', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, type='warning'),
                fac.AntdDivider('type="danger"', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo, type='danger'),
            ]
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = html.Div(
            [
                fac.AntdDivider('默认模式', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us),
                fac.AntdDivider('code=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, code=True),
                fac.AntdDivider('copyable=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, copyable=True),
                fac.AntdDivider(
                    'strikethrough=True', innerTextOrientation='left'
                ),
                fac.AntdParagraph(paragraph_demo_en_us, strikethrough=True),
                fac.AntdDivider('disabled=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, disabled=True),
                fac.AntdDivider('mark=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, mark=True),
                fac.AntdDivider('strong=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, strong=True),
                fac.AntdDivider('italic=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, italic=True),
                fac.AntdDivider('underline=True', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, underline=True),
                fac.AntdDivider(
                    'type="secondary"', innerTextOrientation='left'
                ),
                fac.AntdParagraph(paragraph_demo_en_us, type='secondary'),
                fac.AntdDivider('type="success"', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, type='success'),
                fac.AntdDivider('type="warning"', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, type='warning'),
                fac.AntdDivider('type="danger"', innerTextOrientation='left'),
                fac.AntdParagraph(paragraph_demo_en_us, type='danger'),
            ]
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
paragraph_demo = '　　君不见黄河之水天上来，奔流到海不复回。君不见高堂明镜悲白发，朝如青丝暮成雪。人生得意须尽欢，莫使金樽空对月。天生我材必有用，千金散尽还复来。烹羊宰牛且为乐，会须一饮三百杯。岑夫子，丹丘生，将进酒，杯莫停。与君歌一曲，请君为我倾耳听。钟鼓馔玉不足贵，但愿长醉不复醒。古来圣贤皆寂寞，惟有饮者留其名。陈王昔时宴平乐，斗酒十千恣欢谑。主人何为言少钱，径须沽取对君酌。五花马，千金裘，呼儿将出换美酒，与尔同销万古愁。'

...

html.Div(
    [
        fac.AntdDivider(
            '默认模式',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo
        ),
        fac.AntdDivider(
            'code=True',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            code=True
        ),
        fac.AntdDivider(
            'copyable=True',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            copyable=True
        ),
        fac.AntdDivider(
            'strikethrough=True',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            strikethrough=True
        ),
        fac.AntdDivider(
            'disabled=True',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            disabled=True
        ),
        fac.AntdDivider(
            'mark=True',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            mark=True
        ),
        fac.AntdDivider(
            'strong=True',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            strong=True
        ),
        fac.AntdDivider(
            'italic=True',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            italic=True
        ),
        fac.AntdDivider(
            'underline=True',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            underline=True
        ),
        fac.AntdDivider(
            'type="secondary"',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            type="secondary"
        ),
        fac.AntdDivider(
            'type="success"',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            type="success"
        ),
        fac.AntdDivider(
            'type="warning"',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            type="warning"
        ),
        fac.AntdDivider(
            'type="danger"',
            innerTextOrientation='left'
        ),
        fac.AntdParagraph(
            paragraph_demo,
            type="danger"
        )
    ]
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
paragraph_demo_en_us = """To be, or not to be, that is the question:
Whether 'tis nobler in the mind to suffer
The slings and arrows of outrageous fortune,
Or to take arms against a sea of troubles
And by opposing end them. To die—to sleep,
No more; and by a sleep to say we end
The heart-ache and the thousand natural shocks
That flesh is heir to: 'tis a consummation
Devoutly to be wish'd. To die, to sleep;
To sleep, perchance to dream—ay, there's the rub:
For in that sleep of death what dreams may come,
When we have shuffled off this mortal coil,
Must give us pause—there's the respect
That makes calamity of so long life.
"""

...

html.Div(
    [
        fac.AntdDivider('默认模式', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us),
        fac.AntdDivider('code=True', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, code=True),
        fac.AntdDivider('copyable=True', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, copyable=True),
        fac.AntdDivider(
            'strikethrough=True', innerTextOrientation='left'
        ),
        fac.AntdParagraph(paragraph_demo_en_us, strikethrough=True),
        fac.AntdDivider('disabled=True', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, disabled=True),
        fac.AntdDivider('mark=True', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, mark=True),
        fac.AntdDivider('strong=True', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, strong=True),
        fac.AntdDivider('italic=True', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, italic=True),
        fac.AntdDivider('underline=True', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, underline=True),
        fac.AntdDivider(
            'type="secondary"', innerTextOrientation='left'
        ),
        fac.AntdParagraph(paragraph_demo_en_us, type='secondary'),
        fac.AntdDivider('type="success"', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, type='success'),
        fac.AntdDivider('type="warning"', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, type='warning'),
        fac.AntdDivider('type="danger"', innerTextOrientation='left'),
        fac.AntdParagraph(paragraph_demo_en_us, type='danger'),
    ]
)
'''
            }
        ]

```

## API 文档

- children (a list of or a singular dash component, string or number; optional):
    Component type, embedded elements.

- id (string; optional):
    Unique ID for the component.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- className (string | dict; optional):
    The CSS class name for the current component, supports [dynamic CSS class names](/advanced-classname).

- code (boolean; optional):
    Whether to render as code format.

- copyable (boolean; optional):
    Whether to enable the quick copy feature.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- disabled (boolean; optional):
    Whether to render as disabled.

- ellipsis (dict; default False):
    Configures the ellipsis functionality for content. Set to `False` to disable. Default value: `False`.

    `ellipsis` can be a boolean or a dict with keys:

    - expandable (boolean | a value equal to: 'collapsible'; optional):
        Whether it is expandable.

    - rows (number; optional):
        Maximum number of visible rows.

    - suffix (string; optional):
        Custom suffix after content is ellipsized.

    - symbol (a list of or a singular dash component, string or number; optional):
        Component type, custom content expansion control.

- italic (boolean; optional):
    Whether to render as italic.

- key (string; optional):
    Update the `key` value for the current component, which can force a redraw of the current component.

- loading_state (dict; optional):

    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- locale (a value equal to: 'zh-cn', 'en-us'; default 'zh-cn'):
    The language of the component's text, options include `'zh-cn'`, `'en-us'`. Default value: `'zh-cn'`.

- mark (boolean; optional):
    Whether to render as highlighted.

- strikethrough (boolean; optional):
    Whether to render as strikethrough.

- strong (boolean; optional):
    Whether to render as bold.

- style (dict; optional):
    The CSS styles for the current component.

- type (a value equal to: 'secondary', 'success', 'warning', 'danger'; optional):
    Sets the special state of the content, options include `'secondary'`, `'success'`, `'warning'`, `'danger'`.

- underline (boolean; optional):
    Whether to render as underlined.
