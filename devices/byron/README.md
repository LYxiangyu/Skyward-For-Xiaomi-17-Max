# Xiaomi 17 Max (`byron`) recovery helper

[English](#english) | [简体中文](#简体中文)

## English

### Purpose

The byron stock firmware provides the QTI Secure Element HAL and the NXP
Weaver HAL, but its recovery and mounted system do not provide a native OMAPI
service that can run without Android Framework. The NXP Weaver HAL needs the
Binder service below before it can read its secure-element slots:

```text
android.se.omapi.ISecureElementService/default
```

`se_omapi` supplies that service in recovery. It sits between the official QTI
Secure Element HAL and the official NXP Weaver HAL. It does not contain a
phone's keys or secure-element state.

### Exact provenance

The prebuilt `se_omapi` in this directory was copied unchanged from the public
Xiaomi 17-series TWRP device-tree repository maintained by
[`antocorvo3000`](https://github.com/antocorvo3000):

- Repository: [`antocorvo3000/twrp-xiaomi-17-series`](https://github.com/antocorvo3000/twrp-xiaomi-17-series)
- Commit: [`4a35185d43782b4dd460a7f456d674c0976c0859`](https://github.com/antocorvo3000/twrp-xiaomi-17-series/commit/4a35185d43782b4dd460a7f456d674c0976c0859)
- Original path: [`twrp_device_xiaomi_popsicle/recovery/root/system/bin/se_omapi`](https://github.com/antocorvo3000/twrp-xiaomi-17-series/blob/4a35185d43782b4dd460a7f456d674c0976c0859/twrp_device_xiaomi_popsicle/recovery/root/system/bin/se_omapi)
- SHA-256:
  `12da3e4c9d3e584182a282bcfa9cf7422d3a4650c5b2fd05896a5db5dc715108`

The local file, the file at that fixed commit and the source repository's
`ramdisk-files.sha256sum` all have the same SHA-256.

### Verification boundary

This file is a stripped, prebuilt Android AArch64 ELF targeting Android API 36
and using the OMAPI V1 NDK interface. It was **not** extracted from Xiaomi's
official byron OTA, and this project did **not** build it from AOSP source. The
source repository records the binary and its hash, but does not provide a
reproducible build recipe that proves which exact source produced it.

Do not describe this prebuilt as a Xiaomi-official binary or as a verified
AOSP Android 17 build. Its functionality has been verified on a Xiaomi 17 Max
running OS4.0.3.0.XAFCNXM: NXP Weaver starts and Skyward can decrypt data. That
functional result is not a source audit or a reproducibility guarantee.

Inspection of the official byron OS4.0.3.0 OTA found the official QTI Secure
Element HAL, NXP Weaver HAL and Java `SecureElement.apk`, but no native
`omapi`/`se_omapi` executable. The Java service requires Android Framework and
cannot be started directly in this recovery.

### Acknowledgement

Thanks to **antocorvo3000** and the contributors to
[`twrp-xiaomi-17-series`](https://github.com/antocorvo3000/twrp-xiaomi-17-series)
for publishing the Xiaomi 17-series recovery research, device trees and the
Popsicle recovery files that made this compatibility work possible. This
acknowledgement identifies the immediate file source; it is not a claim of
endorsement, warranty or upstream authorship of the prebuilt.

## 简体中文

### 用途

byron 原厂固件提供 QTI Secure Element HAL 和 NXP Weaver HAL，但原厂 recovery
及挂载后的系统中没有一个能脱离 Android Framework 运行的原生 OMAPI 服务。
NXP Weaver HAL 读取安全芯片槽位之前，需要以下 Binder 服务：

```text
android.se.omapi.ISecureElementService/default
```

`se_omapi` 在 recovery 中提供这个服务，位于官方 QTI Secure Element HAL 与
官方 NXP Weaver HAL 之间。该文件本身不包含任何手机的密钥或安全芯片状态。

### 确切来源

本目录中的预编译 `se_omapi` 未经修改地取自
[`antocorvo3000`](https://github.com/antocorvo3000) 维护的公开 Xiaomi 17
系列 TWRP 设备树仓库：

- 仓库：[`antocorvo3000/twrp-xiaomi-17-series`](https://github.com/antocorvo3000/twrp-xiaomi-17-series)
- 固定提交：[`4a35185d43782b4dd460a7f456d674c0976c0859`](https://github.com/antocorvo3000/twrp-xiaomi-17-series/commit/4a35185d43782b4dd460a7f456d674c0976c0859)
- 原始路径：[`twrp_device_xiaomi_popsicle/recovery/root/system/bin/se_omapi`](https://github.com/antocorvo3000/twrp-xiaomi-17-series/blob/4a35185d43782b4dd460a7f456d674c0976c0859/twrp_device_xiaomi_popsicle/recovery/root/system/bin/se_omapi)
- SHA-256：
  `12da3e4c9d3e584182a282bcfa9cf7422d3a4650c5b2fd05896a5db5dc715108`

本地文件、上述固定提交中的文件，以及来源仓库
`ramdisk-files.sha256sum` 记录的 SHA-256 完全一致。

### 致谢

感谢 **antocorvo3000** 以及
[`twrp-xiaomi-17-series`](https://github.com/antocorvo3000/twrp-xiaomi-17-series)
的贡献者公开 Xiaomi 17 系列 recovery 研究、设备树和 Popsicle recovery 文件，
使本次兼容工作成为可能。
