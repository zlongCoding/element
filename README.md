# element
vue element 兼容思路

看element中在 DateTimePicker组件 无法 step，[官方解释](https://github.com/ElemeFE/element/issues/9878)。
正好公司同事也遇见这个问题，这个提供一种思路。
> 如果有缘人能够搜索到希望对你有用。

#### 思路
>我们知道vue是数据驱动视图的，那么这里的思路就是回归问题的本身，我们通过原生js来改变某一模块的方法，然后在通过数据驱动视图的变化，那么问题就可以解决了。


如果你需要使用，你可以按照下面步骤：
> 1. 需要引入element 的 DateTimePicker组件
> 2. 引入 DateTimer.vue
> 3. 使用方法在 index.vue

## 请注意
如果时间很紧，然后我们引入了第三方的库，如果第三方本身的方法不支持你的需求，那么这个时候你就需要考虑使用原生js来修改了。