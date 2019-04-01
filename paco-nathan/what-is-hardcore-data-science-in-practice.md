# What is hardcore data science—in practice?

{% embed url="https://www.oreilly.com/ideas/what-is-hardcore-data-science-in-practice" %}

Data science has become widely accepted across a broad range of industries in the past few years. Originally more of a research topic, data science has early roots in scientists efforts to understand human intelligence and create artificial intelligence; it has since proven that it can add real business value.

As an example, we can look at the company I work for: [Zalando](http://www.zalando.com/), one of Europe’s biggest fashion retailers, where data science is heavily used to provide data-driven recommendations, among other things. Recommendations are provided as a back-end service in many places, including product pages, catalogue pages, newsletters, and for retargeting.![data-driven recommendations](https://d3ansictanv2wj.cloudfront.net/image_1-24655720fbf19c663573aa6bbd0b2a58.jpg)Figure 1. Slide image courtesy of Mikio Braun.

### Computing recommendations

Naturally, there are many ways to compute data-driven recommendations. For so-called collaborative filtering, user actions like product views, actions on a wish-list, and purchases, are collected over the whole user base and then crunched to determine which items have similar user patterns. The beauty of this approach lies in the fact that the computer does not have to understand the items at all; the downside is that one has to have a lot of traffic to accumulate enough information about the items. Another approach only looks at the attributes of the items, for example, recommending other items from the same brand, or with similar colors. And of course, there are many ways to extend or combine these approaches.

**STRATA DATA CONFERENCE**

[![](https://d3ansictanv2wj.cloudfront.net/stuk19-700x750-a0afb69251ed18db783225e90455f4f7.jpg)](https://conferences.oreilly.com/strata/strata-eu)

### [Strata Data Conference in London, April 29-May 2, 2019](https://conferences.oreilly.com/strata/strata-eu)

[Check it out ](https://conferences.oreilly.com/strata/strata-eu)![data complexity](https://d3ansictanv2wj.cloudfront.net/image_2-a5e8ed6443d5f82bbed5102324acfe7a.jpg)Figure 2. Image courtesy of Antonio Freno, from "[One-Pass Ranking Models for Low-Latency Product Recommendations](http://dl.acm.org/authorize.cfm?key=N91951)," KDD 2015. Used with permission.

Simpler methods consist of little more than counting to compute recommendations, but of course, there is practically no limit to the complexity of such methods. For example, for personalized recommendations, we have been working with [_learning to rank_](https://en.wikipedia.org/wiki/Learning_to_rank)methods that learn individual rankings over item sets. The above figure shows the cost function to optimize here, mostly to illustrate the level of complexity data science sometimes brings with it. The function itself uses a pairwise weighted ranking metric, with regularization terms. While being very mathematically precise, it is also very abstract. This approach can be used not only for recommendations in an e-commerce setting, but for all kinds of ranking problems, provided one has reasonable features.

### Bringing mathematical approaches into industry

So, what does it take to bring a quite formal and mathematical approach like what we’ve described above into production? And what does the interface between data science and engineering look like? What kind of organizational and team structures are best suited for this approach? These are all very relevant and reasonable questions, because they decide whether the investment in a data scientist or a whole team of data scientists will ultimately pay off.

In the remainder of this article, I will discuss a few of these aspects, based on my personal experience of having worked as a machine learning researcher as well as having led teams of data scientists and engineers at Zalando.

### Understanding data science versus production

Let’s start by having a look at data science and back-end production systems, and see what it takes to integrate these two systems.![data science and back-end production systems](https://d3ansictanv2wj.cloudfront.net/image_3-5800f7c7856545a3a7a6cf0727e2d044.jpg)Figure 3. Slide image courtesy of Mikio Braun.

The typical data science workflow looks like this: the first step is always identifying the problem and then gathering some data, which might come from a database or production logs. Depending on the data-readiness of your organization, this might already prove very difficult because you might have to first figure out who can give you access to the data, and then figure out who can give you the green light to actually get the data. Once the data is available, it’s preprocessed to extract features, which are hopefully informative for the task to be solved. These features are fed to the learning algorithm, and the resulting model is evaluated on test data to get an estimate of how well it will work on future data.

**O'REILLY ONLINE LEARNING**

[![](https://d3ansictanv2wj.cloudfront.net/safari-topic-cta-1f60e6f96856da19ba3cb25660472ca5.jpg)](https://learning.oreilly.com/)

### [Learn faster. Dig deeper. See farther.](https://learning.oreilly.com/)

Join the O'Reilly online learning platform. Get a free trial today and find answers on the fly, or master something new and useful.[Learn more ](https://learning.oreilly.com/)

This pipeline is usually done in a one-off fashion, often with the data scientist manually going through the individual steps, using a programming language like Python, that comes with many libraries for data analysis and visualization. Depending on the size of the data, one may also use systems like Spark or Hadoop, but often the data scientist will start with a subset of the data first.

### Why start small?

The main reason for starting small is that this is a process that is not done just once, but will in fact be iterated _many times_. Data science projects are intrinsically exploratory, and to some amount, open ended. The goal might be clear, but what data is available, or whether the available data is fit for the task at hand, is often unclear from the beginning. After all, choosing machine learning as an approach already means that one cannot simply write a program to solve the problem. Instead, one resorts to a data-driven approach.

This means that this pipeline is iterated and improved many times, trying out different features, different forms of preprocessing, different learning methods, or maybe even going back to the source and trying to add more data sources.

The whole process is inherently iterative, and often highly explorative. Once the performance looks good, one is ready to try the method on real data. This brings us to production systems.![production systems](https://d3ansictanv2wj.cloudfront.net/image_4-ac3556edbac05e990582ca3f2b92e973.jpg)Figure 4. Slide image courtesy of Mikio Braun.

### Distinguishing a production system from data science

Probably the main difference between production systems and data science systems is that production systems are real-time systems that are continuously running. Data must be processed and models must be updated. The incoming events are also usually used for computing of key performance indicators like click-through rates. The models are often retrained on available data every few hours and then loaded into the production system that serve the data via a REST interface, for example.

These systems are often written in programming languages like Java for performance and stability reasons.O'Reilly Data Newsletter

### [Get the O'Reilly Data Newsletter](https://www.oreilly.com/ideas/what-is-hardcore-data-science-in-practice)

Receive weekly insight from industry insiders—plus exclusive content, offers, and more on the topic of data.Your EmailCountry- Select Country -United StatesAfghanistanAlbaniaAlgeriaAndorraAngolaAntigua and BarbudaArgentinaArmeniaArubaAustraliaAustriaAzerbaijanThe BahamasBahrainBangladeshBarbadosBelarusBelgiumBelizeBeninBermudaBhutanBoliviaBosnia and HerzegovinaBotswanaBrazilBruneiBulgariaBurkina FasoBurundiCambodiaCameroonCanadaCape VerdeCentral African RepublicChadChilePeople's Republic of ChinaColombiaComorosCongo, Republic of theCongo, Democratic Republic of theCook IslandsCosta RicaCôte d'Ivoire \(Ivory Coast\)CroatiaCubaCyprusCzechiaDenmarkDjiboutiDominicaDominican RepublicEcuadorEgyptEl SalvadorEquatorial GuineaEritreaEstoniaEswatini \(formerly Swaziland\)EthiopiaFederated States of MicronesiaFijiFinlandFranceGabonThe GambiaGeorgiaGermanyGhanaGreeceGrenadaGuatemalaGuineaGuinea-BissauGuyanaHaitiHondurasHungaryIcelandIndiaIndonesiaIranIraqIrelandIsraelItalyJamaicaJapanJordanKazakhstanKenyaKiribatiKorea, Democratic People's Republic ofKorea, Republic ofKuwaitKyrgyzstanLaosLatviaLebanonLesothoLiberiaLibyaLiechtensteinLithuaniaLuxembourgMacedonia, Republic ofMadagascarMalawiMalaysiaMaldivesMaliMaltaMauritaniaMauritiusMexicoMoldovaMonacoMongoliaMontenegroMoroccoMozambiqueMyanmarNamibiaNauruNepalNetherlandsNew ZealandNicaraguaNigerNigeriaNiueNorwayOmanPakistanPalestine, State ofPanamaPapua New GuineaParaguayPeruPhilippinesPolandPortugalQatarRomaniaRussiaRwandaSaint Kitts and NevisSaint LuciaSaint Vincent and the GrenadinesSamoaSan MarinoSão Tomé and PríncipeSaudi ArabiaSenegalSerbiaSeychellesSierra LeoneSingaporeSlovakiaSloveniaSolomon IslandsSomaliaSouth AfricaSouth SudanSpainSri LankaSudanSurinameSwedenSwitzerlandSyriaTaiwanTajikistanTanzaniaThailandTimor-Leste \(East Timor\)TogoTongaTrinidad and TobagoTunisiaTurkeyTurkmenistanTuvaluUgandaUkraineUnited Arab EmiratesUnited KingdomUruguayUzbekistanVanuatuVatican CityVenezuelaVietnamYemenZambiaZimbabweSubscribe[Please read our Privacy Policy.](https://www.oreilly.com/privacy.html)![production systems and data science systems](https://d3ansictanv2wj.cloudfront.net/image_5-0d8e25c02668e476dd491d457f605d89.jpg)Figure 5. Slide image courtesy of Mikio Braun.

If we put these two systems side-by-side, we get a picture like the Figure above. On the top right, there is the data science side, characterized by using languages like Python, or systems like Spark, but often with one-shot, manually-triggered computations, and iterations to optimize the system. The outcome of that is a model, which is essentially a bunch of numbers that describe the learned model. This model is then loaded by the production system. The production system is a more classical enterprise system, written in a language like Java, which is continually running.

The picture is a bit simplifying, of course. In reality, models have to be retrained, so that some version of the processing pipeline must also be put into place on the production side to update the model every now and then.

Note that the A/B testing, which happens in the live system, mirrors the evaluation in the data science side. These are often not exactly comparable because it is hard to simulate the effect of a recommendation, for example, offline, without actually showing it to customers, but there should be a link in performance increase.

Finally, it’s important to note that this whole system is not “done” once it is set up. Just as one first needs to iterate and refine the data analysis pipeline on the data science side, the whole live system also needs to be iterated as data distributions change, and new possibilities for data analysis open up. To me, this "outer iteration" is the biggest challenge to get right—and also the most important one, because it will determine whether you can continually improve the system and secure your initial investment in data science.

### Data scientists and developers: modes of collaboration

So far, we have focused on how systems typically look in production. There are variations in how far you want to go to make the production system really robust and efficient. Sometimes, it may suffice to directly deploy a model in Python, but the separation between the exploratory part and production part is usually there.

One of the big challenges you will face is how to organize the collaboration between data scientists and developers. “Data scientist” is still a somewhat new role, but the work they have to do differs enough from those of typical developers that you should expect some misunderstandings and difficulties in communication.

The work of data scientists is usually highly exploratory. Data science projects often start with a vague goal and some ideas of what kind of data is available and methods that could be used, but very often, you have to try out ideas and get insights into your data. Data scientists write a lot of code, but much of this code is there to test out ideas and is expected to not be part of the final solution.![data scientists and developers](https://d3ansictanv2wj.cloudfront.net/image_6-09fc7b089f2c0d1572f5f65bd204a9f7.jpg)Figure 6. Slide image courtesy of Mikio Braun.

Developers, on the other hand, naturally have a much higher focus on coding. It is their goal to write a system, to build a program that has the required functionality. Developers sometimes also work in an exploratory fashion, building prototypes, proof of concepts, or performing benchmarks, but the main goal of their work is to write code.

These differences are also very apparent in the way the code evolves over time. Developers usually try to stick to a very clearly defined process that involves creating branches for independent work streams, then having those reviewed and merged back into the main branch. People can work in parallel, but need to incorporate approved merges into the main branch back into their branch, and so on. It is a whole process around making sure that the main branch evolves in an orderly fashion.![branches for independent work streams](https://d3ansictanv2wj.cloudfront.net/image_7-37454ac57045ef55b82f07caf46db888.jpg)Figure 7. Slide image courtesy of Mikio Braun.  


