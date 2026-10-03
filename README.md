# tari5 — خدمة استعلام التاريخ

99 كتاباً من كتب التاريخ مقطعة عند حدود فهارسها الأصلية — استعلام بثلاثة طلبات، بلا تحميل ولا مفاتيح:

```
١) كل الكتب المتوفرة:        GET  /api/index.json
٢) فهرس الكتاب المختار:      GET  /api/books/<id>/toc.json
٣) محتوى العنوان المختار:    GET  /api/books/<id>/parts/<NNNN>.json.gz
```

مثال — فهرس كتاب (بدّل <id> برقم الكتاب من index.json):
```
curl -s https://medmrf-10.github.io/tari5/api/books/<id>/toc.json
# ← {id, title, author, toc:[{i,t,d,pg}…]}  i=رقم الجزء، t=العنوان، d=العمق، pg=صفحة المصدر
```

ثم نص أي عنوان:
```
curl -s https://medmrf-10.github.io/tari5/api/books/<id>/parts/0005.json.gz | gunzip
# ← {i,t,pg,b,text}
```

حقل `b` = دقة حدود الجزء: `m` علامة فهرس داخلية في المصدر، `t` حُدّد بمطابقة نص العنوان في صفحته، `a` تقريبي عند بداية صفحة العنوان.

المصدر: shamelaPure (shamela.ws) — التقسيم عند فهارس المؤلفين أنفسهم.
