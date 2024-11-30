---
layout: post
title:  "Gotta Plot 'Em All (Part 2)"
author: Brett Pedersen
description: "Performing an exploratory data analysis on several key features of the hundreds of existing pokemon moves. We identify several interesting details and relationships within the data set."   
image: "/assets/images/pokeball.png"
---

In my last blog post, I introduced the Pokemon moves data set, containing various attributes of hundreds of moves from the Pokemon games. I showcased some interesting features of the data set, including some of the relationships between variables. Once again, here are the first few rows of the moves dataframe.

```python
moves.head()
```

| name        |   power |   accuracy |   pp | damage class   | type     | target           |
|:------------|--------:|-----------:|-----:|:---------------|:---------|:-----------------|
| pound       |      40 |        100 |   35 | physical       | normal   | selected-pokemon |
| karate-chop |      50 |        100 |   25 | physical       | fighting | selected-pokemon |
| double-slap |      15 |         85 |   10 | physical       | normal   | selected-pokemon |
| comet-punch |      18 |         85 |   15 | physical       | normal   | selected-pokemon |
| mega-punch  |      80 |         85 |   20 | physical       | normal   | selected-pokemon |

# Key Relationships

Here are the 2 most interesting relationships I discovered within the data set. The first is the association between a move's power and the number of times it can be used (pp), showcased in the scatterplot and correlation plots below.

```python
sns.scatterplot(data = moves, x = "power", y = "pp")
plt.show()
```

![Figure]({{site.url}}/{{site.baseurl}}/assets/images/powerpp.png)

```python
moves[["power", "pp"]].corr()
```

|       |     power |        pp |
|:------|----------:|----------:|
| power |  1        | -0.514725 |
| pp    | -0.514725 |  1        |

As we can see, the relationship between power and pp is negative and perhaps non-linear. The key insight is that as power increases, the number of times you can use the move decreases. This makes sense as this restriction on usage is a necessary drawback for balancing out the move's increased power.

The second interesting relationship I found was between a move's type and its damage class, pictured below.

```python
sns.countplot(data = moves[moves["damage class"] != "status"], y = "type", hue = "damage class")
plt.show()
```

![Figure]({{site.url}}/{{site.baseurl}}/assets/images/typeclass.png)

According to this plot, while some moves lean more heavily on the physical side (such as fighting and rock), some lean more heavily on the special side (such as psychic and fire). As I discussed in my previous post, much of this plot can be explained by the fact that before 2006, whether a move was physical or special was based on its type. For example, all fighting moves were physical and all psychic moves were special. Even though there's more diversity now, these initial biases haven't been fully overcome.