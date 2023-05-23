---
title: "ازاي تعمل System design ل Facebook messenger"
datePublished: Tue Dec 20 2022 21:34:10 GMT+0000 (Coordinated Universal Time)
cuid: clbwqu980000008js845uhzmt
slug: techcapsule-in-arabic-system-design-fb-messenger
tags: system-design, arabic

---

‫ عملًا ب (اشرح الحاجة عشان تفهمها) ف ده ثريد ب ازاي تعمل System design ل Facebook messenger

‫ في البداية بنحدد ايه هي الrequirements

‫ ١- المستخدمين يقدروا يبعتوا رسايل لبعض.

‫ ٢- نقدر نشوف الonline/offline status

‫ ٣- التشات يبقى موجود و متخزن ف داتابيز للابد

‫ ٤- الرسايل تبقى up to date عند المستخدمين و الداتا تبقى consistent

‫ ٥- ميبقاش فيه delay عشان الرسالة توصل للطرف التاني

‫ ٦- الماسنجر يبقى متاح للي حابب ي access it بس الأهم ان التشات يبقى consistent يعني ميتغيرش .. ف بنفضل الconsistency عن الavailability ف الحالة دي بعدين بنعمل حاجة اسمها Back of the envelope calculations و هي مجرد estimations عن الtraffic اللي الservice حتخدم عليها عشان تعرف الstorage المطلوب و الbandwidth

‫ دلوقتي فيسبوك عنده بليون مستعمل .. نقول ان نصهم عالماسنجر يوميا .. و كل مستخدم من دول بيبعت ٥٠ رسالة يوميًا .. 500 million users \* 50 messages = 25,000,000,000 messages

‫ لو قلنا ان حجم الرسالة الواحدة ب 100 bytes يبقى اجمالي الstorage يعني اجمالي الحجم بالbytes

\= 2500,000,000,000 2.5 Terabyte

‫ لو افترضنا اننا حنجرب الapp لمدة ٥ سنين 5 \* 12 \* 365 = 21900 نحاول نقربها ل 22000 عشان نسهلها على نفسنا .. يعني

2.5 \* 22000 = 55000 Terabyte = 5.5 Peta byte

‫ و دلوقتي لو رجعنا ان كل يوم بيبقى عندنا 2.5 Terabyte من الداتا ف احنا محتاجين bandwidth 2.5T.B./24*60*60

2500,000 MB / 86400 = 30 M.B./second

‫ رايح جي تمام .. نخش بقى ف الrequirements ازاي نحققها User flow نقطة حلوة نبتدي منها هي ال

![نخش في الموضوع على طول - YouTube](https://i.ytimg.com/vi/UfVHrtPEjvk/hqdefault.jpg align="left")

‫ ده شكل مبسط high level بعدين حنتعمق فيه

1.  Sender sends a message to receiver through the server
    
2.  Server acknowledges that it received the message
    
3.  Server forwards the message to receiver.
    
4.  Async call/Another thread writes the message to the database.
    
5.  Receiver acknowledges the receiving of the message to the server.
    
6.  Server notifies sender that receiver saw the message
    

‫ دلوقتي محتاجين نعرف ازاي نلاقي طريقة حلوة عشان الusers يبعتوا و يتسقبلوا رسايل و يتاوصلوا مع الserver

‫ ١- Pull model: و ده عامل زي هنيدي لما قاعد يقول باشا

‫ ٢- Push model الclient بيبعت للسيرفر يسأله لو فيه حاجة جاتله و يسيب الconnection مفتوح .. و معندوش مشاكل ان السيرفر ميردش عليه بسرعة .. و طبعا لو الconnection timeout بيعمل retry

‫ الحل التاني مناسب ف حالتنا عشان لو ٥٠٠ مليون user قعدوا يكلموا السيرفر ده كده مكلف جدًا خصوصا انه عشان نتجنب latency .. محتاجين الclient يفضل يسأل السيرفر كتير و معظم الوقت حيرجعله empty response ف الأفضل اننا نستعمل الأوبشن التاني و نسيب السيرفر يبعتلنا منين ما حاجة تجيلنا طيب دلوقتي السيرفر حيعرف منين انهي user مستني انهي message ؟

‫ ممكن ب داتا بيز ت map الUser Id بالمسج بالconnection object طب و نعرف منين ان اليوزر بقى أونلاين ولا بيوخونا مع حد تاني ؟

‫ أول ما الpush model يبتدي و الuser يسأل السيرفر لو حد بعتله حاجة يقوم السيرفر مجرسه و يبعت للfriend list انه موجود .. ممكن ن optimise اننا نبين انه أونلاين لأكتر ناس هو بيكلمهم عشان دول اللي مهتمين بيه بما ان حيبقى عندنا write operations كتيرة فحت .. و الداتا صغير (المسج بتاعة التشات) .. ف مينفعش نستعمل databse row based عشان ده خراب latency .. ممكن نستعمل column based database زي Casandra او HBase .. و حنستفيد انهم NoSql ف حي scaleو معانا بسهولة زائد ان لما نحب نعمل read operations .. دي الuser حايrequest it بالpagination .. لما بن scroll ف التشات كده.

‫ فاضل اننا نعمل data partitioning عشان ميبقاش البيض كله ف سلة واحدة .. ممكن نعمله على أساس الUserId بحيث ان لو عندنا data بحجم 5.5 Petabytes و الdatabase shard يستحمل 5 TB ف كده حنحتاج حوالي ١٢٠٠ shard .. ف ممكن نعرف مكان الshard بتاع الUser ب hash(UserID) % 1000

‫ حنحتاج ن cache آخر ٢٠ رسالة لليوزر عشان لما الكراش تبعتلنا رسالة .. حنفضل نقراها و نبحلق فيها و محتاجين ن access it بسرعة.

‫ نقول حنخزن آخر ١٠ رسايل لكل user يعني حنحتاج 20% من ال storage يبقى cached

‫ زائد اننا حنحتاج Load balancer من الuser لل application و من الuser للcache و من الapplication لل database عشان الtraffic الكبير .. بس حنحتاج balancing algorithm بحيث انها تforward الusers اللي بيتكلموا كتير لservers ب capability حلوة .. ممكن weighted round robin أو Least Connection Method عشان تروح للسيفير اللي فاضي .. عيب الطريقة التانية ان الload balancer محتاج يشوف الأول الinfo بتاعة الserver قبل ما ي forward الريكويست و بس يا حبايبي .. أتمنى تكونوا استمتعتوا و أتمنى أكون أفدتكم 😃