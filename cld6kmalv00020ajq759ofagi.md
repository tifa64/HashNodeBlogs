---
title: "API Rate Limiter"
datePublished: Sat Jan 21 2023 23:17:25 GMT+0000 (Coordinated Universal Time)
cuid: cld6kmalv00020ajq759ofagi
slug: api-rate-limiter
tags: system-design, api-limiter

---

‫ في الNetwork system بيبقى فيه حاجة اسمها API Rate Limiter و ده بيبقى موجود عشان يتحكم في عدد الrequests اللي طالعة من الclient في فترة معينة و لو عدد الrequests زاد ف بيتعملهم block و الrequest مش حيعدي

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342369081/b210eebb-b081-4ad1-9778-99356baf5a1a.png align="center")

## ‫ فوايد الRate limiter حاجتين:

‫ 1- بيمنع الDenial of Service (DoS) attack .. تقريبًا كل الAPIs بتاعة الشركات الكبيرة بتبقى محمية ب rate limiter عشان تبقى شغالة .. على سبيل المثال تويتر بيlimit عدد التويتات بحيث متعديش 300 تويتة في 3 ساعات و Google docs بيمنع أكتر من users 300 يعملوا Read requests في خلال دقيقة.

‫ 2- السبب التاني و هو الفلوس و تقليل الcost .. زي chatGPT لما بدأ يبطأ أو يقلل من الrequests عشان الrequest بتاعه مكلّف انه ي process السؤال و يجاوب و كل دي servers بتتأجر بفلوس يمكن توفيرها.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342382487/f66a29d7-5839-47d3-98e7-280a58f6ba8e.png align="center")

## Assumptions

‫ 1- لو حنعمل system design ل api rate limiter ف محتاجين نحط assumptions

‫ 2- يمنع الrequests اللي بتكسر الpolicy بتاعة الrate limiter

‫ 3- ميستعملش memory كتير

‫ 3- ينفع يتم استعماله في distributed system environment

‫ 4- fault tolerant

‫ عشان لو وقع ف الAPI حيبقى في خطر من الDoS attack

5- low latency ‫ مش معقول ابقى باعت request من الclient و الclient يبقى مستني كتير عشان الrequest لسه حنشوفه لو مسموحله يعدي و بعدين يعدي علينا الجمعة نكون proccessنا الrequest أصلًا عايز إيه

‫ 6- Exception handling انا ك user محتاج feedback لو الAPI request بتاعي اتعمله block و ياريت يبقى فيه رسالة تقولي ايه اللي حصل .. ف الHTTP Code ده بيبقى كود 429 Too many requests

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342402071/b6f908f9-0c58-41d3-897d-3420e31ee5ce.png align="center")

### ‫ طيب هل نحط الrate limiter ف الclient ولا الserver side ?

‫ الأفضل ف الserver side عشان لو احنا مجرد رجعنا JS للكلاينت ف إحنا ف عرضة انهم يكتشفوا ثغرة و يعدلوه قبل ما يبعتوا الrequest و يهجموا ف DoS attack إنما ف السيرفر ف الورق ورقنا و الدفاتر دفاترنا

‫ فيه حاجة إسمها API Gateway و دي مسئولة عن الSSL Termination authentication و ممكن يتعمل whitelisting او blacklisting لل IPs اللي داخلة تعمل الrequest و ده بيبقى إختيار كويس نحط الAPI limiter بتاعنا فيه

‫ ممكن برضه نحط الlimiter قدام كل الservers لو احنا شغالين monolith او نحطه قدام كل microservice

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342420823/14c88d07-2fc4-42cd-b037-548ccd3e2ff9.png align="center")

.. ده بيعتمد على ال architecture بتاعة الشركة + الstack بتاع التيم

## Algorithms

‫ فيه 5 algorithms مشهورين للrate limiter حنعدي عليهم بسرعة و نقول الpros &cons

### 1- Token bucket algorithm

‫ 1- Token bucket algorithm ‫ بيبقى فيه bucket (ممكن نستعمل stack ك datastructer) و بيبقى فيها عدد معين من الtokens احنا بنحدده .. الrequest بيجي الapi limiter و يشوف لو فيه tokens

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342435346/f4cc6a42-cc0c-456c-9f0a-35859c8b8b89.png align="center")

ف الbucket ولا لأ.

‫ لو فيه ف بياخد token و عدد الtokens ف الbucket بينقص واحد و الrequest يتعمله routing للapi اللي كان عايزه و يديله الtoken عشان يثبت انه حلال و عدى على الrate limiter قبل ما يجيله. ‫ لو مفيش tokens كفاية ف الrequest بتعمله drop و بنرجع رسالة لليوزر بده.

‫ ممكن نحدد ان كل x minutes بنpopulate الbucket بtokens جديدة عشان الrequests التانية و ده بيبقى worker بنسميه refiller ‫ ف كده بيبقى عندنا 2 parameters و هما الbucket size و الrefill rate اللي بيملى الbucket ب tokens لما بيفضى

**pros:**

* easy to implement
    
* memory effecient ‫ و لو فيه spike ف الrequests ف مفيش مشاكل و مش حيحصل throttling او إختناق طالما فيه tokens
    

**cons:** ‫ فيه 2 parameters و ده ممكن يخلق مشاكل للsynchronization و حنشوف ده قدام

### 2- Leaking bucket algorithm

‫ شبه الtoken bucket لكن ده بيبقى queue فيه عدد معين من الrequests ‫ الrequests بتخش First In First Out (FIFO) ‫ لو الqueue مش مليان ف بيخشه على طول ‫ لو الqueue مليان ف بيتعمل drop للrequest

‫ و فيه fixed rate بعد فترة زمنية معينة بيتعمل processing للrequests واحد ورا التاني

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342453844/1b987bd8-c372-45de-940d-5bc4ff2f1647.png align="center")

**pros**:

* memory effecient ‫ و لو الuse case بتاعتك انك ضامن ان ميحصلش spike ف الtraffic (زي امازون وقت الجمعة البيضاء) ف ده مناسب ليكي
    

**cons:** ‫ مش مناسب لو فيه spike ف الtraffic و حيبقى بطيء بسبب اننا بنعمل processing لل requests

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342480615/9be29283-17d9-4e49-b334-73be95178811.png align="center")

ب fixed rate

### 3- Fixed counter algorithm

‫ 3- Fixed counter algorithm ‫ ده ببساطة بيقول ان كل دقيقة حيبقى فيه x number of tokens متاحين .. لو خلصوا ف حتستنى للدقيقة اللي بعدها لو مخلصوش ف خد الtoken و روح عالapi

‫ فيه edge case للalgorithm دي: لنفترض اننا بنسمح ف 5 tokens ف الدقيقة .. و جيت على آخر الدقيقة اللي انا فيها استهلكتهم في آخر 5 ثواني .. بعدين دلوقتي الدقيقة الجديدة إبتدت و فيه 5 tokens جداد و استهلكتهم كلهم برضه في اول 5 ثواني من الدقيقة الجديدة

‫ كده استهلكت 10 tokens في 10 ثواني مع اني المفروض استهلك 5 بس في الدقيقة.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342506877/1d735ff4-1658-4ee6-bf8e-70206506a963.png align="center")

ممكن نحل ده بإننا ن reset الquota في آخر الدقيقة .. بس فيه 2 algorithms باقيين بيحلوا المشكلة دي: ‫

### 4- ‫ Sliding Window log algorithm ‫

* بيبقى فيه memory عشان تخزن الrequest logs ‫
    
* بنخلي الrequest يجي بالtimestamp بتاع لو فيه مكان ف الmemory ‫
    
* لو فيه timestamps اقدم من الcurrent window ف دول بيبقوا outdated و بيتعملهم drop ‫
    
* لو الtimestamps withing الcurrent window ف بنprocessهم
    

‫ pros: accurate ‫ و بتشتغل زي ما الrate limiter المفروض يشتغل

cons: ‫ بتستهلك memory عشان نخزل الrequests بالlogs .. من أشهر الحاجات اللي بيتم استعمالها هي redis عشان memory effecient و سريعة

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342526508/4f45511b-562d-4039-96af-82189fd753ee.png align="center")

### 5- Sliding windows counter algorithm

‫ و دي hybrid algorithm بين ال Sliding window log و الfixed counter window algorithms ‫ لو افترضنا اننا بن process 12 requests ف الدقيقة .. و الدقيقة اللي فاتت كان فيه 9 requests و الدقيقة الحالية فيه 5 requests و جه request جديد ..

‫ عايزين نعرف نعديه ولا لأ منغير الedge case بتاعة الfixed window counter algorithm ‫ الrequest جه ف الربع الأول من الدقيقة الحالية 25% ‫ ف بنحسب بالforumula دي

Requests in current window + (requests in previous windows \* percentage of overlap between the 2 windows)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674342550727/15ba92b9-2760-499c-acc6-bdd94ec66e0b.png align="center")

5 + (9\* 25%) = 5 + 2.25 = 7.25 ~= 8 ‫ ف يجوز اننا نعديه عشان الmaximum amount of requests في حالتنا بيبقى 12

‫ جدير بالذكر ان ال HTTP فيه headers مفيدة لل rate limiter

**HTTP Headers**

X-Ratelimit-Remaining: ‫ عدد الrequests الباقي ف الwindow دي

X-Ratelimit-limit: ‫ أقصى عدد من الrequests المسموح بيه ف time window محددة

X-Ratelimit-Retry-After: ‫ ممكن تجرب تبعت request بعد عدد معين من الثواني

‫ ‫ ‫فيه مشكلتين بنواجهمم ف الrate limiter و هما الrace condition و الsynchronization ‫ الrace condition ممكن نسيب الredis يحله .. كده كده هو single threaded ‫ ف حيتصرف و يحط lock او حاجة لو فيه كذا request ‫ اما مشكلة الsynchronization ف دي ممكن تحصل ف distributed system ‫ ب إني ببعت ريكوست على rate limiter في سيرفر معين .. بعدين ابعت request تاني على سيرفر تاني ب rate limiter تاني ‫ ف كده انا المفروض يبقى بعت 2 requests بس بسبب انفصال الrate limiters ف كده فيه مشكلة synchronization ‫ حل المشكلة دي اننا نستعمل centrilzed cache يبقى عارف الIP بتاع كل ريكوست و عارف فاضله قد ايه

## *المصادر*

أتمنى تكونوا إستدفتدوا و دي المصادر

System Design Interview: Alex Xu https://engineering.classdojo.com/blog/2015/02/06/rolling-rate-limiter/ https://www.tutorialspoint.com/mutex-vs-semaphore https://www.enjoyalgorithms.com/blog/design-api-rate-limiter https://www.thetechnicaltalk.com/2019/12/differentiate-between-leaky-bucket-and.html https://www.wpbeginner.com/wp-tutorials/how-to-fix-the-wordpress-429-too-many-requests-error/ https://redis.io/docs/management/optimization/benchmarks/

‫

‫

‫