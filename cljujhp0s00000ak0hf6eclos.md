---
title: "Zero Trust Secruity Model ايه ال"
datePublished: Sat Jul 08 2023 21:50:33 GMT+0000 (Coordinated Universal Time)
cuid: cljujhp0s00000ak0hf6eclos
slug: zero-trust-secruity-model-ayh-al
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1688852993270/68554fa5-da76-4774-b363-85f9dee6dee8.png
tags: security, securityawareness, zerotrust

---

# Castle moat security Model

أيام العصور الوسطى كانوا بيحفروا خندق حوالين القلعة و يملوه بالمياة عشان لو حد حيهاجم يقدروا يقتلوه و هو بيعوم و لو فيه رسول حد باعته بينزلوله الجسر بتاع القلعة و يخش .. القلعة محصنة و ضامنين ان اللي داخل هما عارفينه

‫ الشركات الأمريكية زي جوجل و مايكروسوفت بيجلهم external attacks يوميًا من الروس و الصين و كوريا الشمالية و زمان كان مهندسين الcybersecurity مركزين على حماية الnetwork perimeter بتاعة الشركة من الهجمات من برة بإستعمال security model اسمه Castle and moat

## Network Perimeter

‫ الnetwork perimeter ده عامل virtual boundary بيفصل الشركة عن العالم الخارجي و هدف الsecurity engineer انها تحمي الinternal resources بتاعة الشركة من أي حد unauthorized. الnetwork perimeter بيتكون من firewalls و routers و حاجتين اسمهم IDS و IPS

### Intrusion Detection Systems (IDS)

‫ ‫ و ده بيراقب الnetwork traffic جوة الشركة و بيحلله و بيقدر يلاحظ لو فيه pattern او anomaly و لو لقى ده بيlog it و بينبه الsecurity adminstrators

### Intrusion Prevention Systems (IPS)

‫ ‫ بيعمل نفس اللي بيعمله الIDS زائد انه ممكن ياخد automated actions بإنه يحجب IP address مسبب مشاكل زي DDos attack و بيعمل deep packet inspection و يشوف الcontent بتاعة الpacket و يتطمن ان مفيهاش حاجة مريبة

‫ الmodel يبان انه حلو و كل حاجة لأن الcompany network هي القلعة المحصنة و الnetwork perimter هو الmoat او الخندق اللي بيشوف مين اللي داخل و اللي طالع. ‫ عيب الموضوع ده انه واثق تمامًا في الناس اللي جوة الشركة و انهم إستحالة يعملوا حاجة غلط عشان هما authorized و مننا و علينا

‫ الثقة دي كانت غلط لأن أشهر تسريب في التاريخ الحديث حصل بسبب (إدوارد سنودن) و اللي كان شغال في الNSA و سرب ان الحكومة الأمريكية بتتجسس على مواطينها و حلافئها بدون علمهم .. بعدها هرب و حاليًا في روسيا.

![Edward Snowden](https://cdn.hashnode.com/res/hashnode/image/upload/v1688852454244/cdef3e96-952d-405f-a554-c40456224f0a.png align="center")

‫ حاجة تاني الCastle moat model مكنش موفرها هي الhybrid work .. الناس عشان تعرف تشتغل و تخش جوة الresources بتاعة الشركة محتاجين يبقوا جوة مبنى الشركة نفسها. ‫ حاجة تاني الCastle moat model مكنش موفرها هي الأمان بيئة عمل hybrid .. عشان الناس تعرف تشتغل و تخش جوة الresources بتاعة الشركة محتاجين يبقوا جوة مبنى الشركة نفسها و الVPN لوحده مش secure كفاية طبعًا وقت الكورونا الموضوع ده كان مستحيل ف بقى فيه الحاجة لmodel جديد ‫ من هنا جت الحاجة لmodel جديد أكثر حماية و مرونة في نفس الوقت

# Zero trust

![عادل إمام و عايدة رياض](https://cdn.hashnode.com/res/hashnode/image/upload/v1688852653495/61911770-876f-4847-bc59-67c1b59998e4.png align="center")

‫ ‫ جي من اسمه انك مش واثق في حد حتى لو جوة الشركة .. كل request حيبقى verified فيه 3 مبادىء أساسيين

![Principles of Zero Trus, credits to NextLabs](https://cdn.hashnode.com/res/hashnode/image/upload/v1688852671085/32ae1b4b-c47b-44a7-9910-12548f39694d.png align="center")

## Never trust & Always verify

‫ ‫ لازم نستعمل كل الdata points اللي عندنا قبل ما ناخد أي security decision زي:

‫ 1- الlocation اللي باعت منه الrequest

‫ 2- الdevice health و هل الجهاز بتاعي updated و مفيهوش ثغرات أمنية

‫ 3- الdata classification و هل الشخص معاه authorization يستعملها

## ‫ Use least privilege access ‫

لو انت محتاج تread database ف الrole access اللي انت محتاجه هو read بس .. مينفعش يبقى معاك read&write role access .. المبدأ ده اسمه JEA أو Just Enough Access

## ‫ Assume Breach

![Blast Raduis from Change management in the age of DevOps article by  GREG SANKER https://itsmtransition.com/2019/08/change-management-in-the-age-of-devops/](https://cdn.hashnode.com/res/hashnode/image/upload/v1688852724866/c2ef5f9f-1ff4-4787-9e04-ee78b7ee23b0.png align="center")

لما قنبلة بتنفجر بيبقى ليها blast raduis و ده المحيط اللي تضرر من الإنفجار .. لو حصلك security breach ف لازم تقلل الblast raduis بتاعه .. متوسط الضرر من الsecurity breach بيكلف 3 مليون دولار ..  
‫

‫ تقدر تحقق ده بالMicrosegemntation ‫ مثال للmicrosegmentation ان لو عندك 4 تيمات ف الشركة كل واحد شغال على repo مختلف .. ف كل repo يبقى ليه security policy بحيث ان اللي شغالين عليه هما بس اللي يقدروا يaccessوه .. عشان لو عندك جاسوس في تيم منهم حب يحط الrepo public ف عند 3 في امان

## ZTNA

![ZTNA architecture  from https://www.cloudflare.com/learning/access-management/what-is-ztna/](https://cdn.hashnode.com/res/hashnode/image/upload/v1688852693160/33d5b47b-225e-464e-9025-fd2614a584ba.png align="center")

‫ لو حاتimplement zero trust model ف بتحتاج Zero Trust Network Access أو ZTNA و ده بديل عن الVPN ‫ الVPN بيexten private network على public network اللي هي الinternet و بيعمل tunnel مشفرة بحيث لو انت معاك passowrd بتقدر ت connect عالشركة و بيبقى ليك access عالresources بتاعة الشركة

‫ الZTNA بيديك الaccess عالresources اللي ليك الsecurity previlige ليها و بيبقى granular و policy-based .. ده مخلي الlatency بتاعته أحسن من الVPN عشان بيتعملك routing للحاجات اللي انت ليك الحق تشوفها فقط مش كل حاجة.

‫ لو كنتي بتكراشي على واحد اسمه أحمد و عايزة تعرفي هو فين دلوقتي ف الVPN بيقولك طالما معاكي بطاقة رقم قومي ف ليكي access تدوري عليه ف مصر كلها و ده حياخد وقت كتير. ‫ لكن الZTNA بيقولك لو معاكي رقم قومي و ليكي الحق تدوري ف محافظة إسكندرية بس ف حتاخدي وقت أقل. ف الZTNA lightweight

‫

## ‫المصادر

‫[https://www.youtube.com/watch?v=yn6CPQ9RioA&ab\_channel=IBMTechnology](https://www.youtube.com/watch?v=yn6CPQ9RioA&ab_channel=IBMTechnology)

[https://en.wikipedia.org/wiki/Colonial\_Pipeline\_ransomware\_attack](https://en.wikipedia.org/wiki/Colonial_Pipeline_ransomware_attack)

[https://en.wikipedia.org/wiki/2021\_Microsoft\_Exchange\_Server\_data\_breach](https://en.wikipedia.org/wiki/2021_Microsoft_Exchange_Server_data_breach)

[https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RWJJdT](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RWJJdT)

[https://www.cloudflare.com/learning/access-management/castle-and-moat-network-security/](https://www.cloudflare.com/learning/access-management/castle-and-moat-network-security/)

[https://www.cloudflare.com/learning/access-management/what-is-the-network-perimeter/](https://www.cloudflare.com/learning/access-management/what-is-the-network-perimeter/)

[https://www.cloudflare.com/learning/security/glossary/what-is-zero-trust/](https://www.cloudflare.com/learning/security/glossary/what-is-zero-trust/)

[https://www.cloudflare.com/learning/access-management/what-is-microsegmentation/](https://www.cloudflare.com/learning/access-management/what-is-microsegmentation/)

[https://www.ibm.com/downloads/cas/QMXVZX6R](https://www.ibm.com/downloads/cas/QMXVZX6R)

[https://www.cloudflare.com/learning/access-management/what-is-ztna/](https://www.cloudflare.com/learning/access-management/what-is-ztna/)

[https://www.cloudflare.com/learning/access-management/what-is-a-vpn/](https://www.cloudflare.com/learning/access-management/what-is-a-vpn/)

[https://www.paloaltonetworks.com/cyberpedia/what-is-zero-trust-network-access-ztna](https://www.paloaltonetworks.com/cyberpedia/what-is-zero-trust-network-access-ztna)

[https://itsmtransition.com/2019/08/change-management-in-the-age-of-devops/](https://itsmtransition.com/2019/08/change-management-in-the-age-of-devops/)

‫

‫

‫