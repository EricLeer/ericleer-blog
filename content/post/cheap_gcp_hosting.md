---
title: "Hosting static pages with google cloud platform on the cheap"
date: 2020-12-01T09:17:00+01:00
draft: true
tags:
  - gcp
---
In this day and age static website are making their reentry again. They have the big advantages of being fast, secure and having a small footprint. Especially this last point makes it suitable for many cheap hosting options. Gitlab and Github pages give you options to host a static page for free, which has been described already many times. 

Another option is to use one of the public cloud providers. Both on AWS and azure you will find similar options, but in this blog I will dive into the different options that exist within gcp. These options entail google cloud storage, firebase, appengine, cloud run and compute engine.

## Hosting on google cloud storage
The first option that shows up when wanting to host a static website is to host it directly from Google Cloud Storage (GCS). This gives you an easy performant way website that scales also scales if your application would become a hit. 

Google has 2 good guides on how to set this up for [http](https://cloud.google.com/storage/docs/hosting-static-website-http) and [https](https://cloud.google.com/storage/docs/hosting-static-website). The http options is basically free for small websites/loads, the https version does incur some costs. 

**HTTP**  
The guide for hosting with http let's you direct your dns to the bucket with a CNAME record. This can be a bit of a problem if you where planning to use a toplevel domain (example.com) instead of subdomain (sub.example.com), since it is not possible to create a CNAME record for a toplevel domain. One possible workaround is to set a CNAME record for a subdomain and then redirect your toplevel domain to the subdomain. Not all DNS providers supply this option though. 

If this is not a problem for your planned usage this is a really cheap option to host your website. Storage costs 2 cents per GB, networking 12 cents per GB and basic operations 5 or 0.4 cents per 10,000 operations. For a basic small/medium sized website with not to high traffic this would lead to a cost of about 1 dollar per month. If your load is considerably lower this option is basically free.

**HTTPS**  
It might be that hosting on a subdomain, or using the above rerouting option is not a possibility. It could also be possible that hosting on http is not wanted since using http over https could result in a hit in SEO. In those case a load balancer has to be put in front of the bucket. This load balancer lets you add an ssl certificate. The guide from Google only sets you up for hosting over https, to also be able to serve clients trying to acces on http an additinal http-to-https redirect should be added. Just like the hosting setup there is a really good [guide](https://cloud.google.com/load-balancing/docs/https/setting-up-http-https-redirect) on how to set this up.

Overall this would set you up with a really performant and scalable solution. The downside is that on top of the GCS costs previously mentioned now also cost for the load balancer is added. The prices for the load balancer mainly fall under the [forwarding rules](https://cloud.google.com/vpc/network-pricing#forwarding-rules-pricing-examples) which cost 2.5 cent per hour for the first 5 forwarding rules. This adds up to about 18 dollars per month, which is quite a bit more then the strictly http setup.

## Firebase hosting
A second option is firebase hosting. According to Google firebase is their *"mobile platform that helps you quickly develop high-quaility apps"*. What it also lets you do is quickly, and cheaply host a static website!

Setting it up is really easy, I followed the [following guide](https://medium.com/@aleemuddin13/how-to-host-static-website-on-firebase-hosting-for-free-9de8917bebf2) which utilizes the firebase cli, but many more resources can be found.
The firebase cli deployment is really fast. In the initialization process you setup the folder which contains your page. With the `firebase deploy` command this folder then gets uploaded to firebase. Which instantly sets your website up with an ssl certificate. It cost me arround 15 minutes to set everything up and get my website going.  

The usage of firebase hosting is billed by the amount of GB stored and transferred. Stored data is free up to 10GB after which it costs 2.6 cents per GB. The GB transferred include all data that is either uploaded or downloaded (so this also includes all te downloads of your users) and is free up to 360MB/day after which it costs 15 cents per GB. So for low usage website this is a very cheap way to host your website. The big plus is that with these costs an ssl certificate is included and using your own domain is easily set up.

## Cloud run/App engine
In very short cloud run and App engine are 2 sides of the same medalion. Cloud run lets you deploy a docker container in a serverless environment. With app engine you can define a .yaml file with which it builds a docker image of you app which is ten hosted. 

The cost of both of these options are fairly similar in that you only pay for what you use. Cloud run has a base free tier, which only incurs cost beyond the free tier. The cost of App engine is based on which instance you use. If you utilize the gcp free plan, which gives you a free f1-micro node, you don't pay anything for this setup as long as your usage stays below a single instance month. With seting up you app on App engine you also get a free ssl certificate. 

More info on hosting on google cloud run can be found [here](https://cloud.google.com/run) and [here](https://daniel-azuma.com/blog/2019/07/01/deploying-my-blog-to-google-cloud-run). More on hosting on app engine can be found in [this](https://github.com/ncruces/appengine-hosting) github repo.

##  Hosting on Compute engine
The final option is of course to set up your own webhosting on compute engine. The really cheap instances (f1-micro, e2-micro) go for around 5 to 6 USD per month. On top of that a static ip and ssl certificate would be needed, making this quite a bit to set up.Altough you can learn a lot of running your own webserver, deploying to your custom vm and making sure everything keeps running is quite a bit more work. Furthermore for just hosting a static website this setup would also be total overkill. 

When we look at the costs there is an option to reduce them a bit. With the free gcp plan you can get a free f1-micro node, which save some costs. To add an ssl certificate you run into the same problem as gcs in that you need to use a load balancer which come with the minimum cost of 18 dollars per month. 

# Conclusion
Fareout the easiest option to quickly get going with your static site on gcp is to host it on firebase. The cli that is supplied makes it easy to set up your project. For the rest it is extremely scalable and an ssl certificate is included. When a little more customization is needed app engine can be used. For app engine you do need to setup your own webserver though. If having your website just accesible over http is fine google cloud storage would also work great. 

The cloud environment is moving constantly in terms of pricing and new options. So I'm sure many more options exists that can also be used for free.