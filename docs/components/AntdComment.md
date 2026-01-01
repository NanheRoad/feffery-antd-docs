# AntdComment

## 简介源码：`views/AntdComment/intro.py`
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
                {'title': 'AntdComment 评论'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdComment 评论', level=2),
        fac.AntdParagraph('构建常用的用户评论相关功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
[
    fac.AntdComment(
        id='comment-demo',
        authorName='费弗里',
        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
        publishTime={
            'value': '2024-01-01 19:29:01',
            'format': 'YYYY-MM-DD hh:mm:ss',
        },
        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
        defaultAction='liked',
        likesCount=1,
    ),
    fac.AntdSpace(
        [
            fac.AntdInput(
                id='comment-demo-input',
                placeholder='发表你的感想...',
                mode='text-area',
                maxLength=140,
                allowClear=True,
                showCount=True,
                style={'width': '100%'},
            ),
            fac.AntdButton(
                '提交评论',
                id='comment-demo-submit',
                type='primary',
                style={'float': 'right'},
            ),
        ],
        size='large',
        direction='vertical',
        style={'width': '100%'},
    ),
]

...

@app.callback(
    [Output('comment-demo', 'children'), Output('comment-demo-input', 'value')],
    [
        Input('comment-demo-submit', 'nClicks'),
        Input({'type': 'comment-demo-children', 'index': ALL}, 'deleteClicks'),
    ],
    [State('comment-demo-input', 'value'), State('comment-demo', 'children')],
    prevent_initial_call=True,
)
def comment_demo_add_children_callback(nClicks, deleteClicks, value, children):
    # 本次回调由子回复删除功能触发
    if 'deleteClicks' in dash.callback_context.triggered[0]['prop_id']:
        triggerIndex = eval(
            dash.callback_context.triggered[0]['prop_id'].replace(
                '.deleteClicks', ''
            )
        )['index']

        return [
            child
            for child in children
            if child['props']['id']['index'] != triggerIndex
        ], dash.no_update

    if value:
        return children + [
            fac.AntdComment(
                id={
                    'type': 'comment-demo-children',
                    'index': str(uuid.uuid4()),
                },
                authorName='dash学习者',
                publishTime={
                    'value': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
                    'format': 'YYYY-MM-DD hh:mm:ss',
                },
                commentContent=value,
                showReply=False,
                showDelete=True,
            )
        ] if children else [
            fac.AntdComment(
                id={
                    'type': 'comment-demo-children',
                    'index': str(uuid.uuid4()),
                },
                authorName='dash学习者',
                publishTime={
                    'value': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
                    'format': 'YYYY-MM-DD hh:mm:ss',
                },
                commentContent=value,
                showReply=False,
                showDelete=True,
            )
        ], None

    else:
        return children, None
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdComment(
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
)
```

### custom_avatar

- 说明：演示 custom_avatar 的用法。

#### 代码
```python
fac.AntdComment(
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    avatarProps={
        'mode': 'image',
        'src': '/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
    },
)
```

### from_now

- 说明：演示 from_now 的用法。

#### 代码
```python
fac.AntdComment(
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    avatarProps={'mode': 'image', 'src': '/assets/imgs/avatar-demo.jpg'},
    fromNow=True,
)
```

### initial_status

- 说明：演示 initial_status 的用法。

#### 代码
```python
fac.AntdComment(
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    defaultAction='liked',
    likesCount=1,
)
```

### nested

- 说明：演示 nested 的用法。

#### 代码
```python
fac.AntdComment(
    [
        fac.AntdComment(
            authorName='dash爱好者',
            publishTime={
                'value': '2024-01-01 19:34:19',
                'format': 'YYYY-MM-DD hh:mm:ss',
            },
            commentContent='资瓷一个！😊',
        ),
        fac.AntdComment(
            authorName='dash-player',
            publishTime={
                'value': '2024-01-01 19:40:29',
                'format': 'YYYY-MM-DD hh:mm:ss',
            },
            commentContent='我要好好学习dash和fac，争取早日开发出自己的个人博客网站！',
        ),
    ],
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    avatarProps={'mode': 'image', 'src': '/assets/imgs/avatar-demo.jpg'},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- children (a list of or a singular dash component, string or number; optional):
    传入内部嵌套的评论组件.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- commentId (string; optional):
    评论唯一id，可用于数据库匹配等场景.

- authorName (string; optional):
    评论发布用户名.

- authorNameHref (string; optional):
    评论发布用户名附带链接地址.

- publishTime (dict; required):
    必填，配置发布日期时间相关参数.

    `publishTime` is a dict with keys:

    - value (string; required):
        必填，日期时间字符串.

    - format (string; optional):
        与日期时间字符串匹配的格式.

- fromNow (boolean; default False):
    是否以相对时间格式呈现发布日期时间.

- showLikeDislike (boolean; default True):
    是否显示“支持/反对”按钮  默认值：`True`.

- showReply (boolean; default True):
    是否显示“添加回复”按钮  默认值：`True`.

- showDelete (boolean; default False):
    是否显示“删除”按钮  默认值：`False`.

- replyClicks (number; default 0):
    监听“添加回复”按钮累计点击次数  默认值：`0`.

- deleteClicks (number; default 0):
    监听“删除”按钮累计点击次数  默认值：`0`.

- commentContent (a list of or a singular dash component, string or number; optional):
    组件型，评论正文内容.

- likesCount (number; default 0):
    监听或设置“支持”次数.

- dislikesCount (number; default 0):
    监听或设置“反对”次数.

- action (a value equal to: 'liked', 'disliked', 'default'; optional):
    监听或设置当前评论“支持/反对”状态，可选项有`'liked'`、`'disliked'`、`'default'`
    默认值：`'default'`.

- defaultAction (a value equal to: 'liked', 'disliked', 'default'; optional):
    设置当前评论初始化时的“支持/反对”状态，可选项有`'liked'`、`'disliked'`、`'default'`.

- avatarProps (dict; optional):
    配置评论用户头像，同`AntdAvatar`.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    相关展开层锚定策略，可选项有`'parent'`、`'body'`  默认值：`'body'`.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

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
