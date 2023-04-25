- 1.安装nodejs环境

- 2.环境安装成功后，解压mj_pro.zip 然后进入mj_pro文件夹，命令换输入npm install 

- 3.修改 midjourney.js 第30行，获取midjourney网页token，如何获取呢，登陆discord网页版然后F12到开发者工具,点击控制台（Console），输入一下代码获取midjoruy 账户的token值
  ```window.webpackChunkdiscord_app.push([
  [Math.random()],
  {},
  req => {
    for (const m of Object.keys(req.c)
         .map(x => req.c[x].exports)
         .filter(x => x)) {
      if (m.default && m.default.getToken !== undefined) {
        return copy(m.default.getToken());
      }
      if (m.getToken !== undefined) {
        return copy(m.getToken());
      }
    }
  },
]);
console.log(`%c token 在你的剪切板，请ctrl V 粘贴在代码里`, 'font-size: 16px');
```
token拷贝在这个地方token_channels.json这个文件

- 4.拷贝浏览器上midjourney 频道(channels)id,如
 https://discord.com/channels/1093538125210468392/1093710890408353803,链接的最后一个id,1093710890408353803

- 5.修改redis.js 第4行，输入你的redis账户 redis://:密码@ip:端口/1（没有自己的redis可以不用改）

- 6.然后运行代码
进入mj_pro 文件夹里，运行node index.js
- 7.生成token可以对api用户进行次数限制（如果自己设置可以把count设置最大）
执行node script.js 

- 8.api 接口说明
这里面的token是你scrpit.js生成的token（限制api调用接口次数的）
(1).提交指令api，token=您的token，prompt=你的指令
http://127.0.0.1:8000/midjourney/imagine?token=替换您的token&prompt=替换你的指令
(2).获取图片api， id=提交指令后返回json里的id
http://127.0.0.1:8000/midjourney/job?id=替换你的id
```{"prompt":"dog","upscale":false,"id":"07c618b4dc1790db9f32","tasks":1,"images":[{"id":"1098425776031924225","url":"https://cdn.discordapp.com/attachments/1093710890408353803/1098425775474090085/love3_dog_id07c618b4dc1790db9f32_c175bd36-ea7e-4f5f-891b-aaa48f0c836b.png","upscaled":false,"actions":[[{"label":"U1","id":"MJ::JOB::upsample::1::c175bd36-ea7e-4f5f-891b-aaa48f0c836b"},{"label":"U2","id":"MJ::JOB::upsample::2::c175bd36-ea7e-4f5f-891b-aaa48f0c836b"},{"label":"U3","id":"MJ::JOB::upsample::3::c175bd36-ea7e-4f5f-891b-aaa48f0c836b"},{"label":"U4","id":"MJ::JOB::upsample::4::c175bd36-ea7e-4f5f-891b-aaa48f0c836b"},{"label":"🔄","id":"MJ::JOB::reroll::0::c175bd36-ea7e-4f5f-891b-aaa48f0c836b::SOLO"}],[{"label":"V1","id":"MJ::JOB::variation::1::c175bd36-ea7e-4f5f-891b-aaa48f0c836b"},{"label":"V2","id":"MJ::JOB::variation::2::c175bd36-ea7e-4f5f-891b-aaa48f0c836b"},{"label":"V3","id":"MJ::JOB::variation::3::c175bd36-ea7e-4f5f-891b-aaa48f0c836b"},{"label":"V4","id":"MJ::JOB::variation::4::c175bd36-ea7e-4f5f-891b-aaa48f0c836b"}]]}]}
```
(3).升级大图获客获取单张图api，client_id =client_id, token=您的token , image=获取图片里面的image_id,action是actions下面id
http://127.0.0.1:8000/midjourney/action?client_id=替换你的client_id&token=替换您的token&image=替换你的image_id&action=替换你的action_id
(4).desc描述接口
filePath=你本地文件路径，图片用数字命名如 121558.jpg
http://127.0.0.1:8000/midjourney/desc?filePath=/Users/hpd/Desktop/121558.jpg
(5).获取描述接口：http://127.0.0.1:8000/midjourney/descjob?id=你的数字命名id
