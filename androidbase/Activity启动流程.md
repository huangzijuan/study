
## Binder内存地址映射

800kb

## ActivityStackSupervisor
是一个Activity栈的管理类，有许多不同类型的list来存放ActivityRecord，ActivityStackSupervisor只是用来管理Activity与任务栈的，它并不具备执行具体操作的能力。
ActivityRecord封装与Activity有关的一系列参数，（例如：我是谁、我从哪里来、我要到哪里去）
