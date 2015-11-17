tornado
===

把特殊字符替换为空格。
safe_value = re.sub(r"[\x00-\x1f]", " ", value)[:4000]

@classmethod 可以直接通过类调用,且第一个参数不用写self.而普通的类中函数第一个参数要写self,调用的时候要通过类的实例来调用。
