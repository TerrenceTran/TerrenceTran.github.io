# DPEA 2017 Mechatronics Projects

## Console 12: Waves In All Dimensions

**Date:** 13 January 2017 Friday

**Objective:** 1.Kuntz Tube Volume Attenuation

**Progress Today:** The Kuntz Tube is a subsystem that consists of:

1. Arduino nano function generator shield
2. 200W audio amplifier
3. Kuntz tube 

When concieved, the 200W amplifier was thought to have the ability to modulate its volume via digital control *IE: I2C, SPI, etc* However, it turns out that neither the function generator nor the amplifier have the ability to do so. Currently, the volume can only be changed via a potentiometer on the amplifier. The goal is to create an intermediate system between the two that will add this functionality.

**Challenges:** There are a couple of ways to do this. Today was spent brainstroming the different methods and their pros and cons. After much consideration it was decided that the faster and easier means of implementation will take succession over the more complicated systems. The latter method has the primary benefit of providing a truer sound, while the crude method will distort the signal somewhat. This is less of a concern for this particular system because of its working nature. It requires resonate frequencies rather than complex signals such as music or conversation. As such, the minor distortion will be slight, uniform, and will not affect its primary mode of operation while being cheaper, and simpler than the alternatives. Win-win.


**Moving Forward:** The easiet implementation would be a digitally controlled potentiometer with all the fixings. I must admit it is a somewhat daunting task due to my inexperience with communication buses, and hopefully I can source parts that only require a simple digital or analog line. It is what I and the students will be most familiar with

## Console 13: Bernoulli's Laws

///////////////////////////////////////      Test Area     ///////////////////////////////////////////

1. Item 1
2. Item 2
3. Item 3
   * Item 3a
   * Item 3b

//////////////////////////////////////////////////////////////////////////////////////////////////////

## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/TerrenceTran/TerrenceTran.github.io/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/TerrenceTran/TerrenceTran.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
