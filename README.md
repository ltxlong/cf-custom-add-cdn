# cf-custom-add-cdn

cloudflare自定义CDN加速


# 配置参数

设置变量 PROXY_URL 为需要加速的第三方url（不带http或者https）

【注意】每次修改完变量，需要重新部署才会生效！

# 使用场景一：

fork项目，部署为pages，相当于第三方url（如vercel分配的域名）直接套cf加速

# 使用场景二：

fork项目，部署为worker，在套cf加速的基础上，实现自定义CDN加速，速度更快

这个的 PROXY_URL 可以是第三方url（如vercel分配的域名），还可以是cf的pages分配的域名

部署完worker，设置完 PROXY_URL 之后，在Workers管理面板打开 ”设置->触发器->路由” 添加一个路由，
填入 ”<域名B>/*”(/*不能掉！)，再选择你cf绑定的区域以添加

最后，添加DNS记录：

添加A记录 或者 CNAME记录，注意关掉CDN （关不关，实践再议）

### 添加A记录（推荐）：

ipv4：

1.1.1.0/16 IP段 和 1.0.0.0/16 IP段（因为这两个IP段线路优化良好），
排除1.1.1.1和1.0.0.1（因为国内某些地区会阻挠，导致不稳定）

如：1.1.1.2, 1.1.1.3, 1.1.1.99, 1.0.0.2, 1.0.0.3, 1.0.0.99

ipv6：

2606:4700:4700::/48 IP段

如：2606:4700:4700::abcd, 2606:4700:4700::2222, 2606:4700:4700::99

### 添加CNAME记录：

CNAME到优选域名上，如：cloudflare.182682.xyz, cloudflare.v6.rocks, ip.sb



