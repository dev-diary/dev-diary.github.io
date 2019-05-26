
---  
title: How to set up custom domain for Github Pages with HTTPS  
image: /images/Automated-deployment-With-CircleCI.jpg  
author: Michal Fabjanski  
categories:  
    - Jekyll  
    - SSL  
    - Github  
    - Google  
layout: post  
---  
The purpose of this guide is to add a custom domain pointing to the website on Github Pages. The domain will use an SSL certificate. Finally, we'll add the domain to [Google](https://www.google.com/webmasters/tools/submit-url "Google"). The whole operation takes only a few minutes and can be done in a few steps.   
  
### Requirements:  
  
 - Purchased domain (I bought it on porkbun.com. You can buy domain anywhere, for example on [Google Domains](https://domains.google/ "Google Domains"))  
 - A github pages repository, e.g. https://github.com/username/username.github.io  
  
  
### Add custom domain to Github Pages settings  
Go to your github repository settings page:  
![devdiaries-settings](/images/devdiaries-settings.JPG)  
Add you custom domain name (www.domain) at Settings -> GitHub Pages -> Custom domain:  
![devdiaries-custom-domain](/images/customdomain-devdiaries.JPG)  
  
### Point your custom domain to your Github Page`s website  
If you also use Porkbun, you can easily point the domain to your GitHub pages using the guide: [Connect domain to Github Pages](https://kb.porkbun.com/article/64-how-to-connect-your-domain-to-github-pages "Connect domain to Github Pages")  
If you use Google Domains, select your domain in the Admin panel. Then go to **DNS> Custom resource records** and add the DNS records:   
- 185.199.111.153  
- 185.199.110.153  
- 185.199.109.153  
- 185.199.108.153  
![devdiaries-custom-domain](/images/dns-google.JPG)  
- Add the CNAME record: name - www, type - CNAME, answer/value - yoursite.github.io  
  
### Enable HTTPS for your GitHub pages website  
Go to your GitHub repository settings. Under Settings > GitHub Pages > Custom domain check the **Enforce HTTPS** checkbox.  
  
After a while (up to several hours) your domain should be available once with an SSL certificate. Go to https://yourdomain and check if you can see your website.  
  
### NET::ERR_CERT_COMMON_NAME_INVALID error  
If after entering **https**: //yourdomain you see a browser warning and **NET :: ERR_CERT_COMMON_NAME_INVALID** error - make sure that you put **www**.yourdomain under Settings > GitHub Pages > Custom domain.  Adding the www prefix should fix the problem.

###  Verify Domain in Google Search Console via DNS

To add your website to Google search, you must verify your domain on [Google Search Console ](https://search.google.com/search-console). 
* Select **Domain** property type:http://
![devdiaries-custom-domain](/images/add-domain.JPG)  

* Copy the TXT record you’ll get:
![devdiaries-custom-domain](/images/DNS-Verify.JPG)  
* Log into your domain`s admin panel. 
*  Add a new DNS record and select TXT as a record type.
* Fill  fields with the following information: **name/host** - empty, **TTL** - 86400 or default, **answer/text** -  your Google verification text from previous step.
* Click **Verify**.

your domain can not be verified right away in Search Console:
![verification-failed](/images/verification-failed.JPG)  

It may take a few minutes (up to 48 hours) to update your DNS. In my case, the domain was verified in 10 minutes. That`s all! There’s no guaranteed time-frame for how long it will take for your website to appear in Google’s search results. It can take anywhere from hours to weeks. 