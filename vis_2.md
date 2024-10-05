Vis I
================
Yucheng Zhao
2024-09-29

weather_df = rnoaa::meteo_pull_monitors( c(“USW00094728”, “USW00022534”,
“USS0023B17S”), var = c(“PRCP”, “TMIN”, “TMAX”), date_min =
“2021-01-01”, date_max = “2022-12-31”) \|\> mutate( name = case_match(
id, “USW00094728” ~ “CentralPark_NY”, “USW00022534” ~ “Molokai_HI”,
“USS0023B17S” ~ “Waterhole_WA”), tmin = tmin / 10, tmax = tmax / 10)
\|\> select(name, id, everything())

``` r
weather_df = read_csv("weather_df.csv") 
```

    ## Rows: 2190 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (2): name, id
    ## dbl  (3): prcp, tmax, tmin
    ## date (1): date
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax, color = name)) +
  geom_point(alpha = 0.3) + 
  labs(title = "Temperature scatterplot",
       x = "Min. Temp (C)",
       y = "max. Temp (C)",
       color = "location",
       caption = ("Weather data taken from rnoaa package for threee stations")
  ) +
  viridis::scale_color_viridis(discrete = TRUE)
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](vis_2_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->
