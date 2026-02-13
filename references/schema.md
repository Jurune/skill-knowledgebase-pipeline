# Metadata Schema Reference

## Feature Record

```json
{
  "id": "feature_F0-01",
  "code": "F0-01",
  "title": "登录",
  "journey": "旅程 0：进入与身份",
  "feature": {
    "summary": "登录",
    "entry": "登录页",
    "details": ["输入账号/密码"]
  },
  "field": ["username", "password"],
  "rule": ["账号/密码必填"],
  "requirement": ["进入系统需要身份验证"],
  "experience_note": [],
  "artifacts": ["sidepanel/pages/Login.jsx"],
  "field_kind_map": {
    "messageNode": "selector"
  }
}
```

## Top-Level Document

```json
{
  "schema_version": "1.0.0",
  "source": "project",
  "features": []
}
```

## Classification Rule

- Use `field` for runtime mutable state.
- Use `artifacts` for files, build outputs, configs, static resources.
- Keep selectors in `field` only when they drive runtime behavior; set `field_kind_map[key] = "selector"`.
