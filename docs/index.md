---
knit: bookdown::render_book
site: bookdown::bookdown_site
title: "Introduction to Data Science with R and Tidyverse"
author: "Lukas Jürgensmeier, based on materials from Data Science in a Box by Mine Çetinkaya-Rundel"
description: "Data Science in a Box contains the materials required to teach (or learn from) the course described above, all of which are freely-available and open-source."
date: "2022-04-26"
github-repo: lukas-jue/intro-tidyverse-2022-summer
cover-image: dsbox.png
url: 'https\://datasciencebox.org/'
documentclass: book
link-citations: yes
---

# Welcome {.unnumbered}

Welcome to the course website for

**Introduction to Data Science with R and Tidyverse**

offered for GRADE Brain and other GRADE Centers at Goethe University in May 2022.
This website serves as the central repository for all course materials.
Here, you will find all slides, lecture materials, and links to your online development environment.

## Course Objective

Most academic fields require proficiency in at least one data-centered analysis tool.
For many, the R programming language has become the tool of choice.
However, the first steps in coding can be intimidating and discouraging---primarily if you have never worked with a programming language before.
This course aims at providing a results-oriented, applied, and hands-on introduction to the essential parts of a Data Science project in R.
We will introduce the libraries and frameworks necessary for your analysis and focus on teaching you the implementation and application of those tools.
We'll present small examples throughout the lecture and provide you with application exercises that you can work on for yourself.

Our goal is to show you the scope of possibilities within R and leave you with the impression that you can confidently implement your empirical projects in R.
We will focus on the Tidyverse ecosystem, a consistent and intuitive framework for building your data analysis from start to finish.
After completing this course, you know how to apply the essential Tidyverse tools for everyday Data Science tasks in R---primarily data wrangling, data visualization, and communicating results.

## Course Description

We aim this course at beginners who are either entirely new to R as a programming language and/or want to learn about the Tidyverse ecosystem.
The course covers four primary areas of the typical data science process and introduces the respective `tidyverse` tools:

-   Plotting with `ggplot2`
-   Data wrangling with `dplyr`
-   Communicating your results with R Markdown
-   Regressions with `tidymodels`

We will not cover statistical or theoretical concepts in this course, as the focus will lie on applied coding.

## Methods

We will *let you eat cake first*.
What does that mean?
Many programming courses start with the absolute basics --- variable types, syntax, loops, etc.
Those are important but quite dull in the beginning.
Instead of monotonously walking you through those, we follow a different teaching philosophy.

Each topic will start with a very friendly and sometimes a bit complicated *cake*.
And you will dive right into it by executing and adapting the code for that "data science cake."

For example, we will show you an advanced visualization right at the beginning of the course and focus on what is possible eventually.
While this might appear intimidating at first (*"how should I ever be able to code that from scratch?"*), we will walk you through the steps and introduce the methods to get there during the course.

The course will alternate between short introductions to a concept or method and small do-it-yourself coding exercises.
In between the three sessions, you are encouraged to work on provided exercises that further deepen your understanding.

## Conditions

This workshop is a beginner-friendly course.
You do not need prior coding experience.
But you are also more than welcome to participate if you are an experienced R user but want to learn more about the Tidyverse.

You will need an RStudio Cloud account.
RStudio Cloud is a very convenient Integrated Development Environment, where we provide you with all necessary code to follow the course and work with small application exercises on your own.

By not installing RStudio locally during the course, we can start right away with the more critical course content.
If you already have set up a local installation of RStudio, you are, of course, more than welcome to use that instead.
In this case, download the source files linked in the respective application exercises.
Note that you won't need to set anything up if you use RStudio Cloud.

Since we do not want to waste precious time on the technical setup, we will use the RStudio Cloud as a simple---and already set up---development environment.
We will send out detailed instructions and an invitation link in advance.

## Course Organization & Video Recordings

We will meet on three Tuesday evenings from *6:00 - 8:00 p.m.* Please access the course via [this Zoom link](https://uni-frankfurt.zoom.us/s/93307941729?pwd=N0YyVGZ3a1lrMXdsR1FSMDFSUFpoZz09) or the meeting ID 933 0794 1729 and passcode 692604.

| Part | Date       | Time          | Video Recording       |
|------|------------|---------------|-----------------------|
| 1    | 03.05.2022 | 18:00 - 20:00 | Link will follow here |
| 2    | 10.05.2022 | 18:00 - 20:00 | Link will follow here |
| 3    | 17.05.2022 | 18:00 - 20:00 | Link will follow here |

We want you to *make your hands dirty* --- that means we want you to code!
Just following along fancy slides won't magically transfer the skill of coding to you.
But you actively engaging with the course content in your development environment will more likely do just that.

That's why we need you to prepare accordingly:

-   Try to follow the course with two screens or two devices (one for Zoom and the slides, and one for your browser with RStudio Cloud)
-   Please create an RStudio Cloud account before the first class. We have sent you a link to access all exercises on RStudio Cloud. Since we want you to start coding very early on in the first class, please ensure that you can access those course materials on RStudio Cloud before meeting on 13 January.

If you have any questions, please reach out to one of us through the e-mail addresses on the bottom of this page.

## Schedule

This workshop alternates between lecture-style presentations and application exercises.
In those hands-on exercises, you will actively try out the discussed tools and techniques in Zoom breakout rooms.
We aim to adhere to the following schedule.
Depending on our progress, we may discuss some parts a bit earlier or later during the course.
You can download a .ics calendar with the schedule and the Zoom link [here](https://lukas-jue.github.io/intro-tidyverse/ics-calendar/intro_to_data_science_with_r_and_tidyverse.ics).

| Part | Date   | Title                              | Type                 | Lecturer |
|------|--------|------------------------------------|----------------------|----------|
| 1    | 03.05. | Welcome                            | Lecture              | Lukas    |
| 1    | 03.05. | First data visualization: UN Votes | Application Exercise |          |
| 1    | 03.05. | Meet the programming toolkit       | Lecture              | Karlo    |
| 1    | 03.05. | The Bechdel Test + R Markdown      | Application Exercise |          |
| 2    | 03.05. | Data and visualization             | Lecture              | Lara     |
| 2    | 03.05. | Visualizing data with ggplot2      | Lecture              | Lara     |
| 2    | 10.05. | Visualizing categorical data       | Lecture              | Lara     |
| 2    | 10.05. | StarWars + Dataviz                 | Application Exercise |          |
| 3    | 10.05. | Tidy data                          | Lecture              | Karlo    |
| 3    | 10.05. | Grammar of data wrangling          | Lecture              | Karlo    |
| 3    | 10.05. | Working with a single data frame   | Lecture              | Lukas    |
| 3    | 10.05. | Hotels + Data wrangling            | Application Exercise |          |
| 3    | 17.05. | Working with multiple data frames  | Lecture              | Lukas    |
| 4    | 17.05. | Data types                         | Lecture              | Karlo    |
| 4    | 17.05. | Importing data                     | Lecture              | Lara     |
| 4    | 17.05. | Nobels + Sales + Data import       | Application Exercise |          |
| 5    | 17.05. | Fitting and interpreting models    | Lecture              | Lukas    |

## Readings

The course is self-contained, and you will most likely get all the necessary information for the application exercises from the slides.
If you want to read more about given topics, we provide links to chapters in open source Data Science/Tidyverse/R textbooks.
You will find the links on the following pages right beside the link to each chapter's slides.

::: reading
We suggest two textbook references:

-   **R4DS**: Wickham, H., Grolemund, G. (2017), "R for Data Science: Import, Tidy, Transform, Visualize, and Model Data", available at [r4ds.had.co.nz](https://r4ds.had.co.nz/)
-   **IMS**: Çetinkaya-Rundel, M., Hardin, J. (2021), "Introduction to Modern Statistics", available at [openintro-ims.netlify.app](https://openintro-ims.netlify.app/)
:::

## Trainers

Feel free to reach out to us by e-mail if you have any questions before, during, or after the course:

-   **Lukas Jürgensmeier**, M.Sc., [PhD Student in Quantitative Marketing](https://www.marketing.uni-frankfurt.de/abteilungen/marketing/professoren/skiera/team/wissenschaftliche-mitarbeiter/lukas-juergensmeier.html) and Member of the Executive Board at [TechAcademy e.V.](https://tech-academy.io/), [send me an e-mail](mailto:lukas.juergensmeier@tech-academy.io), [personal website](https://lukas-juergensmeier.com/).
-   **Lara Zaremba**, M.Sc., Trainee Data Science at the European Central Bank and R Teacher and Course Designer at [TechAcademy e.V.](https://tech-academy.io/), [send me an e-mail](mailto:lara.zaremba@tech-academy.io)
-   **Karlo Lukic**, M.Sc., [PhD Student in Quantitative Marketing](https://www.marketing.uni-frankfurt.de/abteilungen/marketing/professoren/skiera/team/wissenschaftliche-mitarbeiter/karlo-lukic.html), R Teacher and Course Designer at [TechAcademy e.V.](https://tech-academy.io/), [send me an e-mail](mailto:lukic@wiwi.uni-frankfurt.de)

## License {.unnumbered}

<a rel="license" href="https://creativecommons.org/licenses/by-sa/4.0/"><img src="https://licensebuttons.net/l/by-sa/4.0/88x31.png" alt="Creative Commons License" style="border-width:0"/></a><br />This online work is licensed under a <a rel="license" href="https://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International</a>.
Visit [here](https://github.com/rstudio-education/datascience-box/blob/master/LICENSE.md) for more information about the license.

## Acknowledements {.unnumbered}

The entire course is built upon material from [datasciencebox.org](https://datasciencebox.org/) by Mine Çetinkaya-Rundel.

Huge thanks to the #rstats education community who have made numerous suggestions for this resource, Lee Suddaby and Zeno Kujawa, for converting the homework assignments to learnr tutorials and [Müge Çetinkaya](http://muge.fr/) for the hex logo!

This website is built with [bookdown](https://bookdown.org/), the lovely icons by [icons8](http://icons8.com/), and none of this would be possible without the [tidyverse](https://tidyverse.org/).
