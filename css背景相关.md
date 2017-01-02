# css background-clip和background-origin的区别

background-clip：border|padding|content

该属性指定了背景在哪些区域可以显示，但与背景开始绘制的位置无关，背景的绘制的位置可以出现在不显示背景的区域，这时就相当于背景图片被不显示背景的区域裁剪了一部分一样。

background-origin：padding|border|content

该属性指定了背景从哪个区域(边框、补白或内容)开始绘制,但也仅仅能控制背景开始绘制的位置，你可以用这个属性在边框上绘制背景，但边框上的背景显不显示出来那就要由background-clip来决定了