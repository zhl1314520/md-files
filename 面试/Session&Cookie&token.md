## Session & Cookie 流程

###### 用户在首次登录时，服务器端没有 session，浏览器端也没有 cookie。

###### 首次登录成功后，会在服务器端生成 session，并通过 set-cookie 将 session_id 发送给浏览器端。

###### 再次登录，用户点击登录按钮时会携带 cookie(主要是里面的session_id发挥作用)发送请求，此时会和服务器进行比对来确认用户合法性。



cookie：里面存储 session_id

session：里面存储用户信息



## Token（存储 user_info）

Session = 有状态（服务器存数据）
Token = 无状态（服务器不存数据）



###### 登录成功后，服务器端生成 token 返回给客户端报存

###### 后续请求，客户端携带 token 请求服务器。服务器比对（签名、解析user_info、过期时间），合法 ？放行 ：401