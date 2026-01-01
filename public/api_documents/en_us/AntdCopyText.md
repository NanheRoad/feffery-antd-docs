

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- text (string; default ''):
    复制目标内容.

- format (a value equal to: 'text/plain', 'text/html'; default 'text/plain'):
    剪切板内容的类型，可选项有`'text/plain'`、`text/html`  默认值：`'text/plain'`.

- tooltips (list of a list of or a singular dash component, string or numbers | boolean; optional):
    设置复制前后的文字提示内容，格式为`[复制前内容, 复制后内容]`，设置为`False`时关闭文字提示.

- beforeIcon (a list of or a singular dash component, string or number; optional):
    组件型，未复制状态图标.

- afterIcon (a list of or a singular dash component, string or number; optional):
    组件型，完成复制状态图标.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.