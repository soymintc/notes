# R
Personal cheatsheet

## f-string equivalent in `R`
```R
library(glue)
name <- 'SAY-MY-NAME'
glue(f'hello {name}')
```

## Print multiple arrangeGrob plots in different pages of one PDF file
```R
# Load required libraries
library(ggplot2)
library(gridExtra)

# Create some example plots
data(mpg)

p1 <- ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_point() +
  ggtitle("Plot 1: Displacement vs Highway MPG")

p2 <- ggplot(mpg, aes(x = cty, y = hwy)) +
  geom_point() +
  ggtitle("Plot 2: City MPG vs Highway MPG")

p3 <- ggplot(mpg, aes(x = cyl, y = hwy)) +
  geom_point() +
  ggtitle("Plot 3: Cylinders vs Highway MPG")

p4 <- ggplot(mpg, aes(x = class, y = hwy)) +
  geom_point() +
  ggtitle("Plot 4: Class vs Highway MPG")

# Arrange the plots into grids
g1 <- arrangeGrob(p1, p2, ncol = 2)
g2 <- arrangeGrob(p3, p4, ncol = 2)

# Start the PDF device
pdf("/juno/work/shah/users/chois7/notebook/gdan/dlbcl/plots/myplots.pdf")

# Print the arrangeGrob objects
grid::grid.draw(g1)
grid::grid.newpage()
grid::grid.draw(g2)
grid::grid.newpage()
grid::grid.draw(plot.new()) # plot empty plot

# Close the device
dev.off()
```

# Get value counts of a column
```R
some_dataframe %>% dplyr::count(some_column)
```

# Setting .libPaths() when using Rstudio in a container
```bash
echo '.libPaths(c("/path/to/your/writable/directory", .libPaths()))' >> ~/.Rprofile
```
or
```R
.libPaths(c("/path/to/your/writable/directory", .libPaths())) # temporary
```
