#Step 1 Create Tile Package in ArcGIS Desktop (or ArcGIS Server)
  Tip: Enable runtime in GIS options
  ##Create Tile Package 
  
  *Do we mention here that an AWS AMI could also do the processing for you, if for example you used gdal to make tiles and put in S3 bucket, or just not worry about it?*

#Step 2 Upload Tile Package to S3 (create an AWS account) - talk about free account/costs here?
  
##Create S3bucket for the tiles
  
##Use S3 Browser to upload packages
  
##Set S3 settings to allow connection to the imagery
    Blair - explain how to set this up
  
  
#Step 3 Add S3 location to webpage/app

![Image of ESRI JS widget](https://www.arcgis.com/sharing/rest/content/items/97027b553de24137909ce93994698062/info/thumbnail/Screen_Shot_2013-09-17_at_9.22.53_AM.png)

##Find ESRI JS API example, would like to use swipe map with two versions of Pierce County LiDARto illustrate changes 2002/2010 

can we use this widget? [Layer Swipe](https://developers.arcgis.com/javascript/jssamples/widget_swipe.html) *need to edit html below to work with example*

```html
<!DOCTYPE HTML>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="initial-scale=1, maximum-scale=1,user-scalable=no">
  <title>Layer Swipe</title>
  <link rel="stylesheet" href="http://js.arcgis.com/3.13/esri/css/esri.css">
  <style>
    html, body, #map {
      padding:0;
      margin:0;
      height:100%;
    }
  </style>
  <script src="//js.arcgis.com/3.13/"></script>
  <script>

    require([
      "esri/map", 
      "esri/dijit/LayerSwipe",
      "esri/arcgis/utils",
      "dojo/_base/array",
      "dojo/domReady!"
    ], function(
      Map, LayerSwipe, arcgisUtils, array 
    )  {

      var mapDeferred = arcgisUtils.createMap("62702544d70648e593bc05d65180fd64", "map");
      mapDeferred.then(function(response){

        var id;
        var map = response.map;
        var title = "2009 Obesity Rates";
        
        //loop through all the operational layers in the web map 
        //to find the one with the specified title;
        var layers = response.itemInfo.itemData.operationalLayers;
        array.some(layers, function(layer){
          if(layer.title === title){
            id = layer.id;
            if(layer.featureCollection && layer.featureCollection.layers.length){
              id = layer.featureCollection.layers[0].id;
            }
            return true;  
          }else{
            return false;
          }
        });
        //get the layer from the map using the id and set it as the swipe layer. 
        if(id){
          var swipeLayer = map.getLayer(id);
          var swipeWidget = new LayerSwipe({
            type: "vertical",  //Try switching to "scope" or "horizontal"
            map: map,
            layers: [swipeLayer]
          }, "swipeDiv");
          swipeWidget.startup();
        }
      });

    });
  </script>

</head>
<body>
  <div id="map" class="map">
    <div id="swipeDiv"></div>
  </div>
</body>
</html>
```
  
#Step 4 Use Cloudfront Content Delivery Network to Optimize access to your imagery
  
##Define origin server (your S3 bucket) - this is the actual location of the files/data, the original location
  
##Upload data (tile package) to S3 bucket (your origin server)
  Since we're using an Amazon S3 bucket as an origin server, we can make the objects in our bucket publicly readable, so anyone who knows the CloudFront URLs for our objects can access them. We also have the option of keeping objects private and controlling who accesses them. 

  *If you need to keep your data private see: [Serving Private Content through CloudFront](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/PrivateContent.html) for more information.
  
##Create a CloudFront distribution and start using that domain name to develop your web site/apps

The distribution part tells CloudFront which origin servers to get your files from when users request the files through your web site or application and gives you a domain name. Now use the domain name that CloudFront provides for your URLs. For example, if CloudFront returns d111111abcdef8.cloudfront.net as the domain name for your distribution, the URL for logo.jpg in your Amazon S3 bucket (or in the root directory on an HTTP server) will be http://d111111abcdef8.cloudfront.net/logo.jpg.

##
  
  
  
  
  
  
  
  
