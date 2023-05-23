---
title: "OLAP vs OLTP"
datePublished: Mon Jan 23 2023 16:20:21 GMT+0000 (Coordinated Universal Time)
cuid: cld90lmof00000ajygo8c4lqi
slug: olap-vs-oltp
tags: system-design, arabic, oltp

---

‫ الOLTP او Online Transaction Processing ده نوع من الداتا اللي بيمثل الtransaction عمله الcustomer زي لما بنشتري حاجة من أمازون أو لما بنحجز تذاكر طيران او لما بنبعت رسالة

‫ من الخصائص المهمة ف الOLTP هي الConcurrency (يقدر ي support كذا transaction في نفس الوقت) و الAtomicity (يعني يا الtransaction كله على بعضه ينجح يا كله على بعضه يفشل)

لما بنحول فلوس لحد و التحويل بيفشل .. مفيش فلوس بتوصل للشخص المستقبل .. مينفعش يوصله نص الفلوس و نص لأ

‫ جزئية الconcurrency بتسمح ان اكتر من read operation تحصل في نفس الوقت لكن بتسمح ب write operation واحدة تحصل عشان الداتا تفضل consistent .. عشان نقول على OLTP transaction انه complete لازم الrecord يبقى permenant و بنسميه Atomic statefulness

‫ و عشان نتجنب الsingle point of failure الOLTP database servers بيبقوا decentralized و متوزعين على كذا مكان .. ده طبعًا بيخلق مشاكل في الdata consistency بسبب الdistributed databases بس ممكن نتكلم عنها في مثتاني

‫

![](https://techcapsuleinarabic.files.wordpress.com/2022/08/image.png?w=500 align="left")

نوع الداتابيز اللي بيتم استعماله ف الOLTP بيبقى Relational Database و ده منطقي عشان هما معروفين انهم كويسين لل frequent writes/update + الindexation و الhigh availability عشان لو داتابيز وقعت واحنا في بنك ف حنزعل و حنجيب ناس تزعل

‫ الOLAP او Online Analytical Processing يعتبر category من الsoftware tools عشان يساعد في الanalysis و الBusiness intelligence و الفرق الصريح بينها و بين الOLTP انها مختصة بالdata analysis مش الtransaction processing

‫ الinsights اللي ممكن نحققها من الOLAP هي اللي بتحدد الstrategy بتاعة الشركة.

‫

‫ الموضوع بيبتدي من تجميع الداتا .. بسبب اننا عندنا كذا داتا من كذا مصدر ف محتاجين نحطهم في مكان واحد اللي هو datawarehouse

‫ مهمته بتبقى يintegrate مع كذا data source (سواء sql او nosql)

![](https://techcapsuleinarabic.files.wordpress.com/2022/08/image-1.png?w=1000 align="left")

‫ بعدين ي merge الداتا دي ل common data model .. ده بنسميه ETL او Extract Transform-Load و بعتبر حجر أساس للdata strategy في الخمسين سنة اللي فاتوا.

‫ أمثلة على الOLAP:عدد الcustomers من الرجالة و الستات, زيادة البيع لمنتج معين في فترة معينة .. الapp usage بعد ما جربنا UI جديد ..الخ

‫ الOLAP مبتعدلش في الداتا لكن بتعمل داتا جديدة من خلال الداتا الموجودة .. و لأنها الcentralized datawarehouse لكل الداتا الموجودة ف الstorage بيحتاج يبقى أكتر من الOLTP و مفيش مشاكل يبقى بطيء طالما هو realiable

‫ بالإضافة لده ف الqueries بتاعته أعقد بكتير عن الOLTP عشان بنحاول نغوص في كذا column من كذا table من كذا database أصلًا .. عكس الOLTP اللي الqueries بتاعته عبارة عن Create, Update, Delete

‫ دي أول مرة أكتب في الData engineering ف ياريت لو في حاجة غلط قلتها حد يصلحلي و لو مهتمين أكتب عن الdatawarehouse, data lake, database, data lakehouse

https://www.techtarget.com/searchdatacenter/definition/OLTP https://www.guru99.com/oltp-vs-olap.html https://www.oracle.com/database/what-is-oltp/#:~:text=What%20is%20OLTP%3F-,OLTP%20defined,sending%20text%20messages%2C%20for%20example https://www.zuar.com/blog/etl-vs-elt-whats-the-difference/ https://galaktika-soft.com/blog/oltp-and-olap-difference.html https://www.ibm.com/cloud/learn/oltp ‫

‫

‫

‫

‫

‫

‫

‫

‫