port: 7890
socks-port: 7891
allow-lan: true
mode: Rule
log-level: info
external-controller: 127.0.0.1:9090
proxies: []  # 节点列表已清空

proxy-groups:
  - name: 🚀 节点选择
    type: select
    proxies:
      - ♻️ 自动选择
      - 🔯 故障转移
      - 🔮 负载均衡
      - 🇭🇰 香港节点
      - 🇨🇳 台湾节点
      - 🇸🇬 狮城节点
      - 🇯🇵 日本节点
      - 🇺🇲 美国节点
      - 🇬🇧 英国节点
      - 🚀 手动切换

  - name: 🚀 手动切换
    type: select
    proxies: []  # 手动节点列表已清空

  - name: ♻️ 自动选择
    type: url-test
    url: http://www.gstatic.com/generate_204
    interval: 300
    tolerance: 50
    proxies: []  # 自动测试节点列表已清空

  - name: 🔯 故障转移
    type: fallback
    url: http://www.gstatic.com/generate_204
    interval: 300
    tolerance: 50
    proxies: []  # 故障转移节点列表已清空

  - name: 🔮 负载均衡
    type: load-balance
    strategy: consistent-hashing
    url: http://www.gstatic.com/generate_204
    interval: 300
    tolerance: 50
    proxies: []  # 负载均衡节点列表已清空

  # 以下为场景化代理组（结构保留，节点列表已清空）
  - name: 📲 电报消息
    type: select
    proxies: [🚀 节点选择, DIRECT]

  - name: 💬 OpenAi
    type: select
    proxies: [🚀 节点选择, DIRECT]

  - name: 📹 油管视频
    type: select
    proxies: [🚀 节点选择, DIRECT]

  - name: 🎥 奈飞视频
    type: select
    proxies: [🎥 奈飞节点, 🚀 节点选择, DIRECT]

  - name: 📺 巴哈姆特
    type: select
    proxies: [🇨🇳 台湾节点, DIRECT]

  - name: 📺 哔哩哔哩
    type: select
    proxies: [🎯 全球直连, 🇭🇰 香港节点]

  - name: 🌍 国外媒体
    type: select
    proxies: [🚀 节点选择, DIRECT]

  - name: 🌏 国内媒体
    type: select
    proxies: [DIRECT, 🇭🇰 香港节点]

  - name: 📢 谷歌FCM
    type: select
    proxies: [DIRECT, 🚀 节点选择]

  - name: Ⓜ️ 微软服务
    type: select
    proxies: [DIRECT, 🚀 节点选择]

  - name: 🍎 苹果服务
    type: select
    proxies: [DIRECT, 🚀 节点选择]

  - name: 🎮 游戏平台
    type: select
    proxies: [DIRECT, 🚀 节点选择]

  - name: 🎶 网易音乐
    type: select
    proxies: [DIRECT, 🚀 节点选择]

  - name: 🎯 全球直连
    type: select
    proxies: [DIRECT]

  - name: 🛑 广告拦截
    type: select
    proxies: [REJECT, DIRECT]

  - name: 🍃 应用净化
    type: select
    proxies: [REJECT, DIRECT]

  - name: 🐟 漏网之鱼
    type: select
    proxies: [DIRECT, 🚀 节点选择]

    proxy-groups:
  - name: 🔮 负载均衡
    type: load-balance
    strategy: consistent-hashing
    url: http://www.gstatic.com/generate_204
    interval: 600      # 调整测试间隔
    tolerance: 100    # 调整延迟容忍度
    proxies:
      - 🇺🇸 美国1 | ⬇️ 6.9MB/s...
      - 🇭🇰 香港1 | ⬇️ 7.4MB/s...
      # ...（保留稳定节点，移除高延迟节点）

- name: 🔮 负载均衡
  type: load-balance
  strategy: consistent-hashing  # 使用一致性哈希算法
  url: http://www.gstatic.com/generate_204  # 节点测试地址
  interval: 300  # 每5分钟测试一次
  tolerance: 50  # 允许50ms延迟波动
  proxies: 
    - 🇺🇸 美国1 | ⬇️ 6.9MB/s...
    - 🇫🇮 芬兰1 | ⬇️ 3.1MB/s...
    # ...（所有节点均已包含） 
