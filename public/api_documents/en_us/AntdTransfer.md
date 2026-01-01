

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

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- dataSource (list of dicts; optional):
    配置选项.

    `dataSource` is a list of dicts with keys:

    - key (string | number; optional):
        当前选项唯一识别id.

    - title (a list of or a singular dash component, string or number; optional):
        组件型，当前选项标题内容.

    - disabled (boolean; optional):
        是否禁用当前选项  默认值：`False`.

- selectionsIcon (a list of or a singular dash component, string or number; optional):
    组件型，自定义下拉菜单图标.

- height (string | number; optional):
    穿梭框整体高度.

- pagination (dict; default False):
    选项分页展示配置  默认值：`False`.

    `pagination` is a boolean | dict with keys:

    - pageSize (number; optional):
        每页最大选项数.

- oneWay (boolean; default False):
    是否启用单向模式  默认值：`False`.

- operations (list of a list of or a singular dash component, string or numbers; default ['', '']):
    左右移动操作按钮内容  默认值：`'['', '']'`.

- showSearch (boolean; default False):
    是否显示搜索框  默认值：`False`.

- optionFilterMode (a value equal to: 'case-insensitive', 'case-sensitive', 'regex'; default 'case-insensitive'):
    搜索匹配模式，可选项有`'case-insensitive'`（大小写不敏感）、`'case-sensitive'`（大小写敏感）、`'regex'`（正则表达式）
    默认值：`'case-insensitive'`.

- showSelectAll (boolean; default True):
    是否显示全选勾选框  默认值：`True`.

- titles (list of a list of or a singular dash component, string or numbers; optional):
    左右标题内容.

- targetKeys (list of number | strings; optional):
    监听或设置右侧区域已选项`key`值.

- moveDirection (a value equal to: 'left', 'right'; optional):
    监听最近一次选项移动对应方向，可选项有`'left'`、`'right'`.

- moveKeys (list of number | strings; optional):
    监听最近一次选项移动涉及的选项`key`值.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- status (a value equal to: 'error', 'warning'; optional):
    控制校验状态，可选项有`'error'`、`'warning'`.

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

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'targetKeys's; optional):
    开启属性持久化功能的若干属性名，可选项有`'targetKeys'`  默认值：`['targetKeys']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.