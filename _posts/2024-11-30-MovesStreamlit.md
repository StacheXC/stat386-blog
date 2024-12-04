---
layout: post
title:  "Gotta Plot 'Em All (Part 2)"
author: Brett Pedersen
description: "Highlighting some key insights from the Pokemon moves data set, and introducing a streamlit app for further exploration"   
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

# Streamlit App

Since my previous post, I've created a streamlit app for users to discover more insights about the data set. [Here](https://movesfilter.streamlit.app/) is the link. 

The app has two main features. The first is that you can filter moves by certain criteria. For example, you can search for fire type moves that are physical and have a power greater than 80. After inputing criteria, you will see results containing for all relevant moves as well as the number of results. The second feature is a different kind of filter, one that filters by a key word. Even though the name of a move is a unique identifier rather than a variable, there still might be some useful predictors to extract from a move's name. For example, having the word, punch, in a move's name might indicate that it is a physical move.

# Conclusion

If you're interested in checking out the code used to create this app, I will include a link to the repository [here](https://github.com/StacheXC/MovesStreamlit). I'd encourage you to try out the app for yourself, and explore how common moves with various criteria are. I'd also encourage you to check out my previous post if you haven't already, where I got into much greater detail about the data set and cover several more insights.