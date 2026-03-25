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



重启会出现空指向异常，根据堆栈，推测在HDMI调用 dw_hdmi_rockchip_shutdown 死锁







