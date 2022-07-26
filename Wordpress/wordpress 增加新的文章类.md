# 1.注册
找到functions.php
写` register_post_type( 'Demo', $args );`

```php

function custom_post_init() {
    $args = array(
      'public' => true,
      'has_archive' => true,
      'label'  => 'Demo', //这个就是显示出来的名称
      'menu_icon'=> 'dashicons-games',
      'supports' => array('title','editor'),

      'rewrite' => array('slug' => 'demos')
    );
    register_post_type( 'Demo', $args );
}
add_action( 'init', 'custom_post_init' );

```


# 2. 刷新“固定连接”
后台面板里： 设置-固定链接-保存设置（目的是刷新重构一下）。


# 效果
![[src/img/Pasted image 20220301211217.png]]