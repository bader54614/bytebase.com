---
title: From S3 to DataZone, a 16-year Odyssey of the AWS Data Portfolio
author: Tianzhou
published_at: 2023/01/06 08:30:00
feature_image: /static/blog/aws-reinvent-2022-data-review/s3-to-datazone.webp
tags: Industry
featured: true
description: In re:Invent 2022, AWS announces DataZone, the service to manage data assets. This completes the AWS Data Stack and whole jounery starts from S3, the first AWS service announced in 2006.
---

AWS 2022 re:Invent just came to a close in Las Vegas, and compared to last year's 2021 re:Invent, which took place right after the epidemic, the turnout was unprecedented, with over 50,000 attendees by official count. This was Adam Selipsky's second offline re:Invent appearance as the head of AWS, and in Adam's Keynote, he kicked off the event with a three-minute set-up of the stars

![_](/static/blog/aws-reinvent-2022-data-review/galaxy.webp)

Just to introduce the first topic of the Keynote, Data

![_](/static/blog/aws-reinvent-2022-data-review/talking-data.webp)

The starting point for AWS data product line is also the starting point for AWS. Adam said at the Keynote that AWS has the most comprehensive data product matrix in the industry, so let's take a look back at the evolution of the AWS data product line with this re:Invent launch.

## Evolution of AWS Data Products

### S3 - Simple Storage Service

> AWS classifies S3 as Storage, not Data, but S3 is closely related to the data side, so it is discussed together.

S3 was released in March 2006 and is the oldest AWS service, marking the birth of AWS. S3 is also the core service, and if we were to subtract from AWS services, the last one left would definitely be S3.

Of course there is nothing simple behind providing simple services, and Amazon CTO Werner Vogels is a big fan of servitization, using S3 as a case study in every one of his Keynotes. This year he again mentioned that S3 has more than 235 microservices (for comparison, the typical number of microservices for an Internet service is about 5).

![_](/static/blog/aws-reinvent-2022-data-review/s3-2022.webp)

In 2019, however, the number of microservices in S3 is 262. It appears that S3 has still done a series of internal thinning exercises.

![_](/static/blog/aws-reinvent-2022-data-review/s3-2019.webp)

The importance of S3 can also be seen from another perspective. the accident of S3 in the US East in 2017, which caused widespread Internet services to go down, also made many people realize for the first time that S3 has actually become the infrastructure of the Internet (backbone).

![_](/static/blog/aws-reinvent-2022-data-review/s3-outage.webp)

And it's because S3 provides the simplicity, or the basic atomic power, that there are so many possibilities on top of it. I'm sure the designers of S3 didn't expect S3 to be the basis for a Data Lake, because there was no such thing as a Data Lake back then :)

![_](/static/blog/aws-reinvent-2022-data-review/s3-data-lake.webp)

### Modern Data Stack

Starting with S3, the AWS data product line has grown and developed into the **Modern Data Stack** with five verticals and three horizontals:

**Five Verticals** represents the 5 circles on the chart, Databases, Analytics, Business Intelligence (BI), Data Lakes, and Machine Learning.

**Three Horizontals** represents the Catalog and Governance in the middle of the diagram, and Integration implied by the connecting lines.

![_](/static/blog/aws-reinvent-2022-data-review/data-stack-timeline.webp)

#### Five Verticals

1. **Databases**: Application databases that support online business, the core of which are relational (RDBMS) and non-relational (NoSQL), each of which has undergone a product evolution.

- Relational: 2009.10 RDS -> 2014.11 Aurora
- Non-relational: 2007.12 SimpleDB -> 2012.1 DynamoDB

1. **Analytics**: Analytical database / data warehouse, Redshift has been the only product, and this year also happens to be the 10th year of Redshift. In fact, Redshift was originally an acquired product, and its predecessor was ParAccel's PostgreSQL-based magic transformation.

1. **Business Intelligence (BI)**: QuickSight, launched in 2015, is relatively not AWS's strong point. But it's interesting to note that Adam's last job happened to be CEO of Tableau, the leader in BI.

1. **Data Lakes**: The hottest concept in the data space in the past two years, AWS also laid the groundwork early on in this area:

   1. **storage**: 2006.3 released S3, mentioned earlier, somewhat unintentionally into the data lake field roots.
   1. **calculation**: 2009.4 released EMR (Elastic MapReduce), of course, it is no longer only run Hadoop MapReduce, Spark, Flink, TensorFlow, Ray various execution engines can be disliked.
   1. **query**: 2016.11 release of Athena, providing an interface to query S3 and other data sources via SQL.

1. **Machine Learning**: the earliest inclusion is the 2016 re:Invent on the launch of the three Musketeers, image recognition Rekognition, text recognition Polly, speech recognition LEX.

![_](/static/blog/aws-reinvent-2022-data-review/introduce-ai.webp)

That year, I think it was also because Google Cloud AI was very aggressive, so AWS was a bit rushed. But AWS adjusted right away, and one year later, launched SageMaker, a cornerstone product in the AI / ML front.

![_](/static/blog/aws-reinvent-2022-data-review/introduce-sagemaker.webp)

#### Three Horizontals

- **Integration**: allows users to move data from System A to System B, as well as do data transformations right in a single system. This is also an iterative product line, upgraded from 2012.12 Data Pipeline to 2016.12 Glue.
- **Governance**: 2018.11 Lake Formation, a product for data lakes. Because data lakes are much larger than data warehouses and lack structured information, if they are not managed, they are like a pile of building blocks left there, meaningless, and we don't know where someone has taken a piece. However, the boundary between it and DataZone will be somewhat blurred, which will be discussed later.
- **Catalog**: 2022.11 DataZone, a product launched by re:Invent, will be expanded later in the new product explanation.

## Data Gravity

![_](/static/blog/aws-reinvent-2022-data-review/data-gravity.webp)

This is also a concept that was heard at Keynote

- Resources follow the data, and where the data is, everything else is. So several of the major shared cloud vendors do not charge for the data traffic that comes in (screenshot from AWS official website)

And out of the data, the collection is unusually high, Cloudflare last year also wrote a special article on this for AWS (screenshot from https://blog.cloudflare.com/aws-egregious-egress/)

![_](/static/blog/aws-reinvent-2022-data-review/cloudflare-markup.webp)

- Data is accumulating more and more, and the variety of data and database types is getting richer. The ability to harness data is a natural downward trend.

There are three key early AWS product:

1. In the giant inside the first to enter the cloud market, AWS is 2006 has launched S3, EC2, Google is launched in 2008 Google App Engine (GAE), Ali cloud is 2009, and Azure will have to wait until 2010.

1. Bet on a VM-based EC2 solution rather than jumping straight to PaaS. Google has taken a more aggressive approach to the latter, and has taken Azure off course. As it turns out, users are still lift-and-shift to the cloud rather than leapfrog to a cloud-native architecture.

1. The early launch of a variety of standalone data offerings based on the perceived gravitational pull of data quickly put it ahead of Rackspace, the earliest public cloud market leader, which also started with managed cloud hosting. On the other side of the spectrum, Google Cloud's GAE offers a complete PaaS platform, with all data services initially coupled to GAE. Google Cloud's S3 equivalent, GCS, was not released until 2010, four years after the launch of S3. In the AWS system, data and compute are two separate services, with data coming up first, and compute naturally following data because of data gravity. In the Google Cloud system, data and compute are coupled. Google's adoption of the out-of-date Serverless compute runtime (Runtime) makes it necessary for users to transform the compute runtime before they can use data services, leading only new Internet companies like Snapchat, which are willing to experiment with new development paradigms, to choose the family bucket provided by GAE.

![_](/static/blog/aws-reinvent-2022-data-review/intuit-data-gravity.webp)

In addition to respecting the objective fact of data gravity, AWS is also doing Data AntiGravity, and this time we have Intuit on stage to talk about the same topic, and we will start to introduce several new releases around this topic.

## Explanation of the new release features of AWS re:Invent 2022 data products

### DataZone

![_](/static/blog/aws-reinvent-2022-data-review/datazone.webp)

DataZone, the most significant release in the AWS re:Invent data line, was also featured in Adam's Keynote. The introduction of DataZone is "A data management service to catalog, discover, share and govern data", which complements the only big module missing in the entire data line, data asset management. Its product introduction also mentions Govern, and Lake Formation is a governance solution specifically for data lake scenarios, so there is some boundary overlap between DataZone and Lake Formation in this area, and the subsequent integration should be carried out. However, I believe that DataZone will be the cornerstone product of AWS data line and the bearer of DataOps in the future, taking the role of opening up the two veins of each data system. Based on DataZone, we will develop more upper-level applications such as data security and business insights.

Still, AWS released DataZone too late; Google Cloud's comparable product, Dataplex, launched in 2021, and many AWS users have deployed similar solutions. I can think of several reasons why AWS chose to release Lake Formation for data lakes only at this point in 2018, rather than taking a direct step to DataZone.

1. To make a data platform that integrates all data systems requires too many resources to coordinate, and the organizational structure of AWS was not ready at that time.

1. At that time the data lake was on fire, Databricks, Snowflake gave a lot of pressure, so quickly first out a product for the data lake.

The next evolution of Lake Formation can take two paths:

1. Similar to SageMaker, developed into Lake Studio, become the development platform of the data lake, Governance, Catalog these underlying capabilities or to DataZone.

1. Integrate with Redshift Workbench to develop the Lakehouse development platform, which is an integrated lake and warehouse.

### Aurora zero-ETL integration with Redshift

![_](/static/blog/aws-reinvent-2022-data-review/aurora-to-redshift.webp)

ETL synchronization of Aurora data to Redshift without manual user configuration of ETL tasks. I haven't seen more detailed information, but it is said to be based on MySQL binlog, the same solution as AliCloud DTS (AliCloud database product line is still very strong).

### Auto-copy from Amazon S3 to Redshift

![_](/static/blog/aws-reinvent-2022-data-review/s3-to-redshift.webp)

Similar to the one above, but the data source is changed to S3, and there is no ETL function for now. But this is also a solution to a high-frequency scenario, and also paves the way for further ETL solutions in the future.

The above two features as a whole kick off AWS' move towards zero-ETL. The attribution of data can be divided into four main categories.

1. data in the online transaction database
1. data in the data warehouse
1. data in the data lake
1. data in third-party systems such as Salesforce, HubSpot, etc.

In order to achieve zero-ETL, there are two ways to integrate data, one is to integrate database systems, for example, like HTAP database, there is a set of TP and AP engine underneath, whether the data is one set or two sets, the user does not need to care, this is represented by PingCAP's TiDB and Google's AlloyDB. The other way of thinking is to let the data in their own system (the best of the breed), but optimize the flow between data as much as possible, AWS is currently the representative of the latter idea. The former idea is architecturally advanced, while the latter is more pragmatic.

After talking about the number of warehouses, we will introduce two new releases in online databases

### RDS Blue Green Release

![_](/static/blog/aws-reinvent-2022-data-review/rds-blue-green.webp)

![_](/static/blog/aws-reinvent-2022-data-review/rds-blue-green-use-case.webp)

A practical feature for database change scenarios, the scene erupted into a loud cheer when this feature was introduced. This year many databases have started to invest in development workflows (R&D is painful), like PlanetScale, Neon, and RDS finally started to do something in this area after 13 years of launch. Although the scenario of Schema Changes overlaps with our Bytebase, it is a good thing that more companies in the industry are providing solutions for this kind of scenario, so that more people can realize that it is not OK to connect directly to the database for schema changes. Of course RDS has the added benefit of being able to sell twice as many RDS instances, and RDS itself has a very high margin.

### Trusted Language Extensions for PostgreSQL

![_](/static/blog/aws-reinvent-2022-data-review/tle.webp)

I understand that AWS is the vendor with the most experience in PostgreSQL kernel development in all public clouds. For security and stability reasons, PostgreSQL instances on the cloud can only be installed with AWS-specified extensions, so if the business team has its own business requirements, there is no way to write new extensions. This is the problem that TLE wants to solve. TLE provides some hooks that allow development teams to develop their own plugins in this framework and then have the DBAs help install them on the instances, while ensuring security and stability. open a hook for password checking.

![_](/static/blog/aws-reinvent-2022-data-review/tle-hook.webp)

This is a little bit of AWS giving back to the open source community, and over the last 10 years, there has been a lot of drama between the entire AWS data product line and open source commercial companies, so let's go on to talk about the evolution of their previous relationship.

## AWS and the game of open source commercial companies

Most of the more successful open source commercial companies today are focused on data product lines. Together, these companies have the volume to play with AWS, and the evolution of the relationship between AWS and these open source commercial companies can be summarized by the Tuckman Team Development Model.

### Forming

The first encounter between AWS and open source commercial companies was around the Hadoop ecosystem, when the whole industry was still exploring open source business models, such as whether to provide public cloud services or do private deployments. The Hadoop ecosystem of Cloudera, Hortonworks, and MapR chose to deploy privately. The simple and brutal computational model of MapReduce, which started hundreds of EC2 instances for a random task, was a money printing machine for AWS, and then Hive provided SQL query capability, which further expanded the audience and accelerated the speed of money printing. The speed of printing money was further accelerated.

It's interesting to note that the entire Hadoop ecosystem started with a Google paper based on internal MapReduce, which is itself a poor man's version of MapReduce, and it's this less efficient implementation that brings the best scenario to AWS EC2. Google Cloud's counterpart to AWS EMR, Dataproc, was only launched in 2015, six years behind.

Whether intentionally or unintentionally, AWS has achieved great commercial success by using open source software developed by others at a time when open source commercialization was in its infancy, but it has also given AWS a bad name for sucking the blood out of the open source community.

### Storming

After Hadoop, a number of great open source data products emerged, as well as commercial companies based on these products. And because we all started with open (permissive) open source certificates, such as Apache, MIT, so that the big public cloud companies like AWS can also immediately bring, and then integrated with other services on the AWS platform, and soon be able to launch a very competitive distribution. This makes those open source commercial companies sit up and take notice, because after all, the majority of open source product development is done by them, and AWS can easily sit back and take advantage of the AWS platform to compete directly with these open source commercial companies. The most intense of these was Elastic's direct naming of "Amazon: NOT OK - why we have to change Elastic licensing", and the open source projects changed their credentials to stop the public cloud vendors' white whoring during that time.

The dichotomy between AWS and open source commercial companies is a natural part of the industry's evolution. People found that open source products, especially those in the data domain, could generate huge business value by product + Cloud instead of Redhat's service model, so they naturally flocked to them. The existing rules of the open source community can not adapt to the new open source business model, both sides can only test each other, as far as possible to occupy the moral high ground, to get more territory for themselves. Open source commercial companies say that public cloud service providers are prostitutes, and public cloud service providers don't care, thinking that you open source commercial companies are burning VC checks and using open source as a means to attract traffic, and your hands are just as sticky with the smell of copper. After all, open source projects like PostgreSQL, which are purely community-run, are doing just fine.

### Norming

Fortunately, in the past two years, the confrontation between the two sides began to ease, like the beginning of the year, Elastic also reached a settlement with AWS. Open source commercial companies themselves are also users of cloud vendors, their own services to run on the VMs, k8s and other services provided by cloud vendors, they also want to do integration with cloud vendors' services to provide more competitive products, they also need AWS such distribution procurement channels to improve their business efficiency. For cloud vendors, first of all, the market is not just one service provider, while the cloud market still has huge growth space, so there is no need to choose zero-sum game now. And with a foundation of cooperation, Marketplace gives both sides a platform for collaboration, as seen in AWS' Marketplace, where third-party services are also listed in front of its own services.

![_](/static/blog/aws-reinvent-2022-data-review/marketplace.webp)

### Performing

When re:Invent was held this year, MongoDB posted an enthusiastic article looking back at the last decade of collaboration with AWS. While the article was related to the author Matt Asay's own experience, first at Mongo, then at AWS, and now back at Mongo, it was a surprise to see such an article on an official blog, since Mongo and AWS are in direct competition. Let's just say that the relationship between an open source commercial company like Mongo and a cloud platform like AWS is a delicate one, but it seems that we are gradually finding ways to find common ground while preserving differences (and it's definitely a good move to hire people like Matt who have favors on both sides).

Some people feel that open source with commercial elements is not pure. But would you rather the open source software you rely on be a product of individual hobbyists hiding in a dark room, generating electricity with love, and maintaining it in their spare time? Or is it a product with a clear business model and a full-time team to maintain it?
And is open source for commercial purposes a different kind of purity? Like Elastic and AWS, we are all driven by business interests, no moral abductions, one minute we are at war, the next we are hooking up.

![_](/static/blog/aws-reinvent-2022-data-review/xkcd.webp)

## Future Outlook

![_](/static/blog/aws-reinvent-2022-data-review/data-stack-matrix.webp)

With the launch of DataZone, the last missing piece of the AWS data product matrix has been added, and there are two major things I'm looking forward to next.

### Endgame oriented zero-ETL

re:Invent on AWS has expressed will go in the direction of zero-ETL, but the zero-ETL related features introduced this time, the underlying still have to do transfer between different data storage systems. But architecturally speaking, like Google's AlloyDB, the same data, separate OLAP, OLTP execution engine is more advanced. On the other hand, we can also see that AWS RDBMS and NoSQL have been iterated once (RDS -> Aurora, SimpleDB -> DynamoDB), while Redshift, one of the Three Musketeers, is still roughly 10 years old (not counting its predecessor, ParAccel, which started in 2006). Even though Redshift has made many optimizations (such as last year's release and this year's GA serverless), the top-level design is still the product of Snowflake, Google BigQuery's previous generation. And now there is a new scenario of data lakes, where data is placed on S3, and AlloyDB has already implemented a hybrid OLAP/OLTP engine based on S3-like storage. So I'm wondering if AWS' next big move will be to launch a brand new database based on S3, with a collection of TP, AP and Lake, with a name like ALT = A(nalytical) + L(ake) + T(ransactional).

![_](/static/blog/aws-reinvent-2022-data-review/alt.webp)

### More mature Marketplace and eco-collaboration

In addition to the opening Keynote, AWS CEO Adam Selipsky's only other participation was the Partner Keynote, which shows the importance AWS places on its ecological partners. The Marketplace section of Partner is a core position that allows AWS to move from pure technical enablement to commercial enablement, enabling AWS and open source commercial companies to compete on the technical product level but achieve win-win results on the commercial level. The difficulty of this job can be seen in the fact that the head of AWS Partner has changed hands several times in the past few years.

## Next Chapter

![_](/static/blog/aws-reinvent-2022-data-review/s3-to-datazone.webp)

From S3, a simple file storage service, to DataZone, a one-stop data asset management platform from re:Invent, AWS has spent more than 16 years telling a data story. I'm sure the creators of S3 didn't foresee that a cloud service that was meant to store files would give rise to new categories like cloud data warehouses and data lakes, and would likely become the cornerstone of the next generation of databases.
On top of the technology, AWS today has the responsibility of a platform. The Guest Speakers chosen for Adam's keynote are Engie, who is exploring green energy, Siemens, who is exploring space, and Lyell, who is exploring molecularly targeted cancer treatments. Its platform is carrying the business of expanding the boundaries of civilization.

![_](/static/blog/aws-reinvent-2022-data-review/guest-speaker.webp)

And a platform that can balance immediate business interests and long-term idealism can guide the entire industry to the distance, so let's follow AWS and enter its next data story.
