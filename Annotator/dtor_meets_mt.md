---
annotation-target:: http://files.cppblog.com/Solstice/dtor_meets_mt.pdf
---

>%%
>```annotation-json
>{"created":"2023-02-26T14:34:01.228Z","updated":"2023-02-26T14:34:01.228Z","document":{"title":"当析构函数遇到多线程","link":[{"href":"urn:x-pdf:1b2af0c61dee688eca811ef99e075346"},{"href":"http://files.cppblog.com/Solstice/dtor_meets_mt.pdf"}],"documentFingerprint":"1b2af0c61dee688eca811ef99e075346"},"uri":"http://files.cppblog.com/Solstice/dtor_meets_mt.pdf","target":[{"source":"http://files.cppblog.com/Solstice/dtor_meets_mt.pdf","selector":[{"type":"TextPositionSelector","start":18049,"end":18163},{"type":"TextQuoteSelector","exact":"C + + 里可能 出现的内存 问题大致有 这么几个方 面：1 . 缓冲区 溢出2 . 空悬指 针 / 野指针3 . 重复释 放4 . 内存泄 漏5 . 不配对 的 n e w [ ] / d e l e t e6 . 内存碎 ","prefix":"儿，自己写的C + + 程序从来没 有出现过内 存方面的问 题。","suffix":"片正确使 用 智 能 指针 能 很 轻 易地 解 决 前 面 5"}]}]}
>```
>%%
>*%%PREFIX%%儿，自己写的C + + 程序从来没 有出现过内 存方面的问 题。%%HIGHLIGHT%% ==C + + 里可能 出现的内存 问题大致有 这么几个方 面：1 . 缓冲区 溢出2 . 空悬指 针 / 野指针3 . 重复释 放4 . 内存泄 漏5 . 不配对 的 n e w [ ] / d e l e t e6 . 内存碎== %%POSTFIX%%片正确使 用 智 能 指针 能 很 轻 易地 解 决 前 面 5*
>%%LINK%%[[#^g00i5hnssz|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^g00i5hnssz
