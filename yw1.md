Access: https://swopis.github.io/YW-Befriend-Calculator/yw1/

## How does Befriending work?
Make sure to first read how to [Calculate the Difficulty](README.md#calculating-the-difficulty).  
The resulting number will be referenced as `difficulty`

### Base Probability
The base probability can be calculated using the following formula:  

$$ 1 : 2^{difficulty + 2} $$

For example, if the difficulty is `1` the base probability is $1:2^{3}$ or $1:8$ or 12.5%.

### Player-Influenced Bonuses
After calculating the base chance, the bonuses the player can influence are added:
* food bonus
* popularity skill
* unpopularity skill
* wisp bonus (10% or 100%)

> [!NOTE]
> Each bonus can only be added once. Nothing stacks.

#### Bonuses that depend on the difficulty
| Difficulty | Food Tier 1 | Food Tier 2 | Food Tier 3 | Food Tier 4 | popularity | unpopularity |
|------------|-------------|-------------|-------------|-------------|------------|--------------|
| 1          | 10%         | 15%         | 20%         | 25%         | 10%        | -10%         |
| 2          | 5%          | 8%          | 11%         | 14%         | 5%         | -5%          |
| 3          | 4%          | 6%          | 8%          | 10%         | 4%         | -3%          |
| 4          | 4%          | 5%          | 6%          | 7%          | 4%         | -1%          |
| 5          | 3%          | 4%          | 5%          | 6%          | 3%         | -0.7%        |
| 6          | 2%          | 3%          | 4%          | 5%          | 2%         | -0.3%        |
| 7          | 1%          | 2%          | 3%          | 4%          | 1%         | -0.18%       |
| 8          | 1%          | 1%          | 2%          | 3%          | 1%         | -0.08%       |

If the given food was the Yo-Kai's favorite food the value gets multiplied by 1.5. If it was the Yo-Kai's hated food it gets multiplied by 0.4.
For example, if you gave a tier 4 favorite food at difficulty 1 the bonus will be 37.5% instead of 25%.

#### Wisps
A blue wisp with one heart gives a 10% bonus, a golden wisp with three hearts guarantees this Yo-Kai to get selected.

## Modding Opportunities
The befriend bonuses are all stored in the chara param file:
```
CHARA_FRIEND_RATE_INFO (
		BaseChance|False
		FoodTier1|False
		FoodTier2|False
		FoodTier3|False
		FoodTier4|False
		Popularity|False
		Unpopularity|False
		BlueWisp|False
		GoldenWisp|False
)
```
The value represents the percentage that gets added, multiplied by 100, i.e. 1000 means 10%. Except BaseChance where the value is the reciprocal of the base befriend probability, i.e. 8 means 1:8 means 12.5%.
