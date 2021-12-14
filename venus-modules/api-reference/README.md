---
coverY: 0
---

# Venus-Market

### 在使用Market过程中遇到的相关问题：

*   若遇到`Too Many Files`的报错时，先设置如下命令：

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
    通过`ps aux | grep venus` 检查 market 进程的id;\
    通过`cat proc/<Market进程id>/limits` 查看market进程的limit中open files是否已设置成功；\
    若未设置成功请重启market，使limitis生效即可。



* Venus Market 在几次运行过程无法接收远程发送的订单，检查多次也无法确定问题在哪里的情况下，最终的解决的方案是：

{% hint style="info" %}
**解决方案：**

删除.venusmarket/ 的目录，重新在venus-market目中./venus-market run,重新初始化，可以解决大部分遇到的问题。
{% endhint %}



* 一般默认在编辑venus-market时会存放在系统盘，若系统盘目录空间不足时可能会导致诸多问题，此种情况下：

{% hint style="info" %}
**解决方案：**

初始化完成时，将.venusmarket/ 目录移动至磁盘空间充足的目录，启动makret时的命令：`nohup ./venus-market --repo=/<绝对路径>/.venusmarket run >>market.log 2>&1&`&#x20;
{% endhint %}



* 若移动了.venumarket的路径后，/venus-market目录下的相关命令的使用需使用如下命令：

{% hint style="info" %}
**解决方案：**

`./venus-market --repo=/<绝对路径>/.venusmarket data-transfers list`
{% endhint %}

*

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
