

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

- addonBefore (a list of or a singular dash component, string or number; optional):
    组件型，前置标签内容.

- addonAfter (a list of or a singular dash component, string or number; optional):
    组件型，后置标签内容.

- prefix (a list of or a singular dash component, string or number; optional):
    组件型，前缀内嵌内容.

- suffix (a list of or a singular dash component, string or number; optional):
    组件型，后缀内嵌内容.

- autoFocus (boolean; default False):
    是否自动获取焦点  默认值：`False`.

- controls (boolean; default True):
    是否显示增减数值按钮  默认值：`True`.

- keyboard (boolean; default True):
    是否允许通过键盘上下方向键控制数值  默认值：`True`.

- min (number | string; optional):
    允许输入的数值下限，默认无限制.

- max (number | string; optional):
    允许输入的数值上限，默认无限制.

- step (number | string; optional):
    数值增减步长.

- precision (number; optional):
    数值精度.

- stringMode (boolean; default False):
    是否开启字符串模式，用于在接受超高精度数值输入时不丢失精度，开启后，参数`min`、`max`、`step`、`value`、`defaultValue`均需要设置为字符型
    默认值：`False`.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    当前组件尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- bordered (boolean; default True):
    是否显示边框，设置为`True`时等价于`variant='outlined'`  默认值：`True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):
    形态变体类型，可选项有`'outlined'`、`'borderless'`、`'filled'`、`'underlined'`，其中`'outlined'`等价于`bordered=True`，但优先级更高.

- placeholder (string; optional):
    输入框占位文字内容.

- value (number | string; optional):
    监听或设置已输入值.

- defaultValue (number | string; optional):
    初始化已输入值.

- debounceValue (number | string; optional):
    监听防抖版本的已输入值.

- debounceWait (number; default 0):
    防抖延时时长，单位：毫秒  默认值：`0`.

- nSubmit (number; default 0):
    监听输入框聚焦状态下，键盘enter键累计点按次数  默认值：`0`.

- status (a value equal to: 'error', 'warning'; optional):
    控制校验状态，可选项有`'error'`、`'warning'`.

- readOnly (boolean; optional):
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

- persisted_props (list of a value equal to: 'value's; default ['value']):
    开启属性持久化功能的若干属性名，可选项有`'md5Value'`  默认值：`['md5Value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.