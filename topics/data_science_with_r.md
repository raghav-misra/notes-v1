# introduction to r.

## hello.

I wanted to learn R for a long time, but never had the time. I'm finally going to commit to learning it and its vast ecosystem of packages, as it can help with my future economics and statistics courses. These notes will follow along with the book **R for Data Science (2e)**, by Hadley Wickham, Mine Çetinkaya-Rundel, and Garrett Grolemund. 

In order to follow along, we'll need to install [R](https://cloud.r-project.org/), [RStudio](https://posit.co/download/rstudio-desktop/), and the [`tidyverse`](https://www.tidyverse.org/) data science packages. Also, this book seems to recommend that I know R already, which I didn't when I started. But it will *probably* be fine.

## data science?

- **Data science** is a vast discipline that allows us to transform raw data into understanding, insights, and knowledge.
- We can break down a typical data science project into the following steps, demonstrated well by the below graphic.![A diagram displaying the data science cycle: Import -> Tidy -> Understand (which has the phases Transform -> Visualize -> Model in a cycle) -> Communicate. Surrounding all of these is Communicate. ](https://r4ds.hadley.nz/diagrams/data-science/base.png)
  - **Importing** is essentially loading our data into the respective language or platform; in our case, R.
  - **Tidying** our data is cleaning its contents so it can be consistent enough to gain some insights from.
  - Transforming, visualizing, and modeling are often performed multiple times in multiple orders until the desired insights are gained.
    - **Transforming** is narrowing in on interesting observations in the dataset.
    - **Visualizing** is taking our data and displaying it in a more human-readable fashion, think graphs and charts.
    - **Modeling** can be used to extrapolate and predict insights from existing datasets. "Every model makes assumptions, and by its very nature, a model cannot question its own assumptions."
      - Modeling is not covered in this book.
  - And lastly, **communication** is how convert our findings into actionable results. 

## data visualization.

- `ggplot2` is an elegant and versatile graphing library that comes preinstalled with `tidyverse`. `palmerpenguins` is a sample dataset we can use.

  - ```r
    install.packages("tidyverse")
    install.packages("palmerpenguins")
    ```

- To load packages, use the `library` function.

  - ```r
    library("tidyverse")
    library("palmerpenguins")
    ```

- `glimpse(penguins)` previews the data frame.

  - Notice the output: # of rows and columns, the variable names of the data frame, and a few observations to preview.
  - In RStudio, you can use `View(penguins)` for an interactive table view.

- Now let's explore this dataset further with `ggplot2`.

  - ```r
    ggplot(
    	data = penguins,
    	mapping = aes(x = flipper_length_mm, y = body_mass_g)
    )
    ```
  
    - `aes()`  maps variables to $x$ and $y$ axes; we map the flipper length to $x$ and body mass to $y$.
    - This outputs a graph with labeled axes, but nothing displayed. 
  
  - ```r
    ggplot(
    	data = penguins,
    	mapping = aes(x = flipper_length_mm, y = body_mass_g)
    ) +
    	geom_point()
    ```
  
  - `geom_point()` 