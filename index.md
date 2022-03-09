# **Here is the meme I came up with**

![](test_meme.png)

A bit about my meme-making process;
- I found the bottom right image from blindly searching "Shocked Face" in google image
- I changed the text multiple different times while coming up with it
- I resized the second image very messily (I couldn't think of how else to do it then trial and error hard coding it)


For reference these are the two images I used in their native resolutions and sizes.

![](https://pbs.twimg.com/media/DgKOl_5XkAQJbC5.jpg)
![](https://tse2.mm.bing.net/th?id=OIP.icvHPKW4uHRAeqTebtDb6gHaE7&pid=Api&P=0&w=279&h=185)

As you can see, not ideal at all.

## However I managed using the extremely intuitive R package [Magick](https://cran.r-project.org/web/packages/magick/vignettes/intro.html)

### And here is my code,
```{r }
library(magick)

#Creating left hand side of my meme (Block colour + text).
lhs <- image_blank(width = 250, height = 500, color = "#000000") %>%
  image_annotate("\nMe Struggling\n On \n Assignment 1 \n\n\n\n\nWhen It\n Actually \n Works", size = 30, gravity = "center", color = "#FEFEFE")

#Creating top right corner (Common computer meme)
rhs_top <- image_read("https://pbs.twimg.com/media/DgKOl_5XkAQJbC5.jpg") %>%
  image_scale(geometry_size_pixels(250, 250))

#Creating bottom right corner (Shocked face)
rhs_bottom <- image_read("https://tse2.mm.bing.net/th?id=OIP.icvHPKW4uHRAeqTebtDb6gHaE7&pid=Api&P=0&w=279&h=185 ") %>%
  image_scale(geometry_size_percent(90, 135)  )

#Merging right hand side of meme
rhs_images <- c(rhs_top, rhs_bottom)
rhs <- image_append(rhs_images, stack = TRUE)

#Combining final meme
frames = c(lhs, rhs)
meme <- image_append(frames)

#Saving meme
image_write(meme, "test_meme.png")

```

I know, not the finest piece of code, but if you couldn't tell by my meme, I was just excited to see what I could actually do (which was also my motivation for the meme).
