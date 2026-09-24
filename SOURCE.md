# 来源与维护说明

## 原始材料

- 来源文件：用户提供的 `long-horizon-task.zip`。
- 归档日期：2026-09-24。
- 原始内容：`SKILL.md`、两份参考文档和四份模板，共 7 个文件。
- 原作者、上游仓库及许可证：原始材料中未提供，尚未确认。

仓库所有者负责这份副本的存放与维护；仓库所有权本身不构成原始内容的作者证明。本仓库当前未添加 `LICENSE`。

## 本次整理

原始技能内容按字节保留，只增加以下仓库文件：

- `README.md`：用途、安装方法、调用示例与目录导航。
- `SOURCE.md`：来源与维护说明。
- `source-manifest.json`：源压缩包及原始文件的 SHA-256 校验信息。
- `.gitignore`：忽略系统元数据、压缩包、环境文件与运行产物。

压缩包中的 `__MACOSX/` 元数据未导入。本仓库不包含用户的实际任务数据、会话历史或登录凭据。

## 完整性校验

在仓库根目录执行：

```bash
python3 - <<'PY'
import hashlib
import json
from pathlib import Path

manifest = json.loads(Path("source-manifest.json").read_text())
for item in manifest["files"]:
    data = Path(item["path"]).read_bytes()
    if len(data) != item["bytes"]:
        raise SystemExit("文件大小不一致：" + item["path"])
    if hashlib.sha256(data).hexdigest() != item["sha256"]:
        raise SystemExit("校验失败：" + item["path"])
print("原始 7 个文件均与导入版本一致。")
PY
```

后续若修改技能内容，请在 Git 提交中说明原因。`source-manifest.json` 保留本次导入基线；只有重新引入明确的新来源版本时才更新该基线。
