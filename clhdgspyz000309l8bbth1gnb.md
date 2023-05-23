---
title: "The Two Generals Problem"
datePublished: Sun May 07 2023 13:43:39 GMT+0000 (Coordinated Universal Time)
cuid: clhdgspyz000309l8bbth1gnb
slug: the-two-generals-problem
tags: distributed-system, system-design

---

# المقدمة‫

في سبتمبر 2018 كان فيه مشكلة عند Delivroo ان ناس بالهبل في بريطانيا كان بيجلها نفس الأوردر مرتين 3 و بيتم خصم التمن منهم كذا مرة .. دي كانت مصيبة و الcustomer support كان طالع عينه من كتر الشكاوي و الطيارين كانوا تعبانين من كتر التوصيل .. ده بسبب The 2 Generals Problem

![Finematics](https://cdn.hashnode.com/res/hashnode/image/upload/v1683466594655/7663c52e-d981-4fc2-8a88-e1445729b461.png align="center")

## The Two Generals Problem

‫ لو فيه جيشين عايزين يحتلوا قلعة .. القائد بتاع كل جيش حيحب ينسق مع التاني عشان يهاجموا القلعة مع بعض في نفس الوقت لأن لو جيش هاجم لوحده حيموت ف الأحسن يهاجموا سوا الفكرة ان كل واحد فيهم على جنب ف حيبعتوا لبعض رسايل يتفقوا على معاد الهجوم

لما القائد الأولاني يبعت للتاني .. حيبقى عايز رسالة من التاني يقوله انه تمام معاد الهجوم او مش تمام. فيه مشكلة كمان ان ممكن رسالة القائد الأولاني تضيع ف القائد التاني موصلتهوش أي رسالة أو ممكن القائد التاني توصوله الرسالة بس رسالة التأكيد تضيع في النص

![Distributed Systems University of Cambridge Computer Science Tripos, Part IB Michaelmas term 2021/22](https://cdn.hashnode.com/res/hashnode/image/upload/v1683466687818/c38b60e6-617e-4794-aeb9-47bfc7a426b0.png align="center")

‫ ممكن نحل مشاكل التنسيق ان القائد التاني بعد ما يبعت رسالة التأكيد .. يستنى من القائد الأولاني يبعتله رسالة بيأكدله انه وصلتله رسالة التأكيد 😃 بس ممكن رسالة التأكيد تضيع برضه و هكذا .. دي مشكلة في الDistributed Systems إسمها

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683466722086/ed12533c-8000-4806-ac1b-081971351122.png align="center")

## مثال

‫ الموضوع ده نقدر نشوفه في أبليكاشن زي Talabat أو أمازون .. انه لما بتطلب أوردر و حتدفع أونلاين .. الpayment بيكون على سيرفر تاني و غالبًا بتبقى service تانية بتقدمهولك زي Paypal, Stripe .. و Talabat محتاج ينسق مع Stripe ان المطعم ده مفتوح و ان فيه أكل و فيه طيارين يقدروا يروحوله

‫ و Stripe بيتواصل مع البنك - يشوف لو عندك فلوس تكفي أوردر من الطازج طالبه الساعة 2 الفجر - و يسحب الفلوس من الحساب و يتواصل مع Talabat يقوله تمام و ابعت الأوردر. لازم Talabat ينسق مع Stripe بحيث لو المطعم معنهدوش أكل ف مينفعش نسحب فلوس من الزبون

![Distributed Systems University of Cambridge Computer Science Tripos, Part IB Michaelmas term 2021/22](https://cdn.hashnode.com/res/hashnode/image/upload/v1683466757470/dea92371-f710-4ee9-9700-2fc199ac2bad.png align="left")

### سيناريوهات

‫ ده ف الTwo Generals Problem عامل زي القائدين ميتفقوش عالهجوم لو Talabat بعتت الأوردر منغير ما Stripe يأكد انه سحب فلوس من الزبون ف كده Talabat حتخسر فلوس ده زي ما قائد يهاجم عالقلعة منغير ما القائد التاني يأكد انه تمام عالهجوم

‫ و لو Stripe بعتت لTalabat انه تمام سحب الفلوس من الزبون بس Talabat موصلهوش التأكيد ف كده الفلوس اتسحبت و حضرتك لسه جعانة #hangry ده لو القائد التاني قال للأولاني تمام يلا نهاجم لكن الأولاني موصلهوش ف كده القائد التاني حيهاجم القلعة منغير الأولاني

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683466777263/46a63b09-e290-4630-9136-024e945d4d5e.png align="center")

‫ آخر سيناريو و هو السيناريو الجميل ان لو Talabat تواصلت مع Stripe و Stripe سحبت الفلوس و بعتت لTalabat و Talabat بعتت الأوردر

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683466841963/fc7d0ad2-9276-4f71-a088-2df7e849369f.png align="center")

## Idempotent token

‫ حل مشكلة ال2 Generals هي بإستعمال حاجة اسمها Idempotent Key او Idempotent token Idempotency هو مبدأ في الAPI communication ان لو بعت ريكوست للسيرفر 500 مرة بنفس الarguments ف لازم يرد عليك نفس الرد لو انت بعت ريكوست مرة واحدة

‫ و دي المشكلة اللي كانت عند Delivroo .. لما الناس كانت بتبعت ريكوست و تعمل أوردر .. كان فيه مشكلة تواصل بين الPayment Gateway و بين Delivroo عشان الpayment بيسحب فلوس من الزباين و Delivroo مبيوصلهوش Ack من الpayment ف بيtime out و يقولهم جربوا تاني

‫ بعد ما بيجربوا 3 أربع مرات الapp بيقولهم تمام و الزباين بتفتكر انهم طلبوا مرة واحدة. حل الموضوع ده ان لما الclient او الapp يعمل ريكوست للpayment ف لازم يحط Idempotent key و ده عبارة عن UUID (زي 123e4567-e89b-12d3-a456-426614174000) و بيبقى جزء من الinput arguments للريكوست

‫ لما الريكوست يتبعت للpayment service, الأخير بيبص على datastore بيخزن في الidempotent tokens لفترة زمنية معينة بعدين بيexpire (لو الtoken مش موجود) لو موجود ف بيقوله الأوردر إتطلب خلاص مفيش داعي للتكرار

![Diagram done using https://excalidraw.com/](https://cdn.hashnode.com/res/hashnode/image/upload/v1683466920295/f836f7ba-0942-43ad-ad13-4fb57a9639a4.png align="center")

# المصادر

1. [https://www.cl.cam.ac.uk/teaching/2122/ConcDisSys/dist-sys-notes.pdf](https://www.cl.cam.ac.uk/teaching/2122/ConcDisSys/dist-sys-notes.pdf)
    
2. [https://www.youtube.com/watch?v=MDuWnzVnfpI&t=198&ab\_channel=MartinKleppmann](https://www.youtube.com/watch?v=MDuWnzVnfpI&t=198&ab_channel=MartinKleppmann)
    
3. [https://www.youtube.com/watch?v=I08syTslan8&ab\_channel=BeABetterDev](https://www.youtube.com/watch?v=I08syTslan8&ab_channel=BeABetterDev)
    
4. [https://www.youtube.com/watch?v=IP-rGJKSZ3s&ab\_channel=TomScott](https://www.youtube.com/watch?v=IP-rGJKSZ3s&ab_channel=TomScott)