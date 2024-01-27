---
title: "Using Rayshader, GIS, and OpenstreetMap for Shenandoah National Park Hikes - R"
excerpt: ""
classes: wide
header:
  overlay_image: /assets/images/rayshaderShenNatPark/shenandoah_highresTrim.png
  overlay_filter: 0.4 # same as adding an opacity of 0.5 to a black background
  caption: "Using Rayshader rendering"  
---


# Shenandoah National Park

The videos embedded use both html formatting and kramdown. Since different browsers parse kramdown and html tags differently, I added both the html and kramdown version for full coverage (so that most browsers can view the videos regardless). Hence, if there is a broken link icon next to a video, please ignore - that's just the same copy. 
{: .notice--info}


Shenandoah National Park, located in the state of Virginia, is a breathtaking expanse of natural beauty that encompasses the crest of the Blue Ridge Mountains. Established in 1935, the park covers over 200,000 acres and is renowned for its stunning vistas, dense forests, and diverse wildlife. Skyline Drive, a scenic highway that stretches for 105 miles along the park's spine, offers visitors panoramic views of the Shenandoah Valley to the west and the Piedmont region to the east. Hiking enthusiasts can explore a network of over 200 miles of trails, including a portion of the famous Appalachian Trail. The park is a haven for outdoor recreation, with opportunities for camping, birdwatching, and observing the vibrant fall foliage. Shenandoah National Park provides a serene escape into nature, allowing visitors to connect with the great outdoors and experience the tranquility of this protected wilderness.


The image below showcase the Shenandoah National Park sprawling mountains. At the top left are the George Washingtion National Forest and at very top left, are the Appalachian Mountains in West Virginia. Data was taken from [USGS](https://apps.nationalmap.gov/downloader/), and visualized using [Rayshader](https://www.rayshader.com/), following the work of [Spencer Schien](https://spencerschien.info/post/data_viz_how_to/high_quality_rayshader_visuals/).

![Shenandoah-National-Park](/assets/images/rayshaderShenNatPark/shenandoah_highresTrim.png){: .align-center}

Part of my motivation in this project is due to the many hikes I have done in the Shenandoah National Park. A few of these trails are visualized below using Openstreetmap via R. An excerpt of the code is all the way below. 

## McAfee Knob Trail

McAfee Knob, situated within Shenandoah National Park in Virginia, is a renowned and iconic landmark along the Appalachian Trail. This prominent rocky outcrop offers breathtaking panoramic views of the surrounding Blue Ridge Mountains and the Shenandoah Valley. Hikers and nature enthusiasts are drawn to McAfee Knob for its stunning scenery and the rewarding hike it takes to reach the summit.

<video controls="" width="80%" height="80%" muted="" loop="" autoplay="">
<source src="/assets/images/rayshaderShenNatPark/mcafeeknob.mp4" type="video/mp4">
</video>

![mcafee-knob](/assets/images/rayshaderShenNatPark/mcafeeknob.mp4)

## Old Rag Trail 
Old Rag Trail is one of the most popular and challenging hikes in Shenandoah National Park, Virginia. Renowned for its rugged terrain and stunning views, this 9.2-mile loop takes hikers on an exhilarating journey through rocky outcrops, dense forests, and exposed ridges. The highlight of the trail is the summit of Old Rag Mountain, which stands at 3,291 feet and provides unparalleled panoramic views of the surrounding landscapes.

<video controls="" width="80%" height="80%" muted="" loop="" autoplay="">
<source src="/assets/images/rayshaderShenNatPark/oldrag.mp4" type="video/mp4">
</video>

![old-rag](/assets/images/rayshaderShenNatPark/oldrag.mp4)

## Hawskbill Summit Trail
Hawksbill Trail in Shenandoah National Park is a short yet rewarding hike leading to the highest peak in the park, Hawksbill Summit.  Once at the top, hikers are treated to stunning views of the surrounding Blue Ridge Mountains and Shenandoah Valley. The relatively moderate difficulty level makes Hawksbill Trail accessible to a wide range of visitors, making it a popular choice for those seeking a shorter hike with a spectacular payoff in Shenandoah National Park.

There are many trails possible to reach the summit. In the video below, Upper Hawksbill Trail and the Lower Hawksbill Trail are colored in red, while the Skyline Drive is represented by the grey line.
<video controls="" width="80%" height="80%" muted="" loop="" autoplay="">
<source src="/assets/images/rayshaderShenNatPark/hawksbillloop.mp4" type="video/mp4">
</video>

![hawksbill-loop](/assets/images/rayshaderShenNatPark/hawksbillloop.mp4)

## Dark Hallow Falls Trail
Dark Hollow Falls Trail in Shenandoah National Park is a brief but enchanting hike leading to the captivating Dark Hollow Falls. The trail is approximately 1.4 miles round trip, descending through a lush forest to reach the base of the falls. The cascading waters of Dark Hollow Falls create a serene and picturesque setting, making it a favorite spot for nature lovers and photographers. The ease of access and the beauty of the falls make this trail a popular choice for visitors looking to experience the natural wonders of Shenandoah National Park in a short and enjoyable excursion. 

Beyond the Dark Hallow Falls is the Rose River Trails not shown in the video below. White dashed lines are the river lines, and the grey line represents Skyline Drive. 
<video controls="" width="80%" height="80%" muted="" loop="" autoplay="">
<source src="/assets/images/rayshaderShenNatPark/darkhallow.mp4" type="video/mp4">
</video>

![dark-hallow](/assets/images/rayshaderShenNatPark/darkhallow.mp4)

## Dark Hallow Falls Loop Trail
White Oak Canyon Trail is a breathtaking hiking experience nestled within Shenandoah National Park, offering outdoor enthusiasts a captivating journey through lush forests and stunning landscapes. This popular trail is renowned for its cascading waterfalls, with a series of six major falls, each more impressive than the last, creating a symphony of sounds as water rushes over moss-covered rocks. The trail spans approximately 4.6 miles and is well-marked, providing both novice and seasoned hikers with an invigorating adventure. As you traverse the path, you'll encounter picturesque views of the Blue Ridge Mountains and the Shenandoah Valley, making it a photographer's paradise. The trail's diverse ecosystems showcase the region's rich biodiversity, and the soothing sounds of flowing water contribute to the overall serene ambiance. 

As shown below, there are three possible starting point for the loop. Two coming from Skyline drive and one coming from Weakley Hollow Road (not shown but where the river diverges into three paths). Red indicates the trail, grey line iundicate Skyline drive, and the white dashed lines indicate the river lines. The Skyline drive may seem familiar - and it is, the upper trail head of the loop is in the opposite side of the Upper Hawksbill Summit Trail!

<video controls="" width="80%" height="80%" muted="" loop="" autoplay="">
<source src="/assets/images/rayshaderShenNatPark/whiteoak.mp4" type="video/mp4">
</video>

![dark-hallow](/assets/images/rayshaderShenNatPark/whiteoak.mp4)

## Code Excerpt

The code below is for White Oak Canyon Loop Trail . On all the trails above, most effort was done with the filtration of the trail features. 
~~~ r
xmi = -78.396850
xma = -78.336507
ymi = 38.534471
yma = 38.567735

med_bbox <- st_bbox(c(xmin = xmi, xmax = xma, 
                      ymin = ymi, ymax = yma),
                    crs = 4326)
                    
med_bbox_df <- data.frame(x = c(xmi, xma),
                       y = c(ymi, yma))


extent_zoomed <- raster::extent(med_bbox)
prj_dd <- "+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs"

elev_med <- get_elev_raster(med_bbox_df, prj =  prj_dd, z = 12, clip = "bbox")

elev_med_mat <- raster_to_matrix(elev_med)

med_roads <- med_bbox %>%
  opq() %>%
  add_osm_feature(key = "highway") %>%
  osmdata_sf()

med_roads_lines <- med_roads$osm_lines


skylinedrive_= med_roads_lines %>% 
  filter(name %in% c("Skyline Drive"))

med_water <- med_bbox %>%
  opq() %>%
  add_osm_feature(key = "waterway") %>%
  osmdata_sf()

med_water_lines <- med_water$osm_lines


whiteoak_trails= med_roads_lines %>% 
  filter(name %in% c("White Oak Canyon Trail", "Cedar Run Trail", "Whiteoak Canyon Fire Road"))

whiteoak_trails2 = med_roads_lines %>% 
  filter(osm_id %in% c("41881138"))

pal <- "Manet"
colors <- (met.brewer(pal))

base_map <- elev_med_mat %>% 
  height_shade(texture = grDevices::colorRampPalette(colors)(256)) %>% 
  add_overlay(
    generate_line_overlay(
      skylinedrive_, extent = extent_zoomed,
      linewidth = 2, color = "grey",
      heightmap = elev_med_mat
    )) %>%
    add_overlay(generate_line_overlay(
      med_water_lines, extent = extent_zoomed,
      linewidth = 1, lty = 3, color = "white",
      heightmap = elev_med_mat
    )) %>%
  add_overlay(
    generate_line_overlay(
      whiteoak_trails, extent = extent_zoomed,
      linewidth = 1, color = "red",
      heightmap = elev_med_mat
    )) %>%
  add_overlay(
    generate_line_overlay(
      whiteoak_trails2, extent = extent_zoomed,
      linewidth = 1, color = "red",
      heightmap = elev_med_mat
    )) %>%
  plot_3d(elev_med_mat, 
          zscale = 10, 
          windowsize = c(1200, 1000),
          soliddepth = -max(elev_med_mat)/10, 
          wateralpha = 0,
          theta = 25, 
          phi = 30, 
          zoom = 0.65, 
          fov = 60, 
          solid= TRUE)

filename_movie = "whiteoak.mp4"
render_movie(filename = filename_movie)
~~~
