# Tg-bot_agent
利用cf代理TG实现国内服务器使用Tg_bot
# 启用worker
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122131406.png)
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122133195.png)
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122134546.png)
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122134266.png)
复制以下代码
机器人id就是创建机器人后生成的token前面的数字部分
```
const whitelist = ["/bot123456789:"];/*123456789为机器人ID*/
const tg_host = "api.telegram.org";
addEventListener('fetch', event => {
    event.respondWith(handleRequest(event.request))
})
function validate(path) {
    for (var i = 0; i < whitelist.length; i++) {
        if (path.startsWith(whitelist[i]))
            return true;
    }
    return false;
}
async function handleRequest(request) {
    var u = new URL(request.url);
    u.host = tg_host;
    if (!validate(u.pathname))
        return new Response('Unauthorized', {
            status: 403
        });
    var req = new Request(u, {
        method: request.method,
        headers: request.headers,
        body: request.body
    });
    const result = await fetch(req);
    return result;
}
```
# 对接青龙面板的通知
TG_BOT_TOKEN：在TG @BotFather这个机器人获取（上面有说，这里是取完一整串而不是前面几个数字）；
TG_USER_ID：在TG@@userinfobot这个机器人获取；
TG_API_HOST：重点就是要填好这个反代的地址，不需要http/https
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122146878.png)
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122142531.png)
# 青龙面板-系统设置-通知设置
填上对应的，重点就是后面反代地址（不需要http/https）
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122150940.png)
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122152100.png)
# 保存，提示通知发送成功，TG机器人就会收到通知测试了
如果再点击保存的时候报错，需要启动下你的机器人
![](https://cdn.jsdelivr.net/gh/aProfessor23/PicBed@main/img/202203122157958.png)
