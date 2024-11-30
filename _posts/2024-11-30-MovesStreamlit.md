---
layout: post
title:  "Gotta Plot 'Em All (Part 2)"
author: Brett Pedersen
description: "Performing an exploratory data analysis on several key features of the hundreds of existing pokemon moves. We identify several interesting details and relationships within the data set."   
image: "/assets/images/pokeball.png"
---

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

```python
sns.countplot(data = moves[moves["damage class"] != "status"], y = "type", hue = "damage class")
plt.show()
```

![Figure]({{site.url}}/{{site.baseurl}}/assets/images/typeclass.png)