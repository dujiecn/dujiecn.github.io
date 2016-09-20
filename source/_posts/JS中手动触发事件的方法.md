---
title: JS中手动触发事件的方法
date: 2016-09-09 10:23:31
tags: "javascript"
---
如果大家将一张网页看成一个form的话，大致上就成了一个web form的模型。在win form 下要想手动触发某一个对象的事件是很简单的，只要发送一条消息即可达成。(PostMessage) 但是网页并不是基于消息机制的，如果我们想在一张网页上写出一个类似于按键精灵的功能该如何实现呢？
为大家介绍js下的几个方法：

1. createEvent（eventType）
参数：eventType 共5种类型：
    Events ：包括所有的事件. 
          HTMLEvents：包括 'abort', 'blur', 'change', 'error', 'focus', 'load', 'reset', 'resize', 'scroll', 'select', 
                                    'submit', 'unload'. 事件
          UIEevents ：包括 'DOMActivate', 'DOMFocusIn', 'DOMFocusOut', 'keydown', 'keypress', 'keyup'.
                                  间接包含 MouseEvents. 
          MouseEvents：包括 'click', 'mousedown', 'mousemove', 'mouseout', 'mouseover', 'mouseup'. 
          MutationEvents:包括 'DOMAttrModified', 'DOMNodeInserted', 'DOMNodeRemoved', 
                                      'DOMCharacterDataModified', 'DOMNodeInsertedIntoDocument', 
                                      'DOMNodeRemovedFromDocument', 'DOMSubtreeModified'. 
2. 在createEvent后必须初始化，为大家介绍5种对应的初始化方法
  HTMLEvents 和 通用 Events：
            initEvent( 'type', bubbles, cancelable )
    UIEvents ：
                      initUIEvent( 'type', bubbles, cancelable, windowObject, detail )
    MouseEvents： 
                      initMouseEvent( 'type', bubbles, cancelable, windowObject, detail, screenX, screenY, 
                      clientX, clientY, ctrlKey, altKey, shiftKey, metaKey, button, relatedTarget )
    MutationEvents ：
                      initMutationEvent( 'type', bubbles, cancelable, relatedNode, prevValue, newValue, 
                      attrName, attrChange ) 
3. 在初始化完成后就可以随时触发需要的事件了，为大家介绍targetObj.dispatchEvent(event)
    使targetObj对象的event事件触发
  需要注意的是在IE 5.5+版本上请用fireEvent方法，还是浏览兼容的考虑
4. 例子
    //例子1  立即触发鼠标被按下事件
    var fireOnThis = document.getElementById('someID');
        var evObj = document.createEvent('MouseEvents');
        evObj.initMouseEvent( 'click', true, true, window, 1, 12, 345, 7, 220, false, false, true, false, 0, null );
        fireOnThis.dispatchEvent(evObj);

  //例子2  考虑兼容性的一个鼠标移动事件
    var fireOnThis = document.getElementById('someID');
    if( document.createEvent ) 
    {
        var evObj = document.createEvent('MouseEvents');
        evObj.initEvent( 'mousemove', true, false );
        fireOnThis.dispatchEvent(evObj);
    }
  else if( document.createEventObject )
  {
      fireOnThis.fireEvent('onmousemove');
  }
