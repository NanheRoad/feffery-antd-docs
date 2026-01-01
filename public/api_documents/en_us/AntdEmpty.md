

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - root (dict; optional):
        根元素css样式.

    - image (dict; optional):
        图标元素css样式.

    - description (dict; optional):
        描述元素css样式.

    - footer (dict; optional):
        底部元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - root (string; optional):
        根元素css类名.

    - image (string; optional):
        图标元素css类名.

    - description (string; optional):
        描述元素css类名.

    - footer (string; optional):
        底部元素css类名.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- description (a list of or a singular dash component, string or number | boolean; optional):
    描述信息内容.

- image (string | a value equal to: 'default', 'simple'; default 'default'):
    状态图片地址，也可以使用内置图片，可选项有`'default'`、`'simple'`  默认值：`'default'`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.