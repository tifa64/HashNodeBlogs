---
title: "ِBig Dataتطور ال : Apache Spark من مكتبة الإسكندرية إلى ال"
datePublished: Sat Sep 09 2023 17:41:51 GMT+0000 (Coordinated Universal Time)
cuid: clmcbcj4n000209ig7wl68qcr
slug: big-datattor-al-apache-spark-mn-mktba-aliskndrya-il-al
tags: techcapsuleinarabic

---

# ‫ البداية

‫ بدأ تاريخ الBig Data من وجهة نظري وقت مكتبة الإسكندرية القديمة لما دعى (بلطيموس الأول) كتّاب و مؤرخين العالم يجوا يعيشوا ف إسكندرية على حسابه و بعدها فرض (بطليموس الثالث) سياسة ان أي سفينة تيجي عند ميناء إسكندرية يسلموا كل المخطوطات و الكتب للمكتبة ينسخوها و المكتبة تحتفظ بالأصل.

![صورة تصورية عن شكل مكتبة الإسكندرية القديمة https://greekreporter.com/2023/07/05/library-of-alexandria/](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280017342/0bde4bab-ee17-4bfd-ab04-ab87b1c3fc30.png align="center")

‫ الموضوع وصل ان عين ناس تلف دول البحر الأبيض المتوسط تشوف مخطوطات و كتب و أي عمل أدبي و ينسخوه للمكتبة و منع تصدير ورق البردي لبرة عشان الناس تضطر تيجي مصر و تكتب. لأول مرة في التاريخ كان فيه indexation او فهرسة للكم ده من المعلومات في مكان واحد.

![صورة تخيلية للمخطوطات داخل مكتبة الإسكندرية القديمة https://www.youtube.com/watch?v=jvWncVbXfJ0&ab_channel=TED-Ed](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280049955/c40ef6db-4dae-4b7b-aa62-5d0e44e97821.png align="center")

‫ و دي المشكلة اللي لقت جوجل نفسها في مطلع القرن الجديد انهم عايزين يفهرسوا كل المقالات و المدونات عالنت .. ف إخترعوا كذا حاجة زي

# Indexation of WWW

* Google File System (GFS): ‫ و ده distributed system شغال على كذا cluster
    
* Bigtable: ‫ و ده scalable store بيستعمل الGFS
    

## MapReduce

* MapReduce: ‫ و دهparallel data processing technique ‫ لو عندك طبق كشري .. عايز تعد فيه كام حباية رز و عدس و حمص بدل ما تعد البقوليات دي serially .. حتدي كذا معلقة كشري لكل شخص من صحابك .. كل واحد فيهم حيcalculate الرز و بعدين ي report ليك.
    

![Architecture of Google File System  https://en.wikipedia.org/wiki/Google_File_System#/media/File:GoogleFileSystemGFS.svg](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280078895/51d645c0-329c-41da-b2b8-7734ddc15899.png align="center")

‫ حتقوم واخد كل واحد فيهم عد كام حباية رز و كام عدس و إلخ .. و بعدين تقوم مقسم كل واحد فيهم per بقولية .. صاحب حيبقى مسئول عن تجميع عدد الرز .. صاحب حيبقى مسئول عن تجميع عدد الحمص .. و هكذا ‫ صحابك لما عدوا الكشري و هو متلخبط كانوا Mappers معلقة الرز هي fraction of data.

![How MapReduce work  https://www.edupristine.com/blog/hadoop-mapreduce-framework](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280189300/1464d29f-1060-4dc4-b818-d35ebe285cbc.png align="center")

‫

و هما بيعدوا البقوليات ده الMapper job لما قسمتهم per بقولية دي اسمها shuffling لما كل واحد جمع total number of رز و عدس و حمص ده reduce. ‫ الMapeReduce أول ما إخترع كان شغال بengine اسمه Apache Hadoop و جوجل برضه هي اللي كانت مخترعاه بس مكنتش عاملاه open source

![غبي منه فيه مشهد "لو قدامك طبق كشري"](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280120359/67a06f81-63f0-435b-b7ae-93f8be6db467.png align="center")

‫ لكنها نشرت الأبحاث اللي اتكتبت و اللي أدت للMapeReduce و الHDFS او Hadoop Distributed File System .. بعدها المهندسين ف Yahoo كتبوا كود بناءًا على الأوراق البحثية دي و حطوه كopen source بالApache License. ‫ المشكلة بتاعة MapReduce انه بطيء عشان كل stage بيread و يwrite للdisk

## ‫Disk Vs RAM

![MapReduce Jobs Educative.io](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280223870/ae78f539-c12d-4762-b799-b7cf68c74196.png align="center")

‫ الHard disk أبطىء من الRAM عشان هو معمول من magentic material و الarm بياخد وقت عقبال ما يلاقي الdata اللي عالdisk فيما حين ان الRAM معمول من transistors و semi conductors ف الsignlas بتاخد وقت أسرع

![Hard Disk https://www.britannica.com/technology/hard-disk](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280429451/9cea50fc-e48d-4a57-85b4-6ea822b02bae.png align="center")

![RAM clipart https://favpng.com/png_view/ram-ram-computer-memory-computer-hardware-clip-art-png/BYieH7BP](https://img.favpng.com/3/20/2/ram-computer-memory-computer-hardware-clip-art-png-favpng-zh3xWA2ug2DUeEARm5nz1Knt2.jpg align="left")

‫ موضوع بطىء الMapReduce ده واحد اسمه Matei Zaharia في جامعة UC Berkeley لاحظه و كتب بحث عن enginer جديد اسمه Spark بيستعمل الMemory بدلاً من الhard disk و إتكلم ان فيه 3 حاجات MapReduce paradigm مش بيدعمها كويس و Spark أحسن منه فيها:

![MapReduce processing VS Spark Processing Educative.io](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280517905/d5356b94-4ec5-407e-a48a-bea8de9f0068.png align="center")

## ‫محدوديات MapReduce

1. Iterative Jobs: ‫ في حالة الMachine learning ف الalgorithms بتعدي كذا مرة على الداتا و بتضطر تread من الhard disk كل مرة و ده مكلف في الوقت.
    
2. Interactive Analysis: ‫ لو بتعمل كذا SQL queries على dataset حجمها كبير عشان تعمل analysis ليها ف الlatency حتبقى عالية.
    
3. Rich APIs: ‫ في الMapReduce بتضطر تكتب boilerplate code كبير عشان تبتدي تستعمله فيما حين ان الSpark بيقدم APIs حتinvoke it و خلاص ‫
    

بيحلها Spark ال Use Cases كمان طرح

1. Parallel processing of large data sets across clusters.
    
2. Analyzing large data sets: ‫ و ده بيبقى مطلوب من اول الe-commerce لحد الsocial network products
    
3. Building, training, and evaluating machine learning models.
    
4. Creating data pipelines ‫ بغض النظر عن ايه الdata source
    

![Spark Buidling Block Educative.io](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280552407/172ff877-5768-4733-9fd3-3dc344d26ddf.png align="center")

‫ الdata structure اللي من خلالها اي data بيتم تمثيلها في Spark اسمها RDD او Resilient Distributed Datasets ‫ بتبقى immutable و ممكن تتقسم على كذا cluster و تشتغل in paraller و لو cluster وقع ف ممكن يتعملها re-construction.

## Architecture of Spark

Spark ‫ عنده نفس نظامmaster-slave architecture زي MapReduce بحيث ان الmaster هو اللي بينظم الdistributed work و الslave هو اللي بيprocess

‫ اسم الmaster هو Driver مهمته يقرا الcode من الuser بعدين يحوله ل Directed Acyclic Graph او DAG عشان ي optimize و يعرف انهي step تبقى قبل نهون

‫ بعد كده بيدي الorders للslaves و اسم الslave ف Spark هو Executor ‫ الExecutor بياخد الcode من الDriver و بيreport الstate بتاعة الcomputation بتاعتها و مهمة الDriver انه يkeep track من شغل كل Executor

![Drivers and Executors Educative.io](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280586845/d38093de-9eae-48c7-a656-0558f8018788.png align="center")

‫ آخر component ف Spark هو Cluster manager .. سواء شغال MapReduce او Spark ف الjobs بتبقى شغالm على cluster of machines .. الDriver بتاع Spark ميقدرش يallocate resources من الcluster ف بيبقى فيه Cluster manager لده ‫ الDriver بعد كده بيتفاوض مع الCluster manager و يوفرهم للExecutors

### ‫ من أمثلة الCluster Managers ‫

* Local mode: ‫ ده لو عايزة تجربي على الكومبيوتر حجك
    
* Built-in standalone cluster manager: ‫ لو شركتك بانية Cluster Manager بنفسها او شغالة on premise
    
* Hadoop YARN
    
* Kubernetes
    
* Apache Mesos
    

‫ لو حنراجع على ال الApplication Lifecycle بتاعة الSpark job فهي كالتالي: ‫ ك user بتsubmit ال spark job لل cluster manager و بيقول للDriver اصحى عندك طلعة. ‫ في الوقت ده الCluster Manager بيspawn كذا Executor nodes و بيرجع الlocations بتوعهم للDriver عشان يعرف يكلمهم.

‫ بعدها الDriver بيحول الcode لDAG و يقول لكل Executor Node ت execute ايه و يعرف الstatus ‫ أخيرًا لما كل Spark Job بتخلص الCluster manager بيshutdown كل Executor node بالنيابة عن الdriver

‫

![Pipeline of Spark Educative.io](https://cdn.hashnode.com/res/hashnode/image/upload/v1694280650018/7f08c098-afd2-4d76-8b0c-15eb8ecd7a1f.png align="center")

‫

‫

‫و بس كده يا قمامير أتمنى تكونوا إستفدتم و لو قلت معلومة خاطئة حبقى مبسوط لو حد صصحهالي

Hope you found this useful 😊

## المصادر:

[https://www.youtube.com/watch?v=jvWncVbXfJ0&ab\_channel=TED-Ed](https://www.youtube.com/watch?v=jvWncVbXfJ0&ab_channel=TED-Ed)

[https://spark.apache.org/](https://spark.apache.org/)

[https://www.educative.io/courses/introduction-to-spark](https://www.educative.io/courses/introduction-to-spark)

[https://medium.com/@bharvi.vyas123/6-major-hadoop-limitations-with-their-solutions-1cae1d3936e1#:~:text=In%20Hadoop%2C%20the%20MapReduce%20reads,it%20is%20very%20slow%20comparatively](https://medium.com/@bharvi.vyas123/6-major-hadoop-limitations-with-their-solutions-1cae1d3936e1#:~:text=In%20Hadoop%2C%20the%20MapReduce%20reads,it%20is%20very%20slow%20comparatively)

[https://www.edupristine.com/blog/hadoop-mapreduce-framework](https://www.edupristine.com/blog/hadoop-mapreduce-framework)

[https://en.wikipedia.org/wiki/Matei\_Zaharia](https://en.wikipedia.org/wiki/Matei_Zaharia)

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫

‫