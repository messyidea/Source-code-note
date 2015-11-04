tornado
===

把特殊字符替换为空格。
safe_value = re.sub(r"[\x00-\x1f]", " ", value)[:4000]
