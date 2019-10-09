## 不要把es6的export和commonjs的exports搞混淆

同样都是作为模块化导出的方案，这两者看似相似，其实却有着本质的不同，笼统的说，exports后面多一个s，我们可以将其理解成export的升级版(plus)，这样一个升级版自然是要给后台用的，也就是nodejs来用的，把这个搞清楚后，我们现在就只来讨论nodejs后台部分使用的exports和module.exports的区别。

module.exports和exports的关系我们可以用这张图来解释

![avatar](../images/exports.png)

可以打个比方，module.exports和exports就好比是火影忍者里头的柱间和斑，module.exports是柱间，exports是斑，刚开始的时候，两个人目标一直，都渴望建立一个和平的国家，但是此时这个国家还不存在，也就是他们心中指向的都是{}(一个空对象)。
随着时间的推移，这个国家渐渐的出现了，随着忍者数量的增多，需要指派的任务也就渐渐增多，这时就需要柱间(module.exports)和斑(exports)来指派任务，由于两人都是创始人，自然没有什么区分，忍者们既听命于柱间(module.exports)同时也听命于斑(exports)。
可是好景不长，突然有一天，斑(exports)做了一个错误的决定，他心中的理想国变了，想建立一个“更美好”的国家，这个时候斑(exports)倘若再次向忍者们下发指令的话，是没有忍者会听命于他的，所以这时候斑(exports)在下发任何任务都无济于事...
