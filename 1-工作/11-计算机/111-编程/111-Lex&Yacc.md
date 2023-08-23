# Lex & Yacc


## 杂项
### 为什么要匹配 `.`
Lex 对没有匹配到的字符会原样输出，所以如果想要忽略未匹配的字符，就要加 `.` 匹配并不做操作

注意这里是 `.` 而不是 `.*`，这样在过滤不想要的字符时只会一个字符一个字符忽略，否则就会把想要的覆盖掉

注：所以写规则的时候，要注意不要出现空匹配

### 匹配规则
对于输入字符串，首先进行最长匹配：一直匹配，直到没有规则接受字符串，此时按匹配长度最长的规则来；如果多个规则匹配长度相同，则按其中最上面的规则来

例如，对于匹配自然数和小数的两种规则：
```lex
([1-9]+[0-9]*)|[0]	ECHO;
[0-9]+\.[0-9]+
```
当匹配 `0.45` 时，由于规则 2 匹配的长度更长，最终做的操作是按规则 2 的来

### Yacc 的 Midrule
```yacc
FuncDef
    : VOID IDENT '(' ')' {globalSymbolTable.AddFuncSymbol(*$2, 0);} Block {
        auto ast = new FuncDefAST();
        ast->funcType = 0;
        ast->ident = *unique_ptr<string>($2);
        ast->funcFParams = nullptr;
        ast->block = unique_ptr<BaseAST>($6); // 注意 Block 是 $6，因为 Midrule 也占一个返回值

        isGlobal = true;
        
        $$ = ast;
    }
```
