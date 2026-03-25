# HDMI驱动

## bug修复

### 空指向异常

```text
root@armbian:/boot# systemctl reboot -f
root@armbian:/boot# [  691.827981] watchdog: watchdog0: watchdog did not stop!
[  692.292516] Unable to handle kernel NULL pointer dereference at virtual address 0000000000000c85
[  692.301329] Mem abort info:
[  692.304136]   ESR = 0x0000000096000021
[  692.307890]   EC = 0x25: DABT (current EL), IL = 32 bits
[  692.313207]   SET = 0, FnV = 0
[  692.316268]   EA = 0, S1PTW = 0
[  692.319415]   FSC = 0x21: alignment fault
[  692.323430] Data abort info:
[  692.326315]   ISV = 0, ISS = 0x00000021, ISS2 = 0x00000000
[  692.331802]   CM = 0, WnR = 0, TnD = 0, TagAccess = 0
[  692.336856]   GCS = 0, Overlay = 0, DirtyBit = 0, Xs = 0
[  692.342171] user pgtable: 4k pages, 39-bit VAs, pgdp=00000000068cb000
[  692.348615] [0000000000000c85] pgd=0000000000000000, p4d=0000000000000000, pud=0000000000000000
[  692.357326] Internal error: Oops: 0000000096000021 [#1] SMP
[  692.362896] Modules linked in:
[  692.365952] CPU: 2 PID: 1 Comm: systemd-shutdow Not tainted 6.6.89-kdev #1
[  692.372823] Hardware name: Rockchip EMB3531 (DT)
[  692.377437] pstate: 60000005 (nZCv daif -PAN -UAO -TCO -DIT -SSBS BTYPE=--)
[  692.384395] pc : mutex_lock+0x44/0x78
[  692.388068] lr : mutex_lock+0x1c/0x78
[  692.391733] sp : ffffffc08336bbd0
[  692.395044] x29: ffffffc08336bbd0 x28: ffffff8000a38000 x27: 0000000000000000
[  692.402182] x26: ffffff8000eab490 x25: ffffffc0822164e0 x24: ffffffc083244028
[  692.409319] x23: 0000000000000001 x22: ffffffc0832f7210 x21: ffffffc08304c0e8
[  692.416455] x20: 0000000000000c85 x19: 0000000000000c85 x18: ffffffffffffffff
[  692.423591] x17: 000000040044ffff x16: 00000032b5593519 x15: 0000000000000000
[  692.430727] x14: ffffff8000b18000 x13: ffffffbffd46f000 x12: 0000000034d4d91d
[  692.437864] x11: 0000000000000040 x10: ffffff8000f7a020 x9 : ffffffc081b2d670
[  692.445001] x8 : ffffff80004f8270 x7 : 0000000000000000 x6 : ffffff8000a38000
[  692.452137] x5 : ffffff8000eab4f4 x4 : 0000000000000000 x3 : 0000000000000003
[  692.459273] x2 : 0000000000000000 x1 : ffffff8000a38000 x0 : 0000000000000000
[  692.466409] Call trace:
[  692.468855]  mutex_lock+0x44/0x78
[  692.472175]  dw_hdmi_suspend+0x28/0xc8
[  692.475928]  dw_hdmi_rockchip_shutdown+0x98/0xb0
[  692.480550]  platform_shutdown+0x28/0x40
[  692.484476]  device_shutdown+0x12c/0x288
[  692.488404]  kernel_restart+0x44/0xc8
[  692.492073]  __do_sys_reboot+0x100/0x228
[  692.495999]  __arm64_sys_reboot+0x28/0x38
[  692.500013]  invoke_syscall+0x4c/0x120
[  692.503766]  el0_svc_common.constprop.0+0x44/0xf0
[  692.508472]  do_el0_svc+0x24/0x38
[  692.511790]  el0_svc+0x24/0xa8
[  692.514850]  el0t_64_sync_handler+0x134/0x150
[  692.519207]  el0t_64_sync+0x160/0x168
[  692.522872] 
[  692.522872] PC: 0xffffffc081b2f264:
[  692.527831] f064  17fffe46 b900181f 97fffa21 17fffe0a aa1603e0 94001b00 17fffe0d aa0103e0
...
[  692.585202] f144  ffffffc0 aa1e03e9 d503201f a9bf7bfd 52800021 910003fd 97fffdaf a8c17bfd
[  692.593397] f164  d65f03c0 81b7be28 ffffffc0 aa1e03e9 d503201f a9be7bfd 910003fd f9000bf3
...
[  697.845925] ack       0x0068: 20400679 00000010 00000000 00007e00
[  697.852024] rockchip-thermal ff260000.tsadc: channal 0: temperature(32 C)
[  697.858808] rockchip-thermal ff260000.tsadc: channal 1: temperature(32 C)
[  697.865589] THERMAL REGS:
[  697.868213] 00000000: 00000200 00010133 00000303 00000000 00000000 00000000 00000000 00000000
[  697.876736] 00000020: 0000020d 0000020d 00000000 00000000 0000022b 0000022b 00000000 00000000
[  697.885257] 00000040: 00000279 00000279 00000000 00000000 00000000 00000000 00000000 00000000
[  697.893779] 00000060: 00000004 00000004 00000753 00000753 00000000 00000000 00000000 00000000
[  697.902295] 00000080: 00000000 00000000
[  697.906127] Kernel Offset: disabled
[  697.909611] CPU features: 0x0,80000208,34020000,1000401b
[  697.914919] Memory Limit: none
[  697.917982] cpu cpu0: cur_freq: 816000000 Hz, volt: 850000 uV
[  697.923725] cpu cpu4: cur_freq: 816000000 Hz, volt: 900000 uV
[  697.929467] ---[ end Kernel panic - not syncing: Attempted to kill init! exitcode=0x0000000b ]---
󾯾ÿ½Ｃ𺱟𼟿#𺱟彾󿿲þþ©þҪKþ~𽌪ºҚÿ:ÿ:ÿ:ÿ8ÿ8ÿ8ÿ¸ÿ:ÿ:ÿ8ÿ¸ÿ8ÿНڝꃲÿҘÿ򺀒¸ÿ󺀲򺀒¢ªJ¢X<º~ຘ±[»»̹K鋊󳚚ÿªÿª󞀌xd󿿹/򸼱¹q#}o࠽½y
                                                                                               ί}񼞻򷐹{𐼾x׹q§򹣥ֺr

U-Boot 2017.09-g0eeeaecc425-dirty (Mar 25 2026 - 01:07:17 +0000)

```

重启会出现空指向异常，根据堆栈，推测在HDMI调用 dw_hdmi_rockchip_shutdown 死锁。重启看看hdmi

* 触发场景：用户执行了 reboot 命令（调用栈显示 __do_sys_reboot -> kernel_restart -> device_shutdown）。
* 崩溃位置：mutex_lock+0x44/0x78。这意味着内核试图获取一个互斥锁（mutex），但无法获得，导致系统挂起或触发看门狗/软死锁检测（虽然这里直接打印了 Call Trace，通常是任务处于不可中断状态或被调试器捕获）。

关键函数：
1. dw_hdmi_suspend: Synopsys DesignWare HDMI 控制器的 suspend 回调函数。
2. dw_hdmi_rockchip_shutdown: Rockchip 平台特定的 HDMI 关闭回调函数。
3. platform_shutdown -> device_shutdown: 系统重启时的标准设备关闭流程。

这是一个经典的 Shutdown/Suspend 路径上的锁竞争或重复加锁 问题

```text
root@armbian:~# dmesg |grep -i hdmi
[   13.638158] Kernel command line: root=PARTUUID=614e0000-0000-4b53-8000-1d28000054a9 rootwait rw console=ttyS2,115200 cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory net.ifnames=0 biosdevname=0 level=10 loglevel=10 selinux=0 crashkernel=384M-:128M systemd.mask=systemd-growfs@-.service rockchip.dmc_freq=528000 video=HDMI-A-1:1920x1080@60
[   15.825427] /vop@ff900000: Fixed dependency cycle(s) with /hdmi@ff940000
[   15.825850] /vop@ff8f0000: Fixed dependency cycle(s) with /hdmi@ff940000
[   15.826126] /hdmi@ff940000: Fixed dependency cycle(s) with /vop@ff8f0000
[   15.826403] /hdmi@ff940000: Fixed dependency cycle(s) with /vop@ff900000
[   24.263014] dwhdmi-rockchip ff940000.hdmi: Detected HDMI TX controller v2.11a with HDCP (DWC HDMI 2.0 TX PHY)
[   24.273866] dwhdmi-rockchip ff940000.hdmi: can't find route
[   24.279778] rockchip-drm display-subsystem: failed to bind ff940000.hdmi (ops 0xffffffc081cbfbf8): -19
[   35.504358] platform hdmi-sound: deferred probe pending

root@armbian:~# cat /sys/kernel/debug/devices_deferred 
hdmi-sound	asoc-simple-card: parse error
mtd_vendor_storage	


```

没有完全适配好，需要调整hdmi

```c
static void dw_hdmi_rockchip_shutdown(struct platform_device *pdev)
{
    struct rockchip_hdmi *hdmi = dev_get_drvdata(&pdev->dev);

    if (!hdmi || !hdmi->drm_dev)
        return;

    if (hdmi->is_hdmi_qp) {
        if (hdmi->hpd_irq)
            disable_irq(hdmi->hpd_irq);
        cancel_delayed_work(&hdmi->work);
        flush_workqueue(hdmi->workqueue);
        dw_hdmi_qp_suspend(hdmi->dev, hdmi->hdmi_qp);
    } else {
        if (hdmi->hpd_gpiod) {
            disable_irq(hdmi->hpd_irq);
            if (hdmi->hpd_wake_en)
                disable_irq_wake(hdmi->hpd_irq);
        }
        dw_hdmi_suspend(hdmi->hdmi);
    }
    pm_runtime_put_sync(&pdev->dev);
}

```

```c
void dw_hdmi_qp_suspend(struct device *dev, struct dw_hdmi_qp *hdmi)
{
    if (!hdmi) {
        dev_warn(dev, "Hdmi has not been initialized\n");
        return;
    }

    mutex_lock(&hdmi->mutex);  // 关键点

    /*
     * When system shutdown, hdmi should be disabled.
     * When system suspend, dw_hdmi_qp_bridge_disable will disable hdmi first.
     * To prevent duplicate operation, we should determine whether hdmi
     * has been disabled.
     */
    if (!hdmi->disabled)
        hdmi->disabled = true;
    mutex_unlock(&hdmi->mutex);

    if (hdmi->avp_irq)
        disable_irq(hdmi->avp_irq);

    if (hdmi->main_irq)
        disable_irq(hdmi->main_irq);

    if (hdmi->earc_irq)
        disable_irq(hdmi->earc_irq);

    pinctrl_pm_select_sleep_state(dev);
    if (!hdmi->next_bridge)
        drm_connector_update_edid_property(&hdmi->connector, NULL);
}
EXPORT_SYMBOL_GPL(dw_hdmi_qp_suspend);
```

这是最可能导致您看到 Crash 的场景：

1.  **背景**：系统正常运行时，HDMI 的热插拔检测工作队列 `hdmi->work` 周期性运行。该工作队列的执行函数（通常是 `rockchip_hdmi_work_func` 或类似名字）在执行时，**必须先获取 `hdmi->mutex`** (或者内部的 `dw_hdmi->mutex`) 来保护共享数据。
2.  **触发重启**：用户执行 `reboot`。
3.  **时序竞争**：
    *   **T1**: `hdmi->work` 被调度运行，成功获取了 `mutex`。
    *   **T2**: `dw_hdmi_rockchip_shutdown` 开始执行。
    *   **T3**: 执行到 `disable_irq(hdmi->hpd_irq)`。注意：`disable_irq` 只会等待**中断上下文**结束，**不会等待 Workqueue** (`hdmi->work`) 结束。如果 `hdmi->work` 是由定时器或延迟工作触发的，它此时仍在运行并持有锁。
    *   **T4**: `disable_irq` 返回（因为中断已禁用且无中断在处理）。
    *   **T5**: 立即调用 `dw_hdmi_suspend(hdmi->hdmi)`。
    *   **T6**: `dw_hdmi_suspend` 尝试 `mutex_lock(&hdmi->mutex)`。
    *   **死锁发生**：
        *   `dw_hdmi_suspend` (主线程) 等待 `mutex` 释放。
        *   `hdmi->work` (后台线程) 持有 `mutex`，正在执行。
        *   **关键点**：`hdmi->work` 在执行过程中，可能需要访问某些硬件资源（如 I2C 总线、PHY 寄存器）。然而，在 `shutdown` 流程中，其他子系统（如 I2C 控制器、时钟门控）可能已经开始关闭或进入不可用状态。
        *   结果：`hdmi->work` 在持有锁的情况下，因为访问已关闭的硬件而**卡死**（例如在 I2C 读写处无限等待，或者触发异常但未崩溃只是挂起）。
        *   主线程 `dw_hdmi_suspend` 永远拿不到锁，系统看门狗超时或打印 Call Trace 后挂死。


```text
[   24.273866] dwhdmi-rockchip ff940000.hdmi: can't find route
[   24.290116] rockchip-drm display-subsystem: failed to bind ff940000.hdmi (ops 0xffffffc081cbfbf8): -19
```

*   **`can't find route`**: 这是 Rockchip DRM 驱动特有的错误。意味着 HDMI 驱动在尝试建立从 **VOP (Video Output Processor)** 到 **HDMI Controller** 再到 **Connector (显示器)** 的图形显示链路（CRTC -> Encoder -> Connector）时失败了。
*   **`failed to bind ... : -19`**: 错误码 `-19` 对应 `ENODEV` (No such device)。因为找不到路由，HDMI 驱动拒绝绑定到 DRM 子系统。
*   **后果**:
    1.  `rockchip-drm` 子系统认为 HDMI 设备绑定失败。
    2.  HDMI 驱动虽然探测到了硬件 (`Detected HDMI TX controller`)，但因为绑定失败，它的初始化流程中断，处于**“半残”状态**。
    3.  依赖 HDMI 音频的 `hdmi-sound` 因为找不到后端，被放入 `devices_deferred`。
    4.  **最关键点**：虽然绑定失败，但平台驱动 (`platform_driver`) 的 `probe` 可能已经部分执行（分配了内存、初始化了 mutex、注册了部分回调），导致在 `reboot` 时，内核依然会调用它的 `shutdown` 回调，从而进入**死锁陷阱**。

通常是 **设备树 (DTS)** 配置问题。Rockchip 的 DRM 驱动依赖设备树中的 `ports` 和 `endpoint` 节点来自动构建显示链路。如果链路断开或方向错误，就会报这个错。

常见原因：
1.  **Endpoint 连接不匹配**：VOP 的输出端点 (`remote-endpoint`) 没有正确指向 HDMI 的输入端点，或者反之。
2.  **Port 节点缺失或错误**：HDMI 节点下缺少 `ports` 子节点，或者 `reg` 属性配置错误。
3.  **VOP 未启用或配置错误**：对应的 VOP 节点（如 `vop_lit` 或 `vop_big`）没有正确配置输出到 HDMI。
4.  **循环依赖修复副作用**：日志开头显示 `Fixed dependency cycle(s)`。虽然内核尝试修复循环依赖，但这有时意味着设备树的图结构本身画得不对，导致驱动在解析拓扑时迷路。







