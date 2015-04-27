# Tutorial 1 - Deploying A Web Map to Amazon S3

## Description

This tutorial will walk you through the steps necessary to set up and deploy a Esri ArcGIS application from Esri's Github site  to Amazon's S3 (Simple Storage Service) product.  Using S3 you can host a static web application.  A static web application may sound super old school, but if you are using SaaS platforms such as ArcGIS.com, Mapbox, Cartodb, Firebase, and others you can make API calls via RESTful requests.  

You can use Amazon S3 buckets to host simple web applications that <b>do not require</b>:

* Application Server Side Code (.NET, Node.js, RoR, Java, PHP, and others)
* Security
* Load Balancing

## Pre-requisites

* ArcGIS.com Account
* Amazon AWS Account

## Setup development environment

[New to Github? Get started here.](https://github.com/)

For the purpose of this tutorial we will be using Esri's geoform-template application.  The GeoForm is a configurable template for form based data editing of a Feature Service.  The application is built for a mobile first approach.

<b> Step 1 </b> - Clone [geoform-template-js](https://github.com/Esri/geoform-template-js) Web Application from [Esri's Github site](https://github.com/Esri).

<p>Clone the application to your local working folder.</p>

<pre><code>git clone https://github.com/Esri/geoform-template-js.git
</code></pre>


## Resources

* https://aws.amazon.com/articles/Amazon-S3/5050
* https://github.com/Esri/geodev-hackerlabs
* http://blogs.esri.com/esri/arcgis/2014/09/25/the-geoform-graduates/

