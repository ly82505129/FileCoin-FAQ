---
coverY: 0
---

# Venus-Market

Dive into the specifics of each API endpoint by checking out our complete documentation.

#### 配置相关问题：

1.  若遇到`Too Many Files`的报错时，先设置如下命令：

    ```
    cat > /etc/security/limits.conf << EOF
    * soft nofile 655350
    * hard nofile 655360
    * soft nproc 655350
    * hard nproc 655350
    root soft nofile 655350
    root hard nofile 655360
    root soft nproc 655350
    root hard nproc 655350
    EOF

    cat >> /etc/sysctl.conf << EOF
    net.ipv4.neigh.default.gc_thresh1 = 8192
    net.ipv4.neigh.default.gc_thresh2 = 32768
    net.ipv4.neigh.default.gc_thresh3 = 65536
    EOF

    sysctl -p
    sed -i '/#DefaultLimitNOFILE=/a DefaultLimitNOFILE=655350' /etc/systemd/system.conf
    sed -i '/#DefaultLimitNOFILE=/a DefaultLimitNOFILE=655350' /etc/systemd/user.conf
    systemctl daemon-reexec
    ```

    \
    通过`ps aux | grep venus` 检查 market 进程的id\

2. 11







## Pets

All the methods associated with `CRUD`ing some pets. Which isn't as weird as it sounds:

{% content-ref url="pets.md" %}
[pets.md](pets.md)
{% endcontent-ref %}

## Users

Everything related to users:

{% content-ref url="users.md" %}
[users.md](users.md)
{% endcontent-ref %}

{% hint style="info" %}
**Good to know:** Using the 'Page Link' block lets you link directly to a page. If this page's name, URL or parent location changes, the reference will be kept up to date. You can also mention a page – like [pets.md](pets.md "mention") – if you don't want a block-level link.
{% endhint %}
