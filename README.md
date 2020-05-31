emqx_bridge_kafka
====================

This is a template plugin for the EMQ X broker. And you can see [Plugin Development Guide](https://docs.emqx.io/broker/v3/en/plugins.html#plugin-development-template) to learning how to use it.

Plugin Config
-------------

Each plugin should have a 'etc/{plugin_name}.conf|config' file to store application config.

Authentication and ACL
----------------------

```
emqx:hook('client.authenticate', fun ?MODULE:on_client_authenticate/3, [Env]).
emqx:hook('client.check_acl', fun ?MODULE:on_client_check_acl/5, [Env]).
```

Plugin and Hooks
-----------------

[Plugin Design](https://docs.emqx.io/broker/v3/en/design.html#plugin-design)

[Hooks Design](https://docs.emqx.io/broker/v3/en/design.html#hooks-design)

License
-------

Apache License Version 2.0

Author
------

EMQ X Team.



适用示例：https://www.jianshu.com/p/177fb99a9fbf


#修改根目录下的rebar.config文件
修改如下：
{deps,
    [ emqx
    , emqx_retainer
    , emqx_management
    , emqx_reloader
    , emqx_bridge_mqtt
    , emqx_sn
    , emqx_coap
    , emqx_stomp
    , emqx_auth_clientid
    , emqx_auth_username
    , emqx_auth_http
    , emqx_auth_jwt
    , emqx_auth_mysql
    , emqx_web_hook
    , emqx_delayed_publish
    , emqx_recon
    , emqx_psk_file
    , emqx_rule_engine
    , emqx_plugin_template
    //以下为添加的代码（tag一定不能填错，不然make会失败。）
    , {emqx_plugin_customize, {git, "https://gitee.com/suncy666/emqx_plugin_customize.git", {tag, "suncy3.2.1"}}}
    ]}.

{relx,
        ...........
         //以下为添加代码
        , {emqx_plugin_customize, load}
        ]}

#修改Makefile文件：

CT_APPS := emqx_auth_jwt emqx_auth_mysql emqx_auth_username \
                emqx_delayed_publish emqx_management emqx_recon emqx_rule_enginex \
                emqx_stomp emqx_auth_clientid  emqx_auth_ldap   emqx_auth_pgsql \
                emqx_coap emqx_lua_hook emqx_passwd emqx_reloader emqx_sn \
                emqx_web_hook emqx_auth_http emqx_auth_mongo emqx_auth_redis \
                emqx_dashboard emqx_lwm2m emqx_psk_file emqx_retainer emqx_statsd \
   // 以下为添加代码
                emqx_plugin_customize

