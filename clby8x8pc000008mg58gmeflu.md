---
title: "RPC vs REST vs GraphQL"
datePublished: Wed Dec 21 2022 22:48:09 GMT+0000 (Coordinated Universal Time)
cuid: clby8x8pc000008mg58gmeflu
slug: rpc-vs-rest-vs-graphql
tags: graphql, rest-api, arabic, rpc

---

## مقدمة

‫ مبدئيًا انواع الAPIs يا إما Request/Response API او Event Driven API

‫ التلاتة دول هما من النوع الاولاني و الAPI او Application Programming Interfacs هو بروتوكول بيحدد ازاي الclient حيكلم السيرفر و او بشكل أعم ازاي الinformation provider و الinformation seeker حيتواصلوا مع بعض

## REST

‫ الREST هو اختصار ل Representational state transfer و هو عبارة عن contrains و architectual style

‫ عشان يحدد الinterface اللي حيخلي الmachine تكلم machine تانية و REST اتعمل بغرض انه يخلي الcoupling بين الclient (بيبقى اسمه user agent) و الserver تبقى lightweight عند طريق ان يخلق layer مخصوصة للresources اللي عالserver منغير ما الuser agent يحتاج يعرف implementation details

‫ زي هل هو بيrequest من database ولا من file server ..

‫

### RESTخصائص ال

الconstrainst اللي بحتم عليها REST هي:

‫\**Separation of concern*\*: الclient-server design pattern معمول عشان الclient ميشلش هم اي server implementations و الbrowsers الحالية معمولة كده .. ف كان لازم REST يكمل ده عشان يبقى adaptable

‫ **Statelessness**: مينفعش نخزن الsession اللي بتتخلق لما الclient يكلم السيرفر و المفروض لو session جديدة اتعملت متبقاش معتممدة على الsession اللي قبلها .. ده مفيش ف الhigh volume applications

‫ **Cacheability**: الresponses تبقى cacheable عشان العمر قصير و ممكن نخزنها ف Content Delivery Network (CDN).

**‫ Layered system**: عادة الclient مبيعملش connection للسيرفر طوالي كده .. بيبقى فيه Proxy او Load balancer ما بينهم .. المهم ان ده ميأثرش عالcommuinication

‫ **Uniform interface**: و ده أكتر حاجة REST مشهور بيها .. عشان ده بيساعد في تعريف ايه الResource اللي احنا عايزينه و لازم الclient يبقى قادر ي manipulate الresource ده لو عايز ‫ لو اتححقت كل الcontraints دي ف الAPI بتاعك ف تقدري تقولي ان

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671661376739/-8BTKbAh8.png align="center")

‫ الoperations المعروفة لأ persistant storage ايًا كان ايه الAPI Paradiagm هما CRUD Create, Read, Update, Delete

‫ الREST methods اللي بتsupport ده GET, POST, PUT, DELETE, PATCH

‫ POST بي create resource زي اننا نحط records في داتابيز PUT بي update resource اننا بنupdate الداتا دي

### ‫ مزايا الREST APIs

‫ مزايا الREST APIs انه بيستعمل HTTP protocol features و الmethod names و الstatus code معروفة و هو مناسب جدًا لو الoperations بتاعتنا معظمها او كلها CRUD operations

### ‫ عيوب الREST APIs

‫ عيبه ان الpayload كبير .. لو احنا عندنا مثلا DB table لطلبة ف كلية .. ف لو انا مثلا عايز بس اسم طالب .. حيرجعلي الresource كله بتاعة الطالب ده زي اسمه و الid و قسمه و .. و .. انا مطلبتش ده ف الpayload كبير

‫ عشان نحل ده ف ممكن نعمل http roundtrip تانية عشان نfilter و نفلتر

## RPC

‫ RPC او Remote Procedure Call ده تيكنيك ف الdistributed computing بحيث ان computer program يcall a procedure سواء serivce او subroutine موجود في machine تانية

‫ الصورة من Educative.io

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671661430998/Rs5_Eogwd.png align="center")

‫ لما الprogram اللي بيستعمل RPC Framework ي compile ل executable program .. بيبقى فيه حاجة اسمها stub موجودة في الcompiled code .. لما الprogram يتعمله run و يحصل فيه remote procedure call .. الstub بيجيله الrequest و بيcontact الserver

‫ مهمة الstub هي انه يعمل marshalling و ده عبارة عن انه يعمل packing للparameters بتاعة الclient لmessage packet لما الclient يعمل الremote procduer call للserver او لما السيرفر يخلص الprocedure و يرد على الclient

‫ الclient بي call الclient stub بالparameters اللي هو عايز يبعتها للسيرفر

‫ **الخطوات**:‫

‫ 1- الcall ده بيقبى اسمه local procedure call عشان بيحصل على نفس الmachine

‫ 2- الclient stub بي push الparametrs ف الmemory stack عادي

‫ 3- الclient stub يعمل marshalling للparametrs و يحولها ل message packets بعدين بيعمل system call للOSبتاع الclient machine

‫ 4- الOSبتاع الclient machine بيبعت رسالة من الclient machine للremote server machine

‫ 5- الOS بتاع الserver بيforward الmessage packets للstub بتاعه شخصيًا

‫ 6- الstub بتاع الserver يعمل unmarshalling و يحول الmessage packet لparameters عادية

‫ 7- يعمل local procedure call زيتنا في دقيقنا بعدين يرجع الparametrs الجديدة للserver stub و يعمل marshalling

‫ 8- الOS بتاع السيرفر يبعت الmessage لل client

‫ 9- الclient يforward الmessage للstub و يunmarshall الmessage

‫ 10 - الexecution process بترجع كما كانت

خلصنا

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671661491688/0nZjXDhNV.png align="center")

‫ بالمناسبة Slack من أشهر متبنيي الRPC و ده منظر للcalls اللي بتحصل.

### ‫ مزايا الRPC

‫ الRPC جميل عشان الpayloads صغيرة عشان هو action oriented جدًا ف نقدر نحدد احنا عايزين بالظبط .. كمان ده بيساعد ان الperformance بتاعه بيبقى أحسن بكتير

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671661564277/V2lvcd5wo.png align="center")

### ‫ عيوب الRPC

‫ عيوبه ان مفيش standarization كويس ف ده بيخليه ممكن يبقى implemented بكذا طريقة و مفيش طريقة موحدة الكل يتفق عليها .. cost of flexibility

‫ عيب كمان ان الstyle ده ممكن يؤدي لحاجة اسمها function explosion عشان كل ما نضيف features اكتر للfunction كل ما حتكبر

## GraphQL

‫ ابتدى من فيسبوك بس دلوقتي بقى فيه شركات كبيرة بتستعمله زي github و yelp و pinterest

‫ فكرته انه بت expose entry point واحدة و الclient هو اللي ايه هي الstructure المطلوبة و الserver بيفهم ده و يرجعه .. مش العكس

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671661642345/kPCxDzjwB.png align="center")

‫ يعني لو افترضنا اننا عايزينا بيانات للusers من github ف الendpoint بتبقى حاجة زي

[https://api.github.com/graphql](https://api.github.com/graphql)

‫ و الpayload بتاع الrequest و الresponse بيبقى كالتالي

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671661699094/SiPV7LBD7.png align="center")

### **مزايا ال GraphQL**

‫ مزاياه ان بما ان الclient بيحدد الdata structure و ممكن يحدد nested levels من الداتا .. ده بيوفر multiple round trips كتير.

‫ حاجة كمان اننا بنتجنب api versionning .. لو احنا عايزين fields او عايزين ن deprecte fields ف احنا بنتحكم ده من الclient side و مش محتاجين نعمل versionning

### عيوب الGraphQL

‫ عيبوه ان السيرفر بيبقى عليه complexity عشان يفهم الstructure و يرجع اللي مطلوب .. ده بيؤدي لعيب تاني ان الperformance بيبقى مش حلو و الopmitization بتاعه بيكون صعب.

‫ الgraphql غير مناسب لو الAPI محتاجه يعمل حاجات بسيطة

## الخاتمة:

REST

‫ مناسب لو عندك CRUD operations

RPC

‫ حلو لو عايز ت expose كذا action

Graphql ‫ جميل لو محتاج data filtering معقد عالclient side

‫ حتسألني مفيش API قمر ؟ حقولك مفيش قمر غيرك يا قمر ❤️😘