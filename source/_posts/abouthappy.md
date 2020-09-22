---
title: 初步使用alex与happy进行语法分析
date: 2020-09-12 10:30:47
tags:
- haskell
category:
- Program
- 编程
---

# alex + happy 初步使用
### 使用alex进行词法分析获取token流 [alex文档](https://www.haskell.org/alex/doc/html/index.html)

1. 这里有个简单的例子,后缀为x

{% codeblock lang:haskell %}
{
module Lexer(lexer,Token(..)) where
}
%wrapper "basic"
$digit = [0-9]
$alpha = [a-zA-Z]

tokens :-
    $white+ ;
    let {\s -> TokenLet}
    in  {\s -> TokenIn}
    =   {\s -> TokenEq}
    \+   {\s -> TokenPlus}
    \-   {\s -> TokenMinus}
    \*   {\s -> TokenTimes}
    \/   {\s -> TokenDiv}
    \(   {\s -> TokenOB}
    \)   {\s -> TokenCB}
    $digit+ {\s -> TokenInt (read s)}
    $alpha+ {\s -> TokenVar s}
{
data Token
    = TokenLet
    | TokenIn
    | TokenInt Int
    | TokenVar String
    | TokenEq
    | TokenPlus
    | TokenMinus
    | TokenTimes
    | TokenDiv
    | TokenOB
    | TokenCB
 deriving(Show,Eq)

lexer :: String -> [Token]
lexer = alexScanTokens
}

{% endcodeblock %}

2. 导出的lexer ::String->[Token] 将字符串处理为Token流

### 使用happy进行语法分析生成AST[happy 文档](https://www.haskell.org/happy/doc/html/index.html)

1. 例子，后缀为y

{% codeblock lang:haskell %}
{
module Parser(parse,Exp(..),Exp1(..),Term(..),Factor(..)) where
import Lexer
}
%name parse
%tokentype {Token}
%error {parseError}
%token
    let {TokenLet}
    in  {TokenIn}
    int {TokenInt $$}
    var {TokenVar $$}
    '=' {TokenEq}
    '+' {TokenPlus}
    '-' {TokenMinus}
    '*' {TokenTimes}
    '/' {TokenDiv}
    '(' {TokenOB}
    ')' {TokenCB}
%%
Exp   : let var '=' Exp in Exp  { Let $2 $4 $6 }
      | Exp1                    { Exp1 $1 }

Exp1  : Exp1 '+' Term           { Plus $1 $3 }
      | Exp1 '-' Term           { Minus $1 $3 }
      | Term                    { Term $1 }

Term  : Term '*' Factor         { Times $1 $3 }
      | Term '/' Factor         { Div $1 $3 }
      | Factor                  { Factor $1 }

Factor			  
      : int                     { Int $1 }
      | var                     { Var $1 }
      | '(' Exp ')'             { Brack $2 }
{
parseError :: [Token] -> a
parseError _ = error "Parse error"

data Exp  
      = Let String Exp Exp
      | Exp1 Exp1
      deriving Show

data Exp1 
      = Plus Exp1 Term 
      | Minus Exp1 Term 
      | Term Term
      deriving Show

data Term 
      = Times Term Factor 
      | Div Term Factor 
      | Factor Factor
      deriving Show

data Factor 
      = Int Int 
      | Var String 
      | Brack Exp
      deriving Show
}

{% endcodeblock %}


2. 导出的parse ::[Token]->Exp 将Token流处理为AST

### 将lexer,parse 复合即可构成String->Exp的函数

![](/images/alex_happy.png)

###### 链接测试: [学过的语言](../../public/2019/06/12/program-language/index.html)
