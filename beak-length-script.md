# (PART) Appendices {-}

# Beak Length Script

Here is the code you used to analyze the beak length in the finches dataset.

You can either copy the code below and paste it into a new R script, e.g. `plant_height.R`, or [download](beak-length.R) it as an R script, copy, and paste from there.

Once you've copied the code, you can work through changing file paths, object names, column names, and axis labels as needed to perform your Intraspecific Variation Analysis.


```r
# load packages -----------------------------------------------------------

# run every time you restart RStudio
library(readxl)     # load readxl, for reading Excel files
library(tidyverse)  # load tidyverse, for working with datasets


# read data ---------------------------------------------------------------

finches <- read_excel("finches_data.xlsx")  # read the finches data
finches                                     # print finches data in console
glimpse(finches)                            # another way to view data


# histogram ---------------------------------------------------------------

# histogram of beak length, grouped by survival, with labels
ggplot(
  data = finches,                     # use the finches dataset
  mapping = aes(x = beak_length,      # put beak length on the x axis
                fill = outcome)       # fill sets the color of the boxes
) +
  geom_histogram(bins = 14) +         # add the histogram, use 14 bins
  facet_wrap(~ outcome, ncol = 1,     # outcome is the grouping variable
    scales = "free_y") +              # allow y axes to vary on each facet
  guides(fill = "none") +             # don't show a legend for fill color
  labs(
    title = "Figure 1.",                # change number if necessary
    x = "Beak Length (mm)",             # human-readable x-axis label
    y = "Number of Birds",              # human-readable y-axis label
    caption = "Author: YOUR NAME HERE"  # your name so we know who made it
  )

# save your most recent plot
ggsave("beak_length_histogram.png",   # you choose a name for the file
       width = 3.5, height = 3.5)     # dimensions of saved file in inches


# summarize ---------------------------------------------------------------

# summarize the dataset by outcome (survived vs. died)
beak_length_grouped_summary <- 
  finches %>% 
  group_by(outcome) %>%               # for each outcome...
  summarize(                          # calculate the following stats
    mean = mean(beak_length),
    sample_size = n(),
    standard_error = sd(beak_length) / sqrt(sample_size),
    upper_conf_limit = mean + 1.96 * standard_error,
    lower_conf_limit = mean - 1.96 * standard_error
  ) %>% 
  print()                             # print the results in the console


# bar chart ---------------------------------------------------------------

# bar chart of mean beak lengths
ggplot(
  data = beak_length_grouped_summary,   # use summary data, not "finches"
  mapping = aes(x = outcome,            # survival on the x axis
                y = mean,               # mean beak length on the y axis
                fill = outcome)         # make died/survived different colors
) +
  geom_col() +                                 # add columns
  geom_errorbar(                               # add error bars
    mapping = aes(ymin = lower_conf_limit,     #   lower 95% confidence limit
                  ymax = upper_conf_limit),    #   upper 95% confidence limit
    width = .3                                 #   width of horizontal bars
  ) +
  guides(fill = "none") +               # don't show fill color legend
  labs(
    title = "Figure 2.",                # change number if necessary
    x = "Outcome",                      # human-readable x-axis label
    y = "Beak Length (mm)",             # human-readable y-axis label
    caption = "Author: YOUR NAME HERE"  # your name so we know who made it
  )

# save the beak length bar chart
ggsave("beak_length_bar_chart.png", width = 2.5, height = 3.5)

# t-test ------------------------------------------------------------------

# perform a two-sample t-test assuming unequal variances
t.test(beak_length ~ outcome, data = finches)
```

