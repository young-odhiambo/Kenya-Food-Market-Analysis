# Kenya Market Prices: Should Maize Farmers Sell at Harvest or Store?

An analysis of monthly food prices across Kenyan markets from **January 2006 to December 2019**. It focuses on **wholesale maize**: how prices moved year to year, how they rise and fall through the seasons, and whether a farmer who stores maize after harvest usually earns more by selling later.

All work is in [foodpricesanalysis.ipynb](C:\Users\USER\OneDrive\Documents\FoodPrices\notebook\foodprices_analysis.ipynb), using [data/food-prices-kenya.csv](data/food-prices-kenya.csv).

**The short note for Pamoja, with advice for farmers and county officers, is in [PAMOJA_NOTE.md](C:\Users\USER\OneDrive\Documents\FoodPrices\PAMOJA_NOTES.md).**

---

## The data

| Item | Detail |
|---|---|
| Rows | 2,742 monthly price records |
| Period | 2006-01-15 to 2019-12-15 |
| Commodities | Maize and beans |
| Markets | 14 |
| Price types | **Wholesale**, quoted per 90 kg bag (Eldoret, Kisumu, Mombasa, Nairobi, Nakuru) and **Retail**, quoted per kg (Garissa, Hola, Kajiado, Kilifi, Kitui, Lodwar, Mandera, Marigat, Marsabit) |
| Columns | date, region, county, market, commodity, price_type, unit, price_kes, price_usd |
| Source | World Food Programme (WFP) market price data for Kenya, published on the [Humanitarian Data Exchange (HDX)](https://data.humdata.org/) |

**Units for maize:** all 721 wholesale maize records are per **90 KG** bag, and all 955 retail maize records are per **KG**. Wholesale and retail prices are never averaged together. They are only compared after converting to `price_per_kg`.

### Cleaning steps
- Converted `date` to real dates and added `year` and `month` columns.
- **Hola** market had no county or region (59 rows). These were filled in as **Tana River** county, **Coast** region.
- Checked for duplicate rows and found none.
- Added a `price_per_kg` column (90 kg bag price ÷ 90) so wholesale and retail prices can be compared per kg.

---

## Key findings

### 1. Retail maize costs about 68% more per kg than wholesale
| Price type | Average price per kg |
|---|---|
| Wholesale maize | **KES 28.54** |
| Retail maize | **KES 47.92** |

That is a gap of about KES 19 per kg between what traders pay and what households pay. Retail prices also come from different, mostly remote and arid markets (e.g. Lodwar, Mandera, Marsabit), so part of the gap is transport costs and remoteness, not just trader margin.

### 2. Maize prices have roughly doubled since 2006, with sharp swings
Average wholesale price per 90 kg bag:

| Year | Avg (KES) | Change vs previous year |
|---|---|---|
| 2006 | 1,395 | – |
| 2007 | 1,207 | −188 |
| 2008 | 1,906 | +699 |
| 2009 | 2,513 | +607 |
| 2010 | 1,774 | −739 |
| 2011 | 3,020 | **+1,246 (biggest rise)** |
| 2012 | 3,174 | +154 |
| 2013 | 2,962 | −211 |
| 2014 | 2,994 | +31 |
| 2015 | 2,690 | −304 |
| 2016 | 2,763 | +73 |
| 2017 | **3,744 (highest year)** | +981 |
| 2018 | 2,408 | **−1,335 (biggest fall)** |
| 2019 | 3,030 | +622 |

- **Highest average year:** 2017 (KES 3,744 per bag).
- **Biggest rise:** 2011 (+KES 1,246).
- **Biggest fall:** 2018 (−KES 1,335).

Prices do not rise smoothly. Big jumps tend to be followed by big drops, so one year's price is a poor guide to the next.

### 3. There is a clear seasonal cycle: cheapest in January, dearest in June
Average wholesale price per 90 kg bag by month:

| Jan | Feb | Mar | Apr | May | **Jun** | Jul | Aug | Sep | Oct | Nov | Dec |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **2,330** | 2,405 | 2,449 | 2,627 | 2,824 | **2,839** | 2,833 | 2,695 | 2,539 | 2,443 | 2,428 | 2,403 |

Prices are lowest just after the main harvest (around January). They climb through the lean season to a peak in **June–July**, then fall again as the next harvest arrives. On average, June is about **KES 510 per bag (~22%) higher** than January.

### 4. Storing from January to June paid off in about 3 out of 4 cases
Comparing each wholesale market's January price with its June price in the same year (60 market-years):

- June was higher than January in **73.3%** of market-years.
- The **median gain was KES 356 per 90 kg bag** (about KES 4 per kg).
- In about **1 in 4** market-years storing **did not pay**. The worst result was Mombasa in 2010, where June was KES 781 per bag *below* January.
- **Bad years hit every market at once.** In 2010 and 2018 June prices were below January prices in almost every wholesale market. Spreading sales across markets does not protect a farmer in those years.

How often storing paid off, by market:

| Market | Years compared | June > January | Median gain per bag |
|---|---|---|---|
| Eldoret | 14 | 86% | KES 374 |
| Mombasa | 14 | 79% | KES 346 |
| Nakuru | 5 | 80% | KES 562 |
| Nairobi | 14 | 71% | KES 323 |
| Kisumu | 13 | 54% | KES 329 |

Eldoret, in the main maize-growing region, had the most reliable seasonal rise. In Kisumu storing paid off only about half the time.

### 5. Prices differ between markets
Box plots and violin plots of wholesale maize prices by market show that each market has its own price level and spread:

| Market | Median price per bag | Range |
|---|---|---|
| Kisumu | KES 3,082 (highest) | 1,214 – 5,200 |
| Nairobi | KES 2,690 | 1,069 – 4,816 |
| Mombasa | KES 2,586 | 1,035 – 4,898 |
| Nakuru | KES 2,500 | 1,120 – 4,000 (2015–2019 only) |
| Eldoret | KES 2,472 (lowest) | 944 – 4,456 |

Eldoret, close to where much of Kenya's maize is grown, is usually the cheapest. Kisumu and Nairobi, where more maize is consumed, are usually dearer. Where a farmer sells matters, not just when.

### 6. Households in Lodwar and Mandera pay the most for maize
Average retail maize price per kg, 2015–2019, in the nine county markets:

| Rank | Market (county) | Avg price per kg |
|---|---|---|
| 1 | Lodwar (Turkana) | **KES 75.85 (most expensive)** |
| 2 | Mandera | KES 67.53 |
| 3 | Garissa | KES 59.73 |
| 4 | Kajiado | KES 50.88 |
| 5 | Hola (Tana River) | KES 49.87 |
| 6 | Marsabit | KES 47.50 |
| 7 | Marigat (Baringo) | KES 46.53 |
| 8 | Kilifi | KES 43.84 |
| 9 | Kitui | **KES 36.19 (cheapest)** |

Each market's rank within each year (1 = most expensive):

| Market | 2015 | 2016 | 2017 | 2018 | 2019 |
|---|---|---|---|---|---|
| Lodwar | 1 | 1 | 1 | 1 | 3 |
| Mandera | 2 | 2 | 2 | 2 | 1 |
| Garissa | 3 | 3 | 4 | 3 | 2 |
| Kajiado | 5 | 5 | 3 | 5 | 5 |
| Hola | 7 | 4 | 5 | 4 | 4 |
| Marsabit | 4 | 6 | 8 | 6 | 7 |
| Marigat | 6 | 7 | 6 | 8 | 6 |
| Kilifi | 8 | 8 | 7 | 7 | 8 |
| Kitui | 9 | 9 | 9 | 9 | 9 |

- **Lodwar and Mandera were in the top three every single year.** Garissa came close but dropped to 4th in 2017.
- **Kitui was the cheapest every year.** Households in Lodwar paid about **twice** what households in Kitui paid.
- The most expensive markets are remote and arid, far from the maize-growing areas, so transport costs and isolation push prices up.

---

## Assumptions and limitations

- **Prices are nominal.** They are not adjusted for inflation, so part of the long-term rise reflects general inflation, not higher real value.
- **Wholesale market prices are not farm-gate prices.** Farmers usually sell to brokers or traders for less than the wholesale market price, and pay to transport their maize to market.
- **The storage calculation ignores costs and risks**, including:
  - storage pests (weevils, the larger grain borer) and moisture/mould, especially **aflatoxin**, which can make maize unsellable;
  - weight loss while stored;
  - storage bags, chemicals, hermetic bags or silos, and space;
  - the **cost of waiting**: the farmer needs cash for school fees, debts, inputs and food in the meantime, and may have to borrow at interest;
  - theft;
  - price risk from government actions (NCPB buying prices, import duty waivers, imports from Uganda/Tanzania) and weather shocks.
- **January and June are fixed points.** Harvest timing varies by region (the long-rains harvest in the Rift Valley is around Oct–Dec), and a farmer may do better selling in a different month.
- **One price per month.** Each record is a mid-month (15th) observation, so price movements within a month are not captured.
- **Limited coverage.** Wholesale maize data covers only five large urban markets, and Nakuru only from 2015. Prices in rural markets may behave differently.
- **Retail and wholesale come from different markets**, so the retail-vs-wholesale gap mixes trader margin with location differences.
- **Hola** market's county/region was filled in from geographic knowledge (Tana River, Coast), not from the dataset itself.

---

## Recommendations for farmers

1. **Avoid selling everything right after harvest.** Prices are usually at their lowest then. If you can, keep part of your harvest and sell it in the lean season (April–July), when prices have historically been about 20% higher.
2. **Store only what you can afford to wait on.** Storing paid off about 3 years out of 4, but lost money in the rest. Sell enough at harvest to cover urgent needs, and store the rest, so a bad year does not hurt you badly.
3. **Store maize well, or the gain disappears.** The median gain is only about KES 356 per bag. Dry maize properly (to about 13% moisture), use **hermetic (airtight) bags** or treated storage, and check it often for pests and mould. A few damaged bags can wipe out the extra profit.
4. **Work out your own costs before deciding.** Compare the expected gain (a few hundred shillings per bag) with storage costs, losses and any interest on money borrowed while you wait. If storage costs more than about KES 350 per bag, holding is unlikely to pay.
5. **Join a group or warehouse receipt system.** Farmer groups, cooperatives and certified warehouses (the Warehouse Receipt System) offer cheaper, safer storage. Some let you get credit against the stored maize, so you don't have to sell early for cash.
6. **Follow market prices before you sell.** Prices differ between markets and from year to year. Check current prices (e.g. from the Ministry of Agriculture, NCPB, or SMS/mobile price services) and compare nearby markets before agreeing to a price with a broker.
7. **Be careful after a very high-price year.** In this data big rises were often followed by big falls (2017 → 2018). Don't assume a high price will last, and avoid holding too long when a large harvest is expected.
8. **Consider selling closer to the consumer.** Retail maize sells for about KES 19 more per kg than wholesale. Farmers who can sell in smaller quantities, or as a group directly to local buyers, schools or millers, may capture more of that margin.

---

## Advice for county officers

- **Focus food-price support on Turkana and Mandera.** Lodwar and Mandera were among the three most expensive retail maize markets every year from 2015 to 2019, and Lodwar's prices were about twice Kitui's. Better roads and transport, market links with surplus areas such as Eldoret, and food assistance in the lean season (April–July) would do the most good there.

---

## Answers to the guiding questions

| Question | Answer |
|---|---|
| Which units appear for wholesale and retail maize? | Wholesale: 90 KG bag. Retail: KG. |
| How does retail price per kg compare with wholesale? | Retail KES 47.92 vs wholesale KES 28.54 per kg, about KES 19 (68%) more. |
| Which year had the highest average wholesale price? | 2017 (KES 3,744 per bag). |
| Biggest rise and biggest fall vs the year before? | Rise: 2011 (+KES 1,246). Fall: 2018 (−KES 1,335). |
| Cheapest and dearest month? | Cheapest: January (KES 2,330). Dearest: June (KES 2,839). |
| Share of market-years where June > January, and median gain? | 73.3% (44 of 60). Median gain KES 356 per bag. |
| What costs and risks does the storage calculation leave out? | Pests, mould and aflatoxin, weight loss, bag/storage costs, the cost of waiting for cash, theft, policy and price risk, and the gap between market and farm-gate prices (see *Assumptions and limitations*). |
| Most and least expensive retail market, 2015–2019? | Most expensive: Lodwar (KES 75.85/kg). Cheapest: Kitui (KES 36.19/kg). |
| Markets in the top three every year? | Lodwar and Mandera. |

---

## How to run

```bash
uv sync
```
Then open `analysis.ipynb` in VS Code, select the `.venv` kernel, and click **Run All**.

---

## Project structure

```
Kenya_Market_Prices/
├── analysis.ipynb          # All cleaning, analysis and charts
├── data/
│   └── food-prices-kenya.csv
├── PAMOJA_NOTE.md          # One-page note with advice for Pamoja
├── pyproject.toml
└── README.md
```

---

## Data credit

Price data: **World Food Programme (WFP)**, Kenya food prices dataset, published on the **Humanitarian Data Exchange (HDX)**, https://data.humdata.org/.