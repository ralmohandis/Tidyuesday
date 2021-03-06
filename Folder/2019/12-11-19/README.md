
<!-- README.md is generated from README.Rmd. Please edit that file -->

``` r
#Bibliotecas necesarias
library(tidytuesdayR)
library(readr)
library(tidyr)
library(dplyr)
library(ggplot2)
library(gganimate)
library(forcats)
library(ggthemes)
library(png)
library(grid)
library(plotly)
```

``` r
#Lectura de Datos
tt <- tt_load(2019,46) 
df <- tt$loc_cran_packages
save(df,file = "CRAN.Rdata")
load("CRAN.Rdata")
```

``` r
#Seleccion de datos
Data <- df %>% 
  filter(pkg_name %in% c("ggplot2","dplyr","tidyr","readr","httr","purrr","tibble","stringr","forcats","lubridate","hms","feather","haven","jsonlite","readxl","rvest","xml2","modelr","broom"))

g1 <- rasterGrob(readPNG('./hex_png/ggplot2.png', native = T), interpolate=F)
g2 <- rasterGrob(readPNG('./hex_png/dplyr.png', native = T), interpolate=F)
g3 <- rasterGrob(readPNG('./hex_png/broom.png', native = T), interpolate=F)
#g4 <- rasterGrob(readPNG('./hex_png/jsonlite.png', native = T), interpolate=F)
g5 <- rasterGrob(readPNG('./hex_png/haven.png', native = T), interpolate=F)
g6 <- rasterGrob(readPNG('./hex_png/readr.png', native = T), interpolate=F)
g7 <- rasterGrob(readPNG('./hex_png/lubridate.png', native = T), interpolate=F)
g8 <- rasterGrob(readPNG('./hex_png/purrr.png', native = T), interpolate=F)
#g9 <- rasterGrob(readPNG('./hex_png/httr.png', native = T), interpolate=F)
#g9 <- rasterGrob(readPNG('./hex_png/xml2.png', native = T), interpolate=F)
g10 <- rasterGrob(readPNG('./hex_png/readxl.png', native = T), interpolate=F)
g11 <- rasterGrob(readPNG('./hex_png/tibble.png', native = T), interpolate=F)
g12 <- rasterGrob(readPNG('./hex_png/stringr.png', native = T), interpolate=F)
g13 <- rasterGrob(readPNG('./hex_png/tidyr.png', native = T), interpolate=F)
g14 <-rasterGrob(readPNG('./hex_png/forcats.png', native = T), interpolate=F)
g15 <- rasterGrob(readPNG('./hex_png/feather.png', native = T), interpolate=F)
g16 <- rasterGrob(readPNG('./hex_png/hms.png', native = T), interpolate=F)
g17 <- rasterGrob(readPNG('./hex_png/modelr.png', native = T), interpolate=F)
g18 <- rasterGrob(readPNG('./hex_png/rvest.png', native = T), interpolate=F)
```

``` r
g <-   ggplot(Data,aes(x = reorder(pkg_name, file, function(x){ sum(x) }), y=file))+
  geom_bar(stat = "identity", aes(fill=language))+
  scale_fill_viridis_d(option = "magma")+
  scale_y_continuous(breaks = c(0,50,100,150,200,250,300,350,400,450))+
  theme_hc(style =  'darkunica')+
  theme(legend.position = "right",
        plot.caption = element_text(hjust = 5.5),
        legend.text = element_text(size=13),
        legend.title = element_text(size=13),
        axis.title = element_text(size = 15),
        axis.text.x = element_text(family = "Roboto Mono",
                                   size = 11,
                                   colour = "grey76"),
        axis.text.y = element_text(family = "Roboto Mono", 
                                   size = 11,
                                   colour = "grey76"),
        line = element_line(linetype = "dashed"))+
  labs(title = "CRAN Code for Tidyverse",
       y="File",
       x="Package name",
       fill="Language",
       caption = "Vizualization by Duvan Nieves | Data : 'CRAN Code' by CRAN")+
  annotation_custom(g1, xmin = 0, xmax = 38, ymin = -20, ymax = -1) +
  annotation_custom(g2, xmin = 0, xmax = 36, ymin = -20, ymax = -1) +
  annotation_custom(g3, xmin = 0, xmax = 34, ymin = -20, ymax = -1) +
  annotation_custom(g5, xmin = 0, xmax = 30, ymin = -20, ymax = -1) +
  annotation_custom(g6, xmin = 0, xmax = 28, ymin = -20, ymax = -1) +
  annotation_custom(g7, xmin = 0, xmax = 26, ymin = -20, ymax = -1) +
  annotation_custom(g8, xmin = 0, xmax = 24, ymin = -20, ymax = -1) +
  annotation_custom(g10, xmin = 0, xmax = 18, ymin = -20, ymax = -1) +
  annotation_custom(g11, xmin = 0, xmax = 16, ymin = -20, ymax = -1) +
  annotation_custom(g12, xmin = 0, xmax = 14, ymin = -20, ymax = -1) +
  annotation_custom(g13, xmin = 0, xmax = 12, ymin = -20, ymax = -1) +
  annotation_custom(g14, xmin = 0, xmax = 10, ymin = -20, ymax = -1) +
  annotation_custom(g15, xmin = 0, xmax = 8, ymin = -20, ymax = -1) +
  annotation_custom(g16, xmin = 0, xmax = 6, ymin = -20, ymax = -1) +
  annotation_custom(g17, xmin = 0, xmax = 4, ymin = -20, ymax = -1) +
  annotation_custom(g18, xmin = 0, xmax = 2, ymin = -20, ymax = -1) +
  coord_flip() +
  #transition_events()+
  transition_layers(layer_length = .001,transition_length = 1, keep_layers = c(18,17,16,15,14,13,12,11,10,9,8,7,6,5,4,3,2,1)) +
  shadow_mark()+
  enter_fade() + enter_grow() +
  exit_fade() + exit_shrink()

animate(g, renderer = gifski_renderer())
```

<img src="README_files/figure-gfm/unnamed-chunk-2-1.gif" style="display: block; margin: auto;" />
