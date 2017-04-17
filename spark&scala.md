---
typora-copy-images-to: ./images
---

## 算子

#### reduce by key vs group by key

最主要的区别如图，group by key 会先进行shuffle，再合并。 reducebykey 是先在本地合并，在 shuffle 再合并。如下图:

![275EE443-8854-42CB-BDDC-5BD15CC85D23](images/275EE443-8854-42CB-BDDC-5BD15CC85D23.png)![26DB36C4-ACC7-4823-A7AF-D6770EB4835D](images/26DB36C4-ACC7-4823-A7AF-D6770EB4835D.png)





## scala

拼接dataframe。

```
rsDFs.reduce(_ union _)
```

