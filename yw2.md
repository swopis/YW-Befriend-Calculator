Access: https://swopis.github.io/YW-Befriend-Calculator/yw2/

## How does Befriending work?
Make sure to first read the [Common Starting Point](README.md#common-starting-point).  
The resulting number will be referenced as `difficulty`

### Base Probability
The base probability can be calculated using the following formula:  

$$ 1 : 2^{difficulty + 2} $$

For example, if the difficulty is `1` the base probability is $1:2^{3}$ or $1:8$ or 12.5%.

### Player-Influenced Bonuses
After calculating the base chance, the bonuses the player can influence are added:
* food bonus
* befriend poke (10%)
* superstar soul/popularity skill
* unpopularity skill
* whisp bonus (10% or 100%)
* shrine bonus (1%)

> [!NOTE]
> Each bonus can only be added once. Nothing stacks.

#### Bonuses that depend on the difficulty
| Difficulty | Food Tier 1 | Food Tier 2 | Food Tier 3 | Food Tier 4 | popularity | unpopularity |
|------------|-------------|-------------|-------------|-------------|------------|--------------|
| 1          | 10%         | 15%         | 20%         | 25%         | 10%        | -10%         |
| 2          | 5%          | 8%          | 11%         | 14%         | 5%         | -4.5%        |
| 3          | 4%          | 6%          | 8%          | 10%         | 4%         | -2%          |
| 4          | 4%          | 5%          | 6%          | 7%          | 4%         | -1%          |
| 5          | 3%          | 4%          | 5%          | 6%          | 3%         | -0.5%        |
| 6          | 2%          | 3%          | 4%          | 5%          | 2%         | -0.25%       |
| 7          | 1%          | 2%          | 3%          | 4%          | 1%         | -0.1%        |
| 8          | 1%          | 1%          | 2%          | 3%          | 1%         | -0.05%       |

If the given food was the Yo-Kai's favorite food the value gets multiplied by 1.5. If it was the Yo-Kai's hated food it gets multiplied by 0.4.
For example, if you gave a tier 4 favorite food at difficulty 1 the bonus will be 37.5% instead of 25%.

#### What is the shrine bonus?
Sometimes after you have put your 1$ into the shrine in Mt. Wildwood, you get the message: "I have a feeling that I've got a lot more friends now.".
After this message every Yo-Kai has a 1% higher chance of approaching you after a battle for one day.

### Full Example
You are playing against Undy and two Pandles and haven't befriended anyone of them. The base probability for befriending Undy will be 1:64 or about 1.6%, for befriending each Pandle the probability
will be 1:8 or 12.5%. If you now give Undy his favourite tier 4 food this probability gets increased: 1.6% + 1.5*7% = 1.6% + 10.5% = 12.1%. Now you also poke him: 12.1% + 10% = 22.1%. And you get a blue whisp with one heart: both Pandle's chances get increased: 12.5% + 10% = 22.5%. And Undy's chance also: 22.1% + 10% = 32.1%. 

As the fight now ends these probabilities are applied for each Yo-Kai separately. If you want to know the chance you will get Undy, it will just be the calculated 32.1%, because he has a higher difficulty. If however you want to calculate the chance of befriending Pandle in this example, the calculation becomes a bit more complicated. You have to calculate the probability that Undy will not get selected and at least one of the Pandles will:

$$P(U) = 0.321$$
$$P(P1) = 0.225$$
$$P(P2) = 0.225$$
$$P(P) = P((P1 \cup P2) \cap \neg U) = P(\neg U) * P(P1 \cup P2)$$
$$= (1 - P(U)) * (P(P1) + P(P2) - P(P1 \cap P2))$$
$$= (1 - 0.321) * (0.225 + 0.225 - 0.225*0.225)$$
$$= 0.271 = 27.1\\%$$

So the probability for befriending Pandle in this example will be 27.1%. 

### Random Event Befriends
Some Yo-Kai are given to the player in an event and not like most Yo-Kai with "[Yo-Kai] approaches you". Some of these befriends are also randomly decided.  
This system however works differently than the one explained above. The befriend chance is hardcoded into a [CExpression](https://github.com/n123git/yw-cond/)
and only depends on how often that Yo-Kai is already befriended (if it can be befriended more than one time)  
The probabilities are:  

| Yokai Name    | Befriend Count | Probability |
|---------------|----------------|-------------|
| SV Snaggerjag | -              | 7.5%        |
| Slimamander   | -              | 7.5%        |
| Gargaros      | 0              | 5%          |
|               | 1              | 2.5%        |
|               | 2              | 1.2%        |
| Ogralus       | 0              | 5%          |
|               | 1              | 2.5%        |
|               | >=2            | 1.2%        |
| Orcanos       | 0              | 3%          |
|               | 1              | 1.5%        |
|               | >=2            | 0.8%        |

### Other important notes
* Generally befriending a specific Yo-Kai becomes harder if you've already befriended them.
* It is impossible to befriend a Yo-Kai after a battle if you already befriended 6 of them.
* Sometimes it can be better to give the Yo-Kai a tier 4 non-favorite food instead of a tier 1 favorite food.
* If you get a golden whisp with 3 hearts, the Yo-Kai with the highest difficulty as last digit will always become your friend.
* If you are facing multiple of the same Yo-Kai, giving each of them separately a food item and poking each of them separately increases the odds of befriending them. 
* While Type-Rare Yo-Kai always have the same befriend probabilities as their non-rare counterpart, they count as separate Yo-Kai.

## Modding opportunities
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
		BlueWhisp|False
		GoldenWhisp|False
		BefriendPoke|False
		ShrineBonus|False
)
```
The value represents the percentage that gets added, multiplied by 100, i.e. 1000 means 10%. Except BaseChance where the value is the reciprocal of the base befriend probability, i.e. 8 means 1:8 means 12.5%.
