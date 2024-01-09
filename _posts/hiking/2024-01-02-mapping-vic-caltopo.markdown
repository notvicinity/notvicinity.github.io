---
layout: single
title:  "Mapping Vic Hikes Using Caltopo"
date:   2024-01-02 20:00:00 +1100
categories: Hiking
header:
    teaser: "/assets/images/teaser/teaser_caltopo_vic.PNG"
---

Fleeing the city at the end of the year in favour of the coast is an Australian tradition, one of the more important ones. I found myself mapping a hike in Wilson's Prom using Caltopo, my tool of choice.

I've written before about [Caltopo and mapping NSW hikes][nsw-caltopo] where I use the NSW [Spatial Information eXchange][six] as a custom layer but this hike is not in New South Wales...

## Victorian Mapping Resources

I found two official resources that looked like they could be useful as layers:

1. [SMES - Survey Marks Enquiry Service][smes]
2. [Vicmap digital viewer][vicmap-viewer]

Unfortunately I haven't been able to turn topographic information on with either of these, however they have proven valuable for walking tracks, water resources, and other landmarks. Combining this with the Caltopo default topographic options seems like the way to go.

## Finding the URL

To use these with Caltopo, we need to find a compatible URL which for us means either a Web Map Service (WMS) endpoint or a Tile Map Service (TMS) endpoint. Luckily for us, both of these resources do appear to use these standards.

Opening up web developer tools in my browser and then changing the map zoom or location while monitoring the network requests show a flurry of activity, most of which we can see is a call to a WMS endpoint

![SmesUI WMS Request](/assets/images/post_res/smes_network.png)

We can pull the URL out of these requests and feed them to Caltopo - either as it and using the auto-configure option or by manually updating to fit the URL template:

```
Vicmap Viewer:
https://base.maps.vic.gov.au/service?SERVICE=WMS&VERSION=1.1.1&REQUEST=GetMap&STYLES=&BBOX={left},{bottom},{right},{top}&WIDTH={tilesize}&HEIGHT={tilesize}&BGCOLOR=0xCCCCCC&FORMAT=image/png&EXCEPTIONS=application/vnd.ogc.se_inimage&SRS=EPSG:3857&LAYERS=CARTO_WM_256
SMES:
https://maps.land.vic.gov.au/geolassi/wms?SERVICE=WMS&VERSION=1.1.1&REQUEST=GetMap&FORMAT=image/png&TRANSPARENT=true&env=opacity:1&cql_filter=1=2&LAYERS=TICK_SMES_AVWS_LEVEL&styles=&firstTile=true&SRS=EPSG:7899&STYLES=&FORMAT_OPTIONS=dpi:159&WIDTH={tilesize}&HEIGHT={tilesize}&BBOX={left},{bottom},{right},{top}
```

and now we have lovely custom Victorian layers in our Caltopo maps!

![CalTopo Custom Layer](/assets/images/teaser/teaser_caltopo_vic.PNG)

[nsw-caltopo]: /hiking/mapping-nsw-caltopo
[six]: http://maps2.six.nsw.gov.au/
[vicmap-viewer]: https://vicmaptopo.land.vic.gov.au/#/discover-map
[smes]: https://maps.land.vic.gov.au/lassi/SmesUI.jsp