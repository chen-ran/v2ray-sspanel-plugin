# v2ray-sspanel-plugin
v2ray plugin to sspanel

```
curl -L -s https://raw.githubusercontent.com/chen-ran/v2ray-sspanel-plugin/master/install-release.sh | sudo bash
vim /etc/v2ray/config.json
```
#TCP模式
```
{
  "log": {
    "loglevel": "debug"
  },
  "api": {
    "tag": "api",
    "services": [
      "HandlerService",
      "LoggerService",
      "StatsService"
    ]
  },
  "stats": {},
  "inbounds": [
    {
      "port": 10086,
      "protocol": "vmess",
      "tag": "proxy"
    },
    {
      "listen": "127.0.0.1",
      "port": 10085,
      "protocol": "dokodemo-door",
      "settings": {
        "address": "127.0.0.1"
      },
      "tag": "api"
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom"
    }
  ],
  "routing": {
    "rules": [
      {
        "type": "field",
        "inboundTag": [
          "api"
        ],
        "outboundTag": "api"
      }
    ],
    "strategy": "rules"
  },
  "policy": {
    "levels": {
      "0": {
        "statsUserUplink": true,
        "statsUserDownlink": true
      }
    },
    "system": {
      "statsInboundUplink": true,
      "statsInboundDownlink": true
    }
  },
  "ssrpanel": {
    "nodeId": 1,
    "checkRate": 60,
    "user": {
      "inboundTag": "proxy",
      "level": 0,
      "alterId": 16,
      "security": "none"
    },
    "mysql": {
      "host": "144.33.X.X",
      "port": 3306,
      "user": "ssrpanel",
      "password": "password",
      "dbname": "ssrpanel"
    }
  }
}
```
##### 测试运行
```
/usr/bin/v2ray/v2ray -config /etc/v2ray/config.json
```
```
touch v2ray_logrun.sh
vim v2ray_logrun.sh

黏贴如下

nohup /usr/bin/v2ray/v2ray -config /etc/v2ray/config.json >> v2ray_run.log 2>&1 &

保存并执行： chmod a+x v2ray_logrun.sh && sh v2ray_logrun.sh
```

### Thanks:
[ColetteContreras/v2ray-ssrpanel-plugin](https://github.com/ColetteContreras/v2ray-ssrpanel-plugin)

[rico93/v2ray-sspanel-v3-mod_Uim-plugin](https://github.com/rico93/v2ray-sspanel-v3-mod_Uim-plugin)
